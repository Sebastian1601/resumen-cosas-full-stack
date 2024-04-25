* BACKGROUND (fondos de cajas)

shorthand BACKGROUND:(color) (image) (repeat) (attachment) (position)

	color: el color del fondo
	image: url(ruta de la imágen a usar)
	repeat: repite horizontal y verticalmente la imágen usada.
		repeat-x (la imágen se repite solo horizontalmente)
		repeat-y (la imágen se repite solo verticalmente)
		no-repeat (la imágen no se repite)
		space (la imágen se repite la mayor cantidad de veces sin recorte. 		       se distribuye espacio vacío entre las mismas para evitar el 		       corte.)
 		round (la imágen es repetida y ajustada o estirada para llenar los 			espacios vacíos)
		initial (setea la propiedad a valor inicial)
		inherit (hereda la propiedad de su elemento padre)

* BORDER (bordes de una caja)

shorthand BORDER: (border-width) (border-style)[requerido siempre] (border-color)
///////el shorthand no soporta definicion de más de un border width, style, color.//////////

	border-width: ancho del borde a marcar.(se define borde TOP, RIGHT, BOTTOM 			y LEFT) (de definir 2 bordes, se toma TOP/BOTTOM, 				LEFT/RIGHT por cada valor.)

	border-style: estilo del borde a marcar
		Se pueden definir los 4 bordes individualmente(border-top-style / 			border-right-style, border-bottom-style, border-left-style)
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
	 ambas clases dan la posibilidad de "insertar" elementos antes y después 	 del elemento de la selección, pero no forman parte del DOM como  	  	 cualquier otro.
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






































