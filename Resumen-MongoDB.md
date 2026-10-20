# MongoDB NoSQL 

## instalación de MongoDB Server y Shell

para instalar el servidor, de acuerdo a la versión de Windows que tengamos, debemos descargar el paquete instalador desde la web oficial *https://www.mongodb.com/es*

Si usamos Windows 10, la versión soportada es la 6.0.18. Instalar una versión más nueva, no dejará conectar el servicio ni iniciarlo.

para eso, instalamos el paquete de forma "completa" al iniciar el MSI package, y se puede seleccionar si se instala como servicio de Windows, o si es necesario ejecutarlo cada vez que vayamos a utilizarlo.

Finalizado esto, debemos crear la carpeta  
> `C:/Data/db/`

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
### Conectar desde nodejs con mongodb local

Para comenzar a utilizar la el ORM de mongodb localmente, en código, debemos pasar la ubicación donde mongo está escuchando sus eventos.

Normalmente, esto figura en las lineas de comando que se ejecutan e informan el estado de *mongodb* al ejecutar `mongod`.
dentro de toda esa información, tenemos una linea que indica la URI, que por defecto es `127.0.0.1`
y el puerto que suele ser el `27017`

Por lo tanto, la URI local de mongo quedaría siendo `mongodb://127.0.0.1:27017/`
Esa conexión local a mongo, por defecto no pide username y password, pero se puede configurar esto.

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

### Ubicar localmente el lugar de guardado de las bases

Para ubicar el lugar lógico de guardado de la información, mongosh tiene un método que lo indica ya dentro de mongodb.
```Mongosh
db.adminCommand({
	getCmdLineOpts: 1
}).parsed.storage.dbPath
```

La carpeta no tiene separadas las bases por archivos enteros, mongodb utiliza un motor de almacenamiento interno llamado **WiredTiger**, el cual divide y encripta la información en múltiples archivos abstractos con extensiones `.wt` y archivos de registro de transacciones (**journals**)
Mover o renombrar alguno de estos archivos corromperá las bases guardadas de mongodb.
### Comandos Básicos del Shell.
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



