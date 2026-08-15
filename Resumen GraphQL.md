

## Creando una query en Graphql

Si tenemos que escribir una query en este lenguaje, vamos a estar solicitando solo los datos que nos importan, por ej.

```js
query {
	person(personID:1) {
		name
		height
		mass
	}
}
```

La respuesta del servidor será:
```js
{
	"data":{
		"person" {
			"name":"Luke Skywalker",
			"height":172,
			"mass":77
		}
	}
}
```

En el primer código, tenemos nuestra query GraphQL. Solicitamos solo los datos necesarios, DISTINTO a un GET tradicional a una API RESTful.
Debajo tenemos la respuesta en formato JSON, desde el servidor.

>Esto nos da a la idea de que estamos recibiendo solamentre la información que estamos solicitando, y por ende, la respuesta es más rápida.

Suponiendo que ahora nos piden solicitar los datos de las películas donde figura Luke Skywalker, no tenemos que solicitarlas una a una, lo hacemos asi. En principio sabemos de antemano que Luke Skywalker es la persona de ID = 1, por lo tanto, en este caso, vamos a reemplazar justamente con este valor entre paréntesis la persona específica que estamos buscando...

```js
query {
	person(personID:1){
		name 
		height
		mass
		filmConnection {
			films {
				title
			}
		}	
	}
}
```

y esto nos devolvería:

```js
{
	"data":{
		"person":{
			"name":"Luke Skywalker",
			"height":172,
			"mass":77,
			"filmConnection":{
				"films": [
					{
						"title":"A new hope"
					},
					{
						"title":"The Empire strikes back"
					},
					{
						"title":"Return of the Jedi"
					},
					{
						"title":"Revenge of the sith"
					}
				]
			}
		}
	}
}
```
Aqui se puede notar que recibimos solamente los datos que estamos buscando en un solo _request_.

La idea fundamental de **GraphQL** es que el cliente no pide simplemente "el recurso X", sino que **describe exactamente qué datos quiere recibir**.

Se puede pensar GraphQL como una conversación entre cliente y servidor:

> "Dame los datos de este objeto, pero solamente estos campos, y además incluime estos datos relacionados."

## REST vs GraphQL

En REST normalmente tenés endpoints predefinidos:

```
GET /usuarios/15
```

Y el servidor decide qué estructura devuelve:

```
{
  "id": 15,
  "nombre": "Sebastián",
  "email": "sebastian@email.com",
  "telefono": "123456",
  "direccion": "...",
  "fechaNacimiento": "..."
}
```

Aunque solamente necesitaras `nombre` y `email`, el endpoint puede devolverte todo eso.

En GraphQL, en cambio, el cliente puede decir:

```
query {
  usuario(id: 15) {
    nombre
    email
  }
}
```

Y el servidor debería responder:

```
{
  "data": {
    "usuario": {
      "nombre": "Sebastián",
      "email": "sebastian@email.com"
    }
  }
}
```

>[!tip] La diferencia fundamental es:
**REST:** el servidor define principalmente qué estructura recibís.
**GraphQL:** el cliente especifica qué campos necesita.

GraphQL normalmente utiliza **HTTP** como transporte.

Por ejemplo:

```
POST /graphql
Content-Type: application/json
```

El body contiene una consulta:

```
{
  "query": "query { 
	  usuario(id: 15) {
		   nombre email 
		   } 
   }"
}
```

Es decir, hay dos niveles:

```
HTTP
 └── POST /graphql
      └── GraphQL Query
           └── campos solicitados
```

GraphQL en sí mismo no reemplaza HTTP. Es un **lenguaje de consulta + protocolo de ejecución** que suele viajar mediante HTTP.

## Query GraphQL

Una query puede ser muy sencilla:

```
query {
  usuarios {
    nombre
    email
  }
}
```

Acá estamos diciendo:

```
quiero ejecutar una operación de tipo query
    ↓
quiero obtener "usuarios"
    ↓
de cada usuario quiero:
    ↓
    nombre
    email
```

Por ejemplo, el servidor podría devolver:

```
{
  "data": {
    "usuarios": [
      {
        "nombre": "Juan",
        "email": "juan@gmail.com"
      },
      {
        "nombre": "Ana",
        "email": "ana@gmail.com"
      }
    ]
  }
}
```

Observá algo importante:

La estructura del JSON de respuesta **sigue la estructura de la query**.

Si pedís:

```
usuarios {
    nombre
    email
}
```

recibís:

```
usuarios [
    {
        nombre,
        email
    }
]
```


