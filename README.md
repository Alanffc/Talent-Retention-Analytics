# 📊 HR Analytics: Talent Retention & Salary Equity (Caso 1)

## 🎯 Objetivo del Caso
Asumiendo el rol de **People Analytics Scientist** en una corporación multinacional, este proyecto aborda dos problemas críticos de Recursos Humanos mediante modelos de Machine Learning:

1.  **Estimación Salarial (Regresión):** Predecir el ingreso mensual (`MonthlyIncome`) de los empleados para apoyar auditorías internas, detectar anomalías y garantizar la equidad salarial dentro de la organización.
2.  **Alerta Temprana de Fuga de Talento (Clasificación):** Predecir la probabilidad de rotación de un empleado (`Attrition`: Yes/No) para implementar estrategias de retención proactivas, mitigando los altos costos asociados a la pérdida y reemplazo de talento.

---

## 🗂️ Dataset
El análisis se fundamenta en el conjunto de datos "IBM HR Analytics Employee Attrition & Performance".

* **Página del proyecto:** [Kaggle - IBM HR Analytics](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
* **Descarga directa (API):** [Kaggle API Download](https://www.kaggle.com/api/v1/datasets/download/pavansubhasht/ibm-hr-analytics-attrition-dataset)

---

## 🏗️ Estructura del Repositorio
Esta arquitectura de proyecto garantiza la modularidad y reproducibilidad del análisis:

* `notebooks/`: Contiene el Jupyter Notebook principal (`patondemrd.ipynb`) con el EDA detallado, análisis de *data leakage* y entrenamiento de modelos.
* `report/`: Informe técnico en formato PDF con la interpretación de negocio y métricas.
* `slides/`: Presentación ejecutiva de los hallazgos y recomendaciones accionables.
* `src/`: (Opcional) Funciones de utilidad y transformadores personalizados en Python para mantener el pipeline limpio.
* `requirements.txt`: Dependencias y versiones exactas para replicar el entorno de ejecución.

---

## ⚙️ Metodología y Pipeline Técnico



El desarrollo de los modelos sigue rigurosos estándares de ciencia de datos:

### 1. Curación de Datos y Data Leakage
* **Fuga de Información:** Se realizó una auditoría estricta para identificar variables que no estarían disponibles en un escenario real de predicción (ej. evaluaciones futuras o motivos de salida posteriores). Estas variables fueron excluidas y documentadas en el notebook.
* **Variables Constantes/Irrelevantes:** Se eliminaron columnas con varianza cero o identificadores únicos (ej. `EmployeeNumber`, `Over18`, `StandardHours`) basándose en análisis de cardinalidad (`nunique`).

### 2. Preprocesamiento (ColumnTransformer)
Se construyó un pipeline robusto de Scikit-Learn para el tratamiento de características:
* `OneHotEncoder`: Para variables nominales (sin orden implícito).
* `OrdinalEncoder`: Para variables categóricas ordinales, respetando su jerarquía.
* `StandardScaler`: Para estandarizar la magnitud de las variables numéricas y optimizar la convergencia de los modelos.

### 3. Modelado Predictivo
* **Regresión (`MonthlyIncome`):** Se estableció un baseline con **Regresión Lineal** estándar, seguido de regularizaciones **Ridge** (L2) y **Lasso** (L1) para manejar la multicolinealidad y seleccionar características. Se evalúan mediante curvas de aprendizaje (Learning Curves), RMSE y R².
* **Clasificación (`Attrition`):** Implementación de **Regresión Logística**. Debido al desbalance de clases y al contexto del negocio (el costo de un Falso Negativo —perder a un empleado sin preverlo— es mucho mayor que un Falso Positivo), la optimización y evaluación se centran estrictamente en la métrica **Recall**.



---

## 🚀 Instrucciones para Reproducir

1.  Clona el repositorio en tu máquina local:
    ```bash
    git clone [https://github.com/TU_USUARIO/TU_REPOSITORIO.git](https://github.com/TU_USUARIO/TU_REPOSITORIO.git)
    cd TU_REPOSITORIO
    ```
2.  Crea un entorno virtual e instala las dependencias:
    ```bash
    python -m venv venv
    source venv/bin/activate  # En Windows: venv\Scripts\activate
    pip install -r requirements.txt
    ```
3.  Ejecuta el entorno interactivo:
    ```bash
    jupyter notebook notebooks/patondemrd.ipynb
    ```

---

## 📈 Resultados y Entregables (Verificables)
* ✅ **Notebook interactivo** con EDA exhaustivo y control de fuga de datos.
* ✅ **Pipelines integrados** (Preprocesamiento + Modelo) listos para producción.
* ✅ **Reporte de métricas** (RMSE, R², Recall, Matrices de Confusión y Learning Curves).
* ✅ **Interpretación de Coeficientes:** Análisis de los pesos en Ridge/Lasso y Regresión Logística para extraer conclusiones estratégicas sobre qué factores retienen al talento y qué define la curva salarial.