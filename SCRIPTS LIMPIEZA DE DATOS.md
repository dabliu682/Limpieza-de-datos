### LIMPIEZA DE DATOS

1. Reemplazar los valores ‘EK20123’,EK20133’,’EK20142’,’EK20143 y ‘EKO2014’ del atributo estu_cod_aplicacion por ‘EK20122’,’EK20132’,’EK20141’,EK20142’ y EK20141 respectivamente:
>Update saberpro_limpio
Set estu_cod_aplicacion =
(case 
when estu_cod_aplicacion = 'EK20123' then 'EK20122'
when estu_cod_aplicacion = 'EK20133' then 'EK20132'
when estu_cod_aplicacion = 'EK20142' then 'EK20141'
when estu_cod_aplicacion = 'EK20143' then 'EK20142'
when estu_cod_aplicacion = 'EKO2014' then 'EK20141'
else estu_cod_aplicacion
end)
Where estu_cod_aplicacion in ('EK20123','EK20133','EK20142','EK20143' ,'EKO2014');

2. Reemplazar los valores ‘20123’,20133’,’20142’,’20143 y ‘O2014’ del atributo prueba por ‘20122’,’20132’,’20141’,20142’ y 20141 respectivamente:
>Update saberpro_limpio
Set prueba =
(case 
when prueba = '20123' then '20122'
when prueba = '20133' then '20132'
when prueba = '20142' then '20141'
when prueba = '20143' then '20142'
when prueba = 'O2014' then '20141' 
else prueba
end);

3. Reemplazar los valores nulos del atributo estu_genero por ‘SIN DATO’: 
>Update saberpro_limpio
Set estu_genero='SIN DATO'
Where (estu_genero is null or estu_genero = '');
4. Reemplazar los valores nulos del atributo estu_nacimiento_dia por la moda de este atributo en la tabla saberpro_2011_2014.
>Update saberpro_limpio
Set estu_nacimiento_dia='31'
Where (estu_nacimiento_dia is null or estu_nacimiento_dia = '');
5. Reemplazar el valor ‘5’ del atributo estu_nacimiento_dia por ‘05’
>Update saberpro_limpio
Set estu_nacimiento_dia='05'
Where estu_nacimiento_dia = '5';
6. Reemplazar los valores nulos del atributo estu_nacimiento_mes por la moda de este atributo en la tabla saberpro_2011_2014.
>Set estu_nacimiento_mes='02'
Where (estu_nacimiento_mes is null or estu_nacimiento_mes = '');
7. Reemplazar los valores nulos del atributo estu_nacimiento_anno por la diferencia entre el año de la prueba menos la moda de este atributo para las pruebas 20112, 20121, 20122, 20132,20131, 20141 y 20142:
>Update saberpro_limpio 
Set estu_nacimiento_anno = cast(substr(prueba,1,4) as numeric) -22 
Where prueba in ('20112','20121','20122','20132') and 
(estu_nacimiento_anno is null or estu_nacimiento_anno = '');

>Update saberpro_limpio 
Set estu_nacimiento_anno=cast(substr(prueba,1,4) as numeric)-23 
Where prueba in ('20131','20141','20142') and 
( estu_nacimiento_anno is null or estu_nacimiento_anno = '');
8. Reemplazar los valores nulos del atributo estu_pais_reside por ‘COLOMBIA’
>Update saberpro_limpio
Set estu_pais_reside='COLOMBIA'
Where (estu_pais_reside is null or estu_pais_reside = '');
9. Reemplazar los valores ‘CO’ del atributo estu_pais_reside por ‘COLOMBIA’
>Update saberpro_limpio
Set estu_pais_reside='COLOMBIA'
Where estu_pais_reside ='CO';

10. Reemplazar los valores nulos del atributo estu_reside_codmpio por los valores del atributo estu_exam_codmpio_presentacion.
>Update saberpro_limpio
Set estu_reside_codmpio=estu_exam_codmpio_presentacion
Where (estu_reside_codmpio is null or estu_reside_codmpio = '');

11. Estandarizar el valor del atributo estu_exam_mpio_presentacion de “BOGOTÁ D.C.” por el valor “BOGOTA D.C”.
>Update saberpro_limpio
Set estu_exam_mpio_presentacion='BOGOTA'
Where estu_exam_mpio_presentacion like 'BOGOT%';

12. Estandarizar el valor del atributo estu_exam_dpto_presentacion de “BOGOTÁ” por el valor BOGOTA, "BOYACÁ" por BOYACA, CAQUETÁ por CAQUETA, "ATLÁNTICO" por ATLANTICO, “CHOCÓ” por CHOCO, “CÓRDOBA” por CORDOBA,”SAN ANDRÉS” por SAN ANDRES, “VAUPÉS” por VAUPES, “QUINDÍO” por QUINDIO, “GUAINÍA” por GUANIA,”BOLÍVAR” por BOLIVAR.
>Update saberpro_limpio
Set estu_exam_dpto_presentacion =
(case 
when estu_exam_dpto_presentacion like 'BOGOT%' then 'BOGOTA'
when estu_exam_dpto_presentacion like 'BOYAC%' then 'BOYACA'
when estu_exam_dpto_presentacion like 'CAQUET%' then 'CAQUETA'
when estu_exam_dpto_presentacion like 'ATL_NTICO%' then 'ATLANTICO'
when estu_exam_dpto_presentacion like 'CHOC%' then 'CHOCO' 
when estu_exam_dpto_presentacion like 'C_RDOBA%' then 'CORDOBA'
when estu_exam_dpto_presentacion like 'SAN ANDR_S%' then 'SAN ANDRES'
when estu_exam_dpto_presentacion like 'VAUP_S%' then 'VAUPES'
when estu_exam_dpto_presentacion like 'QUIND_O%' then 'QUINDIO'
when estu_exam_dpto_presentacion like 'GUAIN_A%' then 'GUAINIA'
when estu_exam_dpto_presentacion like 'BOL_VAR%' then 'BOLIVAR'
--when estu_exam_dpto_presentacion like 'BOL_VAR' then 'BOLIVAR'
else estu_exam_dpto_presentacion
end);

