alt + 60 = <
alt + 62 = >

alt + 91 = [
alt + 93 = ]

alt + 40 = (
alt + 41 = )

alt + 35 = #

alt + 92 = \ (barra invertida)

alt + 126 = ~

alt + 64 = @

alt + 32 =  (espacio vacío)

*Verificar 02:26:00 del video de CSS. Propiedad POSITION porque tiene datos sobre como cambia el estado de un elemento al cual se le cambia la propiedad.

*Ver la parte de Modificar y deshacer commits nuevamente, del video curso de GIT desde CERO
*Ver GITPULL y GITFETCH

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





# **************************** GIT & GITHUB ************************************


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
					(visual studio code)  --(esto genera que se confirmen los cambiso cuando se cierre
  					 el editor de codigos)

* configurar colores de interfaz
	git config --global color.ui true


** importante para evitar problemas a futuro con el texto (funciona solo en windows)
	git config --global core.autocrlf true (carriage return line feed)

* configurar para que la versiòn abreviada del hash de cada commit, sea de x dígitos (normalmente 10)
  	git config --global core.abbrev X


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


* agregar archivos al area de STAGINGrm
	git add .  (agrega TODOS los archivos de la carpeta al area de staging)

	git add (nombre del archivo uno por uno) ej git add index.html


* ver estado de la carpeta, commits, etc del repo. (muestra qué archivo se va a subir al repo)
	git status

* sacar archivo del area de STAGING
	git rm --cached (nombre del archivo)

 	git restore --staged (nombre del archivo EN EL area de staging que queremos SACAR)


/////////REALIZAR COMMIT ----------------------------------

	git commit -m "(mensaje de actualización en el commit)"  (-m permite agregar mensaje al commit)

	git commit (esto abre automáticamente el editor de texto configurado antes, para escribir en
 	detalle los datos del commit)

* REALIZAR COMMIT -- Sin pasar por el área de STAGING --

	git commit -a

* VER DATOS Y HASH DE LOS COMMITS

  	git log 

  	git log --oneline  :(muestra el log y los hash resumidos configurados de los commits)

	git log --oneline --all  :(muestra los commits de TODAS las ramas)

	git ls-tree -r --name-only (hash resumido del commit a ver) :(muestra lista de  archivos y carpetas en ese commit)
	git ls-tree -r --name-only HEAD (esto refiere al último commit disponible)

* ELIMINAR UN ARCHIVO DEL REPO

	rm (archivo)  :se elimina el archivo.
	luego, se debe agregar la "eliminación del archivo" con git add (nombre de archivo o punto[git add .]) 
	finalmente se realiza el commit.
	git commit -m "(mensaje)" -a

* RESTAURAR UN ARCHIVO ELIMINADO LOCALMENTE DESDE EL REPO

	git restore (ruta/nombre del archivo.ext) :(esto restaura un archivo borrado localmente al punto
			de la última actualización que tuvo el mismo en el repo. si se hicieron cambios
			luego del commit y no se guardaron, no van a estar en el archivo restaurado)


* VOLVER ATRÁS EL ESTADO DE UN ARCHIVO, al último commit actualizado(HEAD).(esto no funciona si hay cambios subidos al ÁREA DE STAGING)

	git checkout (ruta/archivo.ext) :(vuelve el estado del archivo al estado del último commit.
					Todo cambio posterior se descarta)
  	git checkout (hash de un commit anterior cualquiera) :(cambia al estado de los archivos en ese commit, pero es solamente
  							 para revision)

  	SI AL UTILIZAR GIT CHECKOUT, CREAMOS UNA RAMA DESDE ESE PUNTO, PODEMOS LLEVAR ESTE ESTADO A UNA RAMA "OFICIAL"
  	PARA SEGUIR TRABAJANDO DESE ESE PUNTO LOS ARCHIVOS.
  
	== SOLO SE UTILIZA LUEGO DE ver un commit anterior con GIT CHECKOUT y no queremos cambiar nada ==
	git switch - (vuelve el HEAD al último commit disponible del repo)

* VOLVER ATRÁS el estado de un archivo sin tener en cuenta si hay archivos en el área de staging
	======== SIEMPRE HAY QUE TENER LOS ARCHIVOS GUARDADOS ANTE UN RESET HARD =======
	git reset --hard (hash del commit a donde quiero volver el estado de todos los archivos)


