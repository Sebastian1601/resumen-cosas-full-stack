# Expresiones Regulares (Reg-Exp)

Las expresiones regulares se suelen utilizar para comparar y de una manera "manejar" cadenas de caracteres ingresados. Pueden definir un formato de ingreso, caracteres válidos, etc.

`| (barra vertical)` : La barra vertical indica que tanto el elemento a la izquierda como el de la derecha son posibles. 
ej: amarillo| azul : indicaría que tanto amarillo como azul se pueden escribir y son válidos.

## Cuantificadores ?, +, *
---

### SIMBOLO DE INTERROGANTE ?
`?` : este símbolo indica que el caracter que precede al símbolo puede aparecer COMO MUCHO UNA VEZ.

### SIMBOLO DE SUMA +
`+` : este símbolo indica que el caracter que precede aparece AL MENOS UNA VEZ.

### SIMBOLO DE MULTIPLICACION *
`*` : este símbolo indica que el caracter que precede, PUEDE APARECER NINGUNA, UNA o MAS VECES.
```ej: 0*42 valida 42, 042, 0042, 00042, 0000042, etc.```

### PARéNTESIS ()
---

`()` : Los paréntesis agrupan y se utilizan para definir ámbito y precedencia de los demás operadores. Los caracteres especiales mantienen su significado dentro de los paréntesis, y utilizados en conjunto con `|` permiten realizar busquedas opcionales.
```ej: (p|m)adre valida padre, madre.```
```ej: (des)?amor valida amor, desamor```
`ej: (este|oeste|norte|sur)` validará solo esas direcciones cardinales. mientras que:
`este|oeste|norte|sur` validará por ej "esteban" de manera correcta.

### PUNTO .
---
El punto es un símbolo que representa "cualquier caracter", como un comodín.
```ej: G.T valida GAT, GET, GIT, GOT, GUT, GLT, G4T, GCT, GQT, ..., etc.```

### SIGNO DE EXCLAMACION !
---
El símbolo `!` se utiliza para "buscar anticipadamente una negativa".
```ej: (!palabra a excluir)```

### BARRA INVERTIDA \
---
Este símbolo se usa para "escapar" el siguiente caracter de la expresión de busqueda. NO SE USA POR SI SOLA.

```ej: \.  ``` valida que en la expresión, el punto significa un punto "literal"

## Caracteres con barra invertida

|caracteres con barra invertida especiales| que valida|
|----|------|
| \t | representa una tabulación |
| \r | retorno de carro o regreso al inicio |
| \n | nueva linea \r\n |
| \e | representa la tecla ESC o Escape |
| \f | representa un salto de página |
| \v | tabulación vertical |

| caracteres mas usados | que valida                                                    |
| --------------------- | ------------------------------------------------------------- |
| \d                    | representa un dígito del 0 al 9                               |
| \D                    | representa cualquier caracter QUE NO SEA un dígito del 0 al 9 |
| \w                    | representa CUALQUIER caracter ALFANUMERICO                    |
| \W                    | representa cualquier caracter QUE NO SEA alfanumérico         |
| \s                    | representa un espacio en blanco                               |
| \S                    | representa cualquier caracter QUE NO SEA un espacio en blanco |

| caracteres de posicion | que valida                                                                                                              |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| ^                      | representa el inicio de un string                                                                                       |
| $                      | representa el final de un string                                                                                        |
| \A                     | representa el inicio de la cadena, no caracter sino POSICION                                                            |
| \Z                     | representa el final de la cadena, no caracter sino POSICION                                                             |
| \b                     | representa la posición de una palabra, limitado por espacios en blanco, puntuacion, o por el inicio/final de una cadena |
| \B                     | marca la posición entre dos caracteres alfanuméricos, o dos NO ALFANUMERICOS                                            |
| \Q y \E                | se interpreta como LITERAL todo lo indicado entre las marcas                                                            |
| \b                     | representa el inicio o fin de un patrón regular determinando los límites                                                |



ejemplos:
`^[0-9]$` valida un string numérico

