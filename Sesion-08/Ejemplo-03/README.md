# Ejemplo-03 # - Comandos

## Objetivo

- Aplicar los comandos más utilizados de Appium que pueden ser incorporados en los scripts de pruebas automatizados. 

## Desarrollo

Appium ofrece múltiples comandos para interactuar con los dispositivos móviles, en este tema veremos los más importantes:

- `Status`: Devuelve información sobre si un extremo remoto se encuentra en un estado en el que puede crear nuevas sesiones y, además, puede incluir metainformación arbitraria que es específica de la implementación.

```Java
driver.getStatus();
```

- `Ejecutar Script`: Ejecuta una variedad de comandos móviles nativos que no están asociados con un endpoint específico. La sintaxis es `execute("mobile: <commandName>", <argumento JSON serializable>)`

```Java
driver.executeScript("mobile: scroll", ImmutableMap.of("direction", "down"));
```

- __Sesiones__:
    - `Crear`: crea una nueva sesión, es decir, el servidor debe intentar crear una sesión que coincida lo más posible con las capacidades deseadas y requeridas.
    ```Java
    String sessionId = driver.getSessionId().toString();
    ```

    - `Terminar`: termina la sesión en ejecución.
    ```Java
    driver.quit();
    ```

    - `Obtener capacidades de sesión`: recupera las capacidades de la sesión especificada.
    ```Java
    Map<String, Object> caps = driver.getSessionDetails();
    ```

    - `Tomar captura de pantalla`: toma una captura de pantalla de la vista/ventana/página actual, es decir, toma una captura de pantalla de la ventana gráfica en un contexto nativo (iOS, Android) y toma una captura de pantalla de la ventana en contexto web

    ```Java
    File scrFile = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
    ```

    - `Obtener la fuente de la página`: obtiene la jerarquía de aplicaciones actual XML (aplicación) o fuente de página (web). En un contexto web, la fuente devuelve el HTML fuente de la ventana actual. En un contexto nativo (iOS, Android, etc...) devolverá el XML de jerarquía de la aplicación.

    ```Java
    String pageSource = driver.getPageSource();
    ```

    - `Tiempos de espera`: configura la cantidad de tiempo que se puede ejecutar un tipo particular de operación antes de que se cancele. Los tipos de tiempos de espera son 'carga de página', 'script' e 'implícito'.

    ```Java
    driver.manage().timeouts().pageLoadTimeout(30, TimeUnit.SECONDS);
    ```

    - `Espera implícita`: establece la cantidad de tiempo que el conductor debe esperar al buscar elementos. Al buscar un solo elemento, el controlador debe sondear la página hasta que encuentre un elemento o expire el tiempo de espera, lo que ocurra primero. Es decir, al buscar varios elementos, el controlador debe sondear la página `hasta que encuentre al menos un elemento o expire el tiempo de espera`, momento en el que debe devolver una lista vacía. Si nunca se envía este comando, el driver debe tener una `espera implícita de 0 ms por defecto`.

    ```Java
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
    ```

    - `Tiempo de espera del script`: establece la cantidad de tiempo, en milisegundos, que los scripts asincrónicos pueden ejecutarse antes de que se anulen (solo contexto web).

    ```Java
    driver.manage().timeouts().setScriptTimeout(30, TimeUnit.SECONDS);
    ```

    - __Orientación__:
        - `Obtener orientación`: obtiene la orientación actual del dispositivo/navegador

        ```Java
        ScreenOrientation orientation = driver.getOrientation();
        ```

        - `Establecer orientación`: establece la orientación actual del dispositivo/navegador

        ```Java
        driver.rotate(ScreenOrientation.LANDSCAPE);
        ```
    - `Obtener registros`: obtiene los logs (registros) para un tipo de log determinado. El búfer de log se restablece después de cada solicitud.

    ```Java
    LogEntries logEntries = driver.manage().logs().get("driver");
    ```

    - `Instalar aplicación`: instala la aplicación dada en el dispositivo.

    ```Java
    driver.installApp("/Users/johndoe/path/to/app.apk");
    ```

    - `Ejecutar aplicación`: inicia la aplicación bajo prueba en el dispositivo.

    ```Java
    driver.launchApp();
    ```

    - Cerrar aplicación: cierra la aplicación bajo prueba en el dispositivo.
    
    ```Java
    driver.closeApp();
    ```

    - `Bloquear`: bloquea el dispositivo.
    ```Java
    driver.lockDevice();            
    ```

    - `Desbloquear`: desbloquea el dispositivo.
    ```Java
    driver.driver.unlockDevice();
    ```

    - `Presionar el código clave`: presiona una tecla en particular en un dispositivo Android.

    ```Java
    driver.pressKeyCode(AndroidKeyCode.SPACE, AndroidKeyMetastate.META_SHIFT_ON);
    ```

    - `Ocultar el teclado`: oculta el teclado del dispositivo.
    ```Java
    driver.hideKeyboard();
    ```

    - `Grabación de Pantalla`: graba la pantalla del dispositivo.

    ```Java
    driver.startRecordingScreen();
    driver.startRecordingScreen(new BaseStartScreenRecordingOptions(....));
    ```

    - __Elementos__:

        - `Encontrar elemento`: encuentra el elemento en la pantalla del dispositivo. Es decir, obtiene el primer elemento que coincida con una estrategia de localización

        ```Java
        MobileElement elementOne = (MobileElement) driver.findElementByAccessibilityId("SomeAccessibilityID");
        MobileElement elementTwo = (MobileElement) driver.findElementByClassName("SomeClassName");
        ```

        - `Encontrar elementos`: encuentra los elementos en la pantalla del dispositivo. Es decir, obtiene los elementos que coincidan con una estrategia de localización.

        ```Java
        List<MobileElement> elementsOne = (List<MobileElement>) driver.findElementsByAccessibilityId("SomeAccessibilityID");
        List<MobileElement> elementsTwo = (List<MobileElement>) driver.findElementsByClassName("SomeClassName");
        ```
    - __Acciones sobre elementos__:
        - `Click`: hace click sobre un elemento en el dispositivo.
        ```Java
        MobileElement el = driver.findElementByAccessibilityId("SomeId");
        el.click();
        ```

        - `Enviar claves`: envía una secuencia de pulsaciones de teclas a un elemento.

        ```Java
        MobileElement element = (MobileElement) driver.findElementByAccessibilityId("SomeAccessibilityID");
        element.sendKeys("Hello world!");
        ```

        - `Limpiar elemento`: borra el valor de un elemento.

        ```Java
        MobileElement element = (MobileElement) driver.findElementByAccessibilityId("SomeAccessibilityID");
        element.clear();
        ```
    - __Atributos de Elementos__: 
        - `Obtener texto del elemento`: devuelve texto visible para el elemento.

        ```Java
        MobileElement element = (MobileElement) driver.findElementByClassName("SomeClassName");
        String elText = element.getText();
        ```

        - `Elemento seleccionado` : determina si un formulario o elemento similar a un formulario (casilla de verificación, selección, etc.) está seleccionado.

        ```Java
        MobileElement element = (MobileElement) driver.findElementByAccessibilityId("SomeAccessibilityID");
        boolean isSelected = element.isSelected();
        ```

        - `Elemento habilitado`: determina si un elemento está actualmente habilitado.

        ```Java
        MobileElement element = (MobileElement) driver.findElementByAccessibilityId("SomeAccessibilityID");
        boolean isEnabled = element.isEnabled();
        ```

        - `Elemento mostrado`: determina si un elemento se muestra actualmente.

        ```Java
        MobileElement element = (MobileElement) driver.findElementByAccessibilityId("SomeAccessibilityID");
        boolean isDisplayed = element.isDisplayed();
        ````

    - `Enviar formulario`: envía un elemento FORM.

    ```Java
        MobileElement element = (MobileElement) driver.findElementByClassName("SomeClassName");
        element.submit();
    ```

    - `Elementos iguales`: prueba si dos ID de elementos se refieren al mismo elemento.

    ```Java
    MobileElement elementOne = (MobileElement) driver.findElementByClassName("SomeClassName");
    MobileElement elementTwo = (MobileElement) driver.findElementByClassName("SomeOtherClassName");
    boolean isEqual = elementOne.equals(elementTwo);
    ```

    - __Comandos web__:
        - `Ir a URL`: navega a una nueva URL (contexto web) o abre un enlace profundo (Deeplink) de Appium (nativo).
        ```Java
        driver.get("http://bedu.org");
        ```

        - `Regresa`: navega hacia atrás en el historial del navegador, si es posible (solo contexto web).

        ```Java
        
        driver.navigate().back();
        ```

        - `Avanzar`: navega hacia adelante en el historial del navegador, si es posible (solo contexto web).

        ```Java
        driver.navigate().forward();
        ```

        - `Actualizar`: actualiza la página actual. (Solo contexto web).

        ```Java
       driver.navigate().refresh();
        ```


`Ejemplo de Comandos con Appium`

```Java
 package tests;

