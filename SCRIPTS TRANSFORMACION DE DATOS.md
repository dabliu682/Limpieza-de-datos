### TRANSOFORMACION DE DATOS
1. Crear el repositorio saberpro_transformado a partir de saberpro_limpio.
>create table saberpro_transformado as select * from saberpro_2011_2014;

2. Crear el atributo estu_nacimiento_fecha de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_nacimiento_fecha text;

3. Reemplazar los valores atípicos del atributo estu_nacimiento_anno por el año de la prueba -15 años para aquellos valores atípicos del atributo estu_nacimiento_anno que estén:
* Entre 1996 y 2011 para la prueba 20112. 
* Entre 1997 y 2012 para la prueba 20121 y 20122
* Entre 1998 y 2013 para la prueba 20131 y 20132
* Entre 1999 y 2014 para la prueba 20141 y 20142
>CREATE index I_estu_nacimiento_anno on saberpro_transformado(estu_nacimiento_anno);<br> 
CREATE index I_prueba on saberpro_transformado(prueba);<br> 
UPDATE saberpro_transformado set estu_nacimiento_anno= (case when prueba='20112' and estu_nacimiento_anno between '1996' and '2011' then cast((cast(substr(prueba,1,4) as numeric)-15) AS char) when (prueba='20121' or prueba='20122') and estu_nacimiento_anno between '1997' and '2012' then cast((cast(substr(prueba,1,4) as numeric)-15) AS char) when (prueba='20131' or prueba='20132') and estu_nacimiento_anno between '1998' and '2013' then cast((cast(substr(prueba,1,4) as numeric)-15) AS char) when (prueba='20141' or prueba='20142') and estu_nacimiento_anno between '1999' and '2014' then cast((cast(substr(prueba,1,4) as numeric)-15) AS char) else estu_nacimiento_anno end) where estu_nacimiento_anno is not null and estu_nacimiento_anno <> '';

4. Reemplazar los valores atípicos del atributo estu_nacimiento_anno por el año de la prueba - 60 años para aquellos valores atípicos del atributo estu_nacimiento_anno que estén:
* <=1951 para la prueba 20112. 
* <=1952 para la prueba 20121 y 20122
* <=1953 para la prueba 20131 y 20132
* <=1954 para la prueba 20141 y 20142
>select estu_nacimiento_anno from saberpro_transformado where estu_nacimiento_anno = 'estu_nacimiento_anno';
update saberpro_transformado set estu_nacimiento_anno = 0 where estu_nacimiento_anno = 'estu_nacimiento_anno';
update saberpro_transformado set estu_nacimiento_anno = (case when (cast(estu_nacimiento_anno as numeric) <= 1951 and (prueba = '20112')) then cast(cast(substr(prueba,1,4) as numeric) - 60 as char) when (cast(estu_nacimiento_anno as numeric) <= 1952 and (prueba='20121' or prueba='20122')) then cast(cast(substr(prueba,1,4) as numeric) - 60 as char) when (cast(estu_nacimiento_anno as numeric) <= 1953 and (prueba='20131' or prueba='20132')) then cast(cast(substr(prueba,1,4) as numeric) - 60 as char) when (cast(estu_nacimiento_anno as numeric) <= 1954 and (prueba='20141' or prueba='20142')) then cast(cast(substr(prueba,1,4) as numeric) - 60 as char) else estu_nacimiento_anno end) where estu_nacimiento_anno is not null and estu_nacimiento_anno <> '';

5. Reemplazar el valor atípico del atributo estu_nacimiento_anno de 2093 por el año 1993.
>update saberpro_transformado set estu_nacimiento_anno='1993' where estu_nacimiento_anno='2093';

6. Actualizar el atributo estu_nacimiento_fecha concatenando los atributos estu_nacimiento_dia, estu_nacimiento_mes y estu_nacimiento_anno con el formato DD/MM/YYYY.
>UPDATE saberpro_transformado set estu_nacimiento_fecha = estu_nacimiento_dia || '/' || estu_nacimiento_mes || '/' || estu_nacimiento_anno;

7. Crear el atributo estu_fecha_presentacion de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_fecha_presentacion text;

