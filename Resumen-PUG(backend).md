
Pug permite desarrollar html desde el backend para las vistas con codigo más simple, pero aún asi, utilizando emmet expressions.

PUG usa indentación para definir las etiquetas y la apertura y cierre.

```pug
html
	meta
	meta
	link(rel="sytlesheet" href="css/login.css") //linkear archivo css externo
	script(src="js/login.js" defer)	 //linkear javascript externo
	title titulo de la web
body
	h1 Hola mundo
	
	form#login_form
		label(for="usuario") Usuario
		input#usuario(type="text" name="usuario" autocomplete="usuario" required)
```

Gracias a esto podemos presentar una web más rápidamente no teniendo que preocuparnos por las etiquetas de apertura y cierre, sino indentando el código.
Podemos definir clases, atributos e ids de la manera más simple.

##### Preparar el backend para usar plantillas pug
Para poder usar pug(formerly jade) debemos indicarle al backend en nodejs que vamos a utilizar este motor de plantillas.
Esto lo hacemos en la configuración de app al configurar Express.

```js
const app = express();

//aqui seteamos variables globales de express(app)
app.set("views", "ruta a la carpeta templates de pug");
app.set("view engine", "pug");
```

##### Navegar en distinas páginas pug
Para navegar entre una página de pug y otra, mediante hipervínculos con la etiqueta `<a href="/index">` debemos definir en el backend que queremos renderizar esa otra página cuando nuestro frontend intenta alcanzar esa dirección con la petición `get`.

Por lo tanto, si queremos tener la web inicial *login*, y luego *index*, debemos definir ambos endpoints
```js
app.use("/", (req, res)=>{
res.render("plantillaPugCorrespondiente");
});

app.use("/index", (req, res)=>{
res.render("plantillaPugIndex");
});
```

#### Setear la ruta de archivos estáticos
Tenemos que definir la ruta de nuestros archivos estáticos mediante express también, para que asi pug pueda utilizar las rutas relativas a esa carpeta.
Esto lo podemos hacer mediante `express.static("ruta-a-carpeta-static")`
```js
app.use(express.static("ruta-a-static"));
```

---
#### Contenido de una etiqueta abierta
si queremos indicar que una etiqueta contiene texto, lo debemos incluir luego de la definición de la etiqueta, separado por un espacio. *Todo lo que sigue se toma como texto.*

```pug
h1 Hola mundo!
```

---
#### Etiqueta por defecto DIV
para insertar una etiqueta div, podemos obviar escribirla y solamente poner la clase, esto creará un contenedor div con la clase o id o atributos que definamos...ejemplo
```pug
.my-container
	p.mi-parrafo Esto es un parrafo que estará dentro de un div
```

---
#### Comentarios
Podemos comentar de 2 maneras en las plantillas *pug*

>comentario que figura en el dibujado del html 
```pug
body
// comentario 1	 
```
Este comentario definido con las dos barras `//` va a figurar y lo podemos encontrar al explorar el html con las herramientas del navegador.

>comentario multilineas
```pug
//
	usando las 2 lineas, e indentando el texto, se pueden
	comentar varias lineas presentes a las herramientas del navegador

```


>comentario invisible a las herramientas del navegador
```pug
body
//- comentario oculto al navegador, solo visible en el código
```

>comentario invisible multilineas
```pug
body
//- 
	comentario multilinea oculto al navegador,
	solo visible en el código
```

---
#### Definir una clase o Id
Para definir una clase, podemos usar la sintaxis del punto seguido del nombre de la etiqueta, lo mismo con la id, pero usando el hashtag en vez del punto..

```pug
h1.tituloPrincipal Hola Mundo
h2#miId buenas tardes
```
podremos referenciar a estos elementos en js mediante la clase `.tituloPrincipal` o la id `#miId`

Para definir varias clases de una etiqueta o incluso clases e id, podemos concatenar las mismas al definir el elemento.
```pug
h1.tituloPrincipal.sideBar#principal hola mundo
```
esto se traduce a 
`<h1 class="tituloPrincipal sideBar" id="principal">Hola mundo</h1>`

---
#### Definir atributos de las etiquetas html
Para definir atributos de las etiquetas html que estamos usando, lo hacemos creando un paréntesis luego de definir la etiqueta, y los valores van tal cual se usan en html, `atributo="valor"`

```pug
img(src="ruta.png" alt="texto-alternativo" data-id="56")
```

---
#### Evaluar código en la plantilla
Podemos usar la plantilla para evaluar variables o directamente código js inclusive al dibujar la página. Para eso ponemos un guión y luego indentamos el código js siguiente...
```pug
- 
  let nombre = "Carlos"
  let apellido = "Rubenski"
  let resultado = nombre + " " + apellido
```

---
#### Utilizar datos de las variables en el html
Si recibimos datos al dibujar la página o evaluamos js dentro de la misma y necesitamos usar estos datos, podemos interpolar el texto con las variables usando llaves `{}`
```pug
- let titulo = "sr."
- let nombre = "David" 
h1 Hola, bienvenido nuevamente #{titulo} #{nombre}
// Hola, bienvenido nuevamente sr. David

//también podemos definir que una etiqueta tenga
//lo que contiene una variable dentro directamente
p=nombre
```

---
#### Usando Case-When en la plantilla
Al necesitar evaluar variables y condiciones, podemos usar este condicional de la siguiente manera:
**SOLO FUNCIONA CON CASOS ESPECIFICOS, no rangos**

