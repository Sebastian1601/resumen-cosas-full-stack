
En documentos de planillas de cálculo, conocidos como *Google sheets* podemos definir scripts que van desde meros calculos hasta crear nuevos menús con implementaciones complejas.

Para agregar una ventana flotante (cuadro de diálogo personalizado) en **Google Sheets** que te permita almacenar y consultar información importante rápidamente, ==debes usar **Google Apps Script**==.

La forma más eficiente de lograrlo es creando una barra lateral (**Sidebar**), ya que se mantiene fija a la derecha de la pantalla y te permite seguir editando la hoja principal de forma simultánea.

A continuación, tienes el código y los pasos para instalarlo:

### Paso 1: Pegar el código en Apps Script
1. Abre tu documento de [Google Sheets](https://sheets.google.com/).
2. En el menú superior, ve a **Extensiones** > **Apps Script**.
3. Borra el código existente en el archivo `Código.gs` y pega lo siguiente:
```js
// Crea el menú personalizado al abrir la hoja de cálculo 
function onOpen() {
	SpreadsheetApp.getUi() 
		.createMenu('⚙️ Panel de Notas')
		.addItem('Abrir Notas Importantes', 'mostrarSidebar')
		.addToUi();
}

// Muestra la ventana flotante lateral (Sidebar) 
function mostrarSidebar() {
	var html = HtmlService.createHtmlOutputFromFile('Sidebar')
	.setTitle('Notas Importantes')
	.setWidth(300);
	
	 SpreadsheetApp.getUi().showSidebar(html); 
 } 
 
 // Guarda la nota en las propiedades del documento (oculto y persistente) 
function guardarNota(texto) {
	var propiedades = PropertiesService.getDocumentProperties();
	propiedades.setProperty('nota_importante', texto);
	return "¡Nota guardada con éxito!"; 
 }

// Recupera la nota guardada 
function obtenerNota() {
	var propiedades = PropertiesService.getDocumentProperties();
	return propiedades.getProperty('nota_importante') || ""; 
}
```


### Paso 2: Crear la interfaz visual (HTML)
1. Dentro de la ventana de Apps Script, haz clic en el botón **`+`** (Añadir un archivo) junto a "Archivos".
2. Selecciona **HTML** y ponle el nombre exacto de **`Sidebar`** (se guardará como `Sidebar.html`).
3. Borra el código por defecto y pega este diseño limpio y accesible:

```html
<!DOCTYPE html>
<html>
<head>
<base target="_top">
<style> 
	body { font-family: 'Arial',sans-serif;
	padding: 12px;
	color: #333; 
	background-color: #f9f9f9; 
	} 
	
	h3 {
	 margin-top: 0; 
	 color: #1b5e20; 
	 } 
	
	textarea {
	width: 100%; 
	height: 180px; 
	box-sizing: border-box; 
	padding: 8px; 
	border: 1px solid #ccc; 
	border-radius: 4px; 
	resize: vertical; 
	font-size: 13px; 
	} 
	
	button { 
	width: 100%; 
	background-color: #1e7e34; 
	color: white; 
	padding: 10px; 
	border: none; 
	border-radius: 4px; 
	cursor: pointer; 
	font-size: 14px; 
	margin-top: 10px; 
	font-weight: bold;
	} 
	
	button:hover { 
	background-color: #155724; 
	} 
	
	#estado { 
	margin-top: 8px; 
	font-size: 12px; 
	color: #28a745; 
	text-align: center; 
	font-weight: bold; 
	} 
	
</style>
</head>
<body>
	<h3>📌 Información Clave</h3> 
	<p style="font-size: 12px; color: #666;">Escribe aquí los datos importantes que necesites tener a la mano de forma permanente.</p> 
	<textarea id="txtNota" placeholder="Escribe tus notas aquí..."></textarea> 
	<button onclick="guardar()">💾 Guardar Información</button> 
	<div id="estado"></div> 
	<script> // Cargar la nota guardada automáticamente al abrir la ventana 
	window.onload = function() { google.script.run.withSuccessHandler(function(nota) { document.getElementById('txtNota').value = nota; }).obtenerNota(); }; 
	// Función para enviar la nota al backend de Google Sheets 
	function guardar() { var texto = document.getElementById('txtNota').value;
	document.getElementById('estado').innerText = "Guardando..."; 
	google.script.run.withSuccessHandler(function(mensaje) { 
	document.getElementById('estado').innerText = mensaje; setTimeout(function() { 
	document.getElementById('estado').innerText = ""; }, 3000);})
	.guardarNota(texto); } 
	</script> 
</body> 
</html>
```

### Paso 3: Guardar y Ejecutar
1. Haz clic en el icono del **Disco (Guardar proyecto)** en la barra de herramientas de Apps Script.
2. Cierra la pestaña de Apps Script y regresa a tu hoja de cálculo de Google.
3. **Recarga la página** del navegador (F5).
4. Verás que aparece un nuevo menú arriba llamado **`⚙️ Panel de Notas`**. Haz clic en él y selecciona **`Abrir Notas Importantes`**.
5. _Nota:_ La primera vez que lo abras, Google te pedirá **"Autorización de acceso"**. Concédele los permisos necesarios (haz clic en _Configuración avanzada_ y luego en _Ir a Proyecto (no seguro)_) para que el script pueda guardar los textos.

¿Te gustaría realizar alguna modificación al panel, como **agregar un segundo cuadro de texto**, hacer que los datos se guarden **en una celda específica de la hoja** en lugar de ocultos, o que **se abra automáticamente** cada vez que entras al archivo?

----

## Version en producción
1. Agregar menú en barra de menu Archivo en `codigo.gs`
```js
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  ui.createMenu('Registro de botmaker')
    .addItem('Registrar nueva llamada', 'mostrarVentanaFlotante')
    .addToUi();
};

function mostrarVentanaFlotante() {
  var html = HtmlService.createHtmlOutputFromFile('ventanaRegistro')
    .setWidth(440)
    .setHeight(800)
    .setTitle('📌 Registro de llamada botmaker');
  SpreadsheetApp.getUi().showModelessDialog(html, ' ');
}

// Función que recibe los datos de la ventana y los guarda en la hoja
function guardarDatos(data) {
  if (!data) return;
  //obtengo el libro actual y busco la hoja llamada "botmaker"
  var libro = SpreadsheetApp.getActiveSpreadsheet();
  var hojaRegistro = libro.getSheetByName("botmaker");
  //verifico cuál es la primer fila vacia
  var ultimaFilaActiva = hojaRegistro.getLastRow();
  //si la ultima fila es la 0, arranco en la 1, sino le sumo 2 a la ultima fila escrita
  var filaAEscribir = ultimaFilaActiva === 0 ? 1 : ultimaFilaActiva + 2;
  
  var { tecnico,
    tramite,
    cliente,
    userpppoe,
    useriptv,
    telefono,
    puertoActual,
    puertoNuevo,
    medicionActual,
    medicionNueva,
    onuActual,
    onuNueva,
    stbActual,
    stbNuevo
  } = data;

  var fecha = new Date();
  
  //en este array, se define, de acuerdo a la cantidad de columnas y filas, como será la estructura de datos insertada con cada ingreso del formulario.
  var MODELODATOS = [
    ["Fecha", "Técnico", "Trámite", "Cliente", "Puerto Actual", "Medicion", "Puerto Nuevo", "Medicion"],
    [fecha, tecnico, tramite || "vacio", cliente || "vacio", puertoActual || "vacio", medicionActual || "vacio", puertoNuevo || "vacio", medicionNueva || "vacio"],
    ["User PPPoE", "User IPTV", "Teléfono", , "Onu Actual", "Onu Nueva", "STB Actual", "STB Nuevo"],
    [userpppoe || "vacio", useriptv || "vacio", telefono || "vacio", , onuActual || "vacio", onuNueva || "vacio", stbActual || "vacio", stbNuevo || "vacio"]
  ];

  var filasInsertar = MODELODATOS.length;
  var columnasInsertar = MODELODATOS[0].length;

  hojaRegistro.getRange(filaAEscribir, 1, filasInsertar, columnasInsertar)
    .setValues(MODELODATOS);
};
```

2. Crear el html para mostrar la ventana flotante dentro de la planilla en el archivo `ventanaRegistro.html`

```html
<!DOCTYPE html>
<html>
<head>
  <base target="_top">
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 10px;
      background-color: #f9f9f9;
      display:flex;
      flex-flow:column no-wrap;
      justify-item:center;
    }
    label {
      font-size: 14px;
      color: #333;
    }
    textarea {
      width: 93%;
      height: 80px;
      margin-top: 8px;
      margin-bottom: 12px;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
      resize: none;
    }
    button {
      width: 75%;
      background-color: #1a73e8;
      color: white;
      border: none;
      padding: 10px;
      font-size: 14px;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #1557b0;
    }
    .exito {
      color: green;
      font-size: 12px;
      text-align: center;
      margin-top: 5px;
      display: none;
    }
    label {
      padding:2px 5px;
      text-align:right;
      width:150px;
    }
    input {
      border:none;
      border-radius:3px;
    }
    span {
      display:flex;
      flex-flow:row no-wrap;
      margin:5px;
    }
  </style>
</head>
<body>
  <form id="formulario">
    <span>
    <label for="tecnico">Tecnico: </label>
    <input id="tecnico" placeholder="nombre del técnico">
    </span>
    <span>
    <label for="tramite">Nro Trámite: </label>
    <input id="tramite" placeholder="nro trámite">
    </span>
    <span>
    <label for="cliente">Datos del cliente: </label>
    <input id="cliente" placeholder="nro, nombre y apellido">
    </span>
    <span>
    <label for="userpppoe">User PPPoE: </label>
    <input id="userpppoe" placeholder="usuario de internet">
    </span>
    <span>
    <label for="useriptv">user TOR IPTV: </label>
    <input id="useriptv" placeholder="Usuario TOR">
    </span>
    <span>
    <label for="telefono">Telefono: </label>
    <input id="telefono" placeholder="nro de telefono cliente">
    </span>
    <span>
    <label for="puertoActual">Puerto Actual: </label>
    <input id="puertoActual" placeholder="puerto de la central">
    </span>
    <span>
    <label for="medicionActual">Medicion Actual: </label>
    <input id="medicionActual" placeholder="medicion fibra">
    </span>
    <span>
    <label for="puertoNuevo">Puerto Nuevo: </label>
    <input id="puertoNuevo" placeholder="nuevo puerto central">
    </span>
    <span>
    <label for="medicionNueva">Medicion Nueva: </label>
    <input id="medicionNueva" placeholder="medicion fibra">
    </span>
    <button type="submit" id="subir">Guardar datos en hoja "botmaker"</button>
    <div id="mensaje" class="exito">¡Guardado con éxito!</div>
  </form>
  <script>
    const formulario = document.querySelector("#formulario");
    formulario.addEventListener("submit", enviarDatos);
    function enviarDatos(e) {
      console.log("Enviando datos");
      e.preventDefault();  
      let nombre = document.querySelector("#tecnico").value;  
      let tecnico = document.querySelector("#tecnico").value;
      let tramite = document.querySelector("#tramite").value;
      let cliente = document.querySelector("#cliente").value;
      let userpppoe = document.querySelector("#userpppoe").value;
      let useriptv = document.querySelector("#useriptv").value;
      let telefono = document.querySelector("#telefono").value;
      let puertoActual = document.querySelector("#puertoActual").value;
      let medicionActual = document.querySelector("#medicionActual").value;
      let puertoNuevo = document.querySelector("#puertoNuevo").value;
      let medicionNueva = document.querySelector("#medicionNueva").value;
      let data = {
         tecnico,
         tramite,
         cliente,
         userpppoe,
         useriptv,
         telefono,
         puertoActual,
         medicionActual,
         puertoNuevo,
         medicionNueva
        };
        //Deshabilita el botón mientras procesa
        document.querySelector('button').disabled = true;
        // Llama a la función de Google Apps Script
        google.script.run
          .withSuccessHandler(function() {
            //document.getElementById('tecnico').value = ""; // Limpia el cuadro
            document.querySelector('button').disabled = false;
            var msg = document.getElementById('mensaje');
            msg.style.display = "block";
            setTimeout(function() { msg.style.display = "none"; }, 2500); // Oculta el mensaje de éxito
          })
          .guardarDatos(data); //esta linea le pasa a la función definida en el otro archivo "guardarDatos" el objeto con toda la información a procesar.
          }
  </script>
</body>
</html>
```

## Script para verificar ciertas columnas y pasarle un ancho definido.


```js
function copiarMenusDesplegables() {
  var hojaOrigen = "DUPLICADO"; // Nombre de la hoja donde están las reglas originales
  var rangoOrigen = "H2:H100"; // Rango donde están las reglas de menú desplegable
  var hojasDestino = ["1", "2", "3"];
  //Array.from({length:32},(_,i)=>i);  Nombres de las hojas donde copiarás las reglas
  var rangoDestino = "H2:H100"; // Rango destino donde aplicar las reglas en cada hoja
  // Obtiene la hoja activa y el rango original
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var hoja = ss.getSheetByName(hojaOrigen);
  var reglas = hoja.getRange(rangoOrigen).getDataValidations();
  // Aplica las reglas en las hojas destino
  hojasDestino.forEach(function(nombreHoja) {
    var hojaDestino = ss.getSheetByName(nombreHoja);
    if (hojaDestino) {
      hojaDestino.getRange(rangoDestino).setDataValidations(reglas);
    }
  });
}
```



```js
function modificarColumnasPrincipales() {
  var hojaOrigenCambios = "DUPLICADO";
  
  //defino el array para revisar las páginas según su nombre, que en este caso, son strings que van del 1 al 31.
  var hojasDestino = Array.from({ length: 31 }, ((_, i) => `${i + 1}`));
  
  //cambiar para definir el rango de columnas de las cuales tomar el cambio de ancho.
  var rango = 'A1:P1';
  //obtengo la hoja, el rango de celdas a obtener las medidas del ancho, y los guardo en "anchos".
  var HojaActiva = SpreadsheetApp.getActiveSpreadsheet();
  var hoja = HojaActiva.getSheetByName(hojaOrigenCambios);
  var rangos = hoja.getRange(rango);
  var cantidadColumnas = rangos.getNumColumns();
  var anchos = [];
  for (var i = 0; i < cantidadColumnas; i++) {
    var valorAncho = hoja.getColumnWidth(rangos.getColumn() + i);
    anchos.push(valorAncho);
  };

  console.log(anchos);
  console.log(hojasDestino);
  
  hojasDestino.forEach(function (nombreHoja) {
    var hojaDestino1 = HojaActiva.getSheetByName(nombreHoja);
    if (hojaDestino1) {
      for (var i = 0; i < cantidadColumnas; i++) {
        console.log(i, 'ancho:', anchos[i]);
        hojaDestino1.setColumnWidth(i+1, anchos[i]);
      };
    };
  });
}
```

## 1. Clases de Automatización y Ecosistema (Services)
Son los objetos globales exclusivos que sirven como puerta de entrada para manipular cada herramienta de Google sin necesidad de configurar APIs manualmente. [[1](https://developers.google.com/apps-script/overview?hl=es-419), [2](https://developers.google.com/apps-script/guides/services)]

| Clase Global     | Propósito Exclusivo                                              | Ejemplo de Método Clave                             |
| ---------------- | ---------------------------------------------------------------- | --------------------------------------------------- |
| `SpreadsheetApp` | Control total de Google Sheets.                                  | `.getActiveSpreadsheet()` / `.getRange()`           |
| `DocumentApp`    | Manipulación de Google Docs.                                     | `.getActiveDocument()` / `.getBody()`               |
| `GmailApp`       | Lectura, búsqueda y envío de correos desde Gmail.                | `.sendEmail(to, subject, body)` / `.search()`       |
| `DriveApp`       | Gestión del almacenamiento, carpetas y permisos en Google Drive. | `.createFile(name, content)` / `.getFolderById(id)` |
| `CalendarApp`    | Gestión de calendarios, eventos e invitaciones.                  | `.getDefaultCalendar()` / `.createEvent()`          |
| `FormApp`        | Creación y lectura de respuestas en Google Forms.                | `.openById(id)` / `.getResponses()`                 |
| `SlidesApp`      | Generación y edición de Google Slides.                           | `.getActivePresentation()`                          |

## 2. Métodos de Interfaz de Usuario (UI Customization)
Apps Script permite inyectar código directamente para alterar la interfaz gráfica de los editores de Google. Estos métodos no tienen equivalente en JavaScript estándar: [[1](https://developers.google.com/apps-script/reference/base/ui), [2](https://developers.google.com/apps-script/overview?hl=es-419)]

- **`SpreadsheetApp.getUi()` o `DocumentApp.getUi()`**: Obtiene el entorno gráfico de la aplicación abierta.

- **`.createMenu(caption)`**: Añade una pestaña personalizada al menú superior de Sheets o Docs.

- **`.showSidebar(html)`**: Despliega un panel lateral derecho personalizado programado en HTML.

- **`.showModalDialog(html, title)`**: Bloquea la pantalla mostrando una ventana emergente personalizada.

- **`.alert(prompt)` / `.prompt(prompt)`**: Cuadros de texto emergentes nativos para interactuar con el usuario final de la hoja.


## 3. Funciones de Activación Automática (Triggers Simples)
En JavaScript web existen eventos como `onClick` o `onLoad`. En Apps Script, existen **funciones reservadas por el sistema** que se ejecutan automáticamente por eventos de Workspace: [[1](https://developers.google.com/apps-script/guides/triggers)]

- **`onOpen(e)`**: Se ejecuta automáticamente en el segundo exacto en que un usuario abre un documento o documento de cálculo.

- **`onEdit(e)`**: Se dispara cada vez que un usuario cambia el valor de cualquier celda en Google Sheets. Entrega un objeto de evento (`e`) con datos de la celda antigua y la nueva.

- **`onSelectionChange(e)`**: Se activa al mover el cursor o hacer clic en una celda distinta.

- **`doGet(e)` / `doPost(e)`**: Exclusivas para cuando publicas un script como **Web App**. Actúan como los enrutadores de peticiones HTTP `GET` y `POST`


## 4. Servicios de Utilidad del Sistema
Estas clases resuelven problemas del lado del servidor de Google y no guardan relación con las Web APIs comunes:

- **`UrlFetchApp.fetch(url, params)`**: El equivalente exclusivo de Apps Script al `fetch()` de JavaScript moderno o a `axios` en Node.js, optimizado para saltar firewalls internos de Google.

- **`PropertiesService`**: Una base de datos ligera de tipo clave-valor (`.getScriptProperties()`, `.getUserProperties()`) que guarda credenciales o estados persistentes de forma segura tras bastidores. [[1](https://www.linkedin.com/pulse/10-practical-google-apps-script-tips-supercharge-7lfjc)]

- **`CacheService`**: Permite guardar datos temporalmente en memoria caché de Google para acelerar la velocidad del script. [[1](https://developers.google.com/apps-script/guides/support/best-practices)]

- **`HtmlService`**: Utilizado para procesar y renderizar archivos HTML, permitiendo el uso de **Scriptlets** (`<?= código ?>`) para inyectar variables del servidor al cliente web. [[1](https://www.youtube.com/watch?v=5on6s8KlP8U), [2](https://www.linkedin.com/pulse/100-more-advanced-google-apps-script-examples-hvwee)]

- **`ScriptApp`**: Permite programar de forma interna otros activadores complejos (como ejecutar una función exactamente cada hora de forma automática y asíncrona)