8. Actualizar el atributo estu_fecha_presentacion con la fecha de presentación de la prueba saberpro:
* 20112->20/11/2011 
* 20121->03/06/2012
>update 	saberpro_transformado 
set 	estu_fecha_presentacion = case 	when 	prueba = '20112' then '20/11/2011'
					when	prueba = '20121' then '03/06/2012'
					when	prueba = '20122' then '18/11/2012'
					when	prueba = '20131' then '16/06/2013'
					when	prueba = '20132' then '27/11/2013'
					when	prueba = '20141' then '08/06/2014'
					when	prueba = '20142' then '30/11/2014'
					end;

9. Crear el atributo estu_edad_presentacion de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_edad_presentacion text;

10. Actualizar el atributo estu_edad_presentacion a partir de los atributos estu_nacimiento_fecha y estu_fecha_presentacion
>update saberpro_transformado set estu_edad_presentacion = (to_date(estu_fecha_presentacion, 'dd/mm/yyyy') - to_date(estu_nacimiento_fecha, 'dd/mm/yyyy'))/365

11. Crear el atributo estu_rango_edad de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_rango_edad text;

12. Actualizar el atributo estu_rango_edad discretizando el atributo estu_edad_presentacion en 5 bines de igual rango acuerdo a la siguiente tabla:
>update 	saberpro_transformado 
set 	estu_rango_edad	 = case 	when 	estu_edad_presentacion::int < 20 then '<23'
					when	estu_edad_presentacion::int between 23 and 31 then '23 hasta 32'
					when	estu_edad_presentacion::int between 32 and 40 then '32 hasta 41'
					when	estu_edad_presentacion::int between 41 and 49 then '41 hasta 50'
					when	estu_edad_presentacion::int >= 50 then '>=50'
					end;

13. Reemplazar los valores del atributo estu_pais_reside diferente de ‘COLOMBIA’ por ‘OTROS’
>update 	saberpro_transformado set 	estu_pais_reside = 'OTROS' where estu_pais_reside <> 'COLOMBIA';

14. Crear el atributo estu_estado_civil_nom de tipo text15. Actualizar el atributo estu_estado_civil_nom de acuerdo a los códigos del atributo estu_estado_civil:
* TABLA
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_estado_civil_nom text;

15. Crear el atributo estu_discapacidad de tipo text
>update 	saberpro_transformado 
set 	estu_estado_civil_nom = case 	when 	estu_estado_civil = '01' then 'Soltero(a)'
					when 	estu_estado_civil = '02' then 'Casado(a)'
					when 	estu_estado_civil = '03' then 'Viudo(a)'
					when 	estu_estado_civil = '04' then 'Separado(a) y/o Divorciado'
					when 	estu_estado_civil = '05' then 'Unión Libre'


16. Actualizar el atributo estu_discapacidad con ‘S’ si en algunos de estos atributos hay una incapacidad: estu_disc_invidente, estu_disc_sordo_con_interprete, estu_disc_sordo_sin_interprete, estu_disc_motriz y estu_disc_sordo_ceguera.
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_discapacidad text;

17. Reemplazar los valores nulos del atributo estu_discapacidad por ‘N’
>update saberpro_transformado set estu_discapacidad = estu_disc_invidente || ',' || estu_disc_sordo_con_interprete || ',' || estu_disc_sordo_sin_interprete || ',' || estu_disc_motriz || ',' || estu_disc_sordo_ceguera;
>update saberpro_transformado set estu_discapacidad = 'N' where estu_discapacidad is null;

18. Actualizar los valores anómalos del atributo estu_reside_codmpio (que no corresponden a ningún código DANE) teniendo en cuenta los atributos estu_exam_codmpio_presentacion y estu_exam_mpio_presentacion:
>update saberpro_transformado set estu_reside_codmpio='08001' where estu_reside_codmpio='8001';<br>
>update saberpro_transformado set estu_reside_codmpio= case when estu_exam_codmpio_presentacion='11001' then '11001' when estu_exam_codmpio_presentacion='68001' then '68001' when estu_exam_codmpio_presentacion='66170' then '66170' else estu_reside_codmpio end where estu_reside_codmpio='09000';<br>
>update saberpro_transformado set estu_reside_codmpio='05088' where estu_reside_codmpio='27086';

19. Crear el atributo estu_reside_nommpio de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_reside_nommpio text;

20. Actualizar el atributo estu_reside_nommpio con los valores correspondientes a los nombres de los municipios de la tabla municipios del DANE, de acuerdo al código del atributo estu_reside_codmpio.
>update 	saberpro_transformado set estu_reside_nommpio = ( select nombrempio from municipios where cod_mpio = estu_reside_codmpio );

