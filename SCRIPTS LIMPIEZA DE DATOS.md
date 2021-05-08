### LIMPIEZA DE DATOS

1. Reemplazar los valores ‘EK20123’,EK20133’,’EK20142’,’EK20143 y ‘EKO2014’ del atributo estu_cod_aplicacion por ‘EK20122’,’EK20132’,’EK20141’,EK20142’ y EK20141 respectivamente:
2. Reemplazar los valores ‘20123’,20133’,’20142’,’20143 y ‘O2014’ del atributo prueba por ‘20122’,’20132’,’20141’,20142’ y 20141 respectivamente:
3. Reemplazar los valores nulos del atributo estu_genero por ‘SIN DATO’: 
4. 4. Reemplazar los valores nulos del atributo estu_nacimiento_dia por la moda de este atributo en la tabla saberpro_2011_2014.
5. Reemplazar el valor ‘5’ del atributo estu_nacimiento_dia por ‘05’
6. Reemplazar los valores nulos del atributo estu_nacimiento_mes por la moda de este atributo en la tabla saberpro_2011_2014.
7. Reemplazar los valores nulos del atributo estu_nacimiento_anno por la diferencia entre el año de la prueba menos la moda de este atributo para las pruebas 20112, 20121, 20122, 20132,20131, 20141 y 20142:
8. Reemplazar los valores nulos del atributo estu_pais_reside por ‘COLOMBIA’
9. Reemplazar los valores ‘CO’ del atributo estu_pais_reside por ‘COLOMBIA’
10. Reemplazar los valores nulos del atributo estu_estado_civil por la moda de este atributo.
11. Reemplazar los valores nulos del atributo estu_reside_codmpio por los valores del atributo estu_exam_codmpio_presentacion.
12. Estandarizar el valor del atributo estu_exam_mpio_presentacion de “BOGOTÁ D.C.” por el valor “BOGOTA D.C”.
13. Estandarizar el valor del atributo estu_exam_dpto_presentacion de “BOGOTÁ” por el valor BOGOTA, "BOYACÁ" por BOYACA, CAQUETÁ por CAQUETA, "ATLÁNTICO" por ATLANTICO, “CHOCÓ” por CHOCO, “CÓRDOBA” por CORDOBA,”SAN ANDRÉS” por SAN ANDRES, “VAUPÉS” por VAUPES, “QUINDÍO” por QUINDIO, “GUAINÍA” por GUANIA,”BOLÍVAR” por BOLIVAR.
14. Reemplazar los valores nulos del atributo estu_exam_cod por 141 para la prueba 20141 y por 142 para la prueba 20142.
15. Reemplazar los valores nulos del atributo estu_exam_nombre por EXAMEN SABERPRO 2014-1 para la prueba 20141 y por EXAMEN SABER PRO 2014-2 para la 
prueba 20142.
16. Estandarizar los nombres de las instituciones del atributo inst_nombre_institucion a partir de los nombres de las instituciones de la tabla IES teniendo en cuenta los códigos de las instituciones
17. Reemplazar los valores nulos del atributo inst_origen por el código ‘4’ para las instituciones o escuelas normal superior
18. Reemplazar los valores nulos del atributo inst_origen por los valores no nulos del atributo inst_origen en los casos de las instituciones que tienen el mismo código de 
institución inst_cod_institucion
19. Reemplazar los valores del atributo inst_origen por el código ‘5’ para la "ESCUELA NORMAL SUPERIOR ANTIOQUEÑA con código 4.
20. Reemplazar los valores numéricos del atributo inst_origen por su descripción de acuerdo a la siguiente tabla:
