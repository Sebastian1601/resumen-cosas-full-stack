# MongoDB NoSQL 

## instalación de MongoDB Server y Shell

para instalar el servidor, de acuerdo a la versión de Windows que tengamos, debemos descargar el paquete instalador desde la web oficial *https://www.mongodb.com/es*

Si usamos Windows 10, la versión soportada es la 6.0.18. Instalar una versión más nueva, no dejará conectar el servicio ni iniciarlo.

para eso, instalamos el paquete de forma "completa" al iniciar el MSI package, y se puede seleccionar si se instala como servicio de Windows, o si es necesario ejecutarlo cada vez que vayamos a utilizarlo.

Finalizado esto, debemos crear la carpeta  
`C:/Data/db/`

Finalmente, descargamos el shell aparte, aqui no depende del sistema operativa en particular, hay que verificar que sea para windows 10+. 
Si se descarga el zip del shell, se puede descomprimir en la misma carpeta del server, carpeta bin para poder luego agregar dicha carpeta a las variables de entorno.

### Instalación de variables de entorno

Es recomendable copiar en el menú de variables de entorno `PATH` la dirección de la carpeta `BIN` de `mongodb`. (esto permite que los comandos de MongoDB Shell se puedan utilizar desde la consola de comandos desde cualquier ruta)

Se crea un nuevo item del menú Variables de Entorno en `PATH`, con la ruta de la carpeta BIN en archivos de programa de MongoDB.

## Ejecución de MongoDB

Abrimos una Terminal, y ejecutamos   

      >mongod

esto disparará varios comandos y devolverá información en la ventana, que  no se cierra ni se termina mientras esté en uso.

Para conectar el Shell de la terminal, debemos abrir otra Terminal, y ejecutar 

    >mongosh
para que el shell se conecte con el servicio de "MongoD".


Ahi ya tenemos vinculado el Shell con el servicio y podemos ejecutar código de Mongo para administrar bases. 
>[!warning] IMPORTANTE
>Deben estar ambos procesos abiertos!!!.


## Instalación como Servicio de Windows
Si al instalar el programa, dejamos seleccionado la casilla de "instalar MongoDB" como servicio de Windows, el mismo se ejecutará al iniciar windows directamente, estando "de fondo" todo el tiempo activo. Esto permite que al abrir Mongo DB Compass (GUI), el servicio responda correctamente y no haya que conectar manualmente o iniciarlo.

Notar que en este paso de instalación, podemos cambiar el nombre del servicio de windows "MongoDB". En general, dejarlo como está dado que es estándar. Si lo cambiamos, y cerramos, deberemos buscar por la terminal cómo se llama el mismo para volverlo a ejecutar

Si por alguna razón, cerramos el proceso, y no sabemos qué nombre le pusimos al mismo, por defecto es "MongoDb", y para ejeuctarlo nuevamente, no podemos usar el comando `mongod` de la consola. 
En este caso, deberemos usar el comando
`c:\net start MongoDB`
y esto hará que el servicio inicie nuevamente.

Si no recordamos qué nombre le seteamos al servicio, podemos revisar con el comando:
```powershell
Get-Service | Where-Object {$_.DisplayName -like "*Mongo*" -or $_.Name -like "*Mongo*"}
```

Este comando devolverá una tabla, que tiene las dos columnas solicitadas:
- *Name*: es el nombre interno del servicio (el que se debe usar con el comando anterior net start [nombre del servicio])
- *DisplayName*: esto es el nombre descriptivo que se puede haber cambiado en el instalador.

## Comandos Básicos del Shell.
Se puede ejecutar el comando base con el método `.help` y esto nos devolverá la lista de comandos derivados del comando base.
ej:
```shell
db.help //esto dispara ayuda sobre los comandos db.(métodos)
```
### `db`
 este comando devuelve la base de datos que estamos utilizando (independientemente de que el prompt ya lo indica)

### `show dbs`
Este comando devuelve la lista de base de datos que tenemos creadas (==IMPORTANTE==: Las bases deben tener algún dato para figurar en esta lista)

### `use [dbname]`
Este comando "crea" una base de datos nueva de nombre [dbname] y pasa a ella directamente.
>[!example] ejemplo
>`>use peliculas`

### `db.dropDatabase()`
Este comando **elimina** la base de datos donde estábamos parados.

### `db.createCollection("[nombre_de_colección_a_crear]")`
Este comando nos permite crear una colleción nueva dentro de nuestra base de datos.
>[!exmaple] Ejemplo:
> `>db.createCollection("users")`

### `show collections`
Este comando nos devuelve las colecciones dentro de la base de datos actual.

### `db.[nombre_de_una_coleccion].drop()`
Este comando **elimina** la coleccion indicada en el comando, devolviendo "*true*" si es exitoso.
> [!example] Ejemplo:
> `>db.users.drop()`

### Ejemplo de Documento para una coleccion.
Los documentos van a estar agregados en formato *JSON* (Javascript Object Notation) a la base de datos, y como tales, pueden contener datos primitivos, o incluso más objetos, o arrays.

