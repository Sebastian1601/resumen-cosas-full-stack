# HTML de W3Schools

https://www.w3schools.com/html/html_quotation_elements.asp

Formatting text elements

\<b\> - Bold text
\<strong\> - Important text
\<i\> - Italic text
\<em\> - Emphasized text
\<mark\> - Marked text
\<small\> - Smaller text
\<del\> - Deleted text
\<ins\> - Inserted text
\<sub\> - Subscript text
\<sup\> - Superscript text                
\<code\> - se utiliza para indicar que el texto dentro, es un codigo que puede ser computable. (se suele utilizar dentro de una etiqueta \<pre\>)
\<kbd\> - esto define un texto con formato monospace, se usa para formatear como teclas el codigo ingresado.
\<samp\> - esto define que el texto dentro, puede ser resultado de salida de un programa de computadoras.
# quotations

\<blockquote cite="http://www.worldwildlife.org/who/index.html">
   texto
\</blockquote\>

# abreviaciones
```js

<abbr> texto </abbr>

<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p> 
```

# información sobre autor/propietario de un documento o artículo

```js
<address>
         Written by John Doe.<br>
         Visit us at:<br>
         Example.com<br>
         Box 564, Disneyland<br>
         USA
</address> 
```

# The HTML \<cite\> tag defines the title of a creative work (e.g. a book, a poem, a song, a movie, a painting, a sculpture, etc.).


```js
<p><cite>The Scream</cite> by Edvard Munch. Painted in 1893.</p> 
```

# The HTML \<bdo\> tag is used to override the current text direction:

```js
<bdo dir="rtl">This text will be written from right to left</bdo> 
```

# COMENTARIOS en html 

```js
  <!-- Write your comments here -->  (se puede usar multilinea)
```

## VINCULAR archivos externos al HTML 

```js
<head>
    ...
    <link rel="stylesheet" href="styles.css">
    ...
</head>
```


 **ICONOS**
```js

<link rel="icon" type="image/x-icon" href="/images/favicon.ico">
```

**SCRIPTS**
```js
<script src="myscript.js">
```

## VINCULOS

```html
<a href="https://www.w3schools.com/" target="_blank" >Visit W3Schools! </a> 
```

**Atributos:**
*href*: 
- dirección web a vincular (www.google.com)/ mailto: [dirección de mail para enviar correo] 
- \#id del elemento a enfocar con el hipervínculo

*target*: `_self / _blank / _parent / _top`
*title*: texto que apaercerá cuando se pose el mouse sobre el vínculo 
*download*:  especifica qué archivo se descargará al clickear el vinculo

accesskey
class
contenteditable
data-* 
dir
draggable
enterkeyhint
hidden / id / inert / inputmode / lang / popover / spellcheck / style / tabindex / title / translate...

## ATRIBUTOS de EVENTOS HTML
`onafterprint = funcion()` 
script que se corre luego de que se imprime el documento.

`onbeforeprint = funcion()` 
script que se corre antes de que se imprime el documento.

`onbeforeunload = func()`
script que se corre antes de que el documento sea descargado.

`onerror = func()`
script que se corre cuando se registra un error.

`onhaschange = func()`
script que se corre cuando se registran cambios en la paret de vinculo de la url.
  
`onload = func()`
script que se corre una vez el documento ha sido cargado.

ejemplo:
```html
<body onload="func()">
```
  
## HTML tags que soportan eventos

| tag      | descripción       |     |
| -------- | ----------------- | --- |
| body     |                   |     |
| frame    |                   |     |
| frameset |                   |     |
| iframe   |                   |     |
| img      |                   |     |
| input    | sólo type="image" |     |
| link     |                   |     |
| script   |                   |     |
| style    |                   |     |

`onresize = func()`
script que se corre cuando se detecta el resize de la ventana actual.

## IMAGENES

`<img src = " (ruta o dirección web de la imágen.ext) " alt=" (texto a mostrar si la imágen no carga) ">`
esrtuctura básica de la etiqueta que representa una imágen en una página web html.

`loading=" eager / lazy`
define si se carga inmediatamente o si se espera hasta que ciertas condiciones se cumplan.`

`<picture>`
contenedor que define el uso de varias imágenes \<picture\>

### Definir un mapa dentro de una imágen para que sea vínculo

`<img src="(imágen a usar)" alt="(texto alternativo)" usemap="#workmap">`

```html
<map name="workmap">
    <area shape="rect" coords="34,44,270,350" alt="Computer"
    href="computer.htm">
    <area shape="rect" coords="x1,y1,x2,y2" alt="Phone" href="(vinculo a donde dirigir)">
    <area shape="circle" coords="337,300,44" alt="Coffee"
    href="coffee.htm">
