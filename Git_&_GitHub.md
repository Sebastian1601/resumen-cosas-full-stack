# GIT & GITHUB

///////////////////////CONFIGURACION INICIAL////////////////////////////////////

existen distintos scopes de configuración, local, global, y system.

accedemos a las mismas con 
## git config --(local/global/system)

:local realiza cambios para ese repositorio en particular
:global realiza cambios para todos los repos en ese equipo.
:system realiza cambios para todo el sistema.

* limpiar consola git
	`clear`

* ver la lista de configuraciones globales
	`git config --global --list`

* configurando el nombre global de usuario en git
	`git config --global user.name "Davidejemplo"`

* configurando mail
	`git config --global user.email "davidseba.giordano@gmail.com"`


* Configurar el editor(visual studio code) para mensajes
	`git config --global core.editor "code --wait"`
					`(visual studio code)  --(esto genera que se confirmen los cambiso cuando se cierre
  					 el editor de codigos)`

* configurar colores de interfaz
	`git config --global color.ui true`


** importante para evitar problemas a futuro con el texto (funciona solo en windows)
	`git config --global core.autocrlf true (carriage return line feed)`

* configurar para que la versiòn abreviada del hash de cada commit, sea de x dígitos (normalmente 10)
  	`git config --global core.abbrev X`


### info adicional

https://stackoverflow.com/questions/2517190/how-do-i-force-git-to-use-lf-instead-of-crlf-under-windows/13154031#13154031

////////////////// REPOS ////////////////////////////////////////////////////
## comandos basicos del shell

cd (nombre entrar carpeta) 	: entrar a una carpeta.

cd ../ 				:(volver para atrás un nivel en el directorio) (es lo mismo poner cd ..)

mkdir (nombre de carpeta)	:(crea una carpeta en el directorio actual)

rmdir (nombre de la carpeta)	:(borra una carpeta del directorio actual con el nombre)

rm (nombre del archivo)		:(remueve el archivo indicado localmente)

dir				:(lista contenido de directorio actual)

ls				:(lista de archivos)

ls -l				:(lista de archivos como lista efectiva)

ls -lh				:(lista de archivos)

touch (nombre de archivo.ext)	:(crear un archivo nuevo)

cp (nombre del archivo a copiar) (nombre del directorio donde queremos copiarlo) :copia archivos

mv (directorio del archivo/nombre de archivo.ext) (directorio a donde queremos mover el archivo) :mueve archivos

rm -r (nombre de la carpeta a eliminar, junto con sus archivos) :(elimina archivos y carpetas todo junto) 

##  Area de trabajo ---> Area de Staging ---> REPOSITORIO 

## INICIALIZAR EL REPOSITORIO LOCAL----------------
	
  `git init  (esto inicializa la carpeta como repositorio local)`


### Agregar archivos al area de STAGINGrm

   `git add .  (agrega TODOS los archivos de la carpeta al area de staging)`

   `git add (nombre del archivo uno por uno) ej git add index.html`


### Ver estado de la carpeta, commits, etc del repo. (muestra qué archivo se va a subir al repo)

  `git status`

### Sacar archivo del area de STAGING

   `git rm --cached (nombre del archivo)`

   `git restore --staged (nombre del archivo EN EL area de staging que queremos SACAR)`


## REALIZAR COMMIT ------

`git commit -m "(mensaje de actualización en el commit)"  (-m permite agregar mensaje al commit)`

`git commit (esto abre automáticamente el editor de texto configurado antes, para escribir en
 	detalle los datos del commit)`

### REALIZAR COMMIT -- Sin pasar por el área de STAGING --

`git commit -a`

### VER DATOS Y HASH DE LOS COMMITS

  	git log 

  	git log --oneline  :(muestra el log y los hash resumidos configurados de los commits)

	git log --oneline --all  :(muestra los commits de TODAS las ramas)

	git ls-tree -r --name-only (hash resumido del commit a ver) :(muestra lista de  archivos y carpetas en ese commit)
	git ls-tree -r --name-only HEAD (esto refiere al último commit disponible)

* ELIMINAR UN ARCHIVO DEL REPO

	rm (archivo)  :se elimina el archivo.
	luego, se debe agregar la "eliminación del archivo" con git add (nombre de archivo o punto[git add .]) 
	finalmente se realiza el commit.		
	git commit -m "(mensaje)" -a

* RESTAURAR UN ARCHIVO ELIMINADO LOCALMENTE DESDE EL REPO

	git restore (ruta/nombre del archivo.ext) :(esto restaura un archivo borrado localmente al punto
			de la última actualización que tuvo el mismo en el repo. si se hicieron cambios
			luego del commit y no se guardaron, no van a estar en el archivo restaurado)