* CAMBIAR NOMBRE DE UN ARCHIVO

  	git mv (nombre del archivo actual.ext) (nuevo nombre.ext)

* VERIFICAR CONTENIDO DE UN ARCHIVO ¡¡ YA GUARDADO !! EN EL REPOSITORIO LOCAL

  	git show (nombre del archivo.ext)

* COMPARAR ARCHIVOS EN EL REPO(ya commiteados) CON ARCHIVOS EN EL AREA DE STAGING (obviamente no se define el archivo en el comando sino subiendolos al área de staging) 

	git diff --staged

* COMPARAR DIFERENCIAS ENTRE 2 VERSIONES DE LOS COMMITS, DE ACUERDO A SU HASH

   	git diff (1er hash de commit de x dígitos) (2do hash de commit de x dígitos)

* COMPARAR SOLAMENTE CAMBIO DE NOMBRES EN LOS ARCHIVOS

  	git diff --name-only (1er hash de commit de x dígitos) (2do hash de commit de x dígitos)

* COMPARAR QUE SE CAMBIO ENTRE DOS COMMITS

  	git diff --word-diff (1er hash de commit de x dígitos) (2do hash de commit de x dígitos)


* CAMIAR DE MENSAJE EL ÚLTIMO COMMIT REALIZADO (y modificar el último commit)

  	git commit --amend

  	(en caso de necesitar modificar archivos en este ùltimo commit, se agregan al area de STAGING
  	y ahi luego de tener todo organizado en staging se realiza el comando indicado git commit --amend)

  
* DESHACER EL ULTIMO COMMIT (mover el HEAD al commit anterior, y mueve los archivos del ùltimo commit, al área de staging para
  				realizar cambios o eliminarlos, y si ha archivos ya en staging, se agregan todos juntos)

  	git reset --soft (hash de commit anterior al que queremos borrar de x digitos) :(no modifica archivos del área d trabajo)

   	git reset --soft head~1  (esto es lo mismo que pensar desde el commit head - 1 restarle uno)

  	git reset --mixed (hash de commit anterior al que queremos borrar de x digitos) (esto vuelve atràs sin dejar nada
  				 en el area de staging pero sin modificar el área de trabajo)

	*********** ANTES DE USAR GIT RESET HARD hay que guardar los archivos del area de trabajo sino darà error*************
  	***********LOS ARCHIVOS QUE SE USAN CON GIT RESET HARD no pueden ser guardados ***************************************

  	gir reset --hard (hash del commit del que quiero tener todos los archivos en el area de trabajo, pisando todo
  			lo que tenía)


  //////////// RAMAS o BRANCHES //////////////////////////////////////////////////////////////////////////////////////////////

  Tener en cuena que depende de en qué rama estemos posicionado, al crear una nueva rama, puede no ser del proyecto principal
 //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	git branch  (esto muestra todas las ramas activas y creadas del repo)

	git branch  (nombre de la rama)  :esto crea una rama(copia del estado actual) con el nombre indicado.

* cambiar a una rama:
	git checkout (nombre de la rama en la que se quiere trabajar) (ya no se suele utilizar)

	git switch (nombre de la rama en la que se quiere trabajar)

* Crear una rama y cambiar a esa inmediatamente:
	git switch -c (nomber de la rama a crear) 


* Eliminar ramas (ES IMPORTANTE QUE PARA ELIMINAR UNA RAMA, NO DEBEMOS ESTAR PARADOS EN ELLA)
  	git branch -d (nombre de la rama a borrar)

* Cambiar nombre de rama donde NO ESTAMOS PARADOS

  	git branch -m (nombre actual de la rama) (nombre nuevo de la rama)

* Cambiar nombre de la RAMA ACTUAL

  	git branch -m (nuevo nombre a colocar en la rama actual)

//////////////////////////////////////////////////////////////////////////// UNIR RAMAS (MERGE o FUSIONAR) ///////////////////

IMPORTANTE! para fusionar RAMA1 con RAMA2, debemos estar "parados" en la rama a la cual queremos "mantener". En este caso, debemos estar en RAMA1 y fusionar RAMA2 con RAMA1, para que los cambios se agreguen a RAMA1.

* FUSIONAR RAMAS:
	git merge (nombre de la rama a fusionar en la rama actual donde estamos parado)

