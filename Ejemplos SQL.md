
Teniendo las siguientes tablas:

| Buildings     |          |
| ------------- | -------- |
| building_name | capacity |
| 1e            | 24       |
| 1w            | 32       |
| 2e            | 16       |
| 2w            | 20       |

| Employees |            |          |                |
| --------- | ---------- | -------- | -------------- |
| role      | name       | building | years_employed |
| Engineer  | Becky A.   | 1e       | 4              |
| Engineer  | Dan B.     | 1e       | 2              |
| Engineer  | Sharon F.  | 1e       | 6              |
| Engineer  | Dan M.     | 1e       | 4              |
| Engineer  | Malcom S.  | 1e       | 1              |
| Artist    | Tylar S.   | 2w       | 2              |
| Artist    | Sherman D. | 2w       | 8              |
| Artist    | Jakob J.   | 2w       | 6              |
| Artist    | Lillia A.  | 2w       | 7              |
| Artist    | Brandon J. | 2w       | 7              |
| Manager   | Scott K.   | 1e       | 9              |
| Manager   | Shirlee M. | 1e       | 3              |
| Manager   | Daria O.   | 2w       | 6              |
| Engineer  | Yancy I.   |          | 0              |
| Artist    | Oliver P.  |          | 0              |
- Quiero obtener los nombres de los edificios, los cuales todavia no tienen empleados asignados...

```sql
SELECT building_name FROM buildings b
LEFT JOIN employees e
ON b.building_name = e.building
WHERE e.building IS NULL
```
este codigo devuelve

| building_name |
| ------------- |
| 1w            |
| 2e            |
El left join con buildings primero, permite que se seleccionen todos los registros de building_name, incluso los que no tienen asignados trabajadores, luego, el IS NULL permite identificar los empleados que no estan asignados.

---

Ejemplo 2.

Este ejemplo implica bastante práctica sobre el lenguaje, dado que debemos tener una idea de lo que hace cada paso en las cláusulas, y cómo se van aplicando.

EJERCICIO:
*Se nos pide, encontrar el total de las ventas domésticas e internacionales, atribuibles a cada director. Esto implica que hay que sumar las ventas de cada película, y luego sumar las cantidades de las películas de cada director.*

Las tablas son las siguientes

**Tabla: Movies**

| id  | title               | director       | year | length_minutes |
| --- | ------------------- | -------------- | ---- | -------------- |
| 1   | Toy Story           | John Lasseter  | 1995 | 81             |
| 2   | A Bug's Life        | John Lasseter  | 1998 | 95             |
| 3   | Toy Story 2         | John Lasseter  | 1999 | 93             |
| 4   | Monsters, Inc.      | Pete Docter    | 2001 | 92             |
| 5   | Finding Nemo        | Andrew Stanton | 2003 | 107            |
| 6   | The Incredibles     | Brad Bird      | 2004 | 116            |
| 7   | Cars                | John Lasseter  | 2006 | 117            |
| 8   | Ratatouille         | Brad Bird      | 2007 | 115            |
| 9   | WALL-E              | Andrew Stanton | 2008 | 104            |
| 10  | Up                  | Pete Docter    | 2009 | 101            |
| 11  | Toy Story 3         | Lee Unkrich    | 2010 | 103            |
| 12  | Cars 2              | John Lasseter  | 2011 | 120            |
| 13  | Brave               | Brenda Chapman | 2012 | 102            |
| 14  | Monsters University | Dan Scanlon    | 2013 | 110            |


**Tabla: Boxoffice**

| movie_id | rating | domestic_sales | international_sales |
| -------- | ------ | -------------- | ------------------- |
| 5        | 8.2    | 380843261      | 555900000           |
| 14       | 7.4    | 268492764      | 475066843           |
| 8        | 8      | 206445654      | 417277164           |
| 12       | 6.4    | 191452396      | 368400000           |
| 3        | 7.9    | 245852179      | 239163000           |
| 6        | 8      | 261441092      | 370001000           |
| 9        | 8.5    | 223808164      | 297503696           |
| 11       | 8.4    | 415004880      | 648167031           |
| 1        | 8.3    | 191796233      | 170162503           |
| 7        | 7.2    | 244082982      | 217900167           |
| 10       | 8.3    | 293004164      | 438338580           |
| 4        | 8.1    | 289916256      | 272900000           |
| 2        | 7.2    | 162798565      | 200600000           |
| 13       | 7.2    | 237283207      | 301700000           |

La solución se da de la siguiente manera. Se que tengo que encontrar los totales por director, por lo tanto, una agrupación es necesaria dado que tenemos una expresión en el select para la suma.
Aparte, tenemos que vincular la tabla boxoffice con movies, por lo tanto, un join es necesario. y la vinculación se da con los ids de las películas. Por lo tanto, escribimos nuestra consulta SQL

```sql
SELECT Director, SUM(domestic_sales + international_sales) AS Total FROM
boxoffice b
LEFT JOIN movies m 
ON m.id = b.movie_id
GROUP BY director
```

la primer linea, nos indica que vamos a seleccionar la columna "Director", y la columa "Total" para mostrar, los directores y una suma, de la suma de las ventas domesticas e internacionales.
La primer suma obtiene el total por cada película, pero con solo esto, se obtiene registros duplicados de directores.
Usando el group by, obtenemos que la agregación SUM, nos sume la columna TOTAL de cada grupo generado de DIRECTOR, que contiene los registros de cada pelicula y su total de venta.

Con esto, tenemos el resultado de cuantas entradas en total, vendió cada director, sumando las entradas de cada película que dirigió.

