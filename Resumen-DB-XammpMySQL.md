
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

### Oden de las sentencias para generar una consulta 

1- (SELECT / DELETE/ UPDATE)

2- (CONDICION WHERE) 

3- (GROUP BY)

4- (HAVING -solo se usa si usamos group by-)

5- (ORDER BY)

6- (LIMIT)

### Creación de base, tabla y uso.

muestra las bases de datos activas.
`SHOW DATABASES;`

crea la base de datos que indicamos.
`CREATE DATABASE [nombre];`

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


#### Limitaciones (o restricciones) en la definición de columnas, y tablas.

- **NOT NULL** : indica que el campo no puede tener valor NULL al crearse o modificarse un registro.

- **UNIQUE** : indica que el campo será único entre los registros, aparte del id que suele ser autoincrementable.

- **PRIMARY KEY** : una combinación de NOT NULL y UNIQUE. identifica inequívocamente un registro de la tabla.

- **FOREIGN KEY** : evita acciones que destruirían el vínculo entre tablas.

- **CHECK** : determina que los valores en una columna satisfacen una condición específica.

- **DEFAULT** : setea un valor por defecto si no se especifica alguno en el ingreso de registro.

- **CREATE INDEX**:

- **AUTO_INCREMENT** : indica que el campo incrementará automáticamente su valor al crearse un registro.

>[!info] Información importante
>Para agregar una restricción a un campo, luego de creada la tabla, se puede utilizar la siguiente sintaxis 
>```
>ALTER TABLE [nombre_de_tabla] ADD [restricción_a_agregar] (campo_al_cual_agregarle_la_restricción)
>```



Ejemplo:
`ALTER TABLE users ADD UNIQUE(last_name);`

Para ==eliminar== una restricción a un campo, luego de creado, se utiliza la siguiente sintaxis:

`ALTER TABLE [nombre_tabla] DROP INDEX [nombre_campo_a_eliminar_restricciones]`

Ejemplo:
`ALTER TABLE users DROP INDEX last_name;`

*Para ==eliminar== una restricción de ==PRIMARY KEY== en un campo ya creado se usa:

`ALTER TABLE [nombre_de_tabla] DROP PRIMARY KEY;`


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

`DELETE FROM "tabla a obterner los datos" WHERE "condicion"`

 ej:
 `DELETE from Products where ProductId >= 79;`


#### UPDATE
sentencia para ==actualizar==  una tabla o registro.

Se utiliza para actualizar datos sobre registros ya ingresados. Se debe SIEMPRE evaluar una condicion para no actualizar TODOS los campos del mismo nombre seteado.


```
UPDATE "nom tabla" SET "campo a actualizar" = "valor a ingresar" WHERE "condicion a evaluar para encontrar el campo a modificar"
```

ej:

```
UPDATE Products SET ProductName = "salchichas chichas" 
 	WHERE ProductID = 40
```


ej2:

