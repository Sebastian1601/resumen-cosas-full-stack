

## Shortcuts

**botón medio del raton** : orbitar modelo
**shift + botón medio**: panning de la escena
**Rueda**: zoom
**SHIFT + A**: menú para añadir elemento a escena en la posición del cursor 3D. (cámaras, luces, formas, primitivas, etc)
	al agregar un elemento, aparece la ventana propiedades del mismo. si la cerramos, se abre de nuevo con F9
**Shift + Botón derecho del mouse**: mover cursor 3D a la posición clickeada. 
**F2** - Nombrar el objeto seleccionado con el cursor
**G** : mover objeto seleccionado
	si al usar G, y tener el objeto a mover seleccionado, apretamos x, y o z podemos mover el elemento en el eje seleccionado.
**R** : rotar elemento en los ejes
**S** - Escalar un elemento seleccionado.
	con este método, lo unico que hacemos es escalar en el viewport el elemento seleccionado, pero para que el elemento *TOME* los nuevos valores de escala, debemos, con el objeto seleccionado, apretar *Ctrl + A* y luego seleccionar *SCALE* del menú. Esto termina por aplicar los cambios realizados.
**Shift + D** - Duplicar objeto seleccionado
**F12**  - renderizar imagen fija desde vista de camara.
**numpad 0** - ver a traves del punto de vista de camara.
	LUEGO para fijar la vista de la camara y usarla al editar, la seleccionamos de la coleccion de elementos, 
	apretamos **N**,
	eso trae el *menu de cámara*, y en la solapa **VIEW**, podemos clickear **LOCK camera to VIEW**.
	
**F3** : abre el menu para buscar un comando
**FULLSCREEN** - Ctrl + Space

**AGRUPAR** distintos objetos, sin que dejen de ser individuales: *PARENTING*
Se selecciona primer el objeto hijo, que va a seguir al padre, y luego al padre.
Luego con *Ctrl + P*, nos abre el menu de parenting. Ahi seleccionamos de las opciones, la que dice *Parent (Keep Transform)*

**AGRUPAR elementos en la ventana de objetos (Scene Collection)**
Para organizar elementos en la ventana de *Scene Collection*, podemos agregar una *Colección* de elementos(algo así como una carpeta de elementos) desde el mismo menú de objetos.
**Mover objetos de una colección a otra** - con el objeto u objetos seleccionados, apretamos *M* y nos abrirá una ventana donde podemos elegir a qué colección enviaremos el o los objetos seleccionados.

## **Camara** 

Fly View Mode - Activar el modo de mover la camara como un juego FPS. (wsad) - Se puede ir al submenu *View > Navigation > Fly Navigation*


## Iluminacion

Para una iluminacion real, podemos eliminar la luz que va por defecto en la escena, y agregar una luz natural desde el menú propiedades [WORLD] y luego, clickear en el punto amarillo de "*color*", y elegir Sky.


## **MODIFICADORES** - 
Los modificadores son funciones que se aplican al objeto seleccionado en principio en la ventana del viewport. Cuando creamos un modificador, estamos viendo como "quedaría" el objeto finalmente con el modificador aplicado, **PERO TODAVIA NO LO ESTA!** por lo que, para hacer efectivo un modificador, luego de configurado, hay que "*aplicarlo*" desde la flecha hacia abajo del menú al lado del nombre del tipo de modificador. Esto se hace en la *vista de Objetos*
También si el modificador se está aplicando en más de un objeto a la vez, figura un nro en el lado derecho del *nombre automático* que se le asigna cuando se crean(no del nombre del tipo) 
**PARA SEPARAR** A los objetos afectados por este nodo, si apretamos este nro con el elemento seleccionado que queremos esté aislado de los demás, los cambios hechos en ese objeto, se aplicarán SOLO a ese objeto, y no a los demás que SI comparten el modificador.

**Subdivision** - divide exponencialmente una cara en 4 para aplicar detalle.
	*levels viewport* -> representa en el area de trabajo
	*Render* -> se aplica al renderizar una imagen o video.
