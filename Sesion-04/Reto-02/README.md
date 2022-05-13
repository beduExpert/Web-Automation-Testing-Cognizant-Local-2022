# Reto 02# - Dataprovider

## Objetivo

* Demostrar el comportamiento del @DataProvider durante la ejecución de los scripts de pruebas automatizados.

## Desarrollo

Ejecuta el siguiente codigo en tu computadora:

```Java
package tests;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import pages.AgendarCitaPage;
import pages.HomePage;
import tests.data_provider;


public class DataDrivenTestingUsingDataProvider {

	private WebDriver driver;
	private HomePage homePage;
	private AgendarCitaPage agendarCitaPage;

	@BeforeTest
	public void beforeTest() throws InterruptedException {
		System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
		driver = new ChromeDriver();
		driver.manage().window().maximize();
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

	@AfterTest
	public void afterTest() {
		driver.close();
	}
}

```


<details>
  <summary>¿Que fue lo que sucedio y porque?</summary>
> Genero error en la ejecución, esto se debe a que el dataprovider se ejecutara bajo la anotación @Test tantas veces como casos de prueba contenga el objeto retornado por el  `metodoDataProvider`, por lo que el uso de la anotación @BeforeTest y @AfterTest no es la apropiada para la prueba. Es por ello que por si no lo notaste, en la explicación del tema se utilizo la anotación @AfterMethod y @BeforeMethod para que pudieran iniciar y finalizar los casos de prueba correctamente.
</details>

