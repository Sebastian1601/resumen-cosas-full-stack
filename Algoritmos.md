
## Distancia de Leveshtein
La distancia de Levenshtein cuenta el **mínimo de ediciones** para convertir una palabra en otra. Cada edición puede ser *insertar* una letra, *borrar* una letra o *sustituir* una letra por otra, y cada una cuesta ==1==.

Se construye una matriz usando la longitud de las dos palabras a evaluar, por ejemplo, comparando "plato" y "gato" tenemos una matriz de (5 + 1) columnas x (4 + 1) filas.

### ### Cómo se construye la matriz

**1. Tamaño.** Si A tiene _m_ letras y B tiene _n_ letras, la matriz es de (m+1) × (n+1). Las filas representan los prefijos de A y las columnas los prefijos de B. La celda (i, j) guarda la distancia entre las primeras _i_ letras de A y las primeras _j_ letras de B.

**2. Fila y columna 0.** Pasar de la palabra vacía a un prefijo de _j_ letras cuesta _j_ inserciones, y pasar de un prefijo de _i_ letras a la palabra vacía cuesta _i_ borrados. Por eso la primera fila es 0, 1, 2, 3… y la primera columna también.

![[Pasted image 20260928112523.png]]

**3. Cada celda interior.** Comparas la letra de A (fila) con la letra de B (columna). El costo es 0 si son iguales y 1 si son distintas. Luego tomas el **mínimo** de tres opciones:

- **Diagonal + costo:** copiar la letra si son iguales, o sustituirla si son distintas.
- **Arriba + 1:** borrar una letra de A.
- **Izquierda + 1:** insertar una letra de B.

**4. Resultado.** La distancia final es la celda de la esquina inferior derecha. En el ejemplo, «gato» → «plato» da **2**: sustituir `g` por `l` e insertar `p`.


---

- creo la matriz con el largo de una de las palabras + 1.
- lleno cada una de desas celdas con otra matriz, con el largo de la 2da la palabra + 1.
- lleno la primer celda de cada columna con valores del 0 al largo de la palabra inicial
- lleno el primer arreglo con los valores del 0 al largo de la 2da palabra.

esto deja seteado el primer paso, a partir de ahi analizo toda la matriz, partiendo del valor `matriz[1][1]` para ver si la letra 1 de la palabra A es igual, o distinta, asignado 0 si es igual(no tiene costo), y 1 si es que es distinta. 
Luego de esto, al obtener ese valor, se le suma al numero diagonal anterior `[columna - 1] [fila - 1]` y comparo ese valor, con el valor `izquierdo +1` y `arriba +1` para ver cuál es el de menor costo...ese valor se asigna al lugar de la matriz analizado.
- izquierda + 1 :corresponde a insertar una letra de B
- arriba + 1 : corresponde a borrar una letra de A

finalmente, el último valor de la diagonal de la matriz, es el costo de convertir la palabra A en B.
Con ese valor, y calculos de redondeo mas multiplicacion se puede calcular o definir, la similitud entre las palabras. 
generando un umbral de aceptación, podemos indicar que las palabras con un nro mayor a 90% sean similares, etc.



