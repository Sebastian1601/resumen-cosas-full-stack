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



## Operador OR ||

> Evaluación de valores "truthy" y "falsy":

> En JavaScript, ciertos valores son considerados "truthy" (verdaderos) o "falsy" (falsos). Algunos ejemplos de valores "falsy" son:
* false
* 0
* "" (cadena vacía)
* null
* undefined
* NaN (Not-A-Number)

Cualquier valor distinto de los mencionados arriba se considera "truthy".
Comportamiento del operador:

El operador || evalúa de izquierda a derecha.
Devuelve el primer valor "truthy" que encuentre.
Si no encuentra ningún valor "truthy", devuelve el último valor evaluado.

    ej:
    const nombre = "";
    const saludo = nombre || 'usuario anónimo' ;

    console.log(saludo) // ESTO SERA IGUAL A 'usuario anónimo' ;

## Operador de Coalescencia Nula (??)

> El operador de coalescencia nula (??) se utiliza para asignar un valor por defecto cuando una variable o expresión es _null_ o _undefined_. Es útil cuando deseas asegurarte de que un valor no sea nulo ni indefinido, pero quieres permitir otros valores como 0, false, o una cadena vacía.

    ej:
    const nombre = null; // TENER EN CUENTA QUE FIGURA NULL, no es lo mismo que "".
    const saludo = nombre ?? "Anónimo"; 
    console.log(saludo);  // "Anónimo"



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


## OBJETOS EN JS.

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


## OBJETOS | CLASES

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


## OBJETOS | CLASES | Metodos




### OBJETOS metodo protoype

Cuando ya tenemos creado una clase u objeto instanciado, o varios, y queremos agregarle una propiedad para que todos los objetos ya instanciados la tengan disponible, podemos usar el método  _prototype_ 

Usando la clase Perro definida arriba, podemos agregarle una propiedad a todos por igual, por ejemplo, "cantidadPatas".

esto se hace mediante el metodo prototype, de la siguiente manera:

        Perro.prototype.cantidadPatas = 4

Esto genera que si ya tenemos instanciada a "Estrellita" y "Lola", los objetos Estrellita y Lola tenga las propiedades nombre, edad, color y cantidadPatas por igual.

Podemos también definir un método para todos los objetos por igual, de la misma manera:

        Perro.prototype.ladrar = function() {
            console.log(`mi nombre es ${this.nombre} y ladro asi! wau! wau!`);
        };

Esto generaría que al ejecutar el método en cada instancia de Estrellita y Lola, se pueda obtener el código:

        Estrellita.ladrar();   //mi nombre es Estrellita y ladro así! wau! wau! 
        Lola.ladrar();         //mi nombre es Lola y ladro así! wau! wau!
    
## String (PROPIEDADES Y MÉTODOS).
---
Cuando hablamos de una variable que posee información de texto, decimos
que su tipo de dato es String. Hay dos formas de crear una variable de texto:

con el método del objeto `var texto = new String('hola a todos');` o de manera literal (es la más utilizada): 
`var texto = 'Hola a todos';`

existen muchos métodos para strings dado que JavaScript fue diseñado en base a manejar cadenas de texto, por lo tanto, las posibilidades son muchas.

### Metodos de strings que crean una nueva STRING (los strings son inmutables, siempre se obtiene un nuevo string con los métodos)

