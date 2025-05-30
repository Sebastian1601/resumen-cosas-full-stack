
# Indice




---

# Utilizando XAMMP -

-para asignar una clave al usuario root, se puede realizar de distintas maneras.

-Usar el shell de XAMPP es generalmente el método más simple y rápido para cambiar tu contraseña de MySQL. Implica el uso de la línea de comandos, lo que puede parecer desalentador al principio.

-Sin embargo, en realidad es bastante sencillo. Este es también el método que querrás utilizar si has olvidado tu contraseña de MySQL y necesitas restablecerla.

-Ten en cuenta que estos comandos son los mismos tanto si usas Windows como macOS. Dado que este es un shell único y específico de XAMPP, cualquier diferencia típica entre las plataformas no se aplicará.

-Para empezar, inicia tu Panel de Control de XAMPP y haz clic en el botón Shell en el lado derecho.-

-Esto abrirá una nueva ventana con un símbolo del sistema. Introduce el siguiente comando y pulsa la tecla Enter/Return:

    mysqladmin -u root password

-El intérprete de comandos te pedirá que introducir una nueva contraseña. Pulse Enter/Return de nuevo, y se te pedirá que confirmes la nueva contraseña.

-Una vez que lo hayas hecho, habrás terminado y podrás cerrar la ventana del shell.

> Esto puede generar que phpMyAdmin no abra más al acceder a http://127.0.0.1, y de un error que indica que los datos de la clave no coinciden.

para resolver esto, debemos buscar el archivo siguiente:

    (archivodeinstalacionXampp)/mySql/bin/config.inc.php

y en ese archivo, modificamos con la nueva clave la siguiente parte en 'YourPassword':

    $cfg['Servers'][$i]['password'] = 'YourPassword';


---

# Instalar SQLite3 opcional a XAMMP -

- descargamos el paquete de Precompiled binaries for Windows.
- en particular, descargamos *sqlite-tools-win-x64-3460000.zip*
- luego de descargar el zip, creamos una carpeta en el disco donde está instalado windows.
- extraemos.
- abrimos **Editar las variables del entorno del sistema**.
- Abrimos las *"Variables de entorno"*.
- Abrimos la variable llamada *"Path"*.
- creamos una *nueva* variable de ruta, colocando la dirección de la carpeta donde descomprimimos el zip con los archivos de sqlite. `ej: c:/sqlite3`
  ---
 - Ahora descargamos *"SQLite Browser"*
 - Buscamos la versión según nuestra pc.
      `(DB Browser for SQLite - Standard installer for 64-bit Windows)`
 - Luego de instalado el browser, ya se puede abrir para manejar desde ahi las bases.
 ---

## MySQL

#### Tipos de cláusulas

Al trabajar con lenguaje SQL, tenemos que tener en cuenta los distintos tipos de comandos que podemos ejecutar.
Se agrupan en 5 grandes conjuntos.

- DDL [Data Definition Language]
	CREATE | DROP | ALTER | TRUNCATE

- DQL [Dat Query Language]
	SELECT

- DML [Data Manipulation Language]
	INSERT | UPDATE | DELETE | EXPLAIN CALL

- DCL [Data Control Language]
	COMMIT | SAVEPOINT | ROLLBACK

- TCL [Transaction Control Language]
	GRANT | REVOKE


>[!info] Entidad:
>- Es una representación de algo.
>- Para representarlos se utiliza la *Notación de chen*.
>- Para representarlas, se utiliza un sustantivo dentro de un cuadrado.
> -  Una entidad está definida por sus propiedades. Se representan con un óvalo.
> - Las entidades se componen por atributos simples, atributos compuestos, atributos multivalor, y atributos derivados.


## Tablas

 *Tabla* : Es una estructura de datos, organizada en filas y columnas.

 _Campo_ : Es el nombre que tiene una columna en una base de datos.

 _Registro_ : Es un grupo de campos que hacen referencia a un elemento en la base.

 _Valor del campo_ : Es el valor que tiene un campo en particular para un registro particular.

  Al definir un campo, tenemos que definir qué tipo de datos va a almacenar.
  Existen varios tipos de datos, los más utilizados son:
- *Varchar* (cantidad de digitos hasta 255 máximo)
- *Integer* (nro.entero)
- *Text*    (texto libre / ocupa más espacio en la base) 
- *Blob*    (archivos binarios varios, imágenes, videos, etc)
- *Real*    (nros con coma flotante, porcentajes, etc) más rápido, menos precisión en los nros.
- *Decimal* (cant nro entero, cant nro decimal) decimales, por ej decimal(1,1) = 9,3 pero NO 10,1
- *Numeric* (nros matemáticos precisos) de cualquier tamaño
- *BINARY* (datos binarios, por ejemplo los UUID())
---
### Opciones especiales de los campos.

