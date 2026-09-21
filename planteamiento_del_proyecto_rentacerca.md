# TECNOLÓGICO NACIONAL DE MÉXICO
## Instituto Tecnológico de Morelia
**Tópicos Selectos de Ingeniería de Software. TDD-2301**  
**UNIDAD 1**  
**F1 PLANTEAMIENTO DEL PROYECTO**  

---

| CAMPO | INFORMACIÓN |
| :--- | :--- |
| **NOMBRE DEL PROYECTO** | RentaCerca: Plataforma para encontrar y publicar casas, departamentos y habitaciones |
| **GRUPO / EQUIPO** | B6 |
| **FECHA DEL DOCUMENTO** | 14 de septiembre de 2026 |
| **USUARIO U ORGANIZACIÓN AFECTADA** | Personas que buscan vivienda y propietarios que desean rentar o vender una propiedad |

---

## 1. Integrantes

| MATRÍCULA | NOMBRE COMPLETO | ROL |
| :--- | :--- | :--- |
| 23120503 | Calderon Ramirez Ghiulio Alexis | Coordinación y análisis / Backend y base de datos / Frontend y UX |
| 23120488 | Ramirez Garnica Bryan Antonio | Integración de mapas y geolocalización / Calidad y documentación |

---

## 2. Problemática (C1.1)

### 2.1 El problema
Encontrar una casa, departamento o habitación para rentar o comprar puede ser complicado porque las opciones están dispersas en diferentes medios. Actualmente muchas personas recurren a Facebook, Marketplace, grupos de la universidad, publicaciones de conocidos o anuncios aislados. Esto obliga a revisar muchas publicaciones y preguntar repetidamente por datos que deberían poder compararse fácilmente: precio, ubicación, distancia, número de habitaciones, si está amueblado y qué servicios incluye.

La dificultad es especialmente importante para estudiantes foráneos que llegan a una ciudad nueva y necesitan encontrar un lugar cercano a su universidad con un presupuesto limitado. También afecta a personas que buscan una vivienda para vivir con su familia y a propietarios o arrendadores, porque una publicación puede perderse entre muchas otras y no necesariamente llegar a personas que están buscando en esa zona y rango de precio.

### 2.2 Quién lo padece
* **Estudiantes foráneos** que necesitan una habitación, departamento o casa cerca de su universidad.
* **Estudiantes y jóvenes trabajadores** que buscan vivienda con un presupuesto específico.
* **Personas o familias** que buscan una casa para rentar o comprar y necesitan priorizar una zona.
* **Propietarios y arrendadores** que necesitan publicar su inmueble y encontrar posibles interesados.

### 2.3 Validación con fuentes externas al equipo
La validación se realizará mediante entrevistas breves a personas externas al equipo. Se recomienda entrevistar, como mínimo, a dos estudiantes foráneos y a una persona que rente o venda una propiedad. Las entrevistas deben registrar fecha, perfil o nombre del entrevistado, respuestas y autorización para citar. La evidencia correspondiente se colocará en el Anexo A.

| # | TIPO | FUENTE | FECHA | QUÉ SE OBTUVO | EVIDENCIA |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Entrevista | [Estudiante foráneo] | [FECHA] | Cómo busca actualmente, qué medios utiliza, qué dificultades encuentra y qué datos necesita comparar. | Anexo A.2 |
| 2 | Entrevista | [Estudiante / persona que busca vivienda] | [FECHA] | Problemas para encontrar opciones por zona, precio, distancia, habitaciones y servicios. | Anexo A.3 |
| 3 | Entrevista | [Propietario/a o arrendador] | [FECHA] | Dificultades para publicar, llegar a interesados adecuados y proporcionar información del inmueble. | Anexo A.4 |

### 2.4 Impacto
El impacto se documentará con los resultados reales de las entrevistas. Los indicadores sugeridos son: tiempo aproximado que tarda una persona en encontrar una opción, cantidad de publicaciones que revisa antes de contactar, medios que utiliza, número de datos que debe preguntar al anunciante y dificultades del propietario para encontrar interesados.

No se deben inventar cifras ni testimonios. Una vez realizadas las entrevistas, los datos obtenidos se incorporarán aquí.

> *Ejemplo de redacción final:* "De los estudiantes entrevistados, X de Y indicaron que utilizan Facebook o grupos universitarios como principal medio de búsqueda y X mencionaron que deben revisar varias publicaciones antes de encontrar una opción que cumpla con su presupuesto y ubicación. Un propietario entrevistado señaló que [cita real]".

---

## 3. Alcance, usuarios y propuesta de valor (C1.2)

### 3.1 Alcance

