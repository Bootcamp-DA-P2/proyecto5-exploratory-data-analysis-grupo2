# Analisis Exploratorio de Datos: Impacto y Evolucion del COVID-19 en Estados Unidos

## Descripcion del Proyecto
Este proyecto realiza un Analisis Exploratorio de Datos (EDA) exhaustivo sobre la evolucion de la pandemia del COVID-19 en los Estados Unidos utilizando el registro historico de datos recopilados hasta marzo de 2021. El objetivo principal es transformar datos brutos en informacion estructurada y comprensible para la toma de decisiones estrategicas, permitiendo presentar conclusiones claras e informes limpios ante la direccion ejecutiva (CEO).

A traves de este analisis se examinan las metricas clave de la enfermedad, tales como el volumen de pruebas realizadas, casos positivos confirmados, hospitalizaciones e ingresos en unidades de cuidados intensivos (UCI), asi como los indices de mortalidad a nivel estatal y nacional.

## Metodologia Aplicada
El flujo de trabajo implementado en el entorno de desarrollo se divide en las siguientes etapas fundamentales:

1. Diagnostico y Estructura: Evaluacion inicial de los tipos de datos, dimensiones de los conjuntos de datos e identificacion de registros nulos mediante tecnicas de inspeccion estadistica.
2. Limpieza y Preprocesamiento: Tratamiento de valores ausentes, filtrado de inconsistencias operativas en los reportes de salud y adaptacion de formatos temporales.
3. Analisis Exploratorio Detallado (EDA): Evaluacion estadistica de tendencias centrales, analisis de dispersion y calculo de metricas agregadas tanto a nivel de estados individuales como a escala pais.
4. Modelado y Pruebas Estadisticas: Incorporacion de analisis avanzados utilizando librerias cientificas para evaluar correlaciones significativas e hipotesis de comportamiento de las variables sanitarias.
5. Visualizacion de Datos: Construccion de graficas comparativas detalladas para ilustrar la relacion entre el avance de contagios y la tasa de mortalidad en el tiempo.

## Estructura del Repositorio
El proyecto se organiza bajo la siguiente estructura de directorios:

* `data/`: Almacena los archivos fuente en formato .csv con el historico nacional (`national-history.csv`) y por estados (`all-states-history.csv`).
* `notebooks/`: Contiene el Jupyter Notebook (`note_book.ipynb`) donde se desarrolla paso a paso el codigo de extraccion, limpieza, analisis descriptivo e inferencial.
* `reports/`: Espacio dedicado al informe ejecutivo final destinado a la presentacion de resultados ante la gerencia.
* `README.md`: Documentacion tecnica actual del proyecto.

## Tecnologias Utilizadas
El analisis se ha desarrollado utilizando el lenguaje de programacion Python y su ecosistema especializado en ciencia de datos:

* Pandas: Para la carga, manipulacion, transformacion y estructuracion de datos en DataFrames.
* NumPy: Soporte para operaciones matematicas y manejo de matrices numericas.
* Matplotlib (Pyplot): Generacion de graficos de linea, diagramas de dispersion y estructuracion base de las visualizaciones.
* Seaborn: Creacion de visualizaciones estadisticas detalladas con mejor rendimiento estetico.
* SciPy (scipy.stats): Implementacion de pruebas parametricas, analisis de distribuciones y calculos estadisticos.
* Statsmodels: Ajuste de modelos estadisticos y exploracion de relaciones avanzadas entre variables sanitarias.

## Conclusiones Principales del Analisis
* Tendencia Temporal: El analisis temporal evidencia los picos de mayor presion hospitalaria y la correlacion directa entre el incremento de pruebas de diagnostico masivas y la deteccion de curvas de positividad.
* Desigualdad Regional: Se observan marcadas diferencias en el impacto acumulado (hospitalizaciones y decesos) dependiendo de las densidades demograficas y las capacidades de respuesta sanitaria de cada estado.
* Relacion de Metricas Criticas: Las graficas comparativas detalladas entre casos positivos detectados y volumen de decesos muestran los desfases de tiempo naturales entre el contagio inicial, la necesidad de ingreso en UCI y los desenlaces criticos.
