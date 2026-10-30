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
  `mongod`
esto disparará varios comandos y devolverá información en la ventana, que  no se cierra ni se termina mientras esté en uso.

Para conectar el Shell de la terminal, debemos abrir otra Terminal, y ejecutar 
`mongosh`
para que el shell se conecte con el servicio de "MongoD".

Ahi ya tenemos vinculado el Shell con el servicio y podemos ejecutar código de Mongo para administrar bases. 
>[!warning] IMPORTANTE
>Deben estar ambos procesos abiertos!!!.

---
### Conectar desde nodejs con mongodb local

Para comenzar a utilizar la el ORM de mongodb localmente, en código, debemos pasar la ubicación donde mongo está escuchando sus eventos.

Normalmente, esto figura en las lineas de comando que se ejecutan e informan el estado de *mongodb* al ejecutar `mongod`.
dentro de toda esa información, tenemos una linea que indica la URI, que por defecto es `127.0.0.1`
y el puerto que suele ser el `27017`

Por lo tanto, la URI local de mongo quedaría siendo `mongodb://127.0.0.1:27017/`
Esa conexión local a mongo, por defecto no pide username y password, pero se puede configurar esto.

---
### Crear usuario en mongodb local para crear una capa más de seguridad
Para configurar más seguridad localmente, abrimos `mongosh` (el shell de mongo) y usamos el comando
`use admin`
para utilizar la base mongo principal.

ejecutamos ahi el comando
`db.createUser()`
para registrar al usuario con el rol de superusuario(`root`)

```js
db.createUser({
	user:"tu_usuario",
	pwd:"tu_password_seguro",
	roles:[{
	role:"root", db:"admin"
	}]
})
```

Esto creará el user `tu_usuario` autenticado por el password.

Para que esto se lleve a cabo, y mongodb solicite autenticación localmente, debemos configurar también el archivo de configuración de mongoDB llamado 
`mongod-conf` o
`mongod.cfg`

Normalmente este archivo se encuentra en la carpeta de instalación de mongoDB en `c:\programfiles\MongoDB\Server\<version>\bin\mongod.cgf`