## Como se sabe qué campos existen en la api para solicitar?

Acá aparece uno de los conceptos más importantes de GraphQL: **el schema**.
El servidor tiene definido un esquema parecido a:

```
type Usuario {
    id: ID!
    nombre: String!
    email: String
    telefono: String
}
```

Y probablemente tenga una operación:

```
type Query {
    usuarios: [Usuario]
    usuario(id: ID!): Usuario
}
```

Esto define qué puede pedir el cliente.

Por ejemplo, esto sería válido:

```
query {
    usuario(id: 15) {
        nombre
        email
    }
}
```

Pero esto:

```
query {
    usuario(id: 15) {
        nombre
        edad
        colorFavorito
    }
}
```

fallaría si `edad` y `colorFavorito` no existen en el schema.

Por eso GraphQL es **fuertemente tipado**.

## Resolvers

### ¿Y cómo obtiene los datos el servidor?

Acá aparece otro concepto fundamental: los **resolvers**.

Supongamos que tenemos:

```
type Query {
    usuario(id: ID!): Usuario
}
```

El servidor necesita saber qué código ejecutar cuando alguien pide:

```
usuario(id: 15)
```

Podría tener conceptualmente algo así:

```
usuario: (parent, args) => {
    return database.buscarUsuario(args.id);
}
```

Entonces el flujo sería:

```
CLIENTE
   │
   │ POST /graphql
   │
   │ query {
   │   usuario(id: 15) {
   │      nombre
   │      email
   │   }
   │ }
   ▼
SERVIDOR GRAPHQL
   │
   │ interpreta la query
   ▼
SCHEMA
   │
   │ determina que "usuario" existe
   ▼
RESOLVER
   │
   │ buscarUsuario(15)
   ▼
BASE DE DATOS
   │
   │ resultado
   ▼
RESOLVER
   │
   ▼
GRAPHQL
   │
   │ selecciona solamente:
   │ nombre
   │ email
   ▼
JSON
```

Esta separación es importante:

**GraphQL no necesariamente sabe cómo obtener los datos.**

El resolver puede obtenerlos de:

- MySQL
- PostgreSQL
- MongoDB
- otra API REST
- otro servidor GraphQL
- archivos
- memoria
- cualquier otra fuente

## Las relaciones en GraphQL

Supongamos que tenemos:

```
type Usuario {
    id: ID!
    nombre: String!
    email: String
    pedidos: [Pedido]
}

type Pedido {
    id: ID!
    fecha: String
    total: Float
}
```

Entonces podés pedir:

```
query {
    usuario(id: 15) {
        nombre
        email

        pedidos {
            id
            fecha
            total
        }
    }
}
```

La respuesta podría ser:

```
{
  "data": {
    "usuario": {
      "nombre": "Sebastián",
      "email": "sebastian@gmail.com",
      "pedidos": [
        {
          "id": 100,
          "fecha": "2026-08-01",
          "total": 15000
        },
        {
          "id": 101,
          "fecha": "2026-08-05",
          "total": 8500
        }
      ]
    }
  }
}
```

Acá se ve una de las grandes ventajas de GraphQL.

Podés recorrer el **grafo de relaciones** en una sola query:

```
Usuario
  │
  ├── nombre
  ├── email
  │
  └── pedidos
       │
       ├── id
       ├── fecha
       └── total
```

De ahí viene el nombre **GraphQL**: la información puede modelarse como un grafo de entidades relacionadas.

## Filtrado

También podés pasar argumentos:

```
query {
    usuarios(nombre: "Sebastián") {
        id
        nombre
        email
    }
}
```

El schema podría definir:

```
type Query {
    usuarios(nombre: String): [Usuario]
}
```

El resolver recibiría ese argumento y podría hacer algo equivalente a:

```
SELECT id, nombre, email
FROM usuarios
WHERE nombre = 'Sebastián';
```

Pero ojo con algo importante:

**GraphQL no convierte automáticamente la query en SQL.**

Es el código del servidor el que decide cómo traducir esa solicitud a la fuente de datos.

---

## Variables

Normalmente no conviene escribir valores directamente dentro de la query.

En lugar de:

```
query {
    usuario(id: 15) {
        nombre
        email
    }
}
```

podés hacer:

```
query ObtenerUsuario($id: ID!) {
    usuario(id: $id) {
        nombre
        email
    }
}
```

Y enviar las variables separadamente:

```
{
  "query": "query ObtenerUsuario($id: ID!) { usuario(id: $id) { nombre email } }",
  "variables": {
    "id": 15
  }
}
```