import java.net.MalformedURLException;
import java.net.URL;

import org.openqa.selenium.By;
import org.openqa.selenium.ScreenOrientation;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;
import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.remote.MobileCapabilityType;


public class bedu {
	
	//Inicializamos el AndroidDriver
		AndroidDriver driver;
		
		@BeforeTest
		public void beforeTest() throws MalformedURLException {
			
			//Configuramos los DesiredCapabilities		
			DesiredCapabilities dc = new DesiredCapabilities();

			// DesiredCapabilities Generales
			dc.setCapability(MobileCapabilityType.AUTOMATION_NAME, "uiautomator2");
			dc.setCapability(MobileCapabilityType.DEVICE_NAME, "emulator-5554");
			dc.setCapability(MobileCapabilityType.PLATFORM_NAME, "android");
			dc.setCapability(MobileCapabilityType.PLATFORM_VERSION, "12");
			dc.setCapability(MobileCapabilityType.ORIENTATION, "PORTRAIT");
			dc.setCapability(MobileCapabilityType.BROWSER_NAME, "Chrome");
			
			//Establecemos la conexion con el server de Appium
			driver = new AndroidDriver (new URL("http://127.0.0.1:4723/wd/hub"), dc);
			System.out.println("Application started");
			driver.get("https://bedu.org/");
		}
		
		@Test ()
		public void test() throws InterruptedException {
			
			WebElement element = driver.findElement(By.xpath("//button[contains(.,'Agendar Asesoría')]"));
			
	      
	        if(element.isDisplayed()) {
	        	System.out.println("Pagina: " + driver.getCurrentUrl() + "desplegada correctamente..."); 
	        	driver.get("https://www.youtube.com/c/BEDU_Org");
				System.out.println("Accediendo a la pagina: " + driver.getCurrentUrl()); 
				driver.navigate().back();
				
				if(element.isEnabled()) {
					driver.navigate().forward();
					System.out.println("Accediendo a la pagina: " + driver.getCurrentUrl());
					driver.navigate().refresh();
					driver.navigate().back();
				}
	
	        }
	        
	        System.out.println("Accediendo a la pagina: " + driver.getCurrentUrl());
			element.click();
			driver.rotate(ScreenOrientation.LANDSCAPE);
		}
	
		@AfterTest
		public void afterTest() throws InterruptedException {
			Thread.sleep(2000);
			driver.quit();
		}
}
```











 



















































