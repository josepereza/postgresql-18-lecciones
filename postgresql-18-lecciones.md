**PostgreSQL 18**

Guía práctica completa - lecciones compiladas y actualizadas

*Tienda de electrónica · SQL · Administración · PL/pgSQL · Rendimiento*

Edición: noviembre de 2026

| **Contenido:** Compilación de las lecciones disponibles en esta conversación. La numeración original se conserva; no aparece una lección 20 en el hilo disponible. |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|

| **Uso recomendado:** Ejecuta los ejemplos en una base de pruebas PostgreSQL 18. Los objetos lN\_\* están pensados para evitar colisiones entre lecciones. |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------|

# Índice temático

Actualización incluida: lecciones 30-37 sobre concurrencia, bloqueos,
eventos, serialización, seguridad avanzada y observabilidad. La
numeración 20 no aparece en el historial disponible y no se inventa.

**Arquitectura, administración y monitorización**

> [<u>Lección 1: Arquitectura y rendimiento: entrada/salida asíncrona
> (AIO)</u>](#lección-1-arquitectura-y-rendimiento-entradasalida-asíncrona-aio)
>
> [<u>Lección 13: Monitorización con
> pg_stat_activity</u>](#lección-13-monitorización-con-pg_stat_activity)
>
> [<u>Lección 14: MVCC, VACUUM y
> ANALYZE</u>](#lección-14-mvcc-vacuum-y-analyze)
>
> [<u>Lección 15: Transacciones, SAVEPOINT y RETURNING
> old/new</u>](#lección-15-transacciones-savepoint-y-returning-oldnew)
>
> [<u>Lección 23: Particionamiento por fecha y partition
> pruning</u>](#lección-23-particionamiento-por-fecha-y-partition-pruning)

**Consultas SQL, JOIN, subconsultas y CTE**

> [<u>Lección 2: INNER JOIN y relaciones entre
> tablas</u>](#lección-2-inner-join-y-relaciones-entre-tablas)
>
> [<u>Lección 3: LEFT JOIN, NULL y
> COALESCE</u>](#lección-3-left-join-null-y-coalesce)
>
> [<u>Lección 4: Subconsultas correlacionadas con
> EXISTS</u>](#lección-4-subconsultas-correlacionadas-con-exists)
>
> [<u>Lección 5: CTE con WITH para dividir consultas
> complejas</u>](#lección-5-cte-con-with-para-dividir-consultas-complejas)
>
> [<u>Lección 29: CTE recursiva para
> jerarquías</u>](#lección-29-cte-recursiva-para-jerarquías)

**Funciones de ventana**

> [<u>Lección 6: ROW_NUMBER(), RANK() y PARTITION
> BY</u>](#lección-6-row_number-rank-y-partition-by)
>
> [<u>Lección 7: Marcos ROWS y
> acumulados</u>](#lección-7-marcos-rows-y-acumulados)
>
> [<u>Lección 24: Marcos GROUPS y
> EXCLUDE</u>](#lección-24-marcos-groups-y-exclude)

**Índices, EXPLAIN y rendimiento**

> [<u>Lección 8: Índices B-tree y lectura básica de
> EXPLAIN</u>](#lección-8-índices-b-tree-y-lectura-básica-de-explain)
>
> [<u>Lección 21: EXPLAIN ANALYZE: estimado vs
> real</u>](#lección-21-explain-analyze-estimado-vs-real)

**Roles, permisos y seguridad**

> [<u>Lección 9: Roles, permisos y mínimo
> privilegio</u>](#lección-9-roles-permisos-y-mínimo-privilegio)
>
> [<u>Lección 22: Row-Level Security (RLS) en un
> SaaS</u>](#lección-22-row-level-security-rls-en-un-saas)

**PL/pgSQL: funciones, procedimientos y triggers**

> [<u>Lección 10: Funciones PL/pgSQL</u>](#lección-10-funciones-plpgsql)
>
> [<u>Lección 11: Procedimientos almacenados con
> CALL</u>](#lección-11-procedimientos-almacenados-con-call)
>
> [<u>Lección 12: Triggers para controlar el
> stock</u>](#lección-12-triggers-para-controlar-el-stock)

**Funciones y modelado específicos de PostgreSQL 18**

> [<u>Lección 16: Columnas generadas
> virtuales</u>](#lección-16-columnas-generadas-virtuales)
>
> [<u>Lección 17: UUIDv7: identificadores ordenables por
> tiempo</u>](#lección-17-uuidv7-identificadores-ordenables-por-tiempo)
>
> [<u>Lección 18: Periodos sin solapamiento con WITHOUT
> OVERLAPS</u>](#lección-18-periodos-sin-solapamiento-con-without-overlaps)
>
> [<u>Lección 19: Claves foráneas temporales con
> PERIOD</u>](#lección-19-claves-foráneas-temporales-con-period)
>
> [<u>Lección 25: COPY tolerante a errores:
> REJECT_LIMIT</u>](#lección-25-copy-tolerante-a-errores-reject_limit)
>
> [<u>Lección 26: Vistas materializadas para
> informes</u>](#lección-26-vistas-materializadas-para-informes)
>
> [<u>Lección 27: Búsquedas Unicode con
> casefold()</u>](#lección-27-búsquedas-unicode-con-casefold)
>
> [<u>Lección 28: Búsqueda aproximada con
> pg_trgm</u>](#lección-28-búsqueda-aproximada-con-pg_trgm)

# Arquitectura, administración y monitorización

Este bloque agrupa las lecciones relacionadas para estudiar el tema de
forma progresiva.

## Lección 1 · Arquitectura y rendimiento: entrada/salida asíncrona (AIO)

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

PostgreSQL 18 incorpora una infraestructura de E/S asíncrona que permite
solapar varias operaciones de lectura. El parámetro io_method controla
el método de E/S y permite usar worker, sync o io_uring cuando está
disponible.

### Ejemplo ejecutable

SHOW server_version;  
SHOW io_method;  
SHOW effective_io_concurrency;  
  
SELECT name, setting, unit, context  
FROM pg_settings  
WHERE name IN ('io_method','io_workers','effective_io_concurrency')  
ORDER BY name;

### Resultado esperado

| **Comprobación:** Debes ver una versión 18.x. io_method mostrará el método activo; el valor exacto depende de cómo se haya compilado y configurado el servidor. |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Explica qué diferencia práctica hay entre un método síncrono y uno
asíncrono cuando PostgreSQL necesita leer muchos bloques del
almacenamiento.

### Solución explicada

En el método síncrono una operación espera a que termine la anterior. En
AIO PostgreSQL puede emitir varias solicitudes y aprovechar mejor el
dispositivo, reduciendo tiempos muertos. La mejora real depende del
almacenamiento y del plan de ejecución.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: nueva infraestructura AIO y parámetros asociados. No toda consulta se acelera automáticamente. |
|---------------------------------------------------------------------------------------------------------------------------------------|

## Lección 13 · Monitorización con pg_stat_activity

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

pg_stat_activity muestra una fila por proceso de servidor y permite ver
usuario, aplicación, estado, consulta y eventos de espera.

### Ejemplo ejecutable

SET application_name='tienda_monitor';  
  
SELECT
pid,datname,usename,application_name,state,wait_event_type,wait_event  
FROM pg_stat_activity  
WHERE pid=pg_backend_pid();  
  
SELECT pid,usename,now()-query_start AS
duracion,wait_event_type,wait_event  
FROM pg_stat_activity  
WHERE state='active' AND pid\<\>pg_backend_pid()  
ORDER BY query_start;

### Resultado esperado

| **Comprobación:** Tu sesión debe aparecer con application_name = tienda_monitor. Los demás resultados dependen de la actividad real del servidor. |
|---------------------------------------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Cuenta cuántos procesos bloquean tu sesión.

### Solución explicada

SELECT cardinality(pg_blocking_pids(pg_backend_pid()));

### PostgreSQL 18

| **Versión:** pg_stat_activity no es nuevo. PostgreSQL 18 añade funciones/vistas relacionadas con NUMA cuando el servidor lo soporta. |
|--------------------------------------------------------------------------------------------------------------------------------------|

## Lección 14 · MVCC, VACUUM y ANALYZE

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

MVCC conserva versiones de filas para mantener consistencia entre
transacciones. VACUUM permite reutilizar versiones muertas y ANALYZE
actualiza estadísticas.

### Ejemplo ejecutable

CREATE TEMP TABLE l14_productos(id int PRIMARY KEY,stock int);  
INSERT INTO l14_productos SELECT n,n%20 FROM generate_series(1,10000)
n;  
DELETE FROM l14_productos WHERE id\<=8000;  
VACUUM (ANALYZE) l14_productos;  
SELECT COUNT(\*) AS filas FROM l14_productos;  
SELECT reltuples::bigint FROM pg_class WHERE
oid='l14_productos'::regclass;

### Resultado esperado

| **Comprobación:** COUNT(\*) = 2000. reltuples será aproximadamente 2000 después de ANALYZE. |
|---------------------------------------------------------------------------------------------|

### Ejercicio práctico

Elimina stock=0, ejecuta VACUUM ANALYZE y comprueba cuántas filas
quedan.

### Solución explicada

Quedarán 1900 filas. VACUUM normal no suele reducir el archivo en disco;
deja el espacio reutilizable.

### PostgreSQL 18

| **Versión:** MVCC y VACUUM son históricos. PostgreSQL 18 habilita checksums de páginas por defecto en clústeres nuevos creados con initdb. |
|--------------------------------------------------------------------------------------------------------------------------------------------|

## Lección 15 · Transacciones, SAVEPOINT y RETURNING old/new

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

BEGIN/COMMIT agrupan operaciones. SAVEPOINT permite deshacer solo una
parte. PostgreSQL 18 amplía RETURNING para exponer valores old/new
explícitamente.

### Ejemplo ejecutable

CREATE TEMP TABLE l15_productos(id int PRIMARY KEY,nombre text,stock
int);  
INSERT INTO l15_productos VALUES (1,'Teclado',5);  
BEGIN;  
SAVEPOINT antes;  
UPDATE l15_productos  
SET stock=stock-2  
WHERE id=1 AND stock\>=2  
RETURNING nombre,old.stock AS anterior,new.stock AS nuevo;  
ROLLBACK TO SAVEPOINT antes;  
SELECT \* FROM l15_productos;  
COMMIT;

### Resultado esperado

| **Comprobación:** RETURNING muestra 5 -\> 3, pero después del ROLLBACK TO SAVEPOINT el stock vuelve a 5. |
|----------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Crea una transacción que inserte un pedido, descuente stock y luego la
cancele completamente.

### Solución explicada

Usa BEGIN, realiza las operaciones y termina con ROLLBACK. Ningún cambio
debe permanecer.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: referencias old/new explícitas en RETURNING para DML. |
|----------------------------------------------------------------------------------------------|

## Lección 23 · Particionamiento por fecha y partition pruning

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

El particionamiento divide físicamente una tabla grande. El pruning
elimina del plan las particiones imposibles según el filtro.

### Ejemplo ejecutable

CREATE TABLE l23_pedidos(id int,fecha date,total numeric(10,2),PRIMARY
KEY(id,fecha)) PARTITION BY RANGE(fecha);  
CREATE TABLE l23_2026_01 PARTITION OF l23_pedidos FOR VALUES FROM
('2026-01-01') TO ('2026-02-01');  
CREATE TABLE l23_2026_02 PARTITION OF l23_pedidos FOR VALUES FROM
('2026-02-01') TO ('2026-03-01');  
INSERT INTO l23_pedidos VALUES
(1,'2026-01-10',100),(2,'2026-02-10',200);  
EXPLAIN (COSTS OFF) SELECT \* FROM l23_pedidos WHERE
fecha\>='2026-02-01' AND fecha\<'2026-03-01';

### Resultado esperado

| **Comprobación:** El plan debe considerar solo la partición l23_2026_02 cuando enable_partition_pruning=on. |
|-------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Añade una partición de marzo e inserta un pedido del 5 de marzo.

### Solución explicada

Crea FOR VALUES FROM ('2026-03-01') TO ('2026-04-01'); inserta en la
tabla padre y verifica tableoid.

### PostgreSQL 18

| **Versión:** El particionamiento ya existía; PostgreSQL 18 mejora planificación/costes para tablas con muchas particiones. |
|----------------------------------------------------------------------------------------------------------------------------|

# Consultas SQL, JOIN, subconsultas y CTE

Este bloque agrupa las lecciones relacionadas para estudiar el tema de
forma progresiva.

## Lección 2 · INNER JOIN y relaciones entre tablas

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

INNER JOIN combina filas que tienen coincidencia en ambas tablas. Es la
base para reconstruir la información normalizada de clientes, pedidos,
productos y líneas.

### Ejemplo ejecutable

CREATE TEMP TABLE l2_clientes(cliente_id int PRIMARY KEY,nombre text);  
CREATE TEMP TABLE l2_pedidos(pedido_id int PRIMARY KEY,cliente_id int
REFERENCES l2_clientes);  
CREATE TEMP TABLE l2_lineas(pedido_id int REFERENCES l2_pedidos,producto
text,cantidad int,precio numeric(10,2));  
INSERT INTO l2_clientes VALUES (1,'Ana'),(2,'Luis');  
INSERT INTO l2_pedidos VALUES (101,1),(102,2);  
INSERT INTO l2_lineas VALUES
(101,'Teclado',2,50),(101,'Ratón',1,25),(102,'Monitor',1,300);  
  
SELECT c.nombre,p.pedido_id,SUM(l.cantidad\*l.precio) AS total  
FROM l2_pedidos p  
JOIN l2_clientes c ON c.cliente_id=p.cliente_id  
JOIN l2_lineas l ON l.pedido_id=p.pedido_id  
GROUP BY c.nombre,p.pedido_id  
ORDER BY p.pedido_id;

### Resultado esperado

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Comprobación:</strong> Ana | 101 | 125.00<br />
Luis | 102 | 300.00</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### Ejercicio práctico

Añade una columna con el número total de unidades de cada pedido.

### Solución explicada

Añade SUM(l.cantidad) AS unidades al SELECT. Como ya agrupamos por
pedido, la suma se calcula dentro de cada pedido.

### PostgreSQL 18

| **Versión:** JOIN y claves foráneas no son novedades de PostgreSQL 18. |
|------------------------------------------------------------------------|

## Lección 3 · LEFT JOIN, NULL y COALESCE

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

LEFT JOIN conserva todas las filas de la tabla izquierda aunque no
exista coincidencia. COALESCE permite sustituir NULL por un valor
alternativo, por ejemplo 0.

### Ejemplo ejecutable

CREATE TEMP TABLE l3_clientes(id int PRIMARY KEY,nombre text);  
CREATE TEMP TABLE l3_pedidos(id int PRIMARY KEY,cliente_id int
REFERENCES l3_clientes,total numeric(10,2));  
INSERT INTO l3_clientes VALUES (1,'Ana'),(2,'Luis'),(3,'Marta');  
INSERT INTO l3_pedidos VALUES (101,1,125),(102,2,300);  
  
SELECT c.nombre,COUNT(p.id) AS pedidos,COALESCE(SUM(p.total),0) AS
total  
FROM l3_clientes c  
LEFT JOIN l3_pedidos p ON p.cliente_id=c.id  
GROUP BY c.id,c.nombre  
ORDER BY c.id;

### Resultado esperado

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Comprobación:</strong> Ana | 1 | 125.00<br />
Luis | 1 | 300.00<br />
Marta | 0 | 0</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### Ejercicio práctico

Muestra todos los productos y sus unidades vendidas, incluyendo
productos nunca vendidos con 0.

### Solución explicada

Coloca productos a la izquierda, usa LEFT JOIN con líneas de pedido y
COALESCE(SUM(cantidad),0).

### PostgreSQL 18

| **Versión:** LEFT JOIN y COALESCE son conceptos consolidados anteriores a PostgreSQL 18. |
|------------------------------------------------------------------------------------------|

## Lección 4 · Subconsultas correlacionadas con EXISTS

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

EXISTS responde si la subconsulta produce al menos una fila. Es muy útil
para “clientes con pedidos” o “productos nunca vendidos”.

### Ejemplo ejecutable

CREATE TEMP TABLE l4_clientes(id int PRIMARY KEY,nombre text);  
CREATE TEMP TABLE l4_pedidos(id int PRIMARY KEY,cliente_id int
REFERENCES l4_clientes);  
INSERT INTO l4_clientes VALUES (1,'Ana'),(2,'Luis'),(3,'Marta');  
INSERT INTO l4_pedidos VALUES (101,1),(102,2);  
  
SELECT c.nombre  
FROM l4_clientes c  
WHERE EXISTS (  
SELECT 1 FROM l4_pedidos p  
WHERE p.cliente_id=c.id  
)  
ORDER BY c.id;

### Resultado esperado

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Comprobación:</strong> Ana<br />
Luis</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### Ejercicio práctico

Devuelve los clientes que no han realizado pedidos.

### Solución explicada

Cambia EXISTS por NOT EXISTS. Marta será el único resultado.

### PostgreSQL 18

| **Versión:** EXISTS y NOT EXISTS no son novedades de PostgreSQL 18. |
|---------------------------------------------------------------------|

## Lección 5 · CTE con WITH para dividir consultas complejas

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Una CTE da nombre a un resultado intermedio durante una consulta. Mejora
la legibilidad y permite reutilizar cálculos como totales por pedido.

### Ejemplo ejecutable

CREATE TEMP TABLE l5_lineas(pedido_id int,cantidad int,precio
numeric(10,2));  
INSERT INTO l5_lineas VALUES
(101,2,50),(101,1,25),(102,1,300),(103,1,80);  
  
WITH totales AS (  
SELECT pedido_id,SUM(cantidad\*precio) AS total  
FROM l5_lineas  
GROUP BY pedido_id  
)  
SELECT pedido_id,total  
FROM totales  
WHERE total \> (SELECT AVG(total) FROM totales)  
ORDER BY pedido_id;

### Resultado esperado

| **Comprobación:** 102 \| 300.00 |
|---------------------------------|

### Ejercicio práctico

Devuelve el pedido con el menor total utilizando la misma CTE.

### Solución explicada

Ordena total ASC y usa LIMIT 1, o compara con MIN(total).

### PostgreSQL 18

| **Versión:** Las CTE existen desde versiones antiguas. PostgreSQL puede integrar CTE no materializadas en el plan cuando es seguro. |
|-------------------------------------------------------------------------------------------------------------------------------------|

## Lección 29 · CTE recursiva para jerarquías

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

WITH RECURSIVE permite recorrer árboles de profundidad variable:
categorías, organigramas o dependencias. Conviene protegerse contra
ciclos.

### Ejemplo ejecutable

CREATE TEMP TABLE l29_cat(id int PRIMARY KEY,nombre text,padre_id int
REFERENCES l29_cat);  
INSERT INTO l29_cat VALUES
(1,'Electrónica',NULL),(2,'Ordenadores',1),(3,'Accesorios',1),(4,'Portátiles',2),(5,'Teclados',3),(6,'Ratones',3);  
  
WITH RECURSIVE arbol AS (  
SELECT id,nombre,padre_id,0 nivel,ARRAY\[id\] ruta FROM l29_cat WHERE
padre_id IS NULL  
UNION ALL  
SELECT c.id,c.nombre,c.padre_id,a.nivel+1,a.ruta\|\|c.id  
FROM l29_cat c JOIN arbol a ON c.padre_id=a.id  
WHERE NOT c.id=ANY(a.ruta)  
)  
SELECT repeat(' ',nivel)\|\|nombre AS categoria,nivel,ruta  
FROM arbol ORDER BY ruta;

### Resultado esperado

| **Comprobación:** Electrónica -\> Ordenadores -\> Portátiles; Electrónica -\> Accesorios -\> Teclados/Ratones. |
|----------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Obtén todas las subcategorías de Accesorios y suma el stock de sus
productos.

### Solución explicada

Usa una CTE recursiva que empiece en id=3 y JOIN final con productos;
suma el stock de todas las categorías alcanzadas.

### PostgreSQL 18

| **Versión:** Las CTE recursivas y CYCLE ya existían. PostgreSQL 18 mejora observabilidad de nodos relacionados en EXPLAIN. |
|----------------------------------------------------------------------------------------------------------------------------|

# Funciones de ventana

Este bloque agrupa las lecciones relacionadas para estudiar el tema de
forma progresiva.

## Lección 6 · ROW_NUMBER(), RANK() y PARTITION BY

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Las funciones de ventana calculan sobre varias filas sin colapsarlas.
ROW_NUMBER asigna una secuencia única; RANK conserva empates y deja
huecos.

### Ejemplo ejecutable

CREATE TEMP TABLE l6_pedidos(id int PRIMARY KEY,cliente text,total
numeric(10,2));  
INSERT INTO l6_pedidos VALUES
(101,'Ana',125),(102,'Luis',300),(103,'Ana',80),(104,'Ana',125),(105,'Luis',120);  
  
SELECT id,cliente,total,  
ROW_NUMBER() OVER(PARTITION BY cliente ORDER BY total DESC,id) AS pos,  
RANK() OVER(PARTITION BY cliente ORDER BY total DESC) AS rango  
FROM l6_pedidos  
ORDER BY cliente,pos;

### Resultado esperado

| **Comprobación:** Ana: 125 -\> pos 1/rango 1; 125 -\> pos 2/rango 1; 80 -\> pos 3/rango 3. Luis: 300 -\> 1; 120 -\> 2. |
|------------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Obtén solo el pedido de mayor importe de cada cliente.

### Solución explicada

Calcula ROW_NUMBER() en una CTE y filtra pos = 1 en la consulta
exterior.

### PostgreSQL 18

| **Versión:** Las funciones de ventana no son nuevas en PostgreSQL 18. |
|-----------------------------------------------------------------------|

## Lección 7 · Marcos ROWS y acumulados

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

El marco delimita qué filas de una partición utiliza la función de
ventana. ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW produce
acumulados.

### Ejemplo ejecutable

CREATE TEMP TABLE l7_ventas(id int,fecha date,total numeric(10,2));  
INSERT INTO l7_ventas VALUES
(1,'2026-10-15',100),(2,'2026-10-16',150),(3,'2026-10-17',80),(4,'2026-10-18',220);  
  
SELECT id,fecha,total,  
SUM(total) OVER(ORDER BY fecha,id ROWS BETWEEN UNBOUNDED PRECEDING AND
CURRENT ROW) AS acumulado,  
ROUND(AVG(total) OVER(ORDER BY fecha,id ROWS BETWEEN 2 PRECEDING AND
CURRENT ROW),2) AS media3  
FROM l7_ventas  
ORDER BY fecha,id;

### Resultado esperado

| **Comprobación:** Acumulado: 100, 250, 330, 550. Media móvil de 3: 100, 125, 110, 150. |
|----------------------------------------------------------------------------------------|

### Ejercicio práctico

Calcula un acumulado independiente para cada cliente.

### Solución explicada

Añade PARTITION BY cliente dentro de OVER(...).

### PostgreSQL 18

| **Versión:** ROWS, RANGE y GROUPS ya existían antes de PostgreSQL 18. |
|-----------------------------------------------------------------------|

## Lección 24 · Marcos GROUPS y EXCLUDE

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

GROUPS cuenta grupos de pares con el mismo ORDER BY. EXCLUDE permite
quitar la fila actual, sus pares o el grupo completo del marco.

### Ejemplo ejecutable

CREATE TEMP TABLE l24_pedidos(id int,cliente text,fecha date,total
numeric(10,2));  
INSERT INTO l24_pedidos VALUES
(101,'Ana','2026-01-01',100),(102,'Ana','2026-01-01',50),(103,'Ana','2026-01-02',80),(104,'Ana','2026-01-03',120);  
  
SELECT id,fecha,total,  
COALESCE(SUM(total) OVER(  
PARTITION BY cliente ORDER BY fecha  
GROUPS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW  
EXCLUDE GROUP  
),0) AS anteriores  
FROM l24_pedidos  
ORDER BY fecha,id;

### Resultado esperado

| **Comprobación:** Para 1 de enero -\> 0; 2 de enero -\> 150; 3 de enero -\> 230. |
|----------------------------------------------------------------------------------|

### Ejercicio práctico

Compara GROUPS BETWEEN 1 PRECEDING AND CURRENT ROW con ROWS BETWEEN 1
PRECEDING AND CURRENT ROW.

### Solución explicada

GROUPS incluye el grupo completo de la fecha anterior; ROWS solo una
fila física anterior.

### PostgreSQL 18

| **Versión:** GROUPS y EXCLUDE existen desde antes; PostgreSQL 18 mejora rendimiento/observabilidad de algunos agregados de ventana. |
|-------------------------------------------------------------------------------------------------------------------------------------|

# Índices, EXPLAIN y rendimiento

Este bloque agrupa las lecciones relacionadas para estudiar el tema de
forma progresiva.

## Lección 8 · Índices B-tree y lectura básica de EXPLAIN

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Un índice puede reducir las filas y bloques que PostgreSQL necesita
visitar, pero el planificador decide si usarlo. EXPLAIN muestra el plan
estimado.

### Ejemplo ejecutable

CREATE TEMP TABLE l8_pedidos(id int PRIMARY KEY,cliente_id int,fecha
date,total numeric(10,2));  
INSERT INTO l8_pedidos  
SELECT n,((n-1)%500)+1,DATE
'2026-01-01'+(n%365),(10+n%990)::numeric(10,2)  
FROM generate_series(1,20000) n;  
ANALYZE l8_pedidos;  
  
CREATE INDEX l8_cliente_fecha_idx ON l8_pedidos(cliente_id,fecha);  
EXPLAIN (ANALYZE, BUFFERS)  
SELECT id,fecha,total  
FROM l8_pedidos  
WHERE cliente_id=42 AND fecha\>=DATE '2026-07-01'  
ORDER BY fecha;

### Resultado esperado

| **Comprobación:** El plan puede usar Index Scan o Bitmap Index/Heap Scan. El plan exacto depende de estadísticas y costes. |
|----------------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

¿Qué índice crearías para búsquedas frecuentes solo por fecha?

### Solución explicada

CREATE INDEX ... ON l8_pedidos(fecha); aunque PostgreSQL 18 puede
considerar skip scan en ciertos índices multicolumna, no sustituye
siempre a un índice específico.

### PostgreSQL 18

| **Versión:** PostgreSQL 18 añade B-tree skip scan, útil en algunos casos donde falta una condición sobre la primera columna del índice. |
|-----------------------------------------------------------------------------------------------------------------------------------------|

## Lección 21 · EXPLAIN ANALYZE: estimado vs real

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

EXPLAIN ANALYZE ejecuta la consulta y permite comparar rows estimadas
con actual rows, además de tiempo, loops, buffers y memoria de
planificación.

### Ejemplo ejecutable

CREATE TEMP TABLE l21_pedidos(id int PRIMARY KEY,cliente_id int,fecha
date,total numeric(10,2));  
INSERT INTO l21_pedidos  
SELECT n,(n%100)+1,DATE '2026-01-01'+(n%365),(20+n%500)::numeric(10,2)  
FROM generate_series(1,100000) n;  
ANALYZE l21_pedidos;  
CREATE INDEX l21_cliente_fecha_idx ON l21_pedidos(cliente_id,fecha);  
EXPLAIN (ANALYZE, BUFFERS, MEMORY)  
SELECT COUNT(\*),SUM(total) FROM l21_pedidos  
WHERE cliente_id=42 AND fecha\>=DATE '2026-06-01' AND fecha\<DATE
'2026-07-01';

### Resultado esperado

| **Comprobación:** Debe aparecer un plan real. El nodo puede ser Index Scan o Bitmap. Compara rows vs actual rows y buffers. |
|-----------------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Analiza cliente 73 durante septiembre y compara el plan.

### Solución explicada

Cambia cliente y rango de fechas. La combinación cliente_id+fecha puede
usar el mismo índice multicolumna.

### PostgreSQL 18

| **Versión:** PostgreSQL 18 mejora la observabilidad de EXPLAIN, incluida información adicional de memoria y búsquedas en índices. |
|-----------------------------------------------------------------------------------------------------------------------------------|

# Roles, permisos y seguridad

Este bloque agrupa las lecciones relacionadas para estudiar el tema de
forma progresiva.

## Lección 9 · Roles, permisos y mínimo privilegio

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

En PostgreSQL todo son roles. Los roles con LOGIN actúan como usuarios;
los roles NOLOGIN son buenos grupos de permisos.

### Ejemplo ejecutable

BEGIN;  
CREATE ROLE l9_lectura NOLOGIN;  
CREATE ROLE l9_empleado NOLOGIN;  
GRANT l9_lectura TO l9_empleado;  
CREATE SCHEMA l9_tienda;  
CREATE TABLE l9_tienda.productos(id int PRIMARY KEY,nombre text);  
GRANT USAGE ON SCHEMA l9_tienda TO l9_lectura;  
GRANT SELECT ON l9_tienda.productos TO l9_lectura;  
  
SELECT has_table_privilege('l9_empleado','l9_tienda.productos','SELECT')
AS puede_leer,  
has_table_privilege('l9_empleado','l9_tienda.productos','INSERT') AS
puede_insertar;  
ROLLBACK;

### Resultado esperado

| **Comprobación:** puede_leer = true; puede_insertar = false. |
|--------------------------------------------------------------|

### Ejercicio práctico

Crea un grupo de ventas con INSERT, pero sin UPDATE ni DELETE.

### Solución explicada

CREATE ROLE ... NOLOGIN; GRANT INSERT ON ... TO ...; después GRANT el
grupo al rol del empleado.

### PostgreSQL 18

| **Versión:** PostgreSQL 18 añade pg_get_acl() para consultar ACL de objetos de forma más uniforme. |
|----------------------------------------------------------------------------------------------------|

## Lección 22 · Row-Level Security (RLS) en un SaaS

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

RLS filtra filas según políticas dentro de la base de datos. USING
controla qué filas se ven/modifican; WITH CHECK valida nuevas filas.

### Ejemplo ejecutable

CREATE SCHEMA l22;  
CREATE TABLE l22.pedidos(id int PRIMARY KEY,tienda_id int,cliente
text,total numeric(10,2));  
ALTER TABLE l22.pedidos ENABLE ROW LEVEL SECURITY;  
CREATE ROLE l22_tienda_1 NOLOGIN;  
GRANT SELECT,INSERT,UPDATE ON l22.pedidos TO l22_tienda_1;  
GRANT USAGE ON SCHEMA l22 TO l22_tienda_1;  
CREATE POLICY tienda1 ON l22.pedidos TO l22_tienda_1  
USING (tienda_id=1) WITH CHECK (tienda_id=1);

### Resultado esperado

| **Comprobación:** El rol solo puede ver/modificar filas con tienda_id=1 y no puede insertar filas para otra tienda. |
|---------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Crea una política equivalente para tienda 2.

### Solución explicada

Usa otra política TO l22_tienda_2 con USING/WITH CHECK tienda_id=2.

### PostgreSQL 18

| **Versión:** RLS no es nuevo. PostgreSQL 18 añade OAuth y continúa la transición hacia autenticación más moderna; RLS sigue siendo autorización a nivel de filas. |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|

# PL/pgSQL: funciones, procedimientos y triggers

Este bloque agrupa las lecciones relacionadas para estudiar el tema de
forma progresiva.

## Lección 10 · Funciones PL/pgSQL

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Una función puede recibir parámetros, consultar datos y devolver un
valor. SELECT ... INTO asigna el resultado a una variable local.

### Ejemplo ejecutable

CREATE TEMP TABLE l10_lineas(pedido_id int,cantidad int,precio
numeric(10,2));  
INSERT INTO l10_lineas VALUES (101,2,50),(101,1,25),(102,1,300);  
  
CREATE OR REPLACE FUNCTION pg_temp.total_pedido(p_id int)  
RETURNS numeric(12,2) LANGUAGE plpgsql STABLE AS \$\$  
DECLARE v_total numeric(12,2);  
BEGIN  
SELECT COALESCE(SUM(cantidad\*precio),0)::numeric(12,2) INTO v_total  
FROM l10_lineas WHERE pedido_id=p_id;  
RETURN v_total;  
END;\$\$;  
  
SELECT pg_temp.total_pedido(101),pg_temp.total_pedido(999);

### Resultado esperado

| **Comprobación:** 125.00 \| 0.00 |
|----------------------------------|

### Ejercicio práctico

Crea una función total_con_descuento(pedido, porcentaje) que valide
0–100.

### Solución explicada

Usa IF para validar, llama a total_pedido y devuelve ROUND(total \* (1 -
descuento/100), 2).

### PostgreSQL 18

| **Versión:** PL/pgSQL, STABLE, variables y SELECT INTO ya existían antes de PostgreSQL 18. |
|--------------------------------------------------------------------------------------------|

## Lección 11 · Procedimientos almacenados con CALL

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Los procedimientos representan operaciones de negocio y se ejecutan con
CALL. Pueden modificar varias tablas y, en ciertos contextos, controlar
transacciones.

### Ejemplo ejecutable

CREATE TEMP TABLE l11_pedidos(id int PRIMARY KEY,total
numeric(12,2),estado text DEFAULT 'pendiente');  
CREATE TEMP TABLE l11_pagos(id int GENERATED ALWAYS AS IDENTITY PRIMARY
KEY,pedido_id int,importe numeric(12,2));  
INSERT INTO l11_pedidos(id,total) VALUES (101,125),(102,300);  
  
CREATE OR REPLACE PROCEDURE pg_temp.registrar_pago(p_id int,p_importe
numeric)  
LANGUAGE plpgsql AS \$\$  
DECLARE v_total numeric; v_pagado numeric;  
BEGIN  
SELECT total INTO v_total FROM l11_pedidos WHERE id=p_id;  
IF NOT FOUND THEN RAISE EXCEPTION 'Pedido no existe'; END IF;  
SELECT COALESCE(SUM(importe),0) INTO v_pagado FROM l11_pagos WHERE
pedido_id=p_id;  
IF v_pagado+p_importe\>v_total THEN RAISE EXCEPTION 'Pago supera saldo';
END IF;  
INSERT INTO l11_pagos(pedido_id,importe) VALUES(p_id,p_importe);  
IF v_pagado+p_importe=v_total THEN UPDATE l11_pedidos SET
estado='pagado' WHERE id=p_id; END IF;  
END;\$\$;  
CALL pg_temp.registrar_pago(101,125);

### Resultado esperado

| **Comprobación:** El pedido 101 queda con estado pagado. |
|----------------------------------------------------------|

### Ejercicio práctico

Crea un procedimiento para marcar enviado solo si el pedido está pagado.

### Solución explicada

UPDATE ... WHERE id=p_id AND estado='pagado'; IF NOT FOUND THEN RAISE
EXCEPTION ... END IF;

### PostgreSQL 18

| **Versión:** CALL y procedimientos no son novedades de PostgreSQL 18. |
|-----------------------------------------------------------------------|

## Lección 12 · Triggers para controlar el stock

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Un trigger ejecuta una función automáticamente ante
INSERT/UPDATE/DELETE. NEW representa la fila nueva y OLD la fila
anterior.

### Ejemplo ejecutable

CREATE TEMP TABLE l12_productos(id int PRIMARY KEY,nombre text,stock int
CHECK(stock\>=0));  
CREATE TEMP TABLE l12_lineas(id int PRIMARY KEY,producto_id int
REFERENCES l12_productos,cantidad int CHECK(cantidad\>0));  
INSERT INTO l12_productos VALUES (1,'Teclado',5),(2,'Ratón',2);  
  
CREATE OR REPLACE FUNCTION pg_temp.descontar_stock() RETURNS trigger
LANGUAGE plpgsql AS \$\$  
BEGIN  
UPDATE l12_productos  
SET stock=stock-NEW.cantidad  
WHERE id=NEW.producto_id AND stock\>=NEW.cantidad;  
IF NOT FOUND THEN RAISE EXCEPTION 'Stock insuficiente'; END IF;  
RETURN NEW;  
END;\$\$;  
  
CREATE TRIGGER l12_stock_trg BEFORE INSERT ON l12_lineas  
FOR EACH ROW EXECUTE FUNCTION pg_temp.descontar_stock();  
  
INSERT INTO l12_lineas VALUES (1,1,2);  
SELECT \* FROM l12_productos ORDER BY id;

### Resultado esperado

| **Comprobación:** Teclado queda con stock 3; Ratón sigue con 2. |
|-----------------------------------------------------------------|

### Ejercicio práctico

Crea un trigger AFTER DELETE que reponga OLD.cantidad al stock.

### Solución explicada

UPDATE productos SET stock=stock+OLD.cantidad WHERE id=OLD.producto_id;
RETURN OLD;

### PostgreSQL 18

| **Versión:** Triggers, NEW y OLD son funcionalidades anteriores a PostgreSQL 18. |
|----------------------------------------------------------------------------------|

# Funciones y modelado específicos de PostgreSQL 18

Este bloque agrupa las lecciones relacionadas para estudiar el tema de
forma progresiva.

## Lección 16 · Columnas generadas virtuales

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Una columna generada virtual se calcula al leer la fila y no almacena
físicamente el valor derivado.

### Ejemplo ejecutable

CREATE TEMP TABLE l16_lineas(  
id int PRIMARY KEY,  
cantidad int,  
precio numeric(10,2),  
descuento numeric(5,2) DEFAULT 0,  
subtotal numeric(12,2) GENERATED ALWAYS AS
(ROUND(cantidad\*precio\*(1-descuento/100),2)) VIRTUAL  
);  
INSERT INTO l16_lineas(id,cantidad,precio,descuento) VALUES
(1,2,50,0),(2,1,25,10);  
SELECT \* FROM l16_lineas ORDER BY id;

### Resultado esperado

| **Comprobación:** Fila 1 subtotal 100.00; fila 2 subtotal 22.50. |
|------------------------------------------------------------------|

### Ejercicio práctico

Añade una columna virtual total_con_impuesto con un factor 1.08.

### Solución explicada

ALTER TABLE ... ADD COLUMN ... GENERATED ALWAYS AS
(ROUND(cantidad\*precio\*(1-descuento/100)\*1.08,2)) VIRTUAL;

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: columnas generadas VIRTUAL y opción virtual por defecto cuando no se especifica STORED. |
|--------------------------------------------------------------------------------------------------------------------------------|

## Lección 17 · UUIDv7: identificadores ordenables por tiempo

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

UUIDv7 incorpora información temporal y es útil como clave distribuida
con mejor localidad que UUIDv4.

### Ejemplo ejecutable

CREATE TEMP TABLE l17_pedidos(id uuid PRIMARY KEY DEFAULT
uuidv7(),cliente text,total numeric(10,2));  
INSERT INTO l17_pedidos(cliente,total) VALUES
('Ana',125),('Luis',300),('Marta',80);  
SELECT cliente,uuid_extract_version(id) AS
version,uuid_extract_timestamp(id) AS momento  
FROM l17_pedidos  
ORDER BY id;

### Resultado esperado

| **Comprobación:** Todos los UUID tendrán version = 7. Las marcas temporales serán próximas al momento de inserción. |
|---------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Genera UUIDv7 desplazados -2 days, -1 day y actual; ordénalos por UUID.

### Solución explicada

Usa uuidv7(interval) y ORDER BY id. El orden reflejará aproximadamente
la secuencia temporal.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: uuidv7(), uuidv4() y funciones de extracción asociadas. |
|------------------------------------------------------------------------------------------------|

## Lección 18 · Periodos sin solapamiento con WITHOUT OVERLAPS

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

PostgreSQL 18 permite expresar claves temporales que prohíben periodos
solapados para un mismo identificador.

### Ejemplo ejecutable

CREATE EXTENSION IF NOT EXISTS btree_gist;  
CREATE TEMP TABLE l18_precios(  
producto_id int NOT NULL,  
vigencia daterange NOT NULL,  
precio numeric(10,2) NOT NULL,  
PRIMARY KEY(producto_id,vigencia WITHOUT OVERLAPS)  
);  
INSERT INTO l18_precios VALUES  
(1,daterange('2026-01-01','2026-04-01','\[)'),300),  
(1,daterange('2026-04-01','2026-07-01','\[)'),280);  
SELECT \* FROM l18_precios WHERE vigencia @\> DATE '2026-05-15';

### Resultado esperado

| **Comprobación:** Se devuelve el periodo 2026-04-01 a 2026-07-01 con precio 280. |
|----------------------------------------------------------------------------------|

### Ejercicio práctico

Intenta insertar un periodo 2026-03-15 a 2026-05-01 para el mismo
producto.

### Solución explicada

La restricción debe rechazarlo porque se solapa con periodos existentes.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: sintaxis WITHOUT OVERLAPS en claves UNIQUE/PRIMARY KEY. |
|------------------------------------------------------------------------------------------------|

## Lección 19 · Claves foráneas temporales con PERIOD

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

PERIOD permite exigir que un intervalo de la tabla hija esté
completamente cubierto por intervalos válidos de la tabla padre.

### Ejemplo ejecutable

CREATE EXTENSION IF NOT EXISTS btree_gist;  
CREATE TEMP TABLE l19_disp(  
producto_id int, periodo daterange NOT NULL,  
PRIMARY KEY(producto_id,periodo WITHOUT OVERLAPS)  
);  
INSERT INTO l19_disp VALUES  
(1,daterange('2026-01-01','2026-04-01','\[)')),(1,daterange('2026-04-01','2026-07-01','\[)'));  
CREATE TEMP TABLE l19_promo(  
id int PRIMARY KEY, producto_id int, periodo daterange,  
FOREIGN KEY(producto_id,PERIOD periodo) REFERENCES
l19_disp(producto_id,PERIOD periodo)  
);  
INSERT INTO l19_promo VALUES
(101,1,daterange('2026-03-01','2026-05-01','\[)'));

### Resultado esperado

| **Comprobación:** La promoción se acepta porque la unión de los periodos padre cubre completamente marzo-mayo. |
|----------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Crea un hueco en disponibilidad e intenta insertar una promoción que lo
atraviese.

### Solución explicada

La clave foránea temporal debe rechazarla con foreign_key_violation.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: claves foráneas temporales con PERIOD. |
|-------------------------------------------------------------------------------|

## Lección 25 · COPY tolerante a errores: REJECT_LIMIT

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

COPY puede ignorar errores de conversión con ON_ERROR ignore. PostgreSQL
18 permite limitar cuántas filas erróneas se toleran con REJECT_LIMIT.

### Ejemplo ejecutable

CREATE TEMP TABLE l25_productos(id int PRIMARY KEY,nombre text,precio
numeric(10,2),stock int);  
-- En psql:  
COPY l25_productos(id,nombre,precio,stock) FROM STDIN  
WITH (FORMAT csv,HEADER true,ON_ERROR ignore,REJECT_LIMIT
1,LOG_VERBOSITY silent);  
id,nombre,precio,stock  
1,Monitor,299.90,10  
2,Teclado,no_es_numero,15  
3,Ratón,25.50,30  
\\  
SELECT \* FROM l25_productos ORDER BY id;

### Resultado esperado

| **Comprobación:** Se importan Monitor y Ratón; la fila del Teclado se descarta por error de conversión. |
|---------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Repite con dos errores y REJECT_LIMIT 2.

### Solución explicada

Mientras no se supere el límite, las filas válidas se cargan. CHECK, FK
o duplicados no son errores de conversión ignorables automáticamente.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: REJECT_LIMIT y LOG_VERBOSITY silent para COPY con errores ignorables. |
|--------------------------------------------------------------------------------------------------------------|

## Lección 26 · Vistas materializadas para informes

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Una vista materializada almacena físicamente el resultado de una
consulta. REFRESH recalcula el contenido; CONCURRENTLY permite refrescar
manteniendo lecturas.

### Ejemplo ejecutable

CREATE TABLE l26_lineas(producto text,cantidad int,precio
numeric(10,2));  
INSERT INTO l26_lineas VALUES
('Monitor',3,290),('Teclado',2,50),('Ratón',3,25);  
CREATE MATERIALIZED VIEW l26_resumen AS  
SELECT producto,SUM(cantidad)
unidades,SUM(cantidad\*precio)::numeric(12,2) ventas  
FROM l26_lineas GROUP BY producto;  
CREATE UNIQUE INDEX l26_resumen_uq ON l26_resumen(producto);  
SELECT \* FROM l26_resumen ORDER BY producto;

### Resultado esperado

| **Comprobación:** Monitor, Ratón y Teclado aparecen con sus unidades/ventas agregadas. |
|----------------------------------------------------------------------------------------|

### Ejercicio práctico

Inserta una venta nueva, comprueba que la vista no cambia y ejecuta
REFRESH MATERIALIZED VIEW CONCURRENTLY.

### Solución explicada

Después del REFRESH el resumen se actualiza. CONCURRENTLY exige un
índice UNIQUE adecuado.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18 relacionada: COPY TO puede usar directamente una vista materializada poblada. |
|---------------------------------------------------------------------------------------------------------------------|

## Lección 27 · Búsquedas Unicode con casefold()

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

casefold() realiza un plegado Unicode más completo que lower(), útil
para equivalencias como Straße y STRASSE.

### Ejemplo ejecutable

SELECT lower('Straße' COLLATE pg_unicode_fast) AS lower_val,  
casefold('Straße' COLLATE pg_unicode_fast) AS folded;  
  
CREATE TEMP TABLE l27_productos(id int PRIMARY KEY,nombre text);  
INSERT INTO l27_productos VALUES (1,'Straße USB-Adapter'),(2,'STRASSE
Netzteil'),(3,'Büro-Monitor');  
SELECT \* FROM l27_productos  
WHERE casefold(nombre COLLATE pg_unicode_fast) LIKE
'%'\|\|casefold('strasse' COLLATE pg_unicode_fast)\|\|'%';

### Resultado esperado

| **Comprobación:** casefold convierte Straße a strasse y la búsqueda encuentra las filas 1 y 2. |
|------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Busca BÜRO sin distinguir mayúsculas/minúsculas.

### Solución explicada

Aplica casefold() tanto a la columna como al parámetro de búsqueda.

### PostgreSQL 18

| **Versión:** Novedad de PostgreSQL 18: casefold() y la intercalación integrada pg_unicode_fast. |
|-------------------------------------------------------------------------------------------------|

## Lección 28 · Búsqueda aproximada con pg_trgm

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

pg_trgm compara trigramas y permite búsquedas parciales o tolerantes a
errores tipográficos. Puede usar índices GIN o GiST.

### Ejemplo ejecutable

CREATE EXTENSION IF NOT EXISTS pg_trgm;  
CREATE TABLE l28_productos(id int PRIMARY KEY,nombre text);  
INSERT INTO l28_productos VALUES (1,'Büro-Monitor'),(2,'Monitor 27
Zoll'),(3,'Monitorkabel HDMI'),(4,'Gaming-Maus');  
CREATE INDEX l28_trgm_idx ON l28_productos USING gin((casefold(nombre
COLLATE pg_unicode_fast)) gin_trgm_ops);  
SELECT id,nombre  
FROM l28_productos  
WHERE word_similarity(casefold('monotor' COLLATE
pg_unicode_fast),casefold(nombre COLLATE pg_unicode_fast))\>=0.40  
ORDER BY id;

### Resultado esperado

| **Comprobación:** Deben aparecer los tres nombres relacionados con monitor; el umbral puede necesitar ajuste con datos reales. |
|--------------------------------------------------------------------------------------------------------------------------------|

### Ejercicio práctico

Compara el plan de LIKE %monitor% con y sin el índice trigramático en
una tabla grande.

### Solución explicada

Usa EXPLAIN (ANALYZE,BUFFERS). En tablas pequeñas un Seq Scan puede
seguir siendo correcto.

### PostgreSQL 18

| **Versión:** pg_trgm no es nuevo; en PostgreSQL 18 se combina bien con casefold() y pg_unicode_fast. |
|------------------------------------------------------------------------------------------------------|

# Apéndice · Ruta de estudio recomendada

Orden sugerido si quieres repetir el curso desde cero:

**Fundamentos SQL:** Lección 2, Lección 3, Lección 4, Lección 5

**Ventanas:** Lección 6, Lección 7, Lección 24

**Rendimiento:** Lección 8, Lección 21

**Seguridad:** Lección 9, Lección 22

**PL/pgSQL:** Lección 10, Lección 11, Lección 12

**Administración:** Lección 1, Lección 13, Lección 14, Lección 15,
Lección 23

**Funciones PostgreSQL 18:** Lección 16, Lección 17, Lección 18, Lección
19, Lección 25, Lección 26, Lección 27, Lección 28

**Jerarquías:** Lección 29

## Buenas prácticas generales

- Prueba primero en una base de desarrollo; EXPLAIN ANALYZE ejecuta
  realmente la sentencia.

- Usa transacciones para cambios que afecten varias tablas.

- No desactives autovacuum globalmente salvo que sepas exactamente por
  qué.

- Concede permisos a roles de grupo y aplica mínimo privilegio.

- No crees índices “por si acaso”: mide con EXPLAIN (ANALYZE, BUFFERS).

- Parametriza entradas de usuario (\$1, \$2, ...) y evita concatenar
  SQL.

- Cuando una característica sea específica de PostgreSQL 18, comprueba
  SHOW server_version antes de probarla.

# Concurrencia, bloqueos y eventos

Bloque avanzado sobre colas de trabajo, bloqueos, notificaciones, outbox
y aislamiento transaccional.

## Lección 30 · Colas de trabajo con FOR UPDATE SKIP LOCKED

↑ Volver al índice

### Idea principal

Cuando varios workers procesan pedidos en paralelo, FOR UPDATE bloquea
la fila elegida y SKIP LOCKED permite que otros workers salten las filas
ya reclamadas. Es un patrón muy útil para colas de trabajo basadas en
tablas.

### Ejemplo ejecutable

DROP TABLE IF EXISTS l30_pedidos;  
CREATE TABLE l30_pedidos (  
pedido_id integer PRIMARY KEY,  
cliente text NOT NULL,  
estado text NOT NULL DEFAULT 'pendiente',  
trabajador text  
);  
INSERT INTO l30_pedidos (pedido_id, cliente) VALUES  
(101,'Ana'),(102,'Luis'),(103,'Marta'),(104,'Elena');  
  
WITH siguiente AS (  
SELECT pedido_id  
FROM l30_pedidos  
WHERE estado='pendiente'  
ORDER BY pedido_id  
FOR UPDATE SKIP LOCKED  
LIMIT 1  
)  
UPDATE l30_pedidos p  
SET estado='procesando', trabajador='worker-a'  
FROM siguiente s  
WHERE p.pedido_id=s.pedido_id  
RETURNING p.pedido_id, p.cliente, p.estado, p.trabajador;

### Resultado esperado

pedido_id \| cliente \| estado \| trabajador  
-----------+---------+-------------+------------  
101 \| Ana \| procesando \| worker-a

### Ejercicio práctico

Reclama el siguiente pedido pendiente para worker-b sin conocer antes su
pedido_id.

### Solución explicada

WITH siguiente AS (  
SELECT pedido_id FROM l30_pedidos  
WHERE estado='pendiente'  
ORDER BY pedido_id  
FOR UPDATE SKIP LOCKED  
LIMIT 1  
)  
UPDATE l30_pedidos p  
SET estado='procesando', trabajador='worker-b'  
FROM siguiente s  
WHERE p.pedido_id=s.pedido_id  
RETURNING p.pedido_id, p.cliente;

Buena práctica: confirma rápido la transacción que reclama el trabajo;
no mantengas el bloqueo mientras haces llamadas HTTP lentas.

### PostgreSQL 18

SKIP LOCKED existe desde versiones anteriores. PostgreSQL 18 añade la
posibilidad de referirse explícitamente a OLD y NEW en RETURNING, útil
para devolver el cambio de estado en una sola sentencia.

## Lección 31 · Diagnóstico de bloqueos con pg_stat_activity y pg_locks

↑ Volver al índice

### Idea principal

Cuando una sesión espera un bloqueo, pg_stat_activity muestra el estado
y pg_blocking_pids() identifica directamente qué PID la bloquea.
pg_locks permite inspeccionar el tipo de bloqueo, si fue concedido y
desde cuándo espera.

### Ejemplo ejecutable

-- Sesión A  
BEGIN;  
UPDATE l31_stock SET stock=stock-1 WHERE producto_id=1;  
  
-- Sesión B  
BEGIN;  
SET LOCAL lock_timeout='30s';  
UPDATE l31_stock SET stock=stock-2 WHERE producto_id=1;  
  
-- Sesión de diagnóstico  
SELECT bloqueada.application_name AS bloqueada,  
bloqueadora.application_name AS bloqueadora,  
bloqueada.wait_event_type,  
bloqueada.wait_event  
FROM pg_stat_activity bloqueada  
CROSS JOIN LATERAL unnest(pg_blocking_pids(bloqueada.pid)) b(pid)  
JOIN pg_stat_activity bloqueadora ON bloqueadora.pid=b.pid;

### Resultado esperado

bloqueada \| bloqueadora \| wait_event_type \| wait_event  
---------------+--------------+-----------------+---------------  
l31_worker_b \| l31_worker_a \| Lock \| transactionid

### Ejercicio práctico

¿Qué regla simple reduce mucho el riesgo de deadlocks cuando debes
bloquear varias filas?

### Solución explicada

Bloquea siempre las filas en un orden estable, por ejemplo:  
SELECT producto_id, stock  
FROM l31_stock  
WHERE producto_id IN (1,2)  
ORDER BY producto_id  
FOR UPDATE;

Buena práctica: si ocurre un deadlock, PostgreSQL cancela una
transacción; la aplicación debe hacer ROLLBACK y reintentar la
transacción completa.

### PostgreSQL 18

pg_stat_activity, pg_locks y pg_blocking_pids() ya existían. PostgreSQL
18 incorpora log_lock_failures para registrar información adicional
cuando fallan ciertas adquisiciones de bloqueo, como NOWAIT.

## Lección 32 · Avisos en tiempo real con LISTEN, NOTIFY y triggers

↑ Volver al índice

### Idea principal

LISTEN mantiene una conexión escuchando un canal; NOTIFY o pg_notify()
envían avisos al confirmar la transacción. Un trigger AFTER INSERT puede
despertar a un proceso NestJS cuando se crea un pedido.

### Ejemplo ejecutable

CREATE OR REPLACE FUNCTION l32_notificar_pedido()  
RETURNS trigger LANGUAGE plpgsql AS \$\$  
BEGIN  
PERFORM pg_notify(  
'pedidos_nuevos',  
json_build_object('pedido_id',NEW.pedido_id,'estado',NEW.estado)::text  
);  
RETURN NEW;  
END; \$\$;  
  
CREATE TRIGGER l32_pedido_insertado  
AFTER INSERT ON l32_pedidos  
FOR EACH ROW EXECUTE FUNCTION l32_notificar_pedido();  
  
-- En otra conexión  
LISTEN pedidos_nuevos;

### Resultado esperado

Al hacer COMMIT de un nuevo pedido, el listener recibe un aviso
asíncrono con un payload JSON. Si la transacción termina con ROLLBACK,
el aviso no se entrega.

### Ejercicio práctico

Crea un segundo canal pedidos_estado que avise solo cuando OLD.estado
sea distinto de NEW.estado.

### Solución explicada

CREATE OR REPLACE FUNCTION l32_notificar_estado()  
RETURNS trigger LANGUAGE plpgsql AS \$\$  
BEGIN  
PERFORM pg_notify('pedidos_estado',  
json_build_object('pedido_id',NEW.pedido_id,  
'anterior',OLD.estado,  
'nuevo',NEW.estado)::text);  
RETURN NEW;  
END; \$\$;  
  
CREATE TRIGGER l32_estado_modificado  
AFTER UPDATE OF estado ON l32_pedidos  
FOR EACH ROW  
WHEN (OLD.estado IS DISTINCT FROM NEW.estado)  
EXECUTE FUNCTION l32_notificar_estado();

Buena práctica: para eventos que no se pueden perder, guarda el evento
en una tabla outbox y usa NOTIFY solo para despertar al worker.

### PostgreSQL 18

LISTEN/NOTIFY no son nuevos en PostgreSQL 18. Su comportamiento
transaccional sigue siendo clave: las notificaciones se entregan tras
COMMIT. No son una cola duradera.

## Lección 33 · Patrón transactional outbox

↑ Volver al índice

### Idea principal

El patrón outbox guarda el pedido y un evento persistente en la misma
transacción. Así, si la aplicación se cae, el evento sigue en PostgreSQL
y puede reintentarse. Los workers pueden reclamar eventos con SKIP
LOCKED.

### Ejemplo ejecutable

CREATE TABLE l33_outbox (  
evento_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,  
tipo text NOT NULL,  
agregado_id integer NOT NULL,  
payload jsonb NOT NULL,  
estado text NOT NULL DEFAULT 'pendiente',  
trabajador text,  
creado_en timestamptz NOT NULL DEFAULT current_timestamp  
);  
  
CREATE OR REPLACE FUNCTION l33_crear_evento_pedido()  
RETURNS trigger LANGUAGE plpgsql AS \$\$  
BEGIN  
INSERT INTO l33_outbox(tipo,agregado_id,payload)  
VALUES ('pedido.creado', NEW.pedido_id,  
jsonb_build_object('pedido_id',NEW.pedido_id,'cliente',NEW.cliente));  
RETURN NEW;  
END; \$\$;

### Resultado esperado

Al insertar un pedido y hacer COMMIT existe también una fila pendiente
en l33_outbox. Si se hace ROLLBACK, no queda ni el pedido ni el evento.

### Ejercicio práctico

Reclama en un solo lote hasta dos eventos pendientes para worker-b.

### Solución explicada

WITH lote AS (  
SELECT evento_id FROM l33_outbox  
WHERE estado='pendiente'  
ORDER BY evento_id  
FOR UPDATE SKIP LOCKED  
LIMIT 2  
)  
UPDATE l33_outbox o  
SET estado='procesando', trabajador='worker-b'  
FROM lote l  
WHERE o.evento_id=l.evento_id  
RETURNING o.evento_id,o.agregado_id,o.estado,o.trabajador;

Buena práctica: el consumidor debe ser idempotente, porque un evento
puede publicarse de nuevo si el proceso falla antes de marcarlo como
procesado.

### PostgreSQL 18

El patrón outbox usa funciones antiguas de PostgreSQL; PostgreSQL 18
aporta RETURNING con referencias explícitas OLD/NEW, que simplifica
auditorías de cambios al reclamar eventos.

## Lección 34 · Aislamiento SERIALIZABLE y reintentos

↑ Volver al índice

### Idea principal

SERIALIZABLE protege reglas que dependen de varias filas y que podrían
romperse aunque las transacciones actualicen filas distintas. PostgreSQL
detecta dependencias peligrosas y aborta una transacción con SQLSTATE
40001.

### Ejemplo ejecutable

BEGIN ISOLATION LEVEL SERIALIZABLE;  
  
WITH inventario AS (  
SELECT SUM(stock) AS stock_total  
FROM l34_stock_almacen  
)  
UPDATE l34_stock_almacen s  
SET stock=0  
FROM inventario i  
WHERE s.almacen_id=1  
AND s.stock\>0  
AND i.stock_total\>1  
RETURNING s.almacen_id,s.almacen,s.stock;  
  
COMMIT;

### Resultado esperado

Si dos transacciones SERIALIZABLE intentan retirar simultáneamente la
última unidad de almacenes distintos, una puede confirmar y la otra
falla con:  
ERROR: could not serialize access due to read/write dependencies among
transactions  
SQLSTATE: 40001

### Ejercicio práctico

¿Qué parte debe reintentarse cuando recibes el error 40001?

### Solución explicada

Debe reintentarse la transacción completa desde BEGIN, incluida la
lógica que decidió qué consultas ejecutar. No basta con repetir solo el
último UPDATE.

Buena práctica: usa backoff corto y aleatorio en los reintentos para
evitar que las mismas transacciones vuelvan a chocar inmediatamente.

### PostgreSQL 18

SERIALIZABLE y Serializable Snapshot Isolation existen desde versiones
anteriores. PostgreSQL 18 mantiene el mismo principio: las transacciones
confirmadas deben equivaler a alguna ejecución serial y los fallos 40001
requieren reintento.

# Seguridad avanzada y APIs de base de datos

Patrones para exponer operaciones controladas sin conceder acceso
directo a las tablas.

## Lección 35 · API segura con SECURITY DEFINER

↑ Volver al índice

### Idea principal

SECURITY DEFINER permite que una función se ejecute con los permisos de
su propietario. Así, un rol de aplicación puede ejecutar una operación
de negocio concreta sin recibir UPDATE directo sobre toda la tabla.

### Ejemplo ejecutable

CREATE OR REPLACE FUNCTION l35_tienda.reservar_producto(  
p_producto_id integer,  
p_cantidad integer  
)  
RETURNS TABLE(producto_id integer, stock_anterior integer, stock_nuevo
integer)  
LANGUAGE plpgsql  
SECURITY DEFINER  
SET search_path = pg_catalog, pg_temp  
AS \$\$  
DECLARE v_old integer; v_new integer;  
BEGIN  
IF p_cantidad \<= 0 THEN  
RAISE EXCEPTION 'Cantidad inválida';  
END IF;  
  
UPDATE l35_tienda.productos  
SET stock=stock-p_cantidad  
WHERE productos.producto_id=p_producto_id  
AND stock\>=p_cantidad  
RETURNING WITH (OLD AS antes, NEW AS despues)  
antes.stock, despues.stock INTO v_old, v_new;  
  
IF NOT FOUND THEN RAISE EXCEPTION 'Sin stock'; END IF;  
RETURN QUERY SELECT p_producto_id,v_old,v_new;  
END; \$\$;  
  
REVOKE ALL ON FUNCTION l35_tienda.reservar_producto(integer,integer)
FROM PUBLIC;  
GRANT EXECUTE ON FUNCTION l35_tienda.reservar_producto(integer,integer)
TO l35_api;

### Resultado esperado

El rol l35_api puede ejecutar reservar_producto(), pero un UPDATE
directo sobre l35_tienda.productos devuelve permission denied.

### Ejercicio práctico

Reserva cuatro teclados usando solo el rol de API y comprueba el stock
final.

### Solución explicada

SET ROLE l35_api;  
SELECT \* FROM l35_tienda.reservar_producto(2,4);  
RESET ROLE;  
SELECT producto_id,nombre,stock FROM l35_tienda.productos ORDER BY
producto_id;

Buena práctica: fija un search_path seguro y usa nombres de objetos
totalmente cualificados dentro de funciones SECURITY DEFINER.

### PostgreSQL 18

SECURITY DEFINER no es nuevo. PostgreSQL 18 aporta RETURNING WITH (OLD
AS ..., NEW AS ...), útil para devolver el antes y después sin consultas
adicionales.

# Observabilidad y rendimiento avanzado

Herramientas para medir memoria, buffers y consultas costosas antes de
optimizar.

## Lección 36 · Memoria de planificación y ejecución con EXPLAIN

↑ Volver al índice

### Idea principal

EXPLAIN (MEMORY) muestra memoria del planificador. EXPLAIN ANALYZE
muestra la ejecución real; Sort, WindowAgg, Materialize y CTE pueden
indicar uso de memoria o disco. work_mem se aplica por operación, no
como límite total de una consulta.

### Ejemplo ejecutable

EXPLAIN (  
ANALYZE,  
MEMORY,  
BUFFERS,  
TIMING OFF,  
COSTS OFF  
)  
WITH ventas AS MATERIALIZED (  
SELECT p.producto_id,p.nombre,  
SUM(l.cantidad\*l.precio_unitario)::numeric(12,2) AS ventas  
FROM l36_productos p  
JOIN l36_lineas_pedido l ON l.producto_id=p.producto_id  
GROUP BY p.producto_id,p.nombre  
)  
SELECT nombre,ventas,  
SUM(ventas) OVER (  
ORDER BY ventas DESC  
ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING  
) AS ventas_desde_aqui  
FROM ventas  
ORDER BY ventas DESC;

### Resultado esperado

Busca: Planning Memory, Buffers, Sort Method y, cuando corresponda,
Storage: Memory/Disk. Las cifras exactas dependen del servidor y de los
datos.

### Ejercicio práctico

¿Por qué SHOW work_mem = 4MB no significa que una consulta completa
pueda consumir como máximo 4MB?

### Solución explicada

Porque work_mem es un límite base por operación de sort/hash. Una
consulta puede tener varias operaciones y varias conexiones pueden
ejecutarlas a la vez. Para probar cambios de forma segura usa SET LOCAL
work_mem dentro de una transacción.

Buena práctica: no subas work_mem globalmente sin estimar concurrencia y
comprobar qué nodo concreto derrama a disco.

### PostgreSQL 18

EXPLAIN (MEMORY) apareció antes de PostgreSQL 18. PostgreSQL 18 mejora
la observabilidad de nodos como WindowAgg/materialización/CTE y hace que
BUFFERS se incluya automáticamente con EXPLAIN ANALYZE.

## Lección 37 · Encontrar consultas costosas con pg_stat_statements

↑ Volver al índice

### Idea principal

pg_stat_statements agrega estadísticas de consultas normalizadas: número
de llamadas, tiempo acumulado, tiempo medio, filas, buffers, temporales
y WAL. Sirve para elegir qué consultas merecen un EXPLAIN ANALYZE
detallado.

### Ejemplo ejecutable

SHOW shared_preload_libraries;  
SHOW compute_query_id;  
CREATE EXTENSION IF NOT EXISTS pg_stat_statements;  
  
SELECT  
calls,  
rows,  
ROUND(total_exec_time::numeric,2) AS total_ms,  
ROUND(mean_exec_time::numeric,2) AS media_ms,  
shared_blks_read,  
temp_blks_written,  
LEFT(query,120) AS consulta  
FROM pg_stat_statements  
WHERE dbid=(SELECT oid FROM pg_database WHERE
datname=current_database())  
ORDER BY total_exec_time DESC  
LIMIT 10;

### Resultado esperado

Las consultas que solo cambian literales pueden agruparse bajo una forma
normalizada, por ejemplo:  
SELECT nombre, precio FROM productos WHERE precio \> \$1  
La salida exacta de tiempos, queryid y buffers depende de la carga real.

### Ejercicio práctico

Ejecuta tres COUNT(\*) con distintos límites de stock y comprueba que se
agrupan en una entrada con calls = 3.

### Solución explicada

SELECT COUNT(\*) FROM l37_productos WHERE stock \> 0;  
SELECT COUNT(\*) FROM l37_productos WHERE stock \> 5;  
SELECT COUNT(\*) FROM l37_productos WHERE stock \> 9;  
  
SELECT calls,rows,query  
FROM pg_stat_statements  
WHERE query LIKE 'SELECT COUNT(\*)%l37_productos%stock \>%'  
ORDER BY calls DESC;

Buena práctica: prioriza por impacto total, no solo por tiempo medio;
una consulta rápida ejecutada millones de veces puede ser el verdadero
cuello de botella.

### PostgreSQL 18

pg_stat_statements ya existía. PostgreSQL 18 añade métricas como
parallel_workers_to_launch, parallel_workers_launched y
wal_buffers_full, y mejora el seguimiento de varias clases de
sentencias.

# Mantenimiento de esta guía

Archivo maestro: postgresql-18-lecciones.pdf. La guía debe actualizarse
añadiendo nuevas lecciones en su bloque temático, conservando ejemplos
SQL ejecutables, resultados esperados y ejercicios con solución. La
numeración conserva el historial original; si falta una lección en el
chat, no se inventa.