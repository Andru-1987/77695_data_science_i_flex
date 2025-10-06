# **Introducción a Feature Selection (Selección de Características)**

## **¿Qué es Feature Selection?**

**Feature Selection** es el proceso de seleccionar un subconjunto de características relevantes para usar en la construcción de modelos de machine learning. Elimina características irrelevantes o redundantes que no contribuyen al poder predictivo del modelo.

---

## **¿Por qué es importante?**

### **Beneficios principales:**

1. **Mejora del rendimiento del modelo**
   - Reduce overfitting
   - Mejora la generalización
   - Aumenta la precisión

2. **Reducción de complejidad**
   - Modelos más simples y interpretables
   - Menor tiempo de entrenamiento
   - Menor requerimiento computacional

3. **Mejor interpretabilidad**
   - Facilita entender qué características realmente importan
   - Ayuda en la toma de decisiones empresariales

4. **Prevención de maldición de la dimensionalidad**
   - Menos características = menos datos necesarios

---

## **Tipos de Métodos de Feature Selection**

## **1. Métodos de Filtro (Filter Methods)**

**Características:**
- Seleccionan características independientemente del modelo
- Rápidos y computacionalmente eficientes
- Basados en propiedades estadísticas

### **a) Métodos Univariados**
Evalúan cada característica individualmente.

```python
import pandas as pd
import numpy as np
from sklearn.feature_selection import SelectKBest, f_classif, mutual_info_classif
from sklearn.datasets import load_breast_cancer

# Cargar datos
data = load_breast_cancer()
X, y = data.data, data.target
feature_names = data.feature_names

# Selección basada en ANOVA F-value
selector_anova = SelectKBest(score_func=f_classif, k=10)
X_anova = selector_anova.fit_transform(X, y)

# Selección basada en información mutua
selector_mi = SelectKBest(score_func=mutual_info_classif, k=10)
X_mi = selector_mi.fit_transform(X, y)

print("Características seleccionadas (ANOVA):")
print([feature_names[i] for i in selector_anova.get_support(indices=True)])
```

### **Métodos comunes:**
- **Correlación de Pearson**: Para relaciones lineales
- **ANOVA F-test**: Para clasificación
- **Chi-cuadrado**: Para características categóricas
- **Información Mutua**: Para relaciones no lineales

---

## **2. Métodos de Wrapper**

**Características:**
- Evalúan subconjuntos de características usando un modelo específico
- Computacionalmente costosos
- Mayor rendimiento pero menor escalabilidad

### **a) Forward Selection**
```python
from sklearn.feature_selection import SequentialFeatureSelector
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import LogisticRegression

# Forward Selection
model = LogisticRegression()
sfs_forward = SequentialFeatureSelector(
    model, 
    n_features_to_select=10, 
    direction='forward'
)
X_forward = sfs_forward.fit_transform(X, y)

print("Características seleccionadas (Forward):")
print([feature_names[i] for i in sfs_forward.get_support(indices=True)])
```

### **b) Backward Elimination**
```python
# Backward Elimination
sfs_backward = SequentialFeatureSelector(
    model,
    n_features_to_select=10,
    direction='backward'
)
X_backward = sfs_backward.fit_transform(X, y)
```

### **c) Búsqueda Exhaustiva**
```python
from sklearn.feature_selection import RFE

# Recursive Feature Elimination
rfe = RFE(
    estimator=RandomForestClassifier(),
    n_features_to_select=10
)
X_rfe = rfe.fit_transform(X, y)

print("Ranking de características (RFE):")
for i, (feature, rank) in enumerate(zip(feature_names, rfe.ranking_)):
    print(f"{feature}: {rank}")
```

---

## **3. Métodos Integrados (Embedded Methods)**

**Características:**
- La selección ocurre durante el entrenamiento del modelo
- Balance entre eficiencia y rendimiento
- Utilizan regularización

### **a) Regularización L1 (Lasso)**
```python
from sklearn.linear_model import LassoCV
from sklearn.preprocessing import StandardScaler

# Escalar datos
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Lasso para selección de características
lasso = LassoCV(cv=5, random_state=42)
lasso.fit(X_scaled, y)

# Características seleccionadas (coeficientes no cero)
selected_features_lasso = np.where(lasso.coef_ != 0)[0]

print("Características seleccionadas (Lasso):")
print([feature_names[i] for i in selected_features_lasso])
print(f"Número de características: {len(selected_features_lasso)}")
```

### **b) Importancia de Características con Random Forest**
```python
from sklearn.ensemble import RandomForestClassifier

# Random Forest para importancia de características
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X, y)

# Obtener importancia
importances = rf.feature_importances_
feature_importance_df = pd.DataFrame({
    'feature': feature_names,
    'importance': importances
}).sort_values('importance', ascending=False)

print("Top 10 características más importantes:")
print(feature_importance_df.head(10))
```

