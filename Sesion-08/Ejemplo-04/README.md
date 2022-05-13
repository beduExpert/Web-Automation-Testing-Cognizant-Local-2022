# Ejemplo-04# - Localizadores

## Objetivo

- Comparar cómo se obtienen los localizadores en plataformas móviles vs los de plataformas web.

## Desarrollo

Appium admite un subconjunto de las estrategias de localización de WebDriver como:

- Buscar por `"clase"` (es decir, tipo de componente ui)
- Encontrar por `"xpath"` (es decir, una representación abstracta de una ruta a un elemento, con ciertas restricciones)


Appium también es compatible con algunas de las estrategias de localización de `Mobile JSON Wire Protocol`.

#### WebElement vs MobileElement

Puede resultar un poco confuso los 2 elementos de tipo `WebElement` y `MobileElement`. La diferencia entre ambos es
basicamente la siguiente: al usar un elemento de tipo  `WebElement` te permitirá usar todos los comandos normales de `Selenium`. 

Sin embargo, `MobileElement` es el elemento de appium que subclasifica a WebElement y agrega características específicas de appium (como poder realizar gestos táctiles).

Adicionalmente existe elementos de tipo `AndroidElement` e `IOSElement` que implementan `MobileElement` y agregan funciones específicas del sistema operativo, como por ejemplo, en Android, puede el usar `findByUIAutomator` y en iOS puede usar `findByUIAutomation`

#### Estrategias de selección de elementos en dispositivos móviles

Las estrategias de localización de elementos en dispositivos móviles son similares a las que se utilizan para elementos webs. Aca se detallan en el orden de prioridad de localización:

- `ID`: Identificador del elemento nativo. 

```Java
driver.findElement(By.id("com.google.android.calculator:id/digit_7"));
```

- `Name`: nombre del elemento.

```Java
driver.findElement(By.name("name"));
```

- `Android UiAutomator (solo UiAutomator2)`: use la API de `UI Automator`, en particular, la clase `UiSelector` para ubicar elementos. En Appium envías el código Java, como una cadena, al servidor, que lo ejecuta en el entorno de la aplicación, devolviéndote el elemento o elementos. 
> https://developer.android.com/reference/android/support/test/uiautomator/UiSelector.html

```Java
WebElement element = driver.findElementByAndroidUIAutomator("new UiSelector().index(0)");
```

- `Nombre de clase`: nombre completo de la clase.

```Java
driver.findElement(By.className("android.widget.Button"));
```

- `XPath`: busca la fuente XML de la aplicación usando xpath. ¡Cuidado!: no recomendado ya que tiene problemas de rendimiento.

```Java
driver.findElement(By.xpath("/hierarchy/android.widget.FrameLayout/android.widget.FrameLayout/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.view.ViewGroup/android.widget.Button[9]"));

```


En conclusion la localización de elementos para mobile es muy parecida a la localizacion en plataformas web, ya que ambas comparten el uso de `Selenium`

