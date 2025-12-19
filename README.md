# MLZyfra
# ⛏️ Optimización de Recuperación de Oro - Machine Learning para Zyfra

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)

##  Descripción del Proyecto
Este proyecto consiste en el desarrollo de un modelo de Machine Learning para la empresa minera **Zyfra**. El objetivo es predecir la cantidad de oro recuperado del mineral de oro para optimizar la producción y ayudar a identificar parámetros de operación ineficientes.

Se predicen dos objetivos clave:
1.  **Recuperación de la salida bruta (Rougher):** Etapa inicial de flotación.
2.  **Recuperación de la salida final (Final):** Después de todas las etapas de purificación.

La evaluación final se basa en una métrica personalizada: **sMAPE Final (Error Porcentual Absoluto Medio Simétrico)**.

---

##  Pipeline de Datos y EDA
El proceso de purificación pasa por varias etapas: Flotación, Purificación Primaria y Purificación Secundaria.



### Pasos Clave:
* **Verificación de Cálculos:** Se recalculó manualmente la recuperación (`recovery`) para validar la integridad de los datos mediante el Error Absoluto Medio (EAM).
* **Análisis de Brechas (Features):** Se identificaron y manejaron las características ausentes en el conjunto de prueba que sí estaban en el de entrenamiento.
* **Concentración de Metales:** Se analizó cómo cambian las concentraciones de **Au (Oro)**, **Ag (Plata)** y **Pb (Plomo)** en cada etapa.
* **Tamaño de Partículas:** Se verificó que las distribuciones del tamaño de partículas de alimentación fueran similares en ambos conjuntos (train y test) para evitar sesgos en el modelo.
* **Tratamiento de Anomalías:** Eliminación de valores atípicos en las concentraciones totales para mejorar la robustez del modelo.

---

## 🧮 Métrica Personalizada: sMAPE
Implementamos la fórmula sMAPE para evaluar el modelo, la cual trata de igual manera los errores por exceso y por defecto:

$$sMAPE = \frac{1}{n} \sum_{i=1}^{n} \frac{|y_i - \hat{y}_i|}{(|y_i| + |\hat{y}_i|)/2} \times 100$$

El puntaje final es un promedio ponderado:
$$sMAPE\ Final = 25\% \times sMAPE(rougher) + 75\% \times sMAPE(final)$$

---

##  Desarrollo de Modelos
Se compararon múltiples modelos de regresión utilizando **Validación Cruzada**:

1.  **Regresión Lineal:** Modelo base (baseline).
2.  **Árbol de Decisión Regressor:** Ajustado por profundidad.
3.  **Bosque Aleatorio (Random Forest) Regressor:** Optimizado mediante ajuste de hiperparámetros.

### Resultados:
| Modelo |
| :--- |
| sMAPE rougher: 1.8162870021414323 |
| sMAPE final stage: 2.8021734106359526 |
| sMAPE ponderado total: 2.555701808512323 |

---

##  Hallazgos Principales
* **Concentración de Oro (Au):** Aumenta significativamente en cada etapa de purificación, validando la eficacia del proceso.
* **Concentración de Plata (Ag):** Disminuye conforme avanza el proceso, mientras que el **Plomo (Pb)** tiende a estabilizarse.
* El modelo de **Bosque Aleatorio** ofreció el rendimiento más estable y el error más bajo.
* La limpieza de anomalías y el ajuste de características fueron pasos críticos para alcanzar la métrica objetivo.

---

## 📁 Estructura del Repositorio
* `gold_recovery_full.ipynb`: Notebook principal con el análisis y modelado.
* `README.md`: Documentación del proyecto.

##  Cómo ejecutar
1. Clona este repositorio.
2. Asegúrate de tener instaladas las librerías `scikit-learn`, `pandas` y `matplotlib`.
3. Ejecuta el notebook `gold_recovery_full.ipynb`.
4. Junta los 2 archivos csv, leer nota.

**NOTA**
Este proyecto incluye 2 csv's pero existe otro que junta 2 dataframes, por motivos de practicidad y fluidez del repositorio, decidí no incluirlo en las descargas, ya que es un archivo grande.
