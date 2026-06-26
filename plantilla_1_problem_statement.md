# Plantilla 1 — Problem Statement Canvas
## Framework PROMPT | Fase P — Problema de Negocio
### AD5018 Inteligencia Artificial para Negocios | UTEC

---

**Equipo:**
- Tiago Jordan Mar
- Mathias Pariona
- Adriano Raffo

**Fecha de entrega:** PC2 — Semana 14, 2026
**Versión del canvas:** PC2

---

## SECCIÓN 1 — Definición del problema

### 1.1 Usuario afectado

```
Jóvenes de 18 a 30 años que quieren reunirse con grupos de 3 a 6 amigos o compañeros.
Su agenda varía semana a semana (clases, trabajo, gym, compromisos variables) y cada 
uno gestiona su tiempo de forma distinta: algunos tienen Google Calendar activo, otros 
guardan el horario en una foto del celular, y la mayoría lo sabe de memoria. Se 
coordinan principalmente por WhatsApp.
```

---

### 1.2 Problema específico

```
Cuando alguien propone una reunión, la disponibilidad del grupo está fragmentada en 
formatos incompatibles: uno la tiene en Calendar, otro en una foto de su horario de 
clases, otro la sabe de memoria. No hay un punto común donde comparar todo eso.

Para coordinarse, el grupo recurre a WhatsApp. Los mensajes son vagos, sin fecha 
exacta, sin hora, con condiciones implícitas: "puedo el sábado", "el jueves en la 
tarde salvo que me cancelen", "yo casi siempre libre menos los lunes". El resultado 
es una cadena de 15 a 25 mensajes durante varios días donde nadie llega a un acuerdo 
claro, y muchos planes se caen — no por imposibilidad de coincidir, sino porque el 
proceso es tan tedioso que nadie termina de concretarlo.

Las herramientas existentes no resuelven esto:
• Google Calendar y Calendly exigen que todos tengan su agenda actualizada en el mismo 
  ecosistema — condición que casi nunca se cumple en grupos de amigos.
• When2Meet requiere hacer clic en cada bloque horario uno por uno. Es una herramienta 
  de trabajo, no para coordinar una salida.
• Ninguna herramienta entiende "puedo el sábado" tal como se escribe — todas piden 
  que el usuario traduzca primero su disponibilidad a su formato. Esa traducción es la 
  fricción que hace que el proceso fracase.
```

---

### 1.3 Causa raíz

```
Dos causas combinadas:

1. La disponibilidad está descentralizada. Cada persona la gestiona en un formato 
   distinto (Calendar, foto, memoria). No existe un punto común donde comparar sin 
   que alguien tenga que migrar de sistema.

2. El lenguaje de coordinación es informal por naturaleza. Las personas dicen cuándo 
   pueden en español coloquial, ambiguo y contextual. Ninguna herramienta puede leer 
   ese lenguaje directamente — todas exigen que el usuario lo traduzca primero a un 
   formato estructurado. Esa traducción manual es la fricción que hace que el proceso 
   se abandone.
```

---

### 1.4 Consecuencia medible

```
• 15–25 mensajes intercambiados por reunión
• 1 a 3 días para llegar a un acuerdo o desistir
• ~35–40 minutos por persona invertidos en la coordinación
• Muchos encuentros nunca ocurren — no por imposibilidad de coincidir, sino por 
  agotamiento del proceso
```

---

### 1.5 Declaración del problema — formato obligatorio

**"[Tipo de usuario] tiene dificultad para [acción específica] porque [causa raíz], lo que genera [consecuencia medible]."**

```
"Jóvenes de 18 a 30 años tienen dificultad para concretar reuniones con sus grupos 
de amigos porque cada persona gestiona su disponibilidad en un formato distinto 
(calendario, foto, memoria) y la comunica en lenguaje informal que ninguna herramienta 
de coordinación puede interpretar directamente, lo que genera 15–25 mensajes en 
WhatsApp durante 1 a 3 días y frecuentemente hace que la reunión nunca llegue a 
ocurrir — no por falta de ganas, sino por agotamiento del proceso."
```

