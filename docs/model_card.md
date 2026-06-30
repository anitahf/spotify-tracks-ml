# MODEL CARD

## Spotify Hit Predictor  
**Predicción de popularidad de canciones mediante Machine Learning**

**Proyecto:** Spotify Hit Predictor  
**Repositorio:** `spotify-tracks-ml`  
**Fuente principal de datos:** Spotify Tracks Dataset - Kaggle  
**Tipo de modelo:** Clasificación supervisada binaria  
**Variable objetivo:** `popular`  
**Área de aplicación:** Industria musical, analítica de canciones y apoyo a decisiones de promoción  
**Organización simulada:** Sello discográfico independiente  
**Fecha de inicio:** 30 de junio de 2026  
**Unidad de análisis:** Canción única identificada mediante `track_id`

Documento de transparencia, uso responsable, desempeño, limitaciones y consideraciones éticas del modelo.

---

## 1. Información general del modelo

| Campo | Descripción |
|---|---|
| Nombre del modelo | Spotify Hit Predictor. |
| Tipo de tarea | Clasificación supervisada binaria. |
| Algoritmo seleccionado | Pendiente de confirmar con el modelo de mejor desempeño en el notebook final. |
| Responsable del Model Card | David Zapata - ML Engineer / Ethics & Impact Lead. |
| Responsable de modelado | Gabriela Cárdenas - Data Scientist. |
| Objetivo del modelo | Predecir si una canción puede alcanzar un nivel relevante de popularidad en Spotify. |
| Salida esperada | Etiqueta binaria: `popular = 1` o `popular = 0`. |
| Umbral de popularidad | `popular = 1` si `popularity >= 50`; `popular = 0` si `popularity < 50`. |
| Usuario principal | Sello discográfico independiente que necesita priorizar recursos de promoción. |

---

## 2. Propósito del modelo

El propósito del modelo es apoyar la toma de decisiones de un sello discográfico independiente que cuenta con recursos limitados para producción, promoción y distribución de canciones. En lugar de depender únicamente del criterio experto, el modelo busca entregar una estimación analítica sobre qué canciones tienen mayor probabilidad de alcanzar una popularidad igual o superior a 50 en Spotify.

La finalidad del modelo no es reemplazar la decisión de productores, artistas, equipos de marketing o especialistas musicales. Su función es servir como una herramienta de apoyo para priorizar canciones, orientar campañas promocionales y detectar patrones asociados con canciones potencialmente populares.

---

## 3. Usuarios previstos

- Líderes de proyecto y equipos de estrategia musical.
- Analistas de datos del sello discográfico.
- Equipos de marketing musical y promoción digital.
- Productores o responsables de selección de canciones.
- Equipos técnicos encargados de monitoreo, dashboards y reportes.

El modelo debe ser utilizado por personas capaces de interpretar resultados de Machine Learning y contrastarlos con criterio musical, comercial y contextual. No se recomienda su uso automático sin revisión humana.

---

## 4. Datos utilizados

El modelo utiliza el **Spotify Tracks Dataset** disponible en Kaggle. La unidad de análisis es una canción única identificada mediante `track_id`. Para evitar fuga de información y duplicidad, el dataset debe ser limpiado y consolidado antes del entrenamiento.

Variables principales consideradas:

- `track_id`: identificador único de la canción.
- `track_name`: nombre de la canción.
- `artists`: artista o artistas asociados.
- `album_name`: álbum al que pertenece la canción.
- `track_genre`: género musical principal.
- `popularity`: puntaje de popularidad usado para construir la variable objetivo.
- `duration_ms`: duración de la canción en milisegundos.
- `explicit`: indica si la canción tiene contenido explícito.
- `danceability`: nivel de facilidad para bailar la canción.
- `energy`: intensidad y actividad percibida.
- `key`: tonalidad musical.
- `loudness`: volumen general en decibeles.
- `mode`: modo musical.
- `speechiness`: presencia de palabras habladas.
- `acousticness`: grado de sonido acústico.
- `instrumentalness`: probabilidad de que la canción sea instrumental.
- `liveness`: probabilidad de que la canción sea en vivo.
- `valence`: positividad musical percibida.
- `tempo`: velocidad de la canción en BPM.
- `time_signature`: compás de la canción.