* EN CASO DE HABERSE EQUIVOCADO:

  	git reset --hard (HASH del último commit de la rama principal antes de fusionar las ramas)
  								ESTO ELIMINA EL COMMIT DE FUSION DE LAS RAMAS pero
  								no la rama que se fusionó!
* EN EL CASO DE QUERER RECUPERAR UN COMMIT BORRADO CON RESET --HARD, si tenemos el HASH de referencia, podemos recuperarlo con

  	git reset --hard (HASH del commit borrado)


////////// CONFLICTOS DE FUSIONADO (MERGE) ////////////////////////////////////////////////////////////////////////////////////

Esto suele suceder cuando se trabaja en una rama, desde un punto B de la rama principal, y antes de fusionar la rama con el principal, se da que la rama principal tuvo modificaciones. 

			rama1 ---- rama1(2)
   		       /                   \
	    	      /                     \
	main------main(2) ----main(3)------ (main + rama1(2)) = Conflicto Posible

Abriendo el editor de Visual Studio Code permite seleccionar qué código va a quedar seleccionado y se realiza el commit 
desde ahi directamente.
Se pueden aceptar cambios de una rama, de otra, ambas, o seleccionando la opción más conveniente de cada una.

Caso contrario, se pone:
	git merge --continue   (esto finaliza con el commit del merging)

* VER la última actualización de cada rama
  	git branch -v

 //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

 .GITIGNORE 

 	esto define qué archivos GIT debe ignorar al momento de buscar para commitear. y solo funciona para archivos que
  	NUNCA se han guardado en un commit, si el archivo ya se subió

  se crea un archivo .gitignore

  se puede abrir con el VSC y se puede comentar dentro con el símbolo #(comentario)
  se agrega el [nombre.ext] del archivo a ignorar, pero se puede definir por rangos
  	ej: *.txt / *.jpg / *.py
   
*  para excepcionar un archivo dentro del grupo de archivos definidos por ej en *.txt, se pone
  ![nombre de archivo.txt]
  
*  Para ignorar un directorio completo se pone
	[nombre de carpeta]/

* CONFIGURAR QUE LOS REPOS LEAN UN ARCHIVO .GITIGNORE general:

  	git config --global core.excludesfile [ruta en la pc del archivo]
 	ej: git config --global core.excludesfile c:/generalfiles/.gitignore_global

  
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

ALIAS EN GIT
	(se definen como funciones que guardan todos los comandos determinados para ejecutar más simple)

 ej:
   git log --oneline --graph --all
  	
   	se puede resumir configurando lo siguiente: elijiendo el nombre del comando propio como logsimple

   git config --global alias.[nombre del comando propio] "log --oneline --graph --all"

    esto genera que al escribir c:>git logsimple 
    esto genere que se dispare el comando configurado anteriormente.

* Ver la lista de alias asignado:
  	 git config --global --list |grep alias

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

* GIT REFLOG
  	esto es un log de todos los movimientos generados en el repo, borrados, HASH de elementos borrados, etc.
 
  
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

#------------------------------------- GIT HUB [Repositorios Remotos] ----------------------------------------------------------#

                Área de trabajo --> STAGING --> REPOSITORIO LOCAL --> REPOSITORIO EN LINEA
			a		b		c		D


// CREAR Y CONFIGURAR REPOSITORIO REMOTO //

  ## GIT CLONE --------------------------------------------------------------------------------

  c:>CODE .     :abre el VSC dentro de la carpeta actual.

	ESTANDO en la carpeta donde queremos copiar el repositorio por HTTPS, copiamos la dirección http y luego:

 	git clone [dirección https del repositorio a clonar] ↩️
  
  esto ya configura el remote origin, para el push y fetch

 
  
  
  ## GIT PUSH --------------------------------------------------------------------------------

	Para poder subir archivos a nuestro repo, debemos tener configurado el mismo mail con el que iniciamos sesión
 	en Github. 
  	Luego, si queremos subir algo a un repo "clonado", se utiliza el comando

    	git push origin main
     	git push [nombre del repo remoto] [rama del repo remoto]
  	
