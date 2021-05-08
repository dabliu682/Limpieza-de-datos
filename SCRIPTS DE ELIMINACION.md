### SCRIPTS DE ELIMINACION

1. Crear la tabla saberpro_final a partir de saberpro_transformado.
>CREATE TABLE saberpro_final AS SELECT * FROM saberpro_transformado;

2. Eliminar los atributos estu_nacimiento_dia, estu_nacimiento_mes,
>ALTER TABLE saberpro_final DROP estu_nacimiento_dia;<br>
>ALTER TABLE saberpro_final DROP estu_nacimiento_mes;<br>
>ALTER TABLE saberpro_final DROP estu_nacimiento_anno;

3. Eliminar el atributo estu_estado_civil.
>ALTER TABLE saberpro_final DROP estu_estado_civil;<br>

4. Eliminar los atributos estu_disc_invidente, estu_disc_sordo_con_interprete,
>ALTER TABLE saberpro_final DROP estu_disc_invidente;<br>
>ALTER TABLE saberpro_final DROP estu_disc_sordo_con_interprete;<br>
>ALTER TABLE saberpro_final DROP estu_disc_sordo_sin_interprete;<br>
>ALTER TABLE saberpro_final DROP estu_disc_motriz;<br>
>ALTER TABLE saberpro_final DROP estu_disc_sordo_ceguera;

5. Eliminar el atributo estu_zona
>ALTER TABLE saberpro_final DROP estu_zona;

6. Eliminar el atributo estu_anno_egreso
>ALTER TABLE saberpro_final DROP estu_anno_egreso;

7. Eliminar el atributo econ_area_vive
>ALTER TABLE saberpro_final DROP econ_area_vive;

8. Eliminar el atributo estu_reside_codmpio
>ALTER TABLE saberpro_final DROP estu_reside_codmpio;

9. Eliminar el atributo estu_exam_codmpio_presentacion
>ALTER TABLE saberpro_final DROP estu_exam_codmpio_presentacion;

10. Eliminar el atributo estu_exam_mpio_presentacion
>ALTER TABLE saberpro_final DROP estu_exam_mpio_presentacion;

11. Eliminar el atributo estu_exam_dpto_presentacion
>ALTER TABLE saberpro_final DROP estu_exam_dpto_presentacion;

12. Eliminar el atributo estu_exam_cod y estu_exam_nombre
>ALTER TABLE saberpro_final DROP estu_exam_cod;<br>
>ALTER TABLE saberpro_final DROP estu_exam_nombre;

13. Eliminar el atributo estu_metodo_prgm
ALTER TABLE saberpro_final DROP estu_metodo_prgm;

14. Eliminar el atributo dipo_codigomunicipio
>ALTER TABLE saberpro_final DROP dipo_codigomunicipio;

15. Eliminar el atributo inst_cod_jornada
>ALTER TABLE saberpro_final DROP inst_cod_jornada;

16. Eliminar el atributo estu_semestre_cursa
>ALTER TABLE saberpro_final DROP estu_semestre_cursa;

17. Eliminar el atributo estu_pje_creditos
>ALTER TABLE saberpro_final DROP estu_pje_creditos;

18. Eliminar el atributo inst_vlr_matricula_ant
>ALTER TABLE saberpro_final DROP inst_vlr_matricula_ant;

19. Eliminar los atributos: estu_sn_matricula_propio, estu_sn_matricula_padres,
>ALTER TABLE saberpro_final DROP estu_sn_matricula_propio;<br>
>ALTER TABLE saberpro_final DROP estu_sn_matricula_padres;<br>
>ALTER TABLE saberpro_final DROP estu_sn_matricula_beca;<br>
>ALTER TABLE saberpro_final DROP estu_sn_matricula_credito;<br>
>ALTER TABLE saberpro_final DROP estu_titulo_bto;<br>
>ALTER TABLE saberpro_final DROP estu_exam_semestre_pretacion;<br>
>ALTER TABLE saberpro_final DROP estu_exam_anno_presentacion;<br>
>ALTER TABLE saberpro_final DROP estu_hogar_actual;

20. Eliminar los atributos fami_cod_educa_padre , fami_cod_educa_madre, fami_sn_lee_escribe_padre, fami_sn_lee_escribe_madre, fami_num_pers_cargo y estu_sn_cabeza_fmlia
>ALTER TABLE saberpro_final DROP fami_num_pers_cargo;<br>
>ALTER TABLE saberpro_final DROP estu_sn_cabeza_fmlia;