La variable objetivo corresponde a:

```text
popular = 1, si popularity >= 50
popular = 0, si popularity < 50
```

---

## 5. Descripción de la tarea

El problema corresponde a una tarea de **clasificación supervisada binaria**. El modelo recibe como entrada características musicales, técnicas y de género de una canción, y devuelve una predicción sobre si la canción será clasificada como popular o no popular.

> **Pregunta que responde el modelo:** Dadas las características musicales y técnicas de una canción, ¿es posible predecir si alcanzará una popularidad mayor o igual a 50 en Spotify?

---

## 6. Desempeño del modelo seleccionado

El modelo final debe seleccionarse comparando varios modelos de clasificación. El criterio de selección recomendado es combinar métricas técnicas y criterios de negocio, especialmente porque el sello discográfico necesita detectar canciones con potencial sin desperdiciar demasiados recursos promocionales.

| Métrica | Valor | Interpretación |
|---|---:|---|
| Accuracy | Pendiente | Porcentaje total de canciones correctamente clasificadas. |
| Precision | Pendiente | De las canciones predichas como populares, cuántas realmente fueron populares. |
| Recall | Pendiente | De las canciones realmente populares, cuántas logró detectar el modelo. |
| F1-score | Pendiente | Balance entre precision y recall. |
| ROC-AUC | Pendiente | Capacidad del modelo para separar canciones populares y no populares. |
| PR-AUC | Pendiente | Útil si existe desbalance entre canciones populares y no populares. |

**Criterio recomendado de selección:** priorizar un buen equilibrio entre **F1-score**, **Recall de la clase popular** y **ROC-AUC**. En este proyecto, un falso negativo puede ser importante porque significa que una canción con potencial no recibiría inversión promocional.

---

## 7. Resultados por clase

| Clase | Significado | Precision | Recall | F1-score | Soporte |
|---|---|---:|---:|---:|---:|
| `0` | Canción no popular (`popularity < 50`) | Pendiente | Pendiente | Pendiente | Pendiente |
| `1` | Canción popular (`popularity >= 50`) | Pendiente | Pendiente | Pendiente | Pendiente |

La clase más crítica para el negocio es `popular = 1`, porque representa canciones que podrían justificar inversión en promoción. Sin embargo, también debe controlarse la cantidad de falsos positivos, ya que promocionar demasiadas canciones con baja probabilidad real puede generar gasto innecesario.

---

## 8. Análisis de errores

| Tipo de error | Descripción | Impacto en el negocio |
|---|---|---|
| Falso positivo | El modelo predice que una canción será popular, pero realmente no alcanza `popularity >= 50`. | Puede provocar inversión promocional en canciones con bajo retorno. |
| Falso negativo | El modelo predice que una canción no será popular, pero realmente sí alcanza `popularity >= 50`. | Puede hacer que el sello pierda una oportunidad de promoción o distribución. |

El error más delicado desde el punto de vista estratégico es el **falso negativo**, porque una canción con potencial podría quedar fuera de campañas importantes. Aun así, los falsos positivos también deben vigilarse porque el sello tiene recursos limitados.

| Indicador | Valor |
|---|---:|
| Total de canciones evaluadas | Pendiente |
| Canciones clasificadas correctamente | Pendiente |
| Canciones clasificadas incorrectamente | Pendiente |
| Falsos positivos | Pendiente |
| Falsos negativos | Pendiente |

---

## 9. Uso previsto del modelo

- Priorizar canciones con mayor probabilidad de ser populares.
- Apoyar decisiones de promoción en Spotify y plataformas digitales.
- Identificar patrones musicales asociados con mayor popularidad.
- Complementar análisis exploratorios y dashboards del proyecto.
- Comparar canciones nuevas con características de canciones populares del dataset.
- Apoyar presentaciones ejecutivas para justificar decisiones basadas en datos.

