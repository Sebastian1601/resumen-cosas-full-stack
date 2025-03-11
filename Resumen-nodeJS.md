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

