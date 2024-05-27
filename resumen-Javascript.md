# Javascript para principiantes.

una variable se asigna con el operador "="

si ingresamos un nro, puede no tomarse como nro.
un numero escrito en comillas, es tomado como un "string de texto"("cadena")

## Number.parseInt("7130") esto devuelve 7130 como número propiamente dicho.

    Number.parseInt(42000$$) devuelve 42000.

    Number.parseInt("Num. 2345") devuelve NaN (not a number) por lo tanto no puede convertir.

## Number.parseFloat() 

devuelve un nro con coma flotante (decimal)

# Operadores de asignacion

|Operador | Descripción    |
|---------|----------------|
| +       |  Suma          |
| -       | Resta          |
| *       | Multiplicacion |
| **      | Exponenciación |
| /       | Division       |
| %       | Módulo:resto de dividir|
| ++      | Incremento     |
| --      | Decremento     |
____________________________


## Operadores de cadena y números.-

El operador + se puede utilizar también para concaternar cadenas.

ej:
    
        var texto1 = "Juan" ;
        var texto2 = "Pablo" ; 
        var textoJunto = texto1 + " " + texto2 ; 
         
> (se agrega + " " + para sumar un espacio vacío entre las 2 cadenas y que no quede "JuanPablo" sino "Juan Pablo")

ej2:

        var texto3 = "bienvenidos a ";
        var texto3 += "Javascript" ;



## funcion Prompt() :

- Metodo de windows, permite al usuario ingresar datos con una ventana emergente.

      prompt ([mensaje de texto a mostrar:string], [valor por defecto al abrir el prompt, como un placeholder]);

## document.write() :

- comando de consola que permite escribir los datos dentro del paréntesis directamente en el HTML como texto simple, aún asi, se pueden agregar etiquetas completas para darle formato a lo escrito en el HTML.

  ej:
  
      document.write('<div class='ejemplo'>texto a ingresar</div>');


# Operadores de comparación

|Operador ------- | Descripción ------------- |
| ----------------|---------------------------|
| ==              |     igual a    |
| ===               |  igual valor y tipo |
|!=        |no igual a |
|!==           |igual valor no tipo |
| >           | mayor a       |
| <          | menor a          |
| >=         | mayor o igual que |
| <=         | menor o igual que |
|?           | operador ternario |


# Operadores lógicos

> Normalmente se utilizan con valores booleanos (true or false);


| Operador | Descripción |
|----------|-------------|
| &&       | Y lógico    |
|  ||      |  O lógico   |
| !        | No lógico   |


# Operadores Prefijo y Posfijo

| Operador | Descripción | Ejemplo |
|-----------|------------|---------|
| i++       | incremento posfijo | a=i++ primero a=i y luego i=i+1|
|++i       | incremento prefijo| a= ++i primero i=i+1, luego a=i|
|i--       | decremento posfijo| a= i-- primero a=i y luego i=i-1|
|--i       | decremento prefijo| a=--i primero i=i-1 luego a=i|


# Operadores de asignación

|Operador | Descripción | Equivale a |
|---------|-------------|------------|
| =     | x=3          | x=3        |
|+=      | x += y      | x= x+y      |
|-=      | x -= y     | x= x-y      |
|*=      | x *= y       | x = x * y |
|/=      | x/=y        | x= x / y   |
|%=      | x %=y       | x = x % y  |
|**=     | x **= y     | x = x**y    |



))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))

# ESTRUCTURAS DE CONTROL 

> Condicional que evalua una condicion, y de ser verdadera, ejecuta un bloque de código, sino tiene la opción de ejecutar otro código.

## If condicional

    if (condicion) {
    [bloque a ejecutar si la condicion es verdadera]
    } else {
    [bloque a ejecutar si la condicion es falsa]
    };


### Las condiciones pueden ser más de una, donde se utilizan los operadores lógicos && y || para evaluar condiciones más complejas.

    if (condicion1 && condicion2) {
    bloque a ejecutar si ambas son correctas
    };


## Operador Ternario

> es un operador que evalua similar al if/else pero con la estructura más legible

        var calificacion = nota < 5 ? "suspendido" : "aprobado";
        console.log("estoy", calificacion);
    

## Switch evalua cierta cantidad de posibilidades