* VOLVER ATRÁS EL ESTADO DE UN ARCHIVO, al último commit actualizado(HEAD).(esto no funciona si hay cambios subidos al ÁREA DE STAGING)

	git checkout (ruta/archivo.ext) :(vuelve el estado del archivo al estado del último commit.
					Todo cambio posterior se descarta)
  	git checkout (hash de un commit anterior cualquiera) :(cambia al estado de los archivos en ese commit, pero es solamente
  							 para revision)

  	SI AL UTILIZAR GIT CHECKOUT, CREAMOS UNA RAMA DESDE ESE PUNTO, PODEMOS LLEVAR ESTE ESTADO A UNA RAMA "OFICIAL"
  	PARA SEGUIR TRABAJANDO DESE ESE PUNTO LOS ARCHIVOS.
  
	== SOLO SE UTILIZA LUEGO DE ver un commit anterior con GIT CHECKOUT y no queremos cambiar nada ==
	git switch - (vuelve el HEAD al último commit disponible del repo)

* VOLVER ATRÁS el estado de un archivo sin tener en cuenta si hay archivos en el área de staging
	======== SIEMPRE HAY QUE TENER LOS ARCHIVOS GUARDADOS ANTE UN RESET HARD =======
	git reset --hard (hash del commit a donde quiero volver el estado de todos los archivos)


* CAMBIAR NOMBRE DE UN ARCHIVO

  	git mv (nombre del archivo actual.ext) (nuevo nombre.ext)

* VERIFICAR CONTENIDO DE UN ARCHIVO ¡¡ YA GUARDADO !! EN EL REPOSITORIO LOCAL

  	git show (nombre del archivo.ext)

* COMPARAR ARCHIVOS EN EL REPO(ya commiteados) CON ARCHIVOS EN EL AREA DE STAGING (obviamente no se define el archivo en el comando sino subiendolos al área de staging) 

	git diff --staged

* COMPARAR DIFERENCIAS ENTRE 2 VERSIONES DE LOS COMMITS, DE ACUERDO A SU HASH

   	git diff (1er hash de commit de x dígitos) (2do hash de commit de x dígitos)

* COMPARAR SOLAMENTE CAMBIO DE NOMBRES EN LOS ARCHIVOS

  	git diff --name-only (1er hash de commit de x dígitos) (2do hash de commit de x dígitos)

* COMPARAR QUE SE CAMBIO ENTRE DOS COMMITS

  	git diff --word-diff (1er hash de commit de x dígitos) (2do hash de commit de x dígitos)


* CAMIAR DE MENSAJE EL ÚLTIMO COMMIT REALIZADO (y modificar el último commit)

  	git commit --amend

  	(en caso de necesitar modificar archivos en este ùltimo commit, se agregan al area de STAGING
  	y ahi luego de tener todo organizado en staging se realiza el comando indicado git commit --amend)

  
* DESHACER EL ULTIMO COMMIT (mover el HEAD al commit anterior, y mueve los archivos del ùltimo commit, al área de staging para
  				realizar cambios o eliminarlos, y si ha archivos ya en staging, se agregan todos juntos)

  	git reset --soft (hash de commit anterior al que queremos borrar de x digitos) :(no modifica archivos del área d trabajo)

   	git reset --soft head~1  (esto es lo mismo que pensar desde el commit head - 1 restarle uno)

  	git reset --mixed (hash de commit anterior al que queremos borrar de x digitos) (esto vuelve atràs sin dejar nada
  				 en el area de staging pero sin modificar el área de trabajo)

	*********** ANTES DE USAR GIT RESET HARD hay que guardar los archivos del area de trabajo sino darà error*************
  	***********LOS ARCHIVOS QUE SE USAN CON GIT RESET HARD no pueden ser guardados ***************************************

  	gir reset --hard (hash del commit del que quiero tener todos los archivos en el area de trabajo, pisando todo
  			lo que tenía)

## GIT Revert ---

* Git revert es similar a git reset, pero el enfoque es ligeramente diferente. En lugar de eliminar todos los commit a su paso, la reversión SÓLO deshace un único commit, devolviéndote a los archivos organizados antes del commit.

* Así, en lugar de eliminar un commit, git revert invierte los cambios introducidos por el commit original creando un nuevo commit con el contenido inverso subyacente. Esta es una forma segura de revocar un commit porque evita que pierdas tu historial. 

		git revert HEAD

