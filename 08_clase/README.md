# Apredizaje no supervisado  *¿Qué es el Clustering?*

El **clustering** es una técnica de aprendizaje no supervisado que agrupa objetos similares en un mismo grupo (clúster) y separa los que son diferentes.
Se usa en segmentación de clientes, análisis de imágenes, detección de patrones, entre otros.
[Modlos de Clustering](https://hpsuresh12345.medium.com/cluster-analysis-6757d6c6acc9)

---

# Principales enfoques de Clustering

### 1. Particionales

Dividen los datos en *k* grupos predefinidos.

* **K-means**: Asigna puntos al centro más cercano.
* **PAM**: Usa puntos reales (medoides).
* **CLARA**: Versión de PAM para grandes volúmenes.
* **FCM**: Un punto puede pertenecer parcialmente a varios clústeres.

**Ventajas:** rápido y simple.
**Desventajas:** sensible a la forma de los clústeres y a la inicialización.

[Clustering Particionales](https://medium.com/data-science/17-clustering-algorithms-used-in-data-science-mining-49dbfa5bf69a)

---

### 2. Jerárquicos

Construyen una estructura en forma de árbol (dendrograma).

* **Aglomerativo**: Une clústeres paso a paso.
* **Divisivo**: Divide grupos grandes en más pequeños.

**Ventajas:** no requiere definir *k*.
**Desventajas:** costoso en cómputo.

[Clustering Jerarquicos](https://geekscoach.medium.com/clustering-jer%C3%A1rquico-hierarchical-clustering-e3ccd36117b0)
---

### 3. Basados en Densidad

Agrupan puntos densamente conectados.

* **DBSCAN**: Detecta outliers y clústeres arbitrarios.
* **OPTICS**: Maneja densidades variables.

**Ventajas:** detecta formas complejas, maneja ruido.
**Desventajas:** difícil elegir parámetros.


[Clustering Densidad](https://www.atlantbh.com/clustering-algorithms-dbscan-vs-optics/)

---

### 4. Basados en Grillas

Dividen el espacio en celdas y agrupan según densidad local.

* **CLIQUE**, **STING**, **Wavecluster**.

**Ventajas:** eficiente en altas dimensiones.
**Desventajas:** depende del tamaño de las celdas.

- [Clustering Grills](https://www.atlantbh.com/clustering-algorithms-dbscan-vs-optics/)

---

### 5. Basados en Modelos

Asumen que los datos vienen de un modelo estadístico.

* **GMM**: Combinación de distribuciones normales.
* **SOMs**: Redes neuronales que mapean datos en 2D.

**Ventajas:** modelos flexibles y probabilísticos.
**Desventajas:** requieren supuestos sobre la distribución.
[Clustering By Models](https://hpsuresh12345.medium.com/cluster-analysis-6757d6c6acc9)

---

Para empezar, lo más usado en Data Science inicial es:

* **K-means** (rápido y simple).
* **DBSCAN** (para formas irregulares y detección de outliers).
* **Jerárquico** (para visualizar relaciones entre grupos).
