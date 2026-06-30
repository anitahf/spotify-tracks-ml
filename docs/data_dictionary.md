# Diccionario de Datos — Spotify Popularity Prediction

## Información general

- **Fuente principal:** Spotify Tracks Dataset — Kaggle
- **Uso del dataset:** académico
- **Unidad de análisis:** canción o pista musical
- **Número inicial de registros:** 114.000
- **Número inicial de variables:** 22

| Variable | Tipo | Rango / valores esperados | Descripción | Uso en el proyecto | Nivel LOPDP |
|---|---|---|---|---|---|
| `Unnamed: 0.1` | Entero | 0 a 113999 | Índice generado en una exportación previa del dataset. | Se eliminará durante limpieza; no es predictor. | No aplica |
| `Unnamed: 0` | Entero | 0 a 113999 | Índice generado en una exportación previa del dataset. | Se eliminará durante limpieza; no es predictor. | No aplica |
| `track_id` | Texto | Identificador alfanumérico único de Spotify | Código que identifica una canción dentro de Spotify. | Identificación técnica y agrupación de duplicados; no predictor directo. | No aplica |
| `artists` | Texto | Nombre de uno o más artistas | Artista o artistas asociados a la canción. | No se usará directamente por alta cardinalidad; se analizará para posibles features futuras sin fuga de datos. | No aplica |
| `album_name` | Texto | Nombre de álbum | Álbum al que pertenece la canción. | No predictor directo por alta cardinalidad. | No aplica |
| `track_name` | Texto | Nombre de canción | Título comercial de la pista. | Trazabilidad y revisión manual; no predictor directo. | No aplica |
| `popularity` | Entero | 0 a 100 | Indicador de popularidad de Spotify. | Variable original para construir la variable objetivo. | No aplica |
| `duration_ms` | Entero | Milisegundos; valores positivos | Duración de la pista musical. | Predictor numérico y base para crear `is_long_track`. | No aplica |
| `explicit` | Booleano | `True` / `False` | Indica si la canción contiene contenido explícito. | Predictor binario potencial. | No aplica |
| `danceability` | Decimal | 0 a 1 | Medida de qué tan adecuada es una canción para bailar según ritmo, estabilidad y beat. | Predictor. | No aplica |
| `energy` | Decimal | 0 a 1 | Intensidad y actividad percibida de la canción. | Predictor y base para crear `energy_tempo`. | No aplica |
| `key` | Entero | 0 a 11 | Tonalidad musical estimada de la canción. | Predictor categórico/musical. | No aplica |
| `loudness` | Decimal | Decibeles, aproximadamente de -60 a 5 | Intensidad sonora promedio de una canción. | Predictor. | No aplica |
| `mode` | Entero | 0 o 1 | Modalidad musical: menor o mayor. | Predictor. | No aplica |
| `speechiness` | Decimal | 0 a 1 | Presencia estimada de palabras habladas en una canción. | Predictor. | No aplica |
| `acousticness` | Decimal | 0 a 1 | Nivel de confianza de que una canción sea acústica. | Predictor. | No aplica |
| `instrumentalness` | Decimal | 0 a 1 | Probabilidad de que una canción no contenga voz. | Predictor. | No aplica |
| `liveness` | Decimal | 0 a 1 | Probabilidad de que una canción haya sido grabada en vivo. | Predictor. | No aplica |
| `valence` | Decimal | 0 a 1 | Positividad o tono emocional percibido de la canción. | Predictor. | No aplica |
| `tempo` | Decimal | BPM; valores positivos o 0 cuando falta medición | Velocidad estimada de la canción en beats por minuto. | Predictor; los valores 0 se tratarán como ausencia de medición rítmica. | No aplica |
| `time_signature` | Entero | Usualmente 3, 4 o 5; 0 cuando falta medición | Compás estimado de la canción. | Predictor; los valores 0 se tratarán como ausencia de medición rítmica. | No aplica |
| `track_genre` | Texto | 114 categorías musicales | Género musical asociado a la pista. Una canción puede aparecer en varios géneros. | Feature musical y base para análisis de fairness. | No aplica |
| `popular` | Entero | 0 o 1 | Variable objetivo creada a partir de `popularity`. `1` si `popularity >= 50`; caso contrario `0`. | Target de clasificación. | No aplica |
| `rhythm_missing` | Entero | 0 o 1 | Indicará si `tempo` o `time_signature` no tienen medición válida. | Feature derivada futura. | No aplica |
| `energy_tempo` | Decimal | Producto de energía y tempo | Aproximación al dinamismo musical de una canción. | Feature derivada futura. | No aplica |
| `is_long_track` | Entero | 0 o 1 | Indicará si una pista dura 10 minutos o más. | Feature derivada futura. | No aplica |

## Consideraciones de privacidad y LOPDP

No se identificaron datos personales de oyentes ni información individual sensible. El dataset contiene atributos de canciones, artistas, álbumes y géneros musicales.

Por tanto, no se procesa PII ni datos sensibles para este proyecto. Las variables de artista y canción se utilizarán únicamente para trazabilidad, análisis de calidad y agrupación técnica de registros.