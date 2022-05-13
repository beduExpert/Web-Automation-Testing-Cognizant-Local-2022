# Reto 2 # - Primer tests automatizado sobre el emulador de android

## Objetivo

* Modificar los scripts de pruebas de automatizaciones Web a script de pruebas que puedan ser ejecutados en plataformas móviles.

## Desarrollo

En el desarrollo del [**`EJEMPLO 4 - Ejecución del primer tests automatizado sobre el emulador de android`**](./Ejemplo-04) realizamos un script de prueba sobre la funcionalidad de suma de la calculadora.

1. Agrega en el archivo del patrón Page Object Model -> `CalculatorPage` los metodos restantes para al menos 2 operaciones mas.
2. Agregar en el Script de Prueba los test correspondiente al resto de las operaciones de la calculadora.
3. Ejecuta los casos de pruebas con appium en el emulador y valida el comportamiento en la calculadora.


<details>
  <summary> Solución </summary>

`POM`

```Java
package pages;

import org.openqa.selenium.By;

import io.appium.java_client.android.AndroidDriver;

public class CalculatorPage {

	/**
	 * Page Object Model (POM) para aplicación de Calculadora
	 */

	protected AndroidDriver driver;

	// Creamos el método que recibirá el driver en esta clase
	public CalculatorPage(AndroidDriver driver){
		    this.driver = driver; 
		  }

	// Creamos el método que creara el localizador by para los numeros de la calculadora
	public By locateDigit(int digito){
		String locator = "com.google.android.calculator:id/digit_"+ digito;
		By digit = By.id(locator);
		return digit;
		
	}
	
	// Creamos el método que realizara click en los digitos de la calculadora
	public void clickDigit(int digit) throws InterruptedException {
        
        String number = String.valueOf(digit);
        char[] digits = number.toCharArray();

        for(int i = 0; i < digits.length; i++) {
    
        	driver.findElement(locateDigit(Character.getNumericValue(digits[i]))).click();
        }
		
	}
	
	// Creamos el método que realizara click en la suma
	public void clickSuma() throws InterruptedException {
		driver.findElement(By.id("com.google.android.calculator:id/op_add")).click();
	}
	
	// Creamos el método que realizara click en la resta
	public void clickResta() throws InterruptedException {
		driver.findElement(By.id("com.google.android.calculator:id/op_sub")).click();
	}
	
	// Creamos el método que realizara click en la multiplicacion
	public void clickMultiplicar() throws InterruptedException {
		driver.findElement(By.id("com.google.android.calculator:id/op_mul")).click();
	}
	
	
	// Creamos el método que realizara click en la suma
	public void clickClear() throws InterruptedException {
		driver.findElement(By.id("com.google.android.calculator:id/clr")).click();
	}
	
	
	// Creamos el método que obtiene el resultado
	public String getResult() throws InterruptedException {
		Thread.sleep(2000);
		String result = driver.findElement(By.id("com.google.android.calculator:id/result_preview")).getText();
		System.out.println("El resultado es = " + result);
		return result;
	}
	
	
}
```

`TEST`

```Java
package tests;

import org.testng.Assert;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import java.net.MalformedURLException;
import java.net.URL;
import org.openqa.selenium.remote.DesiredCapabilities;
import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.remote.MobileCapabilityType;
import pages.CalculatorPage;

public class mobiletesting {
	//Inicializamos el AndroidDriver
	AndroidDriver driver;
	CalculatorPage calculatorPage;

	@BeforeTest
	public void beforeTest() throws MalformedURLException {
		
		//Configuramos los DesiredCapabilities
		DesiredCapabilities dc = new DesiredCapabilities();
		dc.setCapability(MobileCapabilityType.AUTOMATION_NAME, "uiautomator2");
		dc.setCapability(MobileCapabilityType.DEVICE_NAME, "emulator-5554");
		dc.setCapability(MobileCapabilityType.PLATFORM_NAME, "android");
		dc.setCapability(MobileCapabilityType.PLATFORM_VERSION, "12");
		dc.setCapability("appium:appPackage", "com.google.android.calculator");
		dc.setCapability("appium:appActivity", "com.android.calculator2.Calculator");
		

		//Establecemos la conexion con el server de Appium
		driver = new AndroidDriver (new URL("http://127.0.0.1:4723/wd/hub"), dc);
		System.out.println("Application started");
		
		// 
		calculatorPage = new CalculatorPage(driver);

	
	}
	
	@Test (priority = 1 ,dataProvider = "dataprovider_calc", dataProviderClass = data_provider.class)
	public void suma(int a, int b) throws InterruptedException {
		int suma = a + b;
		//Metodo para validar que la calculadora sume correctamente
		calculatorPage.clickClear();
		calculatorPage.clickDigit(a);
		calculatorPage.clickSuma();
		calculatorPage.clickDigit(b);
		int result = Integer.parseInt(calculatorPage.getResult());
		
		Assert.assertEquals(result, suma);
		
	}
	
	@Test (priority = 2 ,dataProvider = "dataprovider_calc", dataProviderClass = data_provider.class)
	public void resta(int a, int b) throws InterruptedException {
		int resta = a - b;
		//Metodo para validar que la calculadora sume correctamente
		calculatorPage.clickClear();
		calculatorPage.clickDigit(a);
		calculatorPage.clickResta();
		calculatorPage.clickDigit(b);
		int result = Integer.parseInt(calculatorPage.getResult());
		
		Assert.assertEquals(result, resta);
		
	}
	
	@Test (priority = 3 ,dataProvider = "dataprovider_calc", dataProviderClass = data_provider.class)
	public void multiplicar(int a, int b) throws InterruptedException {
		int multiplicacion = a * b;
		//Metodo para validar que la calculadora sume correctamente
		calculatorPage.clickClear();
		calculatorPage.clickDigit(a);
		calculatorPage.clickResta();
		calculatorPage.clickDigit(b);
		int result = Integer.parseInt(calculatorPage.getResult());
		
		Assert.assertEquals(result, multiplicacion);
		
	}
	

	
	@AfterTest
	public void afterTest() {
		driver.quit();
	}

}
```

</details>