---

## SECCIÓN 2 — Filtro de validación IA

| Pregunta | SÍ / NO | Justificación (1 línea) |
|---|---|---|
| ¿Una hoja de cálculo o formulario resuelve esto? | NO | Requiere que el usuario ya tenga la disponibilidad estructurada — es exactamente la fricción que queremos eliminar. |
| ¿El problema escala con volumen de datos o usuarios? | SÍ | A más participantes y formatos distintos, mayor el caos y más necesaria la normalización automática. |
| ¿Hay un patrón repetitivo difícil de procesar manualmente? | SÍ | Extraer bloques de tiempo de texto informal sigue un patrón semántico consistente pero con variación léxica imposible de capturar con reglas fijas. |
| ¿El problema requiere generar contenido o razonar en lenguaje natural? | SÍ | La causa raíz es el lenguaje natural informal: el sistema debe entender "puedo el finde salvo domingo" y convertirlo en horarios comparables. |
| ¿Necesitas predecir Y luego explicar o actuar sobre el resultado? | NO | No se predice el futuro; se extrae y compara disponibilidad que ya existe expresada en texto natural. |

**Conclusión del filtro:**

```
El problema tiene dos dimensiones y la IA Generativa es la única tecnología que 
resuelve ambas:

Formatos heterogéneos: el sistema necesita leer disponibilidad desde texto libre, 
imágenes de horarios y calendarios digitales, y normalizarlos en un formato comparable. 
Un LLM multimodal procesa los tres sin entrenamiento previo.

Lenguaje informal: las formas de decir "estoy disponible" son infinitamente variadas 
("puedo", "libre", "no tengo nada", "ese día sí", "el jue creo que sí"). Esto no 
puede resolverse con reglas fijas ni con ML Tradicional — no existe dataset de 
disponibilidades etiquetadas. Solo un LLM comprende referencias temporales relativas, 
condiciones implícitas y ambigüedad lingüística en tiempo real, sin requerir que el 
usuario cambie cómo habla.
```

---

## SECCIÓN 3 — Tipo de IA elegido

- [x] **IA Generativa** — el problema involucra lenguaje natural e interpretación de múltiples formatos no estructurados
- [ ] **ML Tradicional** — el problema requiere predecir, clasificar o segmentar con datos históricos
- [ ] **Combinación** — se necesita predecir Y comunicar/actuar sobre el resultado

### Justificación de la elección

```
El núcleo del problema es leer disponibilidad desde texto informal en español. La IA 
Generativa es la única tecnología que puede hacer esto porque:

1. El input varía infinitamente: "puedo el jue", "jueves ok", "jueves libre todo el 
   día" son tres formas de decir lo mismo. Imposible de capturar con expresiones 
   regulares o clasificadores.

2. Requiere comprensión de contexto temporal: "el próximo sábado", "esta semana no", 
   "mañana en la tarde" son referencias relativas que el LLM resuelve con la fecha 
   actual como contexto.

3. Maneja ambigüedad e incompletitud: "puedo en la tarde" sin especificar hora exacta 
   — el LLM infiere un rango razonable o pide clarificación puntual.

ML Supervisado descartado: sin dataset de entrenamiento.
ML No Supervisado descartado: no hay variables que segmentar.
Combinación descartada: no hay variable que predecir.
```

## SECCIÓN 4 — Autoevaluación del equipo

| Pregunta de control | Respuesta |
|---|---|
| ¿El problema está descrito sin mencionar tecnología? | SÍ |
| ¿La declaración del problema sigue el formato exacto? | SÍ |
| ¿La elección del tipo de IA se justifica con el problema, no con la preferencia? | SÍ — se justifica por la naturaleza informal y variable del lenguaje |
| ¿Todos los integrantes pueden explicar este canvas sin leerlo? | SÍ |

---
