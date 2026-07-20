# Diseño conceptual y lógico de una base de datos para una aplicación de transporte urbano (inDrive)

## Introducción
En este proyecto se diseñará un sistema de base de datos conceptual y relacional para dar
soporte a las operaciones principales de una plataforma digital de transporte urbano basada en
el modelo de negociación de tarifas en tiempo real. La aplicación tomada es inDrive, una
plataforma de movilidad que permite la interacción directa entre pasajeros y conductores para
acordar el valor de cada viaje.

El sistema propuesto permitirá almacenar de manera persistente la información relacionada con
pasajeros, conductores, vehículos, solicitudes de viaje, viajes realizados, ubicaciones, pagos,
métodos de pago, calificaciones, lugares guardados y reclamos. Esta información será
organizada mediante un modelo conceptual y relacional que facilite la integridad, consistencia,
consulta y administración de los datos generados durante el uso de la aplicación.

El propósito principal del diseño de la base de datos es garantizar que la plataforma pueda
registrar correctamente el ciclo completo de una carrera: desde la solicitud inicial realizada por
el pasajero, pasando por la negociación de tarifas con los conductores disponibles, hasta la
aceptación de una oferta, ejecución del viaje, registro del pago, calificación del viaje, incorporación
del viaje al historial del usuario y registro de reclamos si aplica al caso.

inDrive, originalmente conocida como inDriver y fundada en 2013, es una plataforma
internacional de movilidad y servicios urbanos basada en un modelo de negociación P2P, es
decir, de persona a persona. En este modelo, la tarifa no es impuesta únicamente por un
algoritmo; por el contrario, el pasajero propone un precio inicial por la carrera y los conductores
cercanos pueden aceptar la oferta, ignorarla o enviar una contraoferta. De esta manera, el
pasajero selecciona al conductor que considere más conveniente tomando en cuenta factores
como la tarifa ofertada, el tiempo estimado de llegada del conductor, la calificación del
conductor y las características del vehículo.

## Metodología
Para el desarrollo de este proyecto, se aplicó una metodología estrucuturada de diseño de bases de datos relacionales, dividida en las siguientes fases:

* **Análisis de Requerimientos Funcionales del sistema y Reglas de Negocio**

Se analizó la dinámica e interacciones entre los usuarios o el modelo funcional de inDrive, el cual se basa en la negociación P2P (persona a persona), para establecer los requerimientos del sistema y los distintos niveles de acceso de los usuarios (Pasajeros y Conductores). Con esta base, se definieron 14 reglas de negocio que determinan las restricciones lógicas y cardinalidades del sistema

* **Identificación de Entidades y Relaciones**

Se extrajeron 10 entidades fundamentales para cubrir el ciclo de vida de una carrera (Pasajero, Conductor, Vehículo, Solicitud de Viaje, Oferta, Viaje, Ubicación, Pago, Calificación y Reclamo), estableciendo las interacciones lógicas entre cada una de ellas.

* **Diseño Conceptual (Modelado E/R)**

Se elaboró inicialmente un Diagrama Entidad-Relación (E/R) simple para visualizar la arquitectura general con los atributos más representativos de cada entidad. Posteriormente, se construyó un Diagrama E/R detallado que incorpora de manera exhaustiva todos los atributros, claves primarias (PK) o atributos identificadores y las posibles atributos candidatos a ser claves foráneas (FK). Para esta etapa se opto por el método o estructura de Chen, guiandonos también por la cardinalidad impuesta por Crow's Foot.

* **Diseño Lógico y Esquema Relacional**

Se realizó la transición del modelo conceptual a un esquema relacional, definiendo la estructura de las tablas (entidades) definitiva y asegurando la integridad referencial de los datos. En este caso se identifican las claves primarias, foráneas y se establecen tablas auxiliares o asociativas como Guarda.

* **Construcción del Diccionario de Datos**

