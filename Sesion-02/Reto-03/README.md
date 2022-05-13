# Reto 03# - Condiciones esperadas en esperas Explícitas

## Objetivo

* Practicar el uso de las condiciones esperadas en las esperas Explícitas.

## Desarrollo

Según lo visto en este tema sobre las condiciones de espera explicita:

- `alertIsPresent()`
- `elementSelectionStateToBe()`
- `elementToBeClickable()`
- `elementToBeSelected()`
- `frameToBeAvaliableAndSwitchToIt()`
- `invisibilityOfTheElementLocated()`
- `invisibilityOfElementWithText()`
- `presenceOfAllElementsLocatedBy()`
- `presenceOfElementLocated()`
- `textToBePresentInElement()`
- `textToBePresentInElementLocated()`
- `textToBePresentInElementValue()`
- `titleIs()`
- `titleContains()`
- `visibilityOf()`
- `visibilityOfAllElements()`
- `visibilityOfAllElementsLocatedBy()`
- `visibilityOfElementLocated()`

Realiza un script que contenga al menos 2 de ellas, puedes utilizar este script de base: 

```Java
package com.bedu.web_automation_course;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;

import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class base {

	private WebDriver driver;

	@BeforeTest
	public void beforeTest() {
		System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
		driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.get("https://www.google.com/");
	}

	@Test
	public void test() {

		driver.findElement(By.name("q")).sendKeys("bedu" + Keys.ENTER); // Keys.ENTER simula un enter, proviene de la
																		// clase Keys

		// inicializamos un objeto de tipo WebDriverWait
		WebElement firstResult = new WebDriverWait(driver, Duration.ofSeconds(10))
				.until(ExpectedConditions.elementToBeClickable(By.xpath("//input[@type='submit']"))); // este elemento
																										// no esta en la
																										// pantalla asi
																										// que generara
																										// un
																										// TimeoutException

		// Vemos el resultado
		System.out.println(firstResult.getText());
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

import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class base {

	private WebDriver driver;

	@BeforeTest
	public void beforeTest() {
		System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
		driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.get("https://www.google.com/");
	}

	@Test
	public void test() {

		// inicializamos un objeto de tipo WebDriverWait
		new WebDriverWait(driver, Duration.ofSeconds(5)).until(ExpectedConditions.elementToBeClickable(By.name("q")));

		driver.findElement(By.name("q")).sendKeys("bedu" + Keys.ENTER); // Keys.ENTER simula un enter, proviene de la
																		// clase Keys

		// inicializamos un objeto de tipo WebDriverWait
		new WebDriverWait(driver, Duration.ofSeconds(5))
				.until(ExpectedConditions.elementToBeSelected(By.xpath("//input[@type='submit']"))); // este elemento
																										// no esta en la
																										// pantalla asi
																										// que generara
																										// un
																										// TimeoutException
	}

	@AfterTest
	public void afterTest() {
		driver.close();
	}

}

  ```

  </details>
