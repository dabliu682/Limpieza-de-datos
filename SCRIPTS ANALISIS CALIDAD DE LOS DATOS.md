### ANALISIS CALIDAD DE DATOS

1. Crear la tabla saberpro_limpio a partir de la tabla saberpro_2011_2014 
>create table saberpro_limpio as select * from saberpro_2011_2014
2. Realizar un análisis inicial de la calidad de los datos de la tabla saberpro_limpio contando el numero de registros no nulos, nulos, distintos valores y valores distintos
(mostrar máximo 10 valores distintos, ver anexo RESULTADOS ANALISIS DE DATOS)
>select count(*) from saberpro_limpio where estu_cod_aplicacion is not null;<br>
select count(*) from saberpro_limpio where estu_cod_aplicacion is null;<br>
select count(distinct estu_cod_aplicacion) from saberpro_limpio;<br>
select estuconsecutivo,count(*) from saberpro_limpio group by 1 order by 1 limit 10;