**Solidify** - agrega "cuerpo" a una cara de un objeto, o todo el objeto depende de la selección. 
También con este modificador, se puede hacer que una capa "arriba" de otra, se "pegue" usando la propiedad *Edge Data*, dentro de *Solidify*, y subir el *Crease Inner* a 1. Esto hace que la parte interna no suba en curva, sino que "se pegue" a lo que esté cubriendo.
**Simple deform** - Se utiliza para deformar el objeto seleccionado, útil para crear curvas en objetos rectos y otras propiedades más.

**Shade Smooth**: Suavizar malla de elemento sin agregar vértices
Con el objeto seleccionado, luego *click derecho* -> *shade smooth* : suavizar una mesh con curvas
*shade flat* -> volver a suavizar superficies planas y con ángulos rectos
**TAB** : cambiar entre modos *object* y *edit*

Al generar los modificadores, estos se aplican luego del trabajo en la vista de edición, pero si queremos aplicarlos para trabajar con el modelo ya modificado, hay que "aplicarlos" mediante la flecha para abajo en el menú de cada modificador. Esto hace que quede ya renderizado en el objeto que estamos trabajando.

**ELEGIR SIMILARES** - Shift + G

## **EDITAR MALLA(MESH)**

con un objeto seleccionado, para editar la malla.
en el 2do submenu, está el modo, normalmente *OBJECT MODE*
eso se puede pasar a *EDIT MODE* para modificar los vertex points.
si selecionamos algun *vertex* y activamos el modo *Proportional Editing* con *O*, se abre un circulo que edita los vértices de la malla en proporcion a lo que toca.
se puede agrandar o achicar con la rueda o *pageup* *pagedown*
primero se elige un vertex. Luego se activa *O* y finalmente se aprieta *G* para mover.

**Seleccionar vertices de un edge completo** - *ALT + click* en uno.

**Para seleccionar los vertices unidos en el eje Y**, se selecciona uno, 
*ALT + click* en el siguiente del eje Y.

**A** - seleccionar toda la malla del objeto en cuestión

**Ctrl + +** - Teniendo seleccionado un eje de vertices, por ej el eje X, si apretamos Ctrl + +, esto va sumando más ejes paralelos al seleccionado.

**Ctrl + -**  deselecciona ejes ya seleccionados anteriormente.

**Alt + Z** - ver en tipo Rayo X el objeto, para seleccionar vertices más facil.

**H** - con vértices seleccionados, este shorcut "oculta" los mismos para que no sean modificados con otras herramientas, como la de *estirar/contraer malla*

**Alt + H** - Mostrar vértices ocultos con H.

**Ctrl + B** - [Bevel Angles] Crear ángulos en la cara o vértices seleccionados. Si se usa la *rueda del mouse* se crean más subdivisiones para el ángulo.

Si tenemos dos *Edges*, y queremos aplicar el bevel hasta que estos dos bordes, "se unan", para que no se overlapeen entre si, apretamos C para activar el modo *Clamp*, y esto genera que el bevel se aplique hasta que ambos cortes de los edges se unan.
>[!important] Importante
>Luego de unir dos edges con bevel, podemos terminar con vertices practicamente en el mismo espacio, por unir dos edges, por lo tanto, para eliminar estos vertices duplicados, seleccionamos todo el objeto con **A**, y luego, **M** -> **Menú Merge** y seleccionamos *By Distance*. Esto elimina vértices que estén muy cerca uno de otro. 

**Crear Cara** - Teniendo seleccionado al menos 3 vértices, se presiona F y esto crea una "cara" entre estos 3 puntos

**SELECCIONAR "BORDES"** en vez de *vértices* en modo *Mesh editor* - Estando en modo mesh editor, presionar 2, o seleecionar el 2do modo en los 3 íconos al lado del menú de selección de modo.