Esto es muy parecido a utilizar **parámetros** en SQL en lugar de concatenar valores.

---

## Tipos de operaciones en GraphQL

GraphQL tiene tres tipos de operaciones:
#### Query
Para consultar:

```
query {
    usuarios {
        id
        nombre
    }
}
```
#### Mutation
Para modificar datos:

```
mutation {
    crearUsuario(nombre: "Juan", email: "juan@gmail.com") {
        id
        nombre
    }
}
```

#### Subscription
Para recibir actualizaciones en tiempo real:

```
subscription {
    nuevoUsuario {
        id
        nombre
    }
}
```

Conceptualmente:

```
QUERY
   ↓
leer

MUTATION
   ↓
crear / modificar / eliminar

SUBSCRIPTION
   ↓
recibir eventos
```


## Una diferencia muy importante con REST

Imaginemos una aplicación de una clínica.
En REST podrías tener:

```
GET /pacientes/15
GET /pacientes/15/turnos
GET /pacientes/15/historia-clinica
GET /pacientes/15/medicos
```

En GraphQL podrías tener un único endpoint:

```
POST /graphql
```

y solicitar:

```
query {
    paciente(id: 15) {
        nombre
        apellido

        turnos {
            fecha
            hora
            medico {
                nombre
                especialidad
            }
        }

        historiaClinica {
            diagnostico
            fecha
        }
    }
}
```

Todo eso puede salir de una única operación GraphQL.

Pero hay una precisión importante: **una sola petición HTTP no significa necesariamente una sola consulta a la base de datos**. Internamente el servidor puede ejecutar varias consultas SQL, llamar diferentes servicios, usar caché, etc.

---

## Esquema de capas

GraphQL se puede entender en cuatro capas:

```
┌─────────────────────────────┐
│         CLIENTE             │
│                             │
│  "Quiero usuario.nombre     │
│   y usuario.email"          │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│       GRAPHQL QUERY         │
│                             │
│ usuario(id: 15) {           │
│     nombre                  │
│     email                   │
│ }                           │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│          SCHEMA             │
│                             │
│ ¿Existe usuario?            │
│ ¿Existe nombre?             │
│ ¿email existe?              │
│ ¿id es válido?              │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│         RESOLVERS           │
│                             │
│ ¿De dónde saco los datos?   │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│      BASE DE DATOS / API    │
└─────────────────────────────┘
```

## Creando una API GraphQL

Para este ejemplo, se me ocurrió poner como datos el universo de Saint Seiya. Muchas veces intentamos consumir datos de API's desde el frontend para probar modelar las respuestas y páginas, y me pareció una idea que va conmigo, me gusta y que aparte tiene muchos datos para representar en caso de ser necesario.

### Definiendo el modelo conceptual

El modelo de los datos es lo primero a tener en cuenta cuando queremos diseñar una api. Estos datos son los que van a estar disponibles para las consultar posteriores, y desarrollo del backend, por lo que tener la estructura es imperativo.

Podríamos tener inicialmente:

```
Caballero
│
├── id
├── nombre
├── signo
├── fechaNacimiento
├── poderes
├── amigos
├── maestros
├── enemigos
└── ...
```

y muchos campos más, pero `amigos` no debería ser simplemente un array de strings.

Por ejemplo:

```
Seiya
  │
  ├── amigo → Shiryu
  ├── amigo → Hyoga
  ├── amigo → Shun
  └── amigo → Ikki
```

Eso significa que **Caballero está relacionado con otros Caballeros**.

Ahí GraphQL encaja muy bien.

### Definiendo el Schema GraphQL

Podríamos empezar con algo así:

```
type Caballero {
    id: ID!
    nombre: String!
    signo: Signo
    fechaNacimiento: String
    poderes: [Poder!]!
    amigos: [Caballero!]!
}

type Poder {
    nombre: String!
    descripcion: String
}

type Signo {
    nombre: String!
    constelacion: String
}

type Query {
    caballeros: [Caballero!]!
    caballero(id: ID!): Caballero
}
```

Esto ya define bastante bien la API.

Tenemos que:

```
Query
 │
 ├── caballeros()
 │
 └── caballero(id)
```

y cada `Caballero` tiene:

```
Caballero
 │
 ├── nombre
 ├── signo
 ├── fechaNacimiento
 ├── poderes
 └── amigos
```

>NOTA IMPORTANTE

#### ¿Qué significa `[Poder!]!`?
Esto es importante porque vas a encontrarte mucho con esta sintaxis.

```
poderes: [Poder!]!
```