21. Crear el atributo estu_reside_nomdpto de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_reside_nomdpto text;

22. Actualizar el atributo estu_reside_nomdpto con los valores correspondientes a los nombres de los departamentos de la tabla del DANE, de acuerdo al código de los dos primeros dígitos del atributo estu_reside_codmpio.
>update 	saberpro_transformado set estu_reside_nomdpto = ( select nombredpto from departamentos where cod_dpto = estu_reside_codmpio );

23. Crear el atributo inst_origen_general de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN inst_origen_general text;

24. Actualizar los valores del atributo inst_origen_general con los valores correspondientes a los valores del atributo inst_origen generalizados:
>update 	saberpro_transformado set inst_origen_general = 	case 	when inst_origen in ('OFICIAL MUNICIPAL','OFICIAL DEPARTAMENTAL','OFICIAL NACIONAL','OFICIAL') then 'OFICIAL' when inst_origen in ('NO OFICIAL - FUNDACION','NO OFICIAL CORPORACION','NO OFICIAL') then 'PRIVADA' when inst_origen in ('REGIMEN ESPECIAL ') then 'REGIMEN ESPECIAL' end;

25. Reemplazar el valor del atributo inst_caracter_academico de ACADEMICO por NORMALISTA.
>update 	saberpro_transformado set inst_caracter_academico = 'NORMALISTA' where inst_caracter_academico = 'ACADEMICO';

26. Crear el atributo inst_acreditada de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN inst_acreditada text;

27. Actualizar los valores del atributo inst_prgm_acreditado por ‘ACREDITADO’ si el programa está acreditado en la tabla PRGM_ACREDITADOS y ‘NO ACREDITADO’ sino lo está.
>update 	saberpro_transformado set inst_prgm_acreditado = ( select 'ACREDITADO' from PRGM_ACREDITADOS where codigo_inst = inst_cod_institucion and  nombre_pgrm = estu_prgm_academico limit 1);<br>
>update 	saberpro_transformado set inst_prgm_acreditado = 'NO ACREDITADO' where inst_prgm_acreditado is null or inst_prgm_acreditado = '';

28. Crear el atributo inst_prgm_metodologia de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN inst_prgm_metodologia text;

29. Actualizar el atributo inst_prgm_metodologia, a partir del atributo estu_metodo_prgm estableciendo únicamente como metodologías la “PRESENCIAL” y “DISTANCIA”
>update 	saberpro_transformado set inst_prgm_metodologia = case when estu_metodo_prgm in ('VIRTUAL','DISTANCIA (TRADICIONAL)','A DISTANCIA (VIRTUAL)','SEMIPRESENCIAL') then 'DISTANCIA' 

30. Crear el atributo inst_prgm_municipio de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN inst_prgm_municipio text;

31. Actualizar el atributo inst_prgm_municipio a partir del atributo municipio_programa de la tabla programas_ies en el caso de que sean iguales y sino actualizar con el atributo estu_exam_mpio_presentacion
>update saberpro_transformado set inst_prgm_municipio = municipio_programa;

32. Actualizar los nulos del atributo inst_prgm_municipio (si los hay) con el valor del atributo estu_exam_mpio_presentacion
>update saberpro_transformado set inst_prgm_municipio = estu_exam_mpio_presentacion where inst_prgm_municipio is null;

33. Crear el atributo inst_prgm_dpto de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN inst_prgm_dpto text;

34. Actualizar el atributo inst_prgm_dpto a partir del atributo estu_exam_dpto_presentacion
>update 	saberpro_transformado set inst_prgm_dpto = estu_exam_dpto_presentacion;

35. Crear el atributo inst_prgm_zonageo de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN inst_prgm_zonageo text;

36. Actualizar el atributo inst_prgm_zonageo
>update 	saberpro_transformado 
set 	inst_prgm_zonageo = 	case 	when lower(estu_metodo_prgm) in ('atlántico','bolívar','cesar','córdoba','guajira','magdalena','san andrés','providencia y santa catalina','sucre') then 'ATLANTICA' 
										when lower(estu_metodo_prgm) in ('amazonas','arauca','casanare','guainía','guaviare','putumayo','vaupes','vichada') then 'ORINOQUIA' 
										when lower(estu_metodo_prgm) in ('Boyacá','Cundinamarca','Norte Santander','Santander','Meta') then 'ORIENTAL' 
										when lower(estu_metodo_prgm) in ('caldas','risaralda','quindío','huila','tolima','caquetá') then 'CENTRAL' 
										when lower(estu_metodo_prgm) in ('cauca','chocó','nariño','valle del cauca') then 'PACÍFICA' 
										when lower(estu_metodo_prgm) in ('distrito capital de bogotá') then 'BOGOTÁ' 
										when lower(estu_metodo_prgm) in ('antioquia') then 'ANTIOQUIA' 
								end;
                