| Propiedad ---------------- | Descripción -------------------------------------------------------|
|----------------------------|------------------------------------|
| .toString() | Convierte un integer en string para poder aplicar los métodos correspondientes |
| .length           | Devuelve el número de caracteres de la variable de tipo string en cuestión|
| .charAt(*index*)                | Devuelve el carácter en la posición *index* de la variable. |
| .at(posicion)    | Devuelve el caracter en la posición indicada / ACEPTA posicion negativa|
| .slice(*start*, *end*) | devuelve un nuevo string con el texto desde start hasta end(NO INCLUIDO) / Si se omite el 2do parámetro, se obtiene un nuevo string desde el start hasta el final / ACEPTA start y end negativo|
| .substr(*ini*, *len*) | Devuelve el subtexto generado desde la posición *ini*, hasta *ini* + (*len* - 1) / SI SE OMITE el 2do parámetro, se obtiene el resto del string desde *ini* / ACEPTA PARAMETRO NEGATIVO|
| .substring(*start*, *end*) | Devuelve el subtexto generado desde la posición *start*, hasta *end* / NO ACEPTA VALORES NEGATIVOS|
|  .concat(*str1*, *str2*,...,*strN*) | Devuelve una nueva cadena uniendo *str1*, a *str2*..., a *strN* |
| .toLowerCase () | Devuelve el string de la variable aplicada en minúsculas. |
| .toUpperCase () | Devuelve el string de la variable aplicada en mayúsculas. |
| .trim () | Devuelve el string de la variable aplicada sin espacios al principio y al final |
| .trimStart() | Devuelve el string sin los espacios en blanco desde el principio |
| .trimEnd() | Devuelve el string sin los espacions al final si es que los tiene |
| .padStart(*num*, *string*) | rellena un string con *string* para que contenga *num* cantidad de letras |
| .padEnd(*num*, *string*) | rellena un string con *string* para que contenga *num* cantidad de letras|
| .repeat(*nro de veces*) | devuelve una nueva cadena con el _string_ repetido *nro de veces* |
| .replace (*str*, **nuevastr**) | Reemplaza la primera iteración de *str* con *nuevastr*  / en caso de querer cambiar todas las iteraciones, se coloca en la expresión el flag **/g** y en caso de que se desee que sea case insensitive se coloca el flag **/i** _ej: text.replace(/MICROSOFT/gi,"W3Schools")_ |
| .replaceAll(*str*, **nuevaStr**) | Devuelve un string con todas las iteraciones **str** reemplazadas por **nuevaStr** / ACEPTA REG EXP con el flag /g |
| .split(*separador*, *cantidad de splits*=0) | este metodo puede convertir un string a array, usando separadores. Si el separador se omite, se crea un array con todo el string original en el elemento [0], si el separador es "", se crea un array con una letra por elemento / el valor cantidad determinar qué cantidad de splits se realizan |
| String.fromCharCode(*n1*,*n2*,*n3*,...,*nX*) | Devuelve un string creado de los valores unicode pasados como parámetros.|
| .match(*string or RegExp to search*) | devuelve un ARRAY con las coincidencias de comparar _string_ con la **expresion a buscar** / DEVUELVE NULL si no hay coincidencias|

---



### Metodos de String Booleanos

| Propiedad ---------------- | Descripción -------------------------------------------------------|
|----------------------------|------------------------------------|
| _string_.endsWith(**str**)  | devuelve true or false dependiendo si el _string_ evaluado termina con **str**|
| _string_.startsWith(**str**, *index*=0) | Devuelve true or false dependiendo si el _string_ inicia con **str** si el *index* = 0, o si contiene **str** exactamente desde el *index* especificado. |
| _string_.includes(**str**, *start*=0) | Devuelve true or false dependiendo si _string_ contiene **str** desde *start*|


---

### Metodos de String que devuelven indices

| Propiedad ---------------- | Descripción -------------------------------------------------------|
|----------------------------|------------------------------------|
|  .indexOf(**str**)    |  Devuelve la primera posición del texto *str* pero no puede evaluar una regExp|
|  .indexOf(**str**, from) | Devuelve la posición de *str*, partiendo desde el index *from* |
 | .lastIndexOf(**str**, *from*) | Devuelve la posición de *str*, pero indica la última posición encontrada desde *from* / devuelve -1 si no encuentra nada|
 | _string1_.localeCompare(_string2_) | Compara dos cadenas, devuelve -1, 0 si son iguales, 1 |
 | .search(**regExp**) | Devuelve el *index* al encontrar la primer coincidencia en la cadena con **regExp** / si se pasa un string se transforma a *regExp* / .match() devuelve un array de indices|
|
 
 

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



## OBJETO MATH ------
---
Math es un objeto que tiene propiedades y métodos para constantes y funciones matemáticas.

- Math.E
- Math.LN2
- Math.LN10
- Math.LOG2E
- Math.LOG10E
- Math.PI
- Math.SQRT1_2
- Math.SQRT2