* el código anterior, genera un NUEVO COMMIT, posterior al actual, con los cambios generados en este commit actual desestimados. O sea, elimina los cambios introducidos en el commit actual, pero creando un nuevo commmit "hacia adelante"


		git revert --no-edit <commit ID>

* La opción --no-edit permite al usuario no cambiar el mensaje utilizado para el commit que desea revertir, y esto hará que git revierta el archivo a la rama maestra.


----

		git revert <commit hash>

Esto sólo eliminará los cambios asociados a este hash de commit y no afectará a ningún otro commit. incluso funciona si por ej. se han eliminado archivos en un commit anterior, al revertir ese commit, se recuperan los archivos.

---

		git revert --no-comit <commit ID>  || [git revert -n <commit ID>]

este comando revertirá los cambios del commit indicado, pero no creará un nuevo commit, para que se puedan verificar y decidir si se commitean asi como están o se agregan más cambios.





  //////////// RAMAS o BRANCHES ///////////////////////////////////////////////////////////////////////////////////

  Tener en cuena que depende de en qué rama estemos posicionado, al crear una nueva rama, puede no ser del proyecto principal
 //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	git branch  (esto muestra todas las ramas activas y creadas del repo)

	git branch  (nombre de la rama)  :esto crea una rama(copia del estado actual) con el nombre indicado.

* cambiar a una rama:
	git checkout (nombre de la rama en la que se quiere trabajar) (ya no se suele utilizar)

	git switch (nombre de la rama en la que se quiere trabajar)

* Crear una rama y cambiar a esa inmediatamente:
	git switch -c (nomber de la rama a crear) 


* Eliminar ramas (ES IMPORTANTE QUE PARA ELIMINAR UNA RAMA, NO DEBEMOS ESTAR PARADOS EN ELLA)
  	git branch -d (nombre de la rama a borrar)

* Cambiar nombre de rama donde NO ESTAMOS PARADOS

  	git branch -m (nombre actual de la rama) (nombre nuevo de la rama)

* Cambiar nombre de la RAMA ACTUAL

  	git branch -m (nuevo nombre a colocar en la rama actual)

//////////////////////////////////////////////////////////////////////////// UNIR RAMAS (MERGE o FUSIONAR) ///////////////////

IMPORTANTE! para fusionar RAMA1 con RAMA2, debemos estar "parados" en la rama a la cual queremos "mantener". En este caso, debemos estar en RAMA1 y fusionar RAMA2 con RAMA1, para que los cambios se agreguen a RAMA1.

* FUSIONAR RAMAS:
	git merge (nombre de la rama a fusionar en la rama actual donde estamos parado)

* EN CASO DE HABERSE EQUIVOCADO:

  	git reset --hard (HASH del último commit de la rama principal antes de fusionar las ramas)
  								ESTO ELIMINA EL COMMIT DE FUSION DE LAS RAMAS pero
  								no la rama que se fusionó!
* EN EL CASO DE QUERER RECUPERAR UN COMMIT BORRADO CON RESET --HARD, si tenemos el HASH de referencia, podemos recuperarlo con

  	git reset --hard (HASH del commit borrado)


////////// CONFLICTOS DE FUSIONADO (MERGE) ////////////////////////////////////////////////////////////////////////////////////

Esto suele suceder cuando se trabaja en una rama, desde un punto B de la rama principal, y antes de fusionar la rama con el principal, se da que la rama principal tuvo modificaciones. 

			rama1 ---- rama1(2)
   		       /                   \
	    	      /                     \
	main------main(2) ----main(3)------ (main + rama1(2)) = Conflicto Posible

Abriendo el editor de Visual Studio Code permite seleccionar qué código va a quedar seleccionado y se realiza el commit 
desde ahi directamente.
Se pueden aceptar cambios de una rama, de otra, ambas, o seleccionando la opción más conveniente de cada una.

Caso contrario, se pone:
	
 	  git merge --continue   (esto finaliza con el commit del merging)

* VER la última actualización de cada rama

   	  git branch -v


## EN CASO DE QUE FIGURE EN EL MERGE NO MERGIN UNRELATED HISTORIES(esto es cuando varia demasiado las ramas)

	git merge [nombre de la rama a fusionar con la actual] --allow-unrelated-histories

 esto abre el editor para resolver codigo o dejar el mensaje de commit del merging
 
 //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

 .GITIGNORE 

 	esto define qué archivos GIT debe ignorar al momento de buscar para commitear. y solo funciona para archivos que
  	NUNCA se han guardado en un commit, si el archivo ya se subió

  se crea un archivo .gitignore

  se puede abrir con el VSC y se puede comentar dentro con el símbolo #(comentario)
  se agrega el [nombre.ext] del archivo a ignorar, pero se puede definir por rangos
  	ej: *.txt / *.jpg / *.py
   