`default (valor)` - esto se usa en un campo para indicar que si no se pasa el valor al insertar un dato, se genere un valor "por defecto" el cual figura dentro de los paréntesis
ej: `IDusuario BINARY(16) PRIMARY KEY DEFAULT(UUID_TO_BIN(UUID))`
*esto indica que el campo idusuario, es
* binario de 16bits
* clave primaria 
* por defecto, si no le enviamos un dato al crear un registro, se genere un id universal unico(uuid), el cual se pasará a binario mediante la funcion UUID_TO_BIN() y se guardará.*

`UUID()` : función de SQL que se usa para generar un ID Universal Unico, se utiliza la sentencia 
`SELECT UUID();` y esto crea el valor.

`UUID_TO_BIN()`: esta funcion va acompañada del argumento UUID() para crear el id, y pasarlo a formato binario de 16 bits, y tener un registro único para ese elemento de la base.

`UNSIGNED` : determina que el valor a ingresar, debe ser positivo, sin signo ni valor negativo.

### Oden de las sentencias para generar una consulta (query)

Cada consulta comienza por determinar los datos que necesitamos en la base, y luego, filtrarlos en algo que pueda ser procesado y entendido lo más rápido posible. Gracias a que cada parte de la query es ejecutada secuencialmente, es importante entender el orden de ejecución asi uno puede saber qué datos están disponibles en qué momento.

Una query completa, tiene la siguiente sintaxis

```sql
Complete SELECT query

`SELECT DISTINCT column, AGG_FUNC(_column_or_expression_), … 
FROM mytable 
JOIN another_table 
ON mytable.column = another_table.column 
WHERE _constraint_expression_ 
GROUP BY column 
HAVING _constraint_expression_ 
ORDER BY _column_ ASC/DESC 
LIMIT _count_ 
OFFSET _COUNT_;`
```

#### Orden de ejecución de los distintos pasos de la query.

1. **FROM y JOIN's**
	La cláusula FROM y subsecuentemente JOIN, son las primeras en ejecutarse para determinar el total de los datos a trabajar (*por eso al hacer un join, en el select ya se pueden definir todos los campos necesarios a "traer" de ambas tablas*) 
	Esto incluye subconsultas, y puede causar que temporalmente se construyan tablas "ocultas" conteniendo todas las filas y columnas de las tablas siendo "unidas".

2. **WHERE**
	Una vez que tenemos todos los datos de la consulta, se aplica la condición del WHERE individualmente a cada registro, y los que no satisfacen la misma, son desechados. Cada una de las condiciones puede acceder a datos requeridos inicialmente en el FROM. Los **ALIASES** del SELECT generalmente no son accesibles en la mayoría de bases de datos, dado que pueden incluir expresiones dependientes de partes que la consulta quizás todavia no haya ejecutado.

3. **GROUP BY**
	Los registros resultantes que efectivamente cumplieron la condicion del WHERE son agrupados basados en valores comúnes de la columna especificada en el GROUP BY. Como resultado, habrán una cantidad de filas única como los valores únicos que tienen la columna indicada. I**MPLICITAMENTE, esto significa que deberías usar esto SOLO cuando tienes funciones de agregación en la consulta**.

4. **HAVING**
	Si la consulta tiene una cláusula GROUP BY, entonces las condiciones en el HAVING son aplicadas a los grupos de filas, y se descartan los grupos que no satisfacen la condición.
	ALIASES no son accesibles tampoco desde este punto, como en el WHERE.

5. **SELECT**
	Finalmente, cualquier expresión en la parte SELECT es ejecutada y computada.

6. **DISTINCT** 
	De las filas resultantes luego de todo lo anterior, las duplicadas serán descartadas.

7. **ORDER BY**
	Si una cláusula ORDER BY está escrita, las filas restantes son ordenadas de manera ASCENDETE(por defecto) o DESCENDENTE de acuerdo a la misma.
	*AQUI SI SE PUEDE REFERENCIAR una columna por su alias, dado que ya el select se ha ejecutado.*

8. **LIMIT / OFFSET**
	Finalmente, las filas resultantes que caigan fuera del rango indicado por el LIMIT y el OFFSET son descartadas, dejando el resultante final de registros para mostrar como resultado.

### Creación de base, tabla y uso.

muestra las bases de datos activas.
`SHOW DATABASES;`

crea la base de datos que indicamos.
`CREATE SCHEMA IF NOT EXISTS [nombre];`

usar la tabla de nombre [nombre_de_la_base]
`USE [nombre_de_la_base]`


>[!tip] Sentencia para crear una tabla (ya dentro de la base de datos)
```sql
CREATE TABLE "[nombre]" (
 	"nombre de campo1" [tipo de campo],
  	"nombre de campo2" [tipo de campo],
        .			                  ,	
  		.			                  ,
    	.	      		              ,
   "nombre de campoN" [tipo de campo],
   PRIMARY KEY("nombre de campoX", AUTOINCREMENT)
       )
```


Para ver la estructura de una tabla, se usa la sentencia 
```sql
DESCRIBE [nombre de base].(nombre de tabla);
```

Ejemplo:
```sql
DESCRIBE twitter_db.tabla_usuarios;
```