Se puede leer:
```
[Poder!]!
   │
   │
   └── la lista no puede ser null
        │
        └── y ningún elemento puede ser null
```

En cambio:
```
poderes: [Poder]
```

permitiría prácticamente cualquier combinación de:
```
null
```

o:
```
[]
```

o:
```
[
  null,
  { "nombre": "Meteoros de Pegaso" }
]
```

Mientras que:
```
[Poder!]!
```

exige una lista existente cuyos elementos también existan.

### Creando los datos

Para aprender GraphQL inicialmente ni siquiera necesitamos definir ni usar una base de datos como normalmente se conoce a MySQL o SQlite, o MongoDB.

Se puede utilizar un array en Node.js:

```
const caballeros = [
    {
        id: "1",
        nombre: "Seiya",
        fechaNacimiento: "01/12",
        signo: {
            nombre: "Sagitario",
            constelacion: "Sagittarius"
        },
        poderes: [
            {
                nombre: "Meteoro de Pegaso",
                descripcion: "Una ráfaga de golpes extremadamente rápidos"
            },
            {
                nombre: "Cometa de Pegaso",
                descripcion: "Una versión más poderosa del ataque"
            }
        ]
    }
];
```

Después agregarías los demás.

Pero hay un detalle interesante con `amigos`.

No necesariamente conviene hacer:

```
amigos: ["Shiryu", "Hyoga", "Shun"]
```

Es mejor manejar relaciones mediante IDs:

```
{
    id: "1",
    nombre: "Seiya",
    amigos: ["2", "3", "4", "5"]
}
```

donde:

```
1 → Seiya
2 → Shiryu
3 → Hyoga
4 → Shun
5 → Ikki
```

Y después GraphQL/resolvers se encargan de transformar esos IDs en objetos `Caballero`.

> Para este último concepto, aparecen en escena los Resolvers

#### Resolvers

El *schema* dice:

```
type Query {
    caballeros: [Caballero!]!
    caballero(id: ID!): Caballero
}
```

Pero el schema **no sabe dónde están los datos**.

Los **resolvers** le dicen cómo obtenerlos.

Conceptualmente:
```
const resolvers = {
    Query: {
        caballeros: () => caballeros,

        caballero: (_, args) => {
            return caballeros.find(c => c.id === args.id);
        }
    }
};
```

Entonces cuando alguien hace:

```
query {
    caballero(id: "1") {
        nombre
    }
}
```

GraphQL ejecuta:

```
Query.caballero(_, { id: "1" })
```

y obtiene el objeto correspondiente.

---

#### Lo interesante es que podés pedir solamente lo que querés

Por ejemplo:
```
query {
    caballero(id: "1") {
        nombre
        fechaNacimiento
    }
}
```

Respuesta:
```
{
    "data": {
        "caballero": {
            "nombre": "Seiya",
            "fechaNacimiento": "01/12"
        }
    }
}
```

Pero podrías pedir:
```
query {
    caballero(id: "1") {
        nombre
        signo {
            nombre
            constelacion
        }
        poderes {
            nombre
            descripcion
        }
    }
}
```

Y recibir:
```
{
    "data": {
        "caballero": {
            "nombre": "Seiya",
            "signo": {
                "nombre": "Sagitario",
                "constelacion": "Sagittarius"
            },
            "poderes": [
                {
                    "nombre": "Meteoro de Pegaso",
                    "descripcion": "..."
                },
                {
                    "nombre": "Cometa de Pegaso",
                    "descripcion": "..."
                }
            ]
        }
    }
}
```

El servidor **no te devuelve automáticamente todos los campos de `Caballero`**.
Devuelve los que seleccionaste.

#### Manejando la relación que existe con la propiedad "amigos"

Podés hacer:
```
query {
    caballero(id: "1") {
        nombre

        amigos {
            nombre
            signo {
                nombre
            }
        }
    }
}
```

Y podrías obtener:
```
{
    "data": {
        "caballero": {
            "nombre": "Seiya",
            "amigos": [
                {
                    "nombre": "Shiryu",
                    "signo": {
                        "nombre": "Libra"
                    }
                },
                {
                    "nombre": "Hyoga",
                    "signo": {
                        "nombre": "Acuario"
                    }
                },
                {
                    "nombre": "Shun",
                    "signo": {
                        "nombre": "Piscis"
                    }
                }
            ]
        }
    }
}
```

Fijate lo que acaba de suceder.

Empezaste en:
```
Seiya
```