La estructura de control switch permite definir casos específicos a realizar en el caso de que la
variable expuesta como condición sea igual a los valores que se especifican a continuación mediante los case.

        var nota = 7;
        switch (nota) {
            case 10:
                console.log("sobresaliente");
                break;
            case 9:
                console.log("notable");
                break;
            case 8:
                console.log("bien");
                break;
            case 7:
                console.log("aprobado");
                break;
            case 6:
                console.log("suficiente");
                break;
            case 5:
            case 4:
            case 3:
            case 2:
            case 1:
            default:
                console.log('no es un valor válido');
                break;
        }


# Bucles e Iteraciones:

### Los bucles evalúan una condición y se ejecutan si la condicion es verdadera.
 - Condición : el bucle evalúa la condición para saber si se genera una nueva iteración del mismo o no.
 - Iteracion : se llama así a cada repetición que se genera del bucle.
 - contador : Los bucles suelen usar una variable como **contador** para muchas tareas. la variable suele *vivir* solamente dentro del bucle.
 - Incremento : se debe incrementar la variable contator para que el bucle avance. Un bucle que no tiene un contador, generalmente depende si o si de que la condicion se cumpla o no.
 - Bucle Infinito : esto se da si la condicion nunca se cumple y si el bucle no tiene un contador.

# While (estructura de control)

El bucle *while* se utiliza cuando es necesario generar un bucle analizando una condición a cumplirse.

        while (condicion a evaluar) {
        bloque a ejecutar mientras la condicion sea verdadera
        }`

### Es importante que la condición en algún momento sea falsa, para terminar el bucle, sino se produce un bucle infinito, deteniendo la ejecución del resto del código js.


# FOR (estructura de control definida - bucle finito)

Un bucle *for* depende de el valor de una variable, que automáticamente va incrementandose por lo tanto hay determinada cantidad de iteraciones del mismo.

        for (let i=1 ; i <= 10; i++) {
        bloque de código a ejecutar mientras se cumple el 2do término de la condición
        }`
    

# *FUNCIONES*

Las funciones nos permiten agrupar líneas de código en tareas con un nombre (subprograma), para que posteriormente podamos referenciar ese
nombre para realizar dicha tarea. Algunas razones para declarar funciones:

● Simplificación: Cuando un conjunto de instrucciones se va a usar muchas veces, se
crea una función con esas instrucciones y se llama la cantidad de veces que sea
necesario, reduciendo un programa complejo en unidades más simples.

● División: Una función me permite modularizar, es decir, armar módulos. De esta
manera un equipo puede dividir el trabajo en partes. Cada integrante realiza una
función, para luego integrarlas en un programa principal más grande.

● Claridad: Usando funciones un programa gana claridad, aunque esa función solo
se llame una vez.

● Reusabilidad: Una función es reutilizable, sólo es necesario cambiar los valores de
entrada

- Declarar la función es darle un nombre a la funcion y definir qué realizará.
- Ejecutar la función es "llamar" o "invocar" la función para que se ejecute en el punto del código donde la llamamos.

> El nombre de la función debería ser descriptivo e indicar qué tarea realiza. Deberían ser:
    - simple, claro
    -Representativo de la tarea que realiza la función.
    -verbos en infinitivo, (-ar, -er, -ir)
    -Si es más de una palabra, se usa la nomenclatura camelCase

