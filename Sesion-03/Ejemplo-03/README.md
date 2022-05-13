# Ejemplo-03# - Implementación de POM en Selenium

## Objetivo

* Construir el patrón de diseño `Page Object Model (POM)` en el proyecto de automatización web.

## Desarrollo

Repasemos las principales ventajas de este modelo para empezar a pensar cómo se implementaría este modelo en nuestros proyectos:

- Hay una clara separación entre el código de prueba y el código específico de la página, como los localizadores y el diseño.

- Existe un repositorio único para los servicios u operaciones que ofrece la página en lugar de tener estos servicios dispersos a lo largo de las pruebas.

En ambos casos, esto permite que las modificaciones requeridas debido a los cambios en la interfaz de usuario se realicen en un solo lugar. Para comenzar, ilustraremos los objetos de la página con un ejemplo simple.

```Java
package tests;

import static org.testng.Assert.assertNotNull;
import java.time.Duration;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class agendarCitaTest {

	/***
	 * Pruebas sobre una funcionalidad de Agendar Cita en web de BEDU
	 */

	private WebDriver driver;
	private WebElement bnt_asesoria;

	  @BeforeTest
	  public void beforeTest() throws InterruptedException {
			System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
			driver = new ChromeDriver();
			driver.manage().window().maximize();
			driver.get("https://bedu.org/");
			Thread.sleep(2000);	
	  }

	  @Test
	  public void agendarCita() {
	    // Buscar el botón de agendar asesoria
		  bnt_asesoria = driver.findElement(By.xpath("//button[contains(.,'Agendar Asesoría')]"));
	    
	    //realizar click sobre el btn
		  bnt_asesoria.click();

	    // Validar si el formulario esta presente, validando que este desplegado el boton cancelar en la pantalla
	    driver.findElement(By.xpath("//button[contains(.,'Cancelar')]")).isDisplayed();
	    WebElement bnt_cancelar = new WebDriverWait(driver, Duration.ofSeconds(10))
	            .until(ExpectedConditions.elementToBeClickable(By.xpath("//button[contains(.,'Cancelar')]")));
	    
	    // hacemos una aserción para poder validar el resultado esperado de nuestra prueba
	    assertNotNull(bnt_cancelar.getText() ,"Formulario de Agendar asesoria esta desplegado exitosamente");
	    
	  }
	  
	  @AfterTest
	  public void afterTest() {
		  driver.close();
	  }
	}
```

> __Buena práctica:__ siempre comentar tu código, ten en cuenta que en un proyecto suelen haber más de 1 automatizador de pruebas, con lo cual es importante que comentes líneas de código con comentarios que puedan ayudar a entender que hace el código.

Ahora bien, en este código tenemos dos problemas:

1. No hay separación entre el método de prueba y los localizadores, ambos están entrelazados en un solo método. Si la interfaz de usuario cambia sus identificadores, el diseño o cómo se ingresa y procesa la funcionalidad de agendar cita, la prueba en sí debe cambiar.

2. Los localizadores de ID se distribuirían en múltiples pruebas, en todas las pruebas que tengan que usar esta pagina de agendar cita.

Al aplicar las técnicas de objeto de página `(Page object model)`, este ejemplo podría reescribirse así:

```Java
package pages;

import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class agendarCitaPage {
	
	/**
	 * Page Object Model (POM) para página de Agendar cita bedu
	 */
	
	protected WebDriver driver;

	  // Definimos objetos de tipo locator y le asignamos la localización By.
	  private By bnt_cancelar = By.xpath("//button[contains(.,'Cancelar')]");

	  // Creamos el método que recibirá el driver en esta clase
	  public agendarCitaPage(WebDriver driver){
	    this.driver = driver;
	  }

	  /**
	    * Creamos el método de login que cancelara la  asesoria   
	    * y retorna un objeto HomePage
	    */
	  public HomePage cancelarAsesoria() {
	    driver.findElement(bnt_cancelar).click();
	    return new HomePage(driver);
	  }
	  
	  public String btnIsDispayed() {
		    WebElement bnt_cancelar = new WebDriverWait(driver, Duration.ofSeconds(10))
		            .until(ExpectedConditions.elementToBeClickable(By.xpath("//button[contains(.,'Cancelar')]"))); 
		    return bnt_cancelar.getText();
		  }

}


```
y el Page Object  para la HomePage sería el siguiente:

