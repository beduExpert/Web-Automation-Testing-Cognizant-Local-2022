# Sesión #2 Postwork: 

## :dart: Objetivos

- Automatizar los casos de prueba elaborados en el postwork de la sesión 1 haciendo uso de localizadores, técnicas de manejo de errores, de las clases WebDriver/WebElement y finalmente usando afirmaciones.
- Emplear el uso de las anotaciones de TestNG en los scripts de pruebas automatizados.
- Reconocer la necesidad de implementar esperas (waits) en los script de pruebas.



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


## Desarrollo
- Estructura los casos de pruebas en tu proyecto usando las siguientes anotaciones TestNG para darles lógica de ejecución:
    - @BeforeTest
    - @BeforeMethod
    - @Test
    - @AfterMethod
    - @AfterTest

- Agregale prioridad a tus casos de pruebas con el uso de la anotación de TestNG `@Test (Priority)`
- Utiliza selenium IDE o la herramienta de desarrolladores de google chrome para identificar los localizadores de los elementos en la pantalla para luego incluirlos es los scripts de prueba. __Pro-tip:__ Asegúrate que si tiene id o name usa preferiblemente estos localizadores.
- Incluye en tu código tipos de esperas explícitas, incluyendo a su vez las condiciones esperadas.
- Trata de incluir técnicas de manejo de errores como `Try/catch`.
- Utiliza propiedades/métodos de la clase WebDriver como: `driver.close()`, `driver.manage()`, `driver.get()`.
- Utiliza propiedades/métodos de la clase WebElement como: `click()`, `sendKeys()`,`clear()`.
- Incluye aserciones en tu código para validar el resultado esperado del caso de prueba que estás ejecutando. __Pro-tip:__ Si lo requieres puedes incluir varias aserciones en un mismo caso de prueba. 