### Los métodos más útiles para web.

| Método -----------| Descripción     |
|-------------------|--------|
| Math.abs(x) | Devuelve el valor absoluto de x |
| Math.sign(x) | Devuelve el signo del número: 1 positivo, -1 negativo |
| Math.exp(x)    | Exponenciación W. Devuelve el número *e* elevado a la *x* |
| Math.expm1(x)  |  Equivalente a Math.exp(x) - 1 |
| Math.max(*a*, *b*, *c*, ... , *n*)| Devuelve el número más grande de los indicados por parámetro.|
| Math.min(*a*, *b*, *c*, ... , *n*)| Devuelve el número más pequeño dentro de los indicados |
| Math.pow (*base*, *exp*) | Potenciación W. Devuelve el nro *base* elevado a *exp* |
| Math.sqrt(x) | Devuelve la raíz cuadrada W de *x* |
| Math.cbrt(x) | Devuelve la raíz cúbica W de *x* |



 ### *Math.random()*

 Este método del objeto Math, devuelve un nro aleatorio entre 0 y 1, con 16 decimales. Si queremos usarlo para obtener un nro al azar entre los límites *a* y *b* se puede hacer lo siguiente.

        let randomNro = Math.random() * (b-a);
        let nroFinal = Math.floor (randomNro) + a;

ej: si quiero un nro al azar entre 50 y 70(no incluido):

        let randomNro = Math.random() * (70 - 50);
        let nroFinal = Math.floor (randomNro) + 50;

### metodos similares a floor:

- Math.round(*x*) : Devuelve el redondeo de *X* (entero más cercano)
- Math.ceil (*x*) : Devuelve el redondeo superior de *X* (entero más alto)
- Math.floor (*x*) : Devuelve el redondeo inferior de *X* (entero más bajo)
- Math.fround (*x*) : Devuelve el redondeo de *X* (flotante con precisión simple)
- Math.trunc (*x*) : Devuelve **sólamente** la parte entera de *X*


## ARRAYS (vectores o arreglos)

Un array, también conocido como arreglo o vector, es una colección o agrupación de elementos en una misma variable.

Los elementos del array pueden ser datos de diferentes tipos. Sin embargo, algunos de los métodos que poseen sólo funcionarán correctamente en arrays que tengan todos sus elementos del mismo tipo.

Cada elemento dentro del array posee un índice, un valor que nos permite identificarlo. 
Pensábamos a las variables como una “caja”. De forma similar, podemos imaginar un array como los vagones de un tren, donde cada vagón posee un contenido y un orden. El índice es el orden y el contenido dentro
del vagón es el dato

Se suelen definir de manera literal:
ej:

    const arreglo1 = ['a', 'b', 'c', 'd', 'e'];

o vacío

    const arreglo2 = [];

con distintos elementos:

    const arreglo3 = ['a', 3434, true, {nombre:'juan', edad:21, nacionalidad:'argentina'}];
    
## ACCEDER A LOS ELEMENTOS DE UN ARRAY

Las posiciones de un array se numeran a partir de 0 (cero). Cuando usamos 
`arreglo1[0]`
estamos haciendo referencia a la posición 0 del arreglo cuyo contenido, en este caso, es la letra *“a”*:

Si coloráramos por ej.

`arreglo[7]`, esto daría *undefined* dado que nuestro arreglo, no tiene esa ubicación definida(no hay elemento en la pos 7).
---
### Metodo arreglo.*length*

   Este Metodo devuelve la cantidad de elementos que posee este arreglo en particular.

> Si necesitamos acceder al último elemento de un array donde no sabemos qué indice tiene, se puede usar:

        const arregloN = [1, 4, 334, 2323, ..., 3242354];
        consolelog (arregloN[arregloN.length - 1]);

> Normalmente el nro devuelto por .length, es mayor a 1 con respecto a las ubicaciones del arreglo, que comienzan por 0, por lo tanto, para acceder al último valor del arreglo, se obtiene la posición restándole 1 a la cantidad total de elementos.
---
## Metodos de ARRAYS

