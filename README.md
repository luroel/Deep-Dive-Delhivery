# Delhivery - Análisis de logística y cadena de suministros 
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)

## Índice

- [Indice](#indice)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Instalación](#instalación)
- [Acerca del Dataset](#acerca-del-dataset)
- [Librerías y paquetes](#Librerías-y-paquetes)
- [Insights y hallazgos clave](#insights-y-hallazgos-clave)
- [Acciones tomadas para la limpieza de datos e ingeniería de características](#acciones-tomadas-para-la-limpieza-de-datos-y-la-ingeniería-de-características)
- [Machine learning](#machine-learning)
- [Resumen del conjunto de datos](#resumen-del-conjunto-de-datos)
- [Autor](#Autor)
- [Licencia](#licencia)

  ## Estructura del proyecto

- `data/`: Conjunto de datos de Delhvery.
- `notebooks/`: Análisis en Jupyter Notebooks.
- `output/`: Resultados y visualizaciones.

## Instalación
```bash
   git clone https://github.com/luroel/Deep-Dive-Delhivery.git
```

## Acerca del Dataset
Delhivery es una destacada empresa hindú de cadena de suministros y servicios logísticos, conocida por su amplio alcance y soluciones de entrega eficientes. Delhvery utiliza tecnología sofisticada para ofrecer servicios logísticos integrales, garantizando entregas puntuales y confiables en diversas regiones de la India.

![Texto alternativo](./img/data-cover2.png)

#### Potenciales casos de uso
El análisis de este conjunto de datos ofrece valiosos conocimientos sobre las operaciones logísticas de la empresa, revelando detalles sobre la eficiencia de los viajes, la optimización de rutas, los tipos de transporte y el desempeño de las entregas.

Permite una comprensión integral de cómo se programan y ejecutan los viajes, cómo diferentes factores afectan los tiempos de entrega, y cómo se optimizan las rutas utilizando motores de enrutamiento de código abierto.

Este extenso conjunto de datos es un recurso valioso para mejorar las estrategias logísticas y mejorar el rendimiento de las entregas y tomar decisiones informadas en la gestión de la cadena de suministro.

#### Cómo se puede aportar
Asistir en el desglose y tratamiento de los datos en pipelines de ingeniería:
- Limpieza y manipulación de datos: Limpiar, sintetizar y manipular los datos para extraer características útiles a partir de campos en bruto.
- Interpretación y análisis de datos: Analizar datos sin procesar para apoyar al equipo de ciencia de datos en la construcción de modelos de pronóstico precisos.

#### Perfilado de las columnas
Este conjunto de datos se centra en las operaciones de Delhivery, proporcionando información detallada sobre los viajes y las entregas. Incluye datos de las fases de prueba y entrenamiento, marcas de tiempo de la creación de los viajes, identificadores únicos para los horarios de las rutas y los viajes, tipos de transporte, detalles de carga completa de camiones, información de recolecciones, detalles de origen y destino, horas de inicio y fin de los viajes, tiempos de entrega, distancias y varios campos desconocidos que podrían proporcionar información adicional tras un análisis más profundo.

## Librerías y paquetes
``` python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from geopy.geocoders import Nominatim
import time
import folium
from sklearn.cluster import KMeans
import plotly.express as px
import plotly.graph_objects as go 
import googlemaps
from datetime import datetime
``` 

## Insights y hallazgos clave
1. ### Canitidad de servicios por tipo de ruta

 ![Texto alternativo](./output/op1.png)

2. ### Frecuencia del tiempo y la distancia del trayecto del servicio

![Texto alternativo](./output/op2.png)

3. ### Relación entre la Distancia y el tiempo actual en el Recorrido

![Texto alternativo](./output/op3.png)

4. ### Impacto del tipo de ruta en el tiempo actual de duración del recorrido

![Texto alternativo](./output/op4.png)

5. ### Análisis exploratorio de la ruta Carting

![Texto alternativo](./output/op5.png)

6. ### Análisis exploratorio de la ruta FTL

![Texto alternativo](./output/op6.png)

### Evaluación de la eficiencia en rutas y servicios

7. #### Distribuciones en la evaluación de la eficiencia de las rutas

![Texto alternativo](./output/op8.png)

8. #### Impacto del Cutoff en la duración de los servicios

![Texto alternativo](./output/op9.png)

9. #### Distribución de rutas ineficientes por días de la semana

![Texto alternativo](./output/op10.png)

10. #### Tiempo actual  promedio por estado y diferencia de tiempo por estado en función del actual y el OSRM

![Texto alternativo](./output/op11.png)

11. #### Tiempo actual promedio del servicio por tipo de ruta y diferencia entre el tiempo real y el OSRM por tipo de ruta

![Texto alternativo](./output/op12.png)

12. #### Tiempo actual promedio por fecha y diferencia entre el tiempo actual y el OSRM por fecha

![Texto alternativo](./output/op13.png)

#### Distribución de los datos

- Muchas características muestran distribuciones sesgadas hacia la derecha, particularmente las variables relacionadas con el tiempo y la distancia.
- Se aplicaron transformaciones logarítmicas a las características altamente sesgadas para normalizar sus distribuciones.

#### Correlaciones:

	- Se observaron correlaciones positivas fuertes entre el tiempo real, el tiempo de OSRM y las características relacionadas con la distancia.
	- La variable ‘factor’ muestra correlaciones positivas moderadas con las características relacionadas con el tiempo.

#### Valores Atípicos:

	•	Presencia de valores atípicos en varias características, especialmente en las variables de tiempo y distancia.
	•	Algunos valores extremos pueden representar viajes inusuales o errores en la recopilación de datos.

#### Importancia de las Características:

	- Se seleccionaron características con una correlación > 0.1 con ‘tiempo_real’ para la modelización.
	- Las características predictivas clave probablemente incluyen estimaciones de OSRM, distancias y factores derivados.

#### Variables Categóricas:

	- Se codificaron características categóricas como ‘tipo_de_ruta’, ‘centro_de_origen’ y ‘centro_de_destino’.
	- Estas pueden proporcionar información valiosa sobre las características y patrones de los viajes.

#### Patrones Basados en el Tiempo:

	- Posibilidad de análisis basado en el tiempo utilizando ‘hora_creación_viaje’ y otras características temporales.
	- Podrían revelar patrones en el tráfico o la demanda a lo largo del día/semana.

#### Consideraciones para el Modelo:

	- Dada la presencia de valores atípicos y distribuciones sesgadas, podrían ser adecuados modelos robustos o no paramétricos.
	- La ingeniería de características, como la creación de términos de interacción o características basadas en el tiempo, podría mejorar el rendimiento del modelo.

#### Calidad de los Datos:

	- Algunos valores negativos en las diferencias de tiempo (por ejemplo, ‘tiempo_real_segmento’) sugieren posibles problemas de calidad de los datos.
	-	Puede ser necesario investigar y limpiar estas anomalías.

#### Perspectivas Accionables:

	-	Desarrollar modelos separados para diferentes tipos de rutas o períodos de tiempo para capturar patrones específicos.
	-	Incorporar datos externos (por ejemplo, clima, eventos) para explicar los valores atípicos y mejorar las predicciones.
	-	Implementar una estrategia robusta de detección y manejo de valores atípicos en el proceso de modelización.
	-	Considerar el uso de métodos de ensamble para capturar relaciones complejas en los datos.

## Acciones tomadas para la limpieza de datos e ingeniería de características

Manejo de valores atípicos:

- Se utilizó el método IQR para eliminar valores atípicos de todas las columnas numéricas.
- El resultado fue un conjunto de datos reducido (df_clean).

Corrección de la asimetría:

	•	Se calculó y visualizó la asimetría antes y después de la eliminación de valores atípicos.

Extracción de características basadas en el tiempo:

	•	Se convirtieron las columnas ‘trip_creation_time’ y ‘od_start_time’ al formato datetime.
	•	Se extrajeron la hora, el nombre del día y el nombre del mes de ‘trip_creation_time’.
	•	Se calculó la diferencia de tiempo entre la creación del viaje y el tiempo de inicio.

Creación de características de relación:

	•	distance_time_ratio: actual_distance_to_destination / actual_time
	•	osrm_distance_time_ratio: osrm_distance / osrm_time

Próximos pasos potenciales:

	•	Manejar la asimetría restante mediante transformaciones (por ejemplo, logarítmica, raíz cuadrada).
	•	Codificar las variables categóricas.
	•	Normalizar o estandarizar las características numéricas.
	•	Selección de características basada en análisis de correlación.

## Machine Learning

## Resumen del conjunto de datos
La calidad de este conjunto de datos puede considerarse buena, con un tamaño muestra de alrededor de 145,000 registros y una amplia gama de características.

Los datos están bien estructurados y limpios, sin errores ó inconsistencias relevantes. 

Para mejorar aún más el análisis y el modelado, se debería considerar incluir datos relacionados a otros factores externos que puedan influir en el tiempo de entrega, como los patrones de tráfico, el cierre de carreteras, y aunque es un poco complicado trabajar con variables de clima por su amplío espectro de factores que impiden tener una predicción certera, contar con datos de las condiciones meteorológicas.

Estos datos adicionales pueden contribuir de manera notoria en el aumento de la precisión en las predicciones y la comprensión integral de los factores comunes que afectan los tiempos de entrega de la empresa.

## Autor
Luis Rodríguez Elías


## Licencia

## Contribuciones

Guía para contribuir al proyecto.

## Licencia

Información sobre la licencia del proyecto.
