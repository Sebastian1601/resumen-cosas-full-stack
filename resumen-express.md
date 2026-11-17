
## request: objeto response

Este objeto representa la respuesta HTTP que se le envía al cliente ante una petición HTTP.

todo lo que está entre paréntesis, es opcional
###  res.send([body])
Envia una respuesta de diversos tipos:
	- cadenas de texto
	- objetos
	- arrays
	- buffers
Ajusta automáticamente el encabezado `Content-Type` de acuerdo al tipo de datos enviados.

### res.json([body])
Convierte el parámetro recibido a una cadena **JSON** y envía una respuesta con el encabezado `Content-Type` configurado como `application/json`

### res.status(codigo)
Establece el código de estado HTTP de la respuesta. Es un metodo encadenable
>Ejemplo
>res
>	.status(404)
>	.send("No encontrado")

### res.sendStatus(codigo)
Establece el código de estado HTTP y envía la represtanción de ese código como el cuerpo de la respuesta en formato de texto.

### res.sendFile( path, [opciones], [fn])
Transfiere el archivo ubicado en el `path` y ajusta automáticamente el  `Content-Type` según la extensión del archivo.

### res.redirect([estado], path)
Redirige la ==petición== a otra URL. El código de estado predeterminado es 302.

### res.render( view, [locals], [callback])
Renderiza una plantilla de vista(view) como EJS, Pug o Handlebars y envía la cadena HTML resultante al cliente.
- los parámetros locals, acepta objeto de tipo Javascript, por lo que si hay que pasar muchos valores, ese objeto tendrá una propiedad y detro de ella, pondremos un array si es necesario.

### res.set(field, [value]) / res.header()
Establece uno o varios encabezados HTTP en la respuesta.

### res.cookie(nombre, valor, [opciones])
Establece una cookie en el navegador del cliente con valores opcionales de configuración(expiración, httponly, etc)

### res.clearCookie(nombre, [opciones])
Elimina una cookie específica del cliente

### res.end([datos], [encoding])
Finaliza el proceso de respuesta de forma rápida, habitualmente sin enviar datos adicionales (por ejemplo, en respuestas vacías como un 204 No-Content )

### res.type(tipo)
Establece el encabezado `Content-Type` basándose en una cadena de tipo MIME.

>Ejemplo: `res.type('json')` o `res.type('text/html')`

MIME: **Multipurpose Internet Mail Extensions**
Son identificadores estandar de dos partes que se utilizan para indicar en internet, el formato de un archivo o un conjunto de datos.

>sintaxis: `tipo / subtipo` 

>Ejemplo: `image/png`

- Tipos MIME comúnes
	- text/html: páginas web html
	- text/css: hoja de estilos css
	- text/javascript: texto de código javascript
	- text/plain: texti sin formato
- Datos estructurados
	- application/json : formato json
	- application/xml : archivos xml
	- application/x-www-form-urlencoded : datos enviados desde formularios HTML estándar
- Imágenes
	- image/jpeg
	- image/png
	- image/gif
	- image/svg+xml
	- image/webp
- Audio y video
	- audio/mpeg:
	- audio/wav
	- video/mp4
	- video/webm
- Documentos y archivos binarios
	- application/pdf  
	- application/zip 
	- application/octet-stream : archivos binarios genéricos.