37. Crear el atributo area_grupo_referencia de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN area_grupo_referencia text;

38. Actualizar los valores nulos del atributo area_grupo_referencia
>update 	saberpro_transformado 
set 	area_grupo_referencia = 	case 	when lower(estu_metodo_prgm) like '%ARTES%' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like 'CIENCIAS NATURALES Y EXACTAS ' then 'CIENCIAS NATURALES Y TÉCNICAS'
											when lower(estu_metodo_prgm) like 'CIENCIAS SOCIALES' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like 'HUMANIDADES' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like 'DERECHO' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like 'COMUNICACI_N, PERIODISMO Y PUBLICIDAD' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like 'CIENCIAS MILITARES Y NAVALES' then 'CIENCIAS NATURALES Y TÉCNICAS' 
											when lower(estu_metodo_prgm) like '%CIENCIAS AGROPECUARIAS% ' then 'CIENCIAS NATURALES Y TÉCNICAS' 
											when lower(estu_metodo_prgm) like '%ADMINISTRACI_N' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like 'EDUCACI_N' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like 'ARQUITECTURA Y URBANISMO%' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like 'INGENIER_A' then 'CIENCIAS NATURALES Y TÉCNICAS' 
											when lower(estu_metodo_prgm) like '%SALUD%' then 'CIENCIAS DE LA SALUD' 
											when lower(estu_metodo_prgm) like 'MEDICINA' then 'CIENCIAS DE LA SALUD' 
											when lower(estu_metodo_prgm) like '%INGENIER_A, INDUSTRIA Y MINAS%' then 'CIENCIAS NATURALES Y TÉCNICAS' 
											when lower(estu_metodo_prgm) like '%TIC%' then 'CIENCIAS NATURALES Y TÉCNICAS' 
											when lower(estu_metodo_prgm) like '%ARTES - DISEÑO – COMUNICACI_N% ' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like '%CIENCIAS AGROPECUARIAS% ' then 'CIENCIAS NATURALES Y TÉCNICAS' 
											when lower(estu_metodo_prgm) like 'NORMALES SUPERIORES' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like '%JUDICIAL%' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like '%MILITAR Y POLICIAL%' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like 'RECREACI_N Y DEPORTES' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like '%ECONOM%' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like '%CONTADUR_A%' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like 'PSICOLOG_A' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like 'ENFERMER_A' then 'CIENCIAS DE LA SALUD' 
											when lower(estu_metodo_prgm) like 'GRUPO REFERENCIA NACIONAL UNIVERSITARIO' then 'CIENCIAS NATURALES Y TÉCNICAS' 
											when lower(estu_metodo_prgm) like 'GRUPO REFERENCIA NACIONAL' and estu_prgm_academico = 'ARQUITECTURA' then 'CIENCIAS SOCIALES' 
											when lower(estu_metodo_prgm) like 'GRUPO REFERENCIA NACIONAL' and estu_prgm_academico like '%INGENIER_A%' then 'CIENCIAS NATURALES Y TÉCNICAS'  
											when lower(estu_metodo_prgm) like 'GRUPO REFERENCIA NACIONAL' and estu_prgm_academico like '%LICENCIATURA%' then 'CIENCIAS HUMANAS'  
											when lower(estu_metodo_prgm) like 'GRUPO REFERENCIA NACIONAL' and estu_prgm_academico = '%MUSICA%' then 'CIENCIAS HUMANAS' 
											when lower(estu_metodo_prgm) like 'GRUPO REFERENCIA NACIONAL' and estu_prgm_academico = '%SICOLOG_A%' then 'CIENCIAS HUMANAS'
											when lower(estu_metodo_prgm) like 'GRUPO REFERENCIA NACIONAL' and estu_prgm_academico = '%TEC%' then 'CIENCIAS NATURALES Y TÉCNICAS'  											
end;

39. Crear el atributo estu_sn_vive_flia de tipo text
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_sn_vive_flia text;