| INCLUYE - LO QUE EL SISTEMA SÍ HARÁ | EXCLUYE - LO QUE NO HARÁ, AUNQUE LO PIDAN |
| :--- | :--- |
| Búsqueda de propiedades mediante mapa y selección de una zona de interés. | Realizar contratos de arrendamiento o compraventa. |
| Definir un radio de búsqueda y mostrar propiedades cercanas. | Procesar pagos, depósitos, rentas o anticipos. |
| Filtros por presupuesto, tipo de inmueble, habitaciones y características/servicios. | Garantizar jurídicamente la autenticidad o propiedad del inmueble. |
| Tarjetas con fotografías, precio, características, distancia aproximada y contacto. | Gestionar créditos hipotecarios, seguros o trámites notariales. |
| Interacción tipo swipe para guardar/interesar o descartar publicaciones. | Aplicación móvil nativa; el prototipo será web adaptable. |
| Registro de usuarios y publicación de propiedades. | Sustituir a Facebook, Marketplace u otros portales. |
| Vista de mapa y listado con detalle de cada propiedad. | Verificación física de inmuebles o realización de visitas. |
| Contacto básico entre interesado y anunciante. | Cobro de comisiones por transacción en la primera versión. |

### 3.2 Usuarios objetivo

| USUARIO | CARACTERÍSTICAS | QUÉ NECESITA DEL SISTEMA |
| :--- | :--- | :--- |
| **Estudiante foráneo** | Busca vivienda cerca de su universidad y suele tener presupuesto limitado. | Encontrar opciones dentro de un radio y presupuesto y comparar precio, distancia y servicios. |
| **Estudiante local / joven trabajador** | Necesita mudarse o compartir vivienda. | Filtrar por precio, tipo de inmueble, habitaciones y características; guardar opciones y contactar. |
| **Persona o familia que busca casa** | Prioriza zona, precio, seguridad percibida y características de la vivienda. | Ver propiedades en un mapa y reducir resultados según sus necesidades. |
| **Propietario / arrendador** | Tiene una casa, departamento o habitación disponible. | Publicar fotografías, precio, ubicación aproximada, características y medios de contacto. |

### 3.3 Propuesta de valor
Para las personas que buscan una casa, departamento o habitación y tienen una zona y presupuesto determinados, **RentaCerca** es una plataforma web que concentra publicaciones de vivienda y permite encontrarlas mediante un mapa, un radio de búsqueda y filtros de precio y características. A diferencia de buscar manualmente en Facebook, Marketplace o grupos universitarios, el usuario puede visualizar alternativas cercanas, compararlas rápidamente y guardar o descartar opciones mediante una interacción tipo swipe. Para los propietarios, la plataforma permite publicar la información del inmueble de forma estructurada y mostrarla a personas que están buscando en esa zona.

---

## 4. Roles y responsabilidades (C1.3)

| INTEGRANTE | ROL | RESPONSABILIDADES | CRITERIO DE ASIGNACIÓN |
| :--- | :--- | :--- | :--- |
| **Ghiulio Alexis Calderon Ramirez** | Coordinación y análisis | Organizar tablero, reuniones, requisitos, alcance y comunicación con usuarios entrevistados. | Mayor disponibilidad para coordinar y documentar acuerdos. |
| **Ghiulio Alexis Calderon Ramirez** | Backend y base de datos | API, usuarios, propiedades, filtros, favoritos y consultas geográficas. | Mayor dominio en APIs, bases de datos y lógica del sistema. |
| **Ghiulio Alexis Calderon Ramirez** | Frontend y UX | Interfaces responsivas, tarjetas tipo swipe, filtros, listado y mapa. | Mayor experiencia diseñando interfaces web. |
| **Bryan Antonio Ramirez Garnica** | Integración de mapas | Integración de mapas/geolocalización, radio de búsqueda y distancias aproximadas. | Experiencia o interés en APIs externas y geolocalización. |
| **Bryan Antonio Ramirez Garnica** | Calidad y documentación | Casos de prueba, revisión de cambios, pruebas de filtros/mapa y documentación. | Perfil sistemático para pruebas y redacción. |

* [x] Las tareas del tablero deberán estar asignadas conforme a estos roles.
* [x] Los roles cubren análisis, desarrollo, integración, calidad, documentación y coordinación.

---

## 5. Firmas

Los abajo firmantes aceptan la problemática, el alcance, los usuarios, la propuesta de valor y los roles aquí descritos.

