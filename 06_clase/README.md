# Tipos de variables en un análisis EDA (Exploratory Data Analysis)

*[DIAPOSITIVA CLASE FLEX](https://docs.google.com/presentation/d/1bTgblneO_G2WteTeku40AN-3yKmhiVvpcudqcGo0cco/edit?slide=id.p2#slide=id.p2)*

## 1. Según su naturaleza

### a. Variables Cuantitativas (Numéricas)

Representan cantidades o valores numéricos. Se subdividen en:

**Continuas**
- Pueden tomar infinitos valores dentro de un rango
- Se miden, no se cuentan
- Ejemplos: Altura (1.75 m, 1.76 m), Peso (65.5 kg, 66.2 kg), Tiempo (2.5 horas)

**Discretas**
- Solo pueden tomar valores enteros o finitos
- Se cuentan
- Ejemplos: Número de hijos (0, 1, 2…), Número de autos en una familia, Cantidad de errores en una prueba

### b. Variables Cualitativas (Categóricas)

Representan categorías o cualidades. No implican operaciones matemáticas.

**Nominales**
- No tienen orden lógico
- Ejemplos: Color de ojos (azul, verde, marrón), Género (masculino, femenino, otro), Nacionalidad (argentina, chilena)

**Ordinales**
- Tienen orden o jerarquía, pero no hay distancia precisa entre categorías
- Ejemplos: Nivel educativo (primario, secundario, universitario), Grado de satisfacción (bajo, medio, alto), Rango militar (soldado, cabo, sargento)

## 2. Según su variabilidad

**Dependientes**
- Son afectadas por otras variables
- Ejemplo: La presión arterial depende del nivel de actividad física

**Independientes**
- Se manipulan para ver su efecto
- Ejemplo: Horas de estudio como variable que afecta al rendimiento académico

## 3. Otras clasificaciones útiles

**Binarias o dicotómicas**
- Solo tienen dos categorías posibles
- Ejemplo: Sí / No, Aprobado / Reprobado

**Polinómicas**
- Tienen más de dos categorías
- Ejemplo: Tipo de sangre (A, B, AB, O)

## Series Temporales: Un tipo especial de variable

Las series temporales son conjuntos de datos en los que las observaciones están ordenadas en el tiempo. Se utilizan para analizar y predecir cómo cambian los valores de una variable a lo largo del tiempo.

### Características distintivas de las series temporales:

**Secuencialidad**
- El orden cronológico es fundamental
- Reordenar los datos rompe la estructura de la serie

**Dependencia temporal**
- Los valores sucesivos están relacionados entre sí
- Permite usar modelos especializados como ARIMA, LSTM, Prophet
- [ARIMA | SARIMA](https://datasciencepe.substack.com/p/modelos-arima-sarima-y-metodo-de)
- [LSTM](https://codificandobits.com/blog/redes-lstm/)
- [PROPHET FACEBOOK](https://medium.com/data-science/getting-started-predicting-time-series-data-with-facebook-prophet-c74ad3040525)

**Estructura del tiempo**
- Estacionalidad: patrones que se repiten en intervalos regulares
- Tendencia: crecimiento o disminución a lo largo del tiempo
- Ciclos: fluctuaciones irregulares que pueden durar años
- Eventos especiales: feriados, crisis, etc.

**Frecuencia**
- Puede ser horaria, diaria, semanal, mensual, trimestral, anual
- La frecuencia afecta el tipo de análisis

### Aplicaciones típicas:
- Predicción de ventas o demanda
- Análisis financiero (acciones, divisas)
- Meteorología
- Series biomédicas
- Datos de sensores IoT

**Ejemplo práctico:** El índice trimestral de inflación es una serie temporal porque:
- Tiene observaciones ordenadas en el tiempo
- Los datos se recopilan cada tres meses (intervalo regular)
- Permite analizar tendencia, estacionalidad y ciclos económicos

## Medidas de Resumen y Distribuciones

### Para variables cuantitativas:
- **Media**: Promedio aritmético, sensible a valores extremos
- **Mediana**: Valor central, resistente a outliers
- **Moda**: Valor más frecuente
- **Varianza**: Mide dispersión respecto a la media
- **Desviación estándar**: Dispersión en las mismas unidades que los datos
- **Cuartiles y percentiles**: Dividen el conjunto de datos en segmentos

### Para variables cualitativas:
- **Conteo de observaciones**: Frecuencia de cada categoría
- **Moda**: Categoría más frecuente

### Distribuciones comunes:
- **Distribución uniforme**: Todos los valores tienen igual probabilidad
- **Distribución normal**: Forma de campana, simétrica, con mayor densidad alrededor de la media

### Representación gráfica:
- **Histogramas**: Muestran frecuencias por intervalos
- **Correlación lineal**: Mide fuerza y dirección de la relación entre dos variables (-1 a 1)

## Próximos conocimientos recomendados

Para afianzar estos conceptos, se recomienda profundizar en:

1. **Técnicas de visualización específicas** para cada tipo de variable:
   - Diagramas de caja para variables cuantitativas
   - Gráficos de barras para variables cualitativas
   - Gráficos de líneas para series temporales

2. **Análisis de correlación y causalidad**:
   - Coeficiente de correlación de Pearson y Spearman
   - Diferenciación entre correlación y causalidad

3. **Transformación de variables**:
   - Normalización y estandarización
   - Codificación de variables categóricas (one-hot encoding, label encoding)

4. **Técnicas de imputación de valores faltantes** según el tipo de variable

5. **Análisis de outliers** y técnicas para su tratamiento

6. **Introducción a modelos estadísticos** específicos para series temporales (ARIMA, suavizado exponencial)

7. **Análisis de estacionalidad y tendencia** en series temporales

Estos conocimientos sentarán las bases para el análisis exploratorio avanzado y la construcción de modelos predictivos más robustos.
