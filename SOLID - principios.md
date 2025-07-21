
Los principios SOLID son guías que ayudan a los programadores a seguir un camino en común, para poder crear código más legible, escalable y mantenible.

Estos 5 principios, nos permiten orientar el código para hacerlo escalable. Los principios SOLID introducidos por **Robert C. Martin**, son 5 reglas escenciales que ayudan a los desarrolladores a organizar mejor el código, reducir bugs y facilitar posibles modificaciones futuras.

#### ¿Qué quiere significar SOLID?

- S - Single Responsibility Principle
- O - Open/Closed Principle
- L - Liskov Substitution Principle.
- I - Interface Segregation Principle
- D - Dependency Inversion Principle

##### 1. Single Responsibility Principle (SRP)

"*Una clase, módulo o función, debería tener una única razón para cambiar.*"

En principio, se dice que esto significa que una función, clase o módulo, debería realizar una sola tarea. Esto hace el código legible, más fácil de testear y mantener.
Según lo leído en otros artículos, no es tan así, por lo que queda leer el libro de Clean Code para interpretar a qué se refiere el autor con respecto a este principio.

Un ejemplo de una función que no aplica el principio de SRP.

```js
function procesarRegistroUsuario(userData){
//1.validar el input
if(!userData.email.includes('@')){
throw new Error('Email Inválido');
}

//2.guardar usuario a la base de datos(simnulado)
const userId = Math.floor(Math.random()*1000);

//3.enviar email de bienvenida(simulado)
console.log(`Enviando email de bienvenida al usuario ${userData.email}`);

return userId;
}
```

>[!failure] Porqué esto está mal
>- Valida datos
>- Guarda datos
>- Envía un correo
>Todo esto en la "misma función".


```js
function validarUsuario(userData){
if(!userData.email.includes('@')) {
	throw new Error('Email inválido');
}

function guardarUsuarioBaseDatos(userData){
	const userId = Math.floor(Math.random()*1000);
	//simular la llamada a la base de datos
	console.log(`Usuario guardado con ID ${userId}`);
	return userId;
}

function enviarMailBienvenida(email){
	console.log(`Enviando mail de bienvenida a ${email}`);
}

function registrarUsuario(userData){
	validarUsuario(userData);
	const userId = guardarUsuarioBaseDatos(userData);
	enviarMailBienvenida(userData.email);
	return userId;
}
}
```

>[!success] Beneficios
>- Cada función tiene un propósito claro y definido.
>- Más fácil de testear modular e independientemente.
>- Si la lógica del mail cambia, solo se actualiza la función enviarMailBienvenida()

Incluso en pequeños proyectos de JS, SRP guía a mejor disciplina de código y un mantenimiento a largo plazo. Siempre tenemos que preguntarnos **¿Esta función se dedica a hacer SOLO una tarea?**, si la respuesta es **NO**, entonces hay que **factorizar**.

##### 2. Open/Closed Principle (OCP)

El segundo principio de SOLID, ocp, afirma lo siguiente:

"*Las entidades de software deberían estar abiertas para extensión, pero cerradas para modificación.*"

En términos simples, deberías poder agregar funcionalidad extra sin tener que cambiar el código existente. Este acercamiento reduce el riesgo de introducir nuevos bugs y promueve la reusabilidad y la flexibilidad  del código. 

Ejemplo de mal código
```js
function obtenerPrecioConDescuento(tipoUsuario, precio){
	if (tipoUsuario === 'regular') {
		return price * 0.9;
	} else if (tipoUsuario === 'vip') {
		return price * 0.8;
	} else if (tipoUsuario === 'platinum') {
		return price * 0.7;
	} else {
		return price;
	}
}
```

>[!failure] Qué está mal?
>- Cada vez que se ingresa un nuevo tipo de usuario(ej: "gold"), habrá que *modificar* la función existente.
>- Esto rompe el principio de OCP, dado que cambia la función original arriesgando la funcionalidad.
>- La lógica está acoplada de manera muy fina y no es extensible.


Un buen ejemplo:

```js
class estrategiaDescuento {
	obtenerDescuento(precio) {
		return precio;}
}

class descuentoClienteRegular extends EstrategiaDescuento {
	obtenerDescuento (price) {
		return price * 0.9;
	}
}

class descuentoClienteVIP extends EstrategiaDescuento {
	obtenerDescuento (price) {
		return price * 0.8;
	}
}

class descuentoClientePlatinum extends EstrategiaDescuento {
	obtenerDescuento (price) {
		return price * 0.8;
	}
}

//ejemplo de uso
function obtenerPrecioDescuento (estrategiaDescuento1, price){
	return estrategiaDescuento1.obtenerDescuento(price);
}

const cliente = new descuentoClienteVIP();
console.log(obtenerPrecioDescuento(cliente, 100)); // retorna 80.

```

Creando una clase general para el precio común(sin descuento), y luego una clase para cada cliente, facilita que al usar la función *obtenerPrecioDescuento*, le pasemos el objeto cliente que es de clase VIP, y esto automáticamente genera el descuento con el precio al 80% de lo pasado (100).

>[!success] Porqué es mejor este código?
>- Te permite añadir nuevas estrategias de descuento creando nuevas clases que extiendan a ==estrategiaDescuento== , sin tener que modificar el código existente.
>- Esto adhiere al OCP: la función **obtenerPrecioDescuento()** está **cerrada** a modificación, sin embargo, permanece **abierta** para la extensión de usar otras clases, a través del **polimorfismo**.
>- La lógica es limpia, separada y más fácil de probar o extender.

##### 3. Liskov Substitution Principle (LSP)

Este principio especifica que:

"**Objetos de una superclase, deberían ser reemplazables con objetos de una subclase sin afectar el funcionamiento del programa.**"

En términos más simples, las subclases deberían comportarse como su clase padre. Si debes chequear el tipo de un objeto o sobreescribir métodos en una manera que rompa el comportamiento esperado, seguramente estás violando el LSP.

Veamos un ejemplo:

```js
class Pajaro {
	volar() {
		console.log('Volando');
		}
}

class Pinguino extends Pajaro {
	volar() {
		throw new Error("Pinguinos no pueden volar!");
	}
}
```