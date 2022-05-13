# Reto 2 # - Implementación de Selenium Grid

## Objetivo

* Construir nuevos scripts de pruebas automatizados donde se implemente la ejecución en máquinas remotas con Selenium Grid.

## Desarrollo

Adapta el script de prueba automatizado de la clase `SeleniumGrid` para que sea ejecutada de forma remota en el navegador `google chrome`.

<details>
  <summary> Solución </summary>

```Java
	@BeforeTest
	public void beforeTest() throws MalformedURLException{
		//Seteamos la propiedad del sistema para firefox
		System.setProperty("webdriver.chrome.driver", "src/test/resources/webdrivers/chromedriver");
		//creamos el objeto DesiredCapabilities
		DesiredCapabilities capability = new DesiredCapabilities();
		// le configuramos el navegador y la plataforma
		capability.setBrowserName("chrome");
		capability.setPlatform(Platform.MAC);
		// asignamos el RemoteWebDriver enviadole el objeto capability y la nodeURL
		driver = new RemoteWebDriver(new URL(nodeURL), capability);

	}
```
</details>



