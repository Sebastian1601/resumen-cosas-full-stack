
SQLite se usa localmente para manejar datos persistentes en una aplicación local que no necesite escalarse o de uso multiusuario.
No por eso es mucho más simple que cualquier otro motor relacional de db.

Pero contiene diferencias que la hacen más fácil de manejar.

## Linea de comandos

### Manejo de archivos desde sqlite3

- `sqlite3 [nombre de un archivo db]` *abre* el archivo .db para manejar los datos de la base **SI LA BASE YA EXISTE**, sino, *crea una base de datos nueva* ,con ese nombre, en el directorio desde donde estémos ejecutando sqlite3.
>ejemplo: Si estamos en c:\usuario\nombre1 y ejecutamos ahi sqlite3 miBase.db, 
>la dirección absoluta al archivo será *C:\usuario\nombre1\miBase.db*

- `.open [nombre de un archivo .db ya existente]` si ya estamos dentro de la interfaz sqlite3 de la linea de comandos, este comando abre la base de datos pasada como parámetro.

- `.databases` este comando muestra todas las bases de datos abiertas y sus rutas en la pc.

- `.backup copia_de_base_de_datos.db` este comando crea una copia exacta de la base de datos activa a otro archivo de nombre *copia_de_base_de_datos.db* sin detener el sistema.

- `.restore respaldo.db` reemplaza el contenido de la base de datos actual con el del archivo de *respaldo.db*
 
- `.clone destinoArchivo.db` este comando clona la base de datos actual en un archivo nuevo.

*.clone* y *.backup* parecerían hacer lo mismo, pero .backup se puede utilizar de manera segura en un entorno donde la base esté siendo utilizada, dado que realiza una copia atómica página por página usando una API interna de SQLite.
.clone no bloquea transacciones de la misma manera, por lo que puede capturar información inconsistente o parcial si el sistema está activo, por lo tanto, se deja para entornos de prueba o locales, donde sabemos que la base no está siendo utilizada.

### Exportar e importar datos

- `.output archivo.sql` - envía el resultado de las *siguientes* consultas a un archivo en lugar de mostrarlo en pantalla.

- `.dump` - Convierte toda la base de datos a texto plano con comandos SQL (ideal para respaldos de texto) 

- `.output stdout` - regresa la salida de la terminal a la normalidad(como cuando se entra a sqlite3)

- `.read archivoDeComandos.sql` Ejecuta todos los comandos SQL que estén guardados dentro del archivo *archivoDeComandos.sql* 

### Formato visual de la consola en pantalla

- `.mode box` muestra las tablas con bordes limpios y ordenados. (*recomendado*)
- `.mode csv` cambia el formato de salida a texto separado por comas
- `.headers on` muestra los nombres de las columnas al hacer consultas.

### Información de sistema y salida

- `.tables` muestra las tablas que componen la base de datos actualmente abierta.

- `.schema` muestra la estructura exacta (*Data Definition Language o DDL*) de las tablas que componen la base actual.

- `.help` Muestra la lista completa de todos los comandos de punto disponibles.

- `.exit` o `.quit` cierra la consola Sqlite3 de forma segura salvando los cambios.

## Manejando fechas

### time()

Para manejar horarios en SQLite se utilizan las funciones siguientes 
- `time()` o 
- `datetime()`

Estas funciones pueden llevar parámetros para modificar justamente los resultados, 
*por ejemplo*
`SELECT time('now', 'localtime');`

Esta busqueda devuelve el horario local en donde estamos ejecutando nuestro sistema.

Las funciones globales como `CURRENT_TIME`  devuelven los valores en formato UTC (GMT).
*por ejemplo*:
`SELECT CURRENT_TIME;` devuelve la hora en GTM, donde a buenos aires, tiene 3 horas más (Buenos Aires -3 GTM)

`SELECT date('now');` hace lo propio de la misma manera.


>[!important] Consultar la hora local

**S**i queremos modificar la hora al uso horario que necesitemos, por ejemplo, hora de buenos aires, podemos usar:
```sql
SELECT time('now', 'localtime');
-- (YYYY-MM-DD) formato entregado
```
>Esto nos devuelve el horario local configurado en el dispositivo que estemos usando.

### datetime()

>[!important] Consultar la fecha y hora completas

Si queremos consultar la fecha conjuntamente con la hora actual, ya debemos cambiar nuestra función principal a `datetime()` con los mismos modificadores que usamos antes.

```sql
SELECT datetime('now', 'localtime')
-- (YYYY-MM-DD HH:MM:SS) formato entregado
```


### date()

La función date permite obtener la fecha para poder insertar o leer las mismas, con modificadores útiles para obtener otras fechas.

