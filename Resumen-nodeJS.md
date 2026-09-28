
# Roadmap Node.js

Node.js tiene una cantidad considerable de APIs propias: filesystem, streams, eventos, procesos, workers, networking, buffers, CLI, módulos, testing, etc. La documentación oficial actual las separa precisamente en esas áreas.

La idea sería avanzar desde **“cómo ejecuta JavaScript Node” → “cómo interactúa con el sistema operativo” → “cómo maneja concurrencia” → “cómo construir servidores”**.

## Nivel 0 — JavaScript necesario

Antes de meterte profundamente con Node, deberías dominar:

- `let`, `const`
- tipos y coerción [hecho]
- objetos y arrays 
- destructuring
- spread/rest
- funciones
- arrow functions
- closures
- clases
- módulos
- `map`, `filter`, `reduce`, `find`, etc.
- excepciones
- Promises
- `async/await`
- `Promise.all`
- `Promise.allSettled`
- callbacks
- Event Loop a nivel conceptual

Especialmente:

```
async function obtenerDatos() {
    const resultado = await hacerAlgo();
    return resultado;
}
```

y entender **qué significa realmente que esa función sea asíncrona**.

Esto es importante porque gran parte de Node consiste en trabajar con APIs asíncronas.

---

## Nivel 1 — Node.js como runtime

Primero olvidaría Express, NestJS, Fastify, etc.

Aprendería Node "a pelo".

### 1. Ejecutar programas

```
node archivo.js
```

Aprende:

- `node`
- argumentos
- `process`
- código de salida
- variables de entorno
- `process.argv`
- `process.env`
- `process.stdin`
- `process.stdout`
- `process.stderr`

Por ejemplo:

```
console.log(process.argv);
console.log(process.env.NODE_ENV);
```

Esto te permite empezar a hacer **programas de consola reales**.

---

## Nivel 2 — Sistema de módulos

Aquí tienes dos sistemas que debes conocer:

### CommonJS

```
const fs = require("node:fs");
module.exports = algo;
```

### ES Modules

```
import fs from "node:fs";
export default algo;
```

Node soporta ambos sistemas.

Aprende:

- `require`
- `module.exports`
- `exports`
- `import`
- `export`
- `package.json`
- `"type": "module"`
- `.mjs`
- `.cjs`
- resolución de módulos
- módulos internos de Node con `node:`

Por ejemplo, actualmente es muy habitual ver:

```
import fs from "node:fs/promises";
```

en lugar de paquetes externos.

---

## Nivel 3 — `package.json` y npm

Esto es fundamental.

Aprende:

- `npm init`
- `npm install`
- `npm uninstall`
- `dependencies`
- `devDependencies`
- `package-lock.json`
- scripts
- versiones
- semver
- paquetes locales
- paquetes globales
- `node_modules`
- publicación de paquetes

Por ejemplo:

```
{
    "scripts": {
        "start": "node src/index.js",
        "test": "node --test"
    }
}
```

También entendería qué diferencia hay entre:

```
npm install
```

```
npm install paquete
```

```
npm install -D paquete
```

La documentación de npm considera precisamente `package.json`, dependencias, módulos y semantic versioning como conceptos centrales.

---

## Nivel 4 — Filesystem

Este sería uno de los bloques **más importantes para lo que tú estás buscando**.

Aprende:

### `fs`

- crear archivos
- leer archivos
- modificar archivos
- eliminar archivos
- renombrar
- copiar
- comprobar existencia
- permisos
- directorios

Primero:

```
import fs from "node:fs/promises";
```

Y luego:

```
await fs.readFile(...)
await fs.writeFile(...)
await fs.appendFile(...)
await fs.mkdir(...)
await fs.readdir(...)
await fs.rename(...)
await fs.unlink(...)
```

Después aprende:

```
fs.stat()
```

y:

```
fs.access()
```

### Después: `path`

Esto es importantísimo:

```
import path from "node:path";
```

Aprende:

```
path.join()
path.resolve()
path.basename()
path.dirname()
path.extname()
path.parse()
```

Por ejemplo:

```
const ruta = path.join(
    process.cwd(),
    "data",
    "usuarios.json"
);
```

---

## Nivel 5 — Buffers

Aquí empiezas a entender algo muy importante:

> Node no trabaja únicamente con strings y objetos JavaScript.

Aprende:

```
Buffer
```

Por ejemplo:

```
const buffer = Buffer.from("Hola");

console.log(buffer);
```

Y:

```
buffer.toString();
```

También:

- encoding
- UTF-8
- hexadecimal
- bytes
- `ArrayBuffer`
- `Uint8Array`

Esto después te ayuda muchísimo para entender:

- archivos
- streams
- sockets
- TCP
- imágenes
- protocolos
- criptografía

---

## Nivel 6 — Streams

Este es un punto que muchos cursos de Node prácticamente ignoran.

Y es un error.

Aprende:

- `Readable`
- `Writable`
- `Duplex`
- `Transform`
- `pipe`
- backpressure

Por ejemplo, no es lo mismo:

```
const archivo = await fs.readFile("archivoGigante.txt");
```

que leerlo mediante un stream.

Para un archivo de 10 MB probablemente no importa demasiado.

Pero imagina:

```
archivo de 20 GB
```

No quieres necesariamente cargar todo en RAM.

Ahí aparece:

```
createReadStream()
```

y:

```
createWriteStream()
```

Los streams son una de las piezas centrales del modelo de I/O de Node.

---

## Nivel 7 — Eventos

Aprendería:

```
EventEmitter
```

Ejemplo conceptual:

```
import EventEmitter from "node:events";

const eventos = new EventEmitter();

eventos.on("usuarioCreado", usuario => {
    console.log(usuario);
});

eventos.emit("usuarioCreado", {
    nombre: "Seiya"
});
```

Aquí empiezas a entender mejor el estilo de programación orientado a eventos de Node.

Y posteriormente vas a encontrarte esto constantemente:

```
process.on(...)
socket.on(...)
stream.on(...)
server.on(...)
```

---

## Nivel 8 — Event Loop y concurrencia

Este debería ser un bloque importante de estudio.

No simplemente:

> "Node es single-threaded."

Eso es demasiado simplificado.

Tienes que entender:

```
JavaScript thread
       │
       ▼
   Event Loop
       │
       ├── timers
       ├── I/O
       ├── callbacks
       ├── microtasks
       └── ...
```

Y distinguir:

### I/O-bound

Por ejemplo:

```
leer archivo
consultar DB
hacer HTTP request
esperar socket
```

