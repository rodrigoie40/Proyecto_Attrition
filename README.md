# Predicción de abandono de empleados
Proyecto Final Integrador — Diplomatura en Ciencia de Datos.
## Objetivo
Comparar modelos de clasificación para predecir `Attrition = Yes`
y mejorar el Recall de una Regresión Logística sin balanceo,
con umbral 0,50, en al menos 8 puntos porcentuales.
Como escenario de priorización, se evalúa qué porcentaje de
abandonos se captura al seleccionar el 20% de empleados con
mayor score.
## Datos
Fuente: [IBM HR Analytics Employee Attrition & Performance](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset).
El dataset contiene 1.470 registros y 35 columnas originales.
Los datos son ficticios.
Para ejecutar el proyecto, descargar y descomprimir el CSV en:
`data/WA_Fn-UseC_-HR-Employee-Attrition.csv`
## Metodología
- División estratificada: 80% entrenamiento y 20% test.
- Exploración sobre entrenamiento.
- Preprocesamiento dentro de pipelines.
- Comparación de Regresión Logística, logística balanceada
  y Random Forest mediante validación cruzada de 5 folds.
- Selección de modelo y umbral mediante predicciones out-of-fold.
- Extensión con dos redes neuronales y validación interna.
- Evaluación final sobre test reservado.
- Bootstrap pareado y estratificado para describir incertidumbre.
## Principales resultados
La configuración principal es una Regresión Logística
sin balanceo, con umbral 0,37.
| Métrica en test | Baseline: umbral 0,50 | Seleccionada: umbral 0,37 |
|---|---:|---:|
| Recall | 34,04% | 44,68% |
| Precision | 61,54% | 55,26% |
| F1 | 0,4384 | 0,4941 |
| Average Precision | 0,5836 | 0,5836 |
| ROC-AUC | 0,8115 | 0,8115 |
| Recall@20% | 61,70% | 61,70% |
La mejora de Recall es de **10,64 puntos porcentuales**:
se detectan 5 abandonos adicionales, a costa de 7 falsas
alertas adicionales.
Al priorizar 59 empleados, se capturan 29 de los 47 abandonos.
El intervalo bootstrap aproximado del 95% de la mejora es
de 2,13 a 19,15 puntos. El objetivo se cumple en este test,
pero no puede garantizarse una mejora poblacional mínima
de 8 puntos.
## Estructura
- `Proyecto_Attrition.ipynb`: análisis completo con salidas.
- `data/`: ubicación del CSV de entrada.
- `results/`: tablas, gráficos y registro del entorno.
- `models/`: metadatos y modelos generados al ejecutar.
- `requirements.txt`: dependencias utilizadas.
- `.gitignore`: exclusiones de archivos locales y binarios.
Los modelos binarios no se incluyen en Git; se regeneran
ejecutando el notebook.
## Ejecución
1. Descargar el CSV y colocarlo en `data/`.
2. Crear y activar un entorno virtual.
3. Instalar las dependencias:
   `python -m pip install -r requirements.txt`
4. Abrir `Proyecto_Attrition.ipynb` en VS Code con las
   extensiones Python y Jupyter.
5. Seleccionar el kernel del entorno y ejecutar todas las
   celdas en orden.
La celda de instalación del notebook es una ayuda inicial.
Para reproducir las versiones registradas, utilizar
`requirements.txt` y omitir las celdas de instalación.
## Entorno utilizado
- Python 3.14.6.
- Versiones de las dependencias en `requirements.txt`.
- TensorFlow registrado: 2.22.0rc0, versión candidata
  a lanzamiento.
La compatibilidad puede variar entre plataformas. Las semillas
fijas no garantizan resultados idénticos de las redes neuronales
entre equipos.
## Limitaciones y uso responsable
El dataset es ficticio y pequeño. Las asociaciones no demuestran
causalidad. Las redes y los modelos clásicos utilizaron esquemas
de validación diferentes.
No se evaluaron exhaustivamente equidad, privacidad, calibración
ni eficacia de intervenciones.
**Este proyecto es un ejercicio académico y no constituye
un sistema validado para tomar decisiones laborales.**