#### Propiedades habituales de los capos definidos en la tabla

Tipos de datos para los campos:

**Numéricos**

|   tipo    | descripción                                        |
| :-------: | :------------------------------------------------- |
|    INT    | num entero                                         |
|  TINYINT  | num entero                                         |
|  BIGINT   | num entero                                         |
|   FLOAT   | num con coma flotante                              |
|   REAL    | num real.                                          |
|   BOOL    | boolean(true/false)                                |
|   DATE    | datos en formato fecha(YYYY-MM-DD)                 |
|   TIME    | datos en formato hora(HH:MM:SS)                    |
| DATETIME  | datos en formato fecha y hora(YYYY-MM-DD HH:MM:SS) |
| TIMESTAMP | valor de los segundos pasados desde época Unix     |
|   YEAR    | datos del año en formato de 2 o 4 dígitos          |

**Carácteres**

|      tipo       | descripción                                                      |
| :-------------: | ---------------------------------------------------------------- |
|     DECIMAL     | datos formato decimal, con coma                                  |
| VARCHAR(nroCar) | cadenas de texto acotadas en longitud                            |
|      CHAR       | tipo de datos longitud fija de máximo 8k carácteres              |
|      TEXT       | tipo de datos texto variable en longitud de tamaño máximo de 2GB |


**SQL unicode character y string tipo de datos.**

|   tipo   | descripción                               |
| :------: | ----------------------------------------- |
|  NCHAR   | longitud fija de 4k carácteres            |
| NVARCHAR | longitud variable de máximo 4k carácteres |
|  NTEXT   | longitud varibale de máximo 1Gb datos     |


**SQL misc data types**

| tipo | descripción                          |
| :--: | ------------------------------------ |
| CLOB | obj. de carácteres grandes hasta 2Gb |
| BLOB | obj. binarios grandes                |
| XML  | guardar datos xml                    |
| JSON | guardar datos en formato Json        |


#### Limitaciones (CONSTRAINS) en la definición de columnas, y tablas.

- **NOT NULL** : indica que el campo no puede tener valor NULL al crearse o modificarse un registro.

- **UNIQUE** : indica que el campo será único entre los registros, aparte del id que suele ser autoincrementable.

- **PRIMARY KEY** : una combinación de NOT NULL y UNIQUE. identifica inequívocamente un registro de la tabla.

- **FOREIGN KEY** : evita acciones que destruirían el vínculo entre tablas.
	Las Foreign Key aseguran que el valor ingresado en el campo determinado como foreign key, exista en el campo al que hacen referencia.
	Ejemplo:
```sql
CREATE TABLE followers (
	follower_id int not null,
    following_id int not null,
    Foreign key(follower_id) REFERENCES users(user_id),
    Foreign key(following_id) REFERENCES users(user_id),
    Primary Key(follower_id, following_id)
    );
	```

Esto nos asegura que lo que se ingresa en follower_id como following_id, es un valor que existe en el campo user_id de la tabla Users.-

- **CHECK** : determina que los valores en una columna satisfacen una condición específica.
	Ejemplo:
	
	```sql
	CREATE TABLE seguidores (
	  id SERIAL PRIMARY KEY,
	  follower_id INT NOT NULL,
	  following_id INT NOT NULL,
	  CONSTRAINT evitar_self_follow CHECK (follower_id <> following_id)
	);``` 
	Esto evita que ambos valores en la tabla sean iguales, evitando que un usuario sea su propio seguidor. 

- **DEFAULT(valor o función)** : setea un valor por defecto si no se especifica alguno en el ingreso de registro.

- **CREATE INDEX**:

- **AUTO_INCREMENT** : indica que el campo incrementará automáticamente su valor al crearse un registro.

>[!info] Información importante
>Para agregar una restricción a un campo, luego de creada la tabla, se puede utilizar la siguiente sintaxis 
>```
>ALTER TABLE [nombre_de_tabla] ADD [restricción_a_agregar] (campo_al_cual_agregarle_la_restricción)
>```

Ejemplo:
```sql
ALTER TABLE users ADD UNIQUE(last_name);
```


Para ==eliminar== una restricción a un campo, luego de creado, se utiliza la siguiente sintaxis:

```sql
ALTER TABLE [nombre_tabla] DROP INDEX [nombre_campo_a_eliminar_restricciones]
```

Ejemplo:
`ALTER TABLE users DROP INDEX last_name;`

*Para ==eliminar== una restricción de ==PRIMARY KEY== en un campo ya creado se usa:

```sql
ALTER TABLE [nombre_de_tabla] DROP PRIMARY KEY;
```

---

### Sentencias de busqueda inicial

Mostrar todos los datos de la tabla 'usuarios'
 
 `select * from users` 
- select : selecciona,
- *         : símbolo que significa "todo",
- from   : desde,
- users  : es el nombre de la tabla donde buscar.
---
### Sentencia de ingreso de un registro

ingresar un registro de usuario en la tabla 'usuarios'