*  para excepcionar un archivo dentro del grupo de archivos definidos por ej en *.txt, se pone
  ![nombre de archivo.txt]
  
*  Para ignorar un directorio completo se pone
	[nombre de carpeta]/

* CONFIGURAR QUE LOS REPOS LEAN UN ARCHIVO .GITIGNORE general:

  	git config --global core.excludesfile [ruta en la pc del archivo]
 	ej: git config --global core.excludesfile c:/generalfiles/.gitignore_global

  
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

ALIAS EN GIT
	(se definen como funciones que guardan todos los comandos determinados para ejecutar más simple)

 ej:
   git log --oneline --graph --all
  	
   	se puede resumir configurando lo siguiente: elijiendo el nombre del comando propio como logsimple

   git config --global alias.[nombre del comando propio] "log --oneline --graph --all"

    esto genera que al escribir c:>git logsimple 
    esto genere que se dispare el comando configurado anteriormente.

* Ver la lista de alias asignado:
  	 git config --global --list |grep alias

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

* GIT REFLOG
  	esto es un log de todos los movimientos generados en el repo, borrados, HASH de elementos borrados, etc.
 
  
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

#------------------------------------- GIT HUB [Repositorios Remotos] ----------------------------------------------------------#

                Área de trabajo --> STAGING --> REPOSITORIO LOCAL --> REPOSITORIO EN LINEA
			a		b		c		D


// CREAR Y CONFIGURAR REPOSITORIO REMOTO //

  ## GIT CLONE --------------------------------------------------------------------------------

  c:>CODE .     :abre el VSC dentro de la carpeta actual.

	ESTANDO en la carpeta donde queremos copiar el repositorio por HTTPS, copiamos la dirección http y luego:

 	git clone [dirección https del repositorio a clonar] ↩️
  
  esto ya configura el remote origin, para el push y fetch

 
  
  
  ## GIT PUSH --------------------------------------------------------------------------------

Para poder subir archivos a nuestro repo, debemos tener configurado el mismo mail con el que iniciamos sesión
en Github. 
Luego, si queremos subir algo a un repo "clonado", se utiliza el comando

    	git push origin main
     	git push [nombre del repo remoto] [rama del repo remoto]
  	
*Si esto abre una ventana de log, lo recomendable es hacerlo por [TOKEN]. Para obtener el [TOKEN], 
 vamos a Settings > Developer Settings > Personal Acces Tokens > Tokens (classic) y ahi Generar nuevo token

   		Recomendaciones sobre el token ------
     		- No debería ser eterno. Lo recomendable es de 7 a 30 días.
       		- Los permisos con la primera opción, REPO ya es suficiente.

 Esto generará un código que se debe copiar en el sistema de inicio de sesión de Github por la solapa TOKEN.

 
*Para subir todas las ramas de tu repo local al remoto

 	git push --all

*Para subir al repo remoto OnlineRepo con una rama remota ramaR (distinto nombre a la tuya local) tu rama local ramaL:

	git push OnlineRepo ramaL:ramaR

 
 ## GIT PULL ------------------------------------------------------------------------------------------------------------------------------------------------------

	Se utiliza para descargar CAMBIOS hechos en el repo online, al repo local, de ciertos archivos(no todos, para eso 
 	se usa un git clone).
  	esto es un /git fetch/ y luego hacer un /git merge/ todo junto.

   * Git pull origin main

 # *ERRORES con git push:

   There are two ways of solving the fatal: refusing to merge unrelated histories error

	*git pull origin master --allow-unrelated-histories.

   You can substitute origin with the remote repository you are pulling from. You can also replace the master branch with whatever branch you want the pull request to merge into.

  	Option 2: unstage, stash, clone, unstash, and then commit

The alternative (and longer) way of fixing the fatal: refusing to merge unrelated histories issues is to unstage your current commits, stash them, clone your required remote repository, and then place your stashed branch contents into the new clone.

This will ensure that any conflicts that you may encounter in the code are addressed before merging and prevent application errors from occurring.
To unstage all the files in your last commit, use the following git command: git reset HEAD~.

To stash your unsaved files, use the following git command: git stash.