</map> 
```

shape = [rect / circle / poly / default]
- *rect* : defines a rectangular region (se define poniendo coordenadas para formar el cuadrado desde la parte superior izquierda, hacia la parte inferior derecha)
- *circle* : defines a circular region (se define posicionando la coordenada del centro del circulo, y luego definiendo el RADIO(distancia del centro al extremo))
- *poly* : defines a polygonal region (se define marcando todos los pares de coordenadas de la forma que se quiere definir)
- *default* : defines the entire region

### Definir varias imágenes a mostrar según una regla de ancho de la página.

```html
<picture>
    <source media="(min-width: 650px)" srcset="img_food.jpg">
    <source media="(min-width: 465px)" srcset="img_car.jpg">
    <img src="img_girl.jpg">
</picture> 
```

## Tablas
Las tablas se generan definiendo la fila y dentro de esta, las celdas de datos una por una. luego la siguente fila, y asi.

     <table>
            <caption> Titulo de la tabla </caption>

          <tr> (esto define la fila de encabezado de la tabla)
            <th>Company</th>  (esto define la table header)
            <th>Contact</th>
            <th>Country</th>
          </tr>
          <tr>    (aqui se define la primer table row)
            <td>Alfreds Futterkiste</td> (aca se define la table datacell)
            <td>Maria Anders</td>
            <td>Germany</td>
          </tr>
          <tr>    (se define una nueva table row)
            <td>Centro comercial Moctezuma</td> 
            <td>Francisco Chang</td>
            <td>Mexico</td>
          </tr>
    </table> 


ejemplo de tabla con el header que ocupa 2 columnas:

     <table>
  <tr>
    <th colspan="2">Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table> 


## LISTAS definidas y no definidas

Ls listas se suelen usar mucho para crear barras de navegación. Permiten listar elementos u opciones determinando un orden implícito ya por definición.
### No ordenada
```html
<ul> (unordered list)
    <li> Coffe </li> (list item)
    <li> Tea </li>
    <li> milk </li>
</ul>
``` 

**css** define el estilo del marcador de cada item
 *list-style-type*: [disc / circle / square / none]

### lista ordenada

```html
<ol>
    <li> uno </li>
    <li> dos </li>
    <li> tres </li>
</ol>
```
  
ATRIBUTOS html:
*reversed*
*start="x"* define el nro inicial de una lista ordenada
*type="(1/A/a/I/i)"*

Ej: 
```html
<ol reversed start = "10" type = "A">
	<li> uno </li>
	<li> dos </li>
	<li> tres </li>
</ol>
```

### lista de definición

```html
<dl>
    <dt> cafe </dt>
    <dd> liquido negro caliente </dd>
</dl>
```

## IFRAMES 

se utiliza para ubicar un documento dentro del documento html.

```html
<iframe src=" (ruta del archivo o página) " title= " (descripcion breve) "> </iframe>
```

Se puede usar un Iframe para abrir un vínculo que tengas definido en la página principal.
Agregando el atributo name al iframe, y targeteando al name en el \<a\>

ej:
```html
<iframe src="demo_iframe.htm" name="iframe_a" title="Iframe Example">
</iframe>

<p>
	<a href="https://www.w3schools.com" target="iframe_a">W3Schools.com</a>
</p> 
```

## LA ETIQUETA META

La etiqueta <meta> normalmente se usa para especificar el conjunto de carácteres, descripción de la página, palabras claves, autor del documento, y especificaciones del viewport.

La metadata no será mostrada en la página, pero es usada por los navegadores (para por ej, indicar cómo se mostrará el contenido, o se recargará la página, etc.), por los motores de busquedas, y otros servicios de la web.
Ejemplos:

Define the character set used:
     <meta charset="UTF-8">

Define keywords for search engines:
     <meta name="keywords" content="HTML, CSS, JavaScript">

Define a description of your web page:
     <meta name="description" content="Free Web tutorials">

Define the author of a page:
     <meta name="author" content="John Doe">

Refresh document every 30 seconds:
    <meta http-equiv="refresh" content="30">

Setting the viewport to make your website look good on all devices:
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

## FORMULARIOS

existe una etiquea especial para crear formularios

        <form>

        </form>











































