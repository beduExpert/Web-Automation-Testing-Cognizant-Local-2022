# Reto 04# - Afirmación suave (Soft Assert)

## Objetivo

* Identificar la importancia del metodo `assertAll()` en las Afirmación suave (Soft Assert)

## Desarrollo

Crea una nueva clase que se llame __reto_06__ en tu proyecto e importa este código:

```Java
package com.bedu.web_automation_course;

import org.testng.annotations.Test;
import org.testng.asserts.SoftAssert;

public class reto_06 {
	//Creación del objecto SoftAssert
    SoftAssert obj_softAssert = new SoftAssert();
    
    @Test(priority=1)
    public void test1() {
        obj_softAssert.assertEquals(true, false);
    }

}
```

<details>
  <summary>¿Es correcto el funcionamiento esperado? </summary>
  > No, las condiciones enviadas a la asercion son distintas y en el resultado de la ejecución no marca como fallido el caso de prueba.
</details>


<details>
  <summary>¿Como mejorarias el script?</summary>
  > Agregando la llamada al metodo `assertAll()` --> obj_softAssert.assertAll(); 
</details>
