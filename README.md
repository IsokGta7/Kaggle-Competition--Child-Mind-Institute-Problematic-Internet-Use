# Prediccion de el uso problematico del Internet en la poblacion juvenil.

La meta de este proyecto es crear un modelo capaz de identificar el uso problematico del internet en la poblacion juvenil por medio del uso de patrones en los datos de actividad fisica de la poblacion. Al utilizar estos medios mas accesibles planeamos darle acceso a las comunidades de escazos recursos a la oportunidad de detectar el mal uso del internet para promover mejores habitos.

## Tabla de contenidos
- [Planteamiento del problema](#planteamiento-del-problema)
- [Descripcion de los datos](#descripcion-del-dataset)
- [Metrica de evaluacion](#metrica-de-evaluacion)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Metodos](#metodos)
- [Instalacion](#instalacion)
- [Uso](#uso)
- [Aportadores](#aportadores)
- [Lisencia](#lisencia)

---

## Planteamiento del problema

Los metodos actuales para la solucion de la problematica causada por el mal uso del internet requieren de evaluaciones clinicas, lo cual lo hace inaccesible para las comunidades con escazos recursos, barreras logisticas u otras barreras culturales. El proyecto utiliza datos como patrones de actividad fisica, datos demograficos, y evaluaciones fisicas para predecir el **Indice de Gravedad del Deterioro** o **Severity Impairment Index (sii)** en ingles.

---

## Descripcion de los datos

Los datos para este proyecto fueron proporcionados por [Healthy Brain Network (HBN)](https://healthybrainnetwork.org/), fueron obtenidos por medio de un estudio clinico de participantes entre las edades de 5 a 22 años. Los datos fueron obtenidos por medio de 2 metodos principales:

1. **Datos Tabulados:** Informacion demografica, informacion del uso de internet, medidas de actividad fisica, y evaluaciones de salud mental.
2. **Datos de Actigrafia:** Series de tiempo tomadas de acelerometros en dispositivos utilizados por los participantes.


**Datos clave:**
- Datos Demograficos (edad, sexo)
- Uso del Internet (uso diario en horas)
- Medidas Fisicas (ritmo cardiaco, Indice de Masa Corporal, etc.)
- Examenes Fisicos
- Escala de Perturbaciones del Sueño
- Seguimiento de Actividades Basado en Acelerometros (ENMO, anglez, etc.)

Para una descripcion mas detallada, revisar el archivo `data_dictionary.csv`.

---

## Metrica de Evaluacion

El proyecto utilizara el metodo **Quadratic Weighted Kappa (QWK)** como una evaluacion metrica. Este metodo evalua la concordancia entre los valores reales y los valores predichos, tomando en cuenta el grado de desacuerdo. Una puntuacion QWK de 1 indica una concordancia perfecta, mientras que una puntuacion QWK de 0 indica una concordancia aleatoria.

Formula:  
![QWK Formula](https://miro.medium.com/v2/resize:fit:1350/1*PwYp7fa2DFgCYdjd5awMuQ.png)

---

## Estructura del Proyecto

```plaintext
├── data/
│   ├── train.csv              # Datos de entrenamiento tabulares
│   ├── test.csv               # Datos de prueba tabulares
│   ├── series_train.parquet   # Datos de entrenamiento de series temporales de actigrafía
│   ├── series_test.parquet    # Datos de prueba de series temporales de actigrafía
├── notebooks/
│   ├── exploratory_analysis.ipynb  # Exploracion y visualizacion de datos
│   ├── preprocessing.ipynb         # Limpieza y preprocesamiento de datos
│   ├── modeling.ipynb              # Creacion y evaluacion del modelo
├── src/
│   ├── data_loader.py         # Scripts para cargar y preprocesar datos
│   ├── feature_engineering.py # Métodos de extracción de características
│   ├── train_model.py         # Estructura del entrenamiento del modelo
│   ├── evaluate.py            # Evaluacion con QWK
├── results/
│   ├── model_predictions.csv  # Formato de entrega
├── README.md
├── requirements.txt
└── LICENSE
```


---

## Metodos

### Analisis y Exploracion de Datos
- Resúmenes estadísticos y análisis de correlación
- Visualización de series temporales de características del acelerómetro (ENMO, anglez, etc.)
- Agrupamiento de datos por edad, género y niveles de actividad física

### Preprocesamiento de Datos
- Manejo de datos faltantes mediante técnicas de imputación
- Normalizar y escalar datos numéricos
- Agregar datos de series temporales en características significativas
- Eliminar períodos sin desgaste de los datos de actigrafía

### Desarrollo del Modelo
- **Tipo de problema**: Clasificación de múltiples clases (0 = Ninguno, 1 = Leve, 2 = Moderado, 3 = Grave)
- **Modelos de referencia**: Regresión logística, Bosque aleatorio
- **Modelos avanzados**: Potenciación de gradiente (p. ej., XGBoost, LightGBM), Redes neuronales
- **Ajuste de hiperparámetros**: Utilice optimización bayesiana o búsqueda en cuadrícula con validación cruzada
- Análisis de importancia de características para la interpretabilidad

### Visualizacion
- Histogramas y diagramas de caja para la distribución de datos
- Mapas de calor de correlación
- Gráficos de series temporales de características del acelerómetro
- Gráficos de barras de importancia de características

---

## Instalacion

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/problematic-internet-use.git
   cd problematic-internet-use
