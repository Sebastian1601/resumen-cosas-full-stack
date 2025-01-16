# HTML de W3Schools

https://www.w3schools.com/html/html_quotation_elements.asp

Formatting text elements

        <b> - Bold text
        <strong> - Important text
        <i> - Italic text
        <em> - Emphasized text
        <mark> - Marked text
        <small> - Smaller text
        <del> - Deleted text
        <ins> - Inserted text
        <sub> - Subscript text
        <sup> - Superscript text                
        <code> - se utiliza para indicar que el texto dentro, es un codigo que puede ser computable. (se suele utilizar dentro de una etiqueta <pre>)
        <kbd> - esto define un texto con formato monospace, se usa para formatear como teclas el codigo ingresado.
        <samp> - esto define que el texto dentro, puede ser resultado de salida de un programa de computadoras.

# quotations

    <blockquote cite="http://www.worldwildlife.org/who/index.html">
        texto
    </blockquote>

# abreviaciones

        <abbr> texto </abbr>

        <p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p> 

# información sobre autor/propietario de un documento o artículo

        <address>
            Written by John Doe.<br>
            Visit us at:<br>
            Example.com<br>
            Box 564, Disneyland<br>
            USA
        </address> 

# The HTML <cite> tag defines the title of a creative work (e.g. a book, a poem, a song, a movie, a painting, a sculpture, etc.).


         <p><cite>The Scream</cite> by Edvard Munch. Painted in 1893.</p> 


# The HTML <bdo> tag is used to override the current text direction:

         <bdo dir="rtl">This text will be written from right to left</bdo> 


# COMENTARIOS en html 
        <!-- Write your comments here -->  (se puede usar multilinea)



# VINCULAR CSS EXTERNO, ICONOS O SCRIPTS PARA EL HTML -------------------------------------------------------
    CSS --
        <head>
        ...
          <link rel="stylesheet" href="styles.css">
        ...
        </head>


    ICONOS --

         <link rel="icon" type="image/x-icon" href="/images/favicon.ico">

    SCRIPTS --

        
        <script src="myscript.js">


# VINCULOS ---------------------------------------------------------------------------------------------------

     <a href="https://www.w3schools.com/" target="_blank">Visit W3Schools!</a> 

    atributos:
            *href=" dirección web a vincular / mailto: [dirección de mail para enviar correo] / #(id del elemento a enfocar con el vínculo)"

            *target=" _self / _blank / _parent / _top "
            *title=" [texto que apaercerá cuando se pose el mouse sobre el vínculo] " 
            *download=" [especifica qué archivo se descargará al clickear el vinculo] "

            *accesskey / class / contenteditable / data-* / dir / draggable / enterkeyhint /
            hidden / id / inert / inputmode / lang / popover / spellcheck / style / tabindex / title / translate.

# ATRIBUTOS de EVENTOS HTML
            *onafterprint="funcion()" script que se corre luego de que se imprime el documento.

            *onbeforeprint="funcion()" script que se corre antes de que se imprime el documento.

            *onbeforeunload="func()"  script que se corre antes de que el documento sea descargado.

            *onerror="func()"        script que se corre cuando se registra un error.

            *onhaschange="func()"    script que se corre cuando se registran cambios en la paret de vinculo de la url.
        
            *onload="func()"         script que se corre una vez el documento ha sido cargado. ej <body onload="func ()">
                tags supported : <body>, <frame>, <frameset>, <iframe>, <img>, <input type="image">, <link>, <script> and <style>

            *onresize="func()"       script que se corre cuando se detecta el resize de la ventana actual.


# IMAGENES -------------------------------------------------------------------------------------------------------

        <img src=" (ruta o dirección web de la imágen.ext) " alt=" (texto a mostrar si la imágen no carga) ">

                *loading=" eager / lazy "  *define si se carga inmediatamente o si se espera hasta que ciertas condiciones se cumplan.

        <picture> contenedor que define el uso de varias imágenes </picture>


## definir un mapa dentro de una imágen para que sea vínculo

        <img src="(imágen a usar)" alt="(texto alternativo)" usemap="#workmap">

        <map name="workmap">
          <area shape="rect" coords="34,44,270,350" alt="Computer" href="computer.htm">
          <area shape="rect" coords="x1,y1,x2,y2" alt="Phone" href="(vinculo a donde dirigir)">
          <area shape="circle" coords="337,300,44" alt="Coffee" href="coffee.htm">
        </map> 

                shape="       "
                        rect - defines a rectangular region (se define poniendo coordenadas para formar el 
                                cuadrado desde la parte superior izquierda, hacia la parte inferior derecha)
                        circle - defines a circular region (se define posicionando la coordenada del centro
                                del circulo, y luego definiendo el RADIO(distancia del centro al extremo))
                        poly - defines a polygonal region (se define marcando todos los pares de coordenadas 
                                de la forma que se quiere definir)
                        default - defines the entire region

##definir varias imágenes a mostrar según una regla de ancho de la página.

        <picture>
              <source media="(min-width: 650px)" srcset="img_food.jpg">
              <source media="(min-width: 465px)" srcset="img_car.jpg">
              <img src="img_girl.jpg">
        </picture> 

# TABLAS EN HTML ----------------------------------------------------------------------------------------------


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


# LISTAS definidas y no definidas

las listas se suelen usar mucho para crear barras de navegación.
##lista no ordenada
     
    <ul> (unordered list)
        <li> Coffe </li> (list item)
        <li> Tea </li>
        <li> milk </li>
    </ul>

en css se define el stilo del marcador de cada item
    list-style-type: disc / circle / square / none

## lista ordenada

    <ol>
        <li> uno </li>
        <li> dos </li>
        <li> tres </li>
    </ol>

    ATRIBUTOS:
    *reversed
    *star="x" define el nro inicial de una lista ordenada
    *type="(1/A/a/I/i)"


## lista de definición

    <dl>
        <dt> cafe </dt>
            <dd> liquido negro caliente </dd>
    </dl>



# IFRAMES -----------------------------------------------------------------------------------------------------

se utiliza para ubicar un documento dentro del documento html.

        <iframe src=" (ruta del archivo o página) " title= " (descripcion breve) "> </iframe>



se puede usar un Iframe para abrir un vínculo que tengas definido en la página principal.
agregando el atributo name al iframe, y targeteando al name en el <a>

ej:
         <iframe src="demo_iframe.htm" name="iframe_a" title="Iframe Example"></iframe>

         <p><a href="https://www.w3schools.com" target="iframe_a">W3Schools.com</a></p> 




# LA ETIQUETA META


The <meta> element is typically used to specify the character set, page description, keywords, author of the document, and viewport settings.

The metadata will not be displayed on the page, but is used by browsers (how to display content or reload page), by search engines (keywords), and other web services.
Examples:

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


# FORMULARIOS ----------------------------------------------------------------------------------------------------------


existe una etiquea especial para crear formularios

        <form>

        </form>











































