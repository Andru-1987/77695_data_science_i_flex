# Ejercicios de Manipulación de DataFrames con Series Temporales

## Configuración inicial
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from datetime import datetime, timedelta

# Configurar estilo de gráficos
plt.style.use('default')
```

## 1. Creación de DataFrame con Series Temporales

```python
# Crear rango de fechas
fechas = pd.date_range(start='2023-01-01', end='2023-12-31', freq='D')

# Crear datos sintéticos
np.random.seed(42)
datos = {
    'temperatura': np.random.normal(25, 5, len(fechas)) + 10 * np.sin(2 * np.pi * np.arange(len(fechas)) / 365),
    'humedad': np.random.normal(60, 15, len(fechas)),
    'ventas': np.random.poisson(50, len(fechas)) * (1 + 0.3 * np.sin(2 * np.pi * np.arange(len(fechas)) / 30))
}

# Crear DataFrame
df = pd.DataFrame(datos, index=fechas)
df.index.name = 'fecha'

print("Primeras 5 filas del DataFrame:")
print(df.head())
print(f"\nDimensión del DataFrame: {df.shape}")
```

## 2. Ejercicios de Manipulación

### Ejercicio 1: Resampleo y agregación
```python
# Resampleo mensual - promedio
df_mensual = df.resample('M').mean()
print("Promedio mensual:")
print(df_mensual.head())

# Resampleo semanal - suma de ventas
df_semanal_ventas = df['ventas'].resample('W').sum()
print("\nVentas semanales (suma):")
print(df_semanal_ventas.head())

# Resampleo trimestral - múltiples agregaciones
df_trimestral = df.resample('Q').agg({
    'temperatura': ['mean', 'min', 'max'],
    'humedad': 'mean',
    'ventas': 'sum'
})
print("\nEstadísticas trimestrales:")
print(df_trimestral.head())
```

### Ejercicio 2: Rolling windows y moving averages
```python
# Media móvil de 7 días
df['temp_ma_7d'] = df['temperatura'].rolling(window=7).mean()
df['ventas_ma_30d'] = df['ventas'].rolling(window=30).mean()

# Rolling statistics
df['temp_std_14d'] = df['temperatura'].rolling(window=14).std()
df['ventas_max_30d'] = df['ventas'].rolling(window=30).max()

print("DataFrame con estadísticas móviles:")
print(df[['temperatura', 'temp_ma_7d', 'ventas', 'ventas_ma_30d']].head(10))
```

### Ejercicio 3: Diferencias y cambios porcentuales
```python
# Diferencias diarias
df['cambio_temp'] = df['temperatura'].diff()
df['cambio_ventas'] = df['ventas'].diff()

# Cambios porcentuales
df['pct_cambio_temp'] = df['temperatura'].pct_change() * 100
df['pct_cambio_ventas'] = df['ventas'].pct_change() * 100

print("Diferencias y cambios porcentuales:")
print(df[['temperatura', 'cambio_temp', 'pct_cambio_temp']].head(10))
```

### Ejercicio 4: Agrupamiento por características temporales
```python
# Extraer componentes temporales
df['mes'] = df.index.month
df['dia_semana'] = df.index.dayofweek  # 0=Lunes, 6=Domingo
df['trimestre'] = df.index.quarter
df['es_fin_semana'] = df.index.dayofweek.isin([5, 6])

# Estadísticas por mes
stats_mensuales = df.groupby('mes').agg({
    'temperatura': ['mean', 'std', 'min', 'max'],
    'ventas': 'sum'
})
print("Estadísticas por mes:")
print(stats_mensuales)

# Ventas promedio por día de la semana
ventas_dia_semana = df.groupby('dia_semana')['ventas'].mean()
print("\nVentas promedio por día de la semana:")
print(ventas_dia_semana)
```

### Ejercicio 5: Manipulación de fechas y periodos
```python
# Shift temporal - comparar con periodo anterior
df['ventas_prev_week'] = df['ventas'].shift(7)  # Misma semana anterior
df['temp_prev_year'] = df['temperatura'].shift(365)  # Mismo día año anterior