```pug
- var edad = 17
  
case edad
	when 0
		p
			strong Con 0 años no existes.
	when 18
		p
			strong con 17 años casi puedes entrar.
	when 22
		p
			strong con 22 años ya eres mayor.
```
Esto logra que según el valor que tenga la variable edad, se imprima cierta estructura html predefinida. Cuando pasemos datos a la plantilla, esto cobrará mucha relevancia.

---
#### Usando IF
Usando la estructura de if, podemos utilizar rangos para evaluar, distinto al formato *case-when*

```pug
- let authorized = true;
- let age = 18

if authorized
	h3 autorización verificada. Acceso otorgado.
else if age >= 18
	h3 Aunque tienes 18 años, no tienes autorización.
else
	h3 No tienes ni autorización ni edad para acceder.
```

---
#### Uso de unless
Unless funciona como comprobar una negación, como no se puede usar el operador `!` existe una palabra dedicada para esto. Esto permite tener un codigo que se ejecutar o no, directamente con evaluar algo justamente.

>Ejemplo
```pug
unless authorized
	h3 no tienes autorización para acceder.
```

---
#### Uso de include
`Include` permite incluir justamente, otra plantilla en pug dentro de la actual donde se declara el comando.

Aqui vamos a usar una plantilla pug guardada en `templates` llamada `head.pug` pero no vamos a agregar la extensión a la plantilla, tal cual como cuando definimos el `res.render("index")` en express.

>Ejemplo
```pug
doctype html
html
	include templates/head
	body
		h1 Sitio web 1
		p Bienvenido a la web
		include templates/footer.pug
```


También podemos usar `include`  para adjuntar el codigo de un archivo  `.css` o `.js`, por ejemplo
```pug
doctype html5
html(lang="es")
	head
		meta(charset="utf-8")
		meta(http-equiv="X-UA-Compatible", content="IE=edge")
		title Test Pug
		style
			include "../css/style.css"
	body
		h1 Hola Mundo!
		...
```

---
#### Herencia de templates
Podemos crear un layout que hereden las demás páginas hijas de la principal y asi escribir estructuras combinables.

Para esto, definimos una página inicial, y dentro del código, vamos a definir con la *palabra reservada* `block` y un nombre, donde el resto del contenido será añadido.

>Defino mi página principal llamada "layout.pug"
```pug
doctype html
html(lang="es")
	head
		meta(charset="utf-8")
		meta(http-equiv="X-UA-Compatible", content="IE=edge")
		title=docTitle //esto se pasará mediante express al usar res.render
	body
		block contenido
```

y luego, definimos en otro archivo `pug`, el contenido que va en el *body*...
primero indicamos que este template *extiende* de `layout`

>[!warning] IMPORTANTE
>es muy importante respetar la indentación

>index.pug
```pug
extends templates/layout

block contenido
	h1 Bienvenido usuario!
	br
	hr
	p.miParrafo1 Contenido de párrafo
	...
```

El `title` del documento layout, se puede modificar usando una variable que se enviará al usar `res.render("layout", objetoConVariables)`

- Se pueden usar varios `block` dentro de layout para definir distintos archivos

>Archivo `layout.pug` que usa varios bloques de extensión de la página
```pug
doctype html
html(lang="es")
	head
		meta(charset="utf-8")
		meta(http-equiv="X-UA-Compatible", content="IE=edge")
		title=docTitle
	body
		block contenido
		
		block masContenido
```

y luego, en otro archivo, podemos definir nuevamente, el bloque `masContenido`

```pug
extends templates/layout

block masContenido
	.contenedor
		h5 Titulo
		img(href="./img/perfil01.png" alt="una imagen")
		p descripcion
```

---
#### Iterar sobre arrays para crear estructuras dinámicas 
Dado que pug permite ejecutar contenido js al construir el html, podemos iterar arrays de información que pasemos como parámetros al renderizar la plantilla.

Podemos asignar el valor a la etiqueta o evaluar el valor de las variables que usa los iteradores *each*.

podemos hacer
```pug
- let materias = ["ingles", "español", "quimica", "fisica", "matematica"]
  
//aqui podemos usar esto para crear una lista de estos valores del array
ul
	each value, index in materias
		li #{index + 1}: - #{value}
```
Lo que logra esto es iterar sobre el array y crear en cada elemento, una etiqueta `<li>` con el valor del array que está iterado.

*each* pasa el valor y el indice del array

---
#### Iterar sobre objetos
También podemos iterar sobre los pares clave-valor de objetos de js.

```pug
- let miObjeto = {
	  "ingles":"Prof. Carlos",
	  "espanol":"Profesora Jaqueline",
	  "quimica":"Profesora Claudia"
  }
  
ul 
	each key, value in miObjeto
		li #{key}: #{value}
```

---
#### sentencia While

Disponemos también de un iterador *while*.

```pug
- let contador=0
  
ul
	while contador < 11
		li=contador++
```

y esto generará una lista con 10 elementos `<li>`

---
#### Mixins - funciones en pug
Esto son funciones dentro de las plantillas de pug.
Podemos definirlas asi

```pug

mixin lista1
	ul
		li js
		li pyton
		li php

//para ejecutar la funcion en alguna parte del código, usamos el +
//aqui llamamos 2 veces a la funcion...
+lista1
+lista1
```

Estas funciones pueden recibir parámetros también, permitiendo la reusabilidad al máximo

```pug
mixin lista2(lenguaje=["vacio"])
	ul
		each value in lenguaje
			li=value
			
- let materiasArray = ["ingles", "español", "quimica", "fisica", "matematica"]
 //pasamos el array asi
+lista2(materiasArray)
	// o podemos pasarle un array literal
+lista2(["valor1", "valor2", "valor3", "valorn"])
```

Y los parámetros de las funciones también aceptan valores por defectos.

---


