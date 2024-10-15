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
---
### Insertar documentos en una coleccion

Para insertar documentos en una coleccion, tenemos el método 
`db.insertOne([objeto en formato json a insertar])`

A su vez, podemos crear una coleccion al vuelo, insertando un documento directamente en la nueva colección, con el código

`db.[nombre_de_nueva_coleccion].insertOne([objeto en formato json a insertar])`

y esto nos devuelve un objeto del siguiente formado, confirmando si se agregó el documento:

```
{
      acknowledged:true,
insertedIds: {'[index]': ObjectId('[IdUnicaParaIdentificarElDocumento]')}
}
```
---
### Listar elementos en una coleccion

Para buscar algún objeto dentro de una colección, tenemos el método de Javascript _find()_

ej:

`db.[nombre de la coleccion].find()`

esto nos devuelve el listado de todos los elementos de la coleccion.

ejemplo de elemento guardado ya en la coleccion.

`{
      "_id: ObjectId('jaksljd32345klj8das988s8ds8')
      "nombre":"Pedro",
      "edad":45,
      "vive": true,
      "contactos":{
            "nombre":"Ariana",
            "parentesco":"hermana",
            "nro_contacto":0115465231152
            }
}`

#### Guardar múltiples datos al mismo tiempo

Para guardar una lista de documentos a guardar, se pasa por el método insert, un array de los objetos a agregar...
ej:

`db.[coleccion_donde_agregamos_los_datos].insertMany( [ array de documentos a ingresar ])`

ejemplo práctico:

```
db.productos.insert([
{
"name":"Monitor 24",
"price":9.99
},
{
"name":"Monitor 29",
"price":14.99
}
])
```

---

#### Buscar por una propiedad en particular

Para buscar y obtener resultados de un dato en particular, debemos usar el método find() con un objeto dentro indicando el valor que queremos obtener o buscar.
ej:

`db.productos.find( { "price":4.99 } )`

> Esto nos devolverá una ***lista de elementos*** donde TODOS coincidan con este dato en particular.


#### Eliminar propiedades de las respuesta 

Al buscar documentos que coincidan con el criterio indicado, podemos indicar que los resultados, manejen solamente ciertas propiedades del documento.
ej:

Tengo la siguiente lista de elementos...

```
[
  {
    _id: ObjectId('670dc3b3c5633caa6786b01e'),
    name: 'keyboard',
    price: 4.99
  },
  {
    _id: ObjectId('670dc3c7c5633caa6786b01f'),
    name: 'mouse',
    price: 2
  },
  {
    _id: ObjectId('670dc4ecc5633caa6786b020'),
    name: "Monitor 24'",
    price: 9.99
  },
  {
    _id: ObjectId('670dc4ecc5633caa6786b021'),
    name: "Monitor 29'",
    price: 14.99
  },
  {
    _id: ObjectId('670dc64cc5633caa6786b022'),
    name: 'tablet barata',
    price: 14.99
  }
]
```
Al realizar la busqueda de los mismos, podemos definir qué propiedades queremos obtener de los resultados, algo así como el `SELECT name, price FROM` de SQL, pero con objetos JSON...

Por lo tanto podemos realizar nuestra busqueda de la siguiente manera, de acuerdo a la lista anteriormente mencionada:

`db.productos.find({"price":14.99}, {"name":1, "_id":0})`

...esto devolverá como resultado el siguiente array de documentos:

`[ { name: "Monitor 29'" }, { name: 'tablet barata' } ]`

demostrando que los documentos que coinciden con ese precio, son 2.

---

#### Ordenar resultados al buscar

Para poder ordenar los datos al buscar y obtener una lista de documentos, se utiliza el método .sort().

***NOTESE QUE DENTRO DEL METODO SORT(), NO SE USA COMILLA PARA EL OBJETO PASADO COMO PARAMETRO***

ej:
`db.productos.find().sort({price: 1})`


---

#### Establecer límite en los resultados de una busqueda

Para obtener un límite en la busqueda, le agregamos el método .limit([cant. de resultados que queremos]) 

ej:

`db.productos.find().limit(5)`

> Esto nos devuelve un listado de los primeros 5 documentos de entre todos los que listaría sin el límite.


---

#### Contar documentos de una colección en particular

Podemos contar qué cantidad de documentos tenemos en la colección que queremos, con el método `.countDocuments()`
Ej:
`db.[coleccion].countDocuments()`

---

#### Métodos de arrays en los resultados de busqueda.

Al ser MongoDB un intérprete de Javascript, podemos definir que a los resultados de una busqueda, le apliquemos un callback para cada uno de ellos, como por ejemplo el método `.forEach(callback)`

ej:

`db.productos.find().forEach(producto => print("Nombre del producto: " + producto.name))`

> ⚠️ NOTESE: no se usa el método console.log() para imprimir en consola los datos, se usa print() de igual manera que console.log().
---

### Actualizar datos de un documento

Para poder modificar propiedades de un documento, usamos el método dedicado `.update()`

ej:
`db.productos.updateOne({busqueda de propiedad}, { $set: {propiedad a editar o agregar con su valor}} )`

`db.productos.updateOne({"name":"tablet barata"}, { $set: {"name":"tablet Samsung Galaxy X9"} } )`

esto devolverá un objeto con la siguiente estructura:

```
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
---

### Selectores de busqueda (importante)



