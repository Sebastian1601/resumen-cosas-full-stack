Verificar 02:26:00 del video. Propiedad POSITION porque tiene datos sobre como cambia el estado de un elemento al cual se le cambia la propiedad.


* BACKGROUND (fondos de cajas)

shorthand BACKGROUND:(color) (image) (repeat) (attachment) (position)

	color: el color del fondo
	image: url(ruta de la imágen a usar)
	repeat: repite horizontal y verticalmente la imágen usada.
		repeat-x (la imágen se repite solo horizontalmente)
		repeat-y (la imágen se repite solo verticalmente)
		no-repeat (la imágen no se repite)
		space (la imágen se repite la mayor cantidad de veces sin recorte. se distribuye espacio vacío entre las 
  		mismas para evitar el corte.)
 		round (la imágen es repetida y ajustada o estirada para llenar los espacios vacíos)
		initial (setea la propiedad a valor inicial)
		inherit (hereda la propiedad de su elemento padre)

* BORDER (bordes de una caja)

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


* OBJECT-FIT : (ubicar imágenes en contenedores, no hay que darle ancho ni alto a la imágen para esto)
	contain: (busca ocupar lo más grande del contenedor, ancho o alto, manteniendo el ratio de la imágen y mostrando toda la imágen, aunque tenga que achicarse)

	cover: (mantiene el ratio y ocupa todo el contenedor, aunque se recorte tramos de la imágen)

	none: ()

	scale-down: (elige la mejor propiedad para ajustar la imágen)

* OBJECT-POSITION: (se puede definir en ejes X e Y la posición del objeto en la caja, aparte de predefinidos)
	
	left: 
	
	right:

	top:

	bottom:


* COLORS (colores)



* MEDIAQUERY (las mediaquerys se utilizan para el responsive design, creando cortes según resolución para cambiar propiedades de las cajas mediante el mismo CSS)

		@media only screen and (CONDICION según resolución) {

		bloque de contenido de cambios	
	
		}
	

VOY POR EL MINUTO 04.34.00 DEL VIDEO DE CSS.

PAUSA PARA APRENDER GIT.

*********************** GIT & GITHUB *******************************************


///////////////////////CONFIGURACION INICIAL////////////////////////////////////

existen distintos scopes de configuración, local, global, y system.

accedemos a las mismas con 
git config --(local/global/system)
			:local realiza cambios para ese repositorio en particular
			:global realiza cambios para todos los repos en ese equipo.
			:system realiza cambios para todo el sistema.

* limpiar consola git
	clear

* ver la lista de configuraciones globales
	git config --global --list

* configurando el nombre global de usuario en git
	git config --global user.name "Davidejemplo"

* configurando mail
	git config --global user.email "davidseba.giordano@gmail.com"


* Configurar el editor(visual studio code) para mensajes
	git config --global core.editor "code --wait"
					(visual studio code)  --(esto genera que se 

* confirmen los cambiso cuando se cierre el editor de codigos)

* configurar colores de interfaz
	git config --global color.ui true


** importante para evitar problemas a futuro con el texto (funciona solo en windows)
	git config --global core.autocrlf true (carriage return line feed)


info adicional

https://stackoverflow.com/questions/2517190/how-do-i-force-git-to-use-lf-instead-of-crlf-under-windows/13154031#13154031

////////////////// REPOS ////////////////////////////////////////////////////
* comandos basicos del shell

	cd (nombre entrar carpeta) 	: entrar a una carpeta.

	cd ../ 				:(volver para atrás un nivel en el directorio) (es lo mismo poner cd ..)

	mkdir (nombre de carpeta)	:(crea una carpeta en el directorio actual)

	rmdir (nombre de la carpeta)	:(borra una carpeta del directorio actual con el nombre)

	rm (nombre del archivo)		:(remueve el archivo indicado localmente)

	dir				:(lista contenido de directorio actual)

	ls				:(lista de archivos)

	ls -l				:(lista de archivos como lista efectiva)

	ls -lh				:(lista de archivos)

	touch (nombre de archivo.ext)	:(crear un archivo nuevo)

	cp (nombre del archivo a copiar) (nombre del directorio donde queremos copiarlo) :copia archivos

	mv (directorio del archivo/nombre de archivo.ext) (directorio a donde queremos mover el archivo) :mueve archivos

	rm -r (nombre de la carpeta a eliminar, junto con sus archivos) :(elimina archivos y carpetas todo junto) 

//////// Area de trabajo ---> Area de Staging ---> REPOSITORIO /////////////////

INICIALIZAR EL REPOSITORIO LOCAL----------------
	git init  (esto inicializa la carpeta como repositorio local)


* agregar archivos al area de STAGING
	git add .  (agrega TODOS los archivos de la carpeta al area de staging)

	git add (nombre del archivo uno por uno) ej git add index.html


* ver estado de la carpeta, commits, etc del repo. (muestra qué archivo se va a subir al repo)
	git status

* sacar archivo del area de STAGING
	git rm --cached (nombre del archivo)


/////////REALIZAR COMMIT ----------------------------------

	git commit -m "(mensaje de actualización en el commit)"  (-m permite agregar mensaje al commit)

	git commit (esto abre automáticamente el editor de texto configurado antes, para escribir en 	detalle los datos del commit)

* REALIZAR COMMIT -- Sin pasar por el área de STAGING --

	git commit -a 

* ELIMINAR UN ARCHIVO DEL REPO

	rm (archivo) se elimina el archivo.
	luego, se debe agregar la "eliminación del archivo" con git add (nombre de archivo o punto[git add .]) 
	finalmente se realiza el commit.
	git commit -m "(mensaje)" -a

* RESTAURAR UN ARCHIVO ELIMINADO LOCALMENTE DESDE EL REPO

	git restore (ruta/nombre del archivo.ext) :(esto restaura un archivo borrado localmente al punto
			de la última actualización que tuvo el mismo en el repo. si se hicieron cambios
			luego del commit y no se guardaron, no van a estar en el archivo restaurado)


* VOLVER ATRÁS EL ESTADO DE UN ARCHIVO, al último commit actualizado.(esto no funciona si hay cambios subidos al ÁREA DE STAGING)

	git checkout (ruta/archivo.ext) :(vuelve el estado del archivo al estado del último commit.
					Todo cambio posterior se descarta)


* VOLVER ATRÁS el estado de un archivo sin tener en cuenta si hay archivos en el área de staging

	git reset --hard


* CAMBIAR NOMBRE DE UN ARCHIVO

  	git mv (nombre del archivo actual.ext) (nuevo nombre.ext)

  





































