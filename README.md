# Movies Project

# 1. Objetivo

Para este proyecto, se usarán tres fuentes de datos de diferentes formatos:
|Nombre|	Descripción General|	URL| Formato de Datos|
|------|----------------------|----|------------------|
|MUBI SVOD Platform Database for Movie Lovers |	Recopilación de todas las películas existentes en la plataforma MUBI en donde se conoce el rating, criticas y listas hechas por los usuarios. (+15.000.000 de registros basados en rating con su crítica hecha por usuarios)|https://www.kaggle.com/clementmsika/mubi-sqlite-database-for-movie-lovers?select=mubi_db.sqlite|SQLITE
|TheMovieDB|	Plataforma online donde se puede obtener el listado con información bastante completa de películas y series de televisión| https://developers.themoviedb.org/|	API RESTFul|
|Movies on Netflix, Prime Video, Hulu and Disney+	|Coleccion de informacion respecto a peliculas que se encuentran existentes en las plataformas online de Netflix, Amazon Prime Video, Hulu y Disney+|https://www.kaggle.com/ruchi798/movies-on-netflix-prime-video-hulu-and-disney|CSV|

La preparación de estos datos esta destinada a unir estas fuentes de datos para obtener un dataset bastante completo en donde podamos obtener información general de las películas, el rating, las opiniones que dieron  diferentes usuarios; además, de saber cuantos usuarios usan la plataforma de MUBI de manera gratuita y paga por medio de la creación de las opiniones hechas en las películas.

La union con la idea anterior mencionada con otro de los datasets (Movies on Netflix, Prime Video, Hulu and Disney+) consiste en saber cuales de estas peliculas se encuentran en las plataformas de Netflix, Amazon Prime Video, Hulu y Disney+ 

# 2. Posibles Casos de Uso

Aplicaciones:
- 
-
-
-

• Explicar para qué casos de uso final deseas preparar los datos (por ejemplo, tabla de
análisis, aplicación de fondo, base de datos de fuentes de verdad, etc.)

# 3. Pasos para Limpieza de Datos

## 1. Eliminar variables irrelevantes y redudantes

En este caso por el gran volumen de datos, se realizo la eliminacion de unas columnas inrrelevantes que se presentaban en las tablas existentes en 
la db.

[![sada.png](https://i.postimg.cc/kX2wC711/sada.png)](https://postimg.cc/6yNCLxNn)

- Las tablas "list" y "list_users" se descartaron ya que contenian informacion que se salia del foco de estudio del ejercicio.
- La tabla "rating_users" era informacion redudantes que ya existia en la tabla de "ratings" 
- Se hizo una normalizacion en la tabla de "movies" sacando la informacion de los directores (director) ya que es una entidad dentro de otra que podia se separada; el mismo caso seria para la tabla "ratings" al separar la informacion de los usuarios (users) en donde se posee informacion sobre el tipo de subcripcion que tiene cada cliente

## 2. Descripcion estadistica de los datos


# 4. Modelo de Datos

Paso 3: Definir el modelo de datos

La arquitectura diseñada para este proceso de ETL es: 
[![Untitled-Diagram-5.png](https://i.postimg.cc/HxT7ktpW/Untitled-Diagram-5.png)](https://postimg.cc/GBSpMG86)

El lenguaje escogido para este procesamiento ha sido Python, debido a su versatilidad en manejo de gran volumen de datos y librerias que permiten ejercer tareas de limpieza, union y verificacion mucho mas sencillo y rapido desde una plataforma en la nube. 

Se escogio las herramientas de AWS tales como Sagemaker (procesamiento online con Python para gran volumen de datos y ETL), S3 (almacenamiento en la nube, RDS (servidor en la nube para bases de datos online) debido a que tiene un periodo de prueba bastante aprovechable en comparacion con otras herramientas cloud tales como Azure y Google Cloud, ademas de que es un arquitectura fuertemente interesante para trabajar y utilizada en el mercado por su innovacion. Ademas, que por la compatibilidad, permite un mejor manejo de errores entre la comunicacion de componentes.
Vale destacar el uso de SageMaker como ETL novedosa que permite tomar informacion directamente para aplicar su insercion a alguna base de datos de manera bastante intuituva por parte de interfaz, y tambien permitiendo aplicar codigo para esto.

El modelo de los datos que se decidio aplicar fue un modelo relacion donde se representaran correctamente las llames primarias del modelo y las foraneas que existen entre ellas. 


Se recomienda hacer una actualizacion de datos estaticos como lo son el SQLITE y los CSV de manera semestral o anual, ya que las novedades en gran volumen se presentan en periodo de tiempos largos (cuando se habla de peliculas) y así, en su momento, es de facil adquisicion y de utilidad de estudio los ratings que se generan a partir de ellos. 

• Trazar el modelo de datos conceptuales y explicar por qué se eligió ese modelo.
• Diseñar la arquitectura y los recursos que utilizados
• Indique claramente los motivos de la elección de las herramientas y tecnologías para el
proyecto.
• Proponga con qué frecuencia deben actualizarse los datos y por qué.


# 5. Pasos para crear la ETL

# 6. ¿Que hacer si...

###Si los datos se incrementaran en 100x.
Se veria la necesidad de aumentar la capicidad de la nube para el procesamiento a nivel de la ETL, tambien esta la opcion de manejar lamdas y convertir los datos a datos no estrucurados tales como un JSON para un mejor procesamiento de lo mismo. Tambien, se podria crear mas jobs para los nuevos batch de informacion. 

###Si las tuberías se ejecutaran diariamente a las 7 de la mañana.
En este caso del modelo, se tendria que asegurar que la diferencia de informacion no seria tan diferente dia tras dia, ya que el API traeria nueva informacion pero no lo suficiente para poder usar el dataset en general como una tarea de analisis mas profunda. 

o Si la base de datos necesitara ser accedida por más de 100 personas.
Generar una base de datos que permita un alto volumen de consulta tales como un Snowflake o una base de datos NoSQL para la atencion a la demanda que se podria generar en el servidor. Tambien habria que aumentar la capacidad de peticiones y permisos en el servidor. 



Paso 2: Explorar y evaluar los datos
• Explorar los datos para identificar problemas de calidad de los datos, como valores
perdidos, datos duplicados, problemas de formato etc.
• Documentar los pasos necesarios para limpiar los datos, indicar que tipo de pasos se
sugieren para la limpieza. Tip se puede usar un diagrama, mapa mental o adición en la
arquitectura del paso siguiente con el fin de dejar claro este paso.


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
