# Ejemplo-02 # - Envío de Querys

## Objetivo

- Utilizar el metodo `executeQuery()` para realizar consultas a las bases de datos.
- Adaptar los scripts de pruebas para que consuman los datos provenientes de la ejecución de Querys en la Base de datos.

## Desarrollo

#### ¿Qué es un query o consulta a una base de datos?

Una `Query (Consulta) es un lenguaje de consulta estructurado`, es decir, son consultas realizadas a la base de datos  que ejecuta usan SQL en segundo plano.  Al comprender mejor este lenguaje se podrá crear mejores consultas además de facilitar la forma de solucionar una consulta que no devuelve los resultados que quiere.

#### Tipos de Consulta a base de datos

Las operaciones básicas utilizadas para la manipulación de datos que podemos realizar con SQL se les denomina operaciones `CRUD (de Create, Read, Update and Delete)` o sea, Crear, Leer, Actualizar y Borrar en español.

<img src="assets/crud.png" width="40%"> 

Traduciendo esto en tipo de sentencia SQL tendremos lo siguiente:

- `INSERT`: Agrega uno o varios registros a una tabla. Se corresponde con la `“C”` de CRUD.

- `SELECT`: Es la `“R”`, muestra información sobre los datos almacenados en la base de datos. Dicha información puede pertenecer a una o varias tablas. Una instrucción SELECT contiene una descripción completa de un conjunto de datos que quiere obtener de una base de datos. Se incluye lo siguiente:
    - Qué tablas contienen los datos.
    - Cómo se relacionan los datos de orígenes diferentes.
    - Qué campos o cálculos proporcionarán los datos.
    - Criterios que los datos deben cumplir para ser incluidos.
    - Si se deben ordenar los datos y, en caso de ser así, cómo deben ordenarse.

- `UPDATE`: Actualiza información de una tabla. Es, obviamente, la `“U”`. Esta instrucción no genera un conjunto de resultados, por lo que después de actualizar los registros mediante una consulta de actualización, la operación no se puede deshacer. 

- `DELETE`: Borra filas de una tabla. Se corresponde con la `“D”`. Esta sentencia ​​solo se eliminan los datos; la estructura de tablas y todas las propiedades de tabla, como los atributos de campo y los índices, permanecen intactos.

#### Implementación de Querys con Selenium

Siguiendo el ejemplo anterior y una vez que se realiza la conexión, es posible ejecutar consultas a la base de datos ya conectada a nuestro código, para ello la librería dispone de un objeto de tipo ‘statement’ o ‘declaración’, que es utilizado para enviar consultas a la base de datos.

Mediante el siguiente código:

```Java
Statement stmt = con.createStatement();
```
> El método `createStatement()` se utiliza para crear un objeto que modela una sentencia SQL. Es un objeto del tipo de una clase que implementa la interfaz `Statement`, y provee la infraestructura para ejecutar sentencias SQL sobre una conexión con una base de datos.

Una vez que se crea el objeto de declaración, se utiliza el método `executeQuery` para ejecutar las consultas SQL:

```Java
String query = "SELECT * FROM Agendar_Cita";
ResultSet res = stmt.executeQuery(query);
```
El método `executeQuery()` se utiliza para ejecutar una instrucción `SELECT`, que es casi la instrucción SQL más utilizada. 

Pero tambien existen otros metodos como: 

- `executeUpdate()` que se utiliza para ejecutar instrucciones `INSERT`, `UPDATE` o `DELETE` y sentencias SQL `DDL (lenguaje de definición de datos)`, como `CREATE TABLE` y `DROP TABLE`.

- `execute()` que se utiliza para ejecutar una declaración que devuelve múltiples conjuntos de resultados, múltiples recuentos de actualizaciones o una combinación de ambos.


#### Querys utiles para los scripts de Pruebas con Selenium

La utilidad de los querys va a depender de la funcionalidad a automatizar. Pero ademas de la consulta que retornara todos los registros de la tabla:

```Java
String query = "SELECT * FROM Agendar_Cita";
ResultSet res = stmt.executeQuery(query);
```

Podriamos ejecutar otras consultas que nos ayuden en nuestros proyectos como por ejemplo:

- `Obtener la cantidad de registros de la tabla`: esto nos puede servir por ejemplo para ver si se ha insertado un nuevo valor a la tabla, comparando cuantos registos tenia antes de la ejecución y cuantos tiene despues:

```Java
String query = "SELECT count(*) FROM Agendar_Cita";
ResultSet res = stmt.executeQuery(query);
```

- `Obtener los registros según una condicion dada`: es util  cuando queremos extraer datos con una condicion por ejemplo para un formulario de login, consultamos la BD para buscar registros que no tengan `contraseña`.

```Java
String query = "SELECT * FROM Agendar_Cita where email = null";
ResultSet res = stmt.executeQuery(query);
```