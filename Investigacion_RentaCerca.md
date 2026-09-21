# Investigación técnica para el desarrollo de RentaCerca

**Plataforma web para encontrar y publicar casas, departamentos y habitaciones**

## 1. Introducción

RentaCerca es una propuesta de plataforma web enfocada en facilitar la búsqueda y publicación de viviendas. La idea consiste en reunir en un solo lugar casas, departamentos y habitaciones disponibles para renta, permitiendo que las personas puedan buscar propiedades de acuerdo con su presupuesto, ubicación, distancia respecto a un punto de interés y características del inmueble.

El proyecto puede desarrollarse como una aplicación web utilizando tecnologías modernas para frontend, backend, base de datos y servicios de mapas. Una de las partes más importantes será la búsqueda geográfica, ya que el usuario podrá indicar una ubicación y un radio para encontrar propiedades cercanas.

## 2. Objetivo técnico

El objetivo técnico es construir una aplicación web funcional que permita:

- Registrar e iniciar sesión de usuarios.
- Publicar propiedades.
- Agregar fotografías y características de las propiedades.
- Buscar propiedades por ubicación.
- Definir un radio de búsqueda.
- Filtrar por precio y tipo de inmueble.
- Mostrar propiedades en un mapa.
- Mostrar las propiedades mediante tarjetas.
- Utilizar una interfaz de desplazamiento similar a Tinder.
- Guardar propiedades como favoritas.
- Contactar al propietario.
- Administrar las publicaciones realizadas por cada usuario.

La primera versión debe concentrarse en las funciones necesarias para demostrar que el concepto funciona, dejando para etapas posteriores las funciones más complejas.

## 3. Arquitectura propuesta

Se propone una arquitectura dividida en frontend, backend, base de datos y servicios externos.

### 3.1 Frontend: React

El frontend puede desarrollarse con **React**, ya que permite construir interfaces mediante componentes reutilizables.

Algunos componentes podrían ser:

- Inicio de sesión.
- Registro.
- Barra de búsqueda.
- Filtros.
- Tarjeta de propiedad.
- Vista de mapa.
- Sistema de desplazamiento.
- Favoritos.
- Formulario para publicar propiedades.
- Perfil del usuario.

### 3.2 Backend: FastAPI y Python

El backend puede desarrollarse con **FastAPI**, un framework de Python orientado a la creación de APIs.

El backend será responsable de:

- Autenticación.
- Usuarios.
- Propiedades.
- Favoritos.
- Swipes.
- Contactos.
- Validación de información.
- Consultas a la base de datos.
- Búsquedas por distancia.
- Control de permisos.

FastAPI también proporciona documentación interactiva basada en OpenAPI, lo que facilita probar y documentar los endpoints durante el desarrollo.

### 3.3 Base de datos: PostgreSQL y PostGIS

Se propone utilizar **PostgreSQL** como sistema gestor de base de datos y **PostGIS** para manejar información geográfica.

PostGIS permite almacenar coordenadas y realizar consultas espaciales. Esto es importante porque RentaCerca necesita encontrar propiedades que estén dentro de una determinada distancia.

Por ejemplo:

> Buscar departamentos a menos de 3 kilómetros de una universidad.

### 3.4 Mapas: Google Maps Platform

Para la visualización del mapa se puede utilizar **Google Maps JavaScript API**.

El mapa podría utilizarse para:

- Mostrar la ubicación de las propiedades.
- Colocar marcadores.
- Mostrar información al seleccionar una propiedad.
- Permitir seleccionar una ubicación.
- Mostrar un círculo correspondiente al radio de búsqueda.

Es importante diferenciar dos funciones:

- **Google Maps:** principalmente para la visualización y herramientas relacionadas con mapas.
- **PostGIS:** para realizar la búsqueda geográfica dentro de la base de datos.

## 4. Funcionamiento general

1. El usuario entra a RentaCerca.
2. Selecciona o escribe una ubicación de interés.
3. Define un radio de búsqueda.
4. Selecciona un presupuesto.
5. Selecciona filtros adicionales.
6. El frontend envía los parámetros al backend.
7. El backend consulta PostgreSQL/PostGIS.
8. PostGIS encuentra las propiedades que cumplen con la distancia solicitada.
9. El backend devuelve las propiedades encontradas.
10. React muestra las propiedades en tarjetas y/o en el mapa.
11. El usuario puede revisar una propiedad.
12. Puede marcarla como favorita o descartarla.
13. Si es de su interés, puede consultar sus datos de contacto.

Para los propietarios:

