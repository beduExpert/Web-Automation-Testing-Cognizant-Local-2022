## Sesi贸n 3: Page Object Model (POM) 馃


<div style="text-align: justify;">

### 1. Objetivos :dart: 

- Distinguir los distintos patrones de dise帽o de automatizaci贸n que podemos aplicar en nuestros scripts de pruebas.
- Identificar el Page Object Model como un patr贸n de dise帽o efectivo para desarrollar pruebas automatizadas.
- Adaptar el patr贸n page object model (POM) en los scripts de pruebas automatizados.


### 2. Contenido :blue_book:

Hasta ahora hemos visto c贸mo desarrollar scripts de pruebas automatizados, usando localizadores de selenium para identificar los elementos de la pantalla para realizar acciones sobre ellos, pero si analizamos un poco el c贸digo que hemos realizado nos daremos cuenta que si queremos modificar alg煤n localizador en las distintas clases, tendremos que entrar a cada una de ellas y realizar este cambio, esto no solo puede llevar mucho tiempo, sino tambi茅n un grave factor de desmotivaci贸n cuando se trata de implementar pruebas automatizadas desde el principio. Es por ello que surge una pregunta, __驴qu茅 pasar铆a si pudi茅ramos realizar el cambio en un solo lugar y hacer que todas las pruebas relevantes lo utilicen?__

En esta sesi贸n analizaremos c贸mo podemos usar el patr贸n de dise帽o `Page Object Model` para escribir scripts de pruebas que se puedan mantener y reutilizar. 

---

#### <ins>Tema 1: Patrones de dise帽o de automatizaci贸n</ins> 

Conoceremos sobre que son los patrones de dise帽o de automatizacion de pruebas y sus tipos, si bien solo nos enfocaremos en este modulo en el patr贸n de dise帽o `Page Object Model` es importante conocer que existen otros patrones y cuales son sus usos y ventajas.

<img src="assets/patrones.png" width="60%"> 

- [**`EJEMPLO 1 - Patrones de dise帽o de automatizaci贸n`**](./Ejemplo-01)

---

#### <ins>Tema 2: Page Object Model (POM)</ins> 

`Page Object Model` es un __patr贸n de dise帽o__ que se ha vuelto popular en la automatizaci贸n de pruebas para mejorar el mantenimiento de las pruebas y __reducir la duplicaci贸n de c贸digo__. Un `objeto de p谩gina (page object)` es una clase orientada a objetos que sirve como interfaz para una p谩gina, luego, las pruebas usan los m茅todos de esta clase de objeto de p谩gina cada vez que necesitan interactuar con la interfaz de usuario de esa p谩gina. 

El beneficio es que __si la interfaz de usuario cambia para la p谩gina, las pruebas en s铆 mismas no necesitan cambiar__, solo el c贸digo dentro del objeto de la p谩gina debe cambiar. Posteriormente, todos los cambios para admitir esa nueva interfaz de usuario se ubican en un solo lugar.

<img src="assets/pom.png" width="40%"> 

- [**`EJEMPLO 2 - Page Object Model (POM)`**](./Ejemplo-02)
- [**`RETO 1`**](./Reto-01)
---

#### <ins>Tema 3: Implementaci贸n de POM en Selenium</ins>

En este tema abordaremos con ejercicios practicos como implementar `Page Object Model` en nuestros proyectos de automatizaci贸n de Pruebas.

- [**`EJEMPLO 3 - Implementaci贸n de POM en Selenium`**](./Ejemplo-03)
- [**`RETO 2`**](./Reto-02)
---

### 3. Postwork :memo:

Encuentra las indicaciones y consejos para reflejar los avances de tu proyecto de este m贸dulo.

- [**`POSTWORK SESI脫N 3`**](./Postwork/)

<br/>


</div>

