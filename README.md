# 🎬 Análisis del catálogo de Netflix (Python + Power BI)

Proyecto de limpieza, transformación y análisis de un catálogo de títulos de Netflix (~8,790 registros), usando **Python/pandas** para el preprocesamiento de datos y **Power BI** para la visualización interactiva.

## 📂 Estructura del repositorio

```
netflix-data-analysis/
├── README.md
├── data/
│   ├── netflix1.csv                 # Dataset original (sin procesar)
│   └── netflix1_limpio.csv          # Dataset limpio, listo para BI
├── notebooks/
│   └── limpieza_y_transformacion_con_python.ipynb
├── powerbi/
│   └── Netflixset_PB.pbix
└── images/
    ├── dashboard_global.png         # Screenshot página "Análisis global"
    └── dashboard_detalle.png        # Screenshot página "Especificaciones de películas"
```

> 💡 Sube capturas de pantalla de ambas páginas del dashboard a `images/` y enlázalas aquí abajo — así cualquiera que abra el repo entiende el resultado sin tener que abrir Power BI.

## 🎯 Objetivo del proyecto

Explorar el catálogo de Netflix para responder preguntas como:
- ¿Cómo ha evolucionado el número de títulos añadidos por año?
- ¿Qué países producen más contenido?
- ¿Cómo se distribuye el catálogo entre películas y series?
- ¿Cuál es la clasificación (rating) más común?

## 🧹 Limpieza y transformación (Python)

Notebook: [`notebooks/limpieza_y_transformacion_con_python.ipynb`](notebooks/limpieza_y_transformacion_con_python.ipynb)

Pasos aplicados:
1. **Carga y exploración inicial** — revisión de tipos de dato y detección de que el dataset usa `"Not Given"` como relleno en vez de nulos reales.
2. **Eliminación de duplicados** — filas con mismo `title`, `type`, `release_year` y `country`.
3. **Conversión de fechas** — `date_added` de texto a formato `datetime`.
4. **Eliminación de columnas irrelevantes** — se descarta `show_id`.
5. **Extracción de país y género principal** — nuevas columnas `main_country` y `main_genre` a partir del primer valor de las listas separadas por comas.
6. **Corrección de un salto de línea oculto** en el título *"The Memphis Belle: A Story of a Flying Fortress"*, que causaba desalineación de filas al cargar en Power BI.
7. **Exportación** del dataset limpio a `netflix1_limpio.csv`.

## 📊 Análisis y visualización (Power BI)

Archivo: [`powerbi/Netflixset_PB.pbix`](powerbi/Netflixset_PB.pbix)

**Página 1 — Análisis global:**
- KPI de total de títulos
- Evolución de títulos por año de estreno (gráfico de área apilada)
- Top países por cantidad de títulos (columnas + mapa)
- Distribución por clasificación (rating)
- Proporción Película vs. Serie (gráfico circular)
- Segmentador por fecha de adición al catálogo

**Página 2 — Especificaciones de películas:**
- Buscador de título (segmentador)
- Tarjetas de detalle: director, país principal, año de estreno, rating, géneros y duración

**Columnas y medidas DAX creadas:**
- `Duración en minutos o temporadas` — columna calculada que extrae el número de `duration`, manejando tanto `"X min"` (películas) como `"X Season(s)"` (series).
- `Duración Promedio Películas` — medida que calcula el promedio de duración solo para `type = "Movie"`.

## 🛠️ Herramientas utilizadas

- Python 3.12 (pandas)
- Jupyter Notebook
- Power BI Desktop (Power Query M, DAX)

## 🚀 Cómo reproducirlo

1. Clona el repositorio
2. Corre el notebook en `notebooks/` sobre `data/netflix1.csv` para generar el dataset limpio
3. Abre `powerbi/Netflixset_PB.pbix` en Power BI Desktop
4. En Power Query, apunta el origen de datos a tu copia local de `netflix1_limpio.csv`
5. Actualiza el modelo (Refresh)

## 📌 Fuente del dataset

Catálogo público de títulos de Netflix (Kaggle / dataset educativo).

---
*Proyecto realizado con fines de práctica y aprendizaje en análisis de datos.*