1. Registrar una cuenta.
2. Entrar al formulario para publicar.
3. Capturar los datos del inmueble.
4. Agregar fotografías.
5. Indicar la ubicación.
6. Publicar la propiedad.
7. Administrar o editar la publicación posteriormente.

## 5. Mapa y geolocalización

La ubicación será una parte fundamental de RentaCerca.

Cada propiedad debería contar con coordenadas de latitud y longitud. Estas coordenadas permiten representar la propiedad en un mapa y realizar búsquedas por distancia.

Una propiedad no necesariamente debe mostrar su ubicación exacta públicamente. Para aumentar la privacidad, se puede mostrar únicamente una zona aproximada hasta que el usuario tenga una interacción más avanzada con el propietario.

El usuario podría seleccionar radios como:

- 1 km
- 2 km
- 3 km
- 5 km
- 10 km

También se podría permitir introducir un valor personalizado.

## 6. Búsqueda por radio con PostGIS

Una de las funciones más importantes será la búsqueda de propiedades cercanas.

PostGIS cuenta con la función `ST_DWithin`, que permite comprobar si dos ubicaciones se encuentran dentro de una distancia determinada.

Ejemplo:

```sql
SELECT id, titulo, precio, tipo_inmueble, habitaciones
FROM propiedades
WHERE estado = 'ACTIVA'
  AND precio BETWEEN :precio_min AND :precio_max
  AND ST_DWithin(
      ubicacion,
      ST_SetSRID(
          ST_MakePoint(:longitud, :latitud),
          4326
      )::geography,
      :radio_metros
  );
```

En este ejemplo:

- `ubicacion` representa la ubicación de la propiedad.
- `:latitud` representa la latitud del punto seleccionado.
- `:longitud` representa la longitud.
- `:radio_metros` representa el radio de búsqueda.
- `precio_min` y `precio_max` representan el presupuesto.
- `estado = 'ACTIVA'` evita mostrar publicaciones que ya no estén disponibles.

El uso de `geography` permite trabajar con distancias en metros. PostGIS también puede utilizar índices espaciales para mejorar el rendimiento.

## 7. Diseño propuesto de la base de datos

### usuarios

```text
id
nombre
correo
password_hash
telefono
tipo_usuario
fecha_registro
```

### propiedades

```text
id
usuario_id
titulo
descripcion
tipo_inmueble
precio
habitaciones
banos
amueblado
ubicacion
direccion_aproximada
estado
fecha_publicacion
```

### fotos_propiedad

```text
id
propiedad_id
url
orden
```

### servicios

```text
id
nombre
```

Ejemplos: Internet, estacionamiento, agua, luz, gas, amueblado, lavadora y mascotas permitidas.

### propiedad_servicio

Tabla intermedia para relacionar propiedades con servicios.

```text
propiedad_id
servicio_id
```

### favoritos

```text
id
usuario_id
propiedad_id
fecha
```

### swipes

```text
id
usuario_id
propiedad_id
accion
fecha
```

### contactos

```text
id
usuario_id
propiedad_id
fecha
mensaje
```

## 8. Información que debería tener una propiedad

Cada publicación debería contener:

- Título.
- Descripción.
- Precio.
- Tipo de inmueble.
- Número de habitaciones.
- Número de baños.
- Si está amueblado.
- Servicios incluidos.
- Fotografías.
- Ubicación.
- Zona o dirección aproximada.
- Información de contacto.
- Estado de la publicación.

Posteriormente se podrían agregar depósito, requisitos, disponibilidad, reglas de vivienda, mascotas, estacionamiento y distancia a universidades o transporte público.

## 9. Interfaz similar a Tinder

Una característica diferenciadora de RentaCerca puede ser una interfaz basada en tarjetas.

El usuario podría desplazarse entre propiedades:

- Desplazamiento a la derecha: mostrar interés.
- Desplazamiento a la izquierda: descartar.
- Botón de información: abrir los detalles.
- Botón de favorito: guardar la propiedad.

Ejemplo:

```text
[Fotografía]

$6,500 / mes
Departamento
2 habitaciones
1 baño

A 1.8 km de tu ubicación

[Ver detalles]
```

Esta interacción puede implementarse en React mediante componentes que controlen los gestos y el estado de cada tarjeta.

## 10. API propuesta

### Autenticación

```text
POST /auth/register
POST /auth/login
```

### Propiedades

```text
GET    /properties
GET    /properties/{id}
POST   /properties
PUT    /properties/{id}
DELETE /properties/{id}
```

### Favoritos

```text
POST   /properties/{id}/favorite
DELETE /properties/{id}/favorite
GET    /favorites
```

### Swipes

```text
POST /properties/{id}/swipe
```

### Contactos

