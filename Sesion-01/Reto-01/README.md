# Reto #1: Dependencias Selenium

## Objetivo

- Analizar el comportamiento en la ejecución del script de prueba cuando no se importan las librerias de selenium webdriver.

## Desarrollo

Ahora que sabes como funciona la integración de Selenium con el IDE, copia este contenido en tu archivo pom.xml y ejecuta tu script de pruebas.

#### Ejemplo del archivo pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.bedu.web_automation_course</groupId>
  <artifactId>BeduWebAutomationCourse</artifactId>
  <version>0.0.1-SNAPSHOT</version>

  <dependencies>
	<!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
	<dependency>
	    <groupId>org.seleniumhq.selenium</groupId>
	    <artifactId>selenium-java</artifactId>
 		<scope>test</scope>
	</dependency>
    
	<!-- https://mvnrepository.com/artifact/org.testng/testng -->
	<dependency>
	    <groupId>org.testng</groupId>
	    <artifactId>testng</artifactId>
	    <version>7.4.0</version>
	    <scope>test</scope>
	</dependency>


  </dependencies>
</project>

```

#### 1. ¿Puedes identificar cual es el error?
#### 2. ¿Puedes solucionarlo?

<details>
  <summary>Solución 1 </summary>
  > La dependencia de selenium en el archivo pom.xml no tiene la versión. por ende cuando se ejecuta el proyecto, maven no es capaz de importarlas correctamente, esto genera un error.
</details>

<details>
  <summary>Solución 2 </summary>
  > Agregar la version de selenium al archivo pom.xml
    
   ```xml 
	<dependency>
		<groupId>org.seleniumhq.selenium</groupId>
		<artifactId>selenium-java</artifactId>
		<version>4.1.2</version>
 		<scope>test</scope>
	</dependency>
   ```
</details>
