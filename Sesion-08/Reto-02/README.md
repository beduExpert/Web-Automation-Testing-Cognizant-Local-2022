# Reto 2 # - Desired Capabilities

## Objetivo

- Desarrollar script donde se configuren más propiedades del objeto Desired Capabilities.

## Desarrollo

Desarrolla un script que realice las siguientes acciones:

- Abra google chrome
- Posicione la aplicación de forma vertical (`LANDSCAPE`)
- Abra la URL de youtube
- Cierre el navegador


<details>
  <summary> Solución </summary>

```Java
package tests;

import java.net.MalformedURLException;
import java.net.URL;

import org.openqa.selenium.remote.DesiredCapabilities;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.remote.MobileCapabilityType;

public class youtube {
	
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
			dc.setCapability(MobileCapabilityType.ORIENTATION, "LANDSCAPE");
			dc.setCapability(MobileCapabilityType.BROWSER_NAME, "Chrome");
			

			//Establecemos la conexion con el server de Appium
			driver = new AndroidDriver (new URL("http://127.0.0.1:4723/wd/hub"), dc);
			System.out.println("Application started");
			driver.get("https://www.youtube.com/");
		}
		
		@Test ()
		public void test() {
		}
		
		
		@AfterTest
		public void afterTest() {
			driver.quit();
		}

}
```
</details>

