## Clase 10 - CLase Final y Recomendaciones para el proyecto Final

- [DIAPOSITIVA](https://docs.google.com/presentation/d/1pYAm0WjIsU8mDrXxVUtetFwZEOvJvufgpEE-zVZbc2I/edit?slide=id.g221c7b9e280_0_471#slide=id.g221c7b9e280_0_471)

---
### Propuesta de solución con Machine Learning

| Objetivo del negocio                         | Enfoque ML propuesto                                                                                          |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Predecir día de arribo**                   | Modelo de regresión que estime el *lead time* (días entre despacho y entrega).                                |
| **Predecir franja horaria (mañana / tarde)** | Clasificador binario supervisado, alimentado con la misma matriz de características.                          |
| **Avisar al usuario**                        | API de inferencia en línea ‑o un microservicio event‑driven‑ que consulta el modelo y dispara notificaciones. |
| **Optimizar la logística**                   | Explicar la predicción (SHAP) para entender cuellos de botella y replanificar rutas o asignaciones.           |
| **Mejorar la experiencia**                   | Predicciones probabilísticas (p95‑p05) → comunicamos fecha y margen de error; genera confianza.               |

---

## 1. Formulación del problema

* **Regresión multiclase discreta**
  Convertir la fecha destino en *días hasta la entrega* (`eta_days`) y predecir un valor entero ≥ 0.
  Ventaja: elimina la complejidad de trabajar con calendarios y feriados en la capa de modelado.

* **Clasificación binaria**
  Etiqueta `slot = {0: mañana, 1: tarde}` definida por hora real de entrega.

* **Posibilidad avanzada**: Modelo multi‑tarea (e.g. LightGBM con objetivos múltiples) que aprenda simultáneamente ambos targets y capture interdependencias.

---

## 2. Datos necesarios

| Tipo de dato                       | Ejemplos de campos                                                     | Motivo                                               |
| ---------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------- |
| **Paquete**                        | peso, volumen, servicio (exprés / estándar), valor declarado           | Impacto en priorización y manipulación.              |
| **Origen‑destino**                 | código postal, distancia, densidad poblacional                         | Relaciona con tráfico, disponibilidad de sucursales. |
| **Temporal**                       | fecha/hora de admisión, día de semana, feriados, temporada alta        | Influye en capacidad y congestión.                   |
| **Logística interna**              | centro de distribución de salida/llegada, ruta planificada, driver\_id | Explica cuellos de transporte y carga de trabajo.    |
| **Contexto externo (enriquecido)** | pronóstico de clima, alertas de tránsito, huelgas                      | Reduce varianza causada por factores exógenos.       |

Crear un **Feature Store** (p. ej. Feast o Tecton) para unificar estas fuentes y servir tanto offline como online.

---

## 3. Ingeniería de características

1. **Categóricas**

   * Codificación *target‑based* o *leave‑one‑out* para códigos postales, centros de distribución.
2. **Numéricas**

   * Distancia Haversine, densidad de bultos en la misma ruta, ratio peso/volumen.
3. **Frecuencias históricas**

   * Tiempo promedio por tramo logístico (CD → Sucursal, CD → Última Milla).
4. **Ventanas temporales**

   * Cálculo rolling de congestión: paquetes despachados en las últimas 4 h, 24 h.
5. **Calendario enriquecido**

   * Feriados nacionales y provinciales, quiebre mes, picos estacionales (CyberMonday, Navidad).
6. **Clima**

   * Proyecciones de lluvia/nieve a 48 h en destino; discretizar en niveles de severidad.

---

## 4. Modelos candidatos

| Modelo                                                      | Pros                                                                           | Contras                                                              |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------ | -------------------------------------------------------------------- |
| **Gradient Boosting Trees** (LightGBM / XGBoost / CatBoost) | Lidera en tabulares; manejo nulo de *data prep*; soporta cuantiles             | Interpretabilidad media; se entrena más lento con millones de filas. |
| **Redes tabulares** (TabNet, DeepGBM)                       | Capturan interacciones no lineales; funcionan bien con *embeddings*            | Mayor coste entrenamiento, requiere tuning fino.                     |
| **Survival Analysis / GBDT‑survival**                       | Modela explícitamente la distribución de tiempo; adecuado a eventos censurados | Más complejo de explicar a negocio.                                  |

**Recomendación inicial**: LightGBM ‑ rápido *time‑to‑value*, soporta modo *multiclass* + *quantile regression* (p50, p75, p90). 

---

## 5. Métricas de evaluación

| Target     | Métricas offline                         | Métricas online (post‑deploy)                                                            |
| ---------- | ---------------------------------------- | ---------------------------------------------------------------------------------------- |
| `eta_days` | MAE, RMSE, *pinball loss* para cuantiles | Desviación absoluta media vs. real; porcentaje de entregas dentro del intervalo p90‑p10. |
| `slot`     | Accuracy, F1‑score, ROC‑AUC              | Rate de correctas por día; impacto en re‑intentos de entrega.                            |

Establecer un **baseline** con reglas heurísticas (p. ej. promedio histórico por ruta) para medir uplift real del modelo.


---

**Aplicaciones prácticas de Machine Learning**

La clase presenta ejemplos reales de cómo la Ciencia de Datos se aplica en distintas industrias (automotriz, seguros, logística, hotelería, e-commerce y transporte urbano).

Se analizan los siguientes casos de éxito:

* **Mazda:** uso de segmentación de clientes mediante clustering para diseñar estrategias de marketing específicas.
* **San Cristóbal Seguros:** análisis de datos para identificar patrones y mejorar servicios aseguradores.
* **Andreani:** modelo predictivo para estimar tiempos y franjas horarias de entrega, optimizando la logística.
* **Medplaya (hoteles):** predicción de cancelaciones de reservas para maximizar ocupación e ingresos.
* **Amazon:** sistemas de recomendación basados en filtrado colaborativo y contenido para anticipar preferencias del cliente.
* **Accidentes en Nueva York:** caso de análisis predictivo y feature engineering para diseñar estrategias de reducción de siniestros.


## Entrega `Proyecto Final`

La consigna práctica consiste en crear un notebook con:

1. Selección de características (feature selection).
2. Entrenamiento de un modelo de regresión o clasificación.
3. Evaluación de métricas básicas.
4. Conclusiones basadas en los resultados.

Se cierra la clase con la estructuración del **Proyecto Final Parte III**, donde se debe aplicar todo lo aprendido en un notebook probado y subido a GitHub.
