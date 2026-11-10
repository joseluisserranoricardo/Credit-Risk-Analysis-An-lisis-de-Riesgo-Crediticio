# Credit Risk Analysis | Análisis de Riesgo Crediticio

**Machine Learning · Credit Risk Modeling · XGBoost · Python · Probability of Default**

<img width="1589" height="1082" alt="dashboard_riesgo_calibrado" src="https://github.com/user-attachments/assets/d19f1bda-8c35-41d3-b1cd-ecae30df3d41" />


---

# 🇪🇸 Español

## 1. Descripción del proyecto

Proyecto de análisis de riesgo crediticio mediante técnicas de análisis estadístico y Machine Learning, cuyo objetivo es estimar la probabilidad de incumplimiento de clientes, identificar los principales patrones asociados al default, segmentar la cartera según su nivel de riesgo y cuantificar las pérdidas crediticias esperadas.

El proyecto integra análisis exploratorio de datos, evaluación de variables demográficas y financieras, comparación de diferentes algoritmos de clasificación, calibración de probabilidades y análisis financiero mediante los conceptos de Probability of Default (PD), Loss Given Default (LGD) y Exposure at Default (EAD).

Se desarrolló un proceso progresivo de modelado, comenzando con regresión logística, continuando con Random Forest y finalizando con XGBoost calibrado.

## 2. Objetivos

- Identificar patrones demográficos, financieros y de comportamiento de pago asociados al incumplimiento crediticio.
- Analizar la relación entre variables como edad, sexo, educación, estado civil, historial de pagos y exposición crediticia con la probabilidad de default.
- Comparar diferentes algoritmos de clasificación.
- Estimar la probabilidad de incumplimiento (PD) de cada cliente.
- Calibrar las probabilidades para obtener estimaciones más representativas del riesgo.
- Optimizar el umbral de clasificación considerando los costos de los errores.
- Segmentar la cartera en diferentes niveles de riesgo.
- Estimar las pérdidas crediticias esperadas y generar indicadores financieros para apoyar la toma de decisiones.

## 3. Dataset

Se utilizó el conjunto de datos **Default of Credit Card Clients**, correspondiente a clientes de tarjetas de crédito de Taiwán.

Características principales:

- 30,000 observaciones originales.
- 27 variables predictoras después del preprocesamiento.
- Variable objetivo: `DEFAULT`.
- Clase 0: cliente que no incumple.
- Clase 1: cliente que incumple.

El conjunto contiene información demográfica, características del crédito, historial de pagos, montos facturados y pagos realizados.

### Variables analizadas

| Categoría | Variables | Descripción |
|---|---|---|
| Demográficas | `AGE`, `SEX`, `EDUCATION`, `MARRIAGE` | Edad, sexo, educación y estado civil |
| Crédito | `LIMIT_BAL` | Límite de crédito |
| Historial de pagos | `PAY_0` a `PAY_6` | Comportamiento de pago y retrasos |
| Facturación | `BILL_AMT1` a `BILL_AMT6` | Montos facturados |
| Pagos realizados | `PAY_AMT1` a `PAY_AMT6` | Montos pagados |

## 4. Análisis exploratorio de datos (EDA)

Se realizó un análisis exploratorio para comprender la estructura de la cartera, identificar patrones de incumplimiento y evaluar la relación entre las variables predictoras y la variable objetivo.

### 4.1 Análisis demográfico

Se analizaron las tasas de incumplimiento según:

- Edad de los clientes.
- Sexo.
- Nivel educativo.
- Estado civil.

Se calcularon tasas de incumplimiento por grupos y se compararon las distribuciones de las variables entre clientes que incumplen y aquellos que cumplen sus obligaciones.

### 4.2 Análisis financiero y comportamiento de pago

Se estudió la relación entre el incumplimiento y:

- Límite de crédito (`LIMIT_BAL`).
- Historial de retrasos en pagos (`PAY_0` a `PAY_6`).
- Montos facturados (`BILL_AMT1` a `BILL_AMT6`).
- Montos pagados (`PAY_AMT1` a `PAY_AMT6`).

También se analizaron distribuciones, valores atípicos, correlaciones y tasas de incumplimiento por categorías de variables relevantes.

### 4.3 Principales enfoques del análisis

El análisis permitió estudiar cómo las características demográficas, la exposición crediticia y, especialmente, el historial de pagos se relacionan con el comportamiento de incumplimiento.

Estas relaciones se interpretaron como asociaciones estadísticas y no como relaciones causales.

## 5. Preprocesamiento de datos

Se realizaron las siguientes actividades:

- Revisión de valores faltantes.
- Identificación de registros duplicados.
- Análisis y tratamiento de valores atípicos.
- Revisión de categorías y codificación de variables.
- Selección de variables predictoras.
- División de los datos en entrenamiento, validación y prueba.
- Muestreo estratificado para conservar la proporción de incumplimientos.

La división inicial contempló 24,000 observaciones para entrenamiento y 6,000 para prueba. Posteriormente, el conjunto de entrenamiento se subdividió para realizar la selección del umbral mediante validación.

## 6. Desarrollo y comparación de modelos

Se siguió un proceso progresivo para evaluar diferentes algoritmos de clasificación y mejorar la estimación del riesgo crediticio.

### 6.1 Regresión logística

Se comenzó con un modelo de regresión logística como línea base (*baseline*).

Este modelo permitió establecer una primera aproximación a la clasificación de clientes y estudiar la relación entre las variables predictoras y la probabilidad de incumplimiento.

Su implementación proporcionó un punto de referencia para comparar modelos de mayor complejidad.

### 6.2 Random Forest

Posteriormente, se implementó Random Forest, un algoritmo de aprendizaje basado en conjuntos de árboles de decisión.

Se utilizó para explorar relaciones no lineales entre las variables, capturar interacciones y comparar su capacidad predictiva frente al modelo inicial.

### 6.3 XGBoost

Finalmente, se trabajó con XGBoost, un algoritmo de Gradient Boosting basado en árboles de decisión.

Se realizó optimización de hiperparámetros para mejorar el desempeño predictivo y obtener una mejor aproximación a la probabilidad de incumplimiento.

### 6.4 Calibración de probabilidades

Debido a que el objetivo del proyecto no era únicamente clasificar clientes, sino estimar probabilidades de incumplimiento utilizables en el análisis financiero, se incorporó una etapa de calibración.

Se utilizó:

`CalibratedClassifierCV(method='sigmoid', cv=5)`

La calibración sigmoid permitió ajustar las probabilidades estimadas por el modelo para mejorar su correspondencia con las frecuencias observadas de incumplimiento.

**Modelo final:** XG
