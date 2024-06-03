alt + 60 = <
alt + 62 = >

alt + 91 = [
alt + 93 = ]

alt + 40 = (
alt + 41 = )

alt + 35 = #

alt + 92 = \ (barra invertida)
alt + 96 = ` (backticks)
alt + 126 = ~

alt + 64 = @

alt + 32 =  (espacio vacío)

*Verificar 02:26:00 del video de CSS. Propiedad POSITION porque tiene datos sobre como cambia el estado de un elemento al cual se le cambia la propiedad.

*Ver la parte de Modificar y deshacer commits nuevamente, del video curso de GIT desde CERO
*Ver GITPULL y GITFETCH

# MARKDOWN CHEATSHEET
==Basic Syntax==

| titulo | descripcion |
|  :---:  |  :---:   |
|Element |	Markdown Syntax|
|Heading |	# H1 <br>## H2 <br> ### H3 |
|Bold 	 |	**bold text** |
|Italic	  |	*italicized text* |
|Blockquote 	| > blockquote |
|Ordered List 	|1. First item <br> 2. Second item <br> 3. Third item |
|Unordered List |- First item <br>- Second item <br> - Third item|
|Code 		|  `code`  |
|Horizontal Rule |	---  |
|Link 	| [title](https://www.example.com) |
|Image |	![alt text](image.jpg) |

==Extended Syntax==

These elements extend the basic syntax by adding additional features. Not all Markdown applications support these elements.
Element 	Markdown Syntax
		Table 	| Syntax | Description |
			| ----------- | ----------- |
			| Header | Title |
			| Paragraph | Text |
Fenced Code Block 	```
			{
			  "firstName": "John",
			  "lastName": "Smith",
 			 "age": 25
			}
			```
Footnote 	         Here's a sentence with a footnote. [^1]
		        [^1]: This is the footnote.

Heading ID 	        ### My Great Heading {#custom-id}
Definition List 	term
			: definition
Strikethrough 		~~The world is flat.~~
Task List 		- [x] Write the press release
			- [ ] Update the website
			- [ ] Contact the media
Emoji
(see also Copying and Pasting Emoji) 	That is so funny! :joy:
Highlight 	        I need to highlight these ==very important words==.
Subscript 		H~2~O
Superscript 		X^2^ 

>:warning: <b>IMPORTANT!:</b> #CSS desde aqui ---

* <mark> BACKGROUND </mark> (fondos de cajas)

 ```
shorthand BACKGROUND:(color) (image) (repeat) (attachment) (position)
```

```
color:  *el color del fondo*
image:  *url(ruta de la imágen a usar)*
repeat: *repite horizontal y verticalmente la imágen usada.*
  	*repeat-x (la imágen se repite solo horizontalmente)*	
 	*repeat-y (la imágen se repite solo verticalmente)*
	*no-repeat (la imágen no se repite)*
	*space (la imágen se repite la mayor cantidad de veces sin recorte. se distribuye espacio vacío entre las mismas para evitar el corte.)*
 	*round (la imágen es repetida y ajustada o estirada para llenar los espacios vacíos)*
	*initial (setea la propiedad a valor inicial)*
	*inherit (hereda la propiedad de su elemento padre)*
