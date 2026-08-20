  ---
   
Arquitectura Multi-tenant (multi inquilinos)

Este diseño lógico y físico de una app en la nube está pensado para compartirse entre múltiples clientes (tenants) mediante una suscripción periódica, garantizando seguridad, aislamiento de datos y alta escalabilidad.

- **Capa de cliente (frontend)**: interfaz web o móvil de acceso rápido mediante navegadores, optimizada con redes de distribución de contenido (CDN).
- **Puerta de enlace (API Gateway)**: Punto de entrada único que enruta peticiones, maneja el control de acceso y detecta el identificador de cada *tenant*
- **Capa de lógica (backend)**: Servicios modulares o microservicios que procesan las reglas de negocio de forma independiente.
- **Capa de Datos (Base de datos)**: Almacenamiento central o distribuido adaptado al modelo de multi-tenencia elegido.

Modelos de multi-tenants
- **Base de datos compartida, esquemas compartidos:** Todos los clientes usan las mismas tablas; un campo `tenant_id` separa los registros. Es económico y fácil de iniciar, pero más complejo de auditar.
- **Base de datos compartida, esquemas separados:** Cada cliente tiene su propio esquema dentro de la misma instancia de base de datos. Ofrece un mejor aislamiento lógico.
- **Base de datos dedicada (Single-tenant):** Cada cliente grande o corporativo posee su propia infraestructura exclusiva por motivos de seguridad estricta o cumplimiento normativo.

**Buenas prácticas de diseño**

- **Seguridad y Aislamiento:** Validar el contexto del _tenant_ en cada petición para evitar filtraciones de datos entre cuentas.

- **Escalabilidad horizontal:** Diseñar los servicios sin estado (_stateless_) para añadir recursos de cómputo de manera automática según la demanda.

- **Observabilidad:** Monitorear logs, métricas y rendimiento por usuario o empresa para detectar cuellos de botella rápidamente. 

