# **Modelos de Aprendizaje Supervisado: Clasificación y Regresión**  

Los modelos de **aprendizaje supervisado** son algoritmos de Machine Learning que aprenden a partir de **datos etiquetados**, es decir, datos donde ya se conoce la respuesta correcta (variable objetivo). Su objetivo es **generalizar patrones** para hacer predicciones sobre nuevos datos.  

Se dividen en dos grandes categorías:  
1. **Modelos de Clasificación**: Predicen **categorías discretas** (ej.: sí/no, spam/no spam).  
2. **Modelos de Regresión**: Predicen **valores continuos** (ej.: precio de una casa, temperatura).  

---

## **¿Por qué se llaman "supervisados"?**  
Porque el algoritmo "aprende" bajo la supervisión de **etiquetas conocidas** (datos de entrenamiento con la respuesta correcta).  
- **Ejemplo**:  
  - Si entrenas un modelo para predecir si un correo es *spam*, le proporcionas ejemplos históricos de correos **ya etiquetados** como "spam" o "no spam".  
  - El modelo ajusta sus parámetros para minimizar errores en esas etiquetas.  

---

## **1. Modelos de Clasificación**  
**Objetivo**: Predecir una **clase o categoría**.  

### **Algoritmos comunes**  
| Modelo               | Idea Básica                                                                 | Ejemplo de Uso                     |  
|----------------------|-----------------------------------------------------------------------------|------------------------------------|  
| **Regresión Logística** | Ajusta una función sigmoide para estimar probabilidades de pertenecer a una clase. | Predecir si un cliente comprará (sí/no). |  
| **Árboles de Decisión** | Divide los datos en reglas jerárquicas (preguntas sí/no).                   | Diagnóstico médico (enfermo/sano). |  
| **Random Forest**     | Combina múltiples árboles de decisión para mejorar precisión.               | Detección de fraude.               |  
| **SVM (Máquinas de Vectores Soporte)** | Encuentra el hiperplano óptimo que separa clases. | Clasificación de imágenes (gato/perro). |  
| **K-NN (Vecinos más Cercanos)** | Clasifica según la mayoría de los *k* ejemplos más similares en el dataset. | Reconocimiento de escritura a mano. |  

#### **Ejemplo en código (Regresión Logística - Python)**  
```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

# Datos de ejemplo: X = features, y = etiquetas (0 o 1)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = LogisticRegression()
model.fit(X_train, y_train)  # Entrenamiento con datos etiquetados
predictions = model.predict(X_test)  # Predicciones: [0, 1, 1, 0...]
```

---

## **2. Modelos de Regresión**  
**Objetivo**: Predecir un **valor numérico continuo**.  

### **Algoritmos comunes**  
| Modelo               | Idea Básica                                                                 | Ejemplo de Uso                     |  
|----------------------|-----------------------------------------------------------------------------|------------------------------------|  
| **Regresión Lineal** | Ajusta una línea recta que minimiza el error cuadrático.                   | Predecir el precio de una vivienda. |  
| **Árboles de Regresión** | Similar a árboles de decisión, pero prediciendo valores numéricos en las hojas. | Pronóstico de ventas.              |  
| **Random Forest (Regresión)** | Promedia predicciones de múltiples árboles.                              | Predecir demanda de energía.       |  
| **SVR (Support Vector Regression)** | Versión de SVM para regresión, usando márgenes de error.               | Estimación de temperaturas.        |  

#### **Ejemplo en código (Regresión Lineal - Python)**  
```python
from sklearn.linear_model import LinearRegression

# Datos: X = características (ej.: metros cuadrados), y = valor a predecir (ej.: precio)
model = LinearRegression()
model.fit(X_train, y_train)  # Entrenamiento con datos etiquetados
predictions = model.predict(X_test)  # Predicciones: [45000, 32000, 21000...]
```

---

## **Diferencia Clave entre Clasificación y Regresión**  
| Característica      | Clasificación                          | Regresión                          |  
|---------------------|----------------------------------------|------------------------------------|  
| **Salida**          | Clase discreta (ej.: "sí/no").         | Valor numérico (ej.: 42.5).        |  
| **Métricas**        | Precisión, recall, matriz de confusión. | MSE, R², error absoluto medio.     |  
| **Ejemplo**         | ¿Es spam?                              | ¿Cuánto costará?                   |  

---

### **¿Por qué son supervisados?**  
- **Requieren datos etiquetados** durante el entrenamiento (ej.: `y_train` en los códigos anteriores).  
- **Aprenden comparando** sus predicciones con las etiquetas reales y ajustando parámetros (por eso se "supervisa" su aprendizaje).  

---

### **Resumen**  
- **Clasificación**: Respuestas categóricas.  
- **Regresión**: Respuestas numéricas.  
- **Supervisados**: Necesitan ejemplos con "respuestas correctas" para entrenar.  
