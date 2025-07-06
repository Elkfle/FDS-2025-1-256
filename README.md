# Trending Youtube Video Statistics

# Integrantes:
- Colfer Mendoza, Carlos Alejandro (U20241B820)
- Chavez Merino, Cielo Luwidka (U20191E443)
- Cabrera Díaz, Marco Antonio Luciano (U202318540)

## Objetivo del proyecto
Tenemos por objetivo analizar y comprender las tendencias de los videos en YouTube de Alemania con el fin de extraer información clave que permita al cliente de la consultora tomar decisiones de marketing en base a estos datos. 

Los requerimientos que buscamos responder se dividen en las siguientes categorías:

### Por categorías de videos
- ¿Qué categorías de videos son las de mayor tendencia?  
- ¿Qué categorías de videos son los que más gustan? ¿Y las que menos gustan?  
- ¿Qué categorías de videos tienen la mejor proporción (ratio) de “Me gusta” / “No me gusta”?  
- ¿Qué categorías de videos tienen la mejor proporción (ratio) de “Vistas” / “Comentarios”?  

### Por el tiempo transcurrido
- ¿Cómo ha cambiado el volumen de los videos en tendencia a lo largo del tiempo?  

### Por canales de YouTube
- ¿Qué canales de YouTube son tendencia más frecuentemente?  
- ¿Y cuáles con menos frecuencia?  

### Por la geografía del país
- ¿En qué Estados se presenta el mayor número de “Vistas”, “Me gusta” y “No me gusta”?  

### Preguntas adicionales
- ¿Los videos en tendencia son los que mayor cantidad de comentarios positivos reciben?  
- ¿Es factible predecir el número de “Vistas” o “Me gusta” o “No me gusta”?  

### Propósito Final

Respondiendo estas preguntas, pretendemos:
- Determinar patrones de comportamiento del contenido en distintas regiones y culturas.  
- Identificar preferencias del público por temática, canal o formato.  
- Detectar tendencias temporales útiles para campañas de contenido viral.  
- Reconocer factores predictivos que puedan anticipar el éxito de un video.

## Descripción del dataset
| **Campo**               | **Descripción**                                                                 |
|-------------------------|---------------------------------------------------------------------------------|
| `video_id`              | Identificador único del video en YouTube.                                      |
| `trending_date`         | Fecha en la que el video apareció en tendencias.                               |
| `title`                 | Título del video.                                                               |
| `channel_title`         | Nombre del canal que publicó el video.                                         |
| `category_id`           | Código numérico que indica la categoría del video.                             |
| `publish_time`          | Fecha y hora exacta en la que el video fue publicado.                          |
| `tags`                  | Etiquetas asociadas al video.                                                  |
| `views`                 | Número total de visualizaciones.                                               |
| `likes`                 | Número total de "Me gusta".                                                    |
| `dislikes`              | Número total de "No me gusta".                                                 |
| `comment_count`         | Número de comentarios recibidos.                                               |
| `thumbnail_link`        | URL de la miniatura del video.                                                 |
| `comments_disabled`     | Indica si los comentarios están deshabilitados (booleano).                     |
| `ratings_disabled`      | Indica si las valoraciones están deshabilitadas (booleano).                    |
| `video_error_or_removed`| Indica si el video fue eliminado o tiene un error.                             |
| `state`                 | Nombre del Estado perteneciente al país.                                       |
| `lat`                   | Latitud geográfica de ubicación del Estado.                                    |
| `lon`                   | Longitud geográfica de ubicación del Estado.                                   |
| `geometry`              | Coordenadas de las geometrías donde se ubica el Estado en el planeta.          |

## Conclusiones

- La organización inicial del dataset facilitó el análisis, ya que no se encontraron datos nulos en columnas clave como `views`, `likes`, `dislikes`, `comment_count`, `category_id` y `channel_title`.
- No se intervinieron los valores de la columna `description`, ya que es válido que un video no tenga descripción.
- No se detectaron outliers significativos que alteraran la calidad del análisis.
- Se añadió una nueva columna `category_name` para traducir los `category_id` a nombres de categoría, mejorando la comprensión de los resultados.
- La columna `geometry` fue correctamente transformada al tipo de dato adecuado, lo que permitió su uso con la librería **GeoPandas** para responder consultas espaciales sobre vistas, likes y dislikes por estado.
- Para la predicción de visualizaciones, se utilizó la técnica de regresión **XGBoost**, altamente efectiva para problemas de datos tabulares.
- El modelo obtuvo un **R² de 95.18%**, lo que indica una excelente capacidad para explicar la variabilidad en las visualizaciones.
- Los errores obtenidos fueron:
  - **MAE** ≈ 53,694 vistas (error medio absoluto).
  - **RMSE** ≈ 527,171 vistas (error cuadrático medio).
- Ambos valores son razonables dado que algunos videos tienen millones de vistas, y el modelo mostró buena precisión general.
- Los gráficos de dispersión y de comparación real vs. predicho demostraron una adecuada alineación entre los valores estimados y reales, validando la calidad del modelo y sugiriendo que solo algunos videos con vistas extremadamente altas presentan mayores desviaciones.