>Ejemplo:
```json
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

Podemos definir varias propiedades para una principal, de la siguiente manera

```json
{
	"nombre propiedad1":{
			type:String,
			required:true,
			trim:true
		},
	"nombre propiedad2":{
			type:Mixed,
			trim:true
		},
	"nombre propiedad3":{
			type:Number,
			max:9999,
			min:1,
			required:true
	}
}
```

>Ejemplo 2:
```json
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
Para insertar documentos en una coleccion, tenemos **dos métodos**: 
1.  `db.collections('coleccion a usar').insertOne( {} )` // insertar un elemento.
2. `db.collections('coleccion a usar').insertMany( [{}, {}, ..., {}] )` // insertar varios documentos
### `db.coleccion.insertOne()`
`db.collection('coleccion_donde_insertar').insertOne( {Obj_JSON_a_insertar} )`
A su vez, podemos crear una coleccion al vuelo, insertando un documento directamente en la nueva colección, con el código

`db.[nombre_de_nueva_coleccion].insertOne({ Obj JSON a insertar })`
y esto nos devuelve un objeto del siguiente formado, confirmando si se agregó el documento:
```json
{
  acknowledged:true,
  insertedIds: {'[index]': ObjectId('[IdUnicaParaIdentificarElDocumento]')}
}
```

### `db.coleccion.insertMany()`
`db.collection('coleccion_donde_insertar').insertMany( [ {}, {}, ..., {}] )`

>[!warning] NOTESE:
>al usar `.insertMany` se pasa como argumento, un **array** de *Obj JSON* a insertar. Cada operación es atómica, pero el proceso en sí no lo es.
> Si la colección no existe, el método `.insertMany()` crea la misma para guardar los datos.

---
### Listar elementos en una coleccion
Para buscar algún objeto dentro de una colección, tenemos el método de Javascript `find()`

>Ejemplo:
`> db.[nombre de la coleccion].find()`

Esto nos devuelve el listado de todos los elementos de la coleccion.
Ejemplo de elemento guardado ya en la coleccion.
```json
{
	"_id: ObjectId('jaksljd32345klj8das988s8ds8')
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
### Guardar múltiples datos al mismo tiempo
Para guardar una lista de documentos a guardar, se pasa por el método `insert`, un **array** de los objetos a agregar...
>[!example] Ejemplo:
`db.[coleccion].insertMany( [Documentos_a_ingresar ])`

>Ejemplo práctico:
```js
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
### Búsqueda por propiedad
Para buscar y obtener resultados de un dato en particular, debemos usar el método `.find()` con un objeto dentro indicando el valor que queremos obtener o buscar.

>Ejemplo:
`db.productos.find( { "price":4.99 } )`

Esto nos devolverá una ***lista de elementos*** donde *TODOS* coincidan con este dato en particular.
### Eliminar propiedades de las respuesta 
Al buscar documentos que coincidan con el criterio indicado, podemos indicar que los resultados, manejen solamente ciertas propiedades del documento.

>Ejemplo:
Tengo la siguiente lista de elementos...
```json
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
Al realizar la busqueda de los mismos, podemos definir qué propiedades queremos obtener de los resultados, algo así como el `SELECT name, price FROM` de SQL, pero con objetos *JSON*...

Por lo tanto podemos realizar nuestra busqueda de la siguiente manera, de acuerdo a la lista anteriormente mencionada:
`db.productos.find({"price":14.99}, {"name":1, "_id":0})`

...esto devolverá como resultado el siguiente array de documentos:
`[ { name: "Monitor 29'" }, { name: 'tablet barata' } ]`

demostrando que los documentos que coinciden con ese precio, son 2 y evitando campos que no nos interesan, como el `price` (que ya lo sabemos, y el `_id`)

---
### Ordenar resultados al buscar
Para poder ordenar los datos al buscar y obtener una lista de documentos, se utiliza el método `.sort()`.
***NOTESE QUE DENTRO DEL METODO `SORT()`, NO SE USA COMILLA PARA EL OBJETO PASADO COMO PARAMETRO***

>Ejemplo:
`db.productos.find().sort({price: 1})`

---
### Establecer límite en resultados
Para obtener un límite en la busqueda, le agregamos el método `.limit([cant.])` 

>Ejemplo:
`db.productos.find().limit(5)`

> Esto nos devuelve un listado de los primeros 5 documentos de entre todos los que listaría sin el límite.

---
### Contar documentos de una colección en particular
Podemos contar qué cantidad de documentos tenemos en la colección que queremos, con el método `.countDocuments()`

>Ejemplo:
`db.[coleccion].countDocuments()`

---
### Métodos de arrays en los resultados de busqueda.
Al ser MongoDB un intérprete de *Javascript*, podemos definir que a los resultados de una busqueda, le apliquemos un callback para cada uno de ellos, como por ejemplo el método `.forEach(callback)`

>Ejemplo:
`db.productos.find().forEach(producto => print("Nombre del producto: " + producto.name))`

>[!warning] NOTESE: 
>No se usa el método `console.log()` para imprimir en consola los datos, se usa `print()` de igual manera que `console.log()`.

---
### Actualizar datos de un documento
Para poder modificar propiedades de un documento, usamos el método dedicado `.update()`

>Ejemplo:
`db.productos.updateOne({busqueda de propiedad}, { $set: {propiedad a editar o agregar con su valor}} )`

`db.productos.updateOne({"name":"tablet barata"}, { $set: {"name":"tablet Samsung Galaxy X9"} } )`

esto *devolverá* un objeto con la siguiente estructura:
```js
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