**/** - Aislar el elemento que estamos trabajando / volver a mostrar todos los elementos.

**Ctrl + R** - inserta cortes en un objeto, inicia en 1, con la rueda del mouse se agregan más cortes. Al confirmar con click, da la opción de modificar, pero con click derecho se cancela y se aplica tal cual está.

**Objeto seleccionado -> right click -> Set Origin -> Origin To Geometry** - Setear el punto de orígen de un objeto en el centro(para aplicar modificadores, etc) 

Para que los elementos que modificamos con la malla, se peguen a otro modelo ya hecho debajo, debemos activar el snapping con **SHIFT + TAB** y setear la opción de *INCREMENT* a *Face Project*

**EXTRUDING**: crea nuevas "caras" de acuerdo a la cantidad de vértices que elegimos y duplicamos. Seleccionar los vertices y luego apretar **E**, esto habilita el modo de posición. Podemos mover los vertices que elegimos y se creará una nueva "cara" desde donde estaban los vertices elegidos, hasta la nueva posición donde coloquemos nosotros los vértices.
Esto logra "extender" la malla de edición, creando nuevos vertices para modificar y extender la malla en la que estemos trabajando.
## **Esculpir (sculpting)**
Al esculpir, podemos usar las distintas herramientas en la parte inferior.

**F** - Permite cambiar al vuelo el tamaño del cursor, moviendo a la izquierda el mouse para achicar, y a la derecha para agrandar.

**Shift + F** - Permite cambiar la fuera de la herramienta que estamos usando en el modo *sculpt*

**MASK** la máscara evita que apliquemos cambios a donde marcamos y creamos la máscara, por lo que toda la malla que esté pintada en modo máscara, no tendrá cambio alguno.

normalmente la opción "agrega" una máscara, pero si nos equivocamos y queremos borrar una parte, tenemos los símbolos **+** y **-** al lado del menú de modo donde dice "**Sculpt Mode**". 

Para suavizar una máscara aplicada  y mejorar los resultados si contienen curvas, se puede ir al menu de *Sculpt mode*, a *Mask*, y luego usar "*Smooth Mask*"

**CLEAR MASK** - Borra la máscara creada en absoluto.


### **Materiales** 

Al clickear un objeto, aparece un menu en las propiedades. el de *materiales*. ahi el *BASE COLOR* es el color base de la pieza seleccionada. se puede cambiar.

para ver en el viewport los materiales, tenemos que entrar en "Render mode", que se encuentra en la parte superior derecha, donde están los ejes x, y z. 
el modo básico es el *Viewport shading: Solid*.

en el menú surface del material agregado, tenemos el color, si es metálico, si refleja la luz, etc.
La propiedad *Roughness* indica que tan rugoso o compacto es el material que estamos creando.
Para reemplazar un color plano con una imágen, podemos agregar un material, y en vez de seleccionar un color, abrimos el punto de color de al lado donde dice *Base Color*, y eso abre un menú, donde podemos seleccionar la opción bajo "*Texture*" que se llama "*Image Texture*", y eso nos permitirá agregar una imágen como textura.
Luego, seleccionamos abrir una nueva imágen como textura, o crear una nueva.

Aparte de agregar la textura, vamos a ir a la ventana de materiales dedicada en el menú principal, en la opción "*Shading*", eso cambiará el layout de la pantalla.

Para unir las ventanas, vamos al divisor entre ellas, click derecho y elegimos *JOIN LEFT* para que la ventana de la derecha ocupe todo el espacio.
Aqui se configuran los mapas normales, etc. Esto se tiene que ver en detalle aparte.

Para crear un material, elegimos un objeto y en el menú Materials, creamos "*new material*", le asignamos un nombre, "*material1*" y para que varios elementos lo utilicen, los elegimos, y por último, elegimos con *Shift + click* el material el cual tenía creado la propiedad *material1*, y hacemos *Ctrl + L*, eso abre el menú de *Link/Transfer Data* y ahi elegimos *Link Materials*. Eso hará que al lado del nombre del material, aparezca el nro de elementos que comparten dicho material.

**Creando elementos de distintos colores, saturación y encima, definiendo qué porcentaje de cada uno queremos en el acabado.**
Para eso, vamos al submenu de *Shading*, y ahi tenemos los nodos de shading, donde vamos a crear un nodo llamado *Object Info*, del cual hay una propiedad llamada *Random*. Desde esa salida, unimos con el nodo que vamos a agregar llamado *Color Ramp[Factor]*, y de ahi, de la salida *Color Ramp[color]* lo unimos a *Principled BSDF[Base Color]* que es nuestro nodo central al crearlo en el viewport de objeto.

Si queremos agregar cierta variedad metálica a nuestros objetos mediante el color, podemos crear otro nodo *Color Ramp*, que venga desde la misma propiedad *Random* de *Object Info*, y unir el nuevo *Color Ramp[Color]* a *Principled BSDF[Metallic]*, indicándo que el color será negro para los elementos que no sean metálicos, y blanco para los que sí, en el gradiente *Constante* de nuestro nuevo nodo *Color Ramp*.

![[./img/shadingNodes01.png]]


#### Subsurface Scatering
Esto es una propiedad de ciertos elementos reales, lo que hace es simular el paso de la luz a través de un material (en el que configuremos), y ahi definimos el 
peso entre 0 y 1.
el radio entre 0 y 1 en los 3 colores, RGB, y finalmente la escala, que define qué tan grueso sería el elemento que estamos modelando.

## **TEXTURE PAINT** - en el menú principal

Este modo permite pintar directamente en la textura. Normalmente Aislamos el modelo a modificar con la barra. /

Para pintar sobre una textura, es necesario, primero que nada, tener una textura en el objeto donde queremos pintar.
Normalmente, lo más básico que se puede hacer es asociar una *image texture* desde el menú de *Materiales*, en *base color*, hacemos click en la bolita de color al lado de esta opción, y en el submenu, debajo de *texturas*, buscamos *image texture*.
Ahi seleccionamos +new para crear una textura, de resolución 1024x1024, y podemos ponerle un nombre, y un color base. Hacemos click en *new image* y eso nos crea la textura base. En principio no se ven cambios si estamos en el *viewport: Object*, pero si cambiamos a *viewport: Rendering*, la textura se hará presente.
A partir de ahi, podemos entrar al submenu debajo del principal, **Texture  Paint** y eso nos abrirá el modo de pintar texturas.

## **GEOMETRY NODES** - menú principal

Esto es un modificador, MUY IMPORTANTE, porque los cambios que hagamos aqui, luego, para que se hagan efectivos, hay que aplicarlos, como haciamos con *SOLIDIFY* o *SUBDIVISION*, sino quedan modificando la salida en pantalla, pero en realidad, no se aplican al objeto al cual le estamos generando la modificación.

Tiene su propia ventana de configuración, mucho como la de shading, con nodos que pueden hacer lo que sea.

Ejemplo: si queremos agregar puntos simplemente sobre las "caras" de nuestro objeto(sea cual sea). Podemos hacer
*Shift + A* -> *Points* -> *Distribute Points* on Faces.
Esto crea un nodo, donde lo ponemos entre el input y el output y eso nos generará objetos que están sobre el que nosotros estamos modificando.

El cuadro de *GROUP INPUT*, nos representa el objeto que nosotros tenemos seleccionado, al aplicarle un modificador, transforma de manera habitual esa geometría, en lo que le pedimos, por lo que, para mantener el objeto original, tenemos que agregar otro nodo que se llama *JOIN GEOMETRY* antes del *GROUP OUTPUT*.
*JOIN GEOMETRY* acepta más de un "valor o entrada" de otros nodos, por lo que, si queremos unir dos geometrías, debemos sumar a ambas en la entrada.
Para eso, desde el *GROUP INPUT*, arrastramos la salida a la entrada de *JOIN GEOMETRY*, eso quiere decir que le estamos pasando dos parametros a la funcion *JOIN GEOMETRY*, la capa original que queremos sumar a la capa que se transformó en *DISTRIBUTE POINTS ON SURFACE*
La cantidad de valores que acepta un nodo(o función) está determinada y representada por el ícono de color que tiene a sus lados el cuadro del nodo.

>Si es un punto, toma un solo valor esa entrada. Si es una linea estirada, quiere decir que acepta más de uno.

Podemos usar cualquier elemento que creemos para utilizar como los "puntos" en la superficie, y para eso, creamos un objeto que querramos, y lo arrastramos al panel de *GEOMETRY NODES* (para hacer referencia a ese objeto)

Teniendo el objeto que vamos a usar referenciado en el menú de GEOMETRY NODES, agregamos un nodo llamado *INSTANCES* -> *INSTANCES ON POINTS*.
Eso nos crea un nuevo nodo, y lo que vamos a querer hacer es, desde nuestro nodo referencia al objeto que queremos como punto, desde *GEOMETRY*, llevamos la unión hasta *INSTANCE* de nuestro nuevo nodo *INSTANCE ON POINTS*, y también una unión desde *DISTRIBUTE POINTS ON FACES (points)* hasta *INSTANCE ON POINTS(points)*, para luego sacar de la salida *INSTANCE ON POINTS(Instances)* a la entrada de *JOIN GEOMETRY*

![[./img/geometrynodes01.png]]

Si vemos que estamos manejando valores muy grandes al setear nuestros modificadores, podemos aplicar una función matemática en el mapa de nodos de geometría para que multiplique el valor que nosotros ponemos, y lo escale a lo que necesitemos según el tamaño del objeto.
Por ejemplo, la densidad de objetos se maneja de manera espacial, uno define la densidad de elementos en ese punto del espacio, por lo que si el objeto afectado junta 100 puntos en un tamaño x, si lo achicamos, la densidad va a ser la misma, pero al ser más pequeño nuestro objeto, va a levantar menos puntos por cara.
Para eso agregamos con Ctrl + A, la opción de nodo *Utilities > Math > Math*, y este nodo va entre la entrada que nosotros ingresemos del objeto de referencia, *Group Input*, y el modificador de densidad en *Distribute points on face.*

**Agregar distintos tipos de puntos sobre una cara de un objeto**
Para hacer esto, podemos crear una colección de los elementos que vamos a querer agregar a nuestra objeto principal, y luego, en la vista de nodos, eliminar la entrada de un solo objeto, y arrastras desde el menú de objetos, la colección entera, eso creará una referencia a la colección en los nodos.
Luego de que se crea el nodo, se deben chequear las casillas de 
*SEPARATE CHILDREN* y *RESET CHILDREN*
Luego, para que se elija en cada instancia de los elementos, un solo modelo de la colección, tildamos en *INSTANCE ON POINTS* la opción que dice *PICK INSTANCE*
Si queremos afectar el ángulo en que estos puntos aparecen sobre la cara del objeto principal, basta con rotar en la vista 3D el objeto, y eso modificará cómo aparecen sobre la cara de nuestro objeto principal.

**Crear una rotación sobre objetos punto al azar**
Se crea un nodo llamado *Rotate Rotation* entre *DISTRIBUTE ON POINTS[Rotation]* e *INSTANCE ON POINTS[rotation]*, y se crea otro nodo llamado *RANDOM VALUE* que entre a la propiedad *ROTATE ROTATION*[rotate by].

Para indicar que un elemento puede girar 360 grados completos, se usa la palabra **TAU** en vez del valor de 2 radianes.



## **WEIGHT PAINT** (menú de vistas, object, sculpt, edit mode, weight paint)
Esto se utiliza para crear una "máscara" de cómo afectara ciertos elementos a la malla del objeto.
Esto, se define en un grupo de vértices, que figura en la ventana de propiedades llamada **DATA** en el menú derecho.
Se puede crear un nuevo grupo, para asociar a otro "peso de pintura".

Luego, definido el grupo, vamos a nuestros *GEOMETRY NODES* del objeto que queremos aplicarle los puntos, y desde la entrada de *DISTRIBUTE POINTS ON FACE(Density Factor)*, arrastramos hacia afuera una unión, y al soltar, se nos abre un menú, buscamos la opción "*NAMED ATTRIBUTE*" , y desde ahi, en el campo name, elegimos nuestro vertex group definido antes, por el nombre que le pusimos. Esto hará que donde pintemos más cercano al valor 1 en nuestra ventana de WEIGHT PAINT, se creen más valores de los puntos, y si pintamos más cerca del 0, entonces serán menos los puntos distribuidos, por eso actúa como una máscara.
Apretando *Ctrl* y al pintar en *WEIGHT PAINT*, pinta de manera "*inversa*" al valor del peso que tenemos definido en *Weight*.

>[!important] Duplicando objetos que comparten los mismos valores del geometry node
Si creamos un objeto, que tiene modificador y lo duplicamos, los nodos van a afectar a ambos, SI NO definimos que el valor que queremos que sea distinto, quede como entrada MANUAL de la función modificadora. Por ejemplo, si en el caso de las donas, modificamos la densidad, esta va a afectar de igual manera a las copias que hagamos de cada dona. Ahora, si desde el cuadro de 
*DISTRIBUTE POINTS ON FACE(Density Max)*
sacamos una unión desde *Density Max* hacia el *GROUP INPUT* (que recordemos, era nuestro objeto de entrada), se creará un campo en el menú de Modificadores, que nos permitirá ingresar para cada dona, un valor de densidad de puntos, para la lluvia de objetos. Esto nos permitirá modificar manualmente, para cada dona, cuánta lluvia de puntos queremos.

Para **RENOMBRAR CAMPOS** en un nodo , se selecciona el nodo, y se aprieta *N* para entrar a las propiedades del nodo.

## Render Engines

Por defecto, el motor que renderiza las imágenes se llama *EEVEE*.
Este motor se caracteriza por ser rápido, pero no detallado.




## Voxel Remesh
Esto nos permite unir varias piezas de primitivas en una sola malla, útil en modelado y esculpido.

1. Se crea las primitivas
	cada primitiva es un objeto independiente inicialmente.
2. Se selecciona las piezas que se quieren unir, y se presiona `Ctrl + j`
	Esto ejecuta un Join entre las primitivas.
>[!warning] Importante!
>Esto no fusiona "físicamente" todavia las geometrías, simplemente combina los objetos en un único objeto Blender (se mueve uno, se mueven todos...) pero las mallas siguen siendo independientes y pueden estar superpuestas.

3. Se configura la resolución del **Voxel Remesh**
![[Pasted image 20261112112601.png]]
Ahora viene lo importante:
	1. Se cambia a *sculpt mode*
	2. Se presiona `R` para activar el ajuste de resolución del Voxel Remesh
	3. Se mueve el cursor para modificar el tamaño de los vóxeles (Voxel size).

Voxel pequeños: mayor resolución, más polígonos, y más detalles
Voxel grandes: menor resolución, menos polígonos, y formas simplificadas.

Esto se calcula "a ojo" un valor adecuado sin utilizar una medida exacta.

4. Ejecutar el *Remesh* con `Ctrl + R`
	Blender ejecuta el Voxel Remesh
	Internamente, se analiza el volúmen ocupado por las geometrías.
	se construye una nueva superficie basada en los vóxeles.
	Se fusiona las partes que se intersectan
	Genera una única topología continua.

Esto dejaría ya los objetos unidos y la malla recalculada como una malla única.

## Herramientas de Sculpt mode
### Herramientas principales de escultura
#### Draw
Agrega volumen a la superficie siguiendo el movimiento del cursor.

- Desplaza los vértices en dirección a las normales de la superficie.
- Permite construir volumen progresivamente.
- Es una de las herramientas más utilizadas para bloquear formas generales.

Uso: agregar masa muscular, mejillas, frente, brazos o cualquier volumen básico.
#### Draw Sharp
Similar a Draw, pero genera trazos más definidos y estrechos.
- Produce crestas y relieves pronunciados.
- Permite crear pliegues y líneas de volumen.
- Es útil para detalles más marcados.

Uso: marcar tendones, arrugas, bordes y separaciones anatómicas.
#### Clay
Agrega volumen con un comportamiento similar al de colocar arcilla sobre una superficie.
- Construye volumen progresivamente.
- Tiene un efecto más suave y extendido que Draw.
- Permite desarrollar masas orgánicas.

Uso: construir músculos, pómulos, zonas del rostro y volúmenes corporales.
#### Clay Strips
Agrega volumen mediante trazos que parecen pequeñas tiras de arcilla.

- Produce una superficie más irregular y con textura.
- Permite construir volumen rápidamente.
- Es especialmente útil para definir masas musculares.

Uso: construir brazos, piernas, torso, músculos y estructuras orgánicas.
### 2. Herramientas para modificar y desplazar geometría
#### Grab
Permite agarrar una región de la superficie y desplazarla.
- No agrega ni elimina volumen directamente.
- Mueve los vértices dentro del radio del pincel.
- Permite cambiar la silueta de la escultura.

Uso: modificar proporciones, alargar extremidades, desplazar una nariz o corregir la forma general de una cabeza.
### Snake Hook
Permite estirar la geometría como si estuvieras tirando de una porción de arcilla.
- Desplaza y estira la superficie.
- Puede generar extensiones largas y puntiagudas.
- Es más agresivo que Grab.

Uso: crear cuernos, dedos, orejas, tentáculos y otras extensiones.
### Elastic Deform
Deforma la geometría con un comportamiento elástico.
- Distribuye la deformación sobre una región.
- Intenta conservar una transición suave con el resto de la superficie.
- Permite modificar volúmenes sin generar desplazamientos tan bruscos.

Uso: cambiar proporciones y deformar regiones grandes de una escultura.
### Pose
Permite modificar una parte de la escultura como si tuviera una articulación.
- Define una región que actúa como segmento deformable.
- Permite rotar, desplazar o modificar partes de la geometría.
- Es útil para cambiar la postura de una figura.

Uso: doblar brazos, piernas, dedos o modificar la posición de una extremidad.

### 3. Herramientas para generar pliegues, relieves y detalles
#### Inflate / Deflate
Infla o contrae la superficie desplazando los vértices en dirección a sus normales.
- A diferencia de Draw, afecta el volumen de manera más radial.
- Permite aumentar o reducir el grosor de una zona.
- Es útil para trabajar con superficies redondeadas.

Uso: inflar mejillas, músculos, labios o zonas carnosas.
#### Blob
Genera un volumen redondeado mientras desplazás el pincel.
- Acumula geometría hacia afuera.
- Produce formas más abultadas que Draw.
- Es útil para agregar protuberancias.

Uso: crear nudillos, bultos, verrugas, músculos o irregularidades orgánicas.
### Crease
Permite crear hendiduras y pliegues estrechos.
- Empuja la geometría hacia adentro.
- Concentra los vértices hacia el centro del trazo.
- También permite crear crestas dependiendo de su configuración.

Uso: definir separaciones musculares, arrugas, pliegues de la piel y detalles anatómicos.
### Layer
Agrega volumen hasta alcanzar una altura determinada.
- Construye capas de volumen.
- Permite realizar trazos de altura relativamente uniforme.
- Evita que cada pasada aumente indefinidamente el volumen en el mismo sector.

Uso: construir placas musculares, relieves, zonas del rostro y estructuras superficiales.

### 4. Herramientas para aplanar y definir superficies
#### Flatten
Aplana la superficie tomando como referencia un plano promedio.
- Reduce las irregularidades.
- Lleva los vértices hacia una altura similar.
- Permite crear superficies relativamente planas.

Uso: definir planos de la mandíbula, pómulos, frente o superficies de una escultura.
#### Fill
Rellena zonas hundidas llevando la geometría hacia el plano del pincel.
Uso: levantar hendiduras o corregir depresiones en la superficie.
#### Scrape
Realiza el efecto contrario a Fill: elimina o reduce las zonas que sobresalen del plano.

Uso: definir planos de la cara, superficies de músculos y estructuras con bordes más definidos.
#### Multiplane Scrape
Utiliza dos planos inclinados para trabajar la superficie simultáneamente.
- Genera transiciones angulares.
- Permite construir bordes definidos.
- Es especialmente útil para superficies con aspecto facetado.

Uso: definir estructuras óseas, planos de la mandíbula y formas más angulares.
#### Pinch
Atrae los vértices hacia el centro del pincel.
- Concentra la geometría.
- Estrecha pliegues y bordes.
- Ayuda a definir transiciones.

Uso: acentuar arrugas, bordes de labios, separaciones musculares y pliegues.

### 5. Herramientas para deformar y acomodar la superficie

#### Thumb
Desplaza y aplana la geometría siguiendo el movimiento del pincel.

Es similar a empujar arcilla con el pulgar.

Uso: acomodar pequeños volúmenes, suavizar transiciones y desplazar material superficial.

#### Nudge
Desplaza los vértices siguiendo la dirección del trazo.

Uso: acomodar pliegues, mover pequeñas porciones de geometría y corregir irregularidades.
#### Rotate
Rota los vértices alrededor del centro del pincel.

Uso: generar torsiones y modificar la orientación local de una región.
#### Slide Relax
Permite deslizar la topología para redistribuir los vértices sin modificar demasiado la forma general.

También puede suavizar la distribución de la geometría.

Uso: corregir zonas donde los vértices están demasiado concentrados o distribuidos irregularmente.
#### Boundary
Trabaja específicamente sobre los límites o bordes de una malla.

Uso: deformar bordes abiertos, modificar contornos y trabajar con regiones delimitadas.
#### Cloth
Simula el comportamiento de una tela durante la deformación.
- Permite arrastrar, empujar y tirar de la superficie.
- Produce pliegues y deformaciones con comportamiento similar al tejido.
- Puede utilizar simulaciones físicas locales.

Uso: ropa, telas, pliegues y superficies blandas.

### 6. Herramientas de máscaras y organización de la escultura.
Estas herramientas no necesariamente agregan o eliminan volumen. Su función es controlar qué partes de la geometría se pueden modificar.

#### Mask
Permite pintar una máscara sobre la superficie.
- Las regiones enmascaradas quedan protegidas de las deformaciones de otros pinceles.
- Podés seleccionar zonas complejas mediante trazos.
- Se puede invertir o eliminar la máscara.

Uso: proteger los ojos mientras trabajás la cara, aislar una zona muscular o impedir que una deformación afecte otra parte del modelo.
#### Draw Face Sets
Permite asignar diferentes conjuntos de caras (Face Sets) mediante trazos.

Los Face Sets sirven para organizar una escultura en regiones independientes.

Uso: separar visualmente cabeza, torso, brazos y piernas para facilitar su manipulación.
#### Box Mask / Lasso Mask / Line Mask
Son herramientas para crear máscaras mediante selecciones geométricas:
- Box Mask: selección rectangular.
- Lasso Mask: selección dibujando un contorno libre.
- Line Mask: selección mediante una línea.

Son útiles para proteger regiones sin tener que pintarlas manualmente.
#### Box Face Set / Lasso Face Set
Funcionan de manera similar a las herramientas de selección anteriores, pero crean Face Sets en lugar de máscaras.
#### Edit Face Set
Permite modificar los conjuntos de caras existentes.

### 7. Herramientas de filtros globales
A diferencia de los pinceles tradicionales, estas herramientas permiten aplicar una transformación sobre una región amplia o sobre toda la escultura.

#### Mesh Filter
Aplica diferentes transformaciones a la geometría completa o a una región seleccionada.

Entre sus operaciones se encuentran:

- Smooth: suavizar la geometría.
- Scale: escalar el volumen.
- Inflate: inflar la superficie.
- Sphere: aproximar la geometría a una esfera.
- Relax: relajar la topología.
- Sharpen: acentuar detalles.

Uso: modificar grandes regiones sin tener que recorrerlas manualmente con un pincel.

### Cloth Filter
Aplica una simulación de tela a la geometría.

Permite generar pliegues, arrugas y deformaciones sobre superficies.

### Color Filter
Permite modificar los colores de la superficie cuando trabajás con atributos de color.

### 9. Parámetros que deberías conocer de los pinceles
Independientemente del pincel que selecciones, hay propiedades que determinan cómo se comporta.

|Parámetro|Función|
|---|---|
|Radius (Radio)|Determina el tamaño del área afectada.|
|Strength (Fuerza)|Determina la intensidad del efecto.|
|Falloff|Controla cómo disminuye el efecto desde el centro hacia los bordes.|
|Direction|Determina si el pincel agrega o sustrae volumen, cuando corresponde.|
|Autosmooth|Suaviza automáticamente la geometría durante el trazo.|
|Front Faces Only|Evita afectar las caras orientadas hacia el lado opuesto de la vista.|
|Symmetry|Permite reproducir los trazos simétricamente.|

Dos parámetros merecen especial atención:

Radius: un radio grande permite modificar volúmenes generales; uno pequeño permite trabajar detalles localizados.

Strength: una fuerza baja permite trabajar progresivamente. Una fuerza alta produce modificaciones más agresivas.