El modelo debe utilizarse como una herramienta de apoyo, no como una decisión final automática.

---

## 10. Usos no recomendados

- Decidir de forma definitiva qué artistas o canciones deben recibir apoyo.
- Rechazar canciones únicamente por la predicción del modelo.
- Usar el modelo como sustituto del criterio musical, creativo o comercial.
- Aplicarlo a canciones fuera del contexto del dataset sin validación previa.
- Usar la predicción como garantía de éxito comercial.
- Evaluar talento artístico individual solo con base en variables numéricas.
- Tomar decisiones que afecten contratos, inversión o distribución sin revisión humana.

El modelo predice patrones a partir de datos históricos, pero no puede capturar por completo el contexto cultural, viralidad, marketing, comunidad de fans o calidad artística de una canción.

---

## 11. Consideraciones éticas

El modelo trabaja con datos musicales y de popularidad, no con datos sensibles de personas. Aun así, su uso puede afectar decisiones comerciales sobre artistas, géneros y canciones. Por eso se deben considerar los siguientes puntos:

- Transparencia sobre qué predice el modelo y qué variables utiliza.
- Revisión humana antes de tomar decisiones relevantes de inversión.
- Prevención de sesgos contra géneros musicales menos representados.
- Evitar que el modelo limite la diversidad creativa del sello.
- No interpretar la popularidad como sinónimo absoluto de calidad musical.
- Documentar limitaciones, riesgos y supuestos del dataset.
- Respetar las condiciones de uso de Kaggle y de la fuente de datos.

---

## 12. Fairness y revisión de sesgo

Aunque el modelo no clasifica personas, puede presentar sesgos por género musical, tipo de contenido o características históricas de popularidad. Por ejemplo, si ciertos géneros tienen mayor presencia o mayor popularidad promedio en el dataset, el modelo podría favorecerlos frente a géneros más pequeños o de nicho.

Se recomienda evaluar el desempeño por subgrupos como:

- `track_genre` o grupos de géneros musicales.
- Canciones explícitas vs. no explícitas.
- Canciones cortas vs. canciones largas.
- Rangos de tempo.
- Niveles de energía o bailabilidad.

| Grupo evaluado | Métrica recomendada | Valor | Observación |
|---|---|---:|---|
| Géneros populares | Recall / F1-score | Pendiente | Revisar si el modelo favorece géneros dominantes. |
| Géneros de nicho | Recall / F1-score | Pendiente | Verificar si el modelo subestima canciones de menor representación. |
| Canciones explícitas | Precision / Recall | Pendiente | Analizar diferencias frente a canciones no explícitas. |
| Canciones no explícitas | Precision / Recall | Pendiente | Comparar comportamiento del modelo. |

Si se detecta una diferencia mayor a 10 puntos porcentuales entre grupos relevantes, se recomienda revisar el modelo antes de usarlo en decisiones de promoción.

---

## 13. Transparencia y explicabilidad

El modelo debe explicarse en lenguaje claro para que pueda ser entendido por personas no especialistas en Machine Learning.

**Explicación simple:** el modelo analiza características de una canción, como energía, bailabilidad, duración, contenido explícito, tempo, género y otros atributos musicales, para estimar si puede alcanzar una popularidad mayor o igual a 50 en Spotify.

Para mejorar la explicabilidad, se recomienda acompañar cada predicción con información sobre los factores que más influyeron en el resultado. En modelos interpretables se pueden usar coeficientes o importancia de variables; en modelos más complejos se pueden utilizar herramientas como importancia de características o análisis SHAP.

---

## 14. Cumplimiento y manejo responsable de datos

| Criterio | Aplicación al modelo |
|---|---|
| Finalidad | El propósito es específico: apoyar la priorización de canciones para promoción musical. |
| Minimización de datos | Solo deben usarse variables necesarias para la predicción. |
| Transparencia | El equipo debe documentar qué datos se usaron, cómo se limpió el dataset y qué limitaciones existen. |
| Trazabilidad | Se recomienda registrar versiones del dataset, modelos y métricas mediante MLflow u otra herramienta. |
| Conservación | Los datasets procesados y predicciones deben almacenarse con control de versiones y evitar duplicados innecesarios. |
| Uso de datos públicos | Deben respetarse las condiciones de uso del dataset de Kaggle y cualquier restricción de la fuente original. |
| Revisión humana | Las predicciones deben revisarse antes de convertirse en decisiones comerciales. |