```text
POST /properties/{id}/contact
```

Parámetros de búsqueda:

```text
latitud
longitud
radio
precio_min
precio_max
tipo_inmueble
habitaciones
banos
amueblado
servicios
```

## 11. Manejo de fotografías

Se recomienda no guardar directamente archivos grandes dentro de PostgreSQL. Una alternativa es utilizar almacenamiento de archivos y guardar en la base de datos solamente la URL o referencia del archivo.

Flujo:

```text
Usuario
   ↓
Frontend
   ↓
Backend
   ↓
Almacenamiento de imágenes
   ↓
URL de la fotografía
   ↓
Base de datos
```

También sería conveniente establecer tamaño máximo, tipos de archivo permitidos, cantidad máxima de fotografías y compresión o redimensionamiento.

## 12. Seguridad y privacidad

RentaCerca manejará información de usuarios y propietarios, por lo que se deben implementar medidas básicas:

- Contraseñas almacenadas mediante hash seguro.
- Autenticación para operaciones privadas.
- Permisos para que cada usuario pueda modificar solamente sus publicaciones.
- Variables de entorno para claves y contraseñas.
- Límites y validación para fotografías.
- Ubicación aproximada en la vista pública cuando sea necesario.

## 13. Google Maps y costos

Google Maps Platform puede utilizarse para integrar mapas y servicios relacionados.

Antes de utilizarlo en producción se deben revisar los precios y condiciones vigentes, porque los costos dependen del uso. Google Maps Platform ofrece planes y contempla crédito de prueba para nuevos clientes, pero los precios y condiciones pueden cambiar.

Durante el desarrollo académico se recomienda:

- Utilizar las APIs únicamente cuando sean necesarias.
- Restringir las claves de API.
- Configurar límites de uso.
- Revisar el consumo.
- Evitar consultas innecesarias.

### Alternativa: OpenStreetMap

También existe la posibilidad de utilizar datos de OpenStreetMap. Sin embargo, el servidor público de Nominatim no debe considerarse un servicio ilimitado: su política establece límites de uso y condiciones específicas.

## 14. Despliegue

Una posible estructura:

```text
                    INTERNET
                        |
                        v
                 FRONTEND REACT
                        |
                        v
                  API FASTAPI
                        |
             +----------+----------+
             |                     |
             v                     v
       POSTGRESQL + POSTGIS   ALMACENAMIENTO
             |                 DE IMÁGENES
             |
             v
        DATOS DEL SISTEMA
```

Estructura inicial del proyecto:

```text
rentacerca/
├── frontend/
├── backend/
├── database/
├── docker-compose.yml
├── .env
└── README.md
```

## 15. Organización del desarrollo

### Fase 1: Requisitos

Definir usuarios, funciones, reglas, filtros e información de propiedades.

### Fase 2: Base de datos

Crear PostgreSQL, PostGIS, tablas, relaciones e índices.

### Fase 3: Backend

Implementar registro, login, propiedades, favoritos, swipes y contactos.

### Fase 4: Búsqueda

Implementar precio, tipo, habitaciones, servicios, ubicación y radio.

### Fase 5: Frontend

Crear inicio, login, registro, búsqueda, tarjetas, detalles, favoritos y publicación.

### Fase 6: Mapas

Integrar mapa, marcadores y selección de ubicación.

### Fase 7: Interacción

Agregar swipe, favoritos e historial de propiedades descartadas.

### Fase 8: Publicaciones

Implementar fotografías, edición, eliminación y estado de publicación.

### Fase 9: Contacto

Implementar una forma básica de comunicación con el propietario.

### Fase 10: Pruebas

Realizar pruebas de login, registro, publicación, búsqueda, filtros, radio, mapa, favoritos, swipe y permisos.

### Fase 11: Despliegue

Configurar variables de entorno, base de datos, frontend, backend y seguridad.

## 16. Historias de usuario

### Usuario que busca vivienda

> Como estudiante, quiero indicar mi universidad y un radio de búsqueda para encontrar viviendas cercanas.

### Filtrar por presupuesto

> Como usuario, quiero indicar un precio mínimo y máximo para encontrar propiedades que estén dentro de mi presupuesto.

### Ver propiedades

> Como usuario, quiero ver fotografías y características de una propiedad para decidir si me interesa.

### Guardar propiedad

> Como usuario, quiero guardar una propiedad como favorita para revisarla posteriormente.

### Publicar propiedad

> Como propietario, quiero publicar mi inmueble para que otras personas puedan encontrarlo.

### Administrar publicación

> Como propietario, quiero editar o desactivar mi publicación cuando la propiedad ya no esté disponible.