| --------Metodo--------| ------Descripción ------- |
|------------------------|--------------------------|
| .at(*index*) | devuelve el elemento contenido en el *index* del array / acepta *index* negativos|
| .push(*obj1*, *obj2*, ... , *objn*)| Añade uno o más elementos al final del arreglo. Devuelve el nuevo tamaño del arreglo.|
| .pop()        | Elimina y devuelve el último elemento del arreglo |
| .unshift(*obj1*, *obj2*,...,*objn*)|Añade uno o más elementos al inicio del arreglo. Devuelve el tamaño nuevo|
| .shift()    | Elimina y devuelve el primer elemento del arreglo|
| .concat (*array1*, *array2*, *array3*, ...,*arrayN*)| concatena los elementos de los arreglos pasados por parámetro|
| .copyWithin(*x*, *y*, *z*) | Copia en otro arreglo, en la posición *x*, los elementos desde el index *y*, hasta *z*|
| .indexOf(*obj*, *from*)| Devuelve la posición de la primera aparición de *obj* desde *from* |
| .lastIndexOf(*obj*, *from*) | Devuelve la posición de la última aparición de *obj* desde *from*|
| .slice (*inicio*,*final*) | Retorna una copia de un arreglo desde el indice de *inicio*, hasta el *final* - NO INCLUIDO-|
| .reverse () | Invierte el órden de los elementos en el arreglo.|
| .sort () | Ordena los elementos del array bajo un criterio de ordenación alfabética (no es muy recomendado con nros)|


### _Array_.splice(a, b, c)

El método splice se utiliza de varias maneras, dependiendo de qué parámetros le pasemos, puede simplemente agregar elementos al arreglo, borrar uno, varios e incluso borrar e insertar elementos.


> Si se borra algún elemento, el método devuelve un arreglo nuevo con los elementos eliminados.
> Si no se borra ningún elemento, devuelve un arreglo vacío.
> Si se borra un solo elemento, se devuelve un arreglo de un único elemento.


`.splice(*indice*,*cantidadborrar*,*elemagregar1*, *elemagregar2*,...)`

**indice**:
   - Si *indice* es negativo, la cuenta comienza desde el último elemento al primero.
   - Si *indice* es mayor a la cantidad de elementos, se agregarán solamente los elementos indicados
   - Si *indice* se omite, y .splice se pasa sin argumentos, no se borra nada.
**cantidad a borrar**:
  - cantidad de elementos a borrar desde *indice*.
  - el parámetro *infinity* es válido para borrar todos los elementos a partir de *inicio*.
**elemntos a agregar**:
    -los elementos a agregar desde *inicio*.
    -si no se especifica ningún elemento, .splice solo borra elementos.

### Array.from()
   -Convierte un array de elementos iterables, o objetos tipo-array

   `Array.from(array1, mapFn, thisArg)`

  -array1 :un objeto estilo-array o iterable a convertir en array

  -mapFn : una función a ejecutar en cada elemento del array. Si se pasa como parámetro, todo valor a agregar al array se evalua en la función indicada.
  -la función se evalua pasando *elemento* a procesar, e *index* de dicho elemento a procesar.
  
  - Valor a usar como `this` cuando se ejecute *mapFn*.
### Array.isArray(*array a evaluar*)
   -Evalua y devuelve *true* or *false* dependiento si el elemento evaluado es un array.


### Array(*n*)
  -Crea un array de *n* elementos vacíos.

### *nombrearray*.at(*index*) (acepta *index* negativos)
   -Esto devuelve el contenido de la posición *index*, de los elementos de *nombrearray* 

## Métodos de arrays con funciones.-

### _Array_.forEach (_callback_, _argumentos_); //puede devolver lo que se determine en la función o nada.

   Este método realiza la función _callback_ por cada elemento del array, y se le pueden pasar inclusive otros parámetrosc omo argumento.

ej:

    let array1 = ['carlos', 'juan', 'ernesto'];

    array1.forEach((x)=>{
        console.log('hola, mi nombre es ' + x);
    },parám1, parám2, ..., parámN);


### _Array_.every (_callback_, _argumentos_); //devuelve *true* o *false*

   Este método analiza si TODOS los elementos del _Array_ cumplen con la condición establecida en el _callback_. De cumplirse devuelve _true_, de encontrar un valor que no, ya se termina el análisis devolviendo _false_

ej:
    
    let array1 = ['Juan', 'ernesto', 'alfredo', 'laura'];
    
    array1.every((x)=>{
    x.length>=4})); 
    //devuelve true porque la longitud de cada elemento es igual o mayor a 4.

### _Array_.some (_callback_, _argumentos_);

  Este método analiza si AL MENOS UNO de los elementos del _Array_ cumplen con la condición establecida en el _callback_. De cumplirse devuelve _true_, de NO ENCONTRAR UNO que cumpla, devuelve _false_

  ej:

    let array1 = ['Juan', 'ernesto', 'alfredo', 'laura'];
    
    array1.some((x)=>{
    return x.length == 5
    });
    //devuelve true dado que 'laura' tiene 5 digitos de longitud


### _Array_.map (_callback_, _argumentos_);

   Este método construye un array nuevo, con cada resultado de evaluar cada elemento del array en el _callback_.
   
ej:
   
    let coordenadasX = [1, 7, 14, 19, 27, 41, 63]

    let coordenadasY = coordenadasX.map((elem)=>{
    return (elem * 5) + 1
    })
    //esro devuelve el array [ 6, 36, 71, 96, 136, 206, 316].

### _Array_.filter(_callback_, _argumentos_)

  El método filter() genera un nuevo array con los elementos que cumplen el filtro que genera evaluar cada elemento del array en el callback.
ej:

        let valores54 = [7, 35, 14 , 114, 16, 18, 28, 6652, 2281, 351, 1540, 11525, 5, 66580];

        let resultado54 = valores54.filter((x)=>{
        return x % 5 == 0;
        });

        console.log(resultado54);
        //esto devuelve el array resultado54 = [35, 1540, 11525, 5, 66580]

### _Array_.findIndex(_callback_, _argumentos_)

  El método findIndex devuelve la posición del elemento que cumple con la condición del _callback_.

ej:

    let words66 = ['pato', 'tero', 'califragilistico', 'enero', 'madre', 'boca', 'unico'];

    let resul66 = words66.findIndex((x)=>{
    return x.includes('ico');
    })
    //esto devuelve como resultado el valor 2 solamente, del index 2 de 'califragilistico'
    
### _Array_.find(_callback_, _argumentos_)

El método find, devuelve **EL PRIMER ELEMENTO** que cumple con la condición del _callback_.
ej:

    let valores79 = [7, 35, 14 , 114, 16, 18, 28, 4013, 2281, 351, 1540, 11525, 5, 66580];
    //aca buscamos qué valor tiene 4 digitos, pero hay que transformar a string para poder usar el length.
    let resul79 = valores79.find((valor)=>{
    let eval = valor.toString();
    return eval.length == 4 ;
    })
    console.log(valores79);
    console.log('el primer valor que tiene 4 digitos es : ' + resul79);
    //todo esto devuelve '4013'.

### _Array_.reduce(_callback_, _argumentos_)

El método .reduce() ejecuta el _callback_ con cada elemento de izq. a derecha del array, y acumula el resultado.


ej:

    let nrosNaturales = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

    let factorial = nrosNaturales.reduce((valor)=>{
    return (valor + 5) * 3;
    })

    console.log(factorial);
    //devuelve 167298;


### FOR IN con arrays.

- El método recorre las propiedades de un objeto, string o array.

> sintaxis
> for (let variable in objeto) {
>     bloque a ejecutar
> };

    let arreglo120 = ['P','r','u','e','b','a'];
    console.log(arreglo120);

    for (let index in arreglo120) {
    console.log(index);
    };

//let index define una variable que va a tomar cada indice del array.

    for (let index in arreglo120) {
    console.log(arreglo120[index]);
    };

//let index nuevamente toma cada indice, pero se utiliza en este caso para obtener el valor del array en ese index.

 ### FOR IN recorre también las propiedades de un objeto.
  de principio a fin, sin tener que indicar limites o cantidad de iteraciones.

let Persona1 = {
    nombre:'Ana',
    apellido:'Pax',
    edad:'25'
};

