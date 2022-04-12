# Concepts SQL

## Proyection (Select)
Filtrar campos que se quieran mostrar(reducción vertical)
```mysql
-- Muestra todas los campos `select all` de una entidad
SELECT *; 
-- Muestra Campos especificos y `AS` agrega un alias
SELECT field AS alias;
/**
 * Operaciones matemáticas
 * COUNT - Cuenta el número elementos en un campo
 * SUM - Suma los valores de un campo
 * AVG - Valor promedio de un campo
 * MIN - Minimo valor de un campo
 * MAX - Maximo valor de un campo
 */
SELECT COUNT(id), SUM(quantity), AVG(age);
SELECT MIN(date), MAX(quantity);
-- Control structures
SELECT IF(500<1000, "YES", "NO");

SELECT OrderID, Quantity,
CASE
	WHEN Quantity > 30 THEN "Over 30"
	WHEN Quantity = 30 THEN "Equal 30"
	ELSE "Under 30"
END AS QuantityText
```
## Origen(From)
De donde se obtienen los datos
```mysql
-- All fields from table_diaria table_diaria
SELECT * FROM table_diaria;
-- Muestra todos los campos(*) de la union(JOIN) de dos tablas en
-- base a una condición(ON)
SELECT * FROM table_diaria AS td
	JOIN tabla_mensual AS tm
	ON td.pk = tm.fk;
```
## Productos Cartesianos(Join)
Involucra datos de distintas entidades
```mysql
-- Show campos con elementos en comun
SELECT * FROM table_diaria AS td
	JOIN tabla_mensual AS tm
	ON td.pk = tm.fk;
```
### Teoría de conjuntos
- Left Join
Pertenecen a la left table

- Exclusive Left Join
Pertenecen solo a la left table

- Right Join
Pertenecen a la right left

- Exclusive Right Join
Pertenecen solo a la right table

- Full Outer Join (Union)
Pertenecen a cualquier tabla

- Exclusive Full Outer Join
Pertenecen solo a una tabla

- Inner Join (intersección) or Join(default)
Pertenecen a ambas tablas a la vez

## Selección(Where)
Filtrar registros a mostrar(Reducción horizontal)
```mysql
-- Registros con el campo id igual a 1
SELECT *
FROM tabla_diaria
WHERE id = 1;
-- Registros con el campo cantidad mayor a 10
SELECT *
FROM tabla_diaria
WHERE cantidad > 10;
-- Registros con el campo cantidad menor a 10
SELECT *
FROM tabla_diaria
WHERE cantidad < 10;
-- Multiples sentecias WHERE
SELECT * FROM table_name
/**
 * AND - conjunción
 * BETWEEN- rango
 * OR - disyunción debil
 * LIKE - agregar comodides
 */
WHERE sentence AND other_sentence;
WHERE field BETWEEN limit_infierior AND limit_superior;
WHERE sentence AND (other_sentence OR other_sentence);
-- Uso de comodides
SELECT * FROM users
/**
 * LIKE - permite agregar comodides
 *	'%': Cualquier cantida de caracteres
 *	'_': Cualquier unico caracter
 */
WHERE name LIKE "Is%"; -- Ismael, Israel
WHERE name LIKE "Is_ael"; -- Israel
WHERE name NOT LIKE "Is_ael"; -- Ismmael
-- Others
WHERE name IS NULL;
WHERE name IS NOT NULL;
WHERE name IN ('Israel', 'Laura', 'Luis');
```
## Ordenamiento(Order by)
Ordena por cierto criterio
```mysql
-- Ordenar por campo específico
SELECT * FROM tabla_diaria
.
.
.
ORDER BY fecha;
ORDER BY fecha ASC; -- Ascendente(default)
ORDER BY fecha DESC; -- Descendente
```
### Índices
- Excelentes para búsquedas y ordenamientos
- Cuidar para alta transaccionalidad
## Agreagación(Group By)
Reducir los datos en grupos
```mysql
-- Van junto con COUNT, SUM, AVR, MIN, MAX
SELECT * FROM tabla_diaria
.
.
.
GROUP BY marca;
GROUP BY marca, modelo;
```
## Limitantes(Limit)
Especifica la cantidad final a mostrar
```mysql
-- Los primeros n registros
SELECT * FROM tabla_diaria
LIMIT 1500;
-- Los n2 registros a partir de los  n1 registros
SELECT * FROM tabla_diaria
OFFSET 1500
LIMIT 1500;
```