```


 **BORDER** (bordes de una caja)

shorthand BORDER: (border-width) (border-style)[requerido siempre] (border-color)
///////el shorthand no soporta definicion de más de un border width, style, color.//////////

	border-width: ancho del borde a marcar.(se define borde TOP, RIGHT, BOTTOM y LEFT) (de definir 2 bordes, se toma TOP/
 	BOTTOM, LEFT/RIGHT por cada valor.)

	border-style: estilo del borde a marcar
		Se pueden definir los 4 bordes individualmente(border-top-style / border-right-style, border-bottom-style,
  		border-left-style)
		dotted:	borde de puntos
		dashed:	borde de lineas
		solid: 	borde solido de una linea
		double:	borde solido de dos lineas
		groove:	define un borde 3d, el efecto depende de los colores
		ridge:	define un borde 3d, el efecto depende de los colores
		inset:	define un borde 3d, el efecto depende de los colores
		outset:	define un borde 3d...
		none:	define SIN borde el elemento
		hidden:	define un borde OCULTO.

	border-color: se define el color de cada borde, como el width, se toma 				color TOP, RIGHT, BOTTOM, LEFT si se definen 4 colores, y 				si se definen 2 se toma TOP/BOTTOM, LEFT/RIGHT
	
	border-radius: estilo redondeado de los bordes, definido en pixeles.

	




*  ACCENT-COLOR : le da color a inputs de tipo checkbox / radio / range y progress
	
* MARGIN (margen externo entre la caja y otra caja o elemento)

	margin top
	
	margin right

	margin bottom

	margin left

	shorthand:
		margin:(top) (right) (bottom) (left)		

	Margin Collapse: Si tenemos màrgenes entre la parte superior e inferior de una caja, y hay 2 margenes que deberìan 		sumarse, ambos colapsan para que se aplique el mayor de los 2 solamente, no se suman.

* PADDING (espacio interior entre el margen de un elemento y su contenido)

	padding-top:
	
	padding-right:

	padding-bottom:

	padding-left:

	shorthand:
		padding: (top) (right) (bottom) (left)


* HEIGHT & WIDTH (alto y ancho de un elemento)

	max-width: determina el ancho máximo que debería tomar la caja, aunque se amplíe el espacio disponible.

	min-width: determina el ancho mínimo que puede tomar la caja, al llegar al mínimo no se achica más.

	
* OUTLINE (resaltador de caja que no ocupa lugar en el DOM)

	outline-style: (REQUERIDO)
		dotted:	borde de puntos
		dashed:	borde de lineas
		solid: 	borde solido de una linea
		double:	borde solido de dos lineas
		groove:	define un borde 3d, el efecto depende de los colores
		ridge:	define un borde 3d, el efecto depende de los colores
		inset:	define un borde 3d, el efecto depende de los colores
		outset:	define un borde 3d...
		none:	define SIN borde el elemento
		hidden:	define un borde OCULTO.

	outline-color:

	outline-width:
		thin (1px)
		medium (3px)
		thick (5px)
		un ancho específico(px, pt, cm, em, etc)

	outline-offset: (distancia entre la caja y el outline)

	shorthand  outline: (width) (style) (color)


* TEXT
	text-color: (color del texto)

	text-align: (se determina la alineación horizontal del texto)
		left: (texto alineado a la izquierda)
		center: (texto centrado)
		right: (texto alineado a la derecha)
		justify: (justifica el texto para que ocupe todo el ancho disponible)
	 	
	text-align-last: (especificar como se alinea la última linea del párrafo)
		right: (texto a la derecha)
		center: (texto centrado)
		justify: (justificado)

	direction: (determina la dirección del texto escrito)
		rtl: (derecha a izquierda)
		unicode-bidi:bidi-override

	vertical-align: (determina la alineación vertical)
		baseline: (por defecto)
		text-top: (sobre la linea del texto)
		text-bottom: (debajo de la linea del texto)
		sub: (debajo de la linea del texto)
		super: (por sobre la linea del texto)

	text-decoration-line: (agrega una linea decoradora de texto)
		overline: (agrega una linea sobre el texto)
		line-through: (agrega una linea en medio del texto)
		underline: (agrega una linea debajo del texto)
		overline underline: (lineas sobre y debajo del texto)

	text-decoration-color: (color de la linea de subrayado suprayado, etc)

	text-decoration-style: (estilo de la linea de subrayado suprayado)
		solid: 
		double:
		dotted:
		dashed:
		wavy:

	text-decoration-thickness: (ancho de la linea subrayado o suprayado)
	
	shorthand text-decoration: (line{requerido}) (color) (style) (thickness)

	TEXT-DECORATION: NONE (remueve todo agregado al texto, como el subrayado de
				los hipervínculos)

	text-transformation: (cambio en el texto)
		uppercase: (cambia todo a mayúsculas)
		lowercase: (cambia texto a minúsculas)
		capitalize: (cambia inicial a mayúscula)

	text-indent: [px/em/rem/cm/pt] (sangría del texto)

	letter-spacing: [px/em/rem/cm/pt] (espacio entre los caractéres de un párrafo)
	
	line-height: [px/em/rem/cm/pt] (espacio entre cada renglón de un párrafo)
	
	word-spacing: [px/em/rem/cm/pt] (espacio entre las palabras de un párrafo)

	white-space: (determina si el texto se ajusta a la pantalla o no)
		wrap: (el texto se ajusta)
		nowrap: (el texto no se ajustará, creando barras de desplazamiento)

	text-shadow: (especifica una sombra al texto[se pueden agregar varias, separads con coma])
		   : (horizontal shadow) (vertical shadow) (blur effect) (color)
		   : [px/em/rem/cm/pt]
	  ejemplo  : 5px 10px 3px red, 10px 20px 5px blue	


		





* DISPLAY: 
	Inline no se le puede dar tamaño a la caja contenedora.

	Inline block: si se le puede dar tamaño, pero posisionandose como inline, una caja al lado de la siguiente.

	Block: se compportan como elemeno en bloque (uno debajo de otro y se le puede brindar parámetros de tamaño).




* OVERFLOW: (solo funciona con elementos en bloque con altura definida)
	Visible: contenido no se altera y se sale de la caja
	
	Hidden: el contenido se oculta si es que se saldría de las dimensiones de la caja.
	Scroll: el contenido se "corta" para ajustarse a la caja, y se agrega una barra de desplazamiento para ver el resto.

	Auto: si es necesario agregar barras de desplazamiento porque el contenido se saldría de la caja, se agregan sino no.

	se pueden definir por separado también.
	*OVERFLOW-X:
	*OVERFLOW-Y:



* FLOAT:
	Left: el elemento "flota" a la izquiera del contenedor padre.
	Right: el elemento "flota" a a derecha del contenedor padre.
	none: el elemento "no flota".

	"Luego de utilizar FLOAT, si queremos seguir con el flujo de la página,
	debemos utilizar la propiedad CLEAR, que especifica qué sucede
	con el elemento siguiente luego de los elementos flotantes predefinidos".
* CLEAR:
	Left : 
	
	Right: 

	Both:

	"If a floated element is taller than the containing element, it will 	"overflow" outside of its container. We can then add a clearfix hack to 	solve this problem:"
	
	Hay que agregar esta clase en CSS al CONTENEDOR de los elemenos que estan 	flotados y se salen del tamaño del contendor:

	.clearfix::after {
 	 content: "";
  	clear: both;
  	display: table;
	}


* PSEUDO ELEMENTOS:
	Ambos funcionan si el elemento al que hacen referencia tiene display block ó inline-block.
	
	pseudoclase ::first-letter : selección de la primera letra de un texto.

	 características a aplicar a ::first-letter--------------------------
  	  font properties
   	  color properties 
  	  background properties
  	  margin properties
  	  padding properties
 	  border properties
 	  text-decoration
 	  vertical-align (only if "float" is "none")
 	  text-transform
	  line-height
	  float
 	  clear

	
	pseudoclase ::first-line : selección del primer renglón de un párrafo.
	 características a aplicar a ::first-line----------------------------- 	
 	  font properties
   	  color properties
   	  background properties
  	  word-spacing
  	  letter-spacing
  	  text-decoration
  	  vertical-align
  	  text-transform
  	  line-height
  	  clear


	pseudoclase ::placeholder (exclusivamente para cambiar las propiedades del placeholder de un input)
	 características a aplicar(las mismas que cualquier texto posiblemente)

	pseudoclase ::selection (exclusivamente para selección de texto)
	

	pseudoclase ::before y ::after
	 	ambas clases dan la posibilidad de "insertar" elementos antes y después del elemento de la selección, pero no forman 			parte del DOM como cualquier otro.
	 	Llevan siempre la propiedad "content:"


* PSEUDO-CLASES: 

	:active (selecciona el elemento "activo", cuando se clickea el mismo)

	:checked (selecciona el elemento "chequeado". normalmente son inputs)
	
	:disabled (selecciona el elemento "desactivado")

	:empty (selecciona el elemento "vacio" que no tiene hijos)

	:enabled (selecciona el elemento "habilitado")

	:first-child (selecciona el 1er elemento hijo de su contenedor padre)	
	
	:first-of-type (selecciona el primer elemento del tipo indicado del contenedor padre)

	:focus (selecciona el elemento que tiene el "foco")

	:hover (selecciona el elemento al cual se le posa el mouse encima)

	:in-range (determina cambios al elemento dentro del rango, solo funciona en inputs donde se ingrese un rango min y max)

	:invalid (determina cambios al elemento con un valor inválido)

	:last-child (determina estilos de un ULTIMO elemento contenido por su padre)

	:link (determina estilo de todos los vinculos sin visitar)

	:not(x) (selecciona todos los elementos que no sean elemento x)

	:nth-child(n) (selecciona todo hijo de contenedor padre que cumpla con n (acepta funciones, ej. nth-child(2n-1)))

	:nth-last-child(n) (determina estilo al elemento que cumple con n desde el último)

	:nth-last-of-type(n) (selecciona todos los elementos que son los n elementos de su padre, contando desde el último hijo)

	:nth-of-type(n) (selecciona todos los elementos que son n elementos de su padre)


	:only-of-type (selecciona todo elemento que sea el único elemento de su padre)

	:only-child (selecciona todo elemento que sea único hijo de su contenedor)

	:optional (selecciona elementos generalmente inputs, que no tenga el atributo "requerido")

	:out-of-range (selecciona los elementos, generalmente inputs de rango, que estén fuera del rango establecido)

	:read-only (selecciona generalmente elementos input con el atributo "read-only")

	:read-write (selecciona generalmente inputs, sin el atributo "read-only")

	:required (selecciona elementos con el atributo "required")

	:root (selecciona el elemento root del documento)

	:target 	#news:target 	Selects the current active #news element 		(clicked on a URL containing that anchor name)

	:valid (selecciona elementos, generalmente inputs con un valor establecido Valido)

	:visited (selecciona generalmente vinculos ya visitados "a:visited" {})


* OBJECT-FIT : (se aplica directamente a las <IMG>) (ubicar imágenes en contenedores, no hay que darle ancho ni alto a la imágen para esto)
	contain: (busca ocupar lo más grande del contenedor, ancho o alto, manteniendo el ratio de la imágen y mostrando toda la imágen, aunque tenga que achicarse)

	cover: (mantiene el ratio y ocupa todo el contenedor, aunque se recorte tramos de la imágen)

	none: ()

	scale-down: (elige la mejor propiedad para ajustar la imágen)

* OBJECT-POSITION: (se puede definir en ejes X e Y la posición del objeto en la caja, aparte de predefinidos)
  	si definimos object-position: 0px 0px; esto genera que la imágen se alinee desde el borde superior izquierdo a la caja
  	contenedora
	
	:left :alinea la imágen desde el margen izquierdo al contenedor
	
	:right :alinea la imágen desde el margen derecho al contenedor

	:top :alinea la imágen desde el margen superior al contenedor

	:bottom :alinea la imágen desde el margen inferior al contenedor


* COLORS (colores)



* MEDIAQUERY (las mediaquerys se utilizan para el responsive design, creando cortes según resolución para cambiar propiedades de las cajas mediante el mismo CSS)

		@media only screen and (CONDICION según resolución) {

		bloque de contenido de cambios	
	
		}


# ---------------------- FLEX BOX -------------------

* Flexbos posee 2 ejes, el main axis y el cross axis. (esto depende de la orientación del contenedor flex.)


     -----------------------------------------------------------------
     |                           |cross-star                         |
     |                           |                                   |
     |main start                 |                           main end|
     |---------------------------------------------------------------|
     |                           |                                   |
     |                           |cross end                          |
     |                           |                                   |
     -----------------------------------------------------------------

*Al setear un contenedor con display:flex, todo contenedor hijo directo(exclusivamente) del mismo, se convierte en un flex item.

  ej:

  	<div CLASS="flex_container">
   		<p CLASS="flex_item"> lorem ipsum etc </p>
     		<img src="./img/img_prueba1.jpg" CLASS="flex_item">
       </div>

## PROPIEDADES DEL CONTENEDOR FLEX ------------------------------------------------

* Cambiar dirección del main axis (eje principal)

  		Flex-direction: row (por defecto)
  				column (vertical)
  				row-reverse (horizontal desde derecha a izquierda)
  				column-reverse (vertical desde abajo hacia arriba)

* Adaptar las filas o columnas para que al modificarse, se reubiquen
 
    		flex-wrap: wrap (al no tener espacio, se reubican las cajas en más filas inferiores)
  			   wrap-reverse (al no tener espacio, las cajas se ubican en más filas superiores)
  			   no-wrap (las cajas, van a seguir ocupando una unica fila auque no haya espacio en la pantalla por lo tanto se agrega un scroll horizontal)
* SHORTHAND:

  		flex-flow:[propiedad de flex-direction] [propiedad de flex-wrap]
    
* distribuir en el main axis los flex items:

		justify-content: flex-start (ubica a los flex items al inicio del contenedor flex) 
				 flex-end (ubica a los flex items al final del contenedor flex)
  				 center (ubicar en el centro los flex items sin espacio)
  				 space-around (le da un margin automatico entre cajas y limites del contenedor, todos iguales para usar todo el espacio)
  				 space-between (ubica los flex items con el mayor espacio posible entre ellos, sin margenes entre los limites)
  				 space-evenly (distribuye los flex-items con el mismo margin entre ellos y los limites del contenedor flex)
  				 

* distribuir en el cross axis los flex items cuando hay una sola fila de flex items en el contenedor:

		align-items: flex-start (ubica a los flex items al inicio del contenedor flex y si los items no tienen definido alto, se ajusta al contenido) 
			     flex-end (ubica a los flex items al final del contenedor flex y si los items no tienen definido alto, se ajusta al contenido)
  			     center (ubicar en el centro los flex items sin espacio y si los items no tienen definido alto, se ajusta al contenido)
			     stretch (por defecto)(si los items no tienen definido alto, los items se "estiran" para ocupar todo el alto del contenedor flex)
  			     baseline (ubica a los items, en la parte inferior del contenedor, junto si y solo si con la opción flex-wrap:wrap-reverse)

* distribuir en el cross axis los flex items cuando hay varias filas de flex items en el contenedor:

  		align-content: flex-start (ubica a los flex items al inicio del contenedor flex y si los items no tienen definido alto, se ajusta al contenido) 
			     flex-end (ubica a los flex items al final del contenedor flex y si los items no tienen definido alto, se ajusta al contenido)
  			     center (ubicar en el centro los flex items sin espacio y si los items no tienen definido alto, se ajusta al contenido)
			     stretch (por defecto)(si los items no tienen definido alto, los items se "estiran" para ocupar todo el alto del contenedor flex)
  			     baseline (ubica a los items, en la parte inferior del contenedor, junto si y solo si con la opción flex-wrap:wrap-reverse)

## PROPIEDADES DE LOS ITEMS FLEX ---------------------------------------------------

# EL MARGIN:AUTO EN EL ITEM FLEX FUNCIONA MUY DISTINTO, PERO CENTRA SI HAY UN ITEM SOLO EN EL CENTRO DEL CONTENEDOR. SI HAY MAS DE UN ITEM, LOS CENTRA SOLAMENTE EN EL CROSS AXIS

* ubicar en el cross axis el item en particular seleccionado:

  		align-self: flex-start (ubica al principio del cross axis el item)
   			    center (ubica en el cross axis al centro del contenedor)
  			    flex-end (ubica en el final del cross axis el item dentro del contenedor)

* determinar el orden en el eje flex principal de los items flex

  		order: (x, x E N)


* determinar el tamaño de las cajas para crecer con respecto al espacio vacío en el contenedor:

  		flex-grow: (x, x E N) (esta opción, colocada en el item flex, determina qué parte del espacio vacío
  				se lleva este item)

* determinar el espacio que cede la caja al achicarse con respecto a las demás.-

  		flex-shrink: (x, x E N)

* determinar el ancho inicial del item flex con más importancia que "width".

		flex-basis:200px;

# SHORTHAND : 

		flex: [flex-grow] [flex-shrink] [flex-basis];



# ------------------- GRID BOX -------------------------------------------------

## Grillas dinámicas

* Toda grilla tiene un contenedor.

  		Display:grid;


* Los Grid items, no necesariamente son cada celda de la grilla. Un grid Item puede ocupar varias grid cells.

* La cantidad de grid tracks se determina sumando las filas y las columnas.

* Grid area las definimos para maquetar la grilla.

## PROPIEDADES A APLICAR A LOS GRIDs CONTAINERs -------------------------------

* Determinar cuántas filas (rows) va a tener la grilla:
  
	  grid-template-rows: (tamaño de fila 1) (tamaño de fila 2) (tamaño de fila 3) ... (tamaño de fila 12);

* Determinar cuántas columnas (columns) va a tener la grilla:

  	  grid-template-columns: (tamaño de columna 1) (tamaño de columna 2) ... (tamaño de columna 12);

Unidades para definir filas y columnas: AUTO, Fr, (medidas fijas como px, em, rem, etc.)







 


















