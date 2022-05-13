# Sesión 5 # Postwork: 

## :dart: Objetivos

- Crear una base de datos y tablas en Mysql.
- Desarrollar la conexión a la base de prueba en los scripts de pruebas automatizados.
- Adaptar los scripts de pruebas para que consuman los datos provenientes de la ejecución de Querys en la Base de datos.


## ⚙ Requisitos

- Software de desarrollo
    - Java Software Development Kit (JDK)
- Editor de código
    - Eclipse IDE
- Entorno de pruebas de software
    - Selenium Java Client
    - Selenium Webdriver
    - Selenium IDE
- Navegador
    - Google Chrome
- Selenium browserdriver
    - Chromium/Chrome
- Base de Datos
    - MySql Server
    - MySql Workbench


## Desarrollo

- Crea una base de datos MySql a través de un Query en MySQL Workbench.
- Crea una o varias tablas según la/s funcionalidades de mercado libre escogida para el desarrollo de tu proyecto.
- Ingresa los registros a las tablas según los datos que requieras para las pruebas de tu funcionalidad. `Pro-Tip`: puedes agregar una tabla `general` que contenga información para tus pruebas y que no esté relacionada con alguna funcionalidad en particular.
- Realiza la conexión a la base de datos. `Buena Práctica`: puedes realizar la conexión en una clase independiente e importarla en tu clase de prueba.
- Realiza uno o varios scripts de pruebas según la necesidad de tu funcionalidad.
- Realiza aserciones con los datos obtenidos de la consulta ejecutada.
- Utiliza las consultas a la base de datos como insumo para tus pruebas, es decir, guarda información en las tablas que puedas luego consultar y usarla por ejemplo para llenar campos en formularios.