13. Reemplazar los valores nulos del atributo estu_exam_cod por 141 para la prueba 20141 y por 142 para la prueba 20142.
>Update saberpro_limpio
Set estu_exam_cod =
(case 
when prueba='20141' then '141'
when prueba='20142' then '142'
else estu_exam_cod
end)
Where (estu_exam_cod is null or estu_exam_cod = '');

14. Reemplazar los valores nulos del atributo estu_exam_nombre por EXAMEN SABERPRO 2014-1 para la prueba 20141 y por EXAMEN SABER PRO 2014-2 para la prueba 20142.
>Update saberpro_limpio
Set estu_exam_nombre =
(case 
when prueba='20141' then 'EXAMEN SABER PRO 2014-1'
when prueba='20142' then 'EXAMEN SABER PRO 2014-2'
end)
Where (estu_exam_nombre is null or estu_exam_nombre = '');

15. Reemplazar los valores nulos del atributo inst_origen por el código ‘4’ para las instituciones o escuelas normal superior
>Update saberpro_limpio 
Set inst_origen='4' 
Where inst_nombre_institucion like '%NORMAL%' and 
(inst_origen is null or inst_origen = '');

16. Reemplazar los valores nulos del atributo inst_origen por los valores no nulos del atributo inst_origen en los casos de las instituciones que tienen el mismo código de 
institución inst_cod_institucion
>Update saberpro_limpio
Set inst_origen=
(Select t2.inst_origen 
From saberpro_2011_2014 t2
Where t2.inst_origen is not null and 
t2.inst_origen <>'' and 
inst_cod_institucion=t2.inst_cod_institucion 
limit 1)
Where (inst_origen is null or inst_origen = '');

17. Reemplazar los valores del atributo inst_origen por el código ‘5’ para la "ESCUELA NORMAL SUPERIOR ANTIOQUEÑA con código 4.
>Update saberpro_limpio 
Set inst_origen='5' 
Where inst_origen='4' and inst_nombre_institucion like '%ANTIOQUEÑA%';

18. Reemplazar los valores numéricos del atributo inst_origen por su descripción de acuerdo a la siguiente tabla:<br>

* hola<br>
>Update saberpro_limpio
Set inst_origen=
case 
when  inst_origen='1' then 'OFICIAL NACIONAL'
when  inst_origen='2' then 'OFICIAL DEPARTAMENTAL'
when  inst_origen='3' then 'OFICIAL MUNICIPAL'
when  inst_origen='4' then 'OFICIAL(NORMALES)'
when  inst_origen='5' then 'NO OFICIAL(NORMALES)'
when  inst_origen='7' then 'NO OFICIAL-FUNDACION'
when  inst_origen='8' then 'NO OFICIAL-CORPORACION'
when  inst_origen='9' then 'REGIMEN ESPECIAL'
else inst_origen
end;<br>

19. Estandarizar los valores del atributo inst_origen, para aquellos casos en los que existen tildes: 'NO OFICIAL - FUNDACIÓN', 'NO OFICIAL - CORPORACIÓN' y 'RÉGIMEN ESPECIAL’:
>Update saberpro_limpio
Set inst_origen=
case
when inst_origen='RÉGIMEN ESPECIAL' then 'REGIMEN ESPECIAL'
when inst_origen='NO OFICIAL - CORPORACIÓN' then 'NO OFICIAL - CORPORACION'
when inst_origen='NO OFICIAL - FUNDACIÓN' then 'NO OFICIAL - FUNDACION'
when inst_origen='NO OFICIAL-CORPORACION' then 'NO OFICIAL - CORPORACION'
when inst_origen='NO OFICIAL-FUNDACION' then 'NO OFICIAL - FUNDACION'
else inst_origen
end;

20. Reemplazar los valores nulos del atributo inst_caracter_academico por los valores no nulos del atributo inst_caracter_academico en los casos de las instituciones que tienen el mismo código de institución inst_cod_institucion
>Update saberpro_limpio t1 
Set inst_caracter_academico =
(Select t2.inst_caracter_academico 
From saberpro_2011_2014 t2 
Where t2.inst_caracter_academico is not null and
t2.inst_caracter_academico <> '' and 
t1.inst_cod_institucion=t2.inst_cod_institucion 
limit 1)
Where (inst_caracter_academico is null or inst_caracter_academico = '');

21. Reemplazar los valores nulos del atributo estu_nivel_prgm_academico por el valor no nulo del atributo estu_nivel_prgm_academico de los programas iguales de la  misma institución
>Update saberpro_limpio t1
Set estu_nivel_prgm_academico =
(Select distinct t2.estu_nivel_prgm_academico
From saberpro_2011_2014 t2
Where t2.inst_cod_institucion=t1.inst_cod_institucion and
t2.estu_prgm_academico=t1.estu_prgm_academico and
(t2.estu_nivel_prgm_academico is not null and t2.estu_nivel_prgm_academico <> '')
limit 1)
where (t1.estu_nivel_prgm_academico is null or t1.estu_nivel_prgm_academico = '');

22. Reemplazar los valores nulos del atributo estu_nivel_prgm_academico por “UNIVERSITARIA” para aquellas instituciones cuyo nombre inst_nombre_institucion inicie con “UNIVERSIDAD”
>Update saberpro_limpio
Set estu_nivel_prgm_academico = 'UNIVERSITARIA'
Where inst_nombre_institucion like 'UNIVERSIDAD%'
and (estu_nivel_prgm_academico is null or estu_nivel_prgm_academico = '');

23. Reemplazar los valores nulos del atributo estu_nivel_prgm_academico por “UNIVERSITARIA” para aquellos programas cuyo nombre estu_prgm_academico contengan las palabras INGENIERIA, DERECHO, MEDICINA, ODONTOLOGIA, CONTADURIA,LICENCIATURA,PSICOLOGIA ARQUITECTURA, ECOLOGIA, FISIOTERAPIA, ZOOTECNIA, ADMINISTRACIÓN, DISEÑO, SOCIAL, PUBLICIDAD, INTERNACIONAL, ARTES, PERIODISMO, GASTRONOMÍA, CIENCIA, TERAPIA, SALUD 
>select count(*) from saberpro_limpio Where estu_nivel_prgm_academico is null and
(estu_prgm_academico like '%INGENIERIA%' or
estu_prgm_academico like '%DERECHO%' or
estu_prgm_academico like '%MEDICINA%' or
estu_prgm_academico like '%ODONTOLOGIA%' or
estu_prgm_academico like '%CONTADURIA%' or
estu_prgm_academico like '%LICENCIATURA%' or
estu_prgm_academico like '%PSICOLOGIA%' or
estu_prgm_academico like '%ARQUITECTURA%' or
estu_prgm_academico like '%ECOLOGIA%' or
estu_prgm_academico like '%FISIOTERAPIA%' or
estu_prgm_academico like '%ZOOTECNIA%' or
estu_prgm_academico like '%ADMINISTRACI%' or
estu_prgm_academico like '%DISEÑO%' or
estu_prgm_academico like '%SOCIAL%' or
estu_prgm_academico like '%PUBLICIDAD%' or
estu_prgm_academico like '%INTERNACIONAL%' or
estu_prgm_academico like '%ARTES%' or
estu_prgm_academico like '%PERIODISMO%' or
estu_prgm_academico like '%GASTRON%' or
estu_prgm_academico like '%CIENCIA%' or
estu_prgm_academico like '%TERAPIA%' or
estu_prgm_academico like '%SALUD%');

>Update saberpro_limpio
Set estu_nivel_prgm_academico =
case
when estu_prgm_academico like '%INGENIERIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%DERECHO%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%MEDICINA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%ODONTOLOGIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%CONTADURIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%LICENCIATURA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%PSICOLOGIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%ARQUITECTURA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%ECOLOGIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%FISIOTERAPIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%ZOOTECNIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%ADMINISTRACI%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%DISEÑO%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%SOCIAL%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%PUBLICIDAD%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%INTERNACIONAL%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%ARTES%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%PERIODISMO%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%GASTRON%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%CIENCIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%TERAPIA%' then 'UNIVERSITARIA'
when estu_prgm_academico like '%SALUD%' then 'UNIVERSITARIA'
end
Where (estu_nivel_prgm_academico is null or estu_nivel_prgm_academico = '');

24. Reemplazar los valores nulos del atributo estu_metodo_prgm por el valor no nulo del atributo estu_metodo_prgm de la institución con igual código(inst_cod_institucion) o nombre (inst_nombre_institucion), y de los programas del mismo código(estu_prac_id_prgrm_academico) o nombre (estu_prgm_academico)
>Update saberpro_limpio t1
Set estu_metodo_prgm =
(Select t2.estu_metodo_prgm 
From saberpro_2011_2014 t2
Where t2.inst_cod_institucion=t1.inst_cod_institucion and
t2.estu_prac_id_prgrm_academico=t1.estu_prac_id_prgrm_academico and
t2.estu_metodo_prgm <>'' 
limit 1)
Where estu_metodo_prgm ='';

25. Reemplazar los 2 restantes valores nulos del atributo estu_metodo_prgm por la moda ‘PRESENCIAL’
>Update saberpro_limpio
Set estu_metodo_prgm='PRESENCIAL'
Where estu_metodo_prgm ='' or estu_metodo_prgm is null;

26. Estandarizar los valores del atributo estu_metodo_prgm en mayúsculas;
>Update saberpro_limpio
Set estu_metodo_prgm=upper(estu_metodo_prgm);