40. Actualizar el atributo estu_sn_vive_flia a partir del atributo estu_hogar_actual asi:
* Si estu_hogar_actual=’1’ entonces ‘S’ sino ‘N’
>update saberpro_transformado set	estu_sn_vive_flia = case when estu_hogar_actual = '1' then 'S' else 'N' end ;

41. Crear el atributo estu_sn_pers_cargo
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_sn_pers_cargo text;

42. Actualizar el atributo estu_sn_pers_cargo asi:
* Si fami_num_pers_cargo=’0’ entonces ‘N’ sino ‘S’
>update saberpro_transformado set estu_sn_pers_cargo = case when fami_num_pers_cargo = '0' then 'N' else 'S' end ;

43. Crear el atributo fami_cod_max_nivel_educa_padres
>ALTER TABLE public.saberpro_transformado ADD COLUMN fami_cod_max_nivel_educa_padres text;

44. Actualizar el atributo fami_cod_max_nivel_educa_padres con el máximo nivel educativo entre el padre y la madre
>update saberpro_transformado set	fami_cod_max_nivel_educa_padres = GREATEST(fami_cod_educa_padre::int, fami_cod_educa_madre::int);

45. Crear el atributo fami_max_nivel_educa_padres
>ALTER TABLE public.saberpro_transformado ADD COLUMN fami_max_nivel_educa_padres text;

46. Actualizar el atributo fami_max_nivel_educa_padres con la descripción del código del atributo fami_cod_max_nivel_educa_padres:
>update 	saberpro_transformado 
set 	fami_max_nivel_educa_padres = 	case 	when 	fami_cod_max_nivel_educa_padres = '0' then 'Ninguno'
												when 	fami_cod_max_nivel_educa_padres = '9' then 'Ninguno'
												when 	fami_cod_max_nivel_educa_padres = '10' then 'Primaria'
												when 	fami_cod_max_nivel_educa_padres = '11' then 'Primaria'
												when 	fami_cod_max_nivel_educa_padres = '12' then 'Bachiller'
												when 	fami_cod_max_nivel_educa_padres = '13' then 'Bachiller'
												when 	fami_cod_max_nivel_educa_padres = '14' then 'Técnico/Tecnólogo'
												when 	fami_cod_max_nivel_educa_padres = '15' then 'Bachiller'
												when 	fami_cod_max_nivel_educa_padres = '16' then 'Profesional'
												when 	fami_cod_max_nivel_educa_padres = '17' then 'Postgrado'
												when 	fami_cod_max_nivel_educa_padres = '99' then 'No sabe'
										end;
                    
47. Crear el atributo fami_ocup_padre
>ALTER TABLE public.saberpro_transformado ADD COLUMN fami_ocup_padre text;

48. Crear el atributo fami_ocup_madre
>ALTER TABLE public.saberpro_transformado ADD COLUMN fami_ocup_madre text;

49. Actualizar los atributos fami_ocup_padre y fami_ocup_madre teniendo en cuenta los códigos de los atributos fami_cod_ocup_padre o fami_cod_ocup_madre
>update 	saberpro_transformado set 	fami_ocup_padre = 	case 	when 	fami_cod_ocup_padre = '13' then 'Empresario'
									when 	fami_cod_ocup_padre = '14' then 'Empresario'
									when 	fami_cod_ocup_padre = '15' then 'Empleado'
									when 	fami_cod_ocup_padre = '16' then 'Empleado'
									when 	fami_cod_ocup_padre = '17' then 'Empleado'
									when 	fami_cod_ocup_padre = '18' then 'Empleado'
									when 	fami_cod_ocup_padre = '19' then 'Obrero'
									when 	fami_cod_ocup_padre = '20' then 'Profesional'
									when 	fami_cod_ocup_padre = '21' then 'Independiente'
									when 	fami_cod_ocup_padre = '22' then 'Hogar'
									when 	fami_cod_ocup_padre = '23' then 'Pensionado'
									when 	fami_cod_ocup_padre = '24' then 'Independiente'
									when 	fami_cod_ocup_padre = '25' then 'Estudiante'
									when 	fami_cod_ocup_padre = '26' then 'Otra'
									when 	fami_cod_ocup_padre = '99' then 'No sabe'
							end;
 
 >update 	saberpro_transformado 
