# Movies Project

# 1. Objetivo

Para este proyecto, se usarán tres fuentes de datos de diferentes formatos:
|Nombre|	Descripción| General|	URL| Formato de Datos|
|------|-------------|--------|----|------------------|
|MUBI SVOD Platform Database for Movie Lovers |	Recopilación de todas las películas existentes en la plataforma MUBI en donde se conoce el rating, criticas y listas hechas por los usuarios. (+15.000.000 de registros basados en rating con su crítica hecha por usuarios)|https://www.kaggle.com/clementmsika/mubi-sqlite-database-for-movie-lovers?select=mubi_db.sqlite|SQLITE
|TheMovieDB|	Plataforma online donde se puede obtener el listado con información bastante completa de películas y series de televisión| https://developers.themoviedb.org/|	API RESTFul|
|Movies on Netflix, Prime Video, Hulu and Disney+	|Coleccion de informacion respecto a peliculas que se encuentran existentes en las plataformas online de Netflix, Amazon Prime Video, Hulu y Disney+|https://www.kaggle.com/ruchi798/movies-on-netflix-prime-video-hulu-and-disney|CSV|

La preparación de estos datos esta destinada a unir estas fuentes de datos para obtener un dataset bastante completo en donde podamos obtener información general de las películas, el rating, las opiniones que dieron los diferentes usuarios; además, de saber cuantos usuarios usan la plataforma de MUBI de manera gratuita y paga por medio de la creación de las opiniones hechas en las películas; también podremos saber en cuantas listas creadas por usuarios existen las películas. 
Tambien podremos saber cuales películas de estas, existen en las plataformas de Netflix, Amazon Prime Video, Hulu y Disney+ 

# 2. Posibles Casos de Uso
# 3. Pasos para Limpieza de Datos
# 4. Modelo de Datos
# 5. Pasos para crear la ETL
# 6. ¿Que hacer si...

o Si los datos se incrementaran en 100x.
o Si las tuberías se ejecutaran diariamente a las 7 de la mañana.
o Si la base de datos necesitara ser accedida por más de 100 personas.



Aplicaciones:
-
-
-
-



Dado que el alcance la prueba dependerá en gran medida de los datos, estas dos cosas suceden
simultáneamente. En este paso, debes:
• Identificar y recopilar los datos que usaras para tu proyecto (al menos tres fuentes y más
de un millón de filas.
• Explicar para qué casos de uso final deseas preparar los datos (por ejemplo, tabla de
análisis, aplicación de fondo, base de datos de fuentes de verdad, etc.)
Paso 2: Explorar y evaluar los datos
• Explorar los datos para identificar problemas de calidad de los datos, como valores
perdidos, datos duplicados, problemas de formato etc.
• Documentar los pasos necesarios para limpiar los datos, indicar que tipo de pasos se
sugieren para la limpieza. Tip se puede usar un diagrama, mapa mental o adición en la
arquitectura del paso siguiente con el fin de dejar claro este paso.
Paso 3: Definir el modelo de datos
• Trazar el modelo de datos conceptuales y explicar por qué se eligió ese modelo.
• Diseñar la arquitectura y los recursos que utilizados
• Indique claramente los motivos de la elección de las herramientas y tecnologías para el
proyecto.
• Proponga con qué frecuencia deben actualizarse los datos y por qué.

Paso 4: Ejecutar ETL para modelar los datos
• Crear las tuberías de datos y el modelo de datos
• Incluir un diccionario de datos
• Ejecutar controles de calidad de los datos para asegurar que la tubería funcionó como se
esperaba
• Limitaciones de integridad en la base de datos relacional (por ejemplo, clave única, tipo
de datos, etc.)
• Pruebas de unidad para los “Script” para asegurar que están haciendo lo correcto.
• Comprobaciones de fuente/conteo para asegurar la integridad de los datos.
Paso 5: Completar la redacción del proyecto
• ¿Cuál es el objetivo?
• ¿Qué preguntas quieres hacer?
• ¿Por qué eligió el modelo que eligió?