21. Eliminar econ_cuartos, econ_sn_automovil y fami_cod_max_nivel_educa_padres
>ALTER TABLE saberpro_final DROP econ_cuartos;<br>
>ALTER TABLE saberpro_final DROP econ_sn_automovil;


22. Eliminar los atributos fami_sn_lee_escribe_padre y fami_sn_lee_escribe_madre
>ALTER TABLE saberpro_final DROP fami_sn_lee_escribe_padre;<br>
>ALTER TABLE saberpro_final DROP fami_sn_lee_escribe_madre;


23. Eliminar los atributos fami_cod_ocup_padre, fami_cod_ocup_madre
>ALTER TABLE saberpro_final DROP fami_cod_ocup_padre;<br>
>ALTER TABLE saberpro_final DROP fami_cod_ocup_madre;

24. Eliminar los atributos fami_num_hermanos, fami_nivel_hermano
>ALTER TABLE saberpro_final DROP fami_num_hermanos;<br>
>ALTER TABLE saberpro_final DROP fami_nivel_hermano;

25. Eliminar el atributo econ_material_pisos
>ALTER TABLE saberpro_final DROP econ_material_pisos;

26. Eliminar los atributos infa_dormitorios y fami_num_pers_grup_fam
>ALTER TABLE saberpro_final DROP infa_dormitorios;<br>
>ALTER TABLE saberpro_final DROP fami_num_pers_grup_fam;

27. Eliminar los atributos econ_sn_televisor, econ_sn_motocicleta, econ_sn_energia, econ_sn_acueducto, econ_sn_alcantarillado, econ_sn_aseo, econ_sn_estufa
>ALTER TABLE saberpro_final DROP econ_sn_televisor;<br>
>ALTER TABLE saberpro_final DROP econ_sn_motocicleta;<br>
>ALTER TABLE saberpro_final DROP econ_sn_energia;<br>
>ALTER TABLE saberpro_final DROP econ_sn_acueducto;<br>
>ALTER TABLE saberpro_final DROP econ_sn_alcantarillado;<br>
>ALTER TABLE saberpro_final DROP econ_sn_aseo;<br>
>ALTER TABLE saberpro_final DROP econ_sn_estufa;

28. Eliminar los atributos econ_sn_telefonia, econ_sn _celular, econ_sn_internet,econ_sn_servicio_tv y econ_sn _computador.
>ALTER TABLE saberpro_final DROP econ_sn_telefonia;<br>
>ALTER TABLE saberpro_final DROP econ_sn_celular;<br>
>ALTER TABLE saberpro_final DROP econ_sn_internet;<br>
>ALTER TABLE saberpro_final DROP econ_sn_servicio_tv;<br>
>ALTER TABLE saberpro_final DROP econ_sn_computador;

29. Eliminar los atributos econ_ sn _dvd, econ_sn_lavadora, econ_sn _microondas,econ_sn_horno y econ_sn _nevera.
>ALTER TABLE saberpro_final DROP econ_sn_dvd;<br>
>ALTER TABLE saberpro_final DROP econ_sn_lavadora;<br>
>ALTER TABLE saberpro_final DROP econ_sn_microondas;<br>
>ALTER TABLE saberpro_final DROP econ_sn_horno;<br>
>ALTER TABLE saberpro_final DROP econ_sn_nevera;

30. Eliminar los atributos estu_trabaja y estu_horas_trabajo
>ALTER TABLE saberpro_final DROP estu_trabaja;<br>
>ALTER TABLE saberpro_final DROP estu_horas_trabajo;

31. Eliminar los atributos estu_otro_idioma_lee, estu_otro_idioma_habla, estu_nivel_postgrado y estu_etnia
>ALTER TABLE saberpro_final DROP estu_otro_idioma_lee;<br>
>ALTER TABLE saberpro_final DROP estu_otro_idioma_habla;<br>
>ALTER TABLE saberpro_final DROP estu_nivel_postgrado;<br>
>ALTER TABLE saberpro_final DROP estu_etnia;

32. Eliminar los atributos mod_comunica_escrita_desem y mod_ingles_desem
>ALTER TABLE saberpro_final DROP mod_comunica_escrita_desem;<br>
>ALTER TABLE saberpro_final DROP mod_ingles_desem;