### **Parámetros** 
: Los **parámetros** de la función son variables que ponemos cuando definimos la función.
ej:

        function sumar (a, b) {
        console.log( a+b );
        };`

> En este caso, los parámetros son a y b, definidos entre paréntesis al lado del nombre de la función.

> Los parámetros predeterminados se suelen inicializar con un valor por si no se pasa ningún parámetro para el mismo al invocar la función ==


        function multiplicar (a, b = 1) {
        return a * b;
        }


### **Argumentos**
   : Los **argumentos** son los valores que se le pasan mediante los parámetros

    let a = sumar( 7,4 );
    console.log(a); //se espera 11 como resultado


### Devolución de valores
 : una función puede ejecutar código sin devolver nada al terminar, o puede devolver datos necesarios obtenidos durante el proceso, para posteriormente utilizarlos en otra función u otro evento. Para esto se usa *RETURN*.

    
     function sumar ( a, b){
     return a+b;
     }


> El comando *RETURN* devuelve lo necesario fuera de la función, y termina la ejecución del código, si existe más código a ejecutar luego del return, este no se realiza.


---

#FUNCIONES FLECHA O 'ARROW'

### Las funciones flecha se utilizan para definir funciones de manera más fluida y resumida. Normalmente se asignan a una constante, para que no puedan variar ni reasignarse.

definicion:

    const Variable = (parámetros) => {
    bloque a ejecutar 
    };

 ---

ej:

    function cuadrado (x) {
    return x*x
    }
    console.log(cuadrado(2))


esto es lo mismo que lo siguiente:


    const Cuadrado = x => x*x;
    console.log(Cuadrado(2));



##Sintaxis básica

*Un parámetro. con una expresión simple, no necesita RETURN*

        parámetro => expresión

*Varios parámetros requieren paréntesis, con una expresión simple no necesita RETURN*

        (parámetro1, parámetro2, ..., parámetroN) => expresión

*Un parámetro con varias líneas de código necesitan llaves y RETURN*

        parámetro => {
        varios bloques de código
        .
        .
        .
        bloque de código;
        RETURN (a devolver)
    }

*Varios parámetros requieren paréntesis y varias lineas de código requieren llaves y RETURN*

        (parámetro1, ...,parámetroN) => {
        bloque de código;
        .
        .
        .
        bloque de código;
        RETURN (a devolver)
        }
# FUNCIONES ANÓNIMAS

  Son funciones que se definen **sin nombre**, y se alojan en una variable haciendo referencia a la misma cuando queremos ejecutar la función.

      const Saludo = function (){
            return "Hola"
            }

      const Saludo = function (nombre) {
          var mensaje = "hola "+ nombre;
          return mensaje;
          }


# SCOPE (alcance)

El scope (alcance) determina la accesibilidad (visibilidad) de las variables. Define ¿en qué contexto las variables son visibles y cuándo no lo son?. Una variable que no está “al alcance actual” no está disponible para su uso.
En JavaScript hay dos tipos de alcance:
    ● Alcance local (por ejemplo, una función)
    ● Alcance global (entorno completo de JavaScript)
Las variables definidas dentro de una función no son accesibles (visibles) desde fuera. La función “crea un ámbito cerrado” que impide el acceso a una variable de su interior desde fuera de ella o desde otras funciones. 

Si asignamos un valor a una variable que no ha sido declarada, se convertirá en una variable global. Este ejemplo declara la variable global carName, aún cuando su valor se asigna dentro de una función.
ej:

    myFunction();
    //aqui se puede usar carName
    function myFunction () {
        carName = "Wolkswagen";
    }

> En este concepto, declarar variables con *let* permite que la misma se utilice y "exista" solo en el ámbito donde fue creada, disponiendo de la misma una vez el código del bloque donde se definió termina de ejecutarse. Definir una variable con *var* genera que la misma esté disponible en todo el *SCOPE*, por lo que hay que ser cuidadoso al manejar los valores de la misma.

# CALLBACK

Se determina *"Callback"* a una función que fue pasada como parámetro de otra. 

# CLOSURE

Un *CLOSURE* se define como una función que encierra variables en su propio ámbito.


# OBJETOS EN JS.

Un objeto de JavaScript tiene propiedades asociadas a él. Una propiedad de un objeto se puede explicar como una variable asociada al objeto. Las propiedades de un objeto básicamente son lo mismo que las variables comunes de JavaScript, excepto por el nexo con el objeto.

El objeto se puede crear mediante el operador de asignación (=), o de la manera "literal".
ej:
Manera con el operador de asignación:

        var miAuto = new Object();

        miAuto.marca = "wolkswagen";
        miAuto.tipo = "automóvil";
        miAuto.modelo = 2013;

Manera literal de crear un objeto:

        var miAuto = {
            marca:"wolkswagen",
            tipo: "automovil",
            modelo: 2013
            };

###También los objetos pueden tener *METODOS* (son funciones asociadas a los objetos en si):

ej:

            var miAuto = {
            marca:"wolkswagen",
            tipo: "automovil",
            modelo: 2013,
            datosDelVehiculo: function () {
                return "Este es un " + this.marca + ", tipo " + this.tipo + ", modelo " + this.modelo
            };
esto permite que al nosotros invocar el método del objeto miAuto, se obtenga los 3 datos del objeto.

            console.log(miAuto.datosDelVehiculo()); //esto devuelve "Este es un wolkswagen, tipo automovil, modelo 2013"


### Los metodos pueden ser creados con otra sintaxis, ej:

      var miAuto = {
            marca:"wolkswagen",
            tipo: "automovil",
            modelo: 2013,
            datosDelVehiculo () {
                return "Este es un " + this.marca + ", tipo " + this.tipo + ", modelo " + this.modelo
            };


## Acceder a las propiedades de un objeto.

Para acceder a las propiedades de un objeto hay distintas notaciones. 
Se puede utilizar el punto; `miAuto.marca`, se puede utilizar corchetes; `miAuto['marca']`
            
> ⚠️ El nombre de una propiedad puede ser cualquier cadena válida de JS. Pero si
no es un identificador válido de JS (por ejemplo, comienza con un número)
solo se puede acceder utilizando la notación de corchetes.


# OBJETOS | CLASES

 Las clases son una suerte de *molde* para crear distintas instancias de un tipo de objeto. Se usa el "*CONSTRUCTOR*" y *THIS* para asignar valores a las propiedades y metodos.

ej:

        class Perro {
            constructor ( _nombre, _edad, _color) {
                this.nombre = _nombre
                this.edad = _edad
                this.color = _color
                }
            }

Esto permite generar un nuevo objeto con estas propiedades de la siguiente manera

    var Perro1 = new Perro ('Lola', 4, 'marrón'); 
    var Perro2 = new Perro ('Estrellita', 10, 'blanco');

    
# String (PROPIEDADES Y MÉTODOS).
---
Cuando hablamos de una variable que posee información de texto, decimos
que su tipo de dato es String. Hay dos formas de crear una variable de texto:

con el método del objeto `var texto = new String('hola a todos');` o de manera literal (es la más utilizada): 
`var texto = 'Hola a todos';`

existen muchos métodos para strings dado que JavaScript fue diseñado en base a manejar cadenas de texto, por lo tanto, las posibilidades son muchas.

| Propiedad ---------------- | Descripción -------------------------------------------------------|
|----------------------------|------------------------------------|
|  .length                | Devuelve el número de caracteres de la variable de tipo string en cuestión|
|  .charAt(*index*)                | Devuelve el carácter en la posición *index* de la variable. |
|  .concat(*str1*, *str2*,...,*strN*) | Devuelve una nueva cadena uniendo *str1*, a *str2*..., a *strN* |
|  .indexOf(str)    |  Devuelve la primera posición del texto *str* |
|  .indexOf(str, from) | Devuelve la posición de *str*, partiendo desde el index *from* |
 | .lastIndexOf(str, from) | Devuelve la posición de *str*, pero indica la última posición encontrada desde *from*|
| .toLowerCase () | Devuelve el string de la variable aplicada en minúsculas. |
| .toUpperCase () | Devuelve el string de la variable aplicada en mayúsculas. |
| .repeat (**n**) | Devuelve el string repetido **n** veces  |
| .trim () | Devuelve el string de la variable aplicada sin espacios a la izquierda y derecha |
| .replace (*str*, *nuevastr*) | Reemplaza la primera iteración de *str* con *nuevastr*  |
| .substring(*ini*, *len*) | Devuelve el subtexto generado desde la posición *ini*, hasta *ini* + (*len* - 1) |


---

##TEMPLATE STRINGS

Las Template Strings utilizan las comillas invertidas o backticks para
delimitar sus contenidos, en vez de las tradicionales comillas simples o
dobles de las cadenas de texto normales.
Las principales funcionalidades que aportan las Template Strings son:
● Interpolación de cadenas.
    : La interpolación permite utilizar cualquier expresión válida de JavaScript (como por ejemplo la suma de dos variables)
    dentro de una cadena y obtener como resultado la cadena completa con la expresión evaluada.
    Las partes variables de una Template String se denominan placeholders y utilizan la sintaxis ${ } para diferenciarse del
    resto de la cadena.
● Posibilidad de incluir (y evaluar) expresiones dentro de cadenas.
● Definición de cadenas de texto en varias líneas sin tener que usar hacks.
● Formatear cadenas de manera avanzada.
● Cadenas etiquetadas.
 
ej: 

        var a = 10;
        var b = 10;
        console.log(`Javascript se publicó hace ${ a + b} años!`);

        console.log(`Existen ${2 * (a + b)} frameworks Javascript`);

Dentro inclusive del valor interpolado, se pueden utilizar directamente funciones.

ej:

        function fn () { return "este es el resultado" };
        console.log (`Hola mundo! ${ fn () }`);

Incluso la sintaxis permite acceder a métodos y propiedades...
ej:

    var usuario = {nombre : "Juan Perez"};
    console.log(`Estás hablando con ${ usuario.nombre.toUpperCase() }.`);



# OBJETO MATH ------
---
Math es un objeto que tiene propiedades y métodos para constantes y funciones matemáticas.

```Math.E /n Math.LN2 /n Math.LN10 /n Math.LOG2E /n Math.LOG10E /n Math.PI /n Math.SQRT1_2 /n Math.SQRT2```

###Los métodos más útiles para web.

| Método -----------| Descripción     |
|-------------------|--------|


 




))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))

# Funciones ASYNC y promesas.

  En Javascript el código se realiza una linea a la vez, y si existe un problema, el código no termina de realizarse, esto implica que cuando nos queremos comunicar con un server externo, a través del código, esa respuesta puede demorar.
Para que el código no se detenga hasta obtener dicha respuesta, se utilizan las funciones ASINCRONAS (async) y el manejo de "promesas"-
Las "promesas" son primeras respuestas del servidor a donde nos comunicamos, indicándonos que "nos van a retornar algún tipo de dato.

hay 2 maneras de manejar este tipo de código: por ejemplo, si queremos traer datos desde una api, necesitamos ciertos datos de la misma para comunicarnos, como mínimo, la dirección web de donde nos van a enviar los datos(esto lo define CADA api en su propia documentación).

teniendo este dato, podemos solicitar nos envíen la información de la siguiente manera;

    fetch ('direccion web de la api')  //rdto devuelve una promesa, que tenemos que manejar con .then()//
    
    .then ('datos en formato json'.json())  //aqui normalmente tenemos la respuesta, pero la misma está en formato json, por lo que la convertimos al obtenerla, genenrando una funcion flecha, que a su vez, genera una nueva promesa
    
    .then (('varDatosEnObjeto') => {resto de codigo a ejecutar}) //aqui ya tenemos los datos del json en formato objeto, para poder manipularlos, y normalmente el manejo se hace en esta instancia, mediante funciones, etc porque los datos no se pueden sacar a no ser que se manejen con otra funcion asyncrona.

    .catch (error) {
    //codigo segun el error dado por la respuesta. //si el servidor da una respuesta de error, enviará un codigo del error que se puede ver en developers.mozilla.org.
}
        
)))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))))

# Manejo del DOM ------------------------------------------------------------------------
Tipos de nodo:
    -Document: es el nodo raíz del cual se derivan el resto de nodos.

    -Element: son nodos definidos por etiquetas HTML ej: <div>, <p>, <span>, etc.

    -Text : el texto dentro de un nodo element se considera un nuevo nodo hijo del tipo "text"

    -Attribute: los atributos de las etiquetas definen nodos, pero en js lo vemos como información asociada al nodo.

    -Comment node: los nodos que definen comentarios.

##DOCUMENT - Metodos de seleccion de elementos:

    como son métodos, se aplican al nodo document.

obtener un nodo por id:
    
                document.getElementByID('id a seleccionar');

obtener nodos por nombre de etiqueta:

                document.getElementsByTagName('div'); //esto devuelve una coleccion HTML de elementos, donde se puede acceder a cada elemento por indice(como un array, pero sin ser un array)

obtener nodos por querySelector:

                document.querySelector('.clase'); *// esto permite seleccionar el primer elemento mediante selectores de css, se puede definir #id, .clase, [atributo], etc.*

obtener una lista de nodos por querySelectorAll:

                document.querySelectorAll('#id');


## setAttribute("atributo a cambiar", "nuevo valor de atributo") : permite definir atributos de los elementos html.
    
                const input = document.querySelector('.form__input');
                input.setAttribute("type","text")

## getAttribute("atributo") : permite obtener atributos de los elementos html.
    .getAttribute; //esto devuelve el valor del atributo "type";

## removeAttribute("atributo"): directamente esto elimina el atributo del elemento html.


ATRIBUTOS GLOBALES (TODOS LOS ELEMENTOS TIENEN ESTOS ATRIBUTOS)-------------------------------------

- contenteditable (booleano) : indica si el elemento puede ser modificable por el usuario.

- style:

- tabIndex: permite definir con qué orden se seleccionan las etiquetas con la tecla TAB

- title: atributo que define un titulo al elemento seleccionado.


ATRIBUTOS INPUTS-----------------------------------------------------------------------------------






# Metodos del DOM para agregar elementos desde JS.

> https://lenguajejs.com/javascript/dom/insertar-elementos-dom/
>
> 


            
