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
- Analisis de Sentimientos de acuerdo a las opiniones dadas en las peliculas por edad, genero 
- Analisis descriptivo de la situacion actual de las peliculas disponibles de los diferentes streaming existente.
- Prediccion respecto a la frencuencia de peliculas que se podrian ver
- Serie de tiempo de acuerdo a cuantas opiniones recibio cada pelicula. 


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

- Se realizo un analisis estadistico a alto rasgo para evaluar que los datos estuvieran completos y tuviera completitud.
- Se realizo una limpieza de los datos que tuvieran null o NaN como valores
- Como limpieza de datos se procedio a eliminar columnas, corregir errores y normalizar datos

# 4. Modelo de Datos

La arquitectura diseñada para este proceso de ETL es: 
[![Untitled-Diagram-5.png](https://i.postimg.cc/HxT7ktpW/Untitled-Diagram-5.png)](https://postimg.cc/GBSpMG86)

El lenguaje escogido para este procesamiento ha sido Python, debido a su versatilidad en manejo de gran volumen de datos y librerias que permiten ejercer tareas de limpieza, union y verificacion mucho mas sencillo y rapido desde una plataforma en la nube. 

Se escogio las herramientas de AWS tales como Sagemaker (procesamiento online con Python para gran volumen de datos y ETL), S3 (almacenamiento en la nube, RDS (servidor en la nube para bases de datos online) debido a que tiene un periodo de prueba bastante aprovechable en comparacion con otras herramientas cloud tales como Azure y Google Cloud, ademas de que es un arquitectura fuertemente interesante para trabajar y utilizada en el mercado por su innovacion. Ademas, que por la compatibilidad, permite un mejor manejo de errores entre la comunicacion de componentes.
Vale destacar el uso de SageMaker como ETL novedosa que permite tomar informacion directamente para aplicar su insercion a alguna base de datos de manera bastante intuituva por parte de interfaz, y tambien permitiendo aplicar codigo para esto.

El modelo de los datos que se decidio aplicar fue un modelo relacion donde se representaran correctamente las llames primarias del modelo y las foraneas que existen entre ellas. 

[![Screenshot-3.png](https://i.postimg.cc/1zWKnKHH/Screenshot-3.png)](https://postimg.cc/DWXGRLRJ)

Se recomienda hacer una actualizacion de datos estaticos como lo son el SQLITE y los CSV de manera semestral o anual, ya que las novedades en gran volumen se presentan en periodo de tiempos largos (cuando se habla de peliculas) y así, en su momento, es de facil adquisicion y de utilidad de estudio los ratings que se generan a partir de ellos. 

### Diccionario de Datos
**REPORT**|**ServerName**|**DatabaseName**|**TableName**|**SchemaName**|**ColumnName**|**DataType**|**MaxLength**|**IsNull**|**IsIdentity**|**Description**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|directors|dbo|director\_id|varchar|200|NO|NO|Identificador del Director
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|directors|dbo|director\_name|varchar|200|YES|NO|Nombre del Director
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|movie\_id|int|4|YES|NO|Id de la Pelicula en MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|movie\_title|varchar|250|YES|NO|Titulo de la Pelicula en Mubi
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|movie\_release\_year|int|4|YES|NO|Año de Estreno de la Pelicula según MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|movie\_title\_language|varchar|10|YES|NO|Lenguaje de la Pelicula según MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|movie\_popularity|float|8|YES|NO|Popularidad de la Pelicula Según MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|director\_id|varchar|250|YES|NO|Identificador del Director
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|age|varchar|10|YES|NO|Edad permitida para ver la pelicula
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|imdb|varchar|250|YES|NO|Codigo en IMDB
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|rotten\_tomatoes|varchar|250|YES|NO|Aceptacion de la pelicula
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|netflix|int|4|YES|NO|Si la pelicula se encuentra o no en la plataforma. 1=Si  0=No
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|hulu|int|4|YES|NO|Si la pelicula se encuentra o no en la plataforma. 1=Si  0=No
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|prime\_video|int|4|YES|NO|Si la pelicula se encuentra o no en la plataforma. 1=Si  0=No
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movie\_onstreaming|dbo|disney|int|4|YES|NO|Si la pelicula se encuentra o no en la plataforma. 1=Si  0=No
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movies|dbo|movie\_id|int|4|NO|NO|Id de la Pelicula en MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movies|dbo|movie\_title|varchar|200|YES|NO|Titulo de la Pelicula en Mubi
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movies|dbo|movie\_release\_year|varchar|200|YES|NO|Año de Estreno de la Pelicula según MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movies|dbo|movie\_title\_language|varchar|200|YES|NO|Lenguaje de la Pelicula según MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movies|dbo|movie\_popularity|float|8|YES|NO|Popularidad de la Pelicula Según MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|movies|dbo|director\_id|varchar|200|YES|NO|Identificador del Director
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|rating\_id|int|4|NO|NO|Id de Rating
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|rating\_score|float|8|YES|NO|Score dado según la opinion
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|rating\_timestamp\_utc|varchar|200|YES|NO|Fecha de cuando se hizo la opinion
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|critic|varchar|200|YES|NO|Titulo de la critica
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|critic\_comments|varchar|200|YES|NO|Comentarios extras de la critica
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|critic\_likes|varchar|200|YES|NO|Likes que otros usuarios le dan a la critica
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|user\_id|int|4|YES|NO|Id del usuario que realizo la critica
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|ratings|dbo|movie\_id|int|4|YES|NO|Id de la Pelicula en MUBI
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|users|dbo|user\_id|int|4|NO|NO|Id del usuario que realizo la critica
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|users|dbo|user\_trialist|int|4|YES|NO|Si el usuario tiene servicio gratis. 1= Si 0=No
DATADICTIONARY|EC2AMAZ-6P1CNDE|movie\_db|users|dbo|user\_subscriber|int|4|YES|NO|Si el usuario tiene servicio pago.  1= Si 0=No


# 5. Pasos para crear la ETL
- El manejo de logs y los errores, se manejaron directamente dentro de las opciones que ofrecen Amazon Glue y AWS RDS, ya que se tiene una traza muy precisa de todos los errores que pueden ocurrir a nivel de base de datos, como a la hora de ejecutar los pipeline y los codigos realizados. 

- Posteriormente, al terminar la limpieza se guardo todos los resultados de la limpieza (las entidades) en unos JSON 
[![image.png](https://i.postimg.cc/k41hCmz7/image.png)](https://postimg.cc/xJmPGW9Z)

Que lo ideal seria que al ejecutar una serie de jobs, estos carguen la informacion en Glue Data Catalog que es el medio por el cual se hace la insercion a la RDS de SQL Server existente. 

[![image.png](https://i.postimg.cc/nLK66NnL/image.png)](https://postimg.cc/06QWSWMg)
[![image.png](https://i.postimg.cc/GhVwYkMb/image.png)](https://postimg.cc/rK1P2tXH)

# 6. ¿Que hacer si...

## Si los datos se incrementaran en 100x.
Se veria la necesidad de aumentar la capicidad de la nube para el procesamiento a nivel de la ETL, tambien esta la opcion de manejar lamdas y convertir los datos a datos no estrucurados tales como un JSON para un mejor procesamiento de lo mismo. Tambien, se podria crear mas jobs para los nuevos batch de informacion. 

## Si las tuberías se ejecutaran diariamente a las 7 de la mañana.
En este caso del modelo, se tendria que asegurar que la diferencia de informacion no seria tan diferente dia tras dia, ya que el API traeria nueva informacion pero no lo suficiente para poder usar el dataset en general como una tarea de analisis mas profunda. 

## Si la base de datos necesitara ser accedida por más de 100 personas.
Generar una base de datos que permita un alto volumen de consulta tales como un Snowflake o una base de datos NoSQL para la atencion a la demanda que se podria generar en el servidor. Tambien habria que aumentar la capacidad de peticiones y permisos en el servidor. 

