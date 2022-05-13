# Sesión 6 # Postwork: 

## :dart: Objetivos

- Adaptar scripts de pruebas automatizados para que pueden ser ejecutados  múltiples navegadores (cross browser testing).
- Construir nuevos scripts de pruebas automatizados donde se implemente la ejecución en máquinas remotas con Selenium Grid.


## ⚙ Requisitos

- Software de desarrollo
    - Java Software Development Kit (JDK)

- Editor de código
    - Eclipse IDE

- Entorno de pruebas de software
    - Selenium Java Client
    - Selenium Webdriver
    - Selenium Server GRID

- Navegador
    - Google Chrome

- Selenium browserdriver
    - Chromium/Chrome
    - Mozilla (geckodriver)

## Desarrollo

- Adaptar scripts de pruebas automatizados para que pueden ser ejecutados  múltiples navegadores (cross browser testing).
    - Selecciona una funcionalidad de mercado libre para automatizar o una que ya tengas automatizada. 
        + `Pro-Tip:` es recomendable automatizar una nueva funcionalidad, de esta manera puedes tener un nuevo mecanismo de ejecución de pruebas en tu proyecto.

    - Agrega la parametría al archivo `testng.xml` para que tome la información de los navegadores (2 como mínimo). 
        + `Pro-tip:` Puedes incluir más información en este archivo sobre el navegador que necesites posteriormente en la clase de prueba, como por ejemplo: nombre del explorador, versión, la ruta donde se encuentra el driver, etc.
        
        + `Buena Práctica:` como no tenemos forma de acceder a google analytics o alguna herramienta que nos de la información de cuáles son los navegadores con los que más se ingresa a la web de mercado libre, puedes investigar en internet cuales son los exploradores más utilizados generalmente, eso te ayudará a saber cuáles priorizar.

    - Utiliza la anotación `@Parameters()` en clase de prueba para que consuma la parametría del archivo `testng.xml`
    - Adapta los métodos de pruebas para que ejecuten las pruebas depende de los navegadores parametrizados.

- Construir nuevos scripts de pruebas automatizados donde se implemente la ejecución en máquinas remotas con Selenium Grid 4.
    - Selecciona una funcionalidad de mercado libre para automatizar o una que ya tengas automatizada. 
        + `Pro-Tip:` es recomendable automatizar una nueva funcionalidad, de esta manera puedes tener un nuevo mecanismo de ejecución de pruebas en tu proyecto.
    - Crea la clase de prueba donde se utilicen los objetos DesiredCapabilites y RemoteWebDriver.
    - Inicia Selenium Grid 4
        + `Pro-Tip:` recomendamos usar el rol standalone de Selenium Grid 4 (donde el mismo servidor es el hub y el node). 
    - Ejecuta las pruebas automatizadas.