Finalmente, se documentó un diccionario de datos técnico detallando la composición de cada tabla. En este se especificaron los tipos de variables o datos (INT, VARCHAR, DATETIME, ENUM, entre otras.), los rangos admitidos, los formatos específicos y la obligatoriedad de los atributos. De esta manera se entender+a mejor cómo será el esquema de las tablas y cuando ya sea de construir la base de datos y los mecanismos de consulta.

## Resultados
Luego de haber realizado los pasos detallados en la metodología para entender mejor cómo funciona internamente la base de datos de la aplicación de inDrive, se diseñó una arquitectura de base de datos conceptual y lógica, capaz de soportar el ciclo completo de una carrera bajo el modelo de negociación P2P. Se obtuvieron los siguientes resultados:

***Reglas de negocio identificadas***
1. Un pasajero puede crear cero, una o muchas solicitudes de viaje, pero cada solicitud de
viaje debe ser creada por un solo pasajero.
2. Una solicitud de viaje debe registrar una ubicación de origen y una ubicación de destino,
mientras que una misma ubicación puede utilizarse en diferentes solicitudes de viaje.
3. Una solicitud de viaje puede recibir cero, una o muchas ofertas, pero cada oferta debe
corresponder a una sola solicitud de viaje.
4. Un conductor puede realizar cero, una o muchas ofertas, pero cada oferta debe ser
realizada por un solo conductor.
5. Una oferta puede confirmar como máximo un viaje, y cada viaje confirmado debe
originarse a partir de una sola oferta aceptada.
6. Un conductor puede realizar cero, uno o muchos viajes, pero cada viaje debe ser
realizado por un solo conductor. 
7. Un conductor puede registrar uno o varios vehículos, pero cada vehículo debe estar
registrado por un solo conductor.
8. Cada viaje debe utilizar un solo vehículo, mientras que un vehículo puede utilizarse en
cero, uno o muchos viajes a lo largo del tiempo.
9. Un pasajero puede configurar cero, uno o varios métodos de pago, pero cada método
de pago configurado debe pertenecer a un solo pasajero.
10. Un método de pago puede utilizarse en cero, uno o muchos pagos, pero cada pago debe
utilizar un solo método de pago.
11. Un viaje puede generar como máximo un pago, y cada pago debe corresponder a un
solo viaje.
12. Un viaje completado puede recibir cero, una o varias calificaciones, pero cada
calificación debe corresponder a un solo viaje.
13. Las calificaciones pueden ser emitidas por el pasajero hacia el conductor o por el
conductor hacia el pasajero, según el rol del calificador registrado.
14. Un viaje puede recibir de cero a muchos reclamos, pero cada reclamo debe estar
asociado a un viaje.

Los entregables técnicos obtenidos incluyen:
* **Modelo Conceptual:** creación de Diagramas E/R que organizan gráficamente las 10 entidades y sus relaciones.
* **Modelo Lógico:** transformación del modelo conceptual a un esquema relacional estrucutrado, asegurando la integridad referencial de los datos mediante el uso adecuado de las PK y FK.
* **Diccionario:** contrucción de un diccionario de datos que detalla a profundidad la estructura interna de la base de datos.

*Evidencia visual de los entregables del diseño de la base de datos a nivel conceptual y lógico*


<img width="1381" height="832" alt="image" src="https://github.com/user-attachments/assets/3280c4df-075d-4353-afb9-4b4dec0ab1e2" />
<img width="1432" height="922" alt="image" src="https://github.com/user-attachments/assets/a39b0dfa-c5e9-4f06-a579-f772886d147b" />
<img width="1501" height="810" alt="image" src="https://github.com/user-attachments/assets/230e434e-d04d-4f53-9d60-06c1f7889bf0" />
<img width="1677" height="1196" alt="image" src="https://github.com/user-attachments/assets/d67744e0-e2ef-4477-a8e0-5b284ab271b3" />
<img width="1726" height="935" alt="image" src="https://github.com/user-attachments/assets/5ab799ca-75f7-4444-9641-6ea3482add38" />
<img width="1732" height="596" alt="image" src="https://github.com/user-attachments/assets/f302aa92-9e2d-47dd-96b1-6befb963e6dc" />



  