## Referencias en los modelos

Al crear distintos modelos de datos, vamos a necesitar relacionar unos con otros, y crear referencias. Estas referencias, se pueden realizar de dos maneras, dependiendo de lo que necesite nuestros datos y aplicación.

- Podemos crear referencias manuales, que consiste en guardar el `_id` de un documento de la **colección A**  dentro de un campo en un documento de la **colección B**. Luego, la aplicación se encarga de resolver la relación.

```json
//documento de la coleccion 'autores'
{
	"_id": ObjectId("kdhskjh343434jhjkh23k1"),
	"nombre": "Gabriel García Marquez"
}

//documento de la coleccion 'libros'
{
	"_id":ObjectId("6as65fd514sdfghh87hggfhgf1"),
	"titulo":"Cien años de soledad",
	"autor_id": ObjectId("kdhskjh343434jhjkh23k1")
}
```


### Consultar a nivel de base de datos ($lookup)

Para consultar los datos combinados en una sola petición a la base de datos, MongoDB ofrece la etapa `$lookup`, que actua similar a un LEFT OUTER JOIN en SQL.
```json
db.libros.aggregate([
{
	$lookup:{
		from:"autores", //colección a vincular
		localField:"autor_id", // campo en la coleccion 'libros'
		foreignField:"_id", // campo en la coleccion 'autores'
		as:"datos_autor" // nombre del campo en la salida
	}
}
])
```

#### Mongoose (Abstraccion con ODM)

Si se utiliza la herramienta Mongoose, este proceso se vuelve nativo mediante la propiedad `ref` y la función `.populate()` que automatiza la búsqueda de los documentos de fondo de forma limpia en el código.

#### Creación de "listas virtuales" para relacionar documentos.

Esto permite definir una relación entre un modelo y otro sin necesidad de guardar manualmente un *array de ids* dentro del documento del primer modelo, evitando que crezca innecesariamente.

Supongamos que tenemos un modeo `cliente` y otro `empresas`.

1. Se debe configurar el modelo de la `Empresa` para que guarde el `id del cliente` al que pertenece. 

```js
import mongoose from 'mongoose';
const { Schema } = mongoose;

//1.esquema de la empresa
const empresaSchema = new Schema({
	nombre:{
		type: String,
		required:true
	},
	cuit:{
		type:String,
		required:true
	},
	clienteId:{
		type:Schema.Types.ObjectId,
		ref:'Cliente',
		required:true
	}
});

const Empresa = mongoose.model('Empresa', empresaSchema);
```

Luego, definimos el modelo del `Cliente`, de la  siguiente manera:
```js
import { Schema, model } from 'mongoose';

//2. Esquema del cliente
const clienteSchema = new Schema({
	nombre:{type:String, required:true },
	email:{type:String, required true, unique:true }
},{
//aqui va la configuracion crucial que permite los campos virtuales
//se incluyan al convertir a json los datos
	toJSON: { virtuals:true },
	toObject: { virtuals, true}
});

// Definimos el virtual populate, que permite vincular y traer los datos que queremos ANTES DE EXPORTA EL MODELO
clienteSchema.virtual('misEmpresas', {
	ref:'Empresa', //el MODELO que queremos buscar
	localField: '_id', //el campo de ESTE MODELO Cliente que coincide con la clave foránea
	foreignField: 'clienteId' //el campo en el modelo Empresa que guarda el ID del cliente
});

const Cliente = model('Cliente', clienteSchema);
```


#### Realizar búsqueda usando `.populate()`
Los campos virtuales no se guardan en MongoDB, por lo que **no se muestran por defecto** a menos que le indiquemos explícitamente a Mongoose que los resuelva usando el métódo `.populate('nombredelVirtual')`

```js
import Cliente from ('./modelos');

async function buscarClienteConEmpresas (_clienteId){
	try{
	//buscamos cliente y poblamos la lista virtual
	const cliente = await Cliente.findById(_clienteId)
	  .populate('misEmpresas');
	  
	  console.log(cliente);
	  /* Resultado esperado en consola: 
	  { 
		  _id: ObjectId("60d5ec..."), 
		  nombre: "Juan Pérez", 
		  email: "juan@example.com", 
		  misEmpresas: [ <-- Aquí aparece la lista virtual resuelta 
			  { _id: ObjectId("..."), 
				  nombre: "Empresa Alfa", 
				  cuit: "30-123456-1", 
				  clienteId: "60d5ec..." }, 
			  { _id: ObjectId("..."), 
				  nombre: "Empresa Beta", 
				  cuit: "30-789012-2", 
				  clienteId: "60d5ec..." 
			  }],
			   id: "60d5ec..." }
	   */
	   return cliente
	} catch (error) {
		console.log("error al buscar cliente:", error);
	}
}
```


