# **Métricas de Evaluación para Modelos de Regresión**

Cuando entrenamos un modelo de **regresión**, queremos predecir valores **continuos** (por ejemplo, el precio de una casa, la temperatura, la cantidad de ventas, etc.). Para saber qué tan bien está funcionando el modelo, usamos **métricas de error** que comparan las **predicciones** con los **valores reales**.

---

## **1. Error Absoluto Medio (MAE – Mean Absolute Error)**

**Significado:**  
Mide el **promedio de las diferencias absolutas** entre las predicciones y los valores reales. En otras palabras, nos dice **cuánto se equivoca el modelo en promedio**, sin importar si el error es positivo o negativo.

**Fórmula:**  
```
MAE = (1/n) * Σ|y_i - ŷ_i|
```

Donde:
- \( y_i \): valor real
- \( ŷ_i \): valor predicho por el modelo  
- \( n \): cantidad de observaciones

**Interpretación:**  
Cuanto **menor sea el MAE**, mejor es el modelo. Por ejemplo, un MAE de 500 en un modelo de precios significa que, en promedio, el modelo se equivoca por 500 unidades monetarias.

---

## **2. Error Cuadrático Medio (MSE – Mean Squared Error)**

**Significado:**  
Mide el **promedio de los errores al cuadrado**. Elevar al cuadrado hace que los errores grandes pesen más, por lo que esta métrica penaliza más los errores grandes que los pequeños.

**Fórmula:**  
```
MSE = (1/n) * Σ(y_i - ŷ_i)²
```

**Interpretación:**  
Cuanto más chico el MSE, mejor el modelo. Debido a que los errores están al cuadrado, su unidad de medida no es la misma que la del valor original (por ejemplo, pesos², grados², etc.).

---

## **3. Raíz del Error Cuadrático Medio (RMSE – Root Mean Squared Error)**

**Significado:**  
Es la **raíz cuadrada del MSE**. Sirve para volver a la **unidad original de la variable** (por ejemplo, pesos o grados), lo que facilita su interpretación.

**Fórmula:**  
```
RMSE = √MSE
```

**Interpretación:**  
Un RMSE más bajo indica un modelo más preciso. Es útil cuando queremos entender el error promedio "real" en las mismas unidades que la variable objetivo.

---

## **4. Coeficiente de Determinación (R² o R-squared)**

**Significado:**  
Indica **qué proporción de la variabilidad** en los datos puede ser explicada por el modelo. Va de 0 a 1 (aunque puede ser negativo si el modelo es muy malo).

**Fórmula:**  
```
R² = 1 - [Σ(y_i - ŷ_i)² / Σ(y_i - ȳ)²]
```

Donde \( ȳ \) es el promedio de los valores reales.

**Interpretación:**
- **R² = 1:** el modelo predice perfectamente todos los valores.
- **R² = 0:** el modelo no explica mejor que un promedio.
- **R² < 0:** el modelo es peor que usar el promedio como predicción.

---

## **Ejemplo en Python**

Veamos cómo se calculan estas métricas con un caso muy simple.

Supongamos que queremos predecir el precio de un producto:

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
import numpy as np

# Valores reales
y_true = [100, 200, 300, 400, 500]

# Predicciones del modelo
y_pred = [110, 190, 290, 410, 490]

# Cálculo de las métricas
mae = mean_absolute_error(y_true, y_pred)
mse = mean_squared_error(y_true, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_true, y_pred)

print(f"Error Absoluto Medio (MAE): {mae:.2f}")
print(f"Error Cuadrático Medio (MSE): {mse:.2f}")
print(f"Raíz del Error Cuadrático Medio (RMSE): {rmse:.2f}")
print(f"Coeficiente de Determinación (R²): {r2:.2f}")
```

**Salida esperada:**

```
Error Absoluto Medio (MAE): 8.00
Error Cuadrático Medio (MSE): 100.00
Raíz del Error Cuadrático Medio (RMSE): 10.00
Coeficiente de Determinación (R²): 0.99
```

---

### **Interpretación del ejemplo**

- El modelo se equivoca en promedio **8 unidades** respecto al valor real.
- Los errores grandes pesan más en el **MSE (100)**.
- El **RMSE (10)** nos dice que el error promedio "real" ronda las 10 unidades.
- El **R² = 0.99** indica que el modelo explica el **99% de la variabilidad** de los datos, lo cual es excelente.

---

## **Resumen comparativo**

| Métrica  | Qué mide                  | Penaliza errores grandes | Unidad de medida    | Ideal          |
|----------|---------------------------|--------------------------|---------------------|----------------|
| **MAE**  | Error promedio absoluto   | No                       | Igual a la variable | Más bajo       |
| **MSE**  | Error cuadrático promedio | Sí                       | Cuadrada            | Más bajo       |
| **RMSE** | Error promedio real       | Sí                       | Igual a la variable | Más bajo       |
| **R²**   | Varianza explicada        | No aplica                | Sin unidad          | Más alto (≤ 1) |