27. Reemplazar los valores nulos del atributo dipo_codigomunicipio por los valores del  atributo estu_exam_codmpio_presentacion:
>Update saberpro_limpio
Set dipo_codigomunicipio=estu_exam_codmpio_presentacion
Where (dipo_codigomunicipio is null or dipo_codigomunicipio = '');

28. Reemplazar los valores nulos del atributo inst_cod_jornada por la moda “1” para los nombres de instituciones que contengan la palabra ‘NORMAL’.
>Update saberpro_limpio
Set inst_cod_jornada='1'
Where (inst_cod_jornada is null or inst_cod_jornada = '' ) and
inst_nombre_institucion like '%NORMAL%';

29. Reemplazar los valores nulos del atributo inst_cod_jornada por la moda del resto de instituciones que es ‘12’
>Update saberpro_limpio
Set inst_cod_jornada='12'
Where (inst_cod_jornada is null or inst_cod_jornada = '');

30. Reemplazar los valores nulos del atributo estu_area_conoc de saberpro_limpio, por el valor no nulo del atributo estu_area_conoc de los programas del mismo nombre (estu_prgm_academico) de la tabla saberpro_2011_2014
>Update saberpro_limpio t1
Set estu_area_conoc=
(Select t2.estu_area_conoc 
From saberpro_2011_2014 t2
Where t2.estu_area_conoc <> '' and
t1.estu_prgm_academico=t2.estu_prgm_academico 
limit 1)
Where estu_area_conoc ='';

31. Reemplazar los valores nulos del atributo estu_nucleo_pregrado de saberpro_limpio, por el valor no nulo del atributo estu_nucleo_pregrado de los programas del mismo  nombre (estu_prgm_academico) de la tabla saberpro_2011_2014
>Update saberpro_limpio t1
Set estu_nucleo_pregrado =
(Select t2.estu_nucleo_pregrado 
From saberpro_2011_2014 t2
Where t2.estu_nucleo_pregrado is not null and
t2.estu_nucleo_pregrado <> '' and
t1.estu_prgm_academico=t2.estu_prgm_academico 
limit 1)
Where (estu_nucleo_pregrado is null = estu_nucleo_pregrado='');

32. Reemplazar los valores nulos del atributo estu_cod_grupo_ref de saberpro_limpio, por el valor no nulo del atributo estu_cod_grupo_ref de los grupos de referencia con  el nombre (estu_grupo_referencia) de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set estu_cod_grupo_ref =
(Select t1. estu_cod_grupo_ref
From saberpro_2011_2014 t1
Where estu_grupo_referencia =t1. estu_grupo_referencia
and (t1.estu_cod_grupo_ref is not null and t1.estu_cod_grupo_ref <> '') 
limit 1)
Where (estu_cod_grupo_ref is null or estu_cod_grupo_ref = '');

33. Actualizar en la tabla saberpro_limpio, el atributo estu_cod_grupo_ref utilizando en algunos casos caracteres comodines “%” y “_” asi: (utilice select case when) BELLAS ARTES Y DISEÑO por el código 1, CIENCIAS NATURALES Y EXACTAS por el código 2, CIENCIAS SOCIALES por el código 3,HUMANIDADES por el código 4, DERECHO por el código 5, COMUNICACI_N, PERIODISMO Y PUBLICIDAD por el código 6, CIENCIAS MILITARES Y NAVALES por el código 7, %CIENCIAS AGROPECUARIAS% por el código 8, %ADMINISTRACI_N% por el código 9, EDUCACI_N por el código 10, ARQUITECTURA Y URBANISMO por el código 11, INGENIER_A por el código 12, %SALUD% por el código 13, MEDICINA por el código 14, %INGENIER_A, INDUSTRIA Y MINAS% por el código 15, %TIC% por el código 17, %ARTES - DISEÑO – COMUNICACI_N% por el código 19, %CIENCIAS AGROPECUARIAS% por el código 20, NORMALES SUPERIORES por el código 27, %JUDICIAL% por el código 28, %MILITAR Y POLICIAL% por el código 29, RECREACI_N Y DEPORTES por el código 30, %ECONOM% por el código 31, %CONTADUR_A% por el código 32, PSICOLOG_A por el código 33, ENFERMER_A por el código 34, GRUPO REFERENCIA NACIONAL% por el código 42;
>Update saberpro_limpio
Set estu_cod_grupo_ref=
case
when estu_prgm_academico like 'BELLAS ARTES Y DISEÑO' then '1'
when estu_prgm_academico like 'CIENCIAS NATURALES Y EXACTAS' then '2'
when estu_prgm_academico like 'CIENCIAS SOCIALES' then '3'
when estu_prgm_academico like 'HUMANIDADES' then '4'
when estu_prgm_academico like 'DERECHO' then '5'
when estu_prgm_academico like 'COMUNICACI_N' then '6'
when estu_prgm_academico like 'PERIODISMO' then '6'
when estu_prgm_academico like 'PUBLICIDAD' then '6'
when estu_prgm_academico like 'CIENCIAS MILITARES' then '7'
when estu_prgm_academico like 'NAVALES' then '7'
when estu_prgm_academico like '%CIENCIAS AGROPECUARIAS%' then '8'
when estu_prgm_academico like '%ADMINISTRACI_N%' then '9'
when estu_prgm_academico like 'EDUCACI_N' then '10'
when estu_prgm_academico like 'ARQUITECTURA' then '11'
when estu_prgm_academico like 'URBANISMO' then '11'
when estu_prgm_academico like 'INGENIER_A' then '12'
when estu_prgm_academico like '%SALUD%' then '13'
when estu_prgm_academico like 'MEDICINA' then '14'
when estu_prgm_academico like '%INGENIER_A' then '15'
when estu_prgm_academico like 'INDUSTRIA' then '15'
when estu_prgm_academico like 'MINAS%' then '15'
when estu_prgm_academico like '%TIC%' then '17'
when estu_prgm_academico like '%ARTES%' then '19'
when estu_prgm_academico like '%DISEÑO%' then '19'
when estu_prgm_academico like '%COMUNICACI_N%' then '19'
when estu_prgm_academico like '%CIENCIAS AGROPECUARIAS%' then '20'
when estu_prgm_academico like 'NORMALES SUPERIORES' then '27'
when estu_prgm_academico like '%JUDICIAL%' then '28'
when estu_prgm_academico like '%MILITAR Y POLICIAL%' then '29'
when estu_prgm_academico like 'RECREACI_N Y DEPORTES' then '30'
when estu_prgm_academico like '%ECONOM%' then '31'
when estu_prgm_academico like '%CONTADUR_A%' then '32'
when estu_prgm_academico like 'PSICOLOG_A' then '33'
when estu_prgm_academico like 'ENFERMER_A' then '34'
when estu_prgm_academico like 'GRUPO REFERENCIA NACIONAL%' then '42'
end;