`insert into usuarios (nombre, apellido, edad) values ('Juan', 'Giordano', '21')`

- insert : ingresá,
- into : en la siguiente tabla,
- usuarios : nombre de la tabla,
- (nombre, apellido, edad) : nombre de los campos a ingresar,
- values : los siguientes valores,
- ('Juan', 'Giordano', '21') : valores a ingresar en cada campo descripto antes.


> Se pueden generar un insert con varios registros, de la siguiente manera:

 ```sql
insert into usuarios (nombre, apellido, edad) 
    values  ('Claudia', 'Caceres','44'),
	    	('Daiana','Congregado','17'),
		    ('Ariel','Berneto','25'),
		    ('Juan Jose','Campagnolo','37')
```

> Se puede insertar un registro, o varios, y generar una consulta justamente luego del insert, separando las declaraciones con ; (punto y coma).

 ```sql
insert into usuarios (nombre, apellido, edad)
 values ('lucas', 'dalto', 21);
 select * from usuarios
```

### Seleccionar ciertos campos de la tabla

se ingresa la sentencia 

    select campo1, campo2, ..., campon from tabla1

ej:

    select nombre, edad, apellido from usuarios

---
## Identificadores
 Son datos específicos que se utilizan para identificar inequívocamente a un único registro.

 existen identificadores **"primarios"** y **"foráneos"**.
 Normalmente los identificadores _"primarios"_ es un campo especial que se utilizan para ubicar uno y solo un registro en toda la base de datos.

 
Los identificadores _"Foráneos"_  son campos de una tabla que hacen referencia a _'identificadores primarios'_ de otra tabla, para establecer una relación entre los registros.

> ⚠️ Una tabla puede tener muchos identificadores foráneos(FK), haciendo referencia a PK(claves primarias) de otras tablas, pero SOLO puede tener una PK


# Sentencias de busquedas intermedias

- `as` Asignar _Alias_ al nombre de un campo. (as)

En la sentencia SQL al buscar en una tabla, podemos "renombrar" temporalmente un campo, de la siguiente manera:

`select LastName AS apellido FROM emplpoyees`

otro ej:

`select LastName AS Apellidos, FirstName as Nombre from employees`

- Realizar "funciones" en una busqueda:

`select price as precioOriginal, price*2 as precioDoble from Products`

> nótese que se multiplica por 2 los datos del campo price, y se asignan con el alias preciodoble, desde la tabla productos.



- Ordenar busquedas de manera descendente y ascendente (order by ==campo== ASC / DESC)

      SELECT * FROM Products ORDER BY price


| tipo de dato          | Orden Ascendente |
| --------------------- | ---------------- |
| numeros               | 0 - 9            |
| texto                 | null             |
| numeros               |                  |
| carácteres especiales |                  |
| letras                |                  |
| blob                  | no hay orden     |

  
#### NULLS FIRST, NULLS LAST Al ordenar los datos se puede determinar que se muestren los elementos con campos NULLS al principio con FIRST, o al final con LAST, dependiendo de qué orden se elija.

  ej:
  
	  SELECT * FROM Products ORDER BY ProductName DESC NULLS FIRST

  
#### RANDOM () También exite la función RANDOM() que al no especificar un campo de orden, ordena al azar los elementos en el resultado de la lista. ESTO SIRVE TAMBIEN PARA REALIZAR una misma busqueda varias veces pero variando los elementos presentados que cumplen las condiciones evaluadas.

 ej:

 	SELECT * FROM Products ORDER BY RANDOM()

  
#### ==ORDER BY campo1, campo2, ... campon== 
Realizando una busqueda y ordenando de 2 maneras el resultado:

`SELECT FROM "nom tabla" ORDER BY "campo1", "campo2", ...`

ej:

`SELECT FROM Products ORDER BY ProductName, ProductID`
  
  > esto devuelve la lista ordenada primero por el nombre de los productos, y luego por su ID si es que hay productos con el mismo nombre.
  

#### DISTINCT
Seleccionar una lista de elementos "únicos" ordenados por ProductName:
esto genera que si en una busqueda común, obtuviera 2 o más registros que tuviesen el mismo "nombre de campo", con esta sentencia figuraría solamente uno.

>[!important] ESTO SE APLICA A TODOS LOS CAMPOS QUE COLOQUEMOS EN EL SELECT!
>Si quisieramos realizar la busqueda con un solo campo afectado por distinct, deberiamos realizar una subconsulta, o usar el group by.

`SELECT DISTINCT "nombre de campo" FROM "nom de tabla" `

ej:

`SELECT DISTINCT ProductName from Products ORDER BY ProductName`

#### WHERE Condición para las selecciones.
 
 Esta condicion puede obtener registros de acuerdo a lo que indicamos luego del where
`SELECT "nombre del campo" FROM "nombre de tabla" WHERE "condicion"`

ej:

`select productname from products WHERE productID = 14`


  		
####  DELETE sentencia para borrar la seleccion( ⚠️ o todo! CUIDADO ⚠️)

   Esta sentencia borra los registros donde se cumpla la condicion, ¡SIEMPRE VA SEGUIDA DE UN WHERE!

```sql
DELETE FROM "tabla_donde_estan_los_datos" WHERE "condicion"
```

 ej:
```sql
DELETE from Products where ProductId >= 79;
```

#### TRUNCATE TABLE

Esta sentencia no borra los registros como delete, sino que elimina la tabla y la vuelve a crear sin registro alguno, es más eficiente, más rápida que delete.

El comando es básico:
```sql
TRUNCATE TABLE (nombre_de_tabla_a_borrar_completa)
```

#### UPDATE
sentencia para ==actualizar==  una tabla o registro.

Se utiliza para actualizar datos sobre registros ya ingresados. Se debe SIEMPRE evaluar una condicion para no actualizar TODOS los campos del mismo nombre seteado.


```sql
UPDATE "nombre_tabla"
SET "campo a actualizar" = "valor a ingresar" 
WHERE "condicion a evaluar para encontrar el campo o campos a modificar"
```

ej:

```sql
UPDATE Products SET ProductName = "salchichas chichas" 
 	WHERE ProductID = 40
```


ej2:

```sql
UPDATE "tabla" 
SET "campo1" = "valor1",
	"campo2" = "valor2" 
WHERE "condicion para encontrar el registro o registros"
```
   	

---

### OPERADORES LOGICOS

Se utilizan para armar busquedas con 2 condiciones, o varias posibilidades.

**AND / OR / NOT**

**AND** : si se cumplen ambas, hay resultados =>

`SELECT "nombre de campo" FROM "nombre de tabla" WHERE "condicion1" AND "condicion2"`

**OR** : si se cumple una de las dos, hay resultados =>

`SELECT "nombre de campo" FROM "nombre de tabla" WHERE "condicion1" OR "condicion2"`


Se pueden sumar condiciones a la busqueda, y separar con paréntesis () para aplicar ciertas condiciones juntas a otras.

ej:
```sql
SELECT * FROM Products
WHERE Price < 20    OR CategoryID = 6 AND SupplierID = 6
[1er condicion] [ ------ 2da condicion ------- ]
```

Separando con paréntesis, podemos ejecutar de la siguiente manera las condiciones:

```sql
SELECT * FROM Products
WHERE (Price < 20 OR CategoryID = 6) AND SupplierID = 6
[---- 1er condicion----]      [ 2da condicion ]
```
 
**NOT** : Invertir la condición a evaluar

nos devuelve resultados donde se obtienen los registos que NO SON condicion uno o dos.
SE UTILIZA HABITUALMENTE ANTES DE UN OPERADOR.

ej:

`SELECT * FROM Customers WHERE NOT country = 'USA' AND NOT country = 'Argentina'`

Esto devuelve registros donde el país NO ES 'USA' y NO ES 'Argentina'.

> El NOT se puede pensar en SQL como poner un eventoA 'Distinto' eventoB.


#### LIMIT
Se utiliza para "limitar" la cantidad de resultados en la consulta.

ej:

```sql
SELECT * from Customers WHERE
CustomerID > 50 and NOT Country = 'Germany'
LIMIT 5 //esto limita a 5 resultados en la consulta(que devuelve muchos más)
```


 ## Operador NOT y != (distinto de) 
 
 - La diferencia entre estos dos operadores, es el tipo de clase de cada uno.
   	NOT es un operador lógico.
   	!=  es un operador de comparación.

   Pueden llegar a dar los mismos resultados, pero la sintaxis es distinta y los resultados pueden resultar diferentes.


#### BETWEEN 
   Se utiliza para especificar un rango de busqueda, incluido los límites en la busqueda.
Claramente el valor1 debe ser menor al valor2 y del mismo tipo de dato compatible. Por ej:

`SELECT * FROM Products WHERE Price BETWEEN 20 and 40`

esto devolverá los productos de precios entre 20 y 40.

Tambien maneja datos de _Fechas_:

`SELECT * FROM [tablas] WHERE [campo] BETWEEN 'fecha1' and 'fecha2'`

#### LIKE
Se utiliza para buscar y filtrar patrones de texto en campos. Existen cómodines para las busquedas, y la cantidad depende de la base de datos, por ej Postgres maneja muchos más comodines con busquedas de texto.

ej:

`SELECT * FROM customers WHERE CustomerName LIKE 'Antonio Moreno Taquería'`

- Dentro del operador like, se usan los comodines "%" y " _ " .

 ==(%)== : indica que puede haber más texto(cantidad indefinida) antes o después de donde se ubica en el término de la condición.

ej:

		SELECT * FROM customers WHERE CustomerName LIKE '%r'
  
  > Esto significa y devuelve los registros donde el nombre del cliente, termine con "r", pero antes puede tener cualquier otra cosa el campo.

