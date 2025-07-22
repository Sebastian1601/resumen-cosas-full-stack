

referencia: [SOLID Design Principles Every JavaScript Deveveloper Should Know](https://jsdev.space/solid-design-principles/)

[[#1. Single Responsibility Principle (SRP)| 1. Principio de Responsabilidad Unica]]
[[#2. Open/Closed Principle (OCP)| 2. Principio de Apertura/Cierre]]
[[#3. Liskov Substitution Principle (LSP)| 3. Principio de substitución de Liskov]]
[[#4. Interface Segregation Principle (ISP)| 4. ]]

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

function hacerVolarAlPajaro(pajaro1) {
	pajaro1.volar();
}

const pajaroGenerico = new Pajaro();
const pinguino = new Pinguino();

hacerVolarAlPajaro(pajaroGenerico); // 'Volando'
hacerVolarAlPajaro(pinguino); // Tira ERROR!(Pinguinos no pueden volar) 
```


>[!failure] Qué está mal?
>- la clase Pingüino hereda de Pajaro, pero sobreescribe el método '*volar( )*' de una manera que rompe las espectativas de lo que devuelve el método.
>- La función *hacerVolarAlPajaro( )* asume que cualquier *Pajaro* puede volar, pero eso no es verdad para todas las **subclases**.
>- Esto viola el principio LSP

Esto se resuelve diseñando la estructura de herencia sobre el comportamiento...

```js
class Pajaro {
	ponerHuevo(){
	console.log('Poniendo un huevo');
	}
}

class PajaroVolador extends Pajaro {
	volar() {
		console.log('Volando');
	}
}

class Pinguino extends Pajaro {
	nadar() {
		console.log('Nadando');
	}
}

class Gorrion extends PajaroVolador {}

function hacerVolarAlPajaro(pajaro) {
	pajaro.volar();
}

const gorrion = new Gorrion();
hacerVolarAlPajaro(gorrion); // Volando

```


>[!success] Por qué esto es indudablemente mejor?
>- Una clase separada entre Pajaro y PajaroVolador asegura que solo Pajaros Voladores se pasen en la función *HacerVolarAlPajaro( )*
>-  Un Pinguino es un pájaro, pero no es esperado que vuele.
>- Subclases no rompen el funcionamiento y expectativa seteada por las clases padres.


Notas claves sobre el **LSP** :
 - No sobreescribas metodos en subclases solamente para tirar errores o cambiar el comportamiento drásticamente.
 - Usa interfaces (incluso informalmente, via *duck typing*) para forzar un comportamiento consistente.
 - Diseña alrededor de las posibilidades, no tipos. - Justamente, como separamos las clases *PajaroVolador* de *Pajaro*.

##### 4. Interface Segregation Principle (ISP)

Este principio declara que:

"**Los Clientes no deberían estar forzados a depender de interfaces que no utilizan.** "

Esto, al menos en Javascript, significa que, no hagas que funciones, clases, u objetos implementen cosas que no necesitan. Esto implica que, "rompe" interfaces multipropósitos grandes en otras más pequeñas y específicas para un rol.

Mal ejemplo:

```js
class Maquina {
	imprimir() {
		throw new Error('No implementado');	
	}
	escaner() {
		throw new Error('No implementado');
	}
	fax() {
		throw new Error('No implementado');
	}
}

class ImpresoraVieja extends Maquina {
	imprimir() {
		console.log('Imprimiendo...');
	}
}

//escanear() y fax() no soportados.
```

>[!failure] Qué está mal?
>- *ImpresoraVieja* debe implementar *Maquina*, pero solo soporta el método *imprimir()*
>- Está forzada a heredar métodos (escanear y fax) que no utiliza.
>- Esto puede inducir a errores, confusiones,  y errores de runtime.

Buen ejemplo:

```js
class Impresora {
	imprimir() {
		console.log('Imprimiendo...');
	}
}

class Escaner {
	escanear() {
		console.log('Escaneando...');
	}
}

class maquinaFax {
	fax() {
		console.log('Faxing...');
	}
}

class ImpresoraModerna {
constructor() {
	this.impresora = new Impresora();
	this.escaner = new Escaner();
	this.maquinaFax = new maquinaFax();
}

imprimir() {
	this.impresora.imprimir();
}

escanear() {
	this.escaner.escanear();
}

maquinaFax() {
	this.maquinaFax.fax();1
}
}

class ImpresoraBasica {
constructor() {
this.impresora = new impresora();
}

imprimir() {
	this.impresora.imprimir();
}
}

```

>[!success] Por qué es mejor?
>- Las funciones son modulares, cada interfaz es pequeña y enfocada en su tarea.
>- *ImpresoraBasica* solo depende de las características que soporta.
>- *ImpresoraModerna* tiene capacidades sin ser obligada a heredar métodos no relacionados con su funcionamiento.
>- Ninguna clase es forzada a heredar e implementar más de lo que necesita.


##### 5. Dependency Inversion Principle (DIP)

Módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deberían depender de abstracciones. Las abstracciones no deberían depender de los detalles. Los detalles deberían depender de las abstracciones.

En español:

Tu lógica de negocio principal (código de alto nivel) no debería estar enlazada a los detalles de implementación (*código de bajo nivel como APIs, bases de datos, etc*). En vez de eso, ambos deberían confiar en las interfaces o abstracciones.
Esto promueve la flexibilidad, el testeo, y la separación de finalidades.

Un ejemplo de lo que no se debería hacer.

```js
class MiBaseSQL {
	guardar(data) {
		console.log('Guardando data a mysql:', data);
	}
}

class ServicioUsuario {
	constructor() {
		this.db = new miBaseSQL();
	}

	registrarUsuario(user){
		this.db.guardar(user);
	}
}
```

>[!failure] Qué está mal aqui?
>- *ServicioUsuario* está enlazado estrechamente a *MiBaseSQL*
>- No puedes intercambiar las bases de datos ( cambiar a MongoDB o una API) sin modificar ServicioUsuario.
>- Más dificil de testear - mocking MiBaseSQL requeriría editar la lógica central.


Buen ejemplo:

```js
//abstraccion
class BaseDatos {
	guardar(data) {
		throw new Error('no implementado');
	}
}

//implementación a bajo nivel
class MiBaseDatosSQL extends BaseDatos{
	guardar(data){
		console.log('Guardando data a MySQL:', data);
	}
}

//otra implementacion
class BaseDatosEnMemoria extends BaseDatos {
	constructor() {
		super();
		this.data = [];
	}
	guardar(data) {
		this.data.push(data);
		console.log('Guardada en memoria: ', data);
	}
}

//modulo de alto nivel dependiente de la abstraccion
class ServicioUsuario {
	constructor(basedatos) {
		this.db = basedatos;	
	}
	registrarUsuario(user){
		this.db.guardar(user);
	}
}
```

**USO**:

```js
//1. se crea la instancia de base de datos a usar...
const datab = new MiBaseDatosSQL(); // o new BaseDatosEnMemoria()

//2. Se pasa la instancia de base de datos al crear otra instancia de servicioUsuario
const servicio_usuario = new ServicioUsuario(datab); //se le pasa la base de datos activa

//3. se guarda el usuario, de igual manera, independientemente de qué base de datos  hayamos instanciado.
servicio_usuario.registrarUsuario({ nombre: 'Claudia'});
```


1. Cuales son los principios SOLID?
	SOLID es un acrónimo para cinco principios orientados a diseño de objetos.


