 # Missing Treatment

*Que se debe realizar cuando tengo un ratio de empty values en una columna o en base al dataset?*

# Criterios para Tratamiento de Missing Values

## Tabla Comparativa por Ratio de Nullidad

| Ratio de Nullidad | Criterio Principal | Estrategias Recomendadas | Consideraciones Clave |
|-------------------|-------------------|--------------------------|----------------------|
| **< 5%** | **Eliminación Segura** | - Eliminar filas/columnas<br>- Imputación simple (media, mediana, moda) | - Impacto mínimo en el tamaño de la muestra<br>- Bajo riesgo de sesgo |
| **5% - 10%** | **Imputación Simple** | - Mediana para numéricas (robusta a outliers)<br>- Moda para categóricas<br>- KNN básico | - Validar distribución de datos<br>- Considerar creación de flag de imputación |
| **10% - 20%** | **Imputación Avanzada** | - MICE (Multiple Imputation by Chained Equations)<br>- Random Forest imputation<br>- Modelos predictivos | - Analizar patrón (MCAR/MAR/MNAR)<br>- Incluir variables predictoras relevantes |
| **20% - 50%** | **Análisis de Patrón + Imputación** | - Determinar MCAR/MAR/MNAR<br>- Imputación múltiple<br>- Modelos mixtos | - Alto riesgo de sesgo<br>- Requiere validación cruzada<br>- Considerar análisis de sensibilidad |
| **> 50%** | **Evaluación Crítica** | - Eliminar la variable<br>- Tratamiento como variable categórica especial<br>- Modelos de selección | - Pérdida significativa de información<br>- Posible introducción de sesgo severo<br>- Considerar exclusión del análisis |

##  Criterio por Tipo de Patrón (MCAR/MAR/MNAR)

### **MCAR (Missing Completely At Random)**
- **Criterio**: Los valores faltantes son completamente aleatorios
- **Acción**: Imputación simple aceptable
- **Riesgo**: Bajo sesgo de imputación

### **MAR (Missing At Random)**
- **Criterio**: Los faltantes dependen de otras variables observadas
- **Acción**: Imputación usando variables predictoras
- **Riesgo**: Sesgo moderado si no se incluyen predictores correctos

### **MNAR (Missing Not At Random)**
- **Criterio**: Los faltantes dependen de valores no observados
- **Acción**: Métodos avanzados (Heckman, pattern mixture models)
- **Riesgo**: Alto sesgo potencial

## Criterios Decisorios Clave

### **1. Importancia de la Variable**
- **Crítica para el modelo**: Invertir en imputación avanzada
- **Secundaria**: Considerar eliminación si ratio alto

### **2. Tipo de Variable**
- **Numérica**: Mediana (robusta), MICE, regresión
- **Categórica**: Moda, clasificación, múltiple imputation

