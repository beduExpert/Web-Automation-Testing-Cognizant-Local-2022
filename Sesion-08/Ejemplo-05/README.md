# Ejemplo-05 # - Automatización de Gestos Móviles

## Objetivo

- Utilizar los objetos TouchAction/MultiAction para la automatización de gestos móviles. 

## Desarrollo

En cuanto a la automatización de gestos móviles, si bien la especificación `Selenium WebDriver` es compatible con ciertos tipos de interacción móvil, sus parámetros no siempre se pueden asignar fácilmente a la funcionalidad que proporciona la automatización del dispositivo subyacente (como UIAutomation en el caso de iOS). 
Con ese fin, Appium implementa la nueva API `TouchAction/MultiAction.``

#### TouchAction
Los objetos `TouchAction` contienen una cadena de eventos. En todas las bibliotecas cliente de appium, los objetos táctiles se `crean y reciben una cadena de eventos`.

Los eventos disponibles de la especificación son: 
* `press`: pulsa una acción en la pantalla.
* `release`: retira el toque actual de la pantalla.
* `moveTo`: mueve el toque actual a una nueva posición.
* `tap`: toca en una posición o elemento
* `wait`: espera a que transcurra la cantidad de tiempo especificada antes de continuar con la siguiente acción táctil.
* `longPress`: mantiene presionado en el centro de un elemento hasta que se active el evento del menú contextual.
* `cancel`: cancela la acción si `performsTouchActions` la completó parcialmente.
* `perform`: realiza una cadena de acciones en `performsTouchActions`.

> Documentación oficial de la clase TouchAction: https://www.javadoc.io/doc/io.appium/java-client/7.0.0/io/appium/java_client/TouchAction.html


####  MultiAction

Los objetos `MultiTouch` son colecciones de `TouchActions`. Los gestos `MultiTouch` solo tienen dos métodos, `add` y `perform`. 
- `add` se usa para agregar otra TouchAction a este MultiTouch.
- `perform` cuando este metodo es llamado, todas las TouchActions que se agregaron al MultiTouch se envían a appium y se ejecutan como si ocurrieran al mismo tiempo. 


Appium primero realiza el primer evento de todas las TouchActions juntas, luego el segundo, etc.


__Ejemplo__

```Java
package pages;

import static io.appium.java_client.touch.TapOptions.tapOptions;
import static io.appium.java_client.touch.WaitOptions.waitOptions;
import static io.appium.java_client.touch.offset.ElementOption.element;
import static io.appium.java_client.touch.offset.PointOption.point;
import static java.time.Duration.ofMillis;
import static java.time.Duration.ofSeconds;

import io.appium.java_client.MobileElement;
import io.appium.java_client.MultiTouchAction;
import io.appium.java_client.TouchAction;
import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.android.AndroidElement;
import org.openqa.selenium.Dimension;

public class MobileActions {
    private AndroidDriver<MobileElement> driver;

    public MobileActions (AndroidDriver driver) {
        this.driver = driver;
    }

    //Tap sobre un elementofor 2 segundos
    public void tapByElement (AndroidElement androidElement) {
        new TouchAction(driver)
            .tap(tapOptions().withElement(element(androidElement)))
            .waitAction(waitOptions(ofMillis(200))).perform();
    }

    //Tap por coordenadas
    public void tapByCoordinates (int x,  int y) {
        new TouchAction(driver)
            .tap(point(x,y))
            .waitAction(waitOptions(ofMillis(250))).perform();
    }

    //Press por elementos
    public void pressByElement (AndroidElement element, long seconds) {
        new TouchAction(driver)
            .press(element(element))
            .waitAction(waitOptions(ofSeconds(seconds)))
            .release()
            .perform();
    }

    //Press por coordenadas
    public void pressByCoordinates (int x, int y, long seconds) {
        new TouchAction(driver)
            .press(point(x,y))
            .waitAction(waitOptions(ofSeconds(seconds)))
            .release()
            .perform();
    }

    //Horizontal Swipe
    public void horizontalSwipeByPercentage (double startPercentage, double endPercentage, double anchorPercentage) {
        Dimension size = driver.manage().window().getSize();
        int anchor = (int) (size.height * anchorPercentage);
        int startPoint = (int) (size.width * startPercentage);
        int endPoint = (int) (size.width * endPercentage);

        new TouchAction(driver)
            .press(point(startPoint, anchor))
            .waitAction(waitOptions(ofMillis(1000)))
            .moveTo(point(endPoint, anchor))
            .release().perform();
    }

    //Vertical Swipe
    public void verticalSwipeByPercentages(double startPercentage, double endPercentage, double anchorPercentage) {
        Dimension size = driver.manage().window().getSize();
        int anchor = (int) (size.width * anchorPercentage);
        int startPoint = (int) (size.height * startPercentage);
        int endPoint = (int) (size.height * endPercentage);

        new TouchAction(driver)
            .press(point(anchor, startPoint))
            .waitAction(waitOptions(ofMillis(1000)))
            .moveTo(point(anchor, endPoint))
            .release().perform();
    }

    //Swipe
    public void swipeByElements (AndroidElement startElement, AndroidElement endElement) {
        int startX = startElement.getLocation().getX() + (startElement.getSize().getWidth() / 2);
        int startY = startElement.getLocation().getY() + (startElement.getSize().getHeight() / 2);

        int endX = endElement.getLocation().getX() + (endElement.getSize().getWidth() / 2);
        int endY = endElement.getLocation().getY() + (endElement.getSize().getHeight() / 2);

        new TouchAction(driver)
            .press(point(startX,startY))
            .waitAction(waitOptions(ofMillis(1000)))
            .moveTo(point(endX, endY))
            .release().perform();
    }

    //Accion Multitouch
    public void multiTouchByElement (AndroidElement androidElement) {
        TouchAction press = new TouchAction(driver)
            .press(element(androidElement))
            .waitAction(waitOptions(ofSeconds(1)))
            .release();

        new MultiTouchAction(driver)
            .add(press)
            .perform();
    }
}

```


