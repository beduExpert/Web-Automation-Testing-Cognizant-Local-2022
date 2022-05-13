# Sesión # 7 Postwork 

## :dart: Objetivos

- Utilizar Appium Inspector en los nuevos elementos de la pantalla de una funcionalidad de Mercadolibre para utilizarlos como insumo en los scripts de pruebas automatizados.
- Modificar los scripts de pruebas automatizados de una funcionalidad de la Mercadolibre para ser ejecutado en la aplicación desde un Dispositivo Virtual de Android (AVD).




## ⚙ Requisitos

- Software de desarrollo
    - Java Software Development Kit (JDK)
- Editor de código
    - Eclipse IDE
- Entorno de pruebas de software
    - Selenium Java Client
    - Selenium Webdriver
    - Appium
    - Appium Inspector
- Navegador App
    - Google Chrome
- Emulador
  - Android Virtual Device (Android Studio)


## Desarrollo

+ Selecciona una de las clases de java de tu proyecto donde ya se encuentren automatizados los casos de prueba de alguna funcionalidad de mercado libre.

+ Realiza una nueva clase java donde:

    - Configures el Android Driver
    - Configures los `DesiredCapabilities()` con los atributos requeridos para abrir la aplicación de mercadolibre en el dispositivo. Si tienes dudas sobre este punto puedes revisar la documentacion oficial de appium: https://appium.io/docs/en/writing-running-appium/caps/. `Pro-tip`: utiliza la aplicación `apk info` para obtener los valores del `appPackage` y `appActivity`.

+ Adaptar al menos 10 test de pruebas que utilicen los localizadores de la aplicación de mercadolibre en el dispositivo virtual de android (AVD).

+ Utiliza Appium Inspector para poder encontrar los localizadores que necesitas de la app de mercadolibre en el dispositivo virtual.

+ Recuerda utilizar las anotaciones de TestNG.

+ Recuerda hacer uso del Patrón POM si los localizadores cambian o existen nuevos.
