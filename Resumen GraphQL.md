

### Creando una query en Graphql

Si tenemos que escribir una query en este lenguaje, vamos a estar solicitando solo los datos que nos importan, por ej.

```js
query {
	person(personID:1) {
		name
		height
		mass
	}
}
```

La respuesta del servidor será:
```js
{
	"data":{
		"person" {
			"name":"Luke Skywalker",
			"height":172,
			"mass":77
		}
	}
}
```

En el primer código, tenemos nuestra query GraphQL. Solicitamos solo los datos necesarios, DISTINTO a un GET tradicional a una API RESTful.
Debajo tenemos la respuesta en formato JSON, desde el servidor.

>Esto nos da a la idea de que estamos recibiendo solamentre la información que estamos solicitando, y por ende, la respuesta es más rápida.

Suponiendo que ahora nos piden solicitar los datos de las películas donde figura Luke Skywalker, no tenemos que solicitarlas una a una, lo hacemos asi. En principio sabemos de antemano que Luke Skywalker es la persona de ID = 1, por lo tanto, en este caso, vamos a reemplazar justamente con este valor entre paréntesis la persona específica que estamos buscando...

```js
query {
	person(personID:1){
		name 
		height
		mass
		filmConnection {
			films {
				title
			}
		}	
	}
}
```

y esto nos devolvería:

```js
{
	"data":{
		"person":{
			"name":"Luke Skywalker",
			"height":172,
			"mass":77,
			"filmConnection":{
				"films": [
					{
						"title":"A new hope"
					},
					{
						"title":"The Empire strikes back"
					},
					{
						"title":"Return of the Jedi"
					},
					{
						"title":"Revenge of the sith"
					}
				]
			}
		}
	}
}
```
Aqui se puede notar que recibimos solamente los datos que estamos buscando en un solo _request_