set 	fami_ocup_madre = 	case 	when 	fami_cod_ocup_madre = '13' then 'Empresario'
									when 	fami_cod_ocup_madre = '14' then 'Empresario'
									when 	fami_cod_ocup_madre = '15' then 'Empleado'
									when 	fami_cod_ocup_madre = '16' then 'Empleado'
									when 	fami_cod_ocup_madre = '17' then 'Empleado'
									when 	fami_cod_ocup_madre = '18' then 'Empleado'
									when 	fami_cod_ocup_madre = '19' then 'Obrero'
									when 	fami_cod_ocup_madre = '20' then 'Profesional'
									when 	fami_cod_ocup_madre = '21' then 'Independiente'
									when 	fami_cod_ocup_madre = '22' then 'Hogar'
									when 	fami_cod_ocup_madre = '23' then 'Pensionado'
									when 	fami_cod_ocup_madre = '24' then 'Independiente'
									when 	fami_cod_ocup_madre = '25' then 'Estudiante'
									when 	fami_cod_ocup_madre = '26' then 'Otra'
									when 	fami_cod_ocup_madre = '99' then 'No sabe'
							end;

50. Reemplazar los códigos del atributo fami_nivel_sisben por su descripción:
* TABLA
>update 	saberpro_transformado 
set 	fami_nivel_sisben = 	case 	when 	fami_nivel_sisben = '1' then 'Nivel 1'
										when 	fami_nivel_sisben = '2' then 'Nivel 2'
										when 	fami_nivel_sisben = '3' then 'Nivel 3'
										when 	fami_nivel_sisben = '4' then 'Otro nivel'
										when 	fami_nivel_sisben = '5' then 'Sin Nivel'
								end;

51. Crear el atributo eco_condicion_vive
>ALTER TABLE public.saberpro_transformado ADD COLUMN eco_condicion_vive text;

52. Actualizar el atributo eco_condicion_vive de acuerdo a los valores de los atributos infa_dormitorios y fami_num_pers_grup_fam y la fórmula para calcular el índice de hacinamiento:
* Se entiende por índice de hacinamiento a la relación:
* ihacinam. = (personas habtando una vivienda) / (número de dormitorios en la vivienda)
Generalmente se aceptan los valores:
* hasta 2.4 - sin hacinamiento;
* de 2.5 a 4.9 - hacinamiento medio;
* más de 4.9 - hacinamiento crítico.
>update 	saberpro_transformado set eco_condicion_vive = 	case 	when 	(fami_num_pers_grup_fam::int/infa_dormitorios::int) <= 2.4 then 'sin hacinamiento'
										when 	(fami_num_pers_grup_fam::int/infa_dormitorios::int) between 2.5 and 4.9  then 'hacinamiento medio'
										when 	(fami_num_pers_grup_fam::int/infa_dormitorios::int) > 4.9 then 'hacinamiento crítico'
								end;

53. Crear el atributo eco_condicion_vivienda 
>ALTER TABLE public.saberpro_transformado ADD COLUMN eco_condicion_vivienda text;

54. Actualizar el atributo eco_condicion_vivienda de acuerdo a la discretización del atributo econ_material_pisos de la siguiente tabla
* tabla
>update 	saberpro_transformado 
set 	eco_condicion_vivienda = 	case 	when econ_material_pisos in ('Tierra','Arena') then 'MALA' 
											when econ_material_pisos in ('Cemento', 'Gravilla', 'Ladrillo') then 'REGULAR' 
											when econ_material_pisos in ('Madera Burda', 'Tabla – Tablon') then 'REGULAR' 
											when econ_material_pisos in ('Madera Pulida', 'Baldosa', 'Tableta', 'Marmol', 'Alfombra') then 'BUENA' 
											when econ_material_pisos in ('Madera Pulida', 'Marmol', 'Alfombra - Tapete De Pared A Pared') then 'BUENA' 
									end;
                  
55. Reducir los valores del atributo econ_sn _computador, reemplazando los valores 2,3 y 4 por 1 
>update 	saberpro_transformado set	econ_sn_computador =  1 where econ_sn_computador in ('2,3','4') ;

56. Crear el atributo eco_condicion_tic
>ALTER TABLE public.saberpro_transformado ADD COLUMN eco_condicion_tic text;