Aunque el dataset no contiene datos personales sensibles de usuarios, sí puede incluir información asociada a artistas y canciones. Por eso se recomienda utilizarlo únicamente con fines académicos y analíticos dentro del alcance del proyecto.

---

## 15. Limitaciones del modelo

- La popularidad en Spotify puede cambiar con el tiempo.
- El umbral `popularity >= 50` es una decisión del proyecto y puede ser discutible.
- El dataset puede contener canciones duplicadas o versiones repetidas si no se limpia correctamente.
- La popularidad no depende solo de características musicales; también influyen marketing, playlists, redes sociales, comunidad de fans, colaboraciones y contexto cultural.
- Algunos géneros pueden estar mejor representados que otros.
- El modelo puede aprender patrones históricos y no necesariamente anticipar tendencias futuras.
- El modelo no mide calidad artística, originalidad ni valor cultural.
- Si se incluyen variables como artista o álbum, existe riesgo de que el modelo aprenda fama previa en lugar de características musicales.

---

## 16. Riesgos potenciales

- Promocionar canciones con bajo potencial real por falsos positivos.
- Dejar fuera canciones con potencial por falsos negativos.
- Favorecer géneros dominantes y reducir diversidad musical.
- Interpretar la predicción como una verdad absoluta.
- Usar el modelo para justificar decisiones comerciales sin análisis humano.
- Reforzar patrones históricos de popularidad y limitar propuestas nuevas.
- Sobreajustar el modelo si no se controlan duplicados o fuga de información.

---

## 17. Recomendaciones de implementación

- Validar el modelo con un conjunto de prueba separado y bien definido.
- Controlar duplicados por `track_id` y canciones repetidas antes del entrenamiento.
- Comparar varios modelos base antes de seleccionar el modelo final.
- Reportar matriz de confusión, F1-score, recall, precision y ROC-AUC.
- Evaluar el desempeño por grupos de géneros musicales.
- Documentar el pipeline de limpieza, transformación y entrenamiento.
- Registrar experimentos, parámetros y métricas con MLflow.
- Revisar manualmente los casos con alta probabilidad de popularidad antes de tomar decisiones.
- Mantener actualizado el Model Card cuando cambien datos, modelo o métricas.
- Usar el modelo como apoyo estratégico, no como reemplazo de especialistas musicales.

---

## 18. Conclusión

El modelo **Spotify Hit Predictor** busca apoyar a un sello discográfico independiente en la identificación de canciones con potencial de popularidad en Spotify. Al transformar el problema en una tarea de clasificación binaria, el proyecto permite estimar si una canción puede alcanzar una popularidad mayor o igual a 50 a partir de sus características musicales y técnicas.

Su principal valor está en complementar el criterio experto con evidencia basada en datos. Esto puede ayudar a priorizar campañas, asignar mejor los recursos y detectar patrones asociados con canciones populares. Sin embargo, el modelo no debe utilizarse como una herramienta automática de decisión, ya que la popularidad musical depende también de factores externos que no siempre están presentes en el dataset.

En conclusión, el modelo puede aportar valor al proceso de toma de decisiones del sello discográfico, siempre que sea validado correctamente, revisado por el equipo humano y acompañado de controles de transparencia, fairness y responsabilidad ética.

---

## 19. Campos pendientes antes de la entrega final

Para cerrar el Model Card con resultados reales del proyecto, se deben completar los siguientes campos:

- Algoritmo final seleccionado.
- Métricas del modelo final.
- Matriz de confusión.
- Resultados por clase.
- Número total de canciones evaluadas.
- Falsos positivos y falsos negativos.
- Análisis de desempeño por géneros musicales.
- Evidencia del registro de experimentos o pipeline final.