This will give you a clean working tree to pull your remote repository into. Once you’ve successfully pulled into your branch, you can unstash your files, commit them as a separate commit and resolve any file conflicts that you may have.

To unstash your files, use git pop. This will move the changes stashed and reapplies them to your current working copy.

Alternatively, you can use git stash apply to add the changes to your current working copy of code.

Here is a quick summary of differences between git stash apply and <code”>git pop:

    git pop: ‘pops’ the changes from the stash and applies them to the current code
    git stash apply: keeps the changes in the stash and applies the changes to the current code

The easiest way to prevent the fatal: refusing to merge unrelated histories error is to avoid pulling remote repositories into branches that already have commits on them.
However, sometimes you just want to keep the commits. One way to prevent the error is to create a brand new branch, pull your required code in, and then manually merge your local branch into your main flow.


## GIT STASH (guardar temporalmente los cambios realizados en el area de trabajo sin commitear)------------------------------------------------------------------

	git stash save "(MENSAJE PARA EL STASH-como un commit)" 

 Esto guarda los cambios y revierte el directorio de trabajo a como se veía en tu último commit. Los cambios guardados están disponibles en cualquier rama de ese repositorio.

 ·Ver los cambios guardados en el stash:

 	git stash list

Esto devuelve una lista de tus capturas guardadas en el formato stash@{0}: RAMA-STASHED-CAMBIOS-SON-PARA: MESSAGE. La parte de stash@{0} es el nombre del stash, y el número en las llaves ({ }) es el índice (index) del stash. Si tienes múltiples conjuntos de cambios guardados en stash, cada uno tendrá un índice diferente.

Si olvidaste los cambios que hiciste en el stash, puedes ver un resumen de ellos con el comando 

	git stash show NOMBRE-DEL-STASH

 Si quieres ver las direferencias de los cambios en la consola, se puede ejecutar lo siguiente:

 	git stash show -p NOMBRE-DEL-STASH

Para recuperar los cambios del stash y aplicarlos a la rama actual en la que estás, tienes dos opciones:
   aplica los cambios y deja una copia en el stash:
    	
        git stash apply NOMBRE-DEL-STASH 


   aplica los cambio y elimina los archivos del stash:

     	git stash pop NOMBRE-DEL-STASH

Si quieres remover los cambios guardados en stash sin aplicarlos, ejecuta el comando:

	git stash drop NOMBRE-DEL-STASH

Para limpiar todo del stash, ejecuta el comando:

	git stash clear


## GIT FETCH ---------------------------------------------------------------------------------------------
	esto descarga los cambios en el repo Origin/Main, y crea una rama temporal, del mismo nombre para poder
 	verificar los cambios, y en todo caso, sumarlos a nuestro repo local
	Luego de ejecutar el fetch, debemos "pasar" a la rama temporal que se suele llamar (origin/main) para verificar los cambios hechos, mediante el siguiente comando:

   git switch --detach origin/main (esto genera que se trate como temporal) 
   
 	y luego, si sirven, guardarlos. VOLVER a la rama principal de nuestro repo local
  	para hacer un -git pull-



## Migrar repositorio local a uno remoto ------------------------------------------------------------------

   Luego de crear un repositorio en Github, mediante Git hay que hacer

  	git remote add [nombre de referencia del repo remoto] [dirección http del repositorio remoto creado]

   ej:  	
   			
      git remote add origin https://github.com/Sebastian1601/Codoacodo-tp-nodejs.git
      
   luego se comanda
  				
      		git branch -M main
   y finalmente

    		git push -u origin main
 
# FORK --------------------------------------------------------------------------------------------------
   Un fork es una copia de un repositorio remoto en nuestro repositorio remoto. Cuando queremos duplicar algun proyecto del que podemos copiarnos.
   Al hacerlo, queda en nuestro repo, y se hace el commit para "guardarlo" por primera vez.


# PULL REQUEST --------------------------------------------------------------------------------------------

esto se da cuando hacemos un fork, y guardamos un repositorio que no es nuestro en el repo online.
queremos subirla de nuevo al repo remoto copia del proyecto de alguien más.

cuando ya tenemos cargado en el repo online nuestro el repo local del fork, tenemos una opción llamada [CONTRIBUTE], y de ahi se abre la opción [OPEN PULL REQUEST].
Ahi se verifica que se pueda fusionar ambos repos, y luego se agregan los datos sobre titulo y descripción del pull request.


# ERROR AL USAR GIT LOG (queda la lista de commits y luego dice log file: y no sale de esa pantalla.)

	al registrar este error, hay que presionar ESC, y luego la tecla "Q"