58. Actualizar el atributo eco_condicion_tic teniendo en cuenta los valores de los atributos econ_sn_telefonia, econ_sn _celular, econ_sn_internet, econ_sn_servicio_tv y econ_sn _computador que forman este índice de acuerdo a la sumatoria de los valores de la siguiente tabla:
* Discretizando su valor asi:
* BUENA (4 y 5)
* REGULAR (2 y3)
* MALA (0,1)
>update 	saberpro_transformado set 	eco_condicion_tic = 	case 	when ( econ_sn_telefonia::int + econ_sn_celular::int + econ_sn_internet::int + econ_sn_servicio_tv::int + econ_sn_computador::int )  between 4 and 5 then 'BUENA' 
										when ( econ_sn_telefonia::int + econ_sn_celular::int + econ_sn_internet::int + econ_sn_servicio_tv::int + econ_sn_computador::int )  between 2 and 3 then 'REGULAR'  
										when ( econ_sn_telefonia::int::int + econ_sn_celular::int + econ_sn_internet::int + econ_sn_servicio_tv::int + econ_sn_computador::int )  between 0 and 1 then 'MALA' 
								end;

59. Crear el atributo eco_condicion_electrodomesticos
>ALTER TABLE public.saberpro_transformado ADD COLUMN eco_condicion_electrodomesticos text;

60. Actualizar el atributo eco_condicion_electrodomesticos teniendo en cuenta los atributos econ_ sn _dvd, econ_sn_lavadora, econ_sn _microondas, econ_sn_horno y econ_sn _nevera que forman este índice de acuerdo sumatoria de los valores de la siguiente tabla
* tabla
* Discretizando su valor asi:
* BUENA (4 y 5)
* REGULAR (2 y3)
* MALA (0,1)
>update 	saberpro_transformado set	eco_condicion_electrodomesticos = 	case 	when ( econ_sn_dvd::int + econ_sn_lavadora::int + econ_sn_microondas::int + econ_sn_horno::int + econ_sn_nevera::int )  between 4 and 5 then 'BUENA' 
													when ( econ_sn_dvd::int + econ_sn_lavadora::int + econ_sn_microondas::int + econ_sn_horno::int + econ_sn_nevera::int )  between 2 and 3 then 'REGULAR'  
													when ( econ_sn_dvd::int + econ_sn_lavadora::int + econ_sn_microondas::int + econ_sn_horno::int + econ_sn_nevera::int )  between 0 and 1 then 'MALA' 
											end;

61. Convertir los valores del atributo fami_ing_fmliar_mensual de códigos a descripción de acuerdo a la siguiente tabla
* tabla
>update 	saberpro_transformado set 	fami_ing_fmliar_mensual = 	case 	when fami_ing_fmliar_mensual::numeric = 1 then 'Menos de 1 SM' 
											when fami_ing_fmliar_mensual::numeric = 2 then 'Entre 1 y menos de 2 SM' 
											when fami_ing_fmliar_mensual::numeric = 3 then 'Entre 2 y menos de 3 SM'  
											when fami_ing_fmliar_mensual::numeric = 4 then 'Entre 3 y menos de 5 SM' 
											when fami_ing_fmliar_mensual::numeric = 5 then 'Entre 5 y menos de 7 SM' 
											when fami_ing_fmliar_mensual::numeric = 6 then 'Entre 7 y menos' 
											when fami_ing_fmliar_mensual::numeric = 7 then '10 -más SM'
									end;

62. Crear el atributo estu_sn_trabaja 
>ALTER TABLE public.saberpro_transformado ADD COLUMN estu_sn_trabaja text;

63. Actualizar el atributo estu_sn_trabaja a partir de los códigos del atributo estu_trabaja asi: 
* Si es 0 entonces ‘N’ sino ‘S’.
>update 	saberpro_transformado set	estu_sn_trabaja = case when estu_sn_trabaja = '0' then 'N' else 'S' end ;

64. Crear los atributos mod_lectura_critica_desemp, mod_comunica_escrita_desemp, mod_razona_cuantitativo_desemp , mod_ingles_desemp y mod_comp_ciudadanas_desemp
>ALTER TABLE public.saberpro_transformado ADD COLUMN mod_lectura_critica_desemp text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_comunica_escrita_desemp text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_razona_cuantitativo_desemp text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_ingles_desemp text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_comp_ciudadanas_desemp text;

