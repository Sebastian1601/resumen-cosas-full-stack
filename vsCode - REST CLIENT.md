
La extensión RESTClient se utiliza para probar endpoints en api rest.

### Crear archivo de peticiones
Para iniciar, lo que hacemos es crear un archivo de extensión `.http` para luego, poder crear y definir dentro nuestras peticiones a los endpoints.

### Definir una peticion
Para definir una petición, vamos a poner el método de la misma primero, un espacio y luego la URL de la misma.
Si la petición está definida correctamente, arriba de esto se agregará la leyenda "*send request*" para justamente, enviar la petición y ver si la API responde.

```restClient
GET http://localhost:3000/
```

### crear distintas peticiones en un mismo archivo
Para crear varias peticiones en el mismo archivo, usamos 3 hashtags para delimitar una de otra.

```restClient
GET http://localhost:3000/

###

GET http://localhost:3000/products
```

### diferencias entre pet. get y post
Las peticiones con método GET normalmente no llevan un cuerpo con datos, solamente solicitan uno o varios recursos y los obtienen como respuesta.
Al crear una petición POST, debemos agregarle un cuerpo o body, por lo tanto, debemos definir el tipo de contenido de la petición como ==header==.
Esto lo hacemos creando la dirección del recurso, debajo seteando el o los headers correspondientes, y luego dejando una linea vacía, se define el archivo json que se enviará, abriendo llaves, y los pares clave-valor necesarios.
Ejemplo:
```RESTClient
POST {{base_url}}:{{port}}/products
Content-Type:application/json

{
	"nombre":"producto nuevo",
	"precio":17500,
	"categoria":"jugueteria"
}
```

>[!warning] NOTESE
>verificar la linea vacía entre el header y el JSON del cuerpo.
### variables
Podemos definir variables al inicio de nuestro archivo RESTClient, para poder modularizar las rutas y contenidos.
Lo primero que se viene a la mente, es la url. Podemos definir una variable para utilizar la url y luego usarla en nuestras definiciones de peticiones.
Para eso, definimos la variable de la siguiente manera:
```RESTClient
@base_url = http://localhost

@port = 3000
```

luego, puedo llamar a las variables usando la notación de doble llave:
```RESTClient
GET {{base_url}}:{{port}}
```
y esto actuaría como la misma definición que generamos al principio. 
La ventaja es que defino la ruta u hostname en un solo lugar, minimizando errores.

### guardar la respuesta de una peticion en una variable
Podemos definir que al realizar alguna petición, si conocemos la estructura de la respuesta, podamos guardar algún dato en particular.
Ejemplo: si realizo una peticion post, donde se crea un recurso en la API, esta normalmente me devuelve la ID del recurso creado. Podemos guardar ese recurso de la siguiente manera.

```RESTClient
# @name agregarRecurso

POST {{base_url}}:{{port}}/product
Content-Type:application/json

{
	"nombre":"producto nuevo",
	"precio":17500,
	"categoria":"jugueteria"
}
```

y luego, defino para otra petición, usar la respuesta de esta, con el dato que vino...

```RESTClient
# @idRecurso = {{ agregarRecurso.response.body.id }}

PUT {{base_url}}:{{port}}/product/{{idRecurso}}
Content-Type:application/json

{
	"nombre":"producto actualizado",
	"precio":20000,
	"categoria":"nueva categoria"
}
```

### Generar prompts para peticiones dinamicas
Una calidad poderosa de RESTClient, al ser tan liviando y sutil, es poder generar prompts para valores que definamos en la petición.
Para hacer esto, debemos antes de definir la ruta de la petición, setear las variables que nos solicitará por consola de VSCode de la siguiente manera:
```RESTClient
# @name agregarProducto
# @prompt nombre
# @prompt precio
# @prompt categoria
POST {{base_url}}:{{port}}/product
Content-Type:application/json

{
	"nombre": {{nombre}},
	"precio": {{precio}},
	"categoria": {{categoria}}
}

###
```