### **c) XGBoost para Selección**
```python
from xgboost import XGBClassifier

# XGBoost para importancia de características
xgb = XGBClassifier(random_state=42)
xgb.fit(X, y)

# Importancia de características
xgb_importances = xgb.feature_importances_
xgb_importance_df = pd.DataFrame({
    'feature': feature_names,
    'importance': xgb_importances
}).sort_values('importance', ascending=False)

print("Top 10 características (XGBoost):")
print(xgb_importance_df.head(10))
```

---

## **4. Métodos Híbridos**

Combinan técnicas de filtro y wrapper para obtener lo mejor de ambos enfoques.

```python
from sklearn.feature_selection import RFECV
from sklearn.model_selection import StratifiedKFold

# RFE con validación cruzada
rfecv = RFECV(
    estimator=RandomForestClassifier(random_state=42),
    step=1,
    cv=StratifiedKFold(5),
    scoring='accuracy',
    min_features_to_select=5
)
rfecv.fit(X, y)

print(f"Número óptimo de características: {rfecv.n_features_}")
print("Características seleccionadas (RFECV):")
print([feature_names[i] for i in np.where(rfecv.support_)[0]])
```

---

## **Flujo de Trabajo Recomendado**

### **Paso a Paso:**

```python
def comprehensive_feature_selection(X, y, feature_names, target_features=10):
    """
    Flujo completo de selección de características
    """
    results = {}
    
    # 1. Método de Filtro: Información Mutua
    selector_mi = SelectKBest(score_func=mutual_info_classif, k=target_features)
    X_mi = selector_mi.fit_transform(X, y)
    results['filter_mi'] = [feature_names[i] for i in selector_mi.get_support(indices=True)]
    
    # 2. Método Integrado: Random Forest
    rf = RandomForestClassifier(n_estimators=100, random_state=42)
    rf.fit(X, y)
    importances = rf.feature_importances_
    top_indices_rf = np.argsort(importances)[-target_features:]
    results['embedded_rf'] = [feature_names[i] for i in top_indices_rf]
    
    # 3. Método Wrapper: RFE
    rfe = RFE(
        estimator=LogisticRegression(random_state=42),
        n_features_to_select=target_features
    )
    rfe.fit(X, y)
    results['wrapper_rfe'] = [feature_names[i] for i in np.where(rfe.support_)[0]]
    
    return results

# Aplicar flujo completo
results = comprehensive_feature_selection(X, y, feature_names)
for method, features in results.items():
    print(f"\n{method}: {len(features)} características")
    print(features)
```

---

## **Comparación de Métodos**

| Método | Velocidad | Rendimiento | Interpretabilidad | Escalabilidad |
|--------|-----------|-------------|-------------------|---------------|
| **Filtro** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Wrapper** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| **Integrado** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |

---

## **Mejores Prácticas**

### **1. Consideraciones:**
- **Tamaño del dataset**: Para datasets grandes, empezar con métodos de filtro
- **Dominio del problema**: Usar conocimiento del dominio para guiar la selección
- **Recursos computacionales**: Métodos wrapper son costosos
- **Objetivo del modelo**: Interpretabilidad vs. rendimiento

### **2. Validación:**
```python
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier

def evaluate_feature_set(X_selected, y, model):
    """Evaluar rendimiento del subconjunto seleccionado"""
    scores = cross_val_score(model, X_selected, y, cv=5, scoring='accuracy')
    return np.mean(scores), np.std(scores)

# Evaluar diferentes métodos
model = RandomForestClassifier(random_state=42)

print("Evaluación de métodos de selección:")
for method_name, X_selected in [('Todas', X), 
                               ('Filter', X_mi), 
                               ('Embedded', X[:, selected_features_lasso])]:
    mean_score, std_score = evaluate_feature_set(X_selected, y, model)
    print(f"{method_name}: {mean_score:.3f} ± {std_score:.3f}")
```

### **3. Consejos Finales:**
- **Empezar simple**: Comenzar con métodos de filtro
- **Combinar enfoques**: Usar múltiples métodos y comparar
- **Validar siempre**: Evaluar el impacto en el rendimiento
- **Considerar el costo**: Balance entre rendimiento e interpretabilidad

---

La selección de características es una etapa crucial en el pipeline de machine learning que puede significativamente mejorar el rendimiento y interpretabilidad de tus modelos.


- [Feature Selection](https://www.geeksforgeeks.org/machine-learning/feature-selection-techniques-in-machine-learning/)
- [Wrapper Methods](https://www.youtube.com/watch?v=ZzqWtxOdz3Q)
- [Wrapper Methods](https://arismuhandisin.medium.com/understanding-wrapper-methods-in-machine-learning-a-guide-to-feature-selection-23f71059abf8)