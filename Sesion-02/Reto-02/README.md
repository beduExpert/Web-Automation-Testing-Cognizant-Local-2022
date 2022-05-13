# Reto 2# - Uso de los Tipos de localizadores

## Objetivo

* Comprender el uso de los diferentes tipos de localizadores de elementos en la pagina web.

## Desarrollo

Teniendo en cuenta los distintos tipos de localizadores:

Ingresa en la página web: https://bedu.org/ e intenta localizar 3 o mas elementos con los siguientes localizadores:

- `By.id("xxxxx")`
- `By.name("xxxxx")`
- `By.className("xxxxx.class")`
- `By.tagName("xxxxx")`
- `By.linkText("xxxxx")`
- `By.partialLinkText("xxxxx")`
- `By.cssSelector("input[name=’xxxxx’]")`
- `By.xpath("//input[@name='xxxxx']")`


Puedes usar este codigo de base:

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
	}

	@AfterTest
	public void afterTest() {
		driver.close();
	}

}
```

<details>
  <summary>Solución</summary>

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
		driver.get("https://bedu.org/");
		Thread.sleep(2000);
	}

	@Test
	public void test() {
		driver.findElement(By.xpath("//button[contains(.,'Agendar Asesoría')]"));
		driver.findElement(By.linkText("Términos y condiciones"));
		driver.findElement(By.partialLinkText("Términos"));
	}

	@AfterTest
	public void afterTest() {
		driver.close();
	}
}
  ```

  </details>