==( _ ) ==: 
el guión bajo indica que en su lugar, puede haber un caracter, pero especificando que en ese lugar hay UN SOLO carácter (no puede haber más)

ej:

	SELECT * FROM customers WHERE CustomerName LIKE 'Fu___' (3 underdash)
 
 > Esto devolveria Fulle, Fully, Furia, etc.


#### ISNULL o ISNOTNULL

   Esto evalua si el campo es _null_ o es _notnull_
	Esto serviría para analizar casos en donde los campos no tienen NINGUN tipo de dato, y esto generaría que al analizar los datos, los resultados no den como nos esperamos.
	Ej: Si contamos todos los campos con valores enteros, y luego sacamos un promedio, un valor 0 haría una diferencia en el calculo final, distinto a eliminar los registros con valores NULL para la cuenta de la cantidad. 


#### IN : operador

  Esto puede evaluar si el campo indicado, posee algunos de los valores pasados entre paréntesis.

```
SELECT * FROM "nombre de tabla" WHERE "campo1" IN ("valor1", "valor2", ..., "valorN")
```

ej:

`SELECT * FROM products WHERE CategoryID IN (2, 3)`

 > Esto devuelve los productos donde la categoría de cada uno es 2 o es 3.
 

## AGGREGATE FUNCTIONS y más  

#### COUNT (campo a contar)
Cuenta qué cantidad de registros tengo en un grupo si no se especifica un campo en particular, Sino, cuenta los números de registros que NO TIENEN NULL como valor en la columna especificada.
ej:

`SELECT COUNT(FirstName) AS Cantidad_de_nombres FROM Employees`

#### SUM(campo a sumar)
Cuenta qué cantidad suma todos los valores de una columna.

`SELECT SUM("campo a sumar") FROM "nombre de tabla"`

ej:

`SELECT SUM(price) AS Suma_total FROM Products`

>[!note] Si necesito sumar 2 campos de los registros, siempre que sean numéricos, se puede usar el operador + con los nombres de los campos.

ej:

```sql
SELECT id, nombre, valor1 + valor2 as TOTAL 
FROM Productos
ORDER BY TOTAL DESC;
```

#### AVG (campo a calcular promedio)
Cuenta y reporta el promedio de todos los valores de los registros del campo indicado.

Sintaxis:
	
`SELECT AVG (campo a promediar) FROM "nombre de tabla"`

#### ROUND (campo a calcular)
Cuenta y calcula el redondeo de un valor con coma flotante a su entero más cercano.

Sintaxis:

`SELECT ROUND ("campo a redondear", "cantidad de decimales") FROM "nombre de tabla"`

Ej:

`SELECT ROUND (AVG(Price), 2) FROM Products`

#### MIN (campo a evaluar mínimo)

`SELECT *, Min(Price) FROM Products`

> Esto genera una tabla de UN SOLO registro con el valor minimo en el campo "Price"

#### MAX (campo a evaluar máximo)

`SELECT *, Max(Price) FROM Products`

> Esto genera una tabla de UN SOLO registro con el valor máximo en el campo "Price"

#### GROUP BY 
Este operador agrupa según el campo definido, cada elemento único del campo.

Ej.

   TABLA "VENTAS"

| Frutas    | Cliente | Cantidad |
| --------- | ------- | :------: |
| bananas   | xxxx-xx |    10    |
| manzanas  | xxxx-xx |    2     |
| frutillas | xxxx-xx |    30    |
| bananas   | xxxx-xx |    5     |
| naranjas  | xxxx-xx |    3     |
| frutillas | xxxx-xx |    15    |
| manzanas  | xxxx-xx |    4     |

entonces, para ver cuantas manzanas en total hemos vendido, bananas, frutillas, etc.
escribimos la sentencia:

`SELECT * FROM Ventas GROUP BY Frutas`

#### HAVING
HAVING funciona como un WHERE pero va luego del _GROUP BY_ y se utiliza como una condición para filtrar resultados de grupos cuando se aplica alguna función en el select.

ej:

```sql
SELECT supplierID, ROUND(AVG(price)) AS promedio FROM Products
GROUP BY SupplierID
HAVING promedio > 40
```



#### No se puede aplicar una función de agregación al resultado de otra función de agregación.

## SUBCONSULTAS (relacionar tablas)

Las _Subconsultas_ no alteran las bases de datos, por lo tanto son solo SELECT, pero se pueden utilizar en un **SELECT**, dentro de un **WHERE**, **HAVING, FROM**.

Ej:

Aqui utilizamos la subconsulta dentro del SELECT, seleccionando una tabla que relaciona elementos de las tablas *orderDetails* y *products*.
```sql
SELECT productID, quantity,
(SELECT productname FROM products WHERE orderDetails.productID = ProductID) AS Nombre FROM OrderDetails
```
 
> Esta consulta obtiene el _productID_ y _Quantity_ de la tabla **OrderDetails** pero aparte, con la subconsulta, busca también los _ProductName_ donde el ProductID de la tabla Products es igual al ProductID de la tabla OrderDetails.
   La SUBCONSULTA va entre paréntesis.


