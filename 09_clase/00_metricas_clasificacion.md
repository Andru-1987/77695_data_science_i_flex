# **Métricas de Evaluación para Modelos de Clasificación**

Cuando entrenamos un modelo de **clasificación**, queremos predecir **categorías o clases** (por ejemplo: spam/no spam, enfermedad/sano, tipo de producto, etc.). Para evaluar el rendimiento del modelo, usamos métricas específicas que miden qué tan bien clasifica las instancias.

---

## **Conceptos Fundamentales: Matriz de Confusión**

La **matriz de confusión** es la base para la mayoría de las métricas de clasificación:

```
                Predicción
              Positivo  Negativo
Real Positivo   TP       FN
Real Negativo   FP       TN
```

Donde:
- **TP (True Positive)**: Correctamente clasificado como positivo
- **FP (False Positive)**: Incorrectamente clasificado como positivo
- **TN (True Negative)**: Correctamente clasificado como negativo
- **FN (False Negative)**: Incorrectamente clasificado como negativo

---

## **1. Exactitud (Accuracy)**

**Significado:**  
Mide la **proporción de predicciones correctas** sobre el total de predicciones.

**Fórmula:**  
```
Accuracy = (TP + TN) / (TP + TN + FP + FN)
```

**Interpretación:**  
Valores cercanos a 1 indican mejor rendimiento. Sin embargo, puede ser engañosa cuando las clases están desbalanceadas.

**Cuándo usar:**  
- Cuando las clases están balanceadas
- Cuando los costos de FP y FN son similares

---

## **2. Precisión (Precision)**

**Significado:**  
De todas las predicciones positivas, ¿cuántas eran realmente positivas?

**Fórmula:**  
```
Precision = TP / (TP + FP)
```

**Interpretación:**  
Mide la "calidad" de las predicciones positivas. Alta precisión significa pocos falsos positivos.

**Cuándo usar:**  
- Cuando el costo de FP es alto (ej: diagnóstico médico falso)
- En sistemas de recomendación

---

## **3. Exhaustividad (Recall o Sensibilidad)**

**Significado:**  
De todos los casos realmente positivos, ¿cuántos logramos identificar?

**Fórmula:**  
```
Recall = TP / (TP + FN)
```

**Interpretación:**  
Mide la capacidad de detectar casos positivos. Alto recall significa pocos falsos negativos.

**Cuándo usar:**  
- Cuando el costo de FN es alto (ej: detección de enfermedades)
- En sistemas de seguridad

---

## **4. Puntuación F1 (F1-Score)**

**Significado:**  
**Media armónica** entre precisión y recall. Busca un balance entre ambas métricas.

**Fórmula:**  
```
F1 = 2 * (Precision * Recall) / (Precision + Recall)
```

**Interpretación:**  
Útil cuando se necesita balancear precisión y recall. Valores cercanos a 1 indican buen balance.

**Cuándo usar:**  
- Cuando hay desbalance de clases
- Cuando se necesita un balance entre FP y FN

---

## **5. Especificidad (Specificity)**

**Significado:**  
De todos los casos realmente negativos, ¿cuántos logramos identificar correctamente?

**Fórmula:**  
```
Specificity = TN / (TN + FP)
```

**Interpretación:**  
Complementaria al recall. Mide la capacidad de detectar casos negativos.

---

## **6. Curva ROC y AUC**

**Significado:**  
- **ROC (Receiver Operating Characteristic)**: Curva que muestra el trade-off entre TPR (Recall) y FPR (1 - Specificity)
- **AUC (Area Under Curve)**: Área bajo la curva ROC, mime la capacidad de discriminación del modelo

**Interpretación:**  
- **AUC = 1**: Clasificador perfecto
- **AUC = 0.5**: No mejor que aleatorio
- **AUC < 0.5**: Peor que aleatorio

---

## **Ejemplo en Python - Clasificación Binaria**

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
from sklearn.metrics import confusion_matrix, classification_report, roc_auc_score
import numpy as np

# Valores reales y predicciones
y_true = [1, 0, 1, 1, 0, 1, 0, 0, 1, 0]  # 1: Positivo, 0: Negativo
y_pred = [1, 0, 1, 0, 0, 1, 1, 0, 1, 0]  # Predicciones del modelo