34. Reemplazar los nulos del atributo estu_semestre_cursa por la moda (de las NORMALES) del atributo estu_semestre_cursa de la tabla saberpro_2011_2014, para los nombres de instituciones que contengan la palabra ‘NORMAL’.
>>Update saberpro_limpio
Set estu_semestre_cursa='99'
Where (estu_semestre_cursa is null or estu_semestre_cursa = '' ) and
inst_nombre_institucion like '%NORMAL%';

35. Reemplazar los valores nulos del atributo estu_semestre_cursa de saberpro_limpio, por el valor no nulo del atributo estu_semestre_cursa de la tabla saberpro_2011_2014 de igual instituciones con los mismos programas
>Update saberpro_limpio t1
Set estu_semestre_cursa=
(Select t2.estu_semestre_cursa 
From saberpro_2011_2014 t2
Where (t2.estu_semestre_cursa is not null and estu_semestre_cursa <> '') and
t1.inst_cod_institucion=t2.inst_cod_institucion and
t1.estu_prgm_academico=t2.estu_prgm_academico
limit 1)
Where (estu_semestre_cursa is null or estu_semestre_cursa = '');

36. Reemplazar los nulos del atributo estu_pje_creditos por el código ‘0’ para aquellas instituciones cuyo valor del atributo estu_nivel_prgm_academico es ‘NORMALISTA’ o el nombre de la institución del atributo inst_nombre_institucion contiene la sigla SENA.
>Update saberpro_limpio
Set estu_pje_creditos='0'
Where (estu_nivel_prgm_academico like 'NORMALISTA' or inst_nombre_institucion like '%SENA%')
and (estu_pje_creditos is null or estu_pje_creditos = '');

37. Reemplazar los valores nulos del atributo estu_pje_creditos por el valor no nulo del atributo estu_pje_creditos de la institución con igual código (inst_cod_institucion) o nombre (inst_nombre_institucion), y de los programas del mismo código(estu_prac_id_prgrm_academico) o nombre (estu_prgm_academico)
>Update saberpro_limpio t1
Set estu_pje_creditos=
(Select t2.estu_pje_creditos 
From saberpro_2011_2014 t2
Where (t1.inst_cod_institucion=t2.inst_cod_institucion or t1.inst_nombre_institucion=t2.inst_nombre_institucion) and
(t1.estu_prac_id_prgrm_academico=t2.estu_prac_id_prgrm_academico or t1.estu_prgm_academico=t2.estu_prgm_academico) and 
(t2.estu_pje_creditos is not null and t2.estu_pje_creditos <> '') 
limit 1)
Where (estu_pje_creditos is null or estu_pje_creditos = '');

38. Reemplazar los valores nulos del atributo inst_vlr_matricula_ant por la moda (de las NORMALES) del atributo inst_vlr_matricula_ant de la tabla saberpro_2011_2014, para los nombres de instituciones que contengan la palabra ‘NORMAL’.
>Update saberpro_limpio
Set inst_vlr_matricula_ant='2'
Where inst_nombre_institucion like '%NORMAL%' and
(inst_vlr_matricula_ant is null or inst_vlr_matricula_ant = '');

39. Reemplazar los valores nulos del atributo inst_vlr_matricula_ant de saberpro_limpio, por el valor no nulo del atributo inst_vlr_matricula_ant de la tabla saberpro_2011_2014 de igual instituciones con los mismos programas
>Update saberpro_limpio t1
Set inst_vlr_matricula_ant=
(Select t2.inst_vlr_matricula_ant 
From saberpro_2011_2014 t2
Where (t2.inst_vlr_matricula_ant is not null and t2.inst_vlr_matricula_ant <> '') and
t1.inst_cod_institucion=t2.inst_cod_institucion and
t1.estu_prac_id_prgrm_academico=t2.estu_prac_id_prgrm_academico 
limit 1)
Where (inst_vlr_matricula_ant is null or  inst_vlr_matricula_ant = '');

