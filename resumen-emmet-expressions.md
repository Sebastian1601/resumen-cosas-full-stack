# Emmet shorthands ---
> los shorthands Emmet se entienden como una manera de escribir código más resumida y con mayor rapidéz que escribir el código normal. Esto acelera el flujo de trabajo al diseñar páginas web.

referencias:
* https://docs.emmet.io/cheat-sheet/

* https://www.freecodecamp.org/espanol/news/untitled-11/


> Con Emmet se puede crear rápidamente una plantilla HTML ingresando el shorthand "!" en el inicio del archivo.

### ! : estructura de archivo HTML básica.
> Ingresando el símbolo `!` y presionando `enter` habilita la estructura inicial de un archivo HTML.


## Etiquetas básicas

Para crear etiquetas básicas HTMLs, simplemente se escribe su manera shorthand, y esto permite crear una etiqueta completa, cerrandola si es necesario, y posicionando el cursor dentro de la misma para agregar contenido si es necesario.

* `div` y luego `enter` o `h1` y `enter` creará dichas etiquetas y el cursor quedará activo para poder ingresar datos dentro de ellas.

* esto también funciona para `bq` creará un `<blockquote>`, `hdr` creará un `<header>`, `ftr` hará lo mismo con un `<footer>`, `btn` para un `button` y `sect` para una `<section>`.
  

## Clases .

Emmet usa la misma sintaxis para crear elementos con ciertas clases. Para definir una clase de un elemento que estamos creando, usamos la notación `[elemento].[clase]`

* ej: `div.wrapper` ---> `<div class="wrapper"> </div>`
* `h1.header.center` ---> `<h1 class="header center"></h1>` 
  


## ID's #

Los IDs se determinan combinando con el símbolo `#` y funcionan de una manera muy similar a las clases...aparte de que se pueden combinar las mismas en un mismo elemento.

* ej: `div#hero.wrapper` creará --->
* `<div id="hero" class="wrapper"></div>`


## Atributos de un elemento con []


Podemos especificar atributos de los elementos que estamos definiendo...

* `img[src="cat.jpg"][alt="a picture of a cat"]` creará lo siguiente --->
*  `<img src="cat.jpg" alt="a picture of a cat" />`
  

## INCLUIR CONTENIDO DENTRO DE UNA ETIQUETA (o varias) con las {}

Para agregar al vuelo, mientras vamos creando la estructura con Emmet contenido, lo encerramos dentro de llaves...

* `p{Esto es un párrafo}` creará --->
* `<p>Esto es un párrafo</p>`


## Etiquetas hermanas + e hijas >

Aparte de poder definir muchas de las propiedas de los elementos que estamos creando, podemos agregar al vuelo, etiquetas hermanas (en el mismo nivel de la que estamos creando) o hijas (un nivel más adentro en el DOM) de la siguiente manera.

* `sect + sect` creará --->
* `<section> </section> <section></section>`


* `ul > li` creará ---> 
* `<ul> <li> </li> </ul>`


## Escalar niveles con ^ al crear contenido

Aparte de poder crear hermanos e hijos de los elementos que vamos diseñando, también podemos crear elementos más arriba en niveles del DOM.

* `div + div > p > span > em ^ bq` creará la siguiente estructura --->

```
<div></div>
    <div> 
        <p><span></span><em></em></p>
        <blockquote></blockquote>
    </div>
```

## Agrupar etiquetas mediante paréntesis para evitar "escalar"

Si la estructura es muy completa, es posible que desee evitar el "escalado" y agrupar de manera más conveniente el código.

* `div > (header > ul > li > a) + footer > p` creará --->
  
  ```<div>
    <header>
        <ul>
            <li><a href=""></a></li>
        </ul>
    </header>
    <footer>
        <p></p>
    </footer>
    </div>
    ```

## Multiplicar la creación de elementos con  * y generar números automáticamente con $

Podemos generar múltiples etiquetas con el símbolo `*` y numerar elementos en secuencia usando el signo `$`

* `ul > li * 5` creará --->
 ``` 
  <ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
  ```

* `ul > li{ ITEM $ }*3` creará --->
```
<ul>
    <li>ITEM 1</li>
    <li>ITEM 2</li>
    <li>ITEM 3</li>
</ul>
```

* `ul > li { ITEM $$$}*5` creará --->
```
<ul>
    <li>ITEM 001</li>
    <li>ITEM 002</li>
    <li>ITEM 003</li>
    <li>ITEM 004</li>
    <li>ITEM 005</li>
</ul>
```
* Comenzar con un número específico la numeración...
`ul > li. item$ @ 3 *5` creará --->
```
<ul>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
    <li class="item6"></li>
    <li class="item7"></li>
</ul>
```

## Lorem Ipsum

El texto de "Lorem Ipsum" es un texto ficticio utilizado por los desarrolladores para representar datos en una página. Simplemente se escribe `lorem` y la cantidad de palabras que se desean tenga ese texto ficticio, por ej:
* `lorem10` generará un texto de 10 palabras aleatorias.



## Abreviaciones de HTML.