y navegaste:
```
Seiya
 ↓
amigos
 ↓
Shiryu
 ↓
signo
 ↓
Libra
```

Eso es justamente la naturaleza de **GraphQL como grafo de datos**.

#### Para esto necesitás un resolver para `amigos`

Podrías tener:

```
const resolvers = {
    Query: {
        caballero: (_, args) => {
            return caballeros.find(c => c.id === args.id);
        }
    },

    Caballero: {
        amigos: (caballero) => {
            return caballero.amigos.map(id =>
                caballeros.find(c => c.id === id)
            );
        }
    }
};
```

Esto es muy importante conceptualmente.
Cuando GraphQL encuentra:

```
amigos {
    nombre
}
```

busca el resolver:
```
Caballero.amigos
```
y ese resolver devuelve los objetos correspondientes.

## Podrías ir bastante más lejos

Por ejemplo, en Saint Seiya podrías separar:

```
Caballero
   │
   ├── Signo
   │
   ├── Armadura
   │
   ├── Poderes
   │
   ├── Amigos
   │
   ├── Maestros
   │
   ├── Enemigos
   │
   └── Participaciones en sagas
```

Y crear tipos:

```
type Caballero {
    id: ID!
    nombre: String!
    fechaNacimiento: String
    signo: Signo
    armadura: Armadura
    poderes: [Poder!]!
    amigos: [Caballero!]!
    enemigos: [Caballero!]!
    maestro: Caballero
    sagas: [Saga!]!
}

type Signo {
    nombre: String!
    constelacion: String!
}

type Armadura {
    nombre: String!
    tipo: TipoArmadura!
}

type Poder {
    nombre: String!
    descripcion: String
}

type Saga {
    id: ID!
    nombre: String!
}
```

Y entonces una query podría ser:

```
query {
    caballero(id: "1") {
        nombre

        signo {
            nombre
            constelacion
        }

        armadura {
            nombre
            tipo
        }

        poderes {
            nombre
        }

        amigos {
            nombre
        }

        enemigos {
            nombre
        }

        sagas {
            nombre
        }
    }
}
```

## Involucrando a Node.js en la ecuación de la API?

Node.js sería el entorno donde ejecutás el servidor GraphQL.

Una arquitectura sencilla sería:

```
                CLIENTE
                   │
                   │ HTTP POST
                   ▼
             ┌────────────┐
             │   Node.js  │
             │            │
             │  GraphQL   │
             └─────┬──────┘
                   │
            ┌──────┴──────┐
            │             │
         Schema        Resolvers
                          │
                          ▼
                    ┌───────────┐
                    │ Datos     │
                    │           │
                    │ JSON      │
                    │ o DB      │
                    └───────────┘
```

Para aprender, yo haría primero:
```
Node.js
   ↓
GraphQL
   ↓
datos en memoria //creados en Node.js directamente o en archivos json para practicar la carga de los mismos.
```

Después:
```
Node.js
   ↓
GraphQL
   ↓
MySQL/PostgreSQL
```

Así podés concentrarte primero en entender **schema + query + resolver**, sin meter todavía SQL, conexiones, ORM, etc.

## Una evolución muy buena para tu proyecto

Yo lo construiría progresivamente así:
### Nivel 1 — datos simples
```
Caballero
├── id
├── nombre
├── fechaNacimiento
└── signo
```

### Nivel 2 — objetos relacionados
```
Caballero
├── Signo
├── Armadura
└── Poderes
```

### Nivel 3 — relaciones entre caballeros
```
Caballero
├── amigos
├── enemigos
├── maestro
└── discípulos
```

### Nivel 4 — filtros
Por ejemplo:
```
caballeros(signo: "Sagitario")
```

o:
```
caballeros(tipoArmadura: "Oro")
```

### Nivel 5 — paginación

```
caballeros(limit: 10, offset: 20)
```

### Nivel 6 — mutations

```
crearCaballero(...)
actualizarCaballero(...)
eliminarCaballero(...)
```

### Nivel 7 — base de datos

Reemplazás:

```
const caballeros = [...]
```

por:

```
GraphQL
   ↓
Resolvers
   ↓
Repository / Service
   ↓
ORM
   ↓
MySQL/PostgreSQL
```

Y ahí ya tendrías un proyecto bastante completo para practicar **Node.js + GraphQL + arquitectura de APIs + base de datos**.

Un detalle adicional: si esto fuera un proyecto público, convendría distinguir entre **datos originales de tu API** y material protegido de la franquicia; para una práctica local/educativa no es lo mismo que publicar una base de datos completa con contenido de la obra.