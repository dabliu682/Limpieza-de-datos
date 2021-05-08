## SCRIPTS DE INTEGRACION DE DATOS
1. Crear las bases de datos SABERPRO-2011-2014 en el SGBD PostgreSQL.
>create database SABERPRO-2011-2014;
>3. Crear la tabla saberpro_2011_2014 a partir de la tabla saberpro_2011: 
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
