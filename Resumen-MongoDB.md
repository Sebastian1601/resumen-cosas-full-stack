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

Abrimos una Terminal, y ejecutamos   

      >mongod

esto disparará varios comandos y devolverá información en la ventana, que  no se cierra ni se termina mientras esté en uso.

Para conectar el Shell de la terminal, debemos abrir otra Terminal, y ejecutar 

    >mongosh
para que el shell se conecte con el servicio de "MongoD".


Ahi ya tenemos vinculado el Shell con el servicio y podemos ejecutar código de Mongo para administrar bases. *Deben estar ambos procesos abiertos*.


### Comandos Básicos del Shell.


Se puede ejecutar el comando _base_ con el método .help y esto nos devolverá la lista de comandos derivados del comando base.
ej:

    > db.help //esto dispara ayuda sobre los comandos db.(métodos)
    

#### _db_

>  este comando devuelve la base de datos que estamos utilizando (independientemente de que el prompt ya lo indica)
 
#### _show dbs_

>  este comando devuelve la lista de base de datos que tenemos creadas(esto es importante, las bases deben tener algún dato para figurar en esta lista)

#### _use [dbname]_

>  este comando "crea" una base de datos nueva de nombre [dbname] y pasa a ella directamente.
> ej: >use peliculas

#### _db.dropDatabase()_

> este comando elimina la base de datos donde estábamos parados.

#### _db.createCollection("[nombre de la collecion a crear]")_

> este comando nos permite crear una colleción nueva dentro de nuestra base de datos.
> ej: > db.createCollection("users")


#### _show collections_

> este comando nos devuelve las colecciones dentro de la base de datos actual.

#### _db.[nombre de una coleccion].drop()_

> este comando elimina la coleccion indicada en el comando, devolviendo "true" si es exitoso.
> ej: > db.users.drop()


### Ejemplo de Documento para una coleccion.

> Los documentos van a estar agregados en formato JSON (Javascript) a la base de datos, y como tales, pueden contener datos primitivos, o incluso más objetos, o arrays.

ej:
```
{
      "nombre de propiedad 1":"valor string",
      "nombre de propiedad 2": valor Number,
      "nombre de propiedad 3": valor Boolean,
      "nombre de propiedad 4": valor RegExp,
      "nombre de propiedad 5": {
            otro objeto como el definido,
}
}
```
ej:
```
{
      "nombre":"Pedro",
      "edad":45,
      "vive": true,
      "contactos":{
            "nombre":"Ariana",
            "parentesco":"hermana",
            "nro_contacto":0115465231152
            }
}
```

### Insertar documentos en una coleccion

Para insertar documentos en una coleccion, tenemos el método `db.insert([objeto en formato json a insertar])`

A su vez, podemos crear una coleccion al vuelo, insertando un documento directamente en la nueva colección, con el código

`db.[nombre_de_nueva_coleccion].insert([objeto en formato json a insertar])`

y esto nos devuelve un objeto del siguiente formado, confirmando si se agregó el documento:

```
{
      acknowloedged:true,
insertedIds: {'[index]': ObjectId('[IdUnicaParaIdentificarElDocumento]')}
}
```

















