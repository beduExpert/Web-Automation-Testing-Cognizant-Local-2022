# Reto 01# - Anotaciones TestNG

## Objetivo

* Implementar las anotaciones TestNG en los scripts de pruebas

## Desarrollo

Tomando en cuenta las anotaciones de TestNG:

1. `BeforeSuite`
2. `BeforeTest`
3. `BeforeClass`
4. `BeforeMethod`
5. `Test`
6. `AfterMethod`
7. `AfterClass`
8. `AfterTest`
9. `AfterSuite`

Desarrolla un script de prueba que contenga la mayoria de estas anotaciones.

Código base
```Java
package com.bedu.web_automation_course;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterClass;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.AfterSuite;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.BeforeSuite;


public class base {
	
	@BeforeSuite
	public void beforeSuite() {
		System.out.println("El método anotado con @BeforeSuite se ejecutará antes de que se hayan ejecutado todas las pruebas de la suite.");
		}
	
	@BeforeTest
	  public void beforeTest(){
		System.out.println("El método anotado con @BeforeTest se ejecutará antes de que se ejecute cualquier método de prueba que pertenezca a una clase.");
	  }

	@BeforeClass
	  public void beforeClass(){
		System.out.println("El método anotado con @BeforeClass se ejecutará una vez antes de que se invoque el primer método de prueba en la clase actual.");
	  }
	
	@BeforeMethod
	  public void beforeMethod(){
		System.out.println("El método anotado con @BeforeMethod se ejecutará antes de que se ejecute cualquier método de prueba dentro de una clase.");
	  }
	
	@Test
		public void test() {
		System.out.println("El método anotado con @Test es el método de prueba principal en todo el programa. Se ejecutarán otros métodos anotados en torno a este método.");
		  }

	@AfterMethod
	public void afterMethod() {
		System.out.println("El método anotado con @AfterMethod se ejecutará después de que se ejecute cada método de prueba dentro de una clase.");
	  }
	
	@AfterClass
	public void afterClass() {
		System.out.println("El método anotado con @AfterClass se ejecutará una vez después de que se hayan ejecutado todos los métodos de prueba de la clase actual.");
	  }

	@AfterTest
	public void afterTest() {
		System.out.println("El método anotado con @AfterTest se ejecutará después de que se hayan ejecutado todos los métodos de prueba que pertenecen a una clase.");
	}

	@AfterSuite
	public void afterSuite() {
		System.out.println("El método anotado con @AfterSuite se ejecutará después de que se hayan ejecutado todas las pruebas de la suite.");
	}

}

```



<details>
  <summary>Solución</summary>
  
  ```Java
  package com.bedu.web_automation_course;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;

import static org.testng.Assert.assertTrue;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.AfterSuite;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.BeforeSuite;


public class agendar_cita {
	
	private WebDriver driver;
	
	@BeforeSuite
	public void beforeSuite() {
		System.out.println("---------------------------------------------------------------------------------");
		System.out.println("--------------------     INICIO DE LA EJECUCIÓN   -------------------------------");
		System.out.println("---------------------------------------------------------------------------------");
		}
	
	@BeforeTest
	  public void beforeTest(){


		}

	@BeforeClass
	  public void beforeClass(){
		System.out.println("INICIO DE LAS PRUEBAS SOBRE EL MODULO: AGENDAR ASESORIA");	
		}
	
	@BeforeMethod
	  public void beforeMethod() throws InterruptedException{
		System.out.println("INICIO DE LA PRUEBA");
		
		System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
		driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.get("https://bedu.org/");
		Thread.sleep(2000);
		
		By bnt_asesoria = By.xpath("//button[contains(.,'Agendar Asesoría')]");
		assertTrue(isButtonDisplayed(bnt_asesoria, driver));
		driver.findElement(bnt_asesoria).click();
		Thread.sleep(2000);

		 
	  }
	
	@Test (priority = 1)
		public void test_cancelar() {
		
		System.out.println("Click sobre cancelar..");
		driver.findElement(By.xpath("//button[contains(.,'Cancelar')]")).click();

			
		}
	@Test (priority = 2)
		public void test_agendar() {
		System.out.println("prueba de test_agendar");


		}
	
		//Metodo que recibe el localizador y el driver y retorna true o false si isDisplayed()
		public boolean isButtonDisplayed(By objeto, WebDriver driver) {
			System.out.println("Validando si el objeto isDispayed()...");
			return driver.findElement(objeto).isDisplayed();
		}

	@AfterMethod
	public void afterMethod() throws InterruptedException {
		System.out.println("Cerrando navegador..");	
		Thread.sleep(2000);
		driver.close();	
		}
	
	@AfterClass
	public void afterClass() {
		System.out.println("FIN DE LAS PRUEBAS SOBRE EL MODULO: AGENDAR ASESORIA");	
		}

	@AfterTest
	public void afterTest() {
		System.out.println("FIN DEL LAS DE PRUEBAS");
	}

	@AfterSuite
	public void afterSuite() {
		System.out.println("---------------------------------------------------------------------------------");
		System.out.println("--------------------     FIN DE LA EJECUCIÓN     --------------------------------");
		System.out.println("---------------------------------------------------------------------------------");
	}

}

  ```
</details>

