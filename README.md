# Taller 2 – Ciencia de Datos Aplicada

## Predicción de Precios de Apartamentos en Bogotá

### Integrantes

* Lina Ojeda – 202112324 – [l.ojedaa@uniandes.edu.co](mailto:l.ojedaa@uniandes.edu.co)
* William Toro – 201112526 – [wy.toro993@uniandes.edu.co](mailto:wy.toro993@uniandes.edu.co)

---

# Estructura del repositorio

Taller_2 
* Taller_2.ipynb                # Notebook principal
* Resumen Ejecutivo.pdf         # Resumen ejecutivo del taller 
* Generación de valor.pdf       # Análisis económico del modelo
* Costo_ambiente_AWS_cloud.pdf  # Costos aproximados del ambiente en la nube aws
* apartamentos.csv              # Dataset de precios de apartamentos
* Diccionario de datos - apartamentos.html      # Diccionario de variables
  
README.md

---

# Objetivo del proyecto

Desarrollar un modelo de Machine Learning que estime el precio de venta de apartamentos en Bogotá utilizando variables estructurales, geográficas y categóricas.

El modelo busca:

* Reducir tiempos del proceso de valoración inmobiliaria.
* Mejorar la precisión al estimar precios.
* Identificar las variables más determinantes del valor de un inmueble.
* Servir como base para futuras herramientas analíticas de HabitAlpes.

---

# Metodología general 

## 1. Preparación y enriquecimiento de datos (Taller_2.ipynb)

Incluye:

* Limpieza de datos, imputación y estandarización.
* Agrupación de categorías con baja frecuencia.
* Cálculo de distancias geográficas mediante la fórmula de Haversine:

  * Distancia al centro de la ciudad.
  * Distancia al aeropuerto.
  * Distancia a la terminal de transporte.
* Creación de la variable de vecinos más cercanos mediante BallTree:
* Promedio del precio por metro cuadrado de los 50 vecinos más cercanos.

Estas transformaciones no fueron usadas en ambos modelos. Sirvieorn para comparar los modelos y si diferentes transformaicones mejoraban o no las predicciones.

## 2. Modelos evaluados

Se evaluaron dos modelos principales:

### CatBoost Regressor

* Manejo nativo de variables categóricas.
* Buen rendimiento en datasets con alta heterogeneidad.

### XGBoost Regressor

* Modelo robusto en boosting.
* Requiere codificación de categorías y múltiples pasos de preprocesamiento.

Ambos modelos fueron entrenados con particiones Train, Validation y Test.

---

# Resultados principales

Métricas del mejor modelo (XGBoost):

| Métrica | Validación     | Test           |
| ------- | -------------- | -------------- |
| MAE     | 62.9 millones  | 63.7 millones  |
| RMSE    | 101.1 millones | 106.7 millones |
| R²      | 0.91           | 0.89           |
| MAPE    | 10.3 %         | 10.4 %         |

Interpretación:

* El modelo tiene un error relativo del 10 %.
* R² cercano a 0.90 indica buena capacidad explicativa.
* Desempeño estable entre validación y test, lo que evidencia buena generalización.

---

# Interpretabilidad del modelo

## SHAP

Permitio identificar las variables más influyentes:

1. Área
2. Administración
3. Ubicación (latitud y longitud)
4. Antigüedad
5. Precio histórico de vecinos cercanos
6. Estrato y parqueaderos

También se incluyeron explicaciones locales con gráficos tipo waterfall.

## LIME

Se utilizó para interpretar predicciones puntuales dentro de vecindarios locales del espacio de características. 

---

# Generación de valor sobre el mejor modelo 

El uso del modelo de predicción genera beneficios frente al proceso manual de avalúo:

* **Ahorro operativo:** el tiempo por avalúo se reduce de 6 a 1 hora, lo que equivale a **291 horas ahorradas al mes** en 500 avalúos, con un beneficio de aproximadamente **$2.770.833 COP mensuales**.
* **Costo por errores:** el 31% de los casos presentan subestimación mayor a $20M, lo que requiere revisión presencial con un costo de **$57.000 COP por avalúo**. Aun así, el gasto es menor que el ahorro generado.
* **Costo del proyecto:** el desarrollo y despliegue inicial del modelo cuesta alrededor de **$25.000.000 COP**. La operación mensual en AWS cuesta cerca de **$11.000.000 COP** (según cotización incluida en el documento).
* **Retorno de inversión:** la inversión inicial se recupera en aproximadamente **7 meses**, y desde ese punto el ahorro neto mensual genera valor directo para HabitAlpes.

**Conclusión:** El modelo es rentable, acelera el proceso de valoración y constituye una herramienta escalable con impacto económico positivo.

---

# Resultados y conclusiones generales

* XGBoost fue el modelo con mejor desempeño.
* La ubicación y el área son las variables más relevantes.
* El modelo permite automatizar y estandarizar la valoración de inmuebles.
* La solución es escalable y con impacto económico positivo.

---

# Requisitos y ejecución

## Dependencias

Python 3.9+ y librerías:

* pandas
* numpy
* scikit-learn
* seaborn
* catboost
* xgboost
* shap
* lime

Google Colab ya incluye la mayoría.

## Cómo ejecutar

0. instalar todas las dependencias necesarias con !pip instal nombre_dependencia 
1. Abrir **Taller_2.ipynb**. Preferiblemente en colab
2. Ejecutar todas las celdas en orden.
3. Revisar métricas, gráficos y conclusiones.


