# Reto 2 # - Métodos para procesar los resultados

## Objetivo

* Desarrollar clase java donde se implementen los métodos para procesar los resultados del objeto `ResultSet`.

## Desarrollo

Siguiendo con métodos explicado en el [**`EJEMPLO 3 - Procesamiento de Resultados.`**](./Ejemplo-03), desarrolla una clase java donde se impementen la mayor cantidad de metodos para procesar los resultados del objeto `ResultSet` proveniente de la respuesta de la consulta a la base de datos ejecutada.

Recuerda que java proporciona muchos métodos avanzados para procesar los resultados, entre ellos se encuentran los siguientes:

- `String getString()`: Se utiliza para extraer un valor  String del conjunto de resultado.
- `int getInt()`: Se utiliza para extraer un valor Int del conjunto de resultado.
- `double getDouble()`: Se utiliza para extraer un valor Double del conjunto de resultado.
- `Date getDate()`: Se utiliza para extraer un valor Date del conjunto de resultado.
- `boolean next()`: Se utiliza para moverse al siguiente registro del conjunto de resultado.
- `boolean previous()`: Se utiliza para moverse al registro anterior del conjunto de resultado.
- `boolean first()`: Se utiliza para moverse al primer registro del conjunto de resultado.
- `boolean last()`: Se utiliza para moverse al último registro del conjunto de resultado.
- `boolean absolute(int rowNumber)`: Se utiliza para moverse a un registro específico del conjunto de resultados.

> Pro-tip: puedes consultar mas metodos de esta clase en este link-> https://docs.oracle.com/javase/7/docs/api/java/sql/ResultSet.html




<details>
  <summary> Solución </summary>

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
import org.testng.annotations.Test;

public class DataDrivenTestingUsingDataBase {
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
	public void test() {

		try {

			// Definir y ejecutar la consulta a la base de datos
			String query = "SELECT * FROM Agendar_Cita";
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

Donde:
- `res.next()`: es usado junto el ciclo while para recorrer todos los registros de la colsulta ejecutada.
- `res.getString(i)`: es usado para obtener el string del resultado segun la columna indicada con el valor `i`
- `res.close()`: cierra el ResultSet object.
- `res.getMetaData()`: es usado para obtener el numero de columnas del ResultSet object.

</details>