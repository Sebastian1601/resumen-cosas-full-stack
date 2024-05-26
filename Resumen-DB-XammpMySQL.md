
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


##################################################################################################################################################