65. Actualizar los atributos mod_lectura_critica_desemp, mod_comunica_escrita_desemp, mod_razona_cuantitativo_desemp , mod_ingles_desemp y mod_com y mod_comp_ciudadanas_desemp con los valores:
* SOBRE LA MEDIA (>=media de la respectiva competencia) y BAJO LA MEDIA (< media de la respectiva competencia).
>UPDATE saberpro_transformado SET mod_lectura_critica_desemp = (SELECT CASE WHEN mod_comunica_escrita_punt::numeric > (SELECT avg(mod_lectura_critica::numeric) FROM saberpro_transformado WHERE mod_lectura_critica <> 'NP')::numeric THEN 'SOBRE LA MEDIA' ELSE 'BAJO LA MEDIA' END )WHERE mod_comunica_escrita_punt <> 'NP' AND mod_comunica_escrita_punt <> 'NP';<br>
UPDATE saberpro_transformado SET mod_comunica_escrita_desemp = ( SELECT CASE WHEN mod_comunica_escrita_punt::numeric > (SELECT avg(mod_comunica_escrita_punt::numeric) FROM saberpro_transformado WHERE mod_comunica_escrita_punt <> 'NP')::numeric THEN 'SOBRE LA MEDIA' ELSE 'BAJO LA MEDIA' END ) WHERE mod_comunica_escrita_punt <> 'NP';	<br>
UPDATE saberpro_transformado SET mod_razona_cuantitativo_desemp = (SELECT CASE WHEN mod_razona_cuantitativo_punt::numeric > (SELECT avg(mod_razona_cuantitativo_punt::numeric) FROM saberpro_transformado WHERE mod_razona_cuantitativo_punt <> 'NP')::numeric THEN 'SOBRE LA MEDIA' ELSE 'BAJO LA MEDIA' END ) WHERE mod_razona_cuantitativo_punt <> 'NP';<br>
UPDATE saberpro_transformado SET  mod_ingles_desemp = ( SELECT CASE  WHEN mod_ingles_punt::numeric > (SELECT avg(mod_ingles_punt::numeric) FROM saberpro_transformado WHERE mod_ingles_punt <> 'NP')::numeric THEN 'SOBRE LA MEDIA' ELSE 'BAJO LA MEDIA' END ) WHERE mod_ingles_punt <> 'NP';<br>
UPDATE saberpro_transformado SET mod_comp_ciudadanas_desemp = (SELECT CASE WHEN mod_comp_ciudadanas_punt::numeric > (SELECT avg(mod_comp_ciudadanas_punt::numeric) FROM saberpro_transformado WHERE mod_comp_ciudadanas_punt <> 'NP' AND mod_comp_ciudadanas_punt <> 'NA')::numeric THEN 'SOBRE LA MEDIA' ELSE 'BAJO LA MEDIA' END) WHERE mod_comp_ciudadanas_punt <> 'NP' AND mod_comp_ciudadanas_punt <> 'NA';

66. Crear los atributos mod_sn_lectura_critica, mod_sn_comunica_escrita, mod_sn_razona_cuantitativo, mod_sn_ingles y mod_sn_comp_ciudadanas69. 
>ALTER TABLE public.saberpro_transformado ADD COLUMN mod_sn_lectura_critica text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_sn_comunica_escrita text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_sn_razona_cuantitativo text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_sn_ingles text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN mod_sn_comp_ciudadanas text;

67. Actualizar los atributos mod_sn_lectura_critica, mod_sn_comunica_escrita, mod_sn_razona_cuantitativo, mod_sn_ingles y mod_sn_comp_ciudadanas con el valor ‘S’ si presento el módulo y ‘N’ sino presento.
>update 	saberpro_transformado set mod_sn_lectura_critica = case when mod_sn_lectura_critica is null then 'N' else 'S' end ;<br>
update 	saberpro_transformado set mod_sn_comunica_escrita = case when mod_sn_comunica_escrita is null then 'N' else 'S' end ;<br>
update 	saberpro_transformado set mod_sn_razona_cuantitativo = case when mod_sn_razona_cuantitativo is null then 'N' else 'S' end ;<br>
update 	saberpro_transformado set mod_sn_ingles = case when mod_sn_ingles is null then 'N' else 'S' end ;<br>
update 	saberpro_transformado set mod_sn_comp_ciudadanas = case when mod_sn_comp_ciudadanas is null then 'N' else 'S' end ;

68. Crear los atributos semestre_prue y ano_prue
>ALTER TABLE public.saberpro_transformado ADD COLUMN semestre_prue text;<br>
ALTER TABLE public.saberpro_transformado ADD COLUMN ano_prue text;

69. Actualizar los atributos semestre_prue y ano_prue a partir del atributo prueba
>update 	saberpro_transformado set	ano_prue = substring( prueba from 1 for 4) ;<br>
update 	saberpro_transformado set	semestre_prue = substring( prueba from 4 for 5) ;