ej de subconsulta:

```sql
SELECT productID, SUM(quantity) AS TotalVendido,
(select productName FROM Products WHERE productID = OD.productID) AS NombreProducto,
(select Price FROM Products WHERE productID = OD.productID) AS Precio,
(SUM(Quantity)*(SELECT Price FROM Products WHERE productID = OD.productID)) AS TotalGanado
FROM [OrderDetails] OD 
WHERE Precio > 40
GROUP BY ProductID
```

> Esta sentencia, va a unir resultados de 2 tablas, unidas por el productID de ambas.

- seleccionar el productID, y la SUMA de Cantidad como totalvendido de OrderDetails
- _sc_(seleccionar ProductName de tabla Productos donde ProductID = ProductID de  orderdetails) y presentalo como NombreProducto,
- _sc_(seleccionar Price de tabla Productos donde productID = ProductID de OrderDetails) y presentalo como Precio,
- _sc_(SUMA(Cantidad)) multiplicado (Seleccionar Price de Products donde PoductID = ProductID de OrderDetails)) y presentarlo como TotalGanado,
- DESDE [OrderDetails] alias OD
- Donde la _sc_ Precio sea mayor a 40,
- Agrupar por ProductID.

#### WITH

Las subconsultas también se pueden definir antes de iniciar el select, con la cláusula
	*WITH* (nombre de la tabla temporal) *AS* (aqui vamos a definir la subconsulta que nos devuelve resultados para nuestra tabla temporal)

Ejemplo: Es uno trivial ya que se pueden definir el nombre de las columnas en el mismo SELECT inicial, pero de esta manera, se crea una tabla temporal con dichos nombres, y luego se selecciona todo de nuevo de ella. 
```sql
WITH datos_pacientes AS (
  SELECT patient_id AS id_paciente,
  first_name AS nombre,
  last_name AS apellido
  FROM patients)
  SELECT * FROM datos_pacientes;
```

---
#### JOINS

Existen varios tipos de JOIN. siendo los mismos:

inner Join / Left Join / Right Join / Cross Join

#### CROSS JOIN 
Realizar un producto cartesiano de las tablas.

| tabla a  | tabla b  |
| -------- | -------- |
| valor a1 | valor b1 |
| valor a2 | valor b2 |
| valor a3 | valor b3 |

Con un **cross join** sin condición( *where* ) quedaría lo siguiente de resultado:

| resultados |          |
| ---------- | -------- |
| valor a1   | valor b1 |
| valor a1   | valor b2 |
| valor a1   | valor b3 |
| valor a2   | valor b1 |
| valor a2   | valor b2 |
| valor a2   | valor b3 |
| valor a3   | valor b1 |
| valor a3   | valor b2 |
| valor a3   | valor b3 |

>***No tiene sentido.***

#### INNER JOIN (la intersección de los datos)
(o join a secas) Devuelve la intersección de datos, o dicho de otra manera, los datos de la tabla A que coinciden con datos de la tabla B, *sin valores NULL*).
Al crear y redactar el *INNER JOIN*, en el *SELECT*, podemos seleccionar campos de las *n - tablas* que vayamos a vincular.
Luego va la sentencia del *ON*, y lo que queremos que relacione(normalmente son *primary keys*) 

- SI queremos unir los resultados de la busqueda de 2 tablas podemos realizar lo siguiente:

```sql
SELECT * FROM [Employees] e INNER JOIN [Orders] o
ON e.EmployeeID = o.EmployeeID
```


  El "ON" actua de Where cuando utilizamos JOINs
  > Esto devuelve todos los registros, tanto de los empleados, como de las ordenes emparejados por el employee ID que es una Primary Key en Employees y una Foreign Key en Orders.
  
#### LEFT JOIN

> Es una busqueda que devuelve TODOS los datos solicitados de la tabla A, y los datos de la tabla B que COINCIDEN con A (por definición, permite valores null cuando no hay cruce entre los datos usados para relacionar).

```sql
SELECT firstname AS nombre, Reward AS Recompensa, Month AS Mes 
FROM Rewards r
LEFT JOIN Employees e ON e.EmployeeID = r.EmployeeID
```

#### RIGHT JOIN

>Es una busqueda que devuelve todos los datos solicitados de la tabla B, y los datos de la tabla A que coinciden con B. nuevamente, permite valores null cuando hay datos de B que no tienen su relación con A.

#### FULL JOIN

es una union de LEFT JOIN y RIGHT JOIN, pero evitando los duplicados.

Se usa el **UNION** para unir dos consultas, normalmente left y right.

y esto da el resultado de la busqueda cruzada.

>[!important] Los términos LEFT OUTER JOIN, RIGHT OUTER JOIN Y FULL OUTER JOIN son mantenidos por la compatibilidad con SQL-92, pero las consultas dichas son equivalentes a LEFT JOIN, RIGHT JOIN y FULL JOIN respectivamente.

#### Funciones con JOIN