```Java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

/**
 * Page Object Model (POM) para página de HomePage
 */
public class HomePage {
  protected WebDriver driver;

  // Definimos objetos de tipo locator y le asignamos la localización By.
  private By bnt_asesoria = By.xpath("//button[contains(.,'Agendar Asesoría')]");
  

	  // Creamos el método que recibirá el driver en esta clase
	  public HomePage(WebDriver driver){
	    this.driver = driver;
	
	    // Recuerdas la clase anterior de manejo de errores? bueno en este código hacemos una validación para asegurarnos que estemos en la homePage, validando que el título de la página sea la de bedu, si no lo es, se lanza una excepción y se devuelve la url de la página actual. 
	    if (!driver.getCurrentUrl().equals("https://bedu.org/")) {
	      throw new IllegalStateException("Error, no se recibió la página Home de Bedu, la página recibida es: " + driver.getCurrentUrl());
	    }
	      
	  }
  
	//Creamos el método validara si el botón esta disponible
	  public boolean isButtonDisplayed() {
	    return driver.findElement(bnt_asesoria).isDisplayed();
	  }
  
	//Creamos el método que realizara click en el botón
	  public void clickButton() {
	     driver.findElement(bnt_asesoria).click();
	  }
}
```
> __Buena práctica:__ Podemos hacer tantos métodos como funcionalidad tenga la página que estamos automatizando, en este caso la HomePage podría tener una sección de perfil una vez logueado el usuario.

Finalmente a prueba de inicio de sesión usaría estos dos Pages Objects de la siguiente manera.

```Java
package tests;

import static org.testng.Assert.assertNotNull;
import static org.testng.Assert.assertTrue;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import pages.HomePage;
import pages.agendarCitaPage;

public class agendarCitaTest {

	/***
	 * Pruebas sobre una funcionalidad de Agendar Cita en web de BEDU
	 */

	private WebDriver driver;
	private WebElement bnt_asesoria;

	  @BeforeTest
	  public void beforeTest() throws InterruptedException {
			System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
			driver = new ChromeDriver();
			driver.manage().window().maximize();
			driver.get("https://bedu.org/");
			Thread.sleep(2000);	
	  }

	  @Test
	  public void agendarCita() {
		// Creamos un nuevo objeto de tipo HomePage al que le enviaremos el driver
		 HomePage homePage = new HomePage(driver);
		 agendarCitaPage agendarCitaPage = new agendarCitaPage(driver);
		 
		 //Validamos que el boton de agendar asesoria este disponible
		 assertTrue(homePage.isButtonDisplayed());
		//Clck en boton de agendar asesoria
		 homePage.clickButton();
		 
	    // hacemos una aserción para poder validar el resultado esperado de nuestra prueba
		assertNotNull(agendarCitaPage.btnIsDispayed() ,"Formulario de Agendar asesoria esta desplegado exitosamente");
	    
	  }
	  
	  @AfterTest
	  public void afterTest() {
		  driver.close();
	  }
	}

```


Hay mucha flexibilidad en la forma en que se pueden diseñar los objetos de la página, pero existen algunas reglas básicas para obtener la mantenibilidad deseada de su código de prueba.

- Los `Page Objects` __nunca deben hacer verificaciones o afirmaciones__. Esto es parte de su prueba y siempre debe estar dentro del código de la prueba. Esto se debe a que el page object contendrá la representación de la página y los servicios que la página proporciona a través de métodos, pero ningún código relacionado con lo que se está probando debe estar dentro del objeto de la página.

- Hay una única verificación que puede y debe estar dentro del objeto de la página y es verificar que la página, y posiblemente los elementos críticos de la página, se cargaron correctamente. Esta verificación debe realizarse al instanciar el objeto de la página. En los ejemplos anteriores, los constructores `AgendarCitaPage` y `HomePage` verifican que la página esperada esté disponible y lista para las solicitudes de la prueba.

- Un page object __no necesita necesariamente representar todas las partes de una página en sí__. Los mismos principios utilizados para los objetos de página se pueden usar para crear `Objetos de componentes de página` que representan partes discretas de la página y se pueden incluir en los objetos de página. Estos objetos componentes pueden proporcionar referencias a los elementos dentro de esos fragmentos discretos y métodos para aprovechar la funcionalidad proporcionada por ellos. Incluso puede anidar objetos componentes dentro de otros objetos componentes para páginas más complejas. Si una página tiene varios componentes o componentes comunes utilizados en todo el sitio (por ejemplo, una barra de navegación), entonces puede mejorar la capacidad de mantenimiento y reducir la duplicación de código.