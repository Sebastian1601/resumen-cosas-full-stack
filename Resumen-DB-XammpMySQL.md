
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

##esto puede generar que phpMyAdmin no abra más al acceder a http://127.0.0.1, y de un error que indica que los datos de la clave no coinciden.

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
      1 Integer
      1 Text
      1 Blob
      1 Real
      1 Numeric

 
 





# Entidad:
   - Es una representación de algo. 
   - Para representarlos se utiliza la *Notación de chen*.
   - Para representarlas, se utiliza un sustantivo dentro de un cuadrado.
Una entidad está definida por sus propiedades. Se representan con un óvalo.
   

### Las entidades se componen por atributos simples, atributos compuestos, atributos multivalor, y atributos derivados.








