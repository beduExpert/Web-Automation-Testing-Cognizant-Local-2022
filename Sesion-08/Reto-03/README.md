# Reto 3 # - Comandos

## Objetivo

* Aplicar los comandos más utilizados de Appium que pueden ser incorporados en los scripts de pruebas automatizados. 

## Desarrollo

Desarrolla un script de pruebas que incluya al menos 5 comandos de appium

<details>
  <summary> Solución </summary>

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

</details>

