# Reto 1# - Método executeQuery()

## Objetivo

* Desarrollar clase java donde se implemente el método `executeQuery()` para realizar consultas a la base de datos MySQL.

## Desarrollo

Desarrolla una clase java donde se implemente el método `executeQuery()` para realizar consultas a la base de datos MySQL. Incluye la ejecución de varias sentencias MySQL para obtener información de la base de datos.

__Pro-Tip__: Puedes utilizar el archivo `testng.xml` para parametrizar los querys que quieras ejecutar en la etiqueta `<Test>`, por ejemplo

```Xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="Suite">
	<test name="Test1">
		<parameter name="query" value="SELECT * FROM Agendar_Cita" />
		<classes>
			<!-- Las clases que se informen en esta sección seran ejecutadas en la Suite -->
			<class name="tests.demo" />
		</classes>
	</test> <!-- Test -->
</suite> <!-- Suite -->
```


<details>
  <summary> Solución </summary>


`testng.xml`

```Xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="Suite">

	<test name="Test1">
		<parameter name="query" value="SELECT * FROM Agendar_Cita" />
		<classes>
			<!-- Las clases que se informen en esta sección seran ejecutadas en la Suite -->
			<class name="tests.demo" />
		</classes>
	</test> <!-- Test -->
	<test name="Test2">
		<parameter name="query" value="SELECT * FROM Agendar_Cita where jobTitle = 'QA'" />
		<classes>
			<!-- Las clases que se informen en esta sección seran ejecutadas en la Suite -->
			<class name="tests.demo" />
		</classes>
	</test> <!-- Test -->
	<test name="Test3">
		<parameter name="query" value="SELECT * FROM Agendar_Cita where email = null" />
		<classes>
			<!-- Las clases que se informen en esta sección seran ejecutadas en la Suite -->
			<class name="tests.demo" />
		</classes>
	</test> <!-- Test -->

</suite> <!-- Suite -->
```

`demo.java`

```Java

package tests;


import static org.testng.Assert.assertTrue;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.Statement;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class demo {
	int total = 0;
	// Creación del object de conexión
	static Connection con = null;

	// Creación del object Statement
	private static Statement stmt;
	private ResultSet res;

	// Creación de Constantes para la conexión a la Base de Datos
	public static String DB_URL = "jdbc:mysql://localhost:3306/WebAutomationTesting";
	public static String DB_USER = "root";
	public static String DB_PASSWORD = "root_pass";

	@BeforeTest
	public void setUp() throws Exception {
		try {
			// Conexión a la Base de Datos
			String dbClass = "com.mysql.cj.jdbc.Driver";
			Class.forName(dbClass);
			Connection con = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);

			// Statement object para enviar la declaración SQL a la base de datos
			stmt = con.createStatement();

		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	@Test
	@Parameters({"query"})
	public void test(String query) {

		try {

			// Definir y ejecutar la consulta a la base de datos
			res = stmt.executeQuery(query);

			// objeto ResultSetMetaData para obtener el numero de columnas de la tabla
			ResultSetMetaData rsmd = res.getMetaData();
			int columnsNumber = rsmd.getColumnCount();

			System.out.println(query);
			
			while (res.next()) {

				total++;

				for (int i = 1; i <= columnsNumber; i++) {
					System.out.print(" | " + res.getString(i));
					if (i == columnsNumber) {
						System.out.println(" | " + res.getString(i));
					}
				}
			}
		} catch (Exception e) {
			e.printStackTrace();
		}

		// asersiones
		assertTrue(total >= 1, "No se obtuvieron resultados de la consulta");

	}

	@AfterTest
	public void tearDown() throws Exception {
		if (res != null){
            res.close();
        }
		// Cerrar la conexión a la base de datos
		if (con != null) {
			con.close();
		}
		
	}

}

```

</details>



