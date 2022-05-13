# Ejemplo-05: Clase Webdriver y WebElement

## Objetivo

* Hacer uso de las clases de Selenium: Webdriver y WebElement en los scripts de pruebas automatizados.

## Desarrollo

Selenium WebDriver nos brinda la posibilidad de poder referirnos a estos elementos y ejecutar métodos específicos para realizar las mismas acciones que un humano haría sobre los mismos, gracias a las clases WebDriver y WebElement.

Entremos en más detalle con respecto de que podemos hacer con estas dos clases, ya que serán las más utilizadas para nuestras automatizaciones.

#### Clase WebDriver

Cuenta con una serie de propiedades y métodos para interactuar directamente con la ventana del navegador y sus elementos relacionados, como son pop-ups o alerts.

Los métodos en esta interfaz se dividen en tres categorías:
- Control del propio navegador
- Selección de Elementos Web
- Ayudas de depuración

Los métodos clave son `get(String)`, que se usa para cargar una nueva página web, y varios métodos similares a `findElement(By)`, que se usa para encontrar WebElements.

Estos son las propiedades más utilizados de esta clase:

```Java
package com.bedu.web_automation_course;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;
import java.time.Duration;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;


public class base {

	private WebDriver driver;

		  @BeforeTest
		  public void beforeTest() {
				System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
				driver = new ChromeDriver();
				driver.manage().window().maximize();
				driver.get("https://google.com/");
				driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));			
		  }

		  @Test
		  public void test() {
			  System.out.println("getCurrentUrl = " + driver.getCurrentUrl());		  
			  System.out.println("getWindowHandle = " + driver.getWindowHandle());
			  //System.out.println("getPageSource = " + driver.getPageSource());
			  System.out.println("getTitle = " + driver.getTitle());
		  }

		  @AfterTest
		  public void afterTest() {
			  	driver.close();
		  }
}
```


#### Clase WebElement

Esta clase nos permite interactuar específicamente con elementos de los sitios web como textbox, text area, button, radio button, checkbox, etc.

Estos son las propiedades y métodos más utilizados de esta clase:

```Java
package com.bedu.web_automation_course;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;
import java.time.Duration;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;


public class base {

	private WebDriver driver;
	private WebElement googleSearch;

		  @BeforeTest
		  public void beforeTest() {
				System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
				driver = new ChromeDriver();
				driver.manage().window().maximize();
				driver.get("https://google.com/");
				driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));			
		  }

		  @Test
		  public void test() {
			  googleSearch = driver.findElement(By.name("q"));
			  
			  System.out.println("getClass = " + googleSearch.getClass());
			  System.out.println("getSize = " + googleSearch.getSize());
			  System.out.println("getText = " + googleSearch.getText());
			  System.out.println("getTagName = " + googleSearch.getTagName());	  
			  
			  if(googleSearch.isDisplayed()) {
				  googleSearch.click();
				  googleSearch.sendKeys("Bedu");
				  googleSearch.clear();
				  
			  }

		  }

		  @AfterTest
		  public void afterTest() {
			  	driver.close();
		  }

}
```