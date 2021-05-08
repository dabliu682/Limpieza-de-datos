## SCRIPTS DE INTEGRACION DE DATOS
1. Crear las bases de datos SABERPRO-2011-2014 en el SGBD PostgreSQL.
>create database SABERPRO-2011-2014;
3. Crear la tabla saberpro_2011_2014 a partir de la tabla saberpro_2011: 
>create table saberpro_2011_2014 as select * from saberpro_2011;
4. Adicionar en la tabla saberpro_2011_2014 el atributo prueba de tipo text:
>alter table saberpro_2011_2014 add prueba text;
5. Actualizar en la tabla saberpro_2011_2014 el atributo prueba con el valor de 20112:
>Update saberpro_2011_2014 set prueba=20112;
6. Adicionar en la tabla saberpro_2011_2014 el atributo mod_comp_ciudadanas_punt de tipo text:
>alter table saberpro_2011_2014 add mod_comp_ciudadanas_punt text;
7. Adicionar en la tabla saberpro_2014 el atributo prueba de tipo text:
>alter table saberpro_2014 add prueba text;
8. Actualizar en la tabla saberpro_2014 el atributo prueba substrayendo el valor del año y periodo del atributo estu_consecutivo:
>update saberpro_2014 set prueba=substr(estu_consecutivo,6,5);
9. Adicionar en la tabla saberpro_2014 el atributo estu_cod_aplicacion de tipo text:
>alter table saberpro_2014 add estu_cod_aplicacion text
10. Actualizar en la tabla saberpro_2014 el atributo estu_cod_aplicacion concatenando ‘EK’+prueba
>update saberpro_2014 set estu_cod_aplicacion =’EK’ || prueba;
11. Visualizar los esquemas de las tablas con el fin de obtener los atributos comunes:
>select column_name from information_schema.columns where table_name='saberpro_2011_2014'; <br>
>select column_name from information_schema.columns where table_name='saberpro_2012'; <br>
>select column_name from information_schema.columns where table_name='saberpro_2013'; <br>
>select column_name from information_schema.columns where table_name='saberpro_2014'
12. Comparar los esquemas de las tablas saberpro_2012, saberpro_2013, saberpro_2014 para determinar los atributos comunes entre las tablas con respecto a saberpro_2011_2014:
>select column_name from information_schema.columns where table_name='saberpro_2011_2014' intersect select column_name from information_schema.columns where table_name='saberpro_2012';<br>
>select column_name from information_schema.columns where table_name='saberpro_2011_2014' intersect select column_name from information_schema.columns where table_name='saberpro_2013';<br>
>select column_name from information_schema.columns where table_name='saberpro_2011_2014' intersect select column_name from information_schema.columns where table_name='saberpro_2014';<br>
13. Comparar los esquemas de las tablas saberpro_2012, saberpro_2013, saberpro_2014 para determinar los atributos diferentes de estas tablas con respecto a saberpro_2011_2014:
>select column_name from information_schema.columns where table_name='saberpro_2012' except select column_name from information_schema.columns where table_name='saberpro_2011_2014';<br>
>select column_name from information_schema.columns where table_name='saberpro_2013' except select column_name from information_schema.columns where table_name='saberpro_2011_2014';<br>
>select column_name from information_schema.columns where table_name='saberpro_2014' except select column_name from information_schema.columns where table_name='saberpro_2011_2014';<br>
14. Hacer un análisis de los datos de las tablas saberpro_2012, saberpro_2013 y saberpro-2014 para determinar atributos equivalentes, teniendo en cuenta el diccionario de datos de saberpro_20112 (ver anexo RESULTADOS ANALISIS DE DATOS)
15. Insertar en la tabla saberpro_2011_2014 los datos de las tablas saberpro_2012, saberpro_2013 y saberpro_2014, teniendo en cuenta los atributos comunes y equivalentes. 
>insert into saberpro_2011_2014 <br>         (select estuconsecutivo,<br> estu_cod_aplicacion,<br> estu_genero, estu_nacimiento_dia,
estu_nacimiento_mes, estu_nacimiento_anno, estu_pais_reside, estu_estado_civil,
estu_disc_invidente, ……… from saberpro_2012)