*Si esto abre una ventana de log, lo recomendable es hacerlo por [TOKEN]. Para obtener el [TOKEN], 
 vamos a Settings > Developer Settings > Personal Acces Tokens > Tokens (classic) y ahi Generar nuevo token

   		Recomendaciones sobre el token ------
     		- No debería ser eterno. Lo recomendable es de 7 a 30 días.
       		- Los permisos con la primera opción, REPO ya es suficiente.

 Esto generará un código que se debe copiar en el sistema de inicio de sesión de Github por la solapa TOKEN.

 


 
 ## GIT PULL -----------------------------------------------------------------------------------

	Se utiliza para descargar CAMBIOS hechos en el repo online, al repo local, de ciertos archivos(no todos, para eso 
 	se usa un git clone).
  	esto es un /git fetch/ y luego hacer un /git merge/ todo junto.

   * Git pull origin main

 # *ERRORES con git push:

   There are two ways of solving the fatal: refusing to merge unrelated histories error

	*git pull origin master --allow-unrelated-histories.

   You can substitute origin with the remote repository you are pulling from. You can also replace the master branch with whatever branch you want the pull request to merge into.

  	Option 2: unstage, stash, clone, unstash, and then commit

The alternative (and longer) way of fixing the fatal: refusing to merge unrelated histories issues is to unstage your current commits, stash them, clone your required remote repository, and then place your stashed branch contents into the new clone.

This will ensure that any conflicts that you may encounter in the code are addressed before merging and prevent application errors from occurring.
To unstage all the files in your last commit, use the following git command: git reset HEAD~.

To stash your unsaved files, use the following git command: git stash.

This will give you a clean working tree to pull your remote repository into. Once you’ve successfully pulled into your branch, you can unstash your files, commit them as a separate commit and resolve any file conflicts that you may have.

To unstash your files, use git pop. This will move the changes stashed and reapplies them to your current working copy.

Alternatively, you can use git stash apply to add the changes to your current working copy of code.

Here is a quick summary of differences between git stash apply and <code”>git pop:

    git pop: ‘pops’ the changes from the stash and applies them to the current code
    git stash apply: keeps the changes in the stash and applies the changes to the current code

The easiest way to prevent the fatal: refusing to merge unrelated histories error is to avoid pulling remote repositories into branches that already have commits on them.
However, sometimes you just want to keep the commits. One way to prevent the error is to create a brand new branch, pull your required code in, and then manually merge your local branch into your main flow.





## GIT FETCH ---------------------------------------------------------------------------------------------
	esto descarga los cambios en el repo Origin/Main, y crea una rama temporal, del mismo nombre para poder
 	verificar los cambios, y en todo caso, sumarlos a nuestro repo local
	Luego de ejecutar el fetch, debemos "pasar" a la rama temporal que se suele llamar (origin/main) para verificar los cambios hechos, mediante el siguiente comando:

   git switch --detach origin/main (esto genera que se trate como temporal) 
   
 	y luego, si sirven, guardarlos. VOLVER a la rama principal de nuestro repo local
  	para hacer un -git pull-



## Migrar repositorio local a uno remoto ------------------------------------------------------------------

   Luego de crear un repositorio en Github, mediante Git hay que hacer

  	git remote add [nombre de referencia del repo remoto] [dirección http del repositorio remoto creado]

   ej:  	
   			
      git remote add origin https://github.com/Sebastian1601/Codoacodo-tp-nodejs.git
      
   luego se comanda
  				
      		git branch -M main
   y finalmente

    		git push -u origin main
 	
  

# FORK ----------------------------------------------------------------------------------------------------

   Un fork es una copia de un repositorio remoto en nuestro repositorio remoto. Cuando queremos duplicar algun proyecto del que podemos copiarnos.
   Al hacerlo, queda en nuestro repo, y se hace el commit para "guardarlo" por primera vez.


# PULL REQUEST --------------------------------------------------------------------------------------------

esto se da cuando hacemos un fork, y guardamos un repositorio que no es nuestro en el repo online.
queremos subirla de nuevo al repo remoto copia del proyecto de alguien más.

cuando ya tenemos cargado en el repo online nuestro el repo local del fork, tenemos una opción llamada [CONTRIBUTE], y de ahi se abre la opción [OPEN PULL REQUEST].
Ahi se verifica que se pueda fusionar ambos repos, y luego se agregan los datos sobre titulo y descripción del pull request.


# ERROR AL USAR GIT LOG (queda la lista de commits y luego dice log file: y no sale de esa pantalla.)

	al registrar este error, hay que presionar ESC, y luego la tecla "Q"

 


















