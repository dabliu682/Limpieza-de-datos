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
5. Reemplazar los valores nulos del atributo estu_nacimiento_dia por la moda de este atributo en la tabla saberpro_2011_2014.
>Update saberpro_limpio
Set estu_nacimiento_dia='31'
Where (estu_nacimiento_dia is null or estu_nacimiento_dia = '');
7. Reemplazar el valor ‘5’ del atributo estu_nacimiento_dia por ‘05’
>Update saberpro_limpio
Set estu_nacimiento_dia='05'
Where estu_nacimiento_dia = '5';
9. Reemplazar los valores nulos del atributo estu_nacimiento_mes por la moda de este atributo en la tabla saberpro_2011_2014.
10. Reemplazar los valores nulos del atributo estu_nacimiento_anno por la diferencia entre el año de la prueba menos la moda de este atributo para las pruebas 20112, 20121, 20122, 20132,20131, 20141 y 20142:
11. Reemplazar los valores nulos del atributo estu_pais_reside por ‘COLOMBIA’
12. Reemplazar los valores ‘CO’ del atributo estu_pais_reside por ‘COLOMBIA’
13. Reemplazar los valores nulos del atributo estu_estado_civil por la moda de este atributo.
14. Reemplazar los valores nulos del atributo estu_reside_codmpio por los valores del atributo estu_exam_codmpio_presentacion.
15. Estandarizar el valor del atributo estu_exam_mpio_presentacion de “BOGOTÁ D.C.” por el valor “BOGOTA D.C”.
16. Estandarizar el valor del atributo estu_exam_dpto_presentacion de “BOGOTÁ” por el valor BOGOTA, "BOYACÁ" por BOYACA, CAQUETÁ por CAQUETA, "ATLÁNTICO" por ATLANTICO, “CHOCÓ” por CHOCO, “CÓRDOBA” por CORDOBA,”SAN ANDRÉS” por SAN ANDRES, “VAUPÉS” por VAUPES, “QUINDÍO” por QUINDIO, “GUAINÍA” por GUANIA,”BOLÍVAR” por BOLIVAR.
17. Reemplazar los valores nulos del atributo estu_exam_cod por 141 para la prueba 20141 y por 142 para la prueba 20142.
18. Reemplazar los valores nulos del atributo estu_exam_nombre por EXAMEN SABERPRO 2014-1 para la prueba 20141 y por EXAMEN SABER PRO 2014-2 para la prueba 20142.
19. Estandarizar los nombres de las instituciones del atributo inst_nombre_institucion a partir de los nombres de las instituciones de la tabla IES teniendo en cuenta los códigos de las instituciones
20. Reemplazar los valores nulos del atributo inst_origen por el código ‘4’ para las instituciones o escuelas normal superior
21. Reemplazar los valores nulos del atributo inst_origen por los valores no nulos del atributo inst_origen en los casos de las instituciones que tienen el mismo código de 
institución inst_cod_institucion
19. Reemplazar los valores del atributo inst_origen por el código ‘5’ para la "ESCUELA NORMAL SUPERIOR ANTIOQUEÑA con código 4.
20. Reemplazar los valores numéricos del atributo inst_origen por su descripción de acuerdo a la siguiente tabla:<br>
<table>
    <tr>
        <td>Codigo</td>
        <td>Descripción</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Oficial Nacional</td>
    </tr>
  <tr>
        <td>2</td>
        <td>Oficial Departamental</td>
    </tr>
  <tr>
        <td>3</td>
        <td>Oficial Nacional</td>
    </tr>
  <tr>
        <td>4</td>
        <td>Oficial Municipal</td>
    </tr>
  <tr>
        <td>5</td>
        <td>Oficial (Normales)</td>
    </tr>
  <tr>
        <td>6</td>
        <td>No Oficial(Normales)</td>
    </tr>
  <tr>
        <td>7</td>
        <td>No Oficial – Fundación</td>
    </tr>
  <tr>
        <td>8</td>
        <td>No Oficial – Corporación</td>
    </tr>
  <tr>
        <td>9</td>
        <td>Régimen Especial</td>
    </tr>
</table>