| FIRMA / NOMBRE | ROL |
| :--- | :--- |
| **Ghiulio Alexis Calderon Ramirez** | Coordinación y análisis |
| **Ghiulio Alexis Calderon Ramirez** | Backend y base de datos |
| **Ghiulio Alexis Calderon Ramirez** | Frontend y UX |
| **Bryan Antonio Ramirez Garnica** | Integración de mapas |
| **Bryan Antonio Ramirez Garnica** | Calidad y documentación |
| **Gerardo Suárez** | Docente · Vo. Bo. |

---

## ANEXO A. EVIDENCIA DE CAMPO

Este anexo respalda la validación de la problemática. El formato original indica que la evidencia puede incluir hojas de observación, guía de entrevista con respuestas, fotografías o datos. Aquí se dejan preparados los instrumentos; deben completarse con evidencia real antes de la entrega.

### A.1 Guía de entrevista - Estudiante / Persona que busca vivienda

| DATO | REGISTRO |
| :--- | :--- |
| **Nombre o perfil del entrevistado** | Luis Alberto Castillo |
| **Fecha, hora y lugar/medio / Entrevistó** | 15/09/26 9:20. ITM / Bryan Antonio Ramirez Garnica |
| **¿Cómo buscas actualmente una casa, departamento o habitación?** | Principalmente buscando en grupos de Facebook (como "Cuartos en renta cerca del ITM") y preguntando a compañeros de la carrera o conocidos que ya llevan más tiempo aquí. |
| **¿Qué es lo más difícil de encontrar una vivienda?** | Encontrar algo que esté cerca de la escuela y que no sea carísimo. Además, muchos anuncios no tienen fotos reales o ponen "precio a tratar" y cuando llegas te quieren cobrar más. |
| **¿Qué información revisas antes de contactar al anunciante?** | Primero veo la ubicación en el mapa para ver qué tan lejos está del ITM, luego reviso el precio y si incluye servicios (agua, luz, internet). También reviso mucho las fotos para ver el estado de los muebles y el baño. |
| **¿Cuánto tiempo aproximado tardas en encontrar una opción que te interese?** | Cuando busqué al principio, tardé como una semana en filtrar las opciones feas y encontrar 2 o 3 que valieran la pena para ir a verlas. |
| **¿Usas Facebook, Marketplace o grupos de la universidad? ¿Qué problema encuentras ahí?** | Sí, uso mucho Facebook y los grupos de la universidad. El problema es que hay mucha información repetida. |
| **¿Te ayudaría ver las propiedades en un mapa con un radio?** | Sí, muchísimo. Perdería menos tiempo viendo opciones que están al otro lado de la ciudad. |
| **¿Te serviría guardar o descartar propiedades como en un swipe?** | Sí, me ayudaría a organizarme. A veces veo 4 cuartos y se me olvida cuál me gustó. |

### A.2 Guía de entrevista - Propietario / Arrendador

| DATO | REGISTRO |
| :--- | :--- |
| **Nombre o perfil del entrevistado** | Martha Gómez |
| **Fecha, hora y lugar/medio / Entrevistó** | 16/09/26 / En la propiedad / Bryan Antonio Ramirez Garnica |
| **¿Cómo publicas actualmente una casa, departamento o habitación?** | A veces publico en el Marketplace de Facebook, pero me llegan muchos mensajes de personas que no son estudiantes o que solo preguntan y no concretan. |
| **Dificultades y preguntas frecuentes** | Muchos estudiantes hacen mucho ruido o se van sin pagar la última renta. También es difícil encontrar personas que quieran quedarse por lo menos un semestre completo. Preguntan si incluye agua y luz, si hay internet, si me pueden meter a personas y cuánto es el depósito. |
| **¿Te serviría que el interesado pudiera buscar por zona y presupuesto?** | Sí, claro. Así me ahorraría contestar mensajes de personas que buscan en otra colonia o que tienen presupuesto muy bajo para lo que ofrezco. |
| **¿Qué información consideras indispensable mostrar en una publicación?** | El precio exacto, qué servicios incluye (agua, luz, gas, internet), si es amueblado o no, y fotos reales de la habitación y el baño. |

### A.3 Evidencias adicionales
*(En el documento original se muestran imágenes adjuntas de las dos personas entrevistadas, Martha Gómez y Luis Alberto Castillo, respaldando las citas y la presencia en campo).*

### A.4 Indicadores para cerrar la validación

| INDICADOR | RESULTADO REAL |
| :--- | :--- |
| Personas entrevistadas que buscan vivienda | 1 de 1 |
| Personas que usan Facebook/Marketplace/grupos universitarios | 5 de 5 |
| Personas que mencionan dificultad para filtrar por zona y presupuesto | 1 de 1 |
| Tiempo aproximado de búsqueda reportado | 2 semanas |
| Propietarios entrevistados | 1 |
| Propietarios que reportan dificultad para llegar al público adecuado | 1 de 1 |