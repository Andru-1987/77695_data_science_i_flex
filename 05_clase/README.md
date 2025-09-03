# Visualizaciones con Matplotlib
[Diapositivas](https://docs.google.com/presentation/d/1BCmhYqiqKTKSm4hUkzXXuEcBJTAXw25j3oYJyqioTPQ/edit?slide=id.p1#slide=id.p1)

*Esta guía muestra cómo crear gráficos básicos con `matplotlib`, superponer líneas en gráficos de dispersión, combinar múltiples visualizaciones en una misma figura, y crear un gráfico de paleta (lollipop)*

## 1. Gráfico básico con Matplotlib

```python
import matplotlib.pyplot as plt
import numpy as np

# Datos para el gráfico
t = np.linspace(0, 10, 100)  # 100 puntos entre 0 y 10
y = np.sin(t)  # Función seno

# Crear gráfico
plt.figure(figsize=(8, 4))
plt.plot(t, y, label='sin(t)', color='blue', linestyle='-', linewidth=2)
plt.title('Gráfico de la función seno')
plt.xlabel('Tiempo (t)')
plt.ylabel('Amplitud sin(t)')
plt.legend()
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()
```

## 2. Superponer líneas sobre un Scatterplot

```python
np.random.seed(42)  # Para reproducibilidad
x = np.random.rand(50)  # 50 valores aleatorios entre 0 y 1
y = 2 * x + 1 + np.random.normal(scale=0.1, size=50)  # Datos con ruido

# Línea de regresión teórica
x_line = np.linspace(0, 1, 100)
y_line = 2 * x_line + 1

# Crear scatterplot con línea superpuesta
plt.figure(figsize=(6, 4))
plt.scatter(x, y, label='Datos observados', color='darkorange', alpha=0.7)
plt.plot(x_line, y_line, color='blue', linewidth=2, label='y = 2x + 1 (teórica)')
plt.title('Scatterplot con línea de regresión')
plt.xlabel('Variable x')
plt.ylabel('Variable y')
plt.legend()
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()
```

## 3. Figura con múltiples visualizaciones

```python
# Crear figura con 3 subplots
fig, axs = plt.subplots(1, 3, figsize=(15, 4))

# 1. Scatterplot con línea
axs[0].scatter(x, y, color='darkorange', alpha=0.7)
axs[0].plot(x_line, y_line, color='blue', linewidth=2)
axs[0].set_title('Scatterplot con línea')
axs[0].set_xlabel('x')
axs[0].set_ylabel('y')
axs[0].grid(True, alpha=0.3)

# 2. Histograma
axs[1].hist(y, bins=10, color='green', alpha=0.7, edgecolor='black')
axs[1].set_title('Distribución de y')
axs[1].set_xlabel('Valores de y')
axs[1].set_ylabel('Frecuencia')
axs[1].grid(True, alpha=0.3)

# 3. Función seno
axs[2].plot(t, np.sin(t), color='purple', linewidth=2)
axs[2].set_title('Función senoidal')
axs[2].set_xlabel('Tiempo (t)')
axs[2].set_ylabel('sin(t)')
axs[2].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
```

## 4. Gráfico de Paleta (Lollipop Graph)

```python
# Datos para el gráfico de paleta
categorias = ['Producto A', 'Producto B', 'Producto C', 'Producto D', 'Producto E']
valores = [23, 45, 56, 78, 32]

# Crear gráfico de paleta
plt.figure(figsize=(10, 6))

# Crear líneas verticales (los "palos" del gráfico)
plt.vlines(x=categorias, ymin=0, ymax=valores, color='skyblue', linewidth=2)

# Crear puntos en los extremos (las "paletas")
plt.scatter(categorias, valores, color='navy', s=100, zorder=3)

# Personalizar el gráfico
plt.title('Gráfico de Paleta - Ventas por Producto')
plt.xlabel('Productos')
plt.ylabel('Ventas (unidades)')
plt.xticks(rotation=45)
plt.grid(True, alpha=0.3, axis='y')

# Añadir valores en los puntos
for i, valor in enumerate(valores):
    plt.text(i, valor + 2, str(valor), ha='center', va='bottom', fontweight='bold')

plt.tight_layout()
plt.show()
```

## Explicación de conceptos importantes:

- **plt.figure()**: Crea una nueva figura
- **figsize**: Controla el tamaño de la figura (ancho, alto en pulgadas)
- **plt.subplots()**: Crea múltiples subplots en una figura
- **alpha**: Controla la transparencia (0 = transparente, 1 = opaco)
- **zorder**: Controla el orden de visualización (mayor valor = más arriba)
- **tight_layout()**: Ajusta automáticamente los espacios entre subplots
- **grid()**: Añade una cuadrícula al gráfico