# Cálculo de métricas
accuracy = accuracy_score(y_true, y_pred)
precision = precision_score(y_true, y_pred)
recall = recall_score(y_true, y_pred)
f1 = f1_score(y_true, y_pred)

# Matriz de confusión
cm = confusion_matrix(y_true, y_pred)

print("=== MÉTRICAS DE CLASIFICACIÓN ===")
print(f"Exactitud (Accuracy): {accuracy:.2f}")
print(f"Precisión (Precision): {precision:.2f}")
print(f"Exhaustividad (Recall): {recall:.2f}")
print(f"Puntuación F1: {f1:.2f}")
print(f"\nMatriz de Confusión:\n{cm}")
print(f"\nReporte Completo:\n{classification_report(y_true, y_pred)}")
```

**Salida esperada:**
```
=== MÉTRICAS DE CLASIFICACIÓN ===
Exactitud (Accuracy): 0.80
Precisión (Precision): 0.80
Exhaustividad (Recall): 0.80
Puntuación F1: 0.80

Matriz de Confusión:
[[4 1]
 [1 4]]

Reporte Completo:
              precision    recall  f1-score   support

           0       0.80      0.80      0.80         5
           1       0.80      0.80      0.80         5

    accuracy                           0.80        10
   macro avg       0.80      0.80      0.80        10
weighted avg       0.80      0.80      0.80        10
```

---

## **Ejemplo en Python - Clasificación Multiclase**

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
from sklearn.metrics import confusion_matrix, classification_report
import seaborn as sns
import matplotlib.pyplot as plt

# Clasificación con 3 clases
y_true_multi = [0, 1, 2, 0, 1, 2, 0, 1, 2]  # 0: Clase A, 1: Clase B, 2: Clase C
y_pred_multi = [0, 1, 1, 0, 2, 2, 0, 1, 2]  # Predicciones

# Métricas con promedio macro
precision_macro = precision_score(y_true_multi, y_pred_multi, average='macro')
recall_macro = recall_score(y_true_multi, y_pred_multi, average='macro')
f1_macro = f1_score(y_true_multi, y_pred_multi, average='macro')

print("=== CLASIFICACIÓN MULTICLASE ===")
print(f"Exactitud: {accuracy_score(y_true_multi, y_pred_multi):.2f}")
print(f"Precisión (Macro): {precision_macro:.2f}")
print(f"Recall (Macro): {recall_macro:.2f}")
print(f"F1 (Macro): {f1_macro:.2f}")
print(f"\nReporte Multiclase:\n{classification_report(y_true_multi, y_pred_multi)}")
```

---

## **Resumen Comparativo**

| Métrica | Fórmula | Enfoque | Ideal | Cuándo usar |
|---------|---------|---------|-------|-------------|
| **Accuracy** | (TP+TN)/Total | Rendimiento general | Alto | Clases balanceadas |
| **Precision** | TP/(TP+FP) | Calidad predicciones + | Alto | Costo FP alto |
| **Recall** | TP/(TP+FN) | Detección casos + | Alto | Costo FN alto |
| **F1-Score** | 2*(P*R)/(P+R) | Balance P-R | Alto | Balance general |
| **Specificity** | TN/(TN+FP) | Detección casos - | Alto | Evitar FP |
| **AUC-ROC** | Área bajo curva | Capacidad discriminación | Cercano 1 | Evaluación general |

---

## **Consideraciones Prácticas**

### **Elección de Métricas:**
- **Detección de fraudes**: Priorizar Recall (minimizar FN)
- **Recomendación de productos**: Priorizar Precision (minimizar FP)
- **Diagnóstico médico**: Balance entre Precision y Recall

### **Promedios en Multiclase:**
- **macro**: Promedia métricas por clase (sin considerar desbalance)
- **weighted**: Promedia considerando soporte de cada clase
- **micro**: Calcula métricas globales contando totales

```python
# Ejemplo de diferentes promedios
y_true = [0, 1, 2, 0, 1, 2]
y_pred = [0, 2, 1, 0, 0, 1]

print("Precision macro:", precision_score(y_true, y_pred, average='macro'))
print("Precision weighted:", precision_score(y_true, y_pred, average='weighted'))
print("Precision micro:", precision_score(y_true, y_pred, average='micro'))
```