```sql
SELECT date();
--(YYYY-MM-DD)
```


>[!tip] **Nota de buena práctica:**
>Muchos desarrolladores prefieren almacenar el tiempo en formato UTC puro (usando directamente `CURRENT_TIMESTAMP`) y realizar la conversión a la zona horaria local únicamente al consultar o presentar los datos en la aplicación web o móvil. Esto evita inconsistencias horarias si tu base de datos se muda de servidor o cambia de región geográfica
>
>Siempre hay que pasar los números de fechas entre comillas simples para que SQLite no los maneje como números enteros y expresiones matemáticas.
>- [c] SELECT date( 2026-01-17 );   SQLite evalua la expresión matemática asociada.
>- [p] SELECT date( '2026-01-17' );   SQLite correctamente maneja la fecha 
> 
> Mantener el formato de fecha **YYYY-MM-DD** para usar comparaciones de fechas (**standard big-endian**)
> Esto permite manejar comparaciones standard con ( **>, <, BETWEEN** ) y para ordenamiento con ( **ORDER BY** )


### strftime()
Esta función permite definir como deseamos que se nos represente el valor que buscamos, ya sea guardado o al seleccionarlo. Esta función si o si lleva parámetros para "stringifiar" la misma, con el formato que definamos.


```sql
SELECT strftime('%d / mes %m / año %Y');
--devuelve 14 / mes 06 / año 2026
```

|   |   |   |
|---|---|---|
|%d||day of month: 01-31|
|%e||day of month without leading zero: 1-31|
|%f||fractional seconds: SS.SSS|
|%F||ISO 8601 date: YYYY-MM-DD|
|%G||ISO 8601 year corresponding to %V|
|%g||2-digit ISO 8601 year corresponding to %V|
|%H||hour: 00-24|
|%I||hour for 12-hour clock: 01-12|
|%j||day of year: 001-366|
|%J||Julian day number (fractional)|
|%k||hour without leading zero: 0-24|
|%l||%I without leading zero: 1-12|
|%m||month: 01-12|
|%M||minute: 00-59|
|%p||"AM" or "PM" depending on the hour|
|%P||"am" or "pm" depending on the hour|
|%R||ISO 8601 time: HH:MM|
|%s||seconds since 1970-01-01|
|%S||seconds: 00-59|
|%T||ISO 8601 time: HH:MM:SS|
|%U||week of year (00-53) - week 01 starts on the first Sunday|
|%u||day of week 1-7 with Monday==1|
|%V||ISO 8601 week of year|
|%w||day of week 0-6 with Sunday==0|
|%W||week of year (00-53) - week 01 starts on the first Monday|
|%Y||year: 0000-9999|
|%%||%|


### Modificadores de funciones
Las funciones 
- `date()` 
- `time()`
- `datetime()`
- `julianday()` 
- `strftime()`

Permiten usar modificadores para obtener otras fechas futuras, anteriores, y lo mismo con los horarios.
**TENER EN CUENTA QUE ESTOS MODIFICADORES VAN ENVUELTOS EN COMILLAS SIMPLES dentro de la función que estemos aplicando.**

**Modificadores de fecha y hora**
- `'+1 day'` : Suma un día a la fecha principal
- `'-3 months'` : Le resta 3 meses a la fecha principal
- `'+5 years'` : Le suma 5 años a la fecha principal
- `'+2 hours'` : Le suma 2 horas al horario principal
- `'-30 minutes'` : Le resta 30 minutos a la hora principal
- `'-15 seconds'` : le resta 15 segundos a la hora principal

**Modificadores de zona**
Estos modificadores permiten cambiar el horario entre la zona donde está configurada el equipo que estemos usando o el horario UTC.
- `'localtime'` : convierte a la hora local el tiempo de la función
- `'utc'` : convierte a tiempo UTC 

**Modificadores de inicio de período**
Estos modificadores nos permiten mover la fecha u hora al inicio de la unidad de tiempo seleccionada.

- `'start of month'` : mueve al día 1 del mes actual a las 00:00;00.
- `'start of year'` : mueve al 1 de enero del año actual a las 00:00:00.
- `'start of day'` : resetea la hora a las 00:00:00 del día actual.

Si queremos obtener el último día del mes actual...
```sql
SELECT date('now', 'start of month', '+1 month', '-1 day');
```

**Modificadores de día de la semana**
Estos modificadores nos permiten avanzar hasta el próximo día de la semana indicado justamente con un valor de 0 a 6 (0 = domingo, 1 = lunes, 2 = martes, ..., 6 = sábado) y obtener la fecha de dicho día.

Si queremos obtener la fecha del próximo martes:
```sql
SELECT date('now', 'weekday 2')
```

---