### CPU-bound

Por ejemplo:

```
calcular SHA-512 millones de veces
procesar una imagen
comprimir enormes cantidades de datos
calcular una simulación
```

Esto es fundamental porque **no solucionas ambos problemas de la misma manera**.

---

## Nivel 9 — HTTP sin Express

Ahora sí.

Antes de tocar Express, crea un servidor usando:

```
node:http
```

Por ejemplo:

```
import http from "node:http";

const server = http.createServer((req, res) => {

    res.writeHead(200, {
        "Content-Type": "application/json"
    });

    res.end(JSON.stringify({
        mensaje: "Hola"
    }));
});

server.listen(3000);
```

Aprende:

- request
- response
- headers
- status codes
- métodos HTTP
- URL
- query parameters
- body
- cookies
- streams HTTP
- keep-alive

Después podrás entender mucho mejor qué está haciendo Express realmente.

---

## Nivel 10 — Networking

Aquí ya puedes meterte más abajo.

Aprende:

```
HTTP
HTTPS
TCP
UDP
DNS
Sockets
```

Node tiene APIs para:

- `node:net`
- `node:dgram`
- `node:dns`
- `node:http`
- `node:https`

Esto es especialmente interesante si quieres comprender Node más allá de "hacer APIs".

---

## Nivel 11 — Child Processes

Este es otro bloque que te recomiendo mucho.

Aprende:

```
child_process
```

y especialmente:

```
spawn()
exec()
execFile()
fork()
```

Por ejemplo:

```
spawn("ping", ["google.com"]);
```

Esto permite que Node lance procesos del sistema operativo.

La diferencia entre `spawn`, `exec`, `execFile` y `fork` es importante; además, las versiones síncronas pueden bloquear el Event Loop.

Aquí puedes construir programas interesantes:

```
Node
 │
 ├── ejecuta Python
 ├── ejecuta un programa C#
 ├── ejecuta comandos del SO
 ├── ejecuta otro Node
 └── recibe resultados
```

---

## Nivel 12 — Worker Threads

Ahora sí entraría en lo que mencionaste específicamente como **multiworkers**.

Aprende:

```
node:worker_threads
```

Conceptualmente:

```
              Node process
                   │
        ┌──────────┴──────────┐
        │                     │
   Main Thread            Worker
        │                     │
   Event Loop             JS execution
```

Los Worker Threads permiten ejecutar JavaScript en paralelo y están pensados especialmente para trabajo intensivo de CPU; para I/O normalmente las APIs asíncronas de Node son preferibles.

Aprende:

- `Worker`
- `workerData`
- `parentPort`
- `postMessage`
- mensajes
- terminación
- errores
- pools de workers
- `SharedArrayBuffer`
- `Atomics`

Y algo muy importante:

> **Worker Threads ≠ procesos.**

Un worker es un thread dentro del proceso de Node.

---

## Nivel 13 — Multiproceso

Después de Worker Threads:

```
worker_threads
       ↓
child_process
       ↓
cluster
```

Aquí estudias otra arquitectura:

```
             Master / Primary
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      Node        Node        Node
     process     process     process
```

Esto te ayuda a entender:

- múltiples procesos
- IPC
- balanceo
- aislamiento
- procesos independientes
- escalabilidad

No necesariamente necesitas `cluster` para trabajar profesionalmente, pero **sí vale la pena conocerlo conceptualmente**.

---

## Nivel 14 — CLI

Node también es excelente para crear herramientas de consola.

Aprende:

```
process.argv
process.stdin
process.stdout
readline
```

Puedes llegar a crear:

```
mi-programa crear usuario
mi-programa listar usuarios
mi-programa eliminar usuario 42
```

Y aquí conectarás muchos conceptos anteriores:

```
CLI
 │
 ├── argumentos
 ├── filesystem
 ├── JSON
 ├── streams
 ├── eventos
 └── procesos
```

Esto encaja bastante con las cosas que ya has hecho con `readline` y `process.stdin`.

---

## Nivel 15 — Testing

No dejaría testing para el final absoluto.

Node actualmente tiene su propio:

```
node:test
```

y:

```
node:assert
```

Aprende:

- unit tests
- assertions
- hooks
- mocks
- tests asíncronos
- coverage
- integración

Node incluye actualmente un Test Runner propio en sus APIs oficiales.

Después puedes aprender Jest/Vitest, pero primero entendería el concepto con las herramientas nativas.

---

## Nivel 16 — Debugging

Aprende:

```
console
debugger
Node Inspector
Chrome DevTools
VS Code debugger
```

Especialmente:

```
debugger;
```

y ejecutar Node con las opciones de inspección.

También:

- stack traces
- memory usage
- CPU profiling
- heap snapshots
- performance

---

## Nivel 17 — Seguridad y configuración

Después:

- `process.env`
- configuración por ambiente
- secrets
- permisos
- `crypto`
- hashes
- HMAC
- encryption
- TLS
- certificados
- validación de entrada
- sanitización
- errores

Node también dispone de APIs propias para Crypto, TLS y Permissions.

---

## Nivel 18 — Bases de datos

Recién aquí empezaría a meter:

```
Node
 ↓
SQL
 ↓
MySQL / PostgreSQL / SQLite
```

y después:

```
ORM
 ↓
Prisma / TypeORM / Sequelize
```

Primero aprendería a hablar directamente con una base de datos.

Porque si empiezas directamente con ORM puedes terminar sin entender qué ocurre debajo.

---

## Nivel 19 — Frameworks

Ahora sí:

### Backend HTTP

- Express
- Fastify

### Frameworks más completos

- NestJS

### APIs

- REST
- GraphQL
- WebSockets

Y aquí tu conocimiento anterior de GraphQL te va a resultar mucho más fácil de encajar.

---

## Nivel 20 — Arquitectura

Finalmente:

```
Node.js
   │
   ├── HTTP
   ├── DB
   ├── filesystem
   ├── workers
   ├── processes
   ├── streams
   └── networking
```

y empezar:

- arquitectura por capas
- Repository
- Service
- Controller
- Dependency Injection
- eventos
- colas
- caching
- logging
- configuración
- graceful shutdown
- health checks
- observabilidad

---

## Nivel 21 - CACHE BASICO

Para implementar un caché en una **API REST en Node.js**, la forma más eficiente y común es utilizar **Redis**, una base de datos en memoria rápida.

Pasos básicos con Redis y Express

1. **Instalar dependencias**:
```bash
npm install express redis axios
```

