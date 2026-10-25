# Proyecto Estadísticas de YouTube | Avances IV

**Semana 10 · Informe final de resultados y evaluación**

**Autores:** Jhon Eduard Tinjaca Cruz Y Julián David Silva Guzmán
**Entorno:** Google Colab · Python  
**Dataset:** [YouTube Statistics (Kaggle)](https://www.kaggle.com/datasets/advaypatil/youtube-statistics)

## Descripción

Este proyecto estudia la relación entre los comentarios de vídeos de YouTube y su desempeño. La solución evolucionó desde un modelo directo basado en TF-IDF y Ridge hasta una arquitectura experimental de dos capas:

1. **Análisis de sentimiento:** clasificación de comentarios mediante TF-IDF y regresión logística.
2. **Predicción del desempeño:** agregación de señales por vídeo para estimar `log(1 + Views)` y clasificar el impacto como alto o bajo.

La entrega **Avances IV** presenta la evaluación final respecto al diseño inicial, los resultados obtenidos, los retos resueltos, las lecciones aprendidas y las limitaciones pendientes.


- **Notebook:** consolida resultados documentados, genera tablas y visualizaciones comparativas y permite exportar evidencias CSV en un ZIP.

> El notebook de Avances IV **no vuelve a entrenar los modelos**: utiliza métricas registradas en la ejecución de la etapa III V2. Para repetir el entrenamiento completo, consultar el Colab de la etapa III.

## Resultados documentados

| Tarea | Escenario / modelo | Métrica | Resultado |
|---|---|---|---:|
| Sentimiento | TF-IDF + Regresión Logística | F1 macro | 0,675 |
| Sentimiento | TF-IDF + Regresión Logística | Accuracy | 0,759 |
| Sentimiento (submuestra) | RoBERTa | F1 macro | 0,8526 |
| Regresión | A: Gradient Boosting | R² | 0,5448 |
| Regresión | B: XGBoost | R² | 0,6521 |
| Clasificación | A: XGBoost | F1 / AUC | 0,7824 / 0,8602 |
| Clasificación | B: XGBoost | F1 / AUC | 0,8242 / 0,9068 |
| Clasificación | B: Random Forest | AUC | 0,9099 |

**Escenario A:** características derivadas de comentarios.  
**Escenario B:** comentarios más antigüedad del vídeo.

Los errores RMSE y MAE de regresión se interpretan en escala logarítmica. El resultado de RoBERTa corresponde a una submuestra y no es directamente equivalente al del pipeline completo. La diferencia de R² entre los mejores modelos A y B es descriptiva y no demuestra causalidad.

**Fuente de las cifras:** `Modelo_NLP_YouTube_Colab_III_V2.ipynb - Colab.pdf` (salida de ejecución de la etapa III).

## Evolución y retos

| Aspecto | Diseño inicial | Solución documentada |
|---|---|---|
| Arquitectura | Pipeline TF-IDF + Ridge | Dos capas: sentimiento y desempeño |
| Objetivo | Predicción de Views | Regresión de log(1+Views) y clasificación alto/bajo |
| Modelos | Baseline y Ridge | Comparación de modelos lineales y ensambles |
| Evaluación | Métricas de regresión | Validación agrupada para sentimiento y métricas por tarea |

Principales retos abordados:

- **Desbalance de sentimiento:** ponderación de clases y uso de F1 macro.
- **Dependencia entre comentarios del mismo vídeo:** `GroupKFold` por identificador de vídeo y predicciones fuera de muestra.
- **Asimetría de visualizaciones:** transformación `log(1 + Views)`.
- **Calidad de datos:** limpieza y eliminación de registros duplicados.
- **Selección de algoritmos:** contraste entre baselines, Ridge, Random Forest, Gradient Boosting y XGBoost.
- **Coste computacional:** evaluación exploratoria de RoBERTa sobre una submuestra.

## Ejecución en Google Colab

1. Abrir [Google Colab](https://colab.research.google.com/).
2. Seleccionar **Archivo → Subir cuaderno** y cargar `Proyecto_Estadisticas_YouTube_Avances_IV_Final.ipynb`.
3. Ejecutar las celdas en orden, preferiblemente con **Entorno de ejecución → Ejecutar todas**.
4. Revisar las tablas, la comparación de R² y las conclusiones.
5. En la sección de exportación, descargar `Evidencias_Avances_IV.zip`, que contiene CSV y un archivo JSON de procedencia.

El notebook utiliza `pandas`, `numpy` y `matplotlib` y está orientado al entorno estándar de Colab. La ejecución de este notebook **no requiere descargar el dataset**, porque presenta y analiza resultados históricos ya documentados.

## Enlaces de etapas anteriores

- [Repositorio GitHub de Avances III](https://github.com/juliandavidsilvaguzman-star/Proyecto-estad-sticas-de-Youtube-Avances-III.git)
- [Notebook Google Colab de Avances III](https://colab.research.google.com/drive/1vELCMrSn1MQv2OmY1iZcn_TmtJMsE4pF?usp=sharing)

**Pendiente para la entrega IV:** publicar los archivos de esta etapa en GitHub y sustituir o complementar los enlaces anteriores con la URL del nuevo repositorio y el nuevo cuaderno compartido.

## Limitaciones y estado del producto

La evidencia disponible respalda la experimentación y evaluación de modelos, pero **no permite afirmar que exista** una API o interfaz pública desplegada, un servicio de inferencia en la nube, monitorización operativa ni pruebas con usuarios reales. Estas capacidades deberán demostrarse por separado si se presentan como producto final consumible.

Asimismo, los comentarios se generan después de la publicación del vídeo. Por tanto, los resultados se interpretan como asociaciones predictivas, no como predicción previa a la publicación ni como efectos causales.

## Lecciones aprendidas

- Una validación correcta debe respetar la agrupación natural de los datos.
- Las métricas deben elegirse según la tarea y el desbalance de clases.
- La complejidad del algoritmo no garantiza mejores resultados en todos los componentes.
- El contexto temporal puede mejorar la predicción observada, pero cambia el escenario evaluado.
- La reproducibilidad de un experimento no equivale a disponer de un producto desplegado.

## Trabajo colaborativo

Proyecto elaborado por **Julián David Silva Guzmán** y **Jhon Eduard Tinjaca Cruz**. Para fortalecer la evidencia de colaboración de la entrega final, se recomienda conservar en GitHub el historial de commits, revisiones, incidencias y decisiones técnicas. No se atribuyen responsabilidades individuales sin evidencia documental.

## Referencias

- Dataset: [YouTube Statistics, Kaggle](https://www.kaggle.com/datasets/advaypatil/youtube-statistics).
- Evidencia de modelos: `Modelo_NLP_YouTube_Colab_III_V2.ipynb - Colab.pdf`.
- Documentación de etapa III: `Informe_Etapa3_Modelo_NLP_YouTube_Final 1.docx`.
- Informe de cierre: `Informe_Proyecto_Estadisticas_YouTube_Avances_IV.docx`.