//esto muestra en consola solamente las propiedades del objeto Persona1

    for (let x in Persona1) {
    console.log(x);
    };

//sin embargo, se puede usar para acceder tanto a las propiedades como a los valores.
    
    for (let x in Persona1) {
    console.log('dato ' + x + ':' + Persona1[x]);
    };

FOR OF se utiliza para recorrer una cadena String o array proporcionando acceso directo a cada uno de los valores.


    let arreglo157 = ['Maria', 'Juan', 'Ernesto', 'Adriana'];

    for (let x of arreglo157){
    console.log(x);
    };


## LocalStorage y SessionStorage ---

Los objetos de almacenaje web localStorage y sessionStorage permiten guardar pares de clave/valor en el navegador.

Lo que es interesante sobre ellos es que los datos sobreviven a una recarga de página (en el caso de sessionStorage) y hasta un reinicio completo de navegador (en el caso de localStorage). Lo veremos en breve.

Ya tenemos cookies. ¿Por qué tener objetos adicionales?

Al contrario que las cookies, los objetos de almacenaje web no se envían al servidor en cada petición. Debido a esto, podemos almacenar mucha más información. La mayoría de los navegadores modernos permiten almacenar, como mínimo, 5 megabytes de datos y tienen opciones para configurar estos límites.
También diferente de las cookies es que el servidor no puede manipular los objetos de almacenaje via cabeceras HTTP, todo se hace via JavaScript.
El almacenaje está vinculado al orígen (al triplete dominio/protocolo/puerto). Esto significa que distintos protocolos o subdominios tienen distintos objetos de almacenaje, no pueden acceder a otros datos que no sean los suyos.

Ambos objetos de almacenaje proveen los mismos métodos y propiedades:

    setItem(clave, valor) – almacenar un par clave/valor.

    getItem(clave) – obtener el valor por medio de la clave.
    
    removeItem(clave) – eliminar la clave y su valor.
    
    clear() – borrar todo.
    
    key(índice) – obtener la clave de una posición dada.
    
    length – el número de ítems almacenados.















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

## Manejo del DOM ------------------------------------------------------------------------
Tipos de nodo:
    -Document: es el nodo raíz del cual se derivan el resto de nodos.

    -Element: son nodos definidos por etiquetas HTML ej: <div>, <p>, <span>, etc.

    -Text : el texto dentro de un nodo element se considera un nuevo nodo hijo del tipo "text"

    -Attribute: los atributos de las etiquetas definen nodos, pero en js lo vemos como información asociada al nodo.

    -Comment node: los nodos que definen comentarios.

## DOCUMENT - Metodos de seleccion de elementos:

    como son métodos, se aplican al nodo document.

obtener un nodo por id:
    
                document.getElementByID('id a seleccionar');

obtener nodos por nombre de etiqueta:

                document.getElementsByTagName('div'); //esto devuelve una coleccion HTML de elementos, donde se puede acceder a cada elemento por indice(como un array, pero sin ser un array)

obtener nodos por querySelector:

                document.querySelector('.clase'); *// esto permite seleccionar el primer elemento mediante selectores de css, se puede definir #id, .clase, [atributo], etc.*

obtener una lista de nodos por querySelectorAll:

                document.querySelectorAll('#id');

> ⚠️ LOS HTMLCollections no se recorren con un forEach, pero sí se pueden recorrer con un "for of" para mostrar el contenido(cada etiqueta obtenida) de cada elemento.


### setAttribute("atributo a cambiar", "nuevo valor de atributo") : permite definir atributos de los elementos html.
    
                const input = document.querySelector('.form__input');
                input.setAttribute("type","text")

### getAttribute("atributo") : permite obtener atributos de los elementos html.
    .getAttribute; //esto devuelve el valor del atributo "type";

### removeAttribute("atributo"): directamente esto elimina el atributo del elemento html.


## ATRIBUTOS GLOBALES (TODOS LOS ELEMENTOS TIENEN ESTOS ATRIBUTOS)----------------------------

- contenteditable (booleano) : indica si el elemento puede ser modificable por el usuario.

- dir : indica la dirección del texto.
 
- style: contiene declaraciones de estilos CSS para ser aplicadas al elemento.