2. **Crear el cliente de Redis y el servidor**:  
    Puedes seguir una guía detallada en [Caché en las API de NodeJS](https://cursa.app/es/pagina/cache-en-las-api-de-nodejs). Aquí tienes un ejemplo simple de un middleware o ruta con caché:

```js
    const express = require('express');
    const { createClient } = require('redis');
    const axios = require('axios');
    
    const app = express();
    const client = createClient({ url: 'redis://127.0.0.1:6379' });
    
    client.connect().catch(console.error);
    
    app.get('/api/recurso', async (req, res) => {
      const cacheKey = 'recurso_data';
    
      try {
        // 1. Verificar si existe en el caché
        const cachedData = await client.get(cacheKey);
        if (cachedData) {
          return res.json({
            source: 'cache',
            data: JSON.parse(cachedData)
          });
        }
    
        // 2. Si no está en caché, buscar en la fuente original o base de datos
        const response = await axios.get('https://ejemplo.com');
        const freshData = response.data;
    
        // 3. Guardar en Redis con un tiempo de vida (TTL) de 60 segundos
        await client.setEx(cacheKey, 60, JSON.stringify(freshData));
    
        return res.json({
          source: 'api',
          data: freshData
        });
      } catch (error) {
        res.status(500).json({ error: error.message });
      }
    });
    
    app.listen(3000, () => console.log('Servidor en puerto 3000'));
```

En el siguiente vídeo de FAZT CODE se muestra de manera práctica cómo opera un sistema de caché con Redis en Node.js:

![](data:image/png;base64,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)
[video de cache en server nodejs](https://www.youtube.com/watch?v=TazYA-wqOkY)

### ¿Cómo funciona exactamente?

Cuando un usuario hace una solicitud a tu API REST (por ejemplo, pedir la lista de productos), el flujo es el siguiente:

1. **Primera solicitud:** Tu API recibe la orden, va a la base de datos principal (que puede ser lenta), procesa los datos, **guarda una copia en el caché** y se los envía al usuario.    
2. **Siguientes solicitudes:** Cuando otro usuario (o el mismo) pide lo mismo, tu API ya no va a la base de datos principal. **Toma la copia directamente del caché** y la entrega de inmediato.

### Diferencias entre una Base de Datos y un Caché

Aunque el caché (como **Redis**) técnicamente guarda datos, su propósito y arquitectura son muy diferentes a los de una base de datos tradicional (como _PostgreSQL, MySQL o MongoDB_):

| Característica              | Base de Datos Principal (PostgreSQL, MongoDB)         | Sistema de Caché (Redis, Node-Cache)                                             |
| --------------------------- | ----------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Ubicación de datos**      | Se guardan en el **disco duro** (permanente).         | Se guardan en la **memoria RAM** (volátil y ultra rápida).                       |
| **Tiempo de vida**          | Los datos viven para siempre hasta que los borres.    | Los datos tienen un **TTL (Time-To-Live)** y se borran solos en minutos u horas. |
| **Propósito**               | Ser la fuente de verdad única y segura de tu negocio. | Aliviar la carga de la base de datos y acelerar las respuestas.                  |
| **Si el servidor se apaga** | Los datos están seguros en el disco.                  | Los datos en RAM se pierden (pero no importa, porque se vuelven a generar).      |

---

**Analogía con respecto a un restaurante**
Imagina que eres un cocinero en un restaurante:

- **La Base de Datos** es la despensa trasera. Ir a buscar los ingredientes, picarlos y cocinarlos toma **15 minutos** (Solicitud pesada).
- **El Caché** es un plato que ya preparaste y dejaste en el mostrador listo para servir. Si un cliente pide exactamente eso, se lo entregas en **5 segundos**.

Pasadas un par de horas, si nadie lo compra, tiras ese plato porque ya no está fresco (eso es el **TTL** o tiempo de expiración) y preparas uno nuevo cuando vuelva a entrar un pedido.

### Usando node-cache

Para implementar un caché directamente en la memoria de tu aplicación sin necesidad de instalar bases de datos externas como Redis, la librería

**`node-cache`** es la opción ideal.

**`node-cache` guarda los datos en la memoria RAM de tu propio servidor Node.js**, por lo que es extremadamente rápido y fácil de configurar.

**Pasos para implementar `node-cache`**

1. **Instala la librería** en tu proyecto:
 
```bash
npm install node-cache express
```

2. **Crea el servidor con el caché**:  
    Aquí tienes un ejemplo práctico y limpio. Configuraremos un caché global con un **TTL (tiempo de vida) por defecto de 15 segundos**, pero verás que puedes personalizarlo por cada ruta.

```js
const express = require('express');
const NodeCache = require('node-cache');

const app = express();

// stdTTL: Tiempo de vida por defecto en segundos (15 segundos)
// checkperiod: Cada cuánto tiempo el caché busca y borra datos expirados
const myCache = new NodeCache({ stdTTL: 15, checkperiod: 120 });

// Ruta que simula una consulta pesada a una base de datos
app.get('/api/productos', (req, res) => {
  const cacheKey = 'lista_productos';

  // 1. Intentar obtener los datos del caché
  const cachedData = myCache.get(cacheKey);

  if (cachedData) {
    // Si existen, los devolvemos inmediatamente
    return res.json({
      source: 'cache-local',
      data: cachedData
    });
  }

  // 2. Si no están en caché, simulamos una consulta tardía (ej. a MongoDB o PostgreSQL)
  setTimeout(() => {
    const productosFicticios = [
      { id: 1, nombre: 'Laptop Gamer', precio: 1200 },
      { id: 2, nombre: 'Teclado Mecánico', precio: 80 },
      { id: 3, nombre: 'Ratón Óptico', precio: 45 }
    ];

    // 3. Guardar el resultado en el caché para las siguientes peticiones
    // (Opcional) Puedes pasar un tercer parámetro para cambiar el TTL de esta clave específica: myCache.set(key, val, 60)
    myCache.set(cacheKey, productosFicticios);

    return res.json({
      source: 'base-de-datos',
      data: productosFicticios
    });
  }, 2000); // Simula un retraso de 2 segundos
});

// Ruta para vaciar el caché manualmente (útil si agregas un nuevo producto)
app.post('/api/productos/limpiar-cache', (req, res) => {
  myCache.del('lista_productos'); // Borra una clave específica
  
  // myCache.flushAll(); // Borra ABSOLUTAMENTE TODO el caché
  res.json({ mensaje: 'Caché de productos limpiado correctamente' });
});

app.listen(3000, () => {
  console.log('Servidor corriendo en http://localhost:3000');
});
```

### Limitaciones importantes de `node-cache`

Aunque es excelente por su simplicidad, debes tener en cuenta dos cosas antes de usarlo en producción:

- **Si reinicias el servidor, el caché se borra:** Como vive en la RAM del proceso de Node.js, cualquier reinicio o caída del script vaciará el caché (volverá a cargarse con la primera consulta de los usuarios).
- **No escala horizontalmente:** Si en el futuro clonas tu API en 3 servidores diferentes usando un **balanceador de carga**, cada servidor tendrá su propio caché independiente. Si el Servidor A guarda algo en caché, el Servidor B no lo sabrá. (Para resolver esto es que se usa **Redis**).

### Manejando cache con parámetros de busqueda

Para manejar parámetros en la URL (como `/api/productos?categoria=electronica&orden=precio`), el truco consiste en ==**generar una clave de caché única combinando la ruta con los parámetros de la consulta (**==**`req.query`)**.

Si no haces esto y usas una clave fija como `'lista_productos'`, el primer usuario que busque "**electronica**" guardará sus datos, y cuando un segundo usuario busque "**ropa**", el sistema le devolverá erróneamente los productos de electrónica guardados en el caché.

Aquí tienes cómo implementarlo de forma elegante usando `node-cache`:

**Código de ejemplo con parámetros dinámicos**

```js
const express = require('express');
const NodeCache = require('node-cache');

const app = express();
const myCache = new NodeCache({ stdTTL: 30 }); // 30 segundos de vida por defecto

app.get('/api/productos', (req, res) => {
  // 1. Convertir los parámetros de la URL en un texto único
  // req.query contiene un objeto como { categoria: 'electronica', pagina: '1' }
  const queryParamsString = JSON.stringify(req.query);
  
  // Creamos la clave combinando la ruta base y los parámetros ordenados
  // Ejemplo de resultado: "productos-{"categoria":"electronica"}"
  const cacheKey = `productos-${queryParamsString}`;

  // 2. Intentar buscar esa combinación exacta en el caché
  const cachedData = myCache.get(cacheKey);

  if (cachedData) {
    return res.json({
      source: 'cache-local',
      key_used: cacheKey,
      data: cachedData
    });
  }

  // 3. Si no está en caché, simulamos la búsqueda real usando los parámetros
  setTimeout(() => {
    const categoriaBuscada = req.query.categoria || 'todos';
    
    const respuestaBaseDatos = {
      categoria: categoriaBuscada,
      total: 1,
      items: [{ id: 101, nombre: `Artículo de ${categoriaBuscada}`, precio: 299 }]
    };

    // 4. Guardamos en el caché usando la clave única generada arriba
    myCache.set(cacheKey, respuestaBaseDatos);

    return res.json({
      source: 'base-de-datos',
      key_used: cacheKey,
      data: respuestaBaseDatos
    });
  }, 1500);
});

app.listen(3000, () => console.log('Servidor en puerto 3000'));
```

>[!warning] Importante
>El método anterior usando `JSON.stringify(req.query)` funciona perfecto el 95% de las veces. Sin embargo, tiene un pequeño fallo: si un usuario entra a `/api/productos?categoria=electronica&orden=precio` y otro entra a `/api/productos?orden=precio&categoria=electronica`, los objetos tendrán las propiedades en diferente orden. JavaScript los leerá como textos distintos y creará **dos cachés para la misma consulta**.

Si quieres evitar esto en un entorno de producción real, puedes **ordenar los parámetros alfabéticamente** antes de crear la clave. Se hace de manera muy sencilla reemplazando la línea de la clave por esto:

```js
// Ordena los parámetros alfabéticamente para que el orden de la URL no rompa el caché
const sortedQuery = Object.keys(req.query)
  .sort()
  .reduce((acc, key) => {
    acc[key] = req.query[key];
    return acc;
  }, {});

const cacheKey = `productos-${JSON.stringify(sortedQuery)}`;
```

Esto constituye ya un sistema robusto para implementar cache y flitrar búsquedas.

---

## Cómo lo ordenaría para ti

Teniendo en cuenta que ya has trabajado con JavaScript, `readline`, `process.stdin`, `fetch`, REST, GraphQL, cookies, etc., **no te haría empezar desde JavaScript básico**.

Yo haría este recorrido:

```
                    NODE.JS
                       │
          ┌────────────┴────────────┐
          │                         │
      FUNDAMENTOS               SISTEMA
          │                         │
     modules/npm               filesystem
     process                   path
     events                    buffers
     promises                  streams
     async/await               readline
          │                         │
          └────────────┬────────────┘
                       │
                  CONCURRENCIA
                       │
              ┌────────┼────────┐
              │        │        │
          Event Loop  Workers  Processes
                       │        │
                worker_threads child_process
                                cluster
                       │
                       ▼
                  NETWORKING
                       │
                 HTTP / TCP
                       │
                       ▼
                   SERVERS
                       │
              http → Express
                       │
                       ▼
                  DATABASES
                       │
                       ▼
                 ARQUITECTURA
```

## Y hay 8 temas que yo consideraría "imprescindibles"

Si tu objetivo es realmente **saber Node.js**, y no solamente poder poner en tu CV "Node.js", priorizaría:

1. **Event Loop + asincronía**
2. **Filesystem**
3. **Streams**
4. **Buffers**
5. **Events / EventEmitter**
6. **Child Processes**
7. **Worker Threads**
8. **HTTP / Networking**

Y después:

9. Testing
10. Debugging/performance
11. Databases
12. Express/Fastify/NestJS
13. Arquitectura

La documentación oficial actual de Node incluso agrupa explícitamente filesystem, child processes, cluster, events, HTTP, streams, worker threads, test runner, readline, OS, net, etc., lo que da una muy buena idea de que **Node es bastante más grande que "un runtime para hacer servidores".**

### Un detalle especialmente importante

No estudiaría **Worker Threads antes de entender Event Loop, Promises, streams y procesos**.

Porque si no, es muy fácil terminar pensando:

> "Node es single-threaded → necesito workers para hacer varias cosas."

La idea correcta es más cercana a:

```
             ¿Qué tipo de trabajo tengo?
                       │
            ┌──────────┴──────────┐
            │                     │
           I/O                   CPU
            │                     │
     async Node APIs        Worker Threads
            │                     │
            ▼                     ▼
      Event Loop             paralelismo
```

Y si necesitas aislamiento de procesos o ejecutar programas externos:

```
Node
 │
 └── child_process
        │
        ├── spawn
        ├── exec
        ├── execFile
        └── fork
```

Eso es una distinción arquitectónica mucho más importante que simplemente memorizar APIs.

Como referencia principal, te conviene tener a mano la [documentación oficial de Node.js](https://nodejs.org/api/?utm_source=chatgpt.com) y utilizarla como índice de estudio, no solamente como manual de consulta

# Instalando NodeJS y creando el primer hola mundo!.

## Forma tradicional de instalar una única versión de nodejs en la pc.

Para instalar NodeJS, nos dirigimos a la página oficial
[http://nodejs](https://nodejs.org/en) y vamos a la sección _DOWNLOADS_ y luego _Prebuilt installer_
Vamos a buscar la versión correspondiente al hardware que estemos corriendo y elegir la versión (LTS) long term support. que son las versiones a las que más soporte le dan sin implementar cambios muy significativos.


>[!important] La manera recomendada, es utilizar ciertas apps, para poder manejar las distintas versiones que podemos instalar, y correr los programas dependiendo de cada version que querramos utilizar.

Para esto, necesitamos de 3 aplicaciones requerídas. Windows Terminal (WSL), RUST, y Fast Node Manager (fnm).
fast node manager (https://github.com/Schniz/fnm)

- Para instalar Windows Terminal(que no es cdm, ni windows powershell), podemos instalarlo desde la página oficial de microsoft con una simple busqueda.
- Para instalar RUST, vamos a https://www.rust-lang.org/learn/get-started, y copiamos el código que brinda la página en nuestra Terminal.
- Puede ser que tengamos que instalar Unos archivos de VISUAL STUDIO INSTALLER, pero el mismo instalador de RUST nos da la opción de hacerlo.
- Finalmente, luego de instalado RUST y los derivados de Visual Studio, abrimos la terminal Bash por ej. de GIT, y colocamos el código indicado en la página de fnm.
- esto finalmente indicará que se instaló fnm, para verificarlo, cerrar y reabrir la terminal.
- al finalizar, podemos poner

`fnm --version`

  y esto debería resultar en la versión instalada de fnm.

  comandos:

   - _fnm list_: devuelve la lista de versiones de node js instaladas.
   - _fnm install (version de node a instalar)_ : esto instala la versiòn que existe en la página oficial de node.
   - _fnm use (version de node a usar)_ : esto determina qué versión ejecutará el código indicado.
   - _fnm alias (versión de node a referenciar) default_ : esto hace que la versión indicada de node quede "por defecto" a utilizar cada vez que iniciemos un código, evitando que se usen otras versiones ya instaladas automáticamente.
   - _fnm --HELP_ : muestra los distintos comandos que fnm puede tener.
 
---

>[!warning]  Hay entornos de Windows que pueden no estar configurados para ciertas acciones de los lenguajes o códigos.

*1 Aqui veremos cómo resolver el caso en que FNM se instale, puedas descargar los paquetes de nodejs, pero aún asi, al ejecutar >node en la terminal, no reconozca el comando.
Normalmente para esto hay que correr una linea de código al abrir la terminal, para que se reconozca el path de la instalación de node, pero si la terminal tiene desactivada la ejecución de **scripts** , esto generará que cada vez de abrir la terminal, deberás correr esa linea de código :

`fnm env --use-on-cd | Out-String | Invoke-Expression`

Para evitar esto, y que al abrir la terminal en cualquier lugar (ej. Visual studio code) no tengamos que realizar esto manualmente, se utilizan los perfiles de powershell por ej.
Hay que crear uno, si la terminal activa no tiene uno habilitado, y agregar esa linea de código al final del perfil(si el perfil es nuevo, no va a tener nada excepto esa linea de código)

Según la página _https://learn.microsoft.com/es-es/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7.4#the-profile-variable_

Para crear un perfil del usuario actual de power shell:
```
  if (!(Test-Path -Path $PROFILE)) {
  New-Item -ItemType File -Path $PROFILE -Force
  }
```

Para verificar si se creó correctamente y editarlo, podemos poner en la misma terminal lo siguiente:

`notepad $profile`

Esto abrirá el achivo profile en el bloc de notas para agregar la linea de código indicada en *1

Al guardar el archivo, si cerramos y abrimos de nuevo la terminal, podremos leer si tiene una restricción para ejecutar scripts en la terminal. De ser asi, en la misma terminal podemos cambiar esto de la siguiente manera.

ejecutamos:

`Get-ExecutionPolicy`

Si esto devuelve "_Restricted_" quiere decir que está prohibido ejecutar scripts desde la consola directamente. Ahí debemos cambiar con lo siguiente:

`Set-ExecutionPolicy Unrestricted`

y luego de que tome los cambios, reiniciar la terminal. Al abrirla nuevamente, debería haberse ido el mensaje y podremos ejecutar directamente "node" en la terminal, y esto abrira el REPL (read eval print loop).
A esta altura ya debería funcionar node en cualquier terminal, incluida la de Visual Studio Code, y ejecutar cualquier programa en la versión de NodeJs elegida.

Finalmente, el archivo `$profile` que se crea en powershell para cargar cada vez que se ejecuta el powershell, deberá tener las siguientes lineas al menos para que fnm funcione debidamente.

`oh-my-posh init pwsh --config 'C:\Users\David\AppData\Local\Programs\oh-my-posh\themes\rudolfs-light.omp.json' | Invoke-Expression
Import-Module -Name Terminal-Icons
fnm env --use-on-cd --shell power-shell | Out-String | Invoke-Expression
[System.Environment]::SetEnvironmentVariable("Path", ("$HOME\AppData\Roaming\fnm\aliases\default;" + [System.Environment]::GetEnvironmentVariable("Path", "User")), "User")`

la primer linea se encarga de cargar oh-my-posh si lo tienes instalado, para dejar más personalizada la interfaz de la cli.
la segunda, carga los íconos de la terminal.
la tercera genera que se carge las variables correctas de entorno de fnm
la cuarta justamente carga correctamente la versión default activa de NodeJS, en las variables de entorno. sino muchas cosas no funcionan.

---

---

Luego de esto, podemos iniciar un proyecto, creando la carpeta, un archivos por ej: server.js e iniciar el proyecto, ingresando en la consola

      npm init

  esto inicia el creado del archivo package.json, que guardará información sobre nuestro proyecto, dependencias, y demás info.
Iinicialment el archivo se ve así:

```json
   {
   "name": "proyecto-nodejs",
   "version": "0.0.1",
   "description": "primer proyecto orientado a practicar nodejs",
   "main": "src/server.js",
   "scripts": {
   "start": "node src/server.js",
   "dev": "nodemon src/server.js",
   "console": "echo 'hola mundo desde scripts'"
   },
   "author": "David Giordano",
   "license": "ISC",
   "devDependencies": {
   "nodemon": "^3.1.3"
   }
   }
```
la mayoría de campos se explican solos, pero los de scripts, son campos que pretenden determinar qué se ejecuta al escribir en la consola por ej:

    npm run dev

esto iniciará en la terminal la linea de código escrita en esa propiedad del objeto, o sea 
`src/server.js  // esto inicia nuestro codigo de servidor en server.js`


el comando:

` npm start`

automáticamente inicia nuestra ruta descripta, normalmente se usa para iniciar el codigo, para pruebas, demostración, etc.


      npm run
> Este comando te muestra en consola, todos los "runs" configurados en el package.json, los cuales se pueden usar para iniciar de distintas maneras nuestro proyecto.



### Instalando dependencias

  Las dependencias son módulos de código, que nos permiten realizar distintas cosas ya escritas en javascript, para acelerar el proceso y no tener que crear todo desde 0.

  ejemplos;
    - nodemon : esta dependencia nos permite ejecutar un tipo de "live server" para archivos nodejs. La terminal se actualiza cada vez que se guarda un cambio, evitando tener que pararla y ejecutarla manualmente cada vez que hacemos un cambio.
    - express : esta dependencia se utiliza para el manejo de páginas web.

### Pagina NPM para buscar e instalar modulos.

https://www.npmjs.com/package/express

### Instalacion en detalle de módulos externos

  De forma local

  La mayoría de las dependencias (express, request, etc) se instalan localmente.

> $ npm install [nombre_del_modulo]
> $ npm i [nombre_del_modulo]

  De forma global

  Se utiliza en su mayoría para instalar herramientas de la linea de comandos (mocha, browserify, gulp, etc).

>[!info] 
> $ npm install --global [nombre_del_modulo]
 >$ npm i -g [nombre_del_modulo]


#### Instalar una versión específica de un módulo de nodejs

>[!info] $ npm install nombre_del_paquete@3.3.0

#### Instalar la última versión de un módulo.

>[!info] $ npm install nombre_del_paquete@latest

#### Instalar un módulo como dependencia 

   Si se desea guardar la referencia a los módulos dentro de package.json.

>[!info] $ npm i --save nombre_del_paquete

o su forma corta…

>[!info] $ npm i -S nombre_del_paquete

#### Instalar módulo como dependencia de desarrollo.

   Si se desea instalar una dependencia o devDependency.

>[!info] $ npm i --save-dev nombre_del_paquete

o su forma corta…

>[!info] $ npm i -D nombre_del_paquete



>[!warning] Por default, npm agregará ^ cuando se utilice --save. El símbolo ^ es peligroso ya que mantiene actualizada la instalación con la última versión disponible de la librería. Por ello es echar mano de una versión exacta. 

#### Instalar una versión exacta del módulo.

Esto evita que el módulo instalado se actualice automáticamente.

> $ npm i --exact nombre_del_modulo

o su forma corta…

> $ npm i -E nombre_del_modulo

#### Instalar un módulo de forma global 

> $ npm i --global nombre_del_modulo

o su forma corta…

> $ npm i -g nombre_del_modulo


#### Si se desea mostrar la lista de dependencias.

> $ npm ls -g

#### Desinstalar un módulo de node

> $ npm rm nombre_del_modulo

¿Cómo desinstalar un módulo global de NPM?

> $ npm rm -g nombre_del_modulo

---

### Semantyc Versioning 

Este esquema significa que cada versión del módulo tiene tres dígitos separados por punto, como por ejemplo 6.0.0, 4.3.6, 5.2.1, etc.

Cada dígito indica cómo son los cambios de las nuevas versiones y funciona así. Si el último dígito cambia, significa que los cambios son menores, normalmente se arreglan bugs, brechas de seguridad y problemas de rendimiento. Actualizar a esta versión significa que nuestra app seguirá funcionando, y que de hecho lo hará mejor.

Cuando la versión modifica el dígito de en medio, sabemos que los cambios fueron menores, es decir, que se agregó funcionalidad nueva al framework, que aunque es nueva, es compatible con la versión anterior del framework. Actualizar a esta versión significa que tenemos nuevas funcionalidades disponibles, pero que tu código debería seguir funcionando.

Por último, actualizaciones al primer dígito significa que se agregó nueva funcionalidad, que se pudieron haber eliminado otras características y que el código que se actualice a esta versión podría no ser compatible y requerir de modificaciones sobre el código para que funcione con la nueva versión.

El _caret_ ^ al frente de cada versión de los módulos, indica que ese módulo se actualizará cada vez que se lance una nueva versión. En caso de no querer esto, que será la mayoría de veces, se borra el caret y esto evitará la posibilidad de actualizar el módulo automáticamente.

>[!warning] TENER EN CUENTA ESTO AL MOMENTO DE USAR MODULOS Y MANEJAR EL PACKAGE.JSON


---


## Process.env (importante)
* Este elemento en nodejs, permite ver mucha información sobre el proceso que se ejecuta al iniciar cualquier aplicación en nodejs.
  Normalmente se definen las variables de entorno en este proceso, dado que son datos sensibles, que se pueden utilizar de manera "oculta" para no dejar estos datos en el mismo programa (datos de acceso de la base de datos, palabras clave, etc)

  `console.log(process.argv)` esto devuelve en un array, todos los argumentos utilizados para ejecutar la aplicación donde se está corriendo la app.

  ej:
  `node app7.js Ernesto rojo abh51342 focusin`
  devolverá el array:
  `["path a la app node instalada", "path al archivo app7.js", "Ernesto", "rojo", "abh51342", "focusin"]`


  `Process.exit(0 ó 1)`
  esto nos permite terminar el proceso ejecutado, donde 0 indicaría que el proceso ha terminado exitosamente, o 1 si es que ha habido algún tipo de error.

  `process.cwd()`
  devuelve el directorio actual desde donde se está corriendo la app de Node(NO ES LA UBICACION DEL ARCHIVO).

  `process.on('evento', callback)`
  esto permite escuchar eventos del proceso y poder manejar errores

  


### Importaciones y exportaciones de módulos.

normalmente, vamos a importar muchas funciones, objetos, de distintos módulos, pero si localmente debemos hacer esto, podemos tener las funciones por un lado, por ej en el archivo "funciones.js", y objetos por otro, archivo "objetos.js".

Estos archivos se verían por ej asi:

***FUNCIONES***
 
```node
const getTitle = ()=> 'Curso de node js por sergie code'; //defino la funcion getTitle

    const getAuthor = (author) => `EL auto del curso es ${author}`; //defino la funcion getAuthor

    module.exports = {  //con esta linea, exporto ambas.
    getTitle, 
    getAuthor
}
```

y el archivo de objetos muy similar:

***OBJETOS***
```node
 const Curso = {    //defino el objeto o clase por ejemplo.
 nombre:'Curso de node js',
 autor:'Sergie Code'
 }
   
  module.exports = {  //exporto similar a las funciones.
  Curso
   }
```

Entonces, para importar estos datos desde otro archivo, por ej. index.js, podemos realizar lo siguiente:

```node
const (nombre de la constante) = require('./funciones.js');
const (nombre de la constante) = require('./objetos.js');
```

esto nos habilita a usar funciones y objetos importados de otros archivos con la siguiente sintaxis:

```node
console.log([nombre de la constante].getTitle()); //esto devolvería la leyenda 'Curso de node js por sergie code'.
```


---

Para desestructurar esto, y poder escribir directamente el nombre de la función a usar, se usa la siguiente sintaxis:

    const { getTitle, getAuthor } = require('./funciones');

    const { Curso } = require('./objetos');

>[!warning] Notar como los nombres de los archivos no lleva la extensión js dado que se da por sentado que son archivos js.


>[!warning] La manera de importar se ha actualizado, y se utiliza una manera más moderna. Pero el proyecto debe cumplir con ciertas condiciones.

1 - La descipción del proyecto, debe indicar que el tipo de app es "module".
```node
 "name": "proyecto-nodejs",
 "version": "0.0.1",
 "description": "primer proyecto orientado a practicar nodejs",
 "main": "src/server.js",
  ------"type" : "module",----
```

2 - La sintaxis para importar es la siguiente:

Notar que se agregan las extensiones de ambos archivos al importar...  
```node   
import { getAuthor, getTitle } from './funciones.js';
import { Curso } from './objetos.js';
```

3 - La forma de exportar en el archivo de orígen de la exportación varía de la siguiente manera:

>[!important] Se le agrega la palabra reservada 'export' delante de la definición de la función.

```node
export const getTitle = ()=> 'Curso de node js por sergie code'; //defino la funcion getTitle
export const getAuthor = (author) => `EL auto del curso es ${author}`; //defino la funcion getAuthor
```

y el objeto igual:

```node
 export const Curso = {    //defino el objeto o clase por ejemplo.
   nombre:'Curso de node js',
   autor:'Sergie Code'
   };
```

---

## Cargando variables de entorno al Process.env

Actualmente, a partir de _NodeJS_ ver. 22, se pueden cargar las variables de entorno mediante un método interno de _Process_.

esto se realiza creando un archivo *.env* en el proyecto, y en el mismo definiendo las variables que queremos tener, por ej.

```
USER = 'david@gmail'
PASSWORD = 'testing01'
DBASE = mongo
```

y luego, al iniciar el archivo _.js_, se usa el método:

`process.env.loadEnvFile([ruta al archivo .env])`


## Métodos y módulos nativos más comúnes.

NodeJS viene con módulos nativos que se suelen utilizar mucho en la construcción de distintas aplicaciones y proveen de mucha información del entorno de ejecución del mismo proceso actual. Tenemos métodos para leer archivos, rutas, extensiones, información sobre el sistema operativo, etc.


Para leer el directorio actual, se pueden utilizar algunos métodos básicos.

### process.cwd() 
Este método nos devuelve la ruta al directorio actual del proceso. Si el proceso se ejecuta en 
`c:\gitwork\proyectos\proyecto1\app.js`

...el metodo nos devuelve la siguiente ruta:
 `c:\gitworkproyectos\proyecto1\`


### import.meta.url()
Este método nos devuelve la ruta con file incluido, al archivo donde se ejecuta, independientemente del arbol de subcarpetas que posea el proyecto.
Si el proyecto tiene la estructura:
`c:\gitwork\proyectos\proyecto1\main\utils\app.js`

...el metodo devolverá la misma ruta URL completa:
`file:////c:/gitwork/proyectos/proyecto1/main/utils/app.js`

---
### path

Este módulo nos permite manejar con facilidad las rutas relativas y absolutas usadas en los proyectos. Permite determinar rutas según el sistema operativo, y permitir mucha más compatibilidad con nuestro proyecto.

Principales métodos:

`path.basename([ruta_al_archivo]):`
   * Devuelve el nombre del archivo incluyendo la extensión en la ruta dada.
   * Se le puede pasar un segundo argumento para eliminar la extensión del archivo en el resultado.
  
ej:
```
const ruta = "/users/documentos/archivo.txt"
console.log(path.basename(ruta, '.txt'))   //esto devuelve "archivo"
```

`path.dirname([ruta_al_archivo])`
   * Devuelve el directorio de la ruta, EXCLUYENDO el nombre del archivo.

ej:
```node
const ruta = "/users/documentos/archivo1.png"
console.log(path.dirname(ruta))   //esto devuelve "/users/documentos"
```

`path.extname([ruta_al_archivo])`
* Devuelve la extension del archivo pasado como argumento, incluyendo el punto.

ej:
```node
const ruta = "/users/documentos/archivo1.png"
console.log(path.extname(ruta))   //esto devuelve ".png"
```

`path.join([argumento1, argumento2, argumento3])`

  * Este metodo normaliza las rutas, y une en una sola cadena, la ruta conformada por _argumento1_, _argumento2_ y _argumento3_ con su separador correspondiente de acuerdo al sistema operativo usado.
  
  ej:
```node
const ruta = path.join('users', 'documentos', 'archivo1.png')
console.log(ruta) // esto devolverá "/users/documentos/archivo1.png"
```

`path.resolve([arg1, arg2, ..., argN])`

   * Construye una ruta absoluta a partir de una secuencia de segmentos con arg1, arg2, etc.
   * Si no se especifica un directorio inicial, toma _process.cwd()_(directorio de trabajo actual) como base.


```node
const rutaAbsoluta = path.resolve('documentos', 'archivo1.txt')
console.log(rutaAbsoluta) //esto devuelve 'ruta/actual/documentos/archivo1.txt'
```

`path.normalize([ruta_al_archivo])`
 
 * Normaliza una rura, resolviendo elementos como . y .. y eliminando separadores redundantes en la misma.

ej:
```node
const ruta = '/usuarios//documentos/./archivo.txt'
console.log(path.normalize(ruta)) //esto devuelve '/usuarios/documentos/archivo.txt'
```

` path.isAbsolute([ruta_al_archivo])`

* Devuelve _true_ si la ruta es absoluta, o _false_ si es relativa.

ej:
```
console.log(path.isAbsolute('/usuarios/documentos')); // true
console.log(path.isAbsolute('documentos/archivo.txt')); // false
```

`path.relative([argumento1-FROM, argumento2-TO])`
* Este método calcula la ruta relativa, entre los 2 argumentos pasados, indicando la secuencia de directorios para pasar de una a la otra.

ej:
```node
const ruta1 = '/usuarios/documentos';
const ruta2 = '/usuarios/fotos';
console.log(path.relative(ruta1, ruta2)); // '../fotos'
```

`path.parse() y path.format()`
* El método `path.parse([ruta])` convierte una ruta pasada como argumento, a un objeto con las propiedades `root`, `dir`, `base`, `name` y `ext`.

* El método `path.format(objRuta)` construye un string con los datos de un objeto con las propiedades indicadas anteriormente.
  

```node
const ruta = '/usuarios/documentos/archivo.txt';
const objRuta = path.parse(ruta);
console.log(objRuta);
/* {
  root: '/',
  dir: '/usuarios/documentos',
  base: 'archivo.txt',
  name: 'archivo',
  ext: '.txt'
} */

console.log(path.format(objRuta)); // '/usuarios/documentos/archivo.txt'
```

# Coerción

La coerción es el proceso implícito de cambiar de tipo un dato según sea necesario o lo más lógico de acuerdo a la necesidad.

Los valores en Javascript tienen diferentes tipos, se puede tener números, cadenas de texto, objetos, booleanos, etc.
A veces es necesario convertir de un tipo a otro dada la situación.

Esta conversión de tipo puede ser explícita, dado que el programador lo necesita, o implícita si no se maneja y se deja al lenguaje manejar automáticamente según sea necesaria.

La conversión implícita del tipo de dato es conocida como **coerción**, mientras que la conversión explícita se conoce como **type casting**.

Hay operaciones que quizás quieras realizar en js que no son correctas en términos de tipos de datos. por ej:
```js
const num = 35 + "hello";
```

Aqui, estás tratando de sumar un número a una cadena de caracteres, lo cual no es posible. Sólo puedes sumar números con números, o puedes concaternar cadenas con cadenas.

Si corres dicho código, al ser Javascript un lenguaje débilmente tipado, en vez de tirar un error, va a coercionar el tipo de dato de un valor para acomodarse al otro y poder realizar la operación.

En este caso, al usar el símbolo + con un número y una cadena, 
[el número es coercionado a ser una cadena] para poder concatenar ambas.

```js
const num = 35 + "hello";

console.log(num);
//35hello

console.log(typeof num);
//string
```

En este tipo de operación, con un número y una cadena, es más lógico transformar *el número en cadena*, y poder concatenarlas, que transformar una cadena en número (que al fin y al cabo, no sería un número válido) y tratar de sumarlos.

```js
console.log(String(14); // "14"
console.log(Number(texto); // "NaN"
```

>[!important] Importante
>Se demuestra aqui que es más lógico convertir el número a cadena que la cadena en un número que no existe entre la suma de un número y una cadena.

En el caso de una multiplicación de un número con una cadena, lo más lógico sería convertir la cadena a número, dado que si usamos el asterísco como operador de multiplicación para marcar el producto, las cadenas no tienen este operador que realice algo, los números SI, por lo que es más lógico intentar multiplicarlos. Al convertir la cadena a un número, normalmente el resultado es [NaN] dado que generalmente las cadenas no se transforman a números excepto que sean números escritos como cadena. 
Si ese es el caso, entonces se puede realizar el produco y la operación es válida.

```js
const producto = 35 * "hello";
console.log(producto);
// NaN

//pero si es asi...
const producto = 35 * "2";
console.log(producto);
// 70
```

Existen otros tipos de coerciones, un operador que suele causar coercion de manera habitual es el comparador igual [\=\=] **loose equality operator**

## **El operador de igualdad simple y coercion**
En Javascript, existen ambos operadores, igualdad simple [\=\=] y el operador de igualdad estricta [\=\=\=].
Se suelen utilizar ambos para comparar igualdades entre valores.
El operador de igualdad simple suele hacer un chequeo simple **SOLAMENTE DEL VALOR** contenido en los operandos a comparar. Este operador NO COMPARA TIPOS de valores, solamente los valores.

Ejemplo: Si tenemos 2 variables, valor1 = 20 y  valor2 = "20", cuando se comparan con el operador de igualdad doble, el resultado es **true**.

Aqui se utiliza la coerción para determinar que "20", pasado al tipo número, es 20.
```js
const valor1 = 20;
const valor2 = "20";

console.log(valor1 == valor2);
//true
```

>[!warning] Cuidado!!!
>Cuando usamos el operador de igualdad doble con valores de distintos tipos, lo primero que sucede es **coerción**.

Si tenemos por ejemplo, la comparativa entre un booleano y una cadena vacía, sucede la coerción y luego se comparan dado que una cadena vacía se coerciona al valor booleano **false**

Ejemplo:
```js
const var1 = false;
const var2 = "";
console.log(var1 == var2);
//esto devuelve true
```

## El operador estricto de igualdad
Como el funcionamiento de este operador es chequear tanto valor como tipo de dato a comparar, es imposible que suceda coerción en la comparación de valores de distinto tipo. Si el tipo a comparar es distinto, el resultado será siempre *false*

```js
const variable1 = 20
const variable2 = "20"

console.log(variable1 === variable2)
// false

const variable3 = false
const variable4 = ""

console.log(variable3 === variable4)
// false
```

## Type Casting o conversión manual de tipos

Cuando necesitamos explícitamente que un valor sea de determinado tipo, aplicamos el type casting. Esto se logra con los `type contructors` .

Ejemplos:

Número a string:
```js
const number = 30
const numberConvert = String(number)

console.log(numberConvert)
// "30" es un string

console.log(typeof numberConvert)
// string
```

Número a booleano:
```js
const number = 30
const numberConvert = Boolean(number)

console.log(numberConvert)
// true

console.log(typeof numberConvert)
// boolean
```

Booleano a String:
```js
const boolean = false
const booleanConvert = String(boolean)

console.log(booleanConvert)
// "false"

console.log(typeof booleanConvert)
// string
```

---

# Objetos