_[MICE](https://medium.com/@kunalshrm175/multivariate-imputation-by-chained-equations-mice-2d3efb063434): Realiza rellenado de datos , basado en distintos modelos iterativos estadisticos_

### **3. Tamaño de la Muestra**
- **Muestra grande**: Más tolerante a imputación
- **Muestra pequeña**: Cautela con eliminación

### **4. Objetivo del Análisis**
- **Predictivo**: Maximizar información, imputar
- **Inferencial**: Cautela con sesgo, validar robustez

## ⚠️ Límites Críticos de Actuación

| Ratio | Acción Recomendada |
|-------|-------------------|
| **> 30%** | Reevaluar necesidad de la variable en el modelo |
| **> 40%** | Fuera consideración para imputación simple |
| **> 60%** | Eliminación sistemática (alto riesgo de sesgo) |

##  Matriz de Decisión Final

1. **< 10%** + **MCAR** = Imputación simple
2. **10-30%** + **MAR** = Imputación avanzada con predictores
3. **> 30%** + **MNAR** = Eliminación o métodos especializados
4. **Cualquier ratio** + **Variable crítica** = Imputación avanzada obligatoria

Este criterio balancea el riesgo de sesgo con la pérdida de información, priorizando la validez estadística sobre la completitud de datos.

# Resampling para Missing Values en Series de Tiempo

## Criterios Especificos para Series Temporales

### 1. Patrones de Missing Values en Time Series
- **Missing completamente al azar (MCAR)**: Patron aleatorio sin estacionalidad
- **Missing en bloques**: Periodos completos faltantes (ej: falla de sensor)
- **Missing estacional**: Patrones recurrentes (ej: fines de semana, noches)
- **Missing sistematico**: Relacionado con valores especificos (ej: valores extremos)

## Estrategias de Resampling por Tipo de Serie

### Series con Alta Frecuencia (minutos, horas)
| Ratio Nullidad | Estrategia Principal | Tecnicas Especificas |
|----------------|---------------------|---------------------|
| **< 5%** | Interpolacion temporal | Linear, quadratic, spline interpolation |
| **5-15%** | Resampling estadistico | Rolling statistics, seasonal decomposition |
| **15-30%** | Modelos predictivos | ARIMA, Prophet, LSTM para imputacion |
| **> 30%** | Reconstruccion avanzada | State-space models, multiple imputation |

### Series con Baja Frecuencia (dias, meses)
| Ratio Nullidad | Estrategia Principal | Consideraciones |
|----------------|---------------------|----------------|
| **< 10%** | Interpolacion simple | Media movil, interpolacion lineal |
| **10-25%** | Modelos estacionales | STL decomposition, seasonal ARIMA |
| **25-50%** | Metodos hibridos | Combinacion de metodos + expert knowledge |
| **> 50%** | Reevaluacion | Considerar exclusion o agregacion temporal |

## Tecnicas Especializadas de Resampling

### Metodos de Interpolacion Temporal
- **Linear interpolation**: Para tendencias lineales
- **Spline interpolation**: Para patrones suaves no lineales  
- **Time-weighted avg**: Ponderacion por proximidad temporal
- **Seasonal adjustment**: Ajuste estacional antes de imputar

### Metodos Basados en Modelos
- **ARIMA/SARIMA**: Para series con estacionalidad y tendencia
- **Exponential smoothing**: Para patrones de corto plazo
- **LSTM/RNN**: Para patrones complejos no lineales
- **Prophet**: Para series con multiples estacionalidades

### Metodos de Resampling Estadistico
- **Rolling statistics**: Media movil, mediana movil
- **Expanding window**: Estadisticas acumulativas
- **Seasonal decomposition**: Separar tendencia, estacionalidad, residual
- **Multiple imputation**: Multiples escenarios de imputacion

## Criterios de Seleccion por Contexto

### Segun Patron Temporal
| Patron | Metodo Recomendado | Precauciones |
|--------|-------------------|-------------|
| **Tendencia fuerte** | Interpolacion lineal/polinomica | No sobreajustar |
| **Estacionalidad marcada** | Seasonal decomposition + imputacion | Validar patrones estacionales |
| **Ruido predominante** | Smoothing methods | Evitar suavizado excesivo |
| **Missing en bloques** | Modelos predictivos | Validar extrapolacion |

### Segun Frecuencia de Datos
| Frecuencia | Enfoque Recomendado | Consideraciones |
|------------|---------------------|----------------|
| **Alta freq** (segundos/minutos) | Interpolacion + smoothing | Mantener alta resolucion |
| **Media freq** (horas) | Modelos ARIMA + seasonal | Balancear precision/performance |
| **Baja freq** (dias/meses) | Multiple imputation | Mayor incertidumbre |

## Consideraciones Criticas

### Validacion de Resampling
- **Backtesting**: Testear imputacion en periodos conocidos
- **Cross-validation temporal**: Validacion en ventanas de tiempo
- **Sensitivity analysis**: Probar multiples metodos
- **Error metrics**: MAE, RMSE para imputacion

### Riesgos Especificos
- **Introducir autocorrelacion artificial**: Metodos muy agresivos
- **Suavizar patrones importantes**: Over-smoothing
- **Propagacion de error**: En metodos iterativos
- **Quebrantamiento de estacionalidad**: Metodos no estacionales

## Matriz de Decision Final

### Para Bloques de Missing Values
1. **Duracion < 5% serie**: Interpolacion temporal
2. **Duracion 5-20%**: Modelos predictivos (ARIMA, Prophet)
3. **Duracion > 20%**: Multiple imputation + expert knowledge

### Para Missing Esparcidos
1. **Ratio < 10%**: Interpolacion simple
2. **Ratio 10-30%**: Rolling statistics + seasonal adjustment  
3. **Ratio > 30%**: Modelos avanzados (LSTM, state-space models)

### Para Series con Estacionalidad
1. **Always**: Seasonal decomposition primero
2. **Luego**: Imputar componente residual
3. **Final**: Recomponer serie completa

Este enfoque prioriza mantener la estructura temporal, autocorrelacion y patrones estacionales durante el resampling, minimizando la introduccion de artefactos artificiales en la serie de tiempo.