`\Q .*/ \E` valida .*/ como caracteres

### CORCHETES []
---

Este símbolo se utiliza para representar "clase de caracteres"(grupos).
Se utiliza el guión para especificar "rangos" `ej: [0 - 9]`
Los `metacaracteres` se convierten en literales dentro de los corchetes, sin importar cuántos caracteres se pongan dentro de los corchetes.
El motor de busqueda va a buscar expresiones con solo UNO de ellos.
`ej: expresi[oó]n` valida "expresion" y "expresión".

### DOLAR $
---
Este símbolo representa el final de una cadena o final de linea. No representa caracter, sino posición.
`ej: \.$` valida todos los puntos que esten al final de la cadena evaluada.

### ACENTO CIRCUNFLEJO ^
---
Este símbolo tiene 2 funciones:
* SI SE USA SOLO, representa el inicio de una cadena.
  `ej: ^[a-z]` valida todas las palabras que INICIEN con una letra minúscula.
* SI SE USA EN GRUPO CON OTROS CARACTERES ESPECIALES, valida todos los caracteres que no pertenecen al grupo indicado.
  `ej: [^\W]` valida cualquier caracter que NO SEA ALFANUMERICO o un ESPACIO.

  `otro ej: ^\d\d / \d\d / \d\d\d\d$` valida un nro con formato fecha.

### SIGNO ?
---
Este símbolo tiene varias funciones, en principio, especifica que los caracteres precedentes son opciones, que pueden o no aparecer.
`ej: ob?scuridad` valida "obscuridad" y "oscuridad".

`ej2: a?normal` valida "normal" y "anormal".

- En conjunto al final de un paréntesis, indica que todo esa expresion, es opcional, y puede o no aparecer.
  `ej3: Nov(\.|iembre|ember)?` esto valida "Noviembre", "Nov.", "November".

- Permite al motor de busqueda ignorar la expresión.
  `ej4: Nov(?:\.|iembre|ember)?` esto validaría lo mismo que la expresión anterior, pero validando también las expresiones que contienen "Nov" en el inicio, como "Noverturía", "Novertemás", etc.

  ### MAYOR y MENOR < >
Estos símbolos permiten definir grupos "anónimos" sin usar el ?, y utilizando el ? permite "nombrar" los grupos.
`?<nombre>`

`ej: ^(?<dia>\d\d)\/(?<mes>\d\d)\/(?<año>\d\d\d\d)$`

## SIMBOLOS DE REPETICION
---
Estos símbolos se usan para indicar una repetición de ciertos patrones, cierta cantidad de veces, definiendo patrones más exactos.

### LLAVES {}
  Son símbolos LITERALES, EXCEPTO que encierren uno o más nros separados por coma, y que estén a la derecha de otra expresión regular.
  `ej: \d{2}` valida números de 2 dígitos.

  `ej2: \d {2,4}` esto valida expresiones numéricas de 2, 3 y 4 dígitos. Es lo mismo que definir ^\d\d$, ^\d\d\d$ y ^\d\d\d\d$ pero todo en una expresión.

### ASTERISCO *
  El símbolo * indica que la expresión precedente puede aparecer indefinida cantidad de veces.



### Lookahead y Lookbehind
  estos métodos permiten buscar patrones de expresiones que sean precedidos o seguidos por otros patrones que NO ENTRAN en la busqueda del patrón principal.

  por ej:

  >> Positive Lookahead: Confirma que lo que inmediatamente sigue en la posición del _String_  coincide con el patrón dado.
`Sintáxis: (?=patrón)`

Ej: q(?=u) coincide con "q" solamente si es seguido por una "u"

  >> Negative Lookahead: Confirma que lo que inmediatamente sigue la posición actual en el  _String_ no coincide con el patrón dado. 
`Sintáxis: (?!patrón)`

Ej: q(?!u) coincide con "q" cuando NO ESTÁ seguido de "u".


These assertions are zero-width, meaning they do not consume characters in the string; they only assert whether a match is possible or not

