dentro del archivo buscamos la linea que está indicada con 
`#security`
se borra el hashpad (#) y se deja de la siguiente manera y luego se guardan los cambios:
```json
security:
	authorization: enabled
```

Una vez esté configurado esto, si intentas acceder mediante `mongodb://127.0.0.1.27017/` a secas, el servidor rechazará la conexión.

Para resolver esto, como lo hacemos también con Mongo Atlas, usamos el string de conexión siguiente:
```js
//Estructura: mongodb://USUARIO:CONTRASEÑA@IP:PUERTO/BASE_DE_DATOS?authSource=admin 
const MONGODB_URI = 'mongodb://tu_usuario:tu_password_seguro@127.0.0.1:27017/mi_base_datos?authSource=admin'
```

la parte final, `authSource=admin` le indica a Mongodb que los datos de autenticación se encuentran guardado en la base de datos admin.

---
### Ubicar localmente el lugar de guardado de las bases
Para ubicar el lugar lógico de guardado de la información, mongosh tiene un método que lo indica ya dentro de mongodb.
```Mongosh
db.adminCommand({
	getCmdLineOpts: 1
}).parsed.storage.dbPath
```

La carpeta no tiene separadas las bases por archivos enteros, mongodb utiliza un motor de almacenamiento interno llamado **WiredTiger**, el cual divide y encripta la información en múltiples archivos abstractos con extensiones `.wt` y archivos de registro de transacciones (**journals**)
Mover o renombrar alguno de estos archivos corromperá las bases guardadas de mongodb.

---
## Instalación como Servicio de Windows
Si al instalar el programa, dejamos seleccionado la casilla de "*instalar MongoDB*" como servicio de Windows, el mismo se ejecutará al iniciar windows directamente, estando "de fondo" todo el tiempo activo. Esto permite que al abrir Mongo DB Compass (GUI), el servicio responda correctamente y no haya que conectar manualmente o iniciarlo.

>[!warning] IMPORTANTE
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


## Identificar relaciones

Al comenzar a diagramar nuestra base de datos, vamos a tener que identificar las entidades que haran de guía para nuestro guardado de los datos. En general, las entidades se presentan como sustantivos de elementos componentes de nuestro proyecto, negocio, etc.

Al tener las entidades, deberemos responder las preguntas correspondientes a las relaciones que tienen dichas entidades entre si.

¿Puede existir más de una relación entre la entidad A y la B?
¿Puede existir más de una relación entre la entidad B y la A?

Ejemplo:
Si tuviéramos entidades como *libros*, *autores*, y *editoriales*, nos tenemos que preguntar:
¿un libro puede tener más de un autor? - Respuesta: NO
	relación ==uno a uno==

¿Un autor, puede escribir más de un libro? - Respuesta: SI
	relación: ==uno a muchos==

¿Un libro, puede corresponder a más de una editorial? - Respuesta SI
¿Una editorial, puede imprimir más de un libro? - Respuesta SI
	Relacion: ==muchos a muchos==
## ¿Insertar o referenciar datos?
Normalmente, cuando usamos una base de datos SQL, lo que se hace es si existen referencias de un registro con otros en otra tabla, se referencian mediante una FK, para relacionarlos y poder luego reestablecer estas relaciones en las busquedas.
En mongoDB, podemos optar por otro acercamiento, la inserción de los datos relacionados.

>[!success] La regla dorada de creación de esquemas en MongoDB
>"Los datos que son accesados juntos, deben estar guardado juntos"

Existen también guias para determinar mediante puntaje si corresponde insertar las relaciones o referenciarlas.

Esta guía se basa en varias preguntas que deberíamos hacernos al diseñar los esquemas.
De acuerdo a las respuestas obtenidas, se le va sumando puntos a Incrustar o Referenciar, según corresponda. ==NO TODAS LAS RESPUESTAS== corresponden al mismo puntaje, y esto se realiza normalmente entre dos entidades relacionadas.

- **Simpleza (Simplicity)**:
	¿Mantener las piezas de información juntas nos llevaría a un código y un modelo de datos más simple? 
	Si: Incrustar
	No: Referenciar

- **Van juntas (Go Together)**:
	¿Las piezas de información tiene un "posee un/a...", "contiene...", o relaciones similares?
	Si : Incrustar
	No: Referenciar

- **Atomicidad de la consulta (Query Atomicity)**:
	¿La aplicación realiza ambas consultas juntas normalmente?
	Si: Incrustar
	No: Referenciar

- **Complejidad al actualizar (Update Complexity)**:
	¿Las piezas de información se suelen actualizar juntas?
	Si: Incrustar
	No: Referenciar

- **Archivar (Archival)**:
	¿Ambas piezas de información deberían archivarse al mismo tiempo ante un borrado de una de ellas?
	Si: Incrustar
	No: Referenciar

- **Cardinalidad (Cardinality)**:
	¿Existe la posibilidad de que la cardinalidad de la parte incrustada crezca o sea alta?
	Si: Referenciar
	No: Incrustar

- **Datos duplicados (Data Duplication)**:
	¿La duplicación de datos sería muy complicada de manejar e incluso no deseada?
	Si: Referenciar
	No: Incrustar

- **Tamaño del documento (Document Size)**:
	¿El tamaño combinado de ambas piezas de información ocuparían mucha memoria o ancho de banda de transferencia para la aplicación?
	Si: Referenciar
	No: Incrustar

- **Crecimiento del documento (Document Growth)**:
	La parte de información que se incrusta, ¿crecería sin límites?
	Si: Referenciar
	No: Incrustar

- **Carga de trabajo (Workload)**:
	¿Las partes de información se escriben en diferentes momentos en una carga de trabajo de escritura-intensa?
	Si: Referenciar
	No: Incrustar

- **Individualismo (Individuality)**:
	¿La parte incrustada puede existir en nuestra base de datos sin ser referenciada por la parte padre o tiene sentido que exista sin ser referenciada?
	Si: Referenciar
	No: Incrustar

Al tener las respuestas a todas estas preguntas, se suman los puntos para determinar si conviene `Incrustar` los datos hijos en un documento padre, o si conviene `Referenciar`.

## Validación de esquemas

Normalmente, vamos a definir reglas para validar los esquemas de nuestros modelos de datos de MongoDb.
Para eso, vamos a hacer uso del operador  `$JsonSchema`

>[!important] Importante
>Solo los nuevos documentos o los actualizados se validan al insertarlos de nuevo en la colección. Los documentos ya preexistentes no son validados por el esquema.

Se puede correr el comando 
`db.collection.find( { $nor: [validator] } )`
para identificar los documentos que no son validados por el esquema actual.

Al validar un documento por el esquema, tenemos dos caminos que el sistema seguirá:
- Error
	Rechaza la operación de inserción o actualización.

- Warn
	Permite la operación a realizar, pero anota la violación de la validación en el log.

### Definiendo un esquema

Dejamos un ejemplo para la creación de un esquema con varias propiedades
```json
const bookstore_reviews = {
	bsonType: "object",
	required:["_id", "review_id", "user_id", "timestamp", "review", "rating"],
	additionalProperties: false, //esto evita que se agregen otras propiedades
	properties: {
		_id:{bsonType: "objectId" },
		review_id:{bsonType:"string"},
		user_id:{bsonType:"string"},
		timestamp:{bsonType:"date"},
		review:{bsonType:"string"},
		rating: {
			bsonType:"int",
			minimum: 0,
			maximum: 5,
		},
		comments:{
			bsonType:"array",
			maxItems: 3,
			items: {
				bsonType:"object",
			},
		},
	},
};
```

luego, al tener el esquema definido, corremos el comando que define el modelo;

```js
const schema_validation = { $jsonSchema: bookstore_reviews };

db.runCommand({
	collMod: "reviews",
	validator: schema_validation,
	validationLevel: "strict",
	validationAction: "error",
});
```

Si definimos un esquema de esta manera en un archivo `.js`, podemos cargarlo en el shell de MongoDB con el comando :
`load('ruta_al_archivo');`
el shell nos dará una respuesta `true` si se pudo cargar correctamente el esquema.

### Verificar el esquema de validación de una coleccion

Para poder verificar el esquema en el shell directamente, tenemos el comando
`db.getCollectionInfos({name: 'validador' });`
y si es correcto, se describirá el esquema para validar documentos de esa colección.


## recursos sobre el modelado de datos
Mongodb documentation: https://www.mongodb.com/docs/manual/data-modeling/
https://www.mongodb.com/resources/basics/databases/data-modeling

video: Los principios del modelado de datos
https://www.youtube.com/watch?v=0XVmuyPGy-o

video: Steve Hoberman, Pascal Desmarets, Daniel Coupal 2023
https://www.youtube.com/watch?v=TNGOzuZJg3E


## Comandos Básicos del Shell.
Se puede ejecutar el comando base con el método `.help` y esto nos devolverá la lista de comandos derivados del comando base.
ej:
```shell
db.help //esto dispara ayuda sobre los comandos db.(métodos)
```
### `db`
 este comando devuelve la base de datos que estamos utilizando (independientemente de que el prompt ya lo indica)

### `db.help()`
este comando nos dará una lista de todos los comandos que podemos aplicar en el shell, para identificar alguna tarea en específico que debamos realizar.

### `show dbs`
Este comando devuelve la lista de base de datos que tenemos creadas (==IMPORTANTE==: Las bases deben tener algún dato para figurar en esta lista)

### `use [dbname]`
Este comando "crea" una base de datos nueva de nombre [dbname] y pasa a ella directamente.
>[!example] ejemplo
>`>use peliculas`

### `db.dropDatabase`
Este comando **elimina** la base de datos **donde estamos parados**. No es un método en si, por lo que no lleva `()`

### `db.createCollection("[nombre_de_colección_a_crear]")`
Este comando nos permite crear una colleción nueva dentro de nuestra base de datos.
>[!exmaple] Ejemplo:
> `>db.createCollection("users")`

### `show collections`
Este comando nos devuelve las colecciones dentro de la base de datos actual. No lleva prefijo de la base de datos ni `db`

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
### Crear un modelo de coleccion
Podemos definir esquemas que son la "estructura" de los documentos que guardaremos en cada coleccion. Estos se definen justamente como objetos, y luego, mediante los drivers de mongoose, podemos guardarlos y esto creará las colecciones en nuestra base de datos

Para definir modelos, podemos usar el metodo `Schema` y `model` del driver de *mongoose* en nodejs.

podemos definir un nuevo esquema de la siguiente manera:

```js
import { Schema, model } from 'mongoose';

const miEsquema = new Schema({
	campo1: {
		type:String,
		required:true,
		trim:true
	},
	campo2: {
		type:Number,
		required:true		
	}, campo3: String,
		campo4: [{ propiedad1: String, date:Date}],//esto significa que campo4 toma array de datos
		campo5:{type: Date, default: Date.now },
		campo5: Boolean,
		meta: {
			votes:Number,
			favs:Number
		}
})

//luego, creamos el "modelo"
const esquema = model('Cliente', miEsquema);

export default esquema;
```

Esto generará un modelo con tal esquema, que al crear un nuevo documento, requerirá los campos indicados, y si definimos que son requeridos, no permitírá que el documento no lo tenga.

### Tipos de datos en los esquemas mongoose

- String
- Number
- Date
- Buffer
- Boolean
- Mixed
- ObjectId
- Array
- Decimal128
- Map
- UUID
- Double
- Int32

#### referencias a otro modelo dentro de un esquema
Podemos definir que un esquema utilice un valor de referencia de otro elemento de otra coleccion. Estas relaciones las hacemos por ID,

```js
import { Schema, model } from 'mongoose';

const miEsquema2 = new Schema({
	campo1: {
		type:String,
		required:true
		},
	campo2:{
		type:Schema.Types.ObjectId,
		ref:'Cliente', //aqui definimos el nombre del modelo que creamos en el paso anterior
		required:true
	}
})

const esquema2 = new model('publicacion', miEsquema2);
export default esquema2;
```

### validadores integrados
Podemos validar al construir un modelo, los datos ingresados, agregando una capa de seguridad en ese punto del código.

Según el tipo de dato, vamos a poder definir uno u otro.

```js
import { Schema, model } from 'mongoose';

const productoSchema = new Schema({
	nombre: {
		type:String,
		required:[true, 'el nombre es obligatorio']
	},
	precio: {
		type: Number,
		required: true,
		min:[0, 'el precio no puede ser negativo']
	},
	categoria: {
		type:String,
		enum: {
			values:['electronica', 'ropa', 'hogar'],
			message:'{VALUE} no es una categoría válida'
		}
	}
})

const Producto = model('Producto', productoSchema);
```

- Globales (cualquier tipo de dato)
	- **required** : [true / false]
- String
	- **minLength**: define la longitud mínima de caracteres permitida.
	- **maxLength**: define la cantidad máxima de caracteres permitida.
	- **match**: valida que el texto cumpla con una Expresión Regular específica
	- **enum**: ['valor1', 'valor2', ..., 'valorN'] : define una lista donde se aceptan solo esos valores declarados para guardar
- Number
	- **min**: valor mínimo que acepta el registro
	- **max**: valor máximo permitido.
- Date
	- **min**: fecha mínima permitida (puede ser un objeto `Date` o una cadena convertible en fecha)
	- **max**: fecha máxima permitida
```js
	  fechaReserva: {
		  type:Date,
		  min: '2026-01-01',
		  max: new Date() 
	  }
```

#### Definir los validadores y el mensaje de error

Mongoose permite configurar de 2 maneras equivalentes los mensajes de error de los validadores.
Tambien se acepta `{VALUE}` para interpolar el valor evaluado en el mensaje de error.

- Array syntax: `min:[6, 'debe ser al menos de 6 digitos el valor, {VALUE}]`
- Object syntax: `enum: { values: ["cafe", "te"], message: '{VALUE} no es una opcion valida' }`

>[!warning] IMPORTANTE
>`Unique: true` NO ES UN VALIDADOR, se usa para crear índices de valores únicos, pero esto no evita que se creen más de un documento con el mismo valor, esto se debe validar manualmente.

### validadores personalizados
Podemos definir nuestros propios validadores de datos. Definimos una propiedad `validate` dentro del esquema en la propiedad que querramos validar, donde le pasamos una función o un objeto con la propiedad `validator` y un `message` para dar el mensaje de error.

```js
import { Schema, model } from 'mongoose';

const usuarioSchema = new Schema({
	username: {
		type:String,
		required:true,
		validate: {
			validator: function(v) {
				//solo permite letras y numeros
				return /^[a-zA-Z0-9]+\$/.test(v);
			},
			message: props => `${props.value} no es un nombre de usuario válido. solo se aceptan letras y nros`
		}
	}
})

const usuario = new model('usuario', usuarioSchema);
export default usuario;

```


>[!warning] CUIDADO!
>por defecto, los validadores se ejecutan solamente al crear un documento. Si buscamos para actualizar un documento existente con `findOneAndUpdate()`, el proceso no se realiza.
>Para esto, debemos explícitamente declararlo al correr la actualización, indicando de la siguiente manera

```js
await producto.findByIdAndUpdate(
	id, 
	{ precio: -50},
	{new: true, runValidators: true } //esto activa las validaciones en la operacion actual
);
```



Tambien podemos crear propiedaes "virtuales", que se usarán cuando realicemos busquedas que necesiten de más relaciones.

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


## Mongoose para Node.js

**Mongoose** es una biblioteca para trabajar con MongoDB desde Node.js. Permite definir esquemas, crear modelos, validar datos, consultar documentos y gestionar operaciones sobre la base de datos.

Su principal ventaja frente a utilizar directamente el driver de MongoDB es que agrega una capa de estructura y validación a los datos.

La guía está organizada por conceptos y métodos, con ejemplos orientados a una API REST desarrollada con **Node.js, Express y MongoDB**.

# 1. Conceptos fundamentales

Antes de aprender los métodos, conviene distinguir estos conceptos:

| Concepto               | Qué significa                                               | Ejemplo                                   |
| ---------------------- | ----------------------------------------------------------- | ----------------------------------------- |
| Schema                 | Define la estructura y las reglas de los documentos.        | `productoSchema`                          |
| Model                  | Permite interactuar con una colección de MongoDB.           | `Producto`                                |
| Document               | Representa un registro concreto de la colección.            | Un producto creado                        |
| Query                  | Representa una consulta a la base de datos.                 | Buscar productos por precio               |
| Validation             | Comprueba que los datos cumplan determinadas reglas.        | Precio mayor que cero                     |
| Middleware de Mongoose | Ejecuta lógica antes o después de determinadas operaciones. | Hashear una contraseña antes de guardarla |
La relación entre estos conceptos es:

**Schema → Model → Documentos en MongoDB**

Por ejemplo, el esquema define qué propiedades puede tener un producto, el modelo permite crear y consultar productos, y cada producto almacenado es un documento.

# 2. Conexión con MongoDB

Se suele crear un módulo separado para gestionar la conexión.

```js
// config/database.js

const mongoose = require('mongoose');

async function conectarDB() {
    await mongoose.connect(process.env.MONGO_URI);

    console.log('Conectado a MongoDB');
}

module.exports = conectarDB;
```

La variable `MONGO_URI` contiene la cadena de conexión, normalmente almacenada en un archivo `.env` durante el desarrollo.

Para iniciar el servidor:

```js
const conectarDB = require('./config/database');

async function iniciarServidor() {
    try {
        await conectarDB();

        app.listen(3000, () => {
            console.log('Servidor iniciado');
        });
    } catch (error) {
        console.error('No se pudo conectar a MongoDB:', error);
        process.exit(1);
    }
}

iniciarServidor();
```

**Importante:** si la aplicación depende de MongoDB para funcionar, conviene iniciar el servidor después de confirmar la conexión.

Métodos y propiedades útiles de conexión:

|Método o propiedad|Función|
|---|---|
|`mongoose.connect(uri)`|Establece la conexión.|
|`mongoose.disconnect()`|Desconecta Mongoose.|
|`mongoose.connection.readyState`|Indica el estado de la conexión.|
|`mongoose.connection.close()`|Cierra la conexión actual.|

Los valores habituales de `readyState` son 
- `0` (desconectado)
- `1` (conectado)
- `2` (conectando...) 
- `3` (desconectando...).

# 3. Crear un Schema y un Model

Este es uno de los conceptos más importantes de Mongoose.
Supongamos que necesitás gestionar productos en tu API.

```js
// models/Producto.js
const mongoose = require('mongoose');

const productoSchema = new mongoose.Schema({
    nombre: {
        type: String,
        required: [true, 'El nombre es obligatorio'],
        trim: true
    },

    precio: {
        type: Number,
        required: true,
        min: [0.01, 'El precio debe ser mayor que cero']
    },

    stock: {
        type: Number,
        default: 0,
        min: 0
    },

    activo: {
        type: Boolean,
        default: true
    }
}, {
    timestamps: true
});

const Producto = mongoose.model('Producto', productoSchema);

module.exports = Producto;
```

### ¿Qué aporta cada opción?

- `type`: define el tipo de dato.
- `required`: establece que el campo es obligatorio.
- `trim`: elimina espacios al principio y al final de una cadena.
- `min`: establece un valor mínimo para números.
- `default`: asigna un valor predeterminado.
- `timestamps`: agrega automáticamente `createdAt` y `updatedAt`.

*Mongoose* utiliza el esquema para validar los datos en las operaciones correspondientes, pero no reemplaza todas las validaciones que necesita una API.

Por ejemplo, si un usuario envía un precio negativo, Mongoose puede rechazar la creación del documento. Sin embargo, las reglas de negocio —como comprobar que un producto pertenece a una categoría permitida— pueden requerir lógica adicional.

# 4. Métodos más útiles de Mongoose

Estos son los métodos que más vas a utilizar al desarrollar una API.

## 4.1. Crear documentos
##### `Model.create()`
Crea y guarda uno o varios documentos.

```js
const nuevoProducto = await Producto.create({
    nombre: 'Manzana',
    precio: 1500,
    stock: 20
});
```

Si la operación tiene éxito, devuelve el documento creado.
Si los datos incumplen las validaciones de Mongoose, la operación puede generar un error.
**También permite crear varios documentos:**

```js
const productos = await Producto.create([
    { nombre: 'Manzana', precio: 1500 },
    { nombre: 'Pera', precio: 1800 }
]);
```

##### `new Model()` y `.save()`
También podés crear un documento y guardarlo en dos pasos:

```js
const producto = new Producto({
    nombre: 'Manzana',
    precio: 1500,
    stock: 20
});

await producto.save();
```

La diferencia principal es que `new Producto()` construye el documento en memoria, mientras que `.save()` lo persiste en la base de datos.

Este enfoque es útil cuando necesitás preparar el documento, modificarlo o ejecutar lógica antes de guardarlo.

### ¿Cuál conviene utilizar?

|Método|Cuándo utilizarlo|
|---|---|
|`Model.create(datos)`|Cuando querés crear y guardar directamente.|
|`new Model(datos)`|Cuando necesitás construir el documento antes de guardarlo.|
|`document.save()`|Cuando querés guardar un documento nuevo o persistir cambios en uno existente.|

---

## 4.2. Buscar documentos

##### `Model.find()`
Devuelve todos los documentos que cumplen un criterio. Si no indicás un filtro, devuelve todos los documentos de la colección.

```js
const productos = await Producto.find();
```

Buscar solamente productos activos:
```js
const productos = await Producto.find({
    activo: true
});
```

Buscar productos dentro de un rango de precios:
```js
const productos = await Producto.find({
    precio: {
        $gte: 1000,
        $lte: 3000
    }
});
```

Los operadores `$gte` y `$lte` significan, respectivamente, «mayor o igual» y «menor o igual».

**Importante:** `find()` devuelve un array. Si no encuentra resultados, devuelve un array vacío `[]`, no devuelve `null`.

##### `Model.findOne()`
Devuelve el primer documento que coincide con el filtro o `null` si no encuentra ninguno.

```js
const producto = await Producto.findOne({
    nombre: 'Manzana'
});
```

Es útil cuando buscás un documento por una propiedad que debería identificarlo de manera única, como un email o un código de producto. Para garantizar esa unicidad, necesitás definir la restricción correspondiente en la base de datos.

##### `Model.findById()`
Busca un documento por su identificador `_id`.
```js
const producto = await Producto.findById(req.params.id);
```

Equivale conceptualmente a buscar por `_id`:
```js
const producto = await Producto.findOne({
    _id: req.params.id
});
```

Si el identificador tiene un formato inválido para la conversión a `ObjectId`, Mongoose puede generar un `CastError`.
### Diferencias entre los métodos de búsqueda

| Método       | Resultado              | Si no encuentra resultados                |
| ------------ | ---------------------- | ----------------------------------------- |
| `find()`     | Array de documentos    | `[]`                                      |
| `findOne()`  | Un documento           | `null`                                    |
| `findById()` | Un documento por `_id` | `null`, si el ID es válido pero no existe |

---

## 4.3. Actualizar documentos

Hay varias maneras de actualizar un documento.
##### `Model.findByIdAndUpdate()`
Busca un documento por su `_id` y actualiza sus campos.

```js
const producto = await Producto.findByIdAndUpdate(
    req.params.id,
    {
        precio: 2000
    },
    {
        new: true,
        runValidators: true
    }
);
```

Las opciones importantes son:

- `new: true`: devuelve el documento actualizado.
- `runValidators: true`: ejecuta las validaciones del esquema aplicables a la actualización.

**Atención:** las validaciones de las operaciones de actualización tienen diferencias respecto de las que se ejecutan con `save()`. Por ejemplo, las validaciones de actualización suelen ejecutarse sobre los campos modificados, no necesariamente sobre todo el documento.

Además, `findByIdAndUpdate()` devuelve `null` si el documento no existe. Conviene comprobar ese resultado.
##### `Model.updateOne()`
Actualiza el primer documento que coincide con el filtro.

```js
const resultado = await Producto.updateOne(
    { _id: id },
    { $set: { precio: 2000 } },
    { runValidators: true }
);
```

Devuelve información sobre la operación, no el documento actualizado.

Entre las propiedades del resultado se encuentran:

- `matchedCount`: cantidad de documentos que coincidieron con el filtro.
- `modifiedCount`: cantidad de documentos que se modificaron.

Si el producto no existe, `matchedCount` normalmente será `0`.

##### `Model.findOneAndUpdate()`

Busca por un filtro y actualiza el documento encontrado.

```js
const producto = await Producto.findOneAndUpdate(
    { nombre: 'Manzana' },
    { $set: { stock: 50 } },
    {
        new: true,
        runValidators: true
    }
);
```

Es similar a `findByIdAndUpdate()`, pero permite utilizar cualquier criterio de búsqueda.

### ¿Cuál conviene utilizar?

- `findByIdAndUpdate()`: cuando tenés el identificador del documento.
- `findOneAndUpdate()`: cuando necesitás buscar por otro criterio.
- `updateOne()`: cuando solo te interesa ejecutar la actualización y conocer su resultado.
- `document.save()`: cuando recuperaste el documento, lo modificaste y querés guardar sus cambios.

Por ejemplo, para modificar un documento existente:

```js
const producto = await Producto.findById(id);

if (!producto) {
    // Gestionar el caso de producto inexistente.
}

producto.precio = 2000;

await producto.save();
```

Este último enfoque es especialmente útil cuando necesitás trabajar con el documento y ejecutar lógica antes de persistir los cambios.

---

## 4.4. Eliminar documentos

##### `Model.findByIdAndDelete()`
Elimina un documento por su identificador y devuelve el documento eliminado, o `null` si no existe.

```js
const producto = await Producto.findByIdAndDelete(id);
```

##### `Model.deleteOne()`
Elimina el primer documento que coincide con un filtro.

```js
const resultado = await Producto.deleteOne({
    nombre: 'Manzana'
});
```

Devuelve información sobre la operación, incluyendo `deletedCount`.

##### `Model.deleteMany()`
Elimina todos los documentos que coinciden con un filtro.

```js
const resultado = await Producto.deleteMany({
    activo: false
});
```

**Precaución:** utilizá `deleteMany()` con filtros cuidadosamente definidos. Un filtro vacío puede eliminar todos los documentos de la colección.

---
## 4.5. Contar y comprobar documentos

##### `Model.countDocuments()`
Cuenta los documentos que coinciden con un filtro.

```js
const cantidad = await Producto.countDocuments({
    activo: true
});
```

Sin filtro, cuenta los documentos de la colección.

##### `Model.exists()`
Comprueba si existe un documento que coincida con el filtro.

```js
const existe = await Producto.exists({
    nombre: 'Manzana'
});

if (existe) {
    console.log('El producto existe');
}
```

Devuelve un objeto con el `_id` si encuentra una coincidencia, o `null` si no existe.

Es útil para comprobar la existencia de un registro sin necesidad de recuperar todos sus campos.

---
# 5. Métodos para controlar los resultados de una búsqueda
Estos métodos son especialmente útiles cuando construís endpoints para listar productos, clientes o pedidos.

#### `select()`: elegir qué campos devolver

```
const productos = await Producto.find()
    .select('nombre precio stock');
```

Solo selecciona los campos indicados, además de `_id`, que se incluye por defecto.

También podés excluir campos:
```js
const productos = await Producto.find()
    .select('-stock');
```

Esto permite reducir la cantidad de información devuelta. Es especialmente importante cuando trabajás con documentos que contienen datos privados.

#### `sort()`: ordenar resultados
```js
const productos = await Producto.find()
    .sort({ precio: 1 });
```

- `1`: orden ascendente.
- `-1`: orden descendente.

Por ejemplo, para ordenar los más caros primero:
```js
const productos = await Producto.find()
    .sort({ precio: -1 });
```

#### `limit()`: limitar la cantidad de resultados
```
const productos = await Producto.find()
    .limit(10);
```

Devuelve como máximo diez documentos.

#### `skip()`: saltar resultados
```js
const productos = await Producto.find()
    .skip(10)
    .limit(10);
```

Esto permite obtener una página de resultados.

Por ejemplo, con una página de diez productos:

```js
const pagina = 2;
const limite = 10;

const productos = await Producto.find()
    .skip((pagina - 1) * limite)
    .limit(limite);
```

Esta consulta devuelve los productos de la segunda página.

Para una paginación completa, normalmente también necesitás contar los resultados para calcular la cantidad de páginas. En colecciones muy grandes, la paginación con `skip()` puede resultar costosa; en esos casos puede convenir una paginación basada en cursores.

## `lean()`: obtener objetos JavaScript simples
```js
const productos = await Producto.find()
    .lean();
```

Normalmente, Mongoose devuelve documentos que incluyen **métodos** y **funcionalidades** propias de la biblioteca.

Con `lean()`, devuelve objetos JavaScript simples, sin la funcionalidad completa de los documentos de Mongoose.

Es útil para endpoints de solo lectura, porque reduce el trabajo que realiza **Mongoose** al construir los resultados.

**Diferencia importante:** un objeto obtenido con `lean()` no tiene métodos como `.save()`.
## Encadenar consultas

Podés combinar varios de estos métodos:
```js
const productos = await Producto.find({
    activo: true
})
    .select('nombre precio stock')
    .sort({ precio: 1 })
    .skip(0)
    .limit(10)
    .lean();
```

La consulta busca productos activos, selecciona los campos necesarios, los ordena por precio y devuelve hasta diez resultados como objetos simples.

---

# 6. Validaciones de Mongoose
Las validaciones permiten evitar que se guarden documentos que incumplen las reglas definidas en el esquema.

## Validaciones más utilizadas

|Regla|Función|Ejemplo|
|---|---|---|
|`required`|Campo obligatorio|`required: true`|
|`min`|Valor numérico mínimo|`min: 1`|
|`max`|Valor numérico máximo|`max: 100`|
|`minlength`|Longitud mínima de una cadena|`minlength: 3`|
|`maxlength`|Longitud máxima de una cadena|`maxlength: 50`|
|`enum`|Valores permitidos|`enum: ['activo', 'inactivo']`|
|`match`|Patrón para validar cadenas|`match: /^[A-Z]+$/`|
|`validate`|Validación personalizada|Una función que devuelve `true` o `false`|

### Ejemplo con validaciones

```js
const productoSchema = new mongoose.Schema({
    nombre: {
        type: String,
        required: [true, 'El nombre es obligatorio'],
        minlength: [3, 'El nombre debe tener al menos 3 caracteres']
    },

    precio: {
        type: Number,
        required: true,
        min: [0.01, 'El precio debe ser mayor que cero']
    },

    categoria: {
        type: String,
        enum: ['bebidas', 'frutas', 'verduras']
    }
});
```

Si el precio es negativo o el nombre no cumple la longitud mínima, Mongoose puede generar un error de validación.

### Validación personalizada

Supongamos que querés que un producto tenga al menos una etiqueta.

```js
etiquetas: {
    type: [String],
    validate: {
        validator: function(etiquetas) {
            return etiquetas.length >= 1;
        },
        message: 'El producto debe tener al menos una etiqueta'
    }
}
```

Esta regla se ejecuta cuando Mongoose realiza la validación correspondiente del documento.

**Tené en cuenta:** las validaciones de Mongoose protegen el documento durante las operaciones que las ejecutan, pero no garantizan por sí solas que todos los datos de la base sean válidos, especialmente si existen escrituras que las omiten.

# 7. Manejo de errores

En una API, no alcanza con saber crear o buscar documentos. También necesitás identificar qué ocurrió cuando una operación falla.

Los errores más importantes que conviene reconocer son:

|Error|Qué significa|Respuesta HTTP habitual|
|---|---|---|
|`ValidationError`|Uno o más campos no cumplen las validaciones del esquema.|`400 Bad Request`|
|`CastError`|Mongoose no pudo convertir un valor al tipo esperado.|`400 Bad Request`, si el valor proviene de la solicitud|
|Error `E11000`|Se intentó duplicar un valor sujeto a un índice único.|`409 Conflict`|
|Documento inexistente|La consulta no encontró el registro.|`404 Not Found` cuando el recurso solicitado no existe|
|Error inesperado|Fallo no previsto durante el procesamiento.|`500 Internal Server Error`|

Estos códigos son convenciones habituales; la respuesta exacta depende del contrato de tu API y del contexto del error.

## Ejemplo en un controlador Express

```js
async function crearProducto(req, res, next) {
    try {
        const producto = await Producto.create(req.body);

        return res.status(201).json({
            mensaje: 'Producto creado correctamente',
            producto
        });

    } catch (error) {
        next(error);
    }
}
```

El controlador delega el tratamiento del error al middleware de Express.

Por ejemplo:

```js
app.use((err, req, res, next) => {
    if (err.name === 'ValidationError') {
        return res.status(400).json({
            mensaje: 'Los datos enviados no son válidos',
            errores: Object.values(err.errors).map(
                error => error.message
            )
        });
    }

    if (err.name === 'CastError') {
        return res.status(400).json({
            mensaje: 'El formato de un dato es inválido'
        });
    }

    if (err.code === 11000) {
        return res.status(409).json({
            mensaje: 'Ya existe un registro con ese valor'
        });
    }

    console.error(err);

    return res.status(500).json({
        mensaje: 'Error interno del servidor'
    });
});
```

Este es un ejemplo inicial. En una API real, también conviene validar la estructura de `req.body`, comprobar los identificadores recibidos y evitar enviar al cliente detalles internos de los errores.

---

# 8. Relaciones entre documentos: `ref` y `populate()`

En MongoDB podés guardar información relacionada de distintas maneras. Una opción habitual es guardar el identificador de otro documento.

Supongamos que tenés dos modelos: `Cliente` y `Pedido`.

Un pedido pertenece a un cliente, por lo que podés definir una referencia.

### Modelo Pedido

```js
const pedidoSchema = new mongoose.Schema({
    cliente: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'Cliente',
        required: true
    },

    estado: {
        type: String,
        enum: ['pendiente', 'preparado', 'entregado'],
        default: 'pendiente'
    }
});

const Pedido = mongoose.model('Pedido', pedidoSchema);
```

La propiedad `ref: 'Cliente'` indica a Mongoose qué modelo está asociado con esa referencia.

Por ejemplo, un pedido podría almacenar algo como esto:

```js
{
    "_id": "671a123456789abcdef12345",
    "cliente": "671a987654321abcdef12345",
    "estado": "pendiente"
}
```

El campo `cliente` contiene el identificador del cliente, no necesariamente todos sus datos.

## ¿Qué hace `populate()`?

Permite recuperar los datos del documento relacionado mediante esa referencia.

```
const pedidos = await Pedido.find()
    .populate('cliente');
```

En lugar de recibir solamente el identificador del cliente, los resultados incluyen los datos del documento asociado, si existe.

También podés seleccionar los campos que querés recuperar:
```js
const pedidos = await Pedido.find()
    .populate('cliente', 'nombre email');
```

De esta manera, cada pedido incluirá únicamente los campos `nombre` y `email` del cliente relacionado, además de los campos que correspondan al propio pedido.

**Importante:** `populate()` no crea una relación equivalente a una clave foránea de SQL. La referencia debe apuntar a un documento válido, y tu aplicación debe gestionar los casos en los que el documento relacionado no existe.

### ¿Cuándo conviene usar referencias?

Son útiles cuando:

- Un cliente tiene muchos pedidos.
- Muchos pedidos pueden pertenecer al mismo cliente.
- Necesitás consultar los datos del cliente desde el pedido.
- Querés evitar duplicar información que cambia frecuentemente.

Sin embargo, no toda relación necesita `populate()`. A veces es más eficiente recuperar los documentos por separado.

---
# 9. Arrays y documentos embebidos

Mongoose permite definir arrays de valores y arrays de subdocumentos.

Por ejemplo, si un cliente puede tener varias direcciones, podés definirlas dentro del mismo documento.

```js
const direccionSchema = new mongoose.Schema({
    calle: {
        type: String,
        required: true
    },

    numero: {
        type: String,
        required: true
    },

    localidad: {
        type: String,
        required: true
    }
});

const clienteSchema = new mongoose.Schema({
    nombre: {
        type: String,
        required: true
    },

    direcciones: {
        type: [direccionSchema],
        default: []
    }
});
```

Un cliente podría almacenarse así:

```js
{
    "nombre": "Juan",
    "direcciones": [
        {
            "calle": "San Martín",
            "numero": "125",
            "localidad": "Buenos Aires"
        },
        {
            "calle": "Belgrano",
            "numero": "450",
            "localidad": "Buenos Aires"
        }
    ]
}
```

Esto resulta práctico cuando las direcciones forman parte del cliente y necesitás recuperarlas junto con él.

Si necesitás que exista al menos una dirección, debés agregar una validación personalizada: declarar un array como obligatorio no garantiza por sí solo que tenga elementos.

### ¿Cuándo usar subdocumentos y cuándo referencias?

|Situación|Alternativa habitual|
|---|---|
|Un cliente tiene varias direcciones propias.|Array de subdocumentos.|
|Un cliente tiene muchos pedidos independientes.|Referencias entre documentos.|
|Un pedido debe conservar los precios originales de sus productos.|Guardar una copia de los datos relevantes en los artículos del pedido.|
|Varios pedidos comparten un producto del catálogo.|Referencia al producto y datos históricos embebidos en cada pedido.|

Esta última distinción es importante: **una referencia permite acceder al producto actual, pero no conserva automáticamente una copia de sus datos históricos**.

Por ejemplo, un pedido puede almacenar el identificador del producto y, además, su nombre, precio unitario y cantidad al momento de la compra.

---

# 10. Middleware de Mongoose
Los middleware permiten ejecutar lógica en determinados momentos del ciclo de vida de un documento o de una consulta.

Por ejemplo, podés ejecutar una función antes de guardar un documento.
```js
productoSchema.pre('save', function() {
    console.log('Preparando el documento para guardarlo');
});
```

También existen middleware posteriores, como `post`, que permiten ejecutar lógica después de determinadas operaciones.

Algunos usos posibles son:

- Transformar o normalizar datos.
- Hashear contraseñas antes de guardarlas.
- Registrar determinadas operaciones.
- Ejecutar lógica asociada al ciclo de vida de un documento.

Hay una distinción importante: **los middleware de documentos y los de consultas no son equivalentes**.

Por ejemplo, un middleware `pre('save')` no se ejecuta automáticamente cuando utilizás `findByIdAndUpdate()`.

Si necesitás una lógica común para diferentes operaciones, debés diseñarla teniendo en cuenta los métodos que realmente se utilizan.

Para contraseñas, además, es importante no depender exclusivamente de un middleware `save` si la aplicación también modifica contraseñas mediante operaciones de actualización.

# 11. Métodos intermedios que conviene conocer
Estos métodos no son imprescindibles para empezar, pero resultan útiles a medida que tu API crece.

|Método o concepto|Para qué sirve|
|---|---|
|`Model.aggregate()`|Realizar agregaciones, agrupaciones y cálculos sobre los documentos.|
|`Model.distinct()`|Obtener valores distintos de un campo.|
|`Model.bulkWrite()`|Ejecutar varias operaciones de escritura en una sola solicitud al servidor de MongoDB.|
|`document.toObject()`|Convertir un documento de Mongoose en un objeto JavaScript simple.|
|`document.toJSON()`|Obtener la representación JSON del documento.|
|`document.isModified()`|Comprobar si un campo fue modificado.|
|`document.validate()`|Ejecutar las validaciones del documento sin necesidad de guardarlo.|
|`Model.discriminator()`|Crear modelos especializados que comparten un esquema base.|

### Ejemplo de `aggregate()`
Supongamos que querés calcular cuántos productos hay por categoría:
```js
const resultado = await Producto.aggregate([
    {
        $group: {
            _id: '$categoria',
            cantidad: { $sum: 1 }
        }
    }
]);
```

MongoDB agrupa los productos por categoría y cuenta cuántos hay en cada grupo.

La agregación es especialmente útil para informes, estadísticas y consultas más complejas.

### Ejemplo de `distinct()`

```js
const categorias = await Producto.distinct('categoria');
```

Devuelve los valores distintos de `categoria`.

### Ejemplo de `toObject()`

```js
const producto = await Producto.findById(id);

if (producto) {
    const objeto = producto.toObject();
    console.log(objeto);
}
```

Esto es útil cuando necesitás manipular los datos como un objeto JavaScript común, aunque también debés tener en cuenta las transformaciones que pueda aplicar tu esquema.

---

# 12. Cómo organizar Mongoose dentro de una API Express

Una arquitectura sencilla puede separar las rutas, los controladores y los modelos.

```
src/
├── config/
│   └── database.js
├── models/
│   └── Producto.js
├── controllers/
│   └── productoController.js
├── routes/
│   └── productoRoutes.js
├── middlewares/
│   └── errorHandler.js
└── app.js
```

### Responsabilidades

| Componente              | Responsabilidad                                            |
| ----------------------- | ---------------------------------------------------------- |
| `database.js`           | Configurar y establecer la conexión con MongoDB.           |
| `Producto.js`           | Definir el esquema y el modelo de Mongoose.                |
| `productoController.js` | Procesar la solicitud HTTP y construir la respuesta.       |
| `productoRoutes.js`     | Asociar las rutas HTTP con sus controladores.              |
| `errorHandler.js`       | Centralizar el tratamiento de errores.                     |
| `app.js`                | Configurar Express y registrar las rutas y los middleware. |

Para proyectos más grandes, también podés agregar una capa de servicios que contenga las reglas de negocio.

Por ejemplo:

```
Ruta → Controlador → Servicio → Modelo de Mongoose → MongoDB
```

No es obligatorio agregar un servicio para cada operación. Resulta útil cuando la lógica de negocio supera lo que conviene mantener en un controlador.

## Ejemplo de un controlador que crea un producto

```js
const Producto = require('../models/Producto');

async function crearProducto(req, res, next) {
    try {
        const producto = await Producto.create(req.body);

        return res.status(201).json({
            mensaje: 'Producto creado correctamente',
            producto
        });
    } catch (error) {
        next(error);
    }
}

module.exports = { crearProducto };
```

En este ejemplo, el controlador llama directamente al modelo. Mongoose valida los datos durante la creación y, si ocurre un error, el controlador lo deriva al middleware de errores.

En una aplicación real, antes de crear el producto también conviene validar la entrada y comprobar las reglas de negocio pertinentes. Por ejemplo, que el usuario tenga autorización para crear productos.

---

# 13. Resumen de los métodos que deberías dominar primero

Esta es una lista de referencia rápida para tener a mano mientras programás.

|Necesidad|Método|
|---|---|
|Crear un documento|`Model.create()`|
|Construir un documento|`new Model()`|
|Guardar un documento|`document.save()`|
|Buscar todos los documentos|`Model.find()`|
|Buscar uno por criterio|`Model.findOne()`|
|Buscar por identificador|`Model.findById()`|
|Actualizar por identificador|`Model.findByIdAndUpdate()`|
|Actualizar por criterio|`Model.findOneAndUpdate()`|
|Actualizar sin recuperar el documento|`Model.updateOne()`|
|Eliminar por identificador|`Model.findByIdAndDelete()`|
|Eliminar por criterio|`Model.deleteOne()`|
|Eliminar varios documentos|`Model.deleteMany()`|
|Contar documentos|`Model.countDocuments()`|
|Comprobar si existe un documento|`Model.exists()`|
|Recuperar documentos relacionados|`.populate()`|
|Seleccionar campos|`.select()`|
|Ordenar resultados|`.sort()`|
|Limitar resultados|`.limit()`|
|Saltar resultados|`.skip()`|
|Obtener objetos simples|`.lean()`|
|Agrupar y calcular datos|`Model.aggregate()`|
|Convertir un documento en objeto|`document.toObject()`|
|Ejecutar validaciones|`document.validate()`|

## Orden recomendado para aprender

Para consolidar Mongoose a nivel principiante-intermedio, te recomiendo estudiar estos temas en este orden:

1. **Schema y Model:** tipos, valores predeterminados y validaciones.
2. **CRUD:** crear, buscar, actualizar y eliminar documentos.
3. **Async/await y manejo de errores:** comprender cómo se propagan los errores de Mongoose.
4. **Consultas:** filtros, operadores, `select()`, `sort()`, `limit()` y `skip()`.
5. **Relaciones:** referencias con `ref`, `populate()` y subdocumentos.
6. **Validaciones de actualización:** diferencias entre `save()` y los métodos `findOneAndUpdate()` o `findByIdAndUpdate()`.
7. **Agregaciones:** aprender `aggregate()` para informes y cálculos.
8. **Middleware y servicios:** organizar la lógica cuando la aplicación crece.

**Si dominás los primeros seis puntos, ya vas a tener una base sólida para desarrollar la mayoría de las operaciones habituales de una API REST con Express y MongoDB.** Los últimos dos te ayudarán a resolver problemas más complejos y a mantener una arquitectura ordenada.