```
UPDATE "tabla" SET "campo1" = "valor1", "campo2" = "valor2" 
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

- Dentro del operador like, se usan los comodines "%" y "_" .

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


#### IN : operador

  Esto puede evaluar si el campo indicado, posee algunos de los valores pasados entre paréntesis.

```
SELECT * FROM "nombre de tabla" WHERE "campo1" IN ("valor1", "valor2", ..., "valorN")
```

ej:

`SELECT * FROM products WHERE CategoryID IN (2, 3)`

 > Esto devuelve los productos donde la categoría de cada uno es 2 o es 3.
 

## Funciones y más  

#### COUNT (campo a contar)
Cuenta qué cantidad de registros tengo en el campo indicado.
ej:

`SELECT COUNT(FirstName) AS Cantidad_de_nombres FROM Employees`

#### SUM(campo a sumar)
Cuenta qué cantidad suma todos los valores de una columna.

`SELECT SUM("campo a sumar") FROM "nombre de tabla"`

ej:

`SELECT SUM(price) AS Suma_total FROM Products`

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

> Esto genera una tabla de un registro con el valor minimo en el campo "Price"

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

```
SELECT supplierID, ROUND(AVG(price)) AS promedio FROM Products
GROUP BY SupplierID
HAVING promedio > 40
```

#### No se puede aplicar una función de agregación al resultado de otra función de agregación.

## SUBCONSULTAS (relacionar tablas)

Las _Subconsultas_ no alteran las bases de datos, por lo tanto son solo SELECT, pero se pueden utilizar en un SELECT, dentro de un WHERE, HAVING.

Ej:

```
SELECT productID, quantity,
(select productname from products where orderDetails.productID = ProductID) as Nombre from OrderDetails
```
 
> Esta consulta obtiene el _productID_ y _Quantity_ de la tabla **OrderDetails** pero aparte, con la subconsulta, busca también los _ProductName_ donde el ProductID de la tabla Products es igual al ProductID de la tabla OrderDetails.
   La SUBCONSULTA va entre paréntesis.


ej de subconsulta:

```
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


#### JOIN

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

#### INNER JOIN 
(o join a secas) Devuelve la intersección de datos, o dicho de otra manera, los datos de la tabla A que coinciden con datos de la tabla B)

- SI queremos unir los resultados de la busqueda de 2 tablas podemos realizar lo siguiente:

		SELECT * FROM [Employees] e INNER JOIN [Orders] o
  		ON e.EmployeeID = o.EmployeeID

  El "ON" actua de Where cuando utilizamos JOINs
  > Esto devuelve todos los registros, tanto de los empleados, como de las ordenes emparejados por el employee ID que es una Primary Key en Employees y una Foreign Key en Orders.

  
#### LEFT JOIN Es una busqueda que devuelve todos los datos solicitados de la tabla A, y los datos de la tabla B que COINCIDEN con A.

	select firstname AS nombre, Reward as Recompensa, Month as Mes from Rewards r
	left join Employees e on e.EmployeeID = r.EmployeeID

#### RIGHT JOIN es una busqueda que devuelve todos los datos solicitados de la tabla B, y los datos de la tabla A que coinciden con B.

#### FULL JOIN es una union de LEFT JOIN y RIGHT JOIN, pero evitando los duplicados.

Se usa el UNION para unir dos consultas, normalmente left y right.

y esto da el resultado de la busqueda cruzada.

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

`CREATE INDEX "nombre del indice" ON "nombre de tabla" (campo a indexar)`
  

 - Indice compuesto
   Para crear un índice compuesto, de 2 campos que no deberían tener datos repetidos, dado que normalmente son únicos por naturaleza, pero aún asi no son *Primary Keys* podemos realizar lo siguiente:

`CREATE UNIQUE INDEX "nombre del indice" ON "nombre de tabla" (campo1, campo2)`

La conjunción de los datos de estos 2 campos, crearían un virtual "campo único" donde la composición de sus valores, daría un resultado único, por lo tanto, actuaría como una primary key sin serlo.
El término *INDEX* genera que el campo índice no pueda tener valores repetidos, la misma tabla no permitiría INSERTARLOS

ej:

`CREATE UNIQUE INDEX "nombre" ON Employees (LastName, FirstName).`

 - Esto genera que los campos LastName y FirstName compuestos, no acepten datos duplicados. 
  
 >NO PODEMOS AGREGAR 2 "GIORDANO" "DAVID". La combinación es única. Puede haber otro "David", puede haber otro "GIORDANO" pero no pueden haber 2 empleados con el mismo first y last name. 

## Eliminar índices

  Si vemos que los índices no mejoran las consultas, podemos borrarlos dado que sino ocupan mucho espacio en disco, y generalmente cuando agregamos o borramos datos, los índices afectan la lectura y escritura.

`DROP INDEX "nombre del índice"`

---

## Crear "VISTAS"

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































