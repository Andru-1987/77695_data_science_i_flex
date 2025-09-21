# ¿Qué es Machine Learning?

**Machine Learning (ML)** o *Aprendizaje Automático* es una rama de la **Inteligencia Artificial (IA)** que se centra en desarrollar algoritmos y modelos capaces de aprender patrones a partir de datos, **sin ser programados explícitamente**. En lugar de seguir reglas fijas, los sistemas de ML **mejoran su desempeño con la experiencia** (datos).

El objetivo principal es **generalizar** a partir de ejemplos para realizar predicciones o tomar decisiones en situaciones nuevas.

---

## Particularidades y características principales

1. **Aprendizaje basado en datos**

   * ML necesita **datos históricos o de entrenamiento** para identificar patrones y relaciones.
   * A diferencia de la programación tradicional, en ML el modelo **aprende de los datos** en lugar de reglas codificadas.

2. **Capacidad predictiva y adaptativa**

   * Los modelos pueden **predecir valores futuros** (ejemplo: ventas) o **clasificar información** (ejemplo: spam/no spam).
   * Algunos modelos se ajustan en tiempo real a los cambios en los datos.

3. **Tipos principales de aprendizaje**

   * **Supervisado**: Usa datos etiquetados (ejemplo: predecir precios de casas).
   * **No supervisado**: Busca patrones sin etiquetas (ejemplo: agrupar clientes).
   * **Por refuerzo**: Aprende por prueba y error con recompensas (ejemplo: juegos o robots).

4. **Automatización y escalabilidad**

   * Permite automatizar tareas complejas como detección de fraudes o diagnósticos.
   * Se adapta bien a grandes volúmenes de datos (*Big Data*).

5. **Evaluación y métricas**

   * Se mide el desempeño con métricas como precisión, recall o error cuadrático medio.

6. **Dependencia de los datos**

   * El rendimiento depende de la **calidad y representatividad de los datos**.
   * Problemas de sesgo o datos incompletos afectan el resultado.

7. **Variedad de algoritmos**

   * Desde métodos clásicos como regresión y árboles, hasta redes neuronales y deep learning.

---

## Diferencia con Data Science

**Data Science** abarca todo el ciclo de trabajo con datos: limpieza, exploración, visualización, modelado y comunicación.
**Machine Learning** es una herramienta dentro de Data Science, enfocada en **automatizar el aprendizaje** para predecir o tomar decisiones.

Ejemplo: un modelo de ML predice el abandono de clientes (*churn*), mientras que el data scientist además analiza **por qué** ocurre y cómo actuar.

---

## Primeros pasos en Machine Learning supervisado

### 1. Regresión lineal: predicción de valores numéricos

La **regresión lineal** es uno de los algoritmos más simples y fundamentales.
Se utiliza cuando la variable objetivo es **continua** (ejemplo: precio de una casa, cantidad de ventas).

* **Idea principal**: Ajustar una línea recta (o plano en dimensiones mayores) que mejor represente la relación entre las variables de entrada (*features*) y el valor de salida.
* **Ejemplo**: Predecir el precio de una casa según su superficie.
* **Métrica de evaluación**: Error cuadrático medio (MSE) o R².

Esto introduce el concepto de **modelar relaciones numéricas** con los datos.

---

### 2. Clasificación: predicción de categorías

Cuando el objetivo es **discreto o categórico**, se habla de **clasificación**.
Ejemplo: predecir si un correo es spam o no, o si un cliente comprará o no un producto.

* **Algoritmos comunes**:

  * Regresión logística
  * Árboles de decisión
  * Random Forest
  * Support Vector Machines (SVM)

* **Métricas de evaluación**: Precisión, recall, F1-score, matriz de confusión.

Esto permite construir modelos que **diferencian entre clases** en base a los patrones aprendidos.

---

## Selección de características (Feature Selection)

Para mejorar el rendimiento de los modelos, se utilizan técnicas de **selección de variables relevantes**. Estas se dividen en tres grupos principales:

### 1. Métodos de filtro (Filter Methods)

Evalúan cada característica individualmente con pruebas estadísticas.
Ejemplos: Chi-cuadrado, ANOVA, correlación.

* Ventajas: rápidos, no dependen de un modelo.
* Desventajas: no consideran interacciones entre variables.

### 2. Métodos envolventes (Wrapper Methods)

Prueban distintos subconjuntos de características entrenando modelos.
Ejemplos: RFE, selección hacia adelante o hacia atrás.

* Ventajas: consideran interacciones.
* Desventajas: lentos y costosos en cómputo.

### 3. Métodos embebidos (Embedded Methods)

Seleccionan variables durante el entrenamiento del modelo.
Ejemplos: Lasso, Random Forest, Elastic Net.

* Ventajas: eficientes y capturan interacciones.
* Desventajas: dependen del modelo usado.

---

## Resumen de métodos de selección de características

| Método             | Tipo       | Usa modelo | Considera interacciones | Velocidad | Ejemplos                     |
| ------------------ | ---------- | ---------- | ----------------------- | --------- | ---------------------------- |
| Variance Threshold | Filtro     | No         | No                      | Rápido    | Elimina variables constantes |
| SelectKBest        | Filtro     | No         | No                      | Rápido    | ANOVA, Chi-cuadrado          |
| RFE                | Envolvente | Sí         | Sí                      | Lento     | Logistic Regression + RFE    |
| Boruta             | Envolvente | Sí         | Sí                      | Muy lento | Random Forest                |
