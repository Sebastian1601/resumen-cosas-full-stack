# Instalando NodeJS y creando el primer hola mundo!.

## Forma tradicional de instalar una única versión de nodejs en la pc. 

Para instalar NodeJS, nos dirigimos a la página oficial
[http://nodejs](https://nodejs.org/en) y vamos a la sección _DOWNLOADS_ y luego _Prebuilt installer_
Vamos a buscar la versión correspondiente al hardware que estemos corriendo y elegir la versión (LTS) long term support. que son las versiones a las que más soporte le dan sin implementar cambios muy significativos.


## La manera recomendada, es utilizar ciertas apps, para poder manejar las distintas versiones que podemos instalar, y correr los programas dependiendo de cada version que querramos utilizar.

Para esto, necesitamos de 3 aplicaciones requerídas. Windows Terminal (WSL), RUST, y Fast Node Manager (fnm).

- Para instalar Windows Terminal(que no es cdm, ni windows powershell), podemos instalarlo desde la página oficial de microsoft con una simple busqueda.
- Para instalar RUST, vamos a https://www.rust-lang.org/learn/get-started, y copiamos el código que brinda la página en nuestra Terminal.
- Puede ser que tengamos que instalar Unos archivos de VISUAL STUDIO INSTALLER, pero el mismo instalador de RUST nos da la opción de hacerlo.
- Finalmente, luego de instalado RUST y los derivados de Visual Studio, abrimos la terminal Bash por ej. de GIT, y colocamos el c+odigo indicado en la página de fnm.
- esto finalmente indicará que se instaló fnm, para verificarlo, cerrar y reabrir la terminal.
- al finalizar, podemos poner

              fnm --version

  y esto debería resultar en la versión instalada de fnm.

  comandos:

   - _fnm list_: devuelve la lista de versiones de node js instaladas.
   - _fnm install (version de node a instalar)_ : esto instala la versiòn que existe en la página oficial de node.
   - _fnm use (version de node a usar)_ : esto determina qué versión ejecutará el código indicado.
   - _fnm alias (versión de node a referenciar) default_ : esto hace que la versión indicada de node quede "por defecto" a utilizar cada vez que iniciemos un código, evitando que se usen otras versiones ya instaladas automáticamente.
   - _fnm --HELP_ : muestra los distintos comandos que fnm puede tener.
 
---





---

Luego de esto, podemos iniciar un proyecto, creando la carpeta, un archivos por ej: server.js e iniciar el proyecto, ingresando en la consola

      npm init

  esto inicia el creado del archivo package.json, que guardará información sobre nuestro proyecto, dependencias, y demás info.
Iinicialment el archivo se ve así:

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

la mayoría de campos se explican solos, pero los de scripts, son campos que pretenden determinar qué se ejecuta al escribir en la consola por ej:

    npm run dev

esto iniciará en la terminal la linea de código escrita en esa propiedad del objeto, o sea 
> src/server.js  // esto inicia nuestro codigo de servidor en server.js


el comando:

      npm start

automáticamente inicia nuestra ruta descripta, normalmente se usa para iniciar el codigo, para pruebas, demostración, etc.

### Instalando dependencias

  Las dependencias son módulos de código, que nos permiten realizar distintas cosas ya escritas en javascript, para acelerar el proceso y no tener que crear todo desde 0.

  ejemplos;
    - nodemon : esta dependencia nos permite ejecutar un tipo de "live server" para archivos nodejs. La terminal se actualiza cada vez que se guarda un cambio, evitando tener que pararla y ejecutarla manualmente cada vez que hacemos un cambio.
    - express : esta dependencia se utiliza para el manejo de páginas web.

### Pagina NPM para buscar e instalar modulos.

https://www.npmjs.com/package/express


### Importaciones y exportaciones de módulos.

normalmente, vamos a importar muchas funciones, objetos, de distintos módulos, pero si localmente debemos hacer esto, podemos tener las funciones por un lado, por ej en el archivo "funciones.js", y objetos por otro, archivo "objetos.js".

Estos archivos se verían por ej asi:

_funciones.js_ =>

    const getTitle = ()=> 'Curso de node js por sergie code'; //defino la funcion getTitle

    const getAuthor = (author) => `EL auto del curso es ${author}`; //defino la funcion getAuthor

    module.exports = {  //con esta linea, exporto ambas.
    getTitle, 
    getAuthor
    }

y el archivo de objetos muy similar:

_objetos.js_ =>

    const Curso = {    //defino el objeto o clase por ejemplo.
    nombre:'Curso de node js',
    autor:'Sergie Code'
    }
    
    module.exports = {  //exporto similar a las funciones.
    Curso
    }

Entonces, para importar estos datos desde otro archivo, por ej. index.js, podemos realizar lo siguiente:

    const (nombre de la constante) = require('./funciones.js');
    const (nombre de la constante) = require('./objetos.js');

esto nos habilita a usar funciones y objetos importados de otros archivos con la siguiente sintaxis:

    console.log([nombre de la constante].getTitle()); //esto devolvería la leyenda 'Curso de node js por sergie code'.

---

Para desestructurar esto, y poder escribir directamente el nombre de la función a usar, se usa la siguiente sintaxis:

    const { getTitle, getAuthor } = require('./funciones');

    const { Curso } = require('./objetos');

> Notar como los nombres de los archivos no lleva la extensión js dado que se da por sentado que son archivos js.


⚠️ La manera de importar se ha actualizado, y se utiliza una manera más moderna. Pero el proyecto debe cumplir con ciertas condiciones.

1 - La descipción del proyecto, debe indicar que el tipo de app es "module".

      "name": "proyecto-nodejs",
      "version": "0.0.1",
      "description": "primer proyecto orientado a practicar nodejs",
      "main": "src/server.js",
      ------"type" : "module",----

2 - La sintaxis para importar es la siguiente:
> Notar que se agregan las extensiones de ambos archivos al importar...  
    
    import { getAuthor, getTitle } from './funciones.js';
    import { Curso } from './objetos.js';


3 - La forma de exportar en el archivo de orígen de la exportación varía de la siguiente manera:
> Se le agrega la palabra reservada 'export' delante de la definición de la función.

    export const getTitle = ()=> 'Curso de node js por sergie code'; //defino la funcion getTitle
    export const getAuthor = (author) => `EL auto del curso es ${author}`; //defino la funcion getAuthor

y el objeto igual:

    export const Curso = {    //defino el objeto o clase por ejemplo.
                  nombre:'Curso de node js',
                  autor:'Sergie Code'
                  };


---