## 17. Pruebas funcionales propuestas

- **Búsqueda de 1 km:** comprobar que solamente aparezcan propiedades dentro del radio.
- **Búsqueda de 5 km:** comprobar que aparezcan propiedades adicionales dentro de la nueva distancia.
- **Filtro de precio:** comprobar que no aparezcan propiedades fuera del rango.
- **Filtros combinados:** probar radio, precio, tipo y habitaciones simultáneamente.
- **Publicación:** crear una propiedad y comprobar que aparezca en búsquedas.
- **Edición:** modificar precio o descripción y comprobar los cambios.
- **Favoritos:** guardar una propiedad y comprobar que aparezca en favoritos.
- **Swipe:** comprobar que las acciones de interés y descarte se almacenen.
- **Mapa:** comprobar que los marcadores correspondan a las propiedades.
- **Seguridad:** comprobar que un usuario no pueda modificar una publicación de otro usuario.

## 18. Riesgos y soluciones

### Costos de APIs

**Riesgo:** un uso elevado de servicios de mapas puede generar costos.

**Solución:** controlar el consumo, restringir las claves y revisar periódicamente el uso.

### Propiedades falsas

**Riesgo:** usuarios podrían publicar información falsa.

**Solución:** incorporar reportes, moderación y posteriormente mecanismos de verificación.

### Privacidad

**Riesgo:** mostrar la ubicación exacta de una vivienda puede representar un problema.

**Solución:** mostrar inicialmente una zona aproximada.

### Imágenes demasiado grandes

**Riesgo:** fotografías pesadas pueden hacer lenta la aplicación.

**Solución:** limitar tamaño y dimensiones y comprimir imágenes.

### Consultas espaciales lentas

**Riesgo:** una gran cantidad de propiedades puede hacer más lentas las búsquedas.

**Solución:** utilizar índices espaciales de PostGIS y optimizar consultas.

### Exceso de marcadores

**Riesgo:** demasiados marcadores pueden dificultar la navegación.

**Solución:** utilizar agrupación de marcadores y limitar resultados.

## 19. Primer prototipo funcional

Para la primera versión se recomienda implementar:

- Registro.
- Login.
- Publicación de propiedades.
- Fotografías.
- Búsqueda por presupuesto.
- Búsqueda por tipo.
- Ubicación.
- Radio de búsqueda.
- PostgreSQL.
- PostGIS.
- Mapa.
- Marcadores.
- Swipe.
- Favoritos.
- Contacto básico.

Inicialmente se pueden dejar fuera:

- Pagos.
- Contratos.
- Trámites legales.
- Hipotecas.
- Seguros.
- Verificación física de inmuebles.
- Tours virtuales.
- Aplicación móvil nativa.
- Sistema avanzado de recomendaciones.

Esto permite construir un producto mínimo viable y agregar nuevas funciones posteriormente.

## 20. Conclusión

RentaCerca es técnicamente viable como una aplicación web.

Una arquitectura basada en **React + FastAPI + PostgreSQL/PostGIS** permite separar la interfaz, la lógica del sistema y la información de las propiedades.

El uso de **PostGIS** es especialmente importante porque permite realizar búsquedas por distancia directamente en la base de datos. Esto hace posible implementar una función central del proyecto: encontrar viviendas dentro de un radio determinado.

Un servicio de mapas como **Google Maps Platform** puede utilizarse para visualizar las propiedades y facilitar la selección de ubicaciones.

No es necesario utilizar inteligencia artificial para construir la primera versión. Las funciones principales pueden resolverse mediante reglas, filtros, consultas espaciales y una interfaz de usuario bien estructurada.

## 21. Fuentes consultadas

- Google Maps JavaScript API: https://developers.google.com/maps/documentation/javascript
- Google Maps Platform — Precios: https://mapsplatform.google.com/intl/es-419_mx/pricing/
- Google Maps Platform — Billing and Pricing: https://developers.google.com/maps/billing-and-pricing/overview
- PostGIS — `ST_DWithin`: https://postgis.net/docs/ST_DWithin.html
- PostGIS — Radius queries: https://postgis.net/documentation/tips/st-dwithin/
- PostGIS — Introducción: https://postgis.net/docs/manual-3.7/en/postgis_introduction.html
- FastAPI: https://fastapi.tiangolo.com/
- FastAPI — Features: https://fastapi.tiangolo.com/features/
- React: https://react.dev/
- PostgreSQL — JSON/JSONB: https://www.postgresql.org/docs/16/datatype-json.html
- OpenStreetMap — Nominatim Usage Policy: https://operations.osmfoundation.org/policies/nominatim/