21. Estandarizar los valores del atributo inst_origen, para aquellos casos en los que existen tildes: 'NO OFICIAL - FUNDACIÓN', 'NO OFICIAL - CORPORACIÓN' y 'RÉGIMEN ESPECIAL’:
22. Reemplazar los valores nulos del atributo inst_caracter_academico por los valores no nulos del atributo inst_caracter_academico en los casos de las instituciones que tienen el mismo código de institución inst_cod_institucion
23. Reemplazar los valores nulos del atributo estu_nivel_prgm_academico por el valor no nulo del atributo estu_nivel_prgm_academico de los programas iguales de la  misma institución
24. Reemplazar los valores nulos del atributo estu_nivel_prgm_academico por “UNIVERSITARIA” para aquellas instituciones cuyo nombre inst_nombre_institucion inicie con “UNIVERSIDAD”
25. Reemplazar los valores nulos del atributo estu_nivel_prgm_academico por “UNIVERSITARIA” para aquellos programas cuyo nombre estu_prgm_academico contengan las palabras INGENIERIA, DERECHO, MEDICINA, ODONTOLOGIA, CONTADURIA,LICENCIATURA,PSICOLOGIA ARQUITECTURA, ECOLOGIA, FISIOTERAPIA, ZOOTECNIA, ADMINISTRACIÓN, DISEÑO, SOCIAL, PUBLICIDAD, INTERNACIONAL, ARTES, PERIODISMO, GASTRONOMÍA, CIENCIA, TERAPIA, SALUD 
26. Reemplazar los valores del atributo estu_nivel_prgm_academico por “TECNOLOGIA” para aquellos programas cuyo nombre estu_prgm_academico inicie con la palabra ‘TECNOLOGÍA’ o ‘TECNOLOGIA’
27. Reemplazar los valores del atributo estu_nivel_prgm_academico por “TECNICO” para aquellos programas cuyo nombre estu_prgm_academico inicie con la palabra ‘TECNICO’ , ‘TÉCNICO’,’TÉCNICA’,’TECNICA’
28. Reemplazar los valores nulos del atributo estu_metodo_prgm por el valor no nulo del atributo estu_metodo_prgm de la institución con igual código(inst_cod_institucion) o nombre (inst_nombre_institucion), y de los programas del mismo código(estu_prac_id_prgrm_academico) o nombre (estu_prgm_academico)
29. Reemplazar los valores nulos del atributo estu_metodo_prgm por los valores del atributo metodología de la tabla programas_ies teniendo en cuenta los códigos de las instituciones y de los programas
30. Reemplazar los 2 restantes valores nulos del atributo estu_metodo_prgm por la moda ‘PRESENCIAL’
31. Estandarizar los valores del atributo estu_metodo_prgm en mayúsculas;
32. Reemplazar los valores nulos del atributo dipo_codigomunicipio por los valores del  atributo estu_exam_codmpio_presentacion:
33. Reemplazar los valores nulos del atributo inst_cod_jornada por la moda “1” para los nombres de instituciones que contengan la palabra ‘NORMAL’.
34. Reemplazar los valores nulos del atributo inst_cod_jornada por la moda del resto de instituciones que es ‘12’
35. Reemplazar los valores nulos del atributo estu_area_conoc de saberpro_limpio, por el valor no nulo del atributo estu_area_conoc de los programas del mismo nombre (estu_prgm_academico) de la tabla saberpro_2011_2014
36. Reemplazar los valores nulos del atributo estu_nucleo_pregrado de saberpro_limpio, por el valor no nulo del atributo estu_nucleo_pregrado de los programas del mismo  nombre (estu_prgm_academico) de la tabla saberpro_2011_2014
37. Reemplazar los valores nulos del atributo estu_cod_grupo_ref de saberpro_limpio, por el valor no nulo del atributo estu_cod_grupo_ref de los grupos de referencia con  el nombre (estu_grupo_referencia) de la tabla saberpro_2011_2014
38. Actualizar en la tabla saberpro_limpio, el atributo estu_cod_grupo_ref utilizando en algunos casos caracteres comodines “%” y “_” asi: (utilice select case when) BELLAS ARTES Y DISEÑO por el código 1, CIENCIAS NATURALES Y EXACTAS por el código 2, CIENCIAS SOCIALES por el código 3,HUMANIDADES por el código 4, DERECHO por el código 5, COMUNICACI_N, PERIODISMO Y PUBLICIDAD por el código 6, CIENCIAS MILITARES Y NAVALES por el código 7, %CIENCIAS AGROPECUARIAS% por el código 8, %ADMINISTRACI_N% por el código 9, EDUCACI_N por el código 10, ARQUITECTURA Y URBANISMO por el código 11, INGENIER_A por el código 12, %SALUD% por el código 13, MEDICINA por el código 14, %INGENIER_A, INDUSTRIA Y MINAS% por el código 15, %TIC% por el código 17, %ARTES - DISEÑO – COMUNICACI_N% por el código 19, %CIENCIAS AGROPECUARIAS% por el código 20, NORMALES SUPERIORES por el código 27, %JUDICIAL% por el código 28, %MILITAR Y POLICIAL% por el código 29, RECREACI_N Y DEPORTES por el código 30, %ECONOM% por el código 31, %CONTADUR_A% por el código 32, PSICOLOG_A por el código 33, ENFERMER_A por el código 34, GRUPO REFERENCIA NACIONAL% por el código 42;
39. Reemplazar los nulos del atributo estu_semestre_cursa por la moda (de las NORMALES) del atributo estu_semestre_cursa de la tabla saberpro_2011_2014, para los nombres de instituciones que contengan la palabra ‘NORMAL’.40. Reemplazar los valores nulos del atributo estu_semestre_cursa de saberpro_limpio, por el valor no nulo del atributo estu_semestre_cursa de la tabla saberpro_2011_2014 de igual instituciones con los mismos programas
40. Reemplazar los nulos del atributo estu_pje_creditos por el código ‘0’ para aquellas instituciones cuyo valor del atributo estu_nivel_prgm_academico es ‘NORMALISTA’ o el nombre de la institución del atributo inst_nombre_institucion contiene la sigla SENA.
41. Reemplazar los valores nulos del atributo estu_pje_creditos por el valor no nulo del atributo estu_pje_creditos de la institución con igual código (inst_cod_institucion) o nombre (inst_nombre_institucion), y de los programas del mismo código(estu_prac_id_prgrm_academico) o nombre (estu_prgm_academico)
42. Reemplazar los valores nulos del atributo inst_vlr_matricula_ant por la moda (de las NORMALES) del atributo inst_vlr_matricula_ant de la tabla saberpro_2011_2014, para los nombres de instituciones que contengan la palabra ‘NORMAL’.
43. Reemplazar los valores nulos del atributo inst_vlr_matricula_ant de saberpro_limpio, por el valor no nulo del atributo inst_vlr_matricula_ant de la tabla saberpro_2011_2014 de igual instituciones con los mismos programas
44. Reemplazar los valores nulos del atributo estu_titulo_bto por la moda (de las NORMALES) del atributo estu_titulo_bto de la tabla saberpro_2011_2014, para los nombres de instituciones que contengan la palabra ‘NORMAL’.
45. Reemplazar los valores nulos del atributo estu_titulo_bto al resto de instituciones por la moda del atributo estu_titulo_bto de la tabla saberpro_2011_2014 
46. Reemplazar los valores nulos del atributo estu_hogar_actual por la moda del atributo estu_hogar_actual de la tabla saberpro_2011_2014 
47. Reemplazar los valores nulos del atributo fami_num_pers_grup_fam por la media (redondeada a entera) de los valores no nulos de fami_num_pers_grup_fam de la tabla saberpro_2011_2014:
48. Reemplazar los valores nulos del atributo estu_sn_cabeza_fmlia por la moda del atributo estu_sn_cabeza_fmlia de la tabla saberpro_2011_2014.50. Reemplazar los valores nulos del atributo fami_num_pers_cargo por la media (redondeada a entera) de los valores no nulos de fami_num_pers_cargo de la tabla saberpro_2011_2014;
49. Reemplazar los valores nulos del atributo fami_cod_educa_padre por el código ‘99’
50. Reemplazar los valores 1,2,3,4,5,6,7,8 del atributo fami_cod_educa_padre por el código ‘9’
51. Reemplazar los valores nulos del atributo fami_cod_educa_madre por el código ‘99’
52. Reemplazar los valores 1,2,3,4,5,6,7,8 del atributo fami_cod_educa_madre por el código ‘9’
53. Reemplazar los valores nulos del atributo fami_cod_ocup_madre por el código ‘99’
54. Reemplazar los valores 01,02,03,04,05,06,07,08,09,10,11,12 del atributo fami_cod_ocup_madre por la moda del atributo fami_cod_ocup_madre de la tabla  saberpro_2011_2014
55. Reemplazar los valores nulos del atributo estu_estrato por la moda del atributo estu_estrato de la tabla saberpro_2011_2014 
56. Reemplazar los valores nulos del atributo fami_nivel_sisben por la moda del atributo fami_nivel_sisben de la tabla saberpro_2011_2014
57. Reemplazar los valores nulos del atributo econ_material_pisos por la moda del atributo econ_material_pisos de la tabla saberpro_2011_2014
58. Reemplazar los valores nulos del atributo econ_sn_telefonia por la moda del atributo econ_sn_telefonia de la tabla saberpro_2011_2014 
59. Reemplazar los valores nulos del atributo econ_sn_internet por la moda del atributo econ_sn_internet de la tabla saberpro_2011_2014
60. Reemplazar los valores nulos del atributo econ_sn_servicio_tv por la moda del atributo econ_sn_servicio_tv de la tabla saberpro_2011_2014
61. Reemplazar los valores nulos del atributo econ_sn_computador por la moda del atributo econ_sn_computador de la tabla saberpro_2011_2014
62. Reemplazar los valores nulos del atributo econ_sn_celular y los de econ_sn_celular código 2 por la moda del atributo econ_sn_celular de la tabla saberpro_2011_2014.
63. Reemplazar los valores nulos del atributo econ_sn_dvd y los de econ_sn_dvd código 2 por la moda del atributo econ_sn_dvd de la tabla saberpro_2011_2014
64. Reemplazar los valores nulos del atributo econ_sn_lavadora por la moda del atributo econ_sn_lavadora de la tabla saberpro_2011_2014 
65. Reemplazar los valores nulos del atributo econ_sn_microondas por la moda del atributo econ_sn_microondas de la tabla saberpro_2011_2014
66. Reemplazar los valores nulos del atributo econ_sn_automovil por la moda del atributo econ_sn_automovil de la tabla saberpro_2011_2014
67. Reemplazar los valores nulos del atributo econ_sn_horno por la moda del atributo econ_sn_horno de la tabla saberpro_2011_2014
68. Reemplazar los valores nulos del atributo econ_sn_nevera por la moda del atributo econ_sn_nevera de la tabla saberpro_2011_2014
69. Reemplazar los valores nulos del atributo infa_dormitorios por la moda del atributo infa_dormitorios de la tabla saberpro_2011_2014
70. Reemplazar los valores nulos del atributo fami_ing_fmliar_mensual por la moda del atributo fami_ing_fmliar_mensual de la tabla saberpro_2011_2014
71. Reemplazar los valores nulos del atributo estu_trabaja y los valores de estu_trabaja códigos 1,6,7 por la moda del atributo estu_trabaja de la tabla saberpro_2011_2014
72. Reemplazar los valores nulos del atributo estu_horas_trabajo por 0 para los estudiantes que no trabajan.
73. Reemplazar los valores nulos del atributo estu_horas_trabajo por la media entera de los valores del atributo estu_horas_trabajo de los estudiantes cuyo atributo estu_trabaja es de código ‘3’ de la tabla saberpro_2011_2014. Actualizar únicamente para los estudiantes que trabajan con código ‘3’:
74. Reemplazar los valores nulos del atributo estu_horas_trabajo por la media entera de los valores del atributo estu_horas_trabajo de los estudiantes cuyo atributo estu_trabaja es de código ‘4’ de la tabla saberpro_2011_2014. Actualizar únicamente para los estudiantes que trabajan con código ‘4’:
75. Reemplazar los valores nulos del atributo estu_horas_trabajo por la media entera de los valores del atributo estu_horas_trabajo de los estudiantes cuyo atributo estu_trabaja es de código ‘5’ de la tabla saberpro_2011_2014. Actualizar únicamente para los estudiantes que trabajan con código ‘5’
76. Estandarizar a punto decimal los valores del atributo mod_lectura_critica
77. Reemplazar los valores nulos del atributo mod_lectura_critica por ‘NP’
78. Estandarizar a punto decimal los valores del atributo mod_comunica_escrita_punt
79. Reemplazar los valores nulos del atributo mod_comunica_escrita_punt por ‘NP’
80. Estandarizar a punto decimal los valores del atributo mod_razona_cuantitativo_punt
81. Reemplazar los valores nulos del atributo mod_razona_cuantitativo_punt por ‘NP’
82. Estandarizar a punto decimal los valores del atributo mod_ingles_punt.
83. Reemplazar los valores nulos del atributo mod_ingles_punt por ‘NP’
84. Estandarizar a punto decimal los valores del atributo mod_comp_ciudadanas_punt.
85. Reemplazar los valores nulos del atributo mod_comp_ciudadanas_punt por ‘NA’para la prueba 20112.
86. Reemplazar los valores nulos del atributo mod_comp_ciudadanas_punt por ‘NP

