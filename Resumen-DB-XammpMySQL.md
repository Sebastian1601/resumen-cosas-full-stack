
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

> TABLA : Es una estructura de datos, organizada en filas y columnas.

 _Campo_ : Es el nombre que tiene una columna en una base de datos.

 _Registro_ : Es un grupo de campos que hacen referencia a un elemento en la base.

 _Valor del campo_ : Es el valor que tiene un campo en particular para un registro particular.

  Al definir un campo, tenemos que definir qué tipo de datos va a almacenar.
  Existen varios tipos de datos, los más utilizados son:
- Integer (nro.entero)
- Text    (texto)
- Blob    (archivos binarios varios, imágenes, videos, etc)
- Real    (nros con coma flotante, porcentajes, etc) más rápido, menos precisión en los nros.
- Numeric (nros matemáticos precisos) de cualquier tamaño
---

### Sentencias de busqueda inicial

Mostrar todos los datos de la tabla 'usuarios'
        
        select * from users 
- select : selecciona,
- * : símbolo que significa "todo",
- from : desde,
- users : es el nombre de la tabla donde buscar.
---
### Sentencia de ingreso de un registro

ingresar un registro de usuario en la tabla 'usuarios'

    insert into usuarios (nombre, apellido, edad) values ('Juan', 'Giordano', '21')

- insert : ingresá,
- into : en la siguiente tabla,
- usuarios : nombre de la tabla,
- (nombre, apellido, edad) : nombre de los campos a ingresar,
- values : los siguientes valores,
- ('Juan', 'Giordano', '21') : valores a ingresar en cada campo descripto antes.

> Se pueden generar un insert con varios registros, de la siguiente manera:

    insert into usuarios (nombre, apellido, edad) 
    values  ('Claudia', 'Caceres','44'),
	    	('Daiana','Congregado','17'),
		    ('Ariel','Berneto','25'),
		    ('Juan Jose','Campagnolo','37')

> Se puede insertar un registro, o varios, y generar una consulta justamente luego del insert, separando las declaraciones con ; (punto y coma).

    insert into usuarios (nombre, apellido, edad)
    values ('lucas', 'dalto', 21);
    select * from usuarios

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

- Asignar _Alias_ al nombre de un campo. (as)

En la sentencia SQL al buscar en una tabla, podemos "renombrar" temporalmente un campo, de la siguiente manera:

    select LastName AS apellido FROM emplpoyees
otro ej:

    select LastName as Apellidos, FirstName as Nombre from employees

 Realizar "funciones" en una busqueda:

     select price as precioOriginal, price*2 as precioDoble from Products

> nótese que se multiplica por 2 los datos del campo price, y se asignan con el alias preciodoble, desde la tabla productos.

- Ordenar busquedas de manera descendente y ascendente (order by [campo] ASC / DESC)

      SELECT * FROM Products ORDER BY price

  | tipo de dato | Orden Ascendente |
  |------------|---------|
  | numeros | 0 - 9 |
  |texto    | null     
  |         |numeros  
  |         |carácteres especiales
  |         |letras  |
  | blob    | no hay orden | 
  



## Entidad:
   - Es una representación de algo. 
   - Para representarlos se utiliza la *Notación de chen*.
   - Para representarlas, se utiliza un sustantivo dentro de un cuadrado.
Una entidad está definida por sus propiedades. Se representan con un óvalo.
   

> Las entidades se componen por atributos simples, atributos compuestos, atributos multivalor, y atributos derivados.








