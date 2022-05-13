# Reto 1 # - Automatización Web con dispositivo virtual de Android (AVD)

## Objetivo

- Desarrollar scripts de pruebas automatizados que puedan ser ejecutados en dispositivos móviles con Android por medio de la aplicación del navegador Google Chrome. 

## Desarrollo

Desarrollar un script de prueba automatizado  que puedan ser ejecutado en un dispositivo móvil virtual de Android por medio del navegador `google chrome`.

`Pro-tip`: recuerda que para las ejecuciones en navegadores web solo es necesario configurar correctamente los `DesiredCapabilities`


<details>
  <summary> Solución </summary>

  ```Java
package tests;

import java.net.MalformedURLException;
import java.net.URL;

import org.openqa.selenium.remote.DesiredCapabilities;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.remote.MobileCapabilityType;
import pages.AgendarCitaPage;
import pages.HomePage;

public class agendarCitaMobileTest {
	AndroidDriver driver;
	private HomePage homePage;
	private AgendarCitaPage agendarCitaPage;

	@BeforeMethod
	public void beforeTest() throws InterruptedException, MalformedURLException {
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


	@Test(dataProvider = "dataprovider", dataProviderClass = data_provider.class)
	public void agendarAsesoria(String name, String lastname, String phone, String email, String company,
			String jobtitle, String sector, String company_size, String program) throws InterruptedException {

		homePage = new HomePage(driver);
		// Validamos que el boton de agendar asesoria este disponible
		if (homePage.isButtonDisplayed()) {
			// Clck en boton de agendar asesoria
			try {
				homePage.clickButton();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}

		agendarCitaPage = new AgendarCitaPage(driver);

		if (agendarCitaPage.btn_CancelIsDispayed()) {

			agendarCitaPage.fillName(name);
			agendarCitaPage.fillLastname(lastname);
			agendarCitaPage.fillPhone(phone);
			// agendarCitaPage.fillEmail(email);
			agendarCitaPage.fillCompany(company);
			agendarCitaPage.fillJobTitle(jobtitle);
			agendarCitaPage.fillSector(sector);
			agendarCitaPage.fillCompanySize(company_size);
			agendarCitaPage.fillProgram(program);
			Thread.sleep(2000);
		}

	}

	@AfterMethod
	public void afterTest() {
		driver.close();
	}

}

  ```

</details>