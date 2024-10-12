# MongoDB NoSQL 

### instalación de MongoDB Server y Shell

para instalar el servidor, de acuerdo a la versión de Windows que tengamos, debemos descargar el paquete instalador desde la web oficial *https://www.mongodb.com/es*

Si usamos Windows 10, la versión soportada es la 6.0.18. Instalar una versión más nueva, no dejará conectar el servicio ni iniciarlo.

para eso, instalamos el paquete de forma "completa" al iniciar el MSI package, y se puede seleccionar si se instala como servicio de Windows, o si es necesario ejecutarlo cada vez que vayamos a utilizarlo.

Finalizado esto, debemos crear la carpeta  
> "C:/Data/db/"

Finalmente, descargamos el shell aparte, aqui no depende del sistema operativa en particular, hay que verificar que sea para windows 10+. 
Si se descarga el zip del shell, se puede descomprimir en la misma carpeta del server, carpeta bin para poder luego agregar dicha carpeta a las variables de entorno.

### Instalar en *PATH* la dirección de la carpeta BIN de mongodb. (esto permite que los comandos de MongoDB Shell se puedan utilizar desde la consola de comandos)

Se crea un nuevo item del menú Variables de Entorno en PATH, con la ruta de la carpeta BIN en archivos de programa de MongoDB.

## Ejecutar MongoDB

Abrimos una Terminal, y ejecutamos "MongoD", esto disparará varios comandos y devolverá información en la ventana, que  no se cierra ni se termina mientras esté en uso.

Para conectar el Shell de la terminal, debemos abrir otra Terminal, y ejecutar "MongoSH", para que el shell se conecte con el servicio de "MongoD".


Ahi ya tenemos vinculado el Shell con el servicio y podemos ejecutar código de Mongo para administrar bases.


