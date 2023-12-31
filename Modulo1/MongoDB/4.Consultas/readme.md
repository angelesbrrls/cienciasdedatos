# Consultas sobre una colección

- [x] **Ordenar las canciones por año empezando por el más actual** (incluimos ordenamiento por cantante)

- Se utiliza la opción de Sort, para realizar el ordenamiento, primero por año en orden descendente, como segundo ordenamiento artist por orden ascendente

```other
{year: -1, artist: 1}
```

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/20.1.png)
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/20.2.png)

_ _ _

- [x] **¿Cuál ha sido la canción más escuchada (mayor popularidad)?**

- Se utiliza la opción project para incluir los campos que se requieren mostrar y sort en orden descendente para ordenar desde el de mayor popularidad, como último filtro se hace uso de limit 1.

```other
{title: 1, artist: 1, popularity: 1}
```

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/21.png)

De esta manera, obtenemos la canción más escuchada
_ _ _

- [x] **¿Cuál ha sido la canción más escuchada del año 2020 ( mayor popularidad  2020)?**

- Se utiliza Filtro para realizar la condición del año que se requiere obtener, la opción project para incluir los campos que se requieren mostrar y sort en orden descendente para ordenar desde el de mayor popularidad, como último filtro se hace uso de limit 1.

![Captura de pantalla 2023-06-22 a la(s) 16.18.49.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/22.png)

De este manera, se obtiene la canción más escuchada de un año determinado.

```other
filter: {year: 2020}
project: {title: 1, artist: 1, popularity: 1}
sort: {popularity: 1}
limit: 1
```
_ _ _

- [x] **¿Cuáles son las 10 canciones más positivas?** 

```other
filter: 
project: {title: 1, artist: 1, top_genre: 1, valence: 1}
sort: {valence: -1}
limit: 10
```

- Se utiliza la opción project para incluir los campos que se requieren mostrar y sort en orden descendente para ordenar  el campo valence ( mayor a menor), finalmente se hace uso de limit 10.

![Imagen 42](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/42.png)
![Imagen 43](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/43.png)

De este manera, se obtiene las 10 canciones más positivas del set de datos.

- - -

- [x] **¿Cuáles son las 5 canciones con mayor rítmo (con más probalidad de que se pueda bailar)?** 

```other
filter: 
project: {title: 1, artist: 1, top_genre: 1, danceability: 1}
sort: {danceability: -1}
limit: 5
```

- Se utiliza la opción project para incluir los campos que se requieren mostrar y sort en orden descendente para ordenar  el campo danceability del  mayor al menos valor, finalmente se hace uso de limit 5.

![Imagen 44](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/44.png)

De este manera, se obtiene las 5 canciones con más probabilidad de ser bailable del set de datos.

- - -

- [x] **Obtener los primeros tres años con mayor número de lanzamientos**

- Para realizar esta consulta, hacemos uso de las agregaciones. El Pipeline que utilizamos es **::$group → $sort → $limit::**. A continuación describimos cada uno.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/23.png)

> Stage 1. $group, se agrupan los documentos por año y se suma la cantidad de registros por cada agrupación.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/24.png)

> Stage 2. $sort, la cantidad se ordena de manera descendente para obtener el valor con mayor cantidad.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/25.png)

> Stage 3. $limit, se limita a los primeros años con mayor cantidad.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/26.png)

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/40.png)

De esta manera, obtenemos los tres años con mayor cantidad de lanzamientos.
_ _ _

- [x] **¿Cuál es el género musical con mayor popularidad?**

- Para realizar esta consulta, hacemos uso de las agregaciones. El Pipeline que utilizamos es **::$group → $sort → $limit::**. A continuación describimos cada uno.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/27.png)

> Stage 1. $group, se agrupan los documentos por genero y se suma por cada uno de estos.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/28.png)

> Stage 2. $sort, se ordena de forma descendente para obtener el genero con mayor cantidad.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/29.png)

> Stage 3. $limit, con el límite 1 se obtiene únicamente el primero valor

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/30.png)

De esta manera, se obtiene el género musical con mayor popularidad.

- - -

- [x] **Creación de una vista - Mostrar los 10 primeros géneros con mayor popularidad**

- Para crear una vista en la pestaña de agregaciones, seleccionamos guardar y hacemos click en el botón create view.
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/45.png)

-  Ingresamos el nombre de la vista.
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/46.png)

- Se creará la vista.
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/47.png)


_ _ _

- [x] **¿Cuál es el promedio de tiempo de duración de las canciones (en minutos) ?**

- Para realizar esta consulta, hacemos uso de las agregaciones. El Pipeline que utilizamos es **::$group → $addFields → $addFields::**. A continuación describimos cada uno.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/31.png)

> Stage 1. $group, se agrupa para obtener el total de los documentos y se suma los segundos de duración de cada canción.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/32.png)

> Stage 2. $addFields, se agrega un campo nuevo para calcular el promedio en segundos de todas las canciones.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/33.png)

> Stage 3. $addFields, se agrega un nuevo campo para calcular el promedio en minutos.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/34.png)

De esta manera, será posible obtener el promedio de las canciones de la colección music en minutos.

_ _ _

- [x] **¿Cuál es la cantidad total de cantantes (sin repetir)?**

- Para realizar esta consulta, hacemos uso de las agregaciones. El Pipeline que utilizamos es **::$group → $addFields → $project::** . A continuación describimos cada uno.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/35.1.png)

> Stage 1. $group, agrupamos y limpiamos los documentos, obteniendo los artistas no repetidos.

```other
El operador $addToSet agrega valores en un array a menos de que el valor ya exista.
 (en caso de que ya exista el valor no lo agregará).
```

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/36.1.png)

> Stage 2. $addFiels, se crea un nuevo campo para calcular el total del array de cantantes.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/37.1.png)

> Stage 3. $project, se muestra el total de cantantes y la lista de cada uno de ellos.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/38.1.png)

De esta manera, podremos obtener el total de los cantantes de la lista de canciones sin repetir.

![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/41.1.png)
- - -

- [x] **Creación de la vista cantantes**

- Para crear una vista en la pestaña de agregaciones, seleccionamos guardar y hacemos click en el botón create view.
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/51.png)

-  Ingresamos el nombre de la vista.
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/48.png)

- Se creará la vista.
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/49.png)
![Image.png](https://github.com/angelesbrrls/cienciasdedatos/blob/main/Modulo1/MongoDB/assets/50.png)
_ _ _



[Anterior](https://github.com/angelesbrrls/cienciasdedatos/tree/main/Modulo1/MongoDB/3.Operaciones) | [Menú](https://github.com/angelesbrrls/cienciasdedatos/tree/main/Modulo1/MongoDB)