## **Fundamentos para la Ciencia de Datos**

**Curso:** Data Science I
**Unidad:** 9 - Fundamentos Clave de Data Science
---

[ _Presentacion_ ](https://docs.google.com/presentation/d/1zmIN5N8NCY3Z9f_dm-tkEm3vj387oHs4Jwb2mtpCce8/edit?slide=id.g2f4cdaa5879_2_398#slide=id.g2f4cdaa5879_2_398)

### **1. Objetivos de la Clase**

* Explorar las bases del **Machine Learning (ML)** y reconocer sus conceptos básicos.
* Entender las características de la **Inteligencia Artificial (IA)** y cómo se relaciona con el ML.
* Reconocer las aplicaciones de la IA en la industria y en la vida cotidiana.
* Conocer las **métricas principales** para evaluar el rendimiento de un modelo.
* Analizar los **riesgos y desafíos** que presenta la IA.

---

### **2. Introducción: ¿Qué es la IA y el Machine Learning?**

**¿Qué es la Inteligencia Artificial?**

La **Inteligencia Artificial (IA)** es la capacidad que tienen las máquinas para usar algoritmos, aprender de los datos que reciben y utilizarlos para tomar decisiones.
A diferencia de los humanos, los sistemas con IA pueden analizar grandes volúmenes de información de manera continua, sin necesidad de descanso, y suelen cometer menos errores en tareas repetitivas o de análisis.

**¿Y el Machine Learning (ML) qué rol cumple?**

El **Machine Learning** proporciona los algoritmos que permiten que las máquinas aprendan de los datos.
Podemos pensar que la IA es el concepto general —la meta de crear sistemas inteligentes—, y el ML es una de las herramientas más potentes para lograrlo.
El ML surgió en los años 50 como una forma de resolver problemas complejos de predicción.

**Para pensar:**
¿Cuándo creen que surgió la idea de la IA? ¿Por qué?

---

### **3. La IA en Acción: Aplicaciones Prácticas**

La IA no es ciencia ficción: está presente en múltiples sectores.

**Robótica**

Los robots son un ejemplo claro de IA, dentro de la categoría de “sistemas que actúan como humanos”.
Hoy existen robots dedicados a tareas domésticas, industriales, médicas y de servicios.
También se utilizan en sectores como las finanzas, el turismo, el transporte y el entretenimiento.

**Para debatir:**
Más allá de los robots domésticos, ¿qué otros ejemplos se les ocurren?
¿En qué áreas laborales los ven cada vez más presentes?

**Caso de Estudio: La IA en la Salud**

El área de la salud es uno de los campos donde la IA ha tenido mayor impacto.

* **Radiología e Imágenes Médicas:**
  Los algoritmos de Deep Learning se entrenan con millones de imágenes médicas para detectar anomalías como tumores o fracturas.
  Estos sistemas pueden analizar imágenes en segundos con una precisión que a menudo iguala o supera la de los especialistas.
  Esto acelera los diagnósticos y permite que los médicos se enfoquen en los casos más complejos.

* **Genómica Personalizada:**
  Mediante IA, se analizan secuencias genéticas para identificar mutaciones asociadas a enfermedades.
  Así, se pueden diseñar tratamientos personalizados basados en el perfil genético de cada paciente.

* **Asistentes Virtuales y Atención Personalizada:**
  Los sistemas de IA pueden revisar historiales clínicos completos y ofrecer recomendaciones de tratamiento adaptadas a cada persona.
  Además, los asistentes virtuales ayudan en la comunicación con pacientes, recordatorios de medicación y seguimiento de tratamientos.

**Actividad de Grupo: Análisis del Caso (10 minutos)**

1. **Impactos Positivos:** ¿Cuáles son los principales beneficios que la IA trajo a la salud? ¿Cómo mejoró la calidad del diagnóstico?
2. **Riesgos y Desafíos:** ¿Qué riesgos existen al aplicar IA en diagnósticos médicos? ¿Qué sucede si el algoritmo falla? ¿Cómo se pueden reducir esos riesgos?
3. **El Futuro:** ¿Cómo imaginan el uso de IA en la salud dentro de 10 años? ¿Qué nuevas aplicaciones podrían surgir?

---

### **4. Armado de Modelos: De los Datos al Rendimiento**

Para que un modelo de ML funcione correctamente, no alcanza con usar muchos datos: se necesita una buena estrategia.

**Ingeniería de Factores (Feature Engineering)**

Este proceso consiste en seleccionar, crear y transformar variables que ayuden al modelo a aprender mejor.
Por ejemplo, al predecir el precio de una vivienda, podríamos incluir variables como ubicación, superficie y cantidad de baños.

**Aprendizaje y Validación: Overfitting y Underfitting**

Es fundamental evaluar el modelo con **datos nuevos** (que no haya visto durante el entrenamiento) para evitar errores comunes:

* **Underfitting (Subajuste):**
  Ocurre cuando el modelo es demasiado simple y no logra captar la complejidad de los datos.
* **Overfitting (Sobreajuste):**
  Pasa cuando el modelo se ajusta demasiado a los datos de entrenamiento, incluyendo el ruido y los errores, por lo que falla con datos nuevos.
* **El punto ideal:**
  Es el equilibrio entre ambos extremos: un modelo lo suficientemente complejo como para entender la estructura de los datos, pero generalizable.

**Métricas de Rendimiento**

Para medir el desempeño de un modelo:

* **Clasificación:**
  Se utilizan métricas como **Exactitud (Accuracy)**, **Precisión**, **Sensibilidad (Recall)**, **Especificidad** y **F1 Score**.
* **Regresión:**
  Se aplican métricas como **Error Cuadrático Medio (MSE)** o **Error Absoluto Medio (MAE)**.

**Ejemplo en Python**

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

# Valores reales
y_true = [0, 1, 1, 0, 1, 1, 0, 1, 0, 1]

# Predicciones del modelo
y_pred = [0, 1, 0, 0, 1, 1, 0, 1, 1, 1]

accuracy = accuracy_score(y_true, y_pred)
precision = precision_score(y_true, y_pred)
recall = recall_score(y_true, y_pred)
f1 = f1_score(y_true, y_pred)

print(f"Exactitud (Accuracy): {accuracy:.2f}")
print(f"Precisión (Precision): {precision:.2f}")
print(f"Sensibilidad (Recall): {recall:.2f}")
print(f"F1-Score: {f1:.2f}")
```

**Para pensar:**
En un filtro de spam, ¿qué sería peor: que un correo importante termine en spam (falso negativo) o que un correo basura llegue a la bandeja de entrada (falso positivo)?
¿Qué métrica analizarían con más cuidado?

---

### **5. El Futuro de la IA: Riesgos y Desafíos**

El avance de la IA plantea beneficios enormes, pero también riesgos que deben considerarse.

**Riesgos y Desafíos**

Un mal uso de la IA puede tener impactos negativos en la sociedad.
Algunos de los principales desafíos son:

* **Sesgos:** Si la IA aprende a partir de datos injustos o discriminatorios, puede replicar y amplificar esos sesgos.
* **Trabajo:** La automatización puede reemplazar ciertos empleos y transformar el mercado laboral.
* **Seguridad:** Los sistemas de IA mal utilizados pueden representar amenazas, por ejemplo, en el uso de información personal.
* **Creatividad:** Surge la pregunta de si la IA puede generar contenido con la misma calidad y sentido creativo que un humano.

**Actividad: La Evolución del Trabajo (10 minutos)**
1. Piensen en los trabajos que tenían sus padres o abuelos.
2. ¿Siguen existiendo esos puestos? ¿Podrían ser reemplazados por la IA?