40. Reemplazar los valores nulos del atributo estu_titulo_bto por la moda (de las NORMALES) del atributo estu_titulo_bto de la tabla saberpro_2011_2014, para los nombres de instituciones que contengan la palabra ‘NORMAL’.
>Update saberpro_limpio
Set estu_titulo_bto='N'
Where inst_nombre_institucion like '%NORMAL%' and
(estu_titulo_bto is null or estu_titulo_bto = '');

41. Reemplazar los valores nulos del atributo estu_titulo_bto al resto de instituciones por la moda del atributo estu_titulo_bto de la tabla saberpro_2011_2014 
>Update saberpro_limpio
Set estu_titulo_bto='N'
Where inst_nombre_institucion not like '%NORMAL%' and
(estu_titulo_bto is null or estu_titulo_bto = '');

42. Reemplazar los valores nulos del atributo estu_hogar_actual por la moda del atributo estu_hogar_actual de la tabla saberpro_2011_2014 
>Update saberpro_limpio t1
Set estu_hogar_actual='1'
Where (estu_hogar_actual is null or estu_hogar_actual = '');

43. Reemplazar los valores nulos del atributo fami_num_pers_grup_fam por la media (redondeada a entera) de los valores no nulos de fami_num_pers_grup_fam de la tabla saberpro_2011_2014:
>Update saberpro_limpio
Set fami_num_pers_grup_fam =
(Select cast(round(avg( cast(fami_num_pers_grup_fam as numeric)),0) as text)
From saberpro_2011_2014
Where (fami_num_pers_grup_fam is null or fami_num_pers_grup_fam = ''))
Where (fami_num_pers_grup_fam is null or fami_num_pers_grup_fam = '');

44. Reemplazar los valores nulos del atributo estu_sn_cabeza_fmlia por la moda del atributo estu_sn_cabeza_fmlia de la tabla saberpro_2011_2014.
>Update saberpro_limpio
Set estu_sn_cabeza_fmlia='0'
Where (estu_sn_cabeza_fmlia is null or estu_sn_cabeza_fmlia = '');

45. Reemplazar los valores nulos del atributo fami_num_pers_cargo por la media (redondeada a entera) de los valores no nulos de fami_num_pers_cargo de la tabla saberpro_2011_2014;
>Update saberpro_limpio
Set fami_num_pers_cargo=
(Select round(avg(fami_num_pers_cargo::numeric),0) 
From saberpro_2011_2014
Where (fami_num_pers_cargo is null or fami_num_pers_cargo = '')
)
Where (fami_num_pers_cargo is null or fami_num_pers_cargo = '');

46. Reemplazar los valores nulos del atributo fami_cod_educa_padre por el código ‘99’
>Update saberpro_limpio
Set fami_cod_educa_padre='99'
Where (fami_cod_educa_padre is null or fami_cod_educa_padre = '');

47. Reemplazar los valores 1,2,3,4,5,6,7,8 del atributo fami_cod_educa_padre por el código ‘9’
>Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='1';
Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='2';
Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='3';
Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='4';
Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='5';
Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='6';
Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='7';
Update saberpro_limpio
Set fami_cod_educa_padre='9'
Where fami_cod_educa_padre='8';

48. Reemplazar los valores nulos del atributo fami_cod_educa_madre por el código ‘99’
>Update saberpro_limpio
Set fami_cod_educa_madre='99'
Where (fami_cod_educa_madre is null or fami_cod_educa_madre = '');

49. Reemplazar los valores 1,2,3,4,5,6,7,8 del atributo fami_cod_educa_madre por el código ‘9’
>Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='1';
Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='2';
Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='3';
Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='4';
Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='5';
Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='6';
Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='7';
Update saberpro_limpio
Set fami_cod_educa_madre='9'
Where fami_cod_educa_madre='8';

50. Reemplazar los valores nulos del atributo fami_cod_ocup_madre por el código ‘99’
>Update saberpro_limpio
Set fami_cod_ocup_madre='99'
Where (fami_cod_ocup_madre is null or fami_cod_ocup_madre  = '');

51. Reemplazar los valores 01,02,03,04,05,06,07,08,09,10,11,12 del atributo fami_cod_ocup_madre por la moda del atributo fami_cod_ocup_madre de la tabla  saberpro_2011_2014
>Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='01';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='02';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='03';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='04';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='05';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='06';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='07';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='08';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='09';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='10';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='11';
Update saberpro_limpio
Set fami_cod_ocup_madre='22'
Where fami_cod_ocup_madre='12';

52. Reemplazar los valores nulos del atributo estu_estrato por la moda del atributo estu_estrato de la tabla saberpro_2011_2014 
>Update saberpro_limpio
Set estu_estrato='3'
Where (estu_estrato is null or estu_estrato = '');

53. Reemplazar los valores nulos del atributo fami_nivel_sisben por la moda del atributo fami_nivel_sisben de la tabla saberpro_2011_2014
>Update saberpro_limpio
Set fami_nivel_sisben='5'
Where (fami_nivel_sisben is null or fami_nivel_sisben = '');