Al utilizar JOINs, podemos usar ciertas cláusulas que permiten la mejor lectura de la consulta para evitar tener que estar repitiendo datos.

*USING* : esta cláusula se usa cuando usamos un JOIN con otra tabla, y tanto en la tabla A como en la B, existe *una columna con el mismo nombre y tipo de datos en ella*, los cuales queremos usar para unir los resultados. 

En vez de colocar 
```sql
SELECT * FROM tablaA
JOIN tablaB
ON tablaA.id = tablaB.id;
```

Podemos usar la siguiente sintaxis
```sql
SELECT * FROM tablaA
JOIN tablaB
USING (id); -- esta linea equivale a decir que el campo id de una sea igual al id de la otra.
```

![[./img/joins.png# border]]


---
## Cardinalidad
   La cardinalidad define qué tipo de relaciones une a las tablas, normalmente pueden haber distintas relaciones entre tablas, siendo las siguientes:

   **uno a uno:** Un elemento de una tabla se relaciona con un elemento de otra. ej: una persona con su dni. cada persona es unica y tiene un único nro de documento.

   **uno a muchos:** Relaciones de un elemento de una tabla con n-cantidad de elementos de otra tabla. Ej: un autor puede tener muchos libros.

   **muchos a uno:** Relacion establecida entre varios elementos de una tabla, a uno solo de otra. Es la opción anterior invertida
   Ej: existen muchos libros que tienen un único autor.

   **muchos a muchos:** Varios registros en una tabla se relaciona con varios registros en otra y vicecersa. Normalmente se utiliza una relación con una 3er tabla intermedia de uno a n y de n a 1
   con las 2 tablas principales.

---

## Crear índices 

Los índices ayudan a que las busquedas sean más eficientes y rápidas. Están los índices primarios, que están representados por las *Primary Keys*, pero luego se pueden crear otros indices, para ayudar más a las busquedas y rendimiendo de la base de datos.

- Indice ordinario (permite campos duplicados y vacíos)

```sql
CREATE INDEX "nombre del indice" ON "nombre de tabla" (campo a indexar)`
```
  

 - Indice compuesto
   Para crear un índice compuesto, de 2 campos que no deberían tener datos repetidos, dado que normalmente son únicos por naturaleza, pero aún asi no son *Primary Keys* podemos realizar lo siguiente:

```sql
CREATE UNIQUE INDEX "nombre del indice" ON "nombre de tabla" (campo1, campo2)
```

La conjunción de los datos de estos 2 campos, crearían un virtual "campo único" donde la composición de sus valores, daría un resultado único, por lo tanto, actuaría como una primary key sin serlo.
El término *INDEX* genera que el campo índice no pueda tener valores repetidos, la misma tabla no permitiría INSERTARLOS

ej:

```sql
CREATE UNIQUE INDEX "nombre" ON Employees (LastName, FirstName)
```

 - Esto genera que los campos LastName y FirstName compuestos, no acepten datos duplicados. 
  
 >NO PODEMOS AGREGAR 2 "GIORDANO" "DAVID". La combinación es única. Puede haber otro "David", puede haber otro "GIORDANO" pero no pueden haber 2 empleados con el mismo first y last name. 

## Eliminar índices

  Si vemos que los índices no mejoran las consultas, podemos borrarlos dado que sino ocupan mucho espacio en disco, y generalmente cuando agregamos o borramos datos, los índices afectan la lectura y escritura.

`DROP INDEX "nombre del índice"`

---

## VISTAS

  Las vistas se definen mediante las busquedas SQL que se realizan, obteniendo campos específicos con ciertas condiciones, o sea, podemos nombrar como "vista" a una "tabla resultado de una sentencia SQL".

- Para crear una vista:

CREATE VIEW "nombre de la vista" AS "consulta sql que devuelve la vista de columnas seleccionadas"

- Para eliminar una vista, se corre:

DROP VIEW IF EXIST "nombre de la vista".

---

## BLOQUEOS Y TRANSACCIONES

Esto se refiere al concepto de que las bases de datos deben tener seguridad de los datos consultados modificados al momento de realizarze los cambios.

SQLite maneja un bloqueo compartido (shared lock) el cual permite a un usuario B mientras un usuario A está escribiendo en la base de datos, poder leer todavia los datos de la misma.

## BEGIN, ROLLBACK y COMMIT.

para asegurar las transacciones realizadas en la base de datos, como métodos de seguridad, hay procesos que marcan los inicios y finales de las escrituras de las mismas.

- _BEGIN_ permite iniciar el proceso de escritura cuidado, esto permite realizar un _ROLLBACK_ en caso de que los datos a guardar tengan un error o se hayan guardado de manera incorrecta.

- _ROLLBACK_ devuelve el estado de la base de datos al punto donde se inicio el _BEGIN_.

- _COMMIT_ confirma luego de confirmado los nuevos cambios a la base, guardandolos finalmente en la base real. 




----
[[#Indice|Volver al indice ▲]]