- tabIndex: permite definir con qué orden se seleccionan las etiquetas con la tecla TAB

- title: atributo que define un titulo al elemento seleccionado.

- Hay muchos más...

### ATRIBUTOS directos de INPUTS ----------------------------------------------------------------

- className : esto devuelve la clase asignada al objeto.
- value : esto devuelve el valor ingresado en el objeto.
- type : esto puede modificar directamente el tipo de input.
- accept : esto si ponemos un input para insertar imágenes, determina qué tipo de imágenes son válidas.
- form : este atributo vincula a través del id del formulario, un input que esté fuera del FORM.
- minLength : determina la mínima cantidad de caracteres que debe tener un input para ser válido.
- placeholder : texto que va dentro del input y se borra al momento de escribir.
- required : determina si es necesario el campo y no puede estar vacío o sin selección.

### Atributo Style.(element.style)
   esto permite modificar "al vuelo" propiedades CSS de los elementos. se pueden cambiar todos, pero no es siempre igual.

  element._style_.color = "#91a";
  
  element._style_.backgroundColor = "#48d"; (aca normalmente sería 'background-color:"#48d", pero mediante JS se elimina el guion medio para transformar la propiedad en camelCase)

### ClassList y métodos de ClassList. ------------------------------------------------------------------------

Estos métodos permiten manejar las clases de manera dinámica, agregando, quitando clases, etc.(no cambia directamente las propiedades)

    Element.classList.(método)

- classList.add('clase a agregar') : esto le agrega la clase indicada entre () al elemento.

- classList.remove('clase a quitar') : esto elimina la clase indicada siempre que el elemento la tenga.

- classList.item(n) : este método devuelve la clase posición _n_, si es que el elemento tiene varias.

- classList.contains('nombre de clase') : Esto evalua si el elemento html contiene la clase indicada. Devuelve _TRUE_ o _FALSE_

- classList.toggle('nombre de la clase') : si la clase indicada está en el elemento, la casa, y si no la tiene, la agrega.

- classList.replace('clase a reemplazar', 'clase a agregar') : reemplaza una clase, por otra directamente.

  ### Creación de elementos en HTML.

 - element._textContent_ : devuelve todo lo que tiene de texto el elemento html, sin etiquetas.

 - element._innerHTML_ : devuelve todo el contenido interno del elemento, incluido código html dentro.

 - element._outerHTML_ : devuelve TODO el contenido del elemento, etiquetas externas, internas, texto, etc.
  
  
  
### Crear Elementos en JavaScript.

definimos una constante con el elemento, descripto TODO en mayúscula. ej:

    const Lista = document.createElement('LI');
    
esto crea la etiqueta <li></li> vacía. Por lo tanto, para agregarle texto debemos crear un '_text node_':

    const textDelItem = document.createTextNode('esto es el texto dentro de la etiqueta li');

finalmente, agregamos a **Lista**, el text node creado:

    Lista.innerHTML = textDelItem;

 > ...Pero esta no es la mejor manera de hacerlo, dado que el texto insertado, no está creado como un nodo HTML, y por lo tanto, no tiene las mismas propiedades que un elemento creado de la siguiente manera...


### Métodos Child.

siguiendo el ejemplo anterior para crear los elementos **Lista** y **textDelItem**, podemos agregar el texto a la etiqueta html escribiendo:

    Lista.appendChild(textDelItem);

A su vez, ya creado el elemento <li> con su texto interno, podemos "agregarlo" a otro contenedor padre, por ejemplo un <div>

    let divPadre = document.getElementByID('contenedor');
    divPadre.appendChild('Lista');

y esto devolvería una estructura de la siguiente manera en HTML:

    <div id="contenedor">
        <li>esto es el texto dentro de la eitqueta li</li>
    </div>


### el método para crear más de un elemento html y presentarlo

_document.createDocumentFragment();

Primero creamos una constante de la siguiente manera:

    const fragmento = document.createDocumentFragment(); 
esto crea un "fragmento de documento HTML", para ir agregando elementos a medida que los vamos creando, y cuando ya no se agregarán más(por lo menos en esta instancia) se sube al documento principal, el "fragmento" de html, para agregar varios elementos html en un paso.

ej:
    
    const contenedor = document.querySelector(".contenedor");
    const fragmento = document.createDocumentFragment();
    for (i=0; i<20; i++){
    const item = document.createElement("LI");
    item.innerHTML = "este es un item de la lista";
    fragmento.appendChild(item);
    }

    contenedor.appendChild(fragmento);

Y esto consume muchos menos recursos que hacerlo por separado.


---

### Obtener y modificar Childs.

siendo el ejemplo:

        <body>
            <div class="contenedor">
                <h2> un titulo comun </h2>
                <h4> un h4 comun </h4>
                <p> un simple párrafo </p>
            </div>
        <body>

-Este elemento DIV tiene 2 hijos, _h2_ y _p_ 

- _firstChild_ : Obtiene el primer hijo del contenedor padre.

      let contenedor = document.querySelector (".contenedor");
      const primerHijo = contenedor.firstChild

  esto devuelve el primer elemento luego del DIV, en este caso, va a dar #text dado que el espacio en el código se cuenta como elemento texto. Para esto hay una solución más adelante.

- _lastChild_ : Obtiene el último hijo del contenedor padre.

-  _firstElementChild : Con este método resolvemos el problema de los espacios como #text.
Esto devolvería correctamente el <h2> un titulo comun </h2> aunque haya espaciones e indentaciones en el código HTML.

- _lastElementChild_ : Obtiene el último elemento hijo del contenedor padre, sin tener en cuenta los espacios #text.

- _childNodes_ : devuelve TODOS los elementos hijos de un contenedor padre, incluidos tags html, y #texts siendo espacios vacíos.

-  _children_ : resuelve lo anterior, devolviendo solamente los hijos que son ELEMENTOS del contenedor padre, en este caso:

        let hijoselementos =
        <h2>un titulo comun</h2>
        <h4>un h4 comun</h4>
        <p>un simple parrafo</p>

  > _childNodes_ y _children_ NO SON ARRAYs, son NodeList, se pueden recorrer como un array, pero no se le pueden aplicar los métodos de array.

        console.log(hijoselementos[1]) = <h4>un h4 comun</h4>

> Se pueden recorrer con un forEach los nodelist.

ej:
        
        hijoselementos.forEach( (hijo) => {
            console.log(hijo);
            });

### replaceChild(), removeChild(), hasChildNodes

- Padre._replaceChild('elemento a agregar','elemento viejo a reemplazar')_ : reemplaza un nodo viejo ya existente con uno nuevo.

- Padre._removeChild('elemento hijo de padre a quitar del DOM')_ : quita el elemento hijo del padre del DOM.

- Padre._hasChildNodes()_ : Este método verifica si el Padre tiene hijos, devuelve _true_ o _false_ según corresponda. Hay que tener en cuenta que un #text node se cuenta como hijo.




### parentElement.

- _parentElement_ : Selecciona el ELEMENTO padre, del elemento del método.

ej:
siendo el html:

        <div>
            <h1> un titulo importante </h1>
            <h2 class="h2"> un titulo secundario </h2>
            <p> un párrafo común </p>
        </div>

podemos probar lo siguiente:
        
        const h2_antiguo = document.querySelector('.h2');
        console.log(h2_antiguo.parentElement); //esto devuelve <div></div>


### Siblings (hermanos, elementos en el mismo rango del DOM)

- elemento._nextElementSibling_ : devuelve el hermano ELEMENTO posterior en el DOM.

- elemento._previousElementSibling_ : devuelve el hermano ELEMENTO anterior en el DOM.
        
  Teniendo en cuenta el html anterior

      h2_antiguo.nextElementSibling; //esto devuelve <p>un párrafo común</p>

      h2_antiguo.previousElementSibling; //esto devuelve <h1> un titulo importante

Si no tiene hermano anterior, o posterior, devuelve _null_

### Closest()

- este método devuelve, aplicandolo a un elemento en un punto del DOM, el elemento más cercano indicado con selector CSS.






### Metodos del DOM para agregar elementos desde JS.

> https://lenguajejs.com/javascript/dom/insertar-elementos-dom/

---


            