54. Reemplazar los valores nulos del atributo econ_material_pisos por la moda del atributo econ_material_pisos de la tabla saberpro_2011_2014
>Update saberpro_limpio
Set econ_material_pisos='4'
Where (econ_material_pisos is null or econ_material_pisos = '');

55. Reemplazar los valores nulos del atributo econ_sn_telefonia por la moda del atributo econ_sn_telefonia de la tabla saberpro_2011_2014 
>Update saberpro_limpio
Set econ_sn_telefonia='1'
Where (econ_sn_telefonia is null or econ_sn_telefonia = '');

56. Reemplazar los valores nulos del atributo econ_sn_internet por la moda del atributo econ_sn_internet de la tabla saberpro_2011_2014
Update saberpro_limpio
Set econ_sn_internet='1'
Where (econ_sn_internet is null or econ_sn_internet = '');

57. Reemplazar los valores nulos del atributo econ_sn_servicio_tv por la moda del atributo econ_sn_servicio_tv de la tabla saberpro_2011_2014
>Update saberpro_limpio
Set econ_sn_servicio_tv='1'
Where (econ_sn_servicio_tv is null or econ_sn_servicio_tv ='');

58. Reemplazar los valores nulos del atributo econ_sn_computador por la moda del atributo econ_sn_computador de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set econ_sn_computador=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_computador
ORDER BY econ_sn_computador DESC
Limit 1)
Where (econ_sn_computador is null or econ_sn_computador = '');

59. Reemplazar los valores nulos del atributo econ_sn_celular y los de econ_sn_celular código 2 por la moda del atributo econ_sn_celular de la tabla saberpro_2011_2014.
>Update saberpro_limpio 
Set econ_sn_celular=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_celular
ORDER BY econ_sn_celular DESC
Limit 1)
Where (econ_sn_celular is null or econ_sn_celular = '');

>Update saberpro_limpio 
Set econ_sn_celular=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_celular
ORDER BY econ_sn_celular DESC
Limit 1)
Where econ_sn_celular ='2';


60. Reemplazar los valores nulos del atributo econ_sn_dvd y los de econ_sn_dvd código 2 por la moda del atributo econ_sn_dvd de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set econ_sn_dvd=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_dvd
ORDER BY econ_sn_dvd DESC
Limit 1)
Where (econ_sn_dvd is null or econ_sn_dvd = '');

>Update saberpro_limpio 
Set econ_sn_dvd=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_dvd
ORDER BY econ_sn_dvd DESC
Limit 1)
Where econ_sn_dvd ='2';

61. Reemplazar los valores nulos del atributo econ_sn_lavadora por la moda del atributo econ_sn_lavadora de la tabla saberpro_2011_2014 
>Update saberpro_limpio 
Set econ_sn_lavadora=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_lavadora
ORDER BY econ_sn_lavadora DESC
Limit 1)
Where (econ_sn_lavadora is null or econ_sn_lavadora = '');

62. Reemplazar los valores nulos del atributo econ_sn_microondas por la moda del atributo econ_sn_microondas de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set econ_sn_microondas=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_microondas
ORDER BY econ_sn_microondas DESC
Limit 1)
Where (econ_sn_microondas is null or econ_sn_microondas = '');

63. Reemplazar los valores nulos del atributo econ_sn_automovil por la moda del atributo econ_sn_automovil de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set econ_sn_automovil=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_automovil
ORDER BY econ_sn_automovil DESC
Limit 1)
Where (econ_sn_automovil is null or econ_sn_automovil = '');

64. Reemplazar los valores nulos del atributo econ_sn_horno por la moda del atributo econ_sn_horno de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set econ_sn_horno=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_horno
ORDER BY econ_sn_horno DESC
Limit 1)
Where (econ_sn_horno is null or econ_sn_horno = '');

65. Reemplazar los valores nulos del atributo econ_sn_nevera por la moda del atributo econ_sn_nevera de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set econ_sn_nevera=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY econ_sn_nevera
ORDER BY econ_sn_nevera DESC
Limit 1)
Where (econ_sn_nevera is null or econ_sn_nevera = '');

66. Reemplazar los valores nulos del atributo infa_dormitorios por la moda del atributo infa_dormitorios de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set infa_dormitorios=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY infa_dormitorios
ORDER BY infa_dormitorios DESC
Limit 1)
Where (infa_dormitorios is null or infa_dormitorios='');

67. Reemplazar los valores nulos del atributo fami_ing_fmliar_mensual por la moda del atributo fami_ing_fmliar_mensual de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set fami_ing_fmliar_mensual=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY fami_ing_fmliar_mensual
ORDER BY fami_ing_fmliar_mensual DESC
Limit 1)
Where (fami_ing_fmliar_mensual is null or fami_ing_fmliar_mensual = '');

68. Reemplazar los valores nulos del atributo estu_trabaja y los valores de estu_trabaja códigos 1,6,7 por la moda del atributo estu_trabaja de la tabla saberpro_2011_2014
>Update saberpro_limpio 
Set estu_trabaja=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY estu_trabaja
ORDER BY estu_trabaja DESC
Limit 1)
Where (estu_trabaja is null or estu_trabaja = '');

>Update saberpro_limpio 
Set estu_trabaja=
(SELECT COUNT(*) as repeticiones
FROM saberpro_2011_2014
GROUP BY estu_trabaja
ORDER BY estu_trabaja DESC
Limit 1)
Where estu_trabaja in ('1','6','7');

