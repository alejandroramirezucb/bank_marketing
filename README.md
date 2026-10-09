# Bank Marketing

Experimento comparativo de clasificación binaria sobre el conjunto *Bank Marketing* del UCI Machine
Learning Repository. Se comparan cuatro modelos (SVM, árbol de decisión, Random Forest y XGBoost) en
rendimiento y en costo computacional (tiempo de entrenamiento y de predicción).

## Estructura del repositorio

```
.
├── notebooks/           cinco notebooks numerados, ejecutados y con resultados guardados
├── splits/              gráficos generados por los notebooks (PNG)
├── resultados_modelos.json, tabla_comparativa.csv, entorno.json
├── requirements.txt
└── README.md
```

## Notebooks

Se ejecutan en orden la primera vez, porque cada uno consume archivos que genera el anterior.

| Notebook | Contenido | Requiere |
|---|---|---|
| `01_formulacion_y_variables` | Formulación del problema, objetivos y descripción de variables | Nada |
| `02_estadistica_descriptiva` | Distribuciones, atípicos y correlaciones | Nada |
| `03_calidad_desbalance_y_preprocesamiento` | Calidad de datos, desbalance, partición y escalado | Nada |
| `04_entrenamiento_y_evaluacion_de_modelos` | Ajuste y evaluación de los cuatro modelos | Notebook 03 |
| `05_comparacion_y_conclusiones` | Comparación, selección del modelo y conclusiones | Notebooks 03 y 04 |

## Ejecución

### Google Colab

1. Abrir [colab.research.google.com](https://colab.research.google.com) y subir el notebook (`Archivo → Subir cuaderno`).
2. Ejecutar con `Entorno de ejecución → Ejecutar todo`.

La primera celda monta Google Drive y trabaja en `MyDrive/bank_marketing`. Si el montaje falla, la
ejecución se detiene en lugar de escribir en el disco temporal de Colab.

### Local

```bash
python -m venv .venv
source .venv/bin/activate        # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab notebooks/
```

Fuera de Colab los notebooks escriben en la raíz del repositorio, sin importar si se abren desde la
raíz o desde `notebooks/`. Probado con Python 3.12, scikit-learn 1.8 y xgboost 3.4.

## Datos

Los notebooks descargan el conjunto automáticamente desde el repositorio UCI, sin credenciales:

```
https://archive.ics.uci.edu/static/public/222/bank+marketing.zip
```

Contiene 45.211 clientes y 16 variables predictoras. La variable `duration` se excluye porque solo se
conoce cuando la llamada ya terminó.

## Reproducibilidad

- Semilla fija (`RANDOM_STATE = 42`) en la partición y en todos los modelos.
- Los tiempos dependen de la máquina. El entorno de medición queda registrado en `entorno.json`.
- El notebook 04 tarda entre 35 y 50 minutos, por el ajuste repetido del SVM y del Random Forest.

## Archivos generados

Estos archivos se crean al ejecutar los notebooks y no se versionan: `datos_preparados.joblib`,
`modelos/`, `puntajes_test.npz` y `bank-full.csv`.

## Referencia

Moro, S., Rita, P. y Cortez, P. (2014). *A data-driven approach to predict the success of bank
telemarketing*. Decision Support Systems, 62, 22-31.
