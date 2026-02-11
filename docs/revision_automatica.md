# Revisión cruzada de requisitos (Manual + Automática)

Este documento recoge la revisión automática de los requisitos del sistema (RF-1 a RF-11 y RFN-1 a RFN-2) siguiendo:
1) Reglas de redacción de requisitos estilo INCOSE (claridad, una idea por requisito, sin ambigüedades, sin términos vagos, con condiciones medibles cuando aplique).
2) Objetivos de calidad: SMART, CCC (Correcto, Completo, Consistente), Trazable, Verificable, No ambiguo.

### Prompt (aprox.)
```text
CHATGPT

Tarea:
1) Aplica reglas de redacción de requisitos (estilo INCOSE: frases claras, una idea por requisito, sin ambigüedades, sin términos vagos, con condiciones medibles cuando aplique).
2) Evalúa cada requisito con estos objetivos de calidad:
   - SMART
   - CCC (Correcto, Completo, Consistente)
   - Trazable
   - Verificable
   - No ambiguo

Formato de salida:
Devuelve una tabla con columnas:
id | smart | ccc | trazable | verificable | no_ambiguo | comentario_mejora

Usa OK/KO en cada métrica y en comentario_mejora explica brevemente por qué y cómo mejorar el requisito (sin reescribirlo entero, solo indicando la mejora concreta).

Requisitos a evaluar:
(de RF-1 a RFN-2)

| id    | smart | ccc | trazable | verificable | no_ambiguo | comentario_mejora                                                                                                                                                      ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RF-1  |    KO |  KO |       OK |          KO |         KO | No define el almacén persistente, esquema/tipos ni comportamiento ante errores (duplicados, filas inválidas). Añadir criterios de aceptación y validaciones mínimas.      |
| RF-2  |    OK |  OK |       OK |          OK |         OK | Es claro y testeable (GET vs otros métodos). Especificar respuesta/código de error si método inválido.                                                                    |
| RF-3  |    KO |  KO |       OK |          KO |         KO | No queda claro si date/user/topic son obligatorios siempre, su formato/dominio y dónde van (query/body). Definir formato date y dominio user/topic + manejo de faltantes. |
| RF-4  |    KO |  KO |       OK |          KO |         KO | “Métrica de error correspondiente” es ambiguo. Definir catálogo de errores y estructura de respuesta (código HTTP + body JSON).                                           |
| RF-5  |    KO |  KO |       OK |          KO |         KO | “Valores inválidos” no está definido (formatos/rangos/listas). Añadir reglas de validación concretas para date/user/topic y códigos de error.                             |
| RF-6  |    KO |  KO |       OK |          KO |         KO | “Observaciones” no definido (estructura, granularidad). Especificar qué se genera por entrada, dónde se guarda y campos de la observación.                                |
| RF-7  |    KO |  KO |       OK |          KO |         KO | Falta definir polarity/score/tags (rango, método, formato). Añadir definiciones y criterios de cálculo para que sea medible y verificable.                                |
| RF-8  |    OK |  KO |       OK |          OK |         OK | Límite de 200 caracteres es medible, pero “entradas seleccionadas” no está especificado (filtros exactos). Definir selección y cómo contar caracteres.                    |
| RF-9  |    OK |  KO |       OK |          OK |         KO | Medible (200 palabras), pero “sentimiento global” es ambiguo. Definir método de agregación y regla de conteo de palabras.                                                 |
| RF-10 |    KO |  KO |       OK |          KO |         KO | No define qué representa el eje de barras (por día/topic/bins), ni formato de salida. Especificar agregación y formato (imagen/JSON).                                     |
| RF-11 |    KO |  KO |       OK |          KO |         KO | Recomendación sin algoritmo ni criterio. Definir top-N, métrica/heurística (similitud, co-ocurrencia, tags) y formato de salida.                                          |
| RFN-1 |    OK |  KO |       OK |          OK |         OK | Verificable si hay OpenAPI, pero falta ubicación/versionado y endpoints cubiertos. Indicar ruta del spec y qué operaciones documenta.                                     |
| RFN-2 |    KO |  KO |       OK |          KO |         KO | “HTTPS o autenticación” es impreciso. Definir requisito concreto (HTTPS obligatorio + tipo de auth) y criterios verificables (TLS, token).                                |

GEMINI

Evalúa la calidad de estos requisitos siguiendo:

Tarea:
(1) reglas INCOSE de redacción de requisitos
(2) objetivos: SMART + CCC + trazable + verificable + no ambiguo

Devuelve una tabla con columnas:
ID, SMART, CCC, Trazable, Verificable, No Ambiguo, Comentario de Mejora (Reglas INCOSE)

Requisitos:
(de RF-1 a RFN-2)

ID,SMART,CCC,Trazable,Verificable,No Ambiguo,Comentario de Mejora (Reglas INCOSE)
RF-1,KO,KO,OK,KO,KO,"Ambiguo. No define el destino (""un sistema...""). Debe especificar la base de datos y la frecuencia de lectura."
RF-2,OK,OK,OK,OK,OK,Bien definido. Cumple con la restricción de método.
RF-3,OK,OK,OK,OK,OK,Específico y fácil de probar mediante tests de integración.
RF-4,KO,KO,OK,KO,KO,"Vago. ¿Qué es una ""métrica de error""? Debería especificar un código de estado HTTP (ej. 400 Bad Request)."
RF-5,KO,KO,OK,KO,KO,"Vago. Similar a RF-4. Debe definir qué constituye un ""valor inválido"" y el código de error exacto."
RF-6,KO,KO,OK,KO,KO,"Incompleto. No define qué es una ""observación"" ni el formato del almacén de datos."
RF-7,OK,OK,OK,OK,OK,"Claro, aunque podría mejorar especificando si la información se guarda o solo se muestra."
RF-8,OK,OK,OK,OK,OK,SMART. El límite de 200 caracteres lo hace perfectamente medible y verificable.
RF-9,OK,OK,OK,OK,OK,"Bien definido, aunque la ""calidad"" del lenguaje natural es subjetiva para verificar."
RF-10,OK,OK,OK,OK,OK,Específico sobre el tipo de salida visual.
RF-11,KO,KO,OK,KO,KO,"Ambiguo. ¿En qué se basa el análisis? ""Basadas en el análisis"" es demasiado genérico para un desarrollador."
RFN-1,OK,OK,OK,OK,OK,Muy bueno. El uso de un estándar (OpenAPI) facilita la verificación.
RFN-2,KO,KO,OK,KO,KO,"Ambigüedad lógica. El ""o"" (HTTPS o autenticación) es peligroso. Debería ser ""y"" para garantizar seguridad real."

##  ✅ Bloque de discrepancias 

### Discrepancias principales (ChatGPT vs Gemini)

- **RF-3 (parámetros date, user y topic)**
  - *ChatGPT:* KO en SMART/CCC/Verificable/No ambiguo porque no fija si los parámetros son obligatorios siempre, su formato (p.ej. ISO-8601 para date), su dominio (valores válidos de user/topic) ni el lugar exacto (query/path/body).
  - *Gemini:* OK en todas las métricas, argumentando que es específico y fácil de probar.
  - **Decisión del equipo:** mantenemos **KO en CCC/Verificable/No ambiguo**, ya que sin formato/dominio/ubicación no se puede definir un test completamente determinista.

- **RF-7 (polarity, tags y score)**
  - *ChatGPT:* KO por falta de definición de escalas/rangos, método de cálculo y formato de salida de tags.
  - *Gemini:* OK, indicando solo que podría aclararse si se guarda o se muestra.
  - **Decisión del equipo:** mantenemos **KO en Verificable/No ambiguo** porque sin rango/método de cálculo no hay criterio objetivo de validación.

- **RF-9 (sentimiento global en 200 palabras)**
  - *ChatGPT:* KO en CCC y No ambiguo al no definir qué significa “sentimiento global” (método de agregación) y reglas exactas de conteo.
  - *Gemini:* OK, aunque menciona subjetividad del lenguaje natural.
  - **Decisión del equipo:** mantenemos **OK en SMART** (límite de palabras) pero **KO en No ambiguo/CCC** si no se especifica la agregación del sentimiento.

- **RF-10 (gráfico de barras de polaridad)**
  - *ChatGPT:* KO por no definir ejes, agregación (por día/topic/bins), ni formato de salida (imagen/JSON).
  - *Gemini:* OK por considerar suficiente “gráfico de barras”.
  - **Decisión del equipo:** mantenemos **KO en Verificable/No ambiguo**, ya que faltan decisiones mínimas para implementar y probar la visualización.

- **RFN-1 (OpenAPI)**
  - *ChatGPT:* OK pero marca KO en CCC por no indicar ubicación/versionado y cobertura exacta del spec.
  - *Gemini:* OK en todo.
  - **Decisión del equipo:** mantenemos **KO en CCC** si no se indica dónde está el fichero OpenAPI (ruta en repo o endpoint) y qué endpoints describe.