69. Reemplazar los valores nulos del atributo estu_horas_trabajo por 0 para los estudiantes que no trabajan.
>Update saberpro_limpio
Set estu_horas_trabajo='0'
Where (estu_horas_trabajo is null or estu_horas_trabajo = '') and
estu_trabaja='0';

70. Reemplazar los valores nulos del atributo estu_horas_trabajo por la media entera de los valores del atributo estu_horas_trabajo de los estudiantes cuyo atributo estu_trabaja es de código ‘3’ de la tabla saberpro_2011_2014. Actualizar únicamente para los estudiantes que trabajan con código ‘3’:
>Update saberpro_limpio
Set estu_horas_trabajo=
(
Select round(avg(cast(estu_horas_trabajo as numeric)),0) 
From saberpro_2011_2014
Where estu_trabaja='3'
)
Where (estu_horas_trabajo is null or estu_horas_trabajo = '') and
estu_trabaja='3';

71. Reemplazar los valores nulos del atributo estu_horas_trabajo por la media entera de los valores del atributo estu_horas_trabajo de los estudiantes cuyo atributo estu_trabaja es de código ‘4’ de la tabla saberpro_2011_2014. Actualizar únicamente para los estudiantes que trabajan con código ‘4’:
>Update saberpro_limpio
Set estu_horas_trabajo=
(
Select round(avg(cast(estu_horas_trabajo as numeric)),0) 
From saberpro_2011_2014
Where estu_trabaja='4'
)
Where (estu_horas_trabajo is null or estu_horas_trabajo = '') and
estu_trabaja='4';

72. Reemplazar los valores nulos del atributo estu_horas_trabajo por la media entera de los valores del atributo estu_horas_trabajo de los estudiantes cuyo atributo estu_trabaja es de código ‘5’ de la tabla saberpro_2011_2014. Actualizar únicamente para los estudiantes que trabajan con código ‘5’
>Update saberpro_limpio
Set estu_horas_trabajo=
(
Select round(avg(cast(estu_horas_trabajo as numeric)),0) 
From saberpro_2011_2014
Where estu_trabaja='5'
)
Where (estu_horas_trabajo is null or estu_horas_trabajo = '') and
estu_trabaja='5';

73. Estandarizar a punto decimal los valores del atributo mod_lectura_critica
>Update saberpro_limpio
Set mod_lectura_critica=
replace(mod_lectura_critica,',','.')
Where mod_lectura_critica like '%,%';

74. Reemplazar los valores nulos del atributo mod_lectura_critica por ‘NP’
>Update saberpro_limpio
Set mod_lectura_critica='NP'
Where (mod_lectura_critica is null or mod_lectura_critica = '');

75. Estandarizar a punto decimal los valores del atributo mod_comunica_escrita_punt
>Update saberpro_limpio
Set mod_comunica_escrita_punt=
replace(mod_comunica_escrita_punt,',','.')
Where mod_comunica_escrita_punt like '%,%';

76. Reemplazar los valores nulos del atributo mod_comunica_escrita_punt por ‘NP’
>Update saberpro_limpio
Set mod_comunica_escrita_punt='NP'
Where (mod_comunica_escrita_punt is null or mod_comunica_escrita_punt = '');

77. Estandarizar a punto decimal los valores del atributo mod_razona_cuantitativo_punt
>Update saberpro_limpio
Set mod_razona_cuantitativo_punt=
replace(mod_razona_cuantitativo_punt,',','.')
Where mod_razona_cuantitativo_punt like '%,%';

78. Reemplazar los valores nulos del atributo mod_razona_cuantitativo_punt por ‘NP’
>Update saberpro_limpio
Set mod_razona_cuantitativo_punt='NP'
Where (mod_razona_cuantitativo_punt is null or mod_razona_cuantitativo_punt = '') ;

79. Estandarizar a punto decimal los valores del atributo mod_ingles_punt.
>Update saberpro_limpio
Set mod_ingles_punt=
replace(mod_ingles_punt,',','.')
Where mod_ingles_punt like '%,%';

80. Reemplazar los valores nulos del atributo mod_ingles_punt por ‘NP’
>Update saberpro_limpio
Set mod_ingles_punt='NP'
Where (mod_ingles_punt is null or mod_ingles_punt = '');

81. Estandarizar a punto decimal los valores del atributo mod_comp_ciudadanas_punt.
Update saberpro_limpio
Set mod_comp_ciudadanas_punt=
replace(mod_comp_ciudadanas_punt,',','.')
Where mod_comp_ciudadanas_punt like '%,%';

82. Reemplazar los valores nulos del atributo mod_comp_ciudadanas_punt por ‘NA’para la prueba 20112.
>Update saberpro_limpio
Set mod_comp_ciudadanas_punt='NA'
Where (mod_comp_ciudadanas_punt is null or mod_comp_ciudadanas_punt = '') 
and prueba='20112';

83. Reemplazar los valores nulos del atributo mod_comp_ciudadanas_punt por ‘NP
>Update saberpro_limpio
Set mod_comp_ciudadanas_punt='NP'
Where (mod_comp_ciudadanas_punt is null or mod_comp_ciudadanas_punt = '');