![vide](https://www.youtube.com/watch?v=B8qMVVgj0uM&t=332)

---


# Diseño de sistEmas


![[Pasted image 20260819202353.png|700]]

El primer paso es construir un sistema para un usuario único para luego escalarlo e ir entendiendo como las desiciones y aplicaciones afectan al rendimiento y nuestro producto.

## entendiendo el camino de una solicitud

1. El camino inicia desde el cliente, siendo este un navegador web o una app móvil. Estos clientes tienen la dirección web de nuestro servicio, y la ingresan. 
2. Al ingresar y consultar el DNS sobre esta dirección, el servidor le indica que tiene una IP asignada para dicho dominio, el cual corresponde a **172.16.254.254**.
3. El cliente, recibe esta información y realiza una solicitud HTTP a dicha IP, lo cual genera una respuesta de nuestro servidor que está alojado, escuchando y respondiendo a las *request* entrantes, con datos html o incluso json, lo que sea que le indiquemos que envíe de vuelta.

![[Pasted image 20260819202642.png|700]]

Para el cliente web, el servidor maneja la lógica de negocio [bussiness logic], el guardado de datos[data storage] y la presentación usando HTML, CSS y Javascript.

Para el cliente móvil app, normalmente los datos son requeridos al servidor mediante llamadas *API* y las respuestas normalmente se dan a través del formato JSON.

>[!example] Ejemplo de una API call
>GET /products/:id - obtiene detalles para el producto ID = 456
>.
>La respuesta sería
>```json
>{
>	"productId": 456,
>	"name":"Wireless Headphones",
>	"description":"Noise-cancelling headphones",
>	"categories":[
>		"electronics",
>		"audio"
>	],
>	"seller":{
>		"id":34,
>		"name":"ElectroMart",
>		"rating":4.8
>	}
>}
>```

>**Identificando en qué areas un único servidor se queda corto para manejar demandas de muchos usuarios.**

Inicialmente, a medida que la cantidad de usuarios crece, podemos pensar en separar de nuestro server principal, el manejo de la base de datos. Entonces, tendríamos el server principal para presentación HTML, CSS y Js, junto con el caché, y por otro lado, un server encargado de manejar la base de datos, quedando el esquema de la siguiente manera:

![[Pasted image 20260819213720.png|700]]

Este tipo de escalado nos permitirá aumentar la necesidad de cada servidor de acuerdo a la demanda que tenga cada uno.

## SElEccionar la base de datos correcta

Al desarrollar una web app de este estilo, nos preguntaremos, qué tipo de base de datos nos conviene, y ahi tenemos dos opciones principales, que tienen varios componentes cada una.

### Base de datos relacionales
Las bases de datos relacionales son aquellas que permiten relacionar información en distintas tablas y nos permiten asociar un dato con otro y presentarnos información con esa característica particular.
Tenemos entre otras las principales opciones:
- PostgreSQL
- MySQL
- SQLite
- Oracle Database

Estas bases utilizan el lenguage SQL para generar las consultas que resultan en información si corresponde.
Van organizadas en tablas con filas y columnas.
- Soportan JOIN de datos complejos (relacionan los mismos de acuerdo a la necesidad)
- Proveen integridad de los datos y consistencia, especialmente con las **transacciones**.
  Se basan en el principio **ACID** que significa
	- **Atomicity**: La transacción es tratada como una unidad, lo cual implica que todos los pasos se **completan** o si uno falla, toda la transacción **falla**.
	- **Consistency**: Se parte de un estado válido de los datos y se llega a otro estado válido de los mismos, siguiendo todas las reglas y constraints declarados en la base.
	- **Isolation**: La transacción se aisla completamente de otras transacciones, lo cual implica que dos transacciones funcionando al mismo tiempo, no se interfieren una con otra. El trabajo simultáneo figura haber sucedido en orden, uno después de otro.
	- **Durability**: Los datos permanecen correctos en caso de algún tipo de falla en el sistema. Si la tarea a realizar se logra, los datos están a salvo, sino, no interfieren o dejan inconsistencias en los mismos.

>[!info] **¿ Cuando usar una base de datos relacional ?**
>- Cuando tenemos que manejar información bien estructurada y con relaciones claras y necesarias.
>- Cuando tenemos que manejar datos sensibles y que urgen de la integridad y consistencia de los mismos

### Base de datos no-relacionales
Este tipo de base de datos nos permiten acceder a muchos datos sin relación entre si, pero con gran volúmen de los mismos.
Las opciones más usadas son:
- Kassandra [Wide-colum stores]
- MongoDB [document stores]
- Redis [key-value stores]
- Neo4j [graph stores]

Document Stores:
	Los datos se guardan en documentos estilo *JSON*, por lo que la estructura puede ser variable, no sigue una regla predefinida de los datos a guardar.

Wide-Column stores:
	Los datos se guardan en tablas con filas que a su vez, tienen filas y columnas. Permiten manejar cantidades masivas de datos y son buenas para muchas escrituras de datos.

Graph Stores:
	

Key-value Stores:
	Se guarda la información en pares de key-values, normalmente escritas en la RAM, por lo que son muy rapidas de acceder.

>[!info] **¿ Cuando usar una base de datos NO - RELACIONAL ?**
>- Cuando tenemos que manejar información con mucha velocidad, poca latencia para respuestas rápidas.
>- Cuando los datos no están estructurados o semi-estructurados y las relaciones no son importantes
>- Cuando necesitamos escalar nuestro almacenamiento con grandes cantidades de datos

## Escalando nuestra aplicación

Al momento de necesitar escalar nuestro server debido a la cantidad de usuarios o consultas que maneja, tenemos dos acercamientos

- Vertical scaling
- Horizontal scaling

### Vertical Scaling
Cuando hablamos de vertical scaling, estamos hablando de mejorar el hardware de nuestro servidor. Podemos agregarle más RAM, Almacenamiento, poder de procesamiento, etc.
Esto funciona en aplicaciones de poco a mediano tráfico. Sin embargo, hay un limite de hardware implícito que se da cuando no podemos agregar más recursos al servidor, todo es limitado con respecto al hardware, por lo que habrá un punto máximo que pueda manejar el servidor. La otra desventaja es la "falta de redundancia", esto significa que si el server se cae o sucede algo, la aplicación no funciona hasta que el server vuelva a responder.

### Horizontal scaling
El horizontal scaling se refiere a manejar más servidores activos respondiendo a la misma cantidad de solicitudes que lo hacíamos con uno solo. Esto implica que si uno de los servers se cae, los restantes pueden seguir sirviendo a los clientes hasta que el que no funciona responda nuevamente o se repare. También de esta manera no existe limite a la cantidad de servers que puedes agregar, por lo que puedes tener 10 servidores atendiendo a tu sistema, dividiendo las peticiones entre ellos para aliviar el trabajo de cada uno.

**LOAD BALANCER**
Esto implica que aparte de los servidores, hay que implementar un **load balancer** que es el que maneja el tráfico y lo distribuye entre los servidores respondiendo. Aparte, si uno de los servidores se cae, el load balancer deja de enviar solicitudes a ese servidor.
Ejemplos de load balancer son:
- Equipos físicos especializados como por ejemplo máquinas específicas marca F5 o Cisco
- Un servidor con software: corre un programa en una pc o en la nube, por ejemplo **Nginx** o **HAProxy**
- Un bloque de código o servicio virtual: esto es un programa pequeño o servicio en la nube que hace el trabajo. Un ejemplo de esto es el servicio que da Amazon Web Services o un código propio diseñado para tal fin.

![[Pasted image 20260819221135.png|700]]


### 7 Estrategias y algoritmos usados al balancear las cargas

#### Round Robin
Es la manera más común para dirigir el tráfico entre servidores. La idea es que se van asignado según entran las peticiones una a una a cada server distinto. Si tenemos 3 servidores, A, B y C:
- el primer request se asigna al server A.
- el segundo se asigna al B
- el tercero al C
- el cuarto request se vuelve a asignar al server A y así sucesivamente.
Esto funciona bien siempre y cuando nuestros servidores tengan especificaciones técnicas similares y por consiguiente, capacidad.

#### algoritmo de "Least connections"
Este algoritmo busca identificar qué server está atendiendo la menor cantidad de conexiones activas.
Si el server A tiene 10 conexiones activas, 
el B tiene 9
y el C tiene 30
La siguiente conexión se asignará al server B, y de entrar otra más, nuevamente se asignara al B o al A dado que ambos tienen 10 en ese momento.
Esto es particularmente útil para servidores que manejan *conexiones activas de distinta duración*, dado que según lo que dure la sesión de una conexión, esta puede ocupar y liberar el servidor rápido, y otras no, por lo que ahi se hace útil la verificación de conexiones activas al momento de asignar la siguiente.

#### Algortimo DE "least response time"
Este algoritmo se basa en dirigir hacia el servidor con menor tiempo de respuesta las solicitudes, y balancear la cantidad de las mismas si es que el servidor con menor tiempo de respuesta se carga con muchas request dado su tiempo de respuesta.
Si tenemos 3 servidores, A, B y C y la siguiente disposición:
- Server A - mejor tiempo de respuesta y 30 conexiones activas.
- Server B - peor tiempo de respuesta y 10 conexiones.
- Server C - tiempo de respuesta medio con 20 conexiones.

el balanceador dirigirá cierta cantidad de conexiones al server A, luego al C para aumentar la cantidad de conexiones ahi, mientras que las conexiones de A bajan, y finalmente, si es necesario, dirigir a B las restantes.

Esta opción es particularmente útil cuando tenemos Servers diferentes con distintas especificaciones técnicas, que genera la diferencia en los tiempos de respuesta y capacidad de manejar requests.

#### IP Hash
Este método se utiliza tomando la IP del cliente, generando el hash de la misma, y con esto dirigiendo al server correspondiente al hash. Esto genera que las solicitudes siguientes, tengan el mismo hash y se redirijan al mismo server donde se inició la conexión principal. Esto es particularmente útil cuando el cliente guarda información en ese server al que accedió la primera vez, y luego, debe conectarse al mismo para tener los datos disponibles de acuerdo a su IP.

#### Weighted algorithms
Estos algoritmos son versiones particulares de los algoritmos anteriores, donde se determinan más parámetros para dirigir las requests a ciertos servers en particular.

#### Algoritmos geográficos
Estos algoritmos verifican la región de donde está viniendo las solicitudes, y redirigen las mismas según la ubicación del cliente y los servidores disponibles más cercanos (obviamente en este caso, disponemos de servers en distintas regiones para implementar estos algoritmos, sino no tienen sentido).

#### Consistent hashing
Este algoritmo utiliza una función de hashing, que determina, de acuerdo a la IP del cliente, una zona en la que siempre caerá el hash de su IP, garantizando que esto determinará que la conexión o solicitud, terminará siempre en el mismo server al cual se conectó siempre. 
Este método garantiza que los datos del hash no se recalculen al momento de agregar otro server, por lo que garantizan un movimiento mínimo de datos del hash, sumando asi garantías para una alta escalabilidad y estabilidad del sistema.

El funcionamiento depende de un "anillo virtual" llamado "hash ring", el cual se basa en una función hash criptográfica que define un rango fijo de salida de valores enteros. Este espacio contínuo de valores, se juntan desde el valor más bajo al más alto, formando un "anillo lógico".
Se ubican los servidores de acuerdo a un mapeo de sus posiciones en este "anillo lógico" de acuerdo a su IP o nombre de dominio.

Cuando una llave de datos necesita ser escrita o leída, el ssitema hashea la llave para encontrar su posición en este anillo. El sistema viaja contrareloj en el anillo hasta encontrar el valor del primer server cercano. Asi se asigna el server al host o para procesar la request.

Si se agrega un server, este toma los valores cercanos de las keys encontradas inmediatamente contrareloj desde su posición. Los nodos restantes del cluster no son afectados.

Si se desafecta un server, su trabajo se transfiere al server más cercano contrareloj de su posición, los demás datos del cluster no son afectados y tampoco migrados.

### Chequeos de salud (HeALT CHECKS)

EL load balancer verificar también que todos los servers en su lista estén activos para poder derivarles las solicitudes. Esto lo hacen mediante una request de chequeo de salud, por lo que cada server le responderá sobre su propio estado.
Cuando un server no responde o responde con deficiencia, el **load balancer** evita enviar solicitudes a ese equipo, y se deriva a otro server hasta que el server reporte el funcionamiento correcto nuevamente.

---

### SPOF (single point of failure)

Se determina como SPOF a cualquier componente que al fallar, deja asilado al sistema o no deja funcionar correctamente el mismo.
Digamos que tenemos los clientes, tanto web como móvil, conectándose a un único LOAD BALANCER que redirige las solicitudes a nuestros 10 servidores preparados que habiamos escalado para manejar tanta concurrencia. Estos servers a su vez, se conectan todos a una misma base de datos para obtener la información de las responses.

El primer **SPOF** se encuentra en el único **LOAD BALANCER** que tenemos activo. Si ese equipo queda desafectado por alguna falla, no importa tengamos 10 o 100 servidores, ninguno responderá a una solicitud porque los clientes no pueden llegar a ninguno de ellos.
Lo mismo pasa con la única base de datos que tenemos luego de los servers en la arquitectura. Si la base sostiene alguna falla o desperfecto, no importa qué cantidad de servers tengamos, la información no podrá ser recuperada para ninguno de ellos, generando que la app o sitio queden completamente caídos.

Aqui entra la redundancia en los **LOAD BALANCER**. Al agregar dos, tenemos la posibilidad de que si uno de ellos cae o es atacado con incontables solicitudes, el otro quede funcionando y redirigiendo las peticiones hasta que el primero se reponga y funcione nuevamente.
Se pueden hacer chequeos de salud en los mismos y monitoreo para evitar la caída en lo posible.

Esto eleva la pregunta, qué pasa si el equipo o sistema que redirige el tráfico a uno u otro LB falla, ¿estamos creando otro SPOF "más cercano al cliente" en la conexión?
La respuesta es, el SPOF nunca se evita por completo, sólo se traslada a equipos o estructuras más robustas.

---

## API design

**¿Qué es una API (Application Programming Interface)?**
Una API define un contrato sobre cómo deben comunicarse e interactuar dos sistemas de software y la estructura de la respuesta que se dará al tener una consulta.

![[Pasted image 20260820001011.png|700]]

VOY POR EL MINUTO 30 del video


----


![system design](https://www.youtube.com/watch?v=oYxTTirKY8M)


---
---


## Cache para el diseño de sistemas

![videoCache](https://www.youtube.com/watch?v=ETvLl-8bPbo)

