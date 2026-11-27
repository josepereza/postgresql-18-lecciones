**PostgreSQL 18**

Guía práctica completa - lecciones compiladas y actualizadas

*Tienda de electrónica · SQL · Administración · PL/pgSQL · Rendimiento*

Edición: noviembre de 2026

| **Contenido:** Compilación de las lecciones disponibles en esta conversación. La numeración original se conserva; no aparece una lección 20 en el hilo disponible. |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|

| **Uso recomendado:** Ejecuta los ejemplos en una base de pruebas PostgreSQL 18. Los objetos lN\_\* están pensados para evitar colisiones entre lecciones. |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------|

# Índice temático

Actualización incluida: lecciones 30-45 sobre concurrencia, bloqueos,
eventos, serialización, seguridad avanzada, observabilidad, mantenimiento y SQL avanzado. La
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
>
> [<u>Lección 41: Sincronizar inventario con MERGE ... RETURNING</u>](#lección-41-sincronizar-inventario-con-merge--returning)

**Funciones de ventana**

> [<u>Lección 6: ROW_NUMBER(), RANK() y PARTITION
> BY</u>](#lección-6-row_number-rank-y-partition-by)
>
> [<u>Lección 7: Marcos ROWS y
> acumulados</u>](#lección-7-marcos-rows-y-acumulados)
>
> [<u>Lección 24: Marcos GROUPS y
> EXCLUDE</u>](#lección-24-marcos-groups-y-exclude)
>
> [<u>Lección 45: Ventanas móviles por tiempo con RANGE</u>](#lección-45-ventanas-móviles-por-tiempo-con-range)

**Índices, EXPLAIN y rendimiento**

> [<u>Lección 8: Índices B-tree y lectura básica de
> EXPLAIN</u>](#lección-8-índices-b-tree-y-lectura-básica-de-explain)
>
> [<u>Lección 21: EXPLAIN ANALYZE: estimado vs
> real</u>](#lección-21-explain-analyze-estimado-vs-real)
>
> [<u>Lección 44: Índices parciales y consultas cubiertas</u>](#lección-44-índices-parciales-y-consultas-cubiertas)

**Roles, permisos y seguridad**

> [<u>Lección 9: Roles, permisos y mínimo
> privilegio</u>](#lección-9-roles-permisos-y-mínimo-privilegio)
>
> [<u>Lección 22: Row-Level Security (RLS) en un
> SaaS</u>](#lección-22-row-level-security-rls-en-un-saas)
>
> [<u>Lección 42: Permisos futuros con ALTER DEFAULT PRIVILEGES</u>](#lección-42-permisos-futuros-con-alter-default-privileges)

**PL/pgSQL: funciones, procedimientos y triggers**

> [<u>Lección 10: Funciones PL/pgSQL</u>](#lección-10-funciones-plpgsql)
>
> [<u>Lección 11: Procedimientos almacenados con
> CALL</u>](#lección-11-procedimientos-almacenados-con-call)
>
> [<u>Lección 12: Triggers para controlar el
> stock</u>](#lección-12-triggers-para-controlar-el-stock)
>
> [<u>Lección 43: Triggers por sentencia con tablas de
> transición</u>](#lección-43-triggers-por-sentencia-con-tablas-de-transición)

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

**Concurrencia, bloqueos y eventos**

> [<u>Lección 30: Colas de trabajo con FOR UPDATE SKIP LOCKED</u>](#lección-30-colas-de-trabajo-con-for-update-skip-locked)
>
> [<u>Lección 31: Diagnóstico de bloqueos con pg_stat_activity y pg_locks</u>](#lección-31-diagnóstico-de-bloqueos-con-pg_stat_activity-y-pg_locks)
>
> [<u>Lección 32: Avisos en tiempo real con LISTEN, NOTIFY y triggers</u>](#lección-32-avisos-en-tiempo-real-con-listen-notify-y-triggers)
>
> [<u>Lección 33: Patrón transactional outbox</u>](#lección-33-patrón-transactional-outbox)
>
> [<u>Lección 34: Aislamiento SERIALIZABLE y reintentos</u>](#lección-34-aislamiento-serializable-y-reintentos)

**Seguridad avanzada y APIs de base de datos**

> [<u>Lección 35: API segura con SECURITY DEFINER</u>](#lección-35-api-segura-con-security-definer)

**Observabilidad y rendimiento avanzado**

> [<u>Lección 36: Memoria de planificación y ejecución con EXPLAIN</u>](#lección-36-memoria-de-planificación-y-ejecución-con-explain)
>
> [<u>Lección 37: Encontrar consultas costosas con pg_stat_statements</u>](#lección-37-encontrar-consultas-costosas-con-pg_stat_statements)
>
> [<u>Lección 38: Medir ANALYZE y detectar estadísticas desactualizadas</u>](#lección-38-medir-analyze-y-detectar-estadísticas-desactualizadas)
>
> [<u>Lección 39: E/S por sesión con pg_stat_get_backend_io()</u>](#lección-39-es-por-sesión-con-pg_stat_get_backend_io)
>
> [<u>Lección 40: WAL generado por sesión con pg_stat_get_backend_wal()</u>](#lección-40-wal-generado-por-sesión-con-pg_stat_get_backend_wal)

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

## Lección 41 · Sincronizar inventario con MERGE ... RETURNING

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

`MERGE` compara una fuente con una tabla destino y decide, fila por fila, si
debe insertar, actualizar, eliminar o no hacer nada. PostgreSQL 18 permite
añadir `RETURNING`, usar `merge_action()` y consultar explícitamente los valores
`OLD` y `NEW`. Así podemos sincronizar inventario y saber en la misma sentencia
qué ocurrió.

### Datos mínimos

```sql
DROP TABLE IF EXISTS l41_importacion;
DROP TABLE IF EXISTS l41_productos;

CREATE TABLE l41_productos (
    sku     text PRIMARY KEY,
    nombre  text NOT NULL,
    precio  numeric(10,2) NOT NULL,
    stock   integer NOT NULL CHECK (stock >= 0)
);

CREATE TABLE l41_importacion (
    sku     text PRIMARY KEY,
    nombre  text NOT NULL,
    precio  numeric(10,2) NOT NULL,
    stock   integer NOT NULL CHECK (stock >= 0)
);

INSERT INTO l41_productos VALUES
    ('T-100', 'Teclado', 79.00, 5),
    ('R-200', 'Ratón',   39.00, 10);

INSERT INTO l41_importacion VALUES
    ('T-100', 'Teclado mecánico', 89.00, 8),
    ('M-300', 'Monitor 27',       249.00, 4);
```

### Ejemplo ejecutable

```sql
MERGE INTO l41_productos AS p
USING l41_importacion AS i
ON p.sku = i.sku
WHEN MATCHED THEN
    UPDATE SET nombre = i.nombre,
               precio = i.precio,
               stock = i.stock
WHEN NOT MATCHED THEN
    INSERT (sku, nombre, precio, stock)
    VALUES (i.sku, i.nombre, i.precio, i.stock)
RETURNING merge_action() AS accion,
          new.sku,
          old.precio AS precio_anterior,
          new.precio AS precio_nuevo,
          old.stock AS stock_anterior,
          new.stock AS stock_nuevo;
```

### Resultado esperado

El orden de las filas no está garantizado, pero el contenido será:

| accion | sku | precio_anterior | precio_nuevo | stock_anterior | stock_nuevo |
|---|---|---:|---:|---:|---:|
| UPDATE | T-100 | 79.00 | 89.00 | 5 | 8 |
| INSERT | M-300 | NULL | 249.00 | NULL | 4 |

Para una inserción no existe una fila anterior, por eso los campos `OLD` son
`NULL`.

### Ejercicio práctico

Recibe una segunda importación: el ratón desaparece del catálogo porque llega
con stock cero, mientras que se incorpora un portátil nuevo. Resuélvelo con un
solo `MERGE` y muestra la acción efectuada.

### Solución explicada paso a paso

1. Sustituye los datos de importación.

```sql
TRUNCATE l41_importacion;

INSERT INTO l41_importacion VALUES
    ('R-200', 'Ratón',    39.00, 0),
    ('P-400', 'Portátil', 899.00, 2);
```

2. Coloca primero la condición específica que elimina stock cero. Las cláusulas
`WHEN` se evalúan en el orden escrito y se ejecuta como máximo una acción por
fila candidata.

```sql
MERGE INTO l41_productos AS p
USING l41_importacion AS i
ON p.sku = i.sku
WHEN MATCHED AND i.stock = 0 THEN
    DELETE
WHEN MATCHED THEN
    UPDATE SET nombre = i.nombre,
               precio = i.precio,
               stock = i.stock
WHEN NOT MATCHED AND i.stock > 0 THEN
    INSERT (sku, nombre, precio, stock)
    VALUES (i.sku, i.nombre, i.precio, i.stock)
RETURNING merge_action() AS accion,
          COALESCE(old.sku, new.sku) AS sku,
          old.stock AS stock_anterior,
          new.stock AS stock_nuevo;
```

Resultado esperado, en cualquier orden:

| accion | sku | stock_anterior | stock_nuevo |
|---|---|---:|---:|
| DELETE | R-200 | 10 | NULL |
| INSERT | P-400 | NULL | 2 |

3. Comprueba el inventario final.

```sql
SELECT sku, nombre, precio, stock
FROM l41_productos
ORDER BY sku;
```

Resultado esperado:

| sku | nombre | precio | stock |
|---|---|---:|---:|
| M-300 | Monitor 27 | 249.00 | 4 |
| P-400 | Portátil | 899.00 | 2 |
| T-100 | Teclado mecánico | 89.00 | 8 |

### Buena práctica

Asegura que cada fila de la fuente coincida como máximo con una fila destino;
una clave primaria en `sku` evita ambigüedades. No uses `MERGE` para ocultar
reglas de negocio difíciles de revisar: mantén las condiciones específicas
antes que las generales y prueba siempre los casos de inserción, actualización
y eliminación.

### PostgreSQL 18: novedad frente a concepto existente

- `MERGE` ya existía en versiones anteriores de PostgreSQL.
- PostgreSQL 18 añade `MERGE ... RETURNING` y `merge_action()`, que devuelve
  `INSERT`, `UPDATE` o `DELETE` para cada fila procesada.
- PostgreSQL 18 permite usar `OLD` y `NEW` explícitamente en `RETURNING` para
  comparar el valor anterior con el nuevo.

Documentación oficial: [MERGE](https://www.postgresql.org/docs/18/sql-merge.html),
[funciones auxiliares de MERGE](https://www.postgresql.org/docs/18/functions-merge-support.html)
y [RETURNING](https://www.postgresql.org/docs/18/dml-returning.html).

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

## Lección 45 · Ventanas móviles por tiempo con RANGE

[<u>↑ Volver al índice</u>](#índice-temático)

### Objetivo

Calcular las ventas de los últimos siete días naturales aunque existan días
sin pedidos. La diferencia esencial es:

- `ROWS` cuenta filas físicas anteriores.
- `RANGE` compara el valor de ordenación, en este caso una fecha.

### Datos mínimos

La tabla es independiente de las lecciones anteriores. Hay huecos entre las
fechas precisamente para que la diferencia resulte visible.

```sql
DROP TABLE IF EXISTS l45_pedidos;

CREATE TABLE l45_pedidos (
    pedido_id integer PRIMARY KEY,
    fecha timestamp NOT NULL,
    total numeric(10,2) NOT NULL CHECK (total >= 0)
);

INSERT INTO l45_pedidos (pedido_id, fecha, total) VALUES
    (1, '2026-11-01 10:00', 100.00),
    (2, '2026-11-02 11:00',  50.00),
    (3, '2026-11-05 12:00', 200.00),
    (4, '2026-11-10 09:00',  80.00),
    (5, '2026-11-11 14:00', 120.00);
```

### Ventana de siete días naturales

Primero agregamos por día; después aplicamos la función de ventana. Para
incluir el día actual y los seis anteriores usamos `INTERVAL '6 days'`.

```sql
WITH ventas_diarias AS (
    SELECT date_trunc('day', fecha) AS dia,
           sum(total) AS total_dia
    FROM l45_pedidos
    GROUP BY date_trunc('day', fecha)
)
SELECT dia::date,
       total_dia,
       sum(total_dia) OVER (
           ORDER BY dia
           RANGE BETWEEN INTERVAL '6 days' PRECEDING
                     AND CURRENT ROW
       ) AS total_7_dias
FROM ventas_diarias
ORDER BY dia;
```

Resultado esperado:

| dia | total_dia | total_7_dias |
|---|---:|---:|
| 2026-11-01 | 100.00 | 100.00 |
| 2026-11-02 | 50.00 | 150.00 |
| 2026-11-05 | 200.00 | 350.00 |
| 2026-11-10 | 80.00 | 280.00 |
| 2026-11-11 | 120.00 | 400.00 |

Para el 10 de noviembre, el marco empieza el día 4: entran las ventas del 5 y
del 10, pero ya no las del 1 ni las del 2. `RANGE` utiliza la distancia
temporal, no el número de filas disponibles.

### Ejercicio práctico

Calcula, para cada fecha:

1. las ventas de los últimos **tres días naturales**;
2. las ventas de las últimas **tres filas con ventas**.

Compara especialmente el resultado del 10 de noviembre.

### Solución paso a paso

1. Tres días naturales significan el día actual más dos días anteriores:
   `RANGE ... INTERVAL '2 days' PRECEDING`.
2. Tres filas significan la fila actual y las dos anteriores:
   `ROWS ... 2 PRECEDING`.
3. Ambas ventanas pueden calcularse en la misma consulta.

```sql
WITH ventas_diarias AS (
    SELECT date_trunc('day', fecha) AS dia,
           sum(total) AS total_dia
    FROM l45_pedidos
    GROUP BY date_trunc('day', fecha)
)
SELECT dia::date,
       total_dia,
       sum(total_dia) OVER (
           ORDER BY dia
           RANGE BETWEEN INTERVAL '2 days' PRECEDING
                     AND CURRENT ROW
       ) AS ultimos_3_dias,
       sum(total_dia) OVER (
           ORDER BY dia
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS ultimas_3_filas
FROM ventas_diarias
ORDER BY dia;
```

Resultado esperado:

| dia | total_dia | ultimos_3_dias | ultimas_3_filas |
|---|---:|---:|---:|
| 2026-11-01 | 100.00 | 100.00 | 100.00 |
| 2026-11-02 | 50.00 | 150.00 | 150.00 |
| 2026-11-05 | 200.00 | 200.00 | 350.00 |
| 2026-11-10 | 80.00 | 80.00 | 330.00 |
| 2026-11-11 | 120.00 | 200.00 | 400.00 |

El 10 de noviembre no hubo ventas el 8 ni el 9, por lo que el total natural de
tres días es solo `80`. En cambio, `ROWS` retrocede hasta las filas del 5 y del
2 de noviembre y obtiene `50 + 200 + 80 = 330`.

### Matices y buenas prácticas

- Agrega primero por día si puede haber varios pedidos en una misma fecha. Así
  evitas tratar cada pedido como si fuera un día distinto.
- Con un desplazamiento, `RANGE` exige exactamente una expresión en el
  `ORDER BY` de la ventana.
- Para columnas `date` o `timestamp`, el desplazamiento de `RANGE` se expresa
  normalmente como `interval`.
- Decide si “últimos siete días” incluye el día actual: en ese caso el límite
  inferior es seis días antes, no siete.
- Para informes grandes, un índice sobre `fecha` puede ayudar a filtrar el
  periodo inicial, aunque la agregación y la ventana todavía requieren trabajo.

### PostgreSQL 18: novedad frente a concepto existente

- Las funciones de ventana no son nuevas en PostgreSQL 18.
- Los desplazamientos `RANGE ... PRECEDING/FOLLOWING`, `GROUPS` y las opciones
  `EXCLUDE` se incorporaron en PostgreSQL 11 como parte del soporte de marcos
  definido por SQL:2011.
- PostgreSQL 18 conserva esta sintaxis; para ordenar por fechas o marcas de
  tiempo, la documentación admite un `interval` como desplazamiento.

Documentación oficial: [expresiones y marcos de ventana](https://www.postgresql.org/docs/18/sql-expressions.html),
[funciones de ventana](https://www.postgresql.org/docs/18/functions-window.html)
y [novedades de PostgreSQL 11](https://www.postgresql.org/docs/11/release-11.html).

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

## Lección 44 · Índices parciales y consultas cubiertas

[<u>↑ Volver al índice</u>](#índice-temático)

### Objetivo

Acelerar la consulta frecuente de pedidos pendientes sin mantener un índice
para los miles de pedidos ya entregados. Combinaremos:

- un **índice parcial**, que guarda únicamente las filas interesantes;
- `INCLUDE`, que añade columnas de salida sin convertirlas en claves de
  búsqueda;
- `EXPLAIN (ANALYZE, BUFFERS)`, para comprobar el plan real.

### Datos mínimos reproducibles

```sql
DROP TABLE IF EXISTS l44_pedidos;

CREATE TABLE l44_pedidos (
    pedido_id integer PRIMARY KEY,
    creado_en timestamp NOT NULL,
    estado text NOT NULL
        CHECK (estado IN ('pendiente', 'pagado', 'entregado')),
    total numeric(10,2) NOT NULL
);

INSERT INTO l44_pedidos (pedido_id, creado_en, estado, total)
SELECT g,
       timestamp '2026-01-01 00:00' + g * interval '1 minute',
       CASE
           WHEN g > 9990 THEN 'pendiente'
           WHEN g > 9900 THEN 'pagado'
           ELSE 'entregado'
       END,
       (g / 100.0)::numeric(10,2)
FROM generate_series(1, 10000) AS g;

ANALYZE l44_pedidos;
```

La tabla contiene 10 pedidos pendientes, 90 pagados y 9900 entregados.

### Crear el índice parcial

```sql
CREATE INDEX l44_pedidos_pendientes_fecha_idx
ON l44_pedidos (creado_en DESC)
INCLUDE (pedido_id, total)
WHERE estado = 'pendiente';

VACUUM (ANALYZE) l44_pedidos;
```

El índice solo contiene las 10 filas pendientes. `creado_en DESC` ayuda con el
orden y `INCLUDE` guarda `pedido_id` y `total` para que PostgreSQL pueda
resolver la consulta usando únicamente el índice cuando el mapa de visibilidad
lo permita.

### Comprobar el plan

```sql
EXPLAIN (ANALYZE, BUFFERS, COSTS OFF, SUMMARY OFF)
SELECT pedido_id, creado_en, total
FROM l44_pedidos
WHERE estado = 'pendiente'
ORDER BY creado_en DESC
LIMIT 3;
```

Fragmento esperado del plan; los tiempos y buffers exactos pueden variar:

```text
Limit
  ->  Index Only Scan using l44_pedidos_pendientes_fecha_idx
        on l44_pedidos
        Heap Fetches: 0
```

Comprueba también el resultado:

```sql
SELECT pedido_id, creado_en, total
FROM l44_pedidos
WHERE estado = 'pendiente'
ORDER BY creado_en DESC
LIMIT 3;
```

| pedido_id | creado_en | total |
|---:|---|---:|
| 10000 | 2026-01-07 22:40:00 | 100.00 |
| 9999 | 2026-01-07 22:39:00 | 99.99 |
| 9998 | 2026-01-07 22:38:00 | 99.98 |

### Ejercicio práctico

Crea otro índice parcial para obtener rápidamente los dos pedidos pagados más
recientes. La consulta debe devolver `pedido_id`, `creado_en` y `total` sin
necesitar esas tres columnas como claves de búsqueda.

### Solución paso a paso

1. Usa `creado_en` como clave porque filtra el orden y el límite.
2. Incluye las columnas que solo se devuelven.
3. Repite exactamente el predicado de la consulta.

```sql
CREATE INDEX l44_pedidos_pagados_fecha_idx
ON l44_pedidos (creado_en DESC)
INCLUDE (pedido_id, total)
WHERE estado = 'pagado';

VACUUM (ANALYZE) l44_pedidos;

EXPLAIN (ANALYZE, BUFFERS, COSTS OFF, SUMMARY OFF)
SELECT pedido_id, creado_en, total
FROM l44_pedidos
WHERE estado = 'pagado'
ORDER BY creado_en DESC
LIMIT 2;

SELECT pedido_id, creado_en, total
FROM l44_pedidos
WHERE estado = 'pagado'
ORDER BY creado_en DESC
LIMIT 2;
```

Resultado esperado:

| pedido_id | creado_en | total |
|---:|---|---:|
| 9990 | 2026-01-07 22:30:00 | 99.90 |
| 9989 | 2026-01-07 22:29:00 | 99.89 |

### Matices y buenas prácticas

- PostgreSQL solo puede usar un índice parcial si reconoce que el `WHERE` de
  la consulta implica el predicado del índice. Escribe el predicado de forma
  coherente.
- Una consulta preparada con un parámetro genérico como `estado = $1` puede no
  demostrar durante la planificación que necesita el subconjunto del índice.
- `INCLUDE` puede evitar accesos a la tabla, pero aumenta el tamaño del índice.
  No incluyas columnas anchas sin medir.
- `VACUUM` se usa aquí para favorecer un `Index Only Scan` reproducible. En una
  tabla con muchas escrituras puede haber `Heap Fetches` mayores que cero.
- No desactives `enable_seqscan` como solución permanente: deja que el
  planificador compare costes y revisa estadísticas y selectividad.

### PostgreSQL 18: novedad frente a concepto existente

- Los índices parciales son anteriores a PostgreSQL 18; ya aparecían en la
  documentación de PostgreSQL 10.
- `INCLUDE` se incorporó en PostgreSQL 11, no en PostgreSQL 18.
- PostgreSQL 18 mantiene estas capacidades y permite verificar su uso con
  `EXPLAIN`; la elección concreta del plan depende de los datos y estadísticas.

Documentación oficial: [índices parciales](https://www.postgresql.org/docs/18/indexes-partial.html),
[consultas cubiertas e Index Only Scan](https://www.postgresql.org/docs/18/indexes-index-only-scans.html)
y [uso de EXPLAIN](https://www.postgresql.org/docs/18/using-explain.html).

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

## Lección 42 · Permisos futuros con ALTER DEFAULT PRIVILEGES

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

Un `GRANT` normal modifica objetos que ya existen. `ALTER DEFAULT PRIVILEGES`
define qué permisos recibirán los objetos que un rol cree en el futuro. Es útil
para que cada tabla nueva de la tienda sea legible por el grupo de informes sin
tener que recordar un nuevo `GRANT` cada vez.

Esta práctica requiere ejecutarse con un usuario que pueda crear roles. Los
roles del ejemplo son `NOLOGIN`: representan un grupo y un usuario de prueba,
pero no permiten conectarse.

### Datos mínimos y ejemplo ejecutable

```sql
DO $bloque$
BEGIN
    IF NOT EXISTS (SELECT 1 FROM pg_roles WHERE rolname = 'l42_lectura') THEN
        CREATE ROLE l42_lectura NOLOGIN;
    END IF;

    IF NOT EXISTS (SELECT 1 FROM pg_roles WHERE rolname = 'l42_usuario') THEN
        CREATE ROLE l42_usuario NOLOGIN;
    END IF;
END
$bloque$;

GRANT l42_lectura TO l42_usuario;

DROP SCHEMA IF EXISTS l42_tienda CASCADE;
CREATE SCHEMA l42_tienda;

REVOKE ALL ON SCHEMA l42_tienda FROM PUBLIC;
GRANT USAGE ON SCHEMA l42_tienda TO l42_lectura;

-- Se crea antes de cambiar los privilegios predeterminados.
CREATE TABLE l42_tienda.productos_antiguos (
    producto_id integer PRIMARY KEY,
    nombre      text NOT NULL
);

ALTER DEFAULT PRIVILEGES IN SCHEMA l42_tienda
GRANT SELECT ON TABLES TO l42_lectura;

-- Se crea después: recibirá SELECT automáticamente.
CREATE TABLE l42_tienda.productos (
    producto_id integer PRIMARY KEY,
    nombre      text NOT NULL,
    precio      numeric(10,2) NOT NULL
);

INSERT INTO l42_tienda.productos VALUES
    (1, 'Monitor', 249.00),
    (2, 'Teclado', 79.00);
```

Comprueba los permisos efectivos del usuario, incluida su pertenencia al rol de
grupo:

```sql
SELECT has_schema_privilege(
           'l42_usuario', 'l42_tienda', 'USAGE'
       ) AS puede_usar_esquema,
       has_table_privilege(
           'l42_usuario', 'l42_tienda.productos_antiguos', 'SELECT'
       ) AS lee_tabla_antigua,
       has_table_privilege(
           'l42_usuario', 'l42_tienda.productos', 'SELECT'
       ) AS lee_tabla_nueva,
       has_table_privilege(
           'l42_usuario', 'l42_tienda.productos', 'INSERT'
       ) AS puede_insertar;
```

### Resultado esperado

| puede_usar_esquema | lee_tabla_antigua | lee_tabla_nueva | puede_insertar |
|---|---|---|---|
| true | false | true | false |

La tabla antigua no cambia retroactivamente. La tabla nueva hereda `SELECT`,
pero no `INSERT`, respetando el principio de mínimo privilegio.

### Ejercicio práctico

Concede lectura sobre las tablas que ya existían y verifica además que una
tercera tabla creada después recibe el permiso predeterminado.

### Solución explicada paso a paso

1. Corrige los objetos existentes con un `GRANT` explícito.

```sql
GRANT SELECT ON ALL TABLES IN SCHEMA l42_tienda TO l42_lectura;
```

2. Crea otra tabla después de configurar los permisos predeterminados.

```sql
CREATE TABLE l42_tienda.pedidos (
    pedido_id integer PRIMARY KEY,
    total     numeric(10,2) NOT NULL
);
```

3. Comprueba ambas tablas.

```sql
SELECT has_table_privilege(
           'l42_usuario', 'l42_tienda.productos_antiguos', 'SELECT'
       ) AS antigua_corregida,
       has_table_privilege(
           'l42_usuario', 'l42_tienda.pedidos', 'SELECT'
       ) AS futura_automatica,
       has_table_privilege(
           'l42_usuario', 'l42_tienda.pedidos', 'UPDATE'
       ) AS puede_actualizar;
```

Resultado esperado:

| antigua_corregida | futura_automatica | puede_actualizar |
|---|---|---|
| true | true | false |

### Buena práctica

Concede permisos a roles de grupo (`l42_lectura`) y añade usuarios al grupo;
evita repetir permisos usuario por usuario. Si las tablas las crea otro rol,
configura sus valores predeterminados explícitamente con:

```sql
ALTER DEFAULT PRIVILEGES FOR ROLE rol_propietario
IN SCHEMA l42_tienda
GRANT SELECT ON TABLES TO l42_lectura;
```

El ejecutor debe ser ese propietario, un miembro autorizado del rol o un
administrador con los privilegios necesarios.

### PostgreSQL 18: novedad frente a concepto existente

- `ALTER DEFAULT PRIVILEGES`, roles de grupo y `USAGE` sobre esquemas no son
  novedades de PostgreSQL 18.
- En PostgreSQL 18 sigue siendo esencial recordar que solo afecta a objetos
  futuros y que los valores predeterminados del creador no se obtienen por
  herencia desde otros roles.
- `has_table_privilege()` y `has_schema_privilege()` permiten probar permisos
  efectivos sin depender de la presentación de `\dp` en `psql`.

Documentación oficial: [ALTER DEFAULT PRIVILEGES](https://www.postgresql.org/docs/18/sql-alterdefaultprivileges.html),
[privilegios](https://www.postgresql.org/docs/18/ddl-priv.html)
y [funciones de comprobación](https://www.postgresql.org/docs/18/functions-info.html).

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

## Lección 43 · Triggers por sentencia con tablas de transición

[<u>↑ Volver al índice</u>](#índice-temático)

### Objetivo

Auditar una actualización masiva de existencias con **una sola fila de
auditoría por sentencia SQL**, en vez de ejecutar una función una vez por cada
producto modificado.

### Repaso breve

En la lección 12 usamos `FOR EACH ROW`: `OLD` y `NEW` representaban una fila.
Ahora usaremos `FOR EACH STATEMENT` y dos **tablas de transición**:

- `OLD TABLE`: todas las filas tal como estaban antes del `UPDATE`.
- `NEW TABLE`: todas las filas tal como quedan después del `UPDATE`.

La cláusula `REFERENCING` asigna nombres a esos conjuntos. Dentro de la función
se consultan como tablas temporales de solo lectura.

### Datos mínimos

El bloque es independiente de las lecciones anteriores y puede ejecutarse
completo en PostgreSQL 18:

```sql
DROP TABLE IF EXISTS l43_auditoria_stock;
DROP TABLE IF EXISTS l43_productos;

CREATE TABLE l43_productos (
    producto_id integer PRIMARY KEY,
    nombre text NOT NULL,
    stock integer NOT NULL CHECK (stock >= 0)
);

CREATE TABLE l43_auditoria_stock (
    auditoria_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    filas_afectadas integer NOT NULL,
    cambio_total integer NOT NULL,
    registrado_en timestamptz NOT NULL DEFAULT current_timestamp
);

INSERT INTO l43_productos (producto_id, nombre, stock) VALUES
    (1, 'Teclado', 4),
    (2, 'Ratón', 8),
    (3, 'Monitor', 20);
```

### Función y trigger

```sql
CREATE OR REPLACE FUNCTION l43_registrar_actualizacion_stock()
RETURNS trigger
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO l43_auditoria_stock (filas_afectadas, cambio_total)
    SELECT count(*)::integer,
           coalesce(sum(n.stock - o.stock), 0)::integer
    FROM filas_anteriores AS o
    JOIN filas_nuevas AS n USING (producto_id);

    RETURN NULL;
END;
$$;

CREATE TRIGGER l43_stock_actualizado
AFTER UPDATE ON l43_productos
REFERENCING OLD TABLE AS filas_anteriores
            NEW TABLE AS filas_nuevas
FOR EACH STATEMENT
EXECUTE FUNCTION l43_registrar_actualizacion_stock();
```

`RETURN NULL` es adecuado porque PostgreSQL ignora el valor devuelto por un
trigger `AFTER` por sentencia.

### Prueba

Una única sentencia cambia dos productos:

```sql
UPDATE l43_productos
SET stock = stock + 5
WHERE producto_id IN (1, 2);

SELECT producto_id, nombre, stock
FROM l43_productos
ORDER BY producto_id;

SELECT auditoria_id, filas_afectadas, cambio_total
FROM l43_auditoria_stock
ORDER BY auditoria_id;
```

Resultados esperados:

| producto_id | nombre | stock |
|---:|---|---:|
| 1 | Teclado | 9 |
| 2 | Ratón | 13 |
| 3 | Monitor | 20 |

| auditoria_id | filas_afectadas | cambio_total |
|---:|---:|---:|
| 1 | 2 | 10 |

Hay una sola fila de auditoría: el trigger vio las dos filas del `UPDATE` como
un conjunto y sumó `(9 - 4) + (13 - 8) = 10`.

### Ejercicio práctico

Incrementa en 3 unidades el stock de todos los productos cuyo stock actual sea
menor que 10. Después, comprueba la auditoría completa.

### Solución paso a paso

1. Tras la primera prueba, solo `Teclado` tiene stock menor que 10.
2. La siguiente sentencia modifica ese producto, de 9 a 12:

```sql
UPDATE l43_productos
SET stock = stock + 3
WHERE stock < 10;
```

3. Consulta el estado final y las dos operaciones auditadas:

```sql
SELECT producto_id, nombre, stock
FROM l43_productos
ORDER BY producto_id;

SELECT auditoria_id, filas_afectadas, cambio_total
FROM l43_auditoria_stock
ORDER BY auditoria_id;
```

Resultados esperados:

| producto_id | nombre | stock |
|---:|---|---:|
| 1 | Teclado | 12 |
| 2 | Ratón | 13 |
| 3 | Monitor | 20 |

| auditoria_id | filas_afectadas | cambio_total |
|---:|---:|---:|
| 1 | 2 | 10 |
| 2 | 1 | 3 |

### Matiz y buena práctica

Un trigger `FOR EACH STATEMENT` también se ejecuta si la sentencia no modifica
ninguna fila. Esta función registraría entonces `0` filas y un cambio total de
`0`. Para omitir ese registro, añade al principio del cuerpo:

```sql
IF NOT EXISTS (SELECT FROM filas_nuevas) THEN
    RETURN NULL;
END IF;
```

Las tablas de transición requieren un trigger `AFTER` sobre una tabla ordinaria;
en un trigger de `UPDATE` con `REFERENCING` no se admite una lista `UPDATE OF
columna`. Mantén ligera la función: su trabajo forma parte de la misma
transacción y prolonga su duración.

### PostgreSQL 18: novedad frente a concepto existente

- Los triggers por sentencia y las tablas de transición **no son novedades de
  PostgreSQL 18**; ya estaban documentados en PostgreSQL 10.
- PostgreSQL 18 conserva `REFERENCING OLD TABLE` y `NEW TABLE` para que un
  trigger vea el conjunto completo afectado.
- No debe confundirse esto con `RETURNING old.columna` y `new.columna`, ampliado
  en PostgreSQL 18: aquí `OLD TABLE` y `NEW TABLE` pertenecen a la definición
  del trigger.

Documentación oficial: [CREATE TRIGGER](https://www.postgresql.org/docs/18/sql-createtrigger.html),
[comportamiento de los triggers](https://www.postgresql.org/docs/18/trigger-definition.html)
y [funciones trigger en PL/pgSQL](https://www.postgresql.org/docs/18/plpgsql-trigger.html).

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

**Ventanas:** Lección 6, Lección 7, Lección 24, Lección 45

**Rendimiento:** Lección 8, Lección 21, Lección 44

**Seguridad:** Lección 9, Lección 22

**PL/pgSQL:** Lección 10, Lección 11, Lección 12, Lección 43

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

## Lección 38 · Medir ANALYZE y detectar estadísticas desactualizadas

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

El planificador decide entre escaneos, índices y métodos de JOIN usando
estadísticas sobre el número y la distribución de filas. `ANALYZE` las
actualiza; el autovacuum también puede ejecutar `AUTOANALYZE`. La vista
`pg_stat_user_tables` permite comprobar cuándo ocurrió, cuántas veces y,
desde PostgreSQL 18, cuánto tiempo acumulado consumió.

### Datos mínimos y ejemplo ejecutable

```sql
DROP TABLE IF EXISTS l38_productos;

CREATE TABLE l38_productos (
    producto_id integer PRIMARY KEY,
    nombre      text NOT NULL,
    precio      numeric(10,2) NOT NULL,
    stock       integer NOT NULL
);

INSERT INTO l38_productos VALUES
    (1, 'Portátil', 899.00, 4),
    (2, 'Monitor',  249.00, 8),
    (3, 'Teclado',   79.00, 15),
    (4, 'Ratón',      39.00, 20);

ANALYZE l38_productos;
SELECT pg_stat_clear_snapshot();

SELECT relname,
       n_live_tup,
       analyze_count >= 1 AS analizada,
       total_analyze_time >= 0 AS tiempo_registrado
FROM pg_stat_user_tables
WHERE relname = 'l38_productos';
```

### Resultado esperado

| relname | n_live_tup | analizada | tiempo_registrado |
|---|---:|---|---|
| l38_productos | 4 | true | true |

El tiempo exacto no es fijo: depende del servidor. `pg_stat_clear_snapshot()`
evita reutilizar dentro de la transacción una instantánea anterior de las
estadísticas acumuladas.

### Ejercicio práctico

Inserta dos productos sin ejecutar `ANALYZE`. Comprueba primero la estimación
guardada en `pg_class`, actualiza las estadísticas y vuelve a comprobarla.

```sql
INSERT INTO l38_productos VALUES
    (5, 'Webcam',   99.00, 6),
    (6, 'Auriculares', 129.00, 10);

SELECT reltuples::bigint AS filas_estimadas
FROM pg_class
WHERE oid = 'l38_productos'::regclass;
```

Antes de analizar, el resultado esperado es `4`: las dos filas existen, pero
la estimación del catálogo todavía procede del análisis anterior.

### Solución explicada paso a paso

1. Actualiza las estadísticas de la tabla.

```sql
ANALYZE l38_productos;
```

2. Comprueba la nueva estimación.

```sql
SELECT reltuples::bigint AS filas_estimadas
FROM pg_class
WHERE oid = 'l38_productos'::regclass;
```

Resultado esperado: `6`.

3. Comprueba que hubo al menos dos análisis manuales y que el tiempo acumulado
es un valor no negativo.

```sql
SELECT n_live_tup,
       analyze_count >= 2 AS dos_analisis,
       ROUND(total_analyze_time::numeric, 3) AS total_analyze_ms
FROM pg_stat_user_tables
WHERE relname = 'l38_productos';
```

Resultado comprobable: `n_live_tup = 6` y `dos_analisis = true`. El valor de
`total_analyze_ms` varía, pero nunca debe ser negativo.

Para inspeccionar el trabajo realizado puedes ejecutar también:

```sql
ANALYZE (VERBOSE) l38_productos;
```

### Buena práctica

No ejecutes `ANALYZE` continuamente por calendario sin observar la carga.
Revisa `last_analyze`, `last_autoanalyze`, sus contadores y los cambios reales
de datos. Si el autovacuum mantiene estadísticas recientes, un análisis manual
puede ser innecesario.

### PostgreSQL 18: novedad frente a concepto existente

- `ANALYZE`, `pg_class.reltuples`, `last_analyze` y los contadores ya existían.
- PostgreSQL 18 añade `total_vacuum_time`, `total_autovacuum_time`,
  `total_analyze_time` y `total_autoanalyze_time` a `pg_stat_all_tables` y sus
  variantes.
- PostgreSQL 18 amplía `ANALYZE (VERBOSE)` con estadísticas de WAL, CPU y
  lectura media. El tiempo de retraso por coste requiere
  `track_cost_delay_timing`.

Documentación oficial: [ANALYZE](https://www.postgresql.org/docs/18/sql-analyze.html),
[estadísticas acumuladas](https://www.postgresql.org/docs/18/monitoring-stats.html)
y [notas de PostgreSQL 18](https://www.postgresql.org/docs/18/release-18.html).

## Lección 39 · E/S por sesión con pg_stat_get_backend_io()

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

`pg_stat_io` muestra actividad de entrada/salida agregada por tipo de proceso.
PostgreSQL 18 añade `pg_stat_get_backend_io(pid)`, que permite observar cuánto
lee, escribe, amplía o encuentra en caché una sesión concreta. Es útil para
distinguir una consulta lenta por CPU de otra que mueve muchos datos.

### Datos mínimos y ejemplo ejecutable

```sql
DROP TABLE IF EXISTS l39_productos;

CREATE TABLE l39_productos (
    producto_id integer PRIMARY KEY,
    nombre      text NOT NULL,
    precio      numeric(10,2) NOT NULL,
    stock       integer NOT NULL
);

INSERT INTO l39_productos
SELECT n,
       'Producto ' || n,
       (20 + n % 500)::numeric(10,2),
       n % 50
FROM generate_series(1, 5000) AS g(n);

ANALYZE l39_productos;
SELECT pg_backend_pid() AS mi_pid;

SELECT backend_type,
       object,
       context,
       reads,
       read_bytes,
       writes,
       write_bytes,
       hits
FROM pg_stat_get_backend_io(pg_backend_pid())
WHERE object = 'relation'
  AND context = 'normal';
```

### Resultado esperado

Debe aparecer una fila semejante a esta; los números dependen de la sesión:

| backend_type | object | context | reads | read_bytes | writes | write_bytes | hits |
|---|---|---|---:|---:|---:|---:|---:|
| client backend | relation | normal | valor ≥ 0 | valor ≥ 0 | valor ≥ 0 | valor ≥ 0 | valor ≥ 0 |

Comprueba de forma determinista que la función devuelve contadores válidos:

```sql
SELECT COUNT(*) > 0 AS hay_estadisticas,
       bool_and(COALESCE(reads, 0) >= 0
            AND COALESCE(read_bytes, 0) >= 0
            AND COALESCE(writes, 0) >= 0
            AND COALESCE(write_bytes, 0) >= 0) AS contadores_validos
FROM pg_stat_get_backend_io(pg_backend_pid());
```

Resultado esperado:

| hay_estadisticas | contadores_validos |
|---|---|
| true | true |

### Ejercicio práctico

Guarda una fotografía de los contadores, recorre toda la tabla y comprueba si
aumentaron las lecturas o los aciertos de caché de la sesión.

### Solución explicada paso a paso

1. Guarda los valores actuales en una tabla temporal.

```sql
DROP TABLE IF EXISTS l39_io_antes;

CREATE TEMP TABLE l39_io_antes AS
SELECT object, context, reads, read_bytes, hits
FROM pg_stat_get_backend_io(pg_backend_pid());
```

2. Ejecuta una consulta que recorra los productos.

```sql
SELECT SUM(stock) AS stock_total
FROM l39_productos;
```

Resultado esperado: `122500`.

3. Compara la fotografía con los contadores nuevos.

```sql
WITH ahora AS (
    SELECT object, context, reads, read_bytes, hits
    FROM pg_stat_get_backend_io(pg_backend_pid())
)
SELECT COALESCE(SUM(GREATEST(a.reads - b.reads, 0)), 0) AS lecturas_nuevas,
       COALESCE(SUM(GREATEST(a.read_bytes - b.read_bytes, 0)), 0) AS bytes_nuevos,
       COALESCE(SUM(GREATEST(a.hits - b.hits, 0)), 0) AS hits_nuevos,
       COALESCE(SUM(GREATEST(a.reads - b.reads, 0)
                          + GREATEST(a.hits - b.hits, 0)), 0) > 0
           AS hubo_actividad
FROM ahora a
JOIN l39_io_antes b USING (object, context)
WHERE a.object = 'relation'
  AND a.context = 'normal';
```

Resultado comprobable: `hubo_actividad = true`. Si los bloques ya estaban en
memoria, pueden aumentar los `hits` y quedar `lecturas_nuevas = 0`; eso no es
un error, sino una lectura satisfecha por la caché compartida.

### Buena práctica

No interpretes `reads = 0` como «la consulta no leyó nada». Revisa también
`hits`. Para medir tiempos de espera de E/S activa `track_io_timing` solo tras
evaluar su pequeño coste de medición. No reinicies estadísticas globales en un
servidor de producción solo para hacer una prueba.

### PostgreSQL 18: novedad frente a concepto existente

- `pg_stat_io` y `pg_backend_pid()` ya existían.
- PostgreSQL 18 incorpora `pg_stat_get_backend_io(integer)` y
  `pg_stat_reset_backend_stats(integer)` para consultar o reiniciar estadísticas
  de un proceso concreto; el reinicio requiere privilegios elevados por defecto.
- PostgreSQL 18 añade a las estadísticas de E/S los contadores en bytes
  `read_bytes`, `write_bytes` y `extend_bytes`.

Documentación oficial: [sistema de estadísticas acumuladas](https://www.postgresql.org/docs/18/monitoring-stats.html),
[configuración de estadísticas](https://www.postgresql.org/docs/18/runtime-config-statistics.html)
y [notas de PostgreSQL 18](https://www.postgresql.org/docs/18/release-18.html).

## Lección 40 · WAL generado por sesión con pg_stat_get_backend_wal()

[<u>↑ Volver al índice</u>](#índice-temático)

### Idea principal

WAL (*Write-Ahead Log*) registra los cambios antes de que las páginas de datos
se escriban definitivamente. Hace posibles la recuperación tras fallos, la
replicación y las copias físicas. `pg_stat_wal` ofrece datos de todo el clúster;
PostgreSQL 18 añade `pg_stat_get_backend_wal(pid)` para saber cuánto WAL genera
una sesión concreta.

### Datos mínimos y ejemplo ejecutable

```sql
DROP TABLE IF EXISTS l40_lineas_pedido;
DROP TABLE IF EXISTS l40_pedidos;

CREATE TABLE l40_pedidos (
    pedido_id  integer PRIMARY KEY,
    cliente    text NOT NULL,
    creado_en  timestamptz NOT NULL DEFAULT current_timestamp
);

CREATE TABLE l40_lineas_pedido (
    pedido_id       integer NOT NULL REFERENCES l40_pedidos,
    producto        text NOT NULL,
    cantidad        integer NOT NULL CHECK (cantidad > 0),
    precio_unitario numeric(10,2) NOT NULL CHECK (precio_unitario >= 0)
);

SELECT wal_records,
       wal_fpi,
       wal_bytes,
       wal_buffers_full,
       stats_reset
FROM pg_stat_get_backend_wal(pg_backend_pid());
```

### Resultado esperado

La función devuelve una fila. Los valores exactos dependen de todo lo ejecutado
previamente por la conexión:

| wal_records | wal_fpi | wal_bytes | wal_buffers_full | stats_reset |
|---:|---:|---:|---:|---|
| valor ≥ 0 | valor ≥ 0 | valor ≥ 0 | valor ≥ 0 | fecha/hora o NULL |

Comprobación automática:

```sql
SELECT wal_records >= 0 AS registros_validos,
       wal_fpi >= 0 AS fpi_validas,
       wal_bytes >= 0 AS bytes_validos,
       wal_buffers_full >= 0 AS buffers_validos
FROM pg_stat_get_backend_wal(pg_backend_pid());
```

Resultado esperado: las cuatro columnas muestran `true`.

### Ejercicio práctico

Mide si una transacción que crea un pedido y sus líneas aumenta el WAL de tu
sesión.

### Solución explicada paso a paso

1. Guarda los contadores actuales en una tabla temporal.

```sql
DROP TABLE IF EXISTS l40_wal_antes;

CREATE TEMP TABLE l40_wal_antes AS
SELECT wal_records, wal_fpi, wal_bytes, wal_buffers_full
FROM pg_stat_get_backend_wal(pg_backend_pid());
```

2. Crea el pedido y sus líneas dentro de una sola transacción.

```sql
BEGIN;

INSERT INTO l40_pedidos (pedido_id, cliente)
VALUES (401, 'Ana');

INSERT INTO l40_lineas_pedido
    (pedido_id, producto, cantidad, precio_unitario)
VALUES
    (401, 'Teclado', 2, 79.00),
    (401, 'Ratón',   1, 39.00);

COMMIT;
```

3. Comprueba los datos de negocio.

```sql
SELECT p.pedido_id,
       p.cliente,
       SUM(l.cantidad * l.precio_unitario) AS total
FROM l40_pedidos p
JOIN l40_lineas_pedido l USING (pedido_id)
GROUP BY p.pedido_id, p.cliente;
```

Resultado esperado:

| pedido_id | cliente | total |
|---:|---|---:|
| 401 | Ana | 197.00 |

4. Compara el WAL anterior y posterior.

```sql
WITH despues AS (
    SELECT wal_records, wal_fpi, wal_bytes, wal_buffers_full
    FROM pg_stat_get_backend_wal(pg_backend_pid())
)
SELECT d.wal_records - a.wal_records AS registros_nuevos,
       d.wal_bytes - a.wal_bytes AS bytes_nuevos,
       d.wal_fpi - a.wal_fpi AS fpi_nuevas,
       d.wal_records > a.wal_records AS genero_wal
FROM despues d
CROSS JOIN l40_wal_antes a;
```

Resultado comprobable: `genero_wal = true`, con `registros_nuevos > 0` y
`bytes_nuevos > 0`. `fpi_nuevas` puede ser cero: una imagen completa de página
solo se genera cuando las reglas de protección de página lo requieren.

### Buena práctica

Una operación que genera mucho WAL también puede aumentar el uso de disco, el
tráfico hacia réplicas y el volumen de archivado. Compara sesiones antes de
optimizar y no reinicies sus estadísticas en producción sin un motivo claro.
El WAL confirma cambios físicos registrados, pero no sustituye a medir tiempo,
bloqueos y E/S.

### PostgreSQL 18: novedad frente a concepto existente

- WAL, `pg_stat_wal` y sus contadores ya existían.
- PostgreSQL 18 incorpora `pg_stat_get_backend_wal(integer)`, que devuelve los
  contadores WAL de un proceso concreto.
- Las estadísticas de una sesión pueden reiniciarse con
  `pg_stat_reset_backend_stats(integer)`; por defecto esta operación está
  restringida a usuarios con privilegios elevados.
- PostgreSQL 18 mueve el seguimiento de tiempos de E/S de WAL a las filas
  `object = 'wal'` de `pg_stat_io`, controladas por `track_wal_io_timing`.

Documentación oficial: [estadísticas acumuladas](https://www.postgresql.org/docs/18/monitoring-stats.html),
[configuración de estadísticas](https://www.postgresql.org/docs/18/runtime-config-statistics.html)
y [notas de PostgreSQL 18](https://www.postgresql.org/docs/18/release-18.html).

# Mantenimiento de esta guía

Archivo maestro: postgresql-18-lecciones.pdf. La guía debe actualizarse
añadiendo nuevas lecciones en su bloque temático, conservando ejemplos
SQL ejecutables, resultados esperados y ejercicios con solución. La
numeración conserva el historial original; si falta una lección en el
chat, no se inventa.
