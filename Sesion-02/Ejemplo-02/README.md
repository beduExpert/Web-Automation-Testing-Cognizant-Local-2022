# Ejemplo-02: Localización de elementos con Selenium IDE

## Objetivo

* Emplear los diferentes tipos de localizadores de selenium para identificar la presencia de elementos en la pagina web.

## Desarrollo

Para entrar en el mundo de los localizadores de Selenium tenemos que explicar el concepto de `WebElement`, la misma es una clase creada para los elementos que componen la página web. Para Selenium WebDriver todos los elementos de una página web (campos de texto, botones, links, imágenes, entre otros..) son `WebElements`.

Para poder encontrar WebElements en la página web, Selenium utiliza los localizadores que le permite al encontrarlo, ejecutar alguna acción sobre el cómo extraer su contenido, hacer un click, revisar si se encuentra disponible, etc..

Ahora bien, __¿Cómo le indicamos a Selenium qué es lo que debe hacer?__

Esto se realiza con los siguiente comando:

```Java
driver.findElement();
driver.findElements();
```

<img src="assets/find.png" width="80%"> 

Estos son los métodos encargados de devolver el/los WebElement recibiendo como parámetro un localizador (By). 

>**💡 Conoceremos más sobre estos dos metodos en la sesión [**`Find element Vs Find elements`**](../Ejemplo-04)**


#### Tipos de localizadores:

- `By.id("xxxxx")`: El id es el identificador único del elemento. Debido a esto se recomienda siempre que el elemento tenga un id, utilizarlo como primera opción de localización.

    ```Java
    driver.findElement(By.id("id"));
    ```

- `By.name("xxxxx")`:  busca si el elemento tiene un atributo name determinado. En caso que no tengamos un id y es recomendable usar el name (si lo tiene). Usualmente los nombres de los elementos son únicos y nos permiten ubicar un elemento con facilidad.

    ```Java
    driver.findElement(By.name("name"));
    ```

- `By.className("xxxxx.class")`: Este localizador se refiere al atributo class del elemento Web.

    ```Java
    driver.findElement(By.className("className"));
    ```

- `By.tagName("xxxxx")`:  Este localizador busca por el nombre del tag del elemento dentro del DOM(Document Object Model)

    ```Java
    driver.findElement(By.tagName("tagName"));
    ```

- `By.linkText("xxxxx")`:  Este localizador busca links en la página donde el texto coincida con el parámetro que le pasamos al método linkText().

    ```Java
    driver.findElement(By.linkText("linkText"));
    ```

- `By.partialLinkText("xxxxx")`: Este localizador busca links en la página donde el texto coincida parcialmente con el parámetro que le pasamos al método partialLinkText(“string”).

    ```Java
    driver.findElement(By.partialLinkText("partialLinkText"));
    ```

- `By.cssSelector("input[name=’xxxxx’]")`: Este localizador es una estrategia de localización que utiliza el lenguaje CSS para encontrar el elemento.

    ```Java
    driver.findElement(By.cssSelector("cssSelector"));
    ```

- `By.xpath("//input[@name='xxxxx']")`: Permite encontrar elementos por su XPATH(es un lenguaje que permite recorrer y procesar los elementos del DOM, por lo que es muy útil para encontrar un WebElement)

    ```Java
    driver.findElement(By.xpath("//input[@type='submit']"));
    ```


#### Puedes ejecutar este código de Ejemplo:

```Java
package com.bedu.web_automation_course;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;


public class base {

	private WebDriver driver;


		@BeforeTest
		  public void beforeTest() throws InterruptedException {
				System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
				driver = new ChromeDriver();
				driver.manage().window().maximize();
				driver.get("https://google.com");	
				Thread.sleep(2000);
		  }

		  @Test
		  public void test() {
			  driver.findElement(By.xpath("//input[@type='submit']"));
			  driver.findElement(By.name("q"));
			  driver.findElement(By.className("gNO89b"));		  
			  driver.findElement(By.xpath("//input[@type='submit']"));		  
		  }

		  @AfterTest
		  public void afterTest() {
			  	driver.close();
		  }

}
```

