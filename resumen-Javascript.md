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

    `while (condicion a evaluar) {
    bloque a ejecutar mientras la condicion sea verdadera
    }`

### Es importante que la condición en algún momento sea falsa, para terminar el bucle, sino se produce un bucle infinito, deteniendo la ejecución del resto del código js.


# FOR (estructura de control definida - bucle finito)

Un bucle *for* depende de el valor de una variable, que automáticamente va incrementandose por lo tanto hay determinada cantidad de iteraciones del mismo.

    `for (let i=1 ; i <= 10; i++) {
    bloque de código a ejecutar mientras se cumple el 2do término de la condición
    }
    `




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


            