# Crear períodos
df['periodo_mensual'] = df.index.to_period('M')
df['periodo_trimestral'] = df.index.to_period('Q')

# Diferencia con mismo día de la semana anterior
df['diff_ventas_semanal'] = df['ventas'] - df['ventas'].shift(7)

print("Comparaciones temporales:")
print(df[['ventas', 'ventas_prev_week', 'diff_ventas_semanal']].head(15))
```

## 3. Visualización de Series Temporales

```python
# Crear figura con múltiples subplots
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(15, 10))

# 1. Serie temporal original
ax1.plot(df.index, df['temperatura'], label='Temperatura diaria', alpha=0.7)
ax1.plot(df.index, df['temp_ma_7d'], label='Media móvil 7 días', color='red', linewidth=2)
ax1.set_title('Temperatura - Serie Temporal')
ax1.set_ylabel('Temperatura (°C)')
ax1.legend()
ax1.grid(True, alpha=0.3)

# 2. Ventas con media móvil
ax2.plot(df.index, df['ventas'], label='Ventas diarias', alpha=0.7, color='green')
ax2.plot(df.index, df['ventas_ma_30d'], label='Media móvil 30 días', color='orange', linewidth=2)
ax2.set_title('Ventas - Serie Temporal')
ax2.set_ylabel('Ventas')
ax2.legend()
ax2.grid(True, alpha=0.3)

# 3. Boxplot por mes
meses = ['Ene', 'Feb', 'Mar', 'Abr', 'May', 'Jun', 
         'Jul', 'Ago', 'Sep', 'Oct', 'Nov', 'Dic']
df.boxplot(column='temperatura', by='mes', ax=ax3)
ax3.set_title('Distribución de Temperatura por Mes')
ax3.set_xticklabels(meses)
ax3.set_ylabel('Temperatura (°C)')

# 4. Ventas por día de la semana
dias_semana = ['Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb', 'Dom']
ventas_dia_semana.plot(kind='bar', ax=ax4, color='skyblue')
ax4.set_title('Ventas Promedio por Día de la Semana')
ax4.set_xlabel('Día de la Semana')
ax4.set_ylabel('Ventas Promedio')
ax4.set_xticklabels(dias_semana, rotation=0)

plt.tight_layout()
plt.show()
```

## 4. Ejercicio Adicional: Análisis de Estacionalidad

```python
# Análisis de estacionalidad mensual
estacionalidad_mensual = df.groupby('mes').agg({
    'temperatura': 'mean',
    'ventas': 'mean'
}).rename(index=lambda x: meses[x-1])

# Normalizar para ver patrones estacionales
estacionalidad_mensual['temp_norm'] = (estacionalidad_mensual['temperatura'] / 
                                      estacionalidad_mensual['temperatura'].mean())
estacionalidad_mensual['ventas_norm'] = (estacionalidad_mensual['ventas'] / 
                                        estacionalidad_mensual['ventas'].mean())

print("Patrones estacionales mensuales (normalizados):")
print(estacionalidad_mensual[['temp_norm', 'ventas_norm']])

# Gráfico de estacionalidad
plt.figure(figsize=(12, 5))
plt.plot(estacionalidad_mensual.index, estacionalidad_mensual['temp_norm'], 
         marker='o', label='Temperatura', linewidth=2)
plt.plot(estacionalidad_mensual.index, estacionalidad_mensual['ventas_norm'], 
         marker='s', label='Ventas', linewidth=2)
plt.axhline(y=1, color='red', linestyle='--', alpha=0.5, label='Promedio')
plt.title('Patrones Estacionales Mensuales (Normalizados)')
plt.xlabel('Mes')
plt.ylabel('Valor Normalizado')
plt.legend()
plt.grid(True, alpha=0.3)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

