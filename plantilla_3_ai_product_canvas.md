# Plantilla 3 — AI Product Canvas
## Framework PROMPT | Fase O — Oportunidad de IA
### AD5018 Inteligencia Artificial para Negocios | UTEC

---

**Equipo:**
- Integrante 1: Tiago Jordan Mar
- Integrante 2: Adriano Enrique Raffo Mariaca
- Integrante 3: Mathias Pariona Mego

**Fecha de entrega:** Semana 6 — 2025
**Versión del canvas:** v1

---

## SECCIÓN 1 — Identidad del producto

### 1.1 Nombre del producto / MVP
```
EasyMeet
```

### 1.2 Problema que resuelve
> *Copia exactamente la declaración del Problem Statement Canvas.*

```
"Jóvenes adultos de 18 a 30 años tienen dificultad para coordinar reuniones con sus grupos de amigos
porque no existe una plataforma que unifique disponibilidades expresadas en distintos formatos
(Google Calendar, Outlook, fotos de horario, texto libre y audio), lo que genera demoras de entre 1
y 3 días para encontrar un horario común y provoca frustración, pérdida de interés y abandono frecuente
de planes durante el proceso de coordinación."
```

### 1.3 Usuario principal
```
Jóvenes adultos de 18 a 30 años que organizan reuniones sociales con grupos de amigos
de 3 a 6 personas, donde cada integrante gestiona su tiempo de manera diferente.
Dentro del grupo, existe un "organizador" (quien crea la sala) y "participantes"
(quienes ingresan su disponibilidad).
```

### 1.4 Tipo de IA
- [x] IA Generativa

---

## SECCIÓN 2 — Tech & Cost Overview

### 2.1 Categorías de IA que podrían aplicar al problema

| Categoría | ¿Podría aplicar? | Razonamiento en 1 línea |
|---|---|---|
| **Modelos de lenguaje (LLM)** | SÍ | Núcleo del producto: parsea texto libre e identifica bloques de disponibilidad |
| **Visión computacional** | SÍ | Extrae horarios de fotos de agenda usando GPT-4o Vision o Claude con visión |
| **ML supervisado tabular** | NO | No hay dataset histórico de disponibilidades; cada usuario genera su propia información |
| **ML no supervisado** | NO | No se busca segmentar ni agrupar — se busca encontrar intersección de horarios |
| **Automatización de flujos con IA** | SÍ | n8n orquesta el flujo: recibe input → envía al LLM → almacena → compara → presenta |
| **Clasificación de audio / voz** | TAL VEZ | Whisper API puede transcribir audio a texto para que el LLM lo procese (v2 del producto) |

---

### 2.2 Estimación de costo rough del MVP

| Componente | Categoría de herramienta | Nivel de costo estimado | Comentario |
|---|---|---|---|
| Motor de IA principal | GPT-4o API (OpenAI) o Claude API (Anthropic) | 🟡 | GPT-4o: ~$0.005 por llamada de ~500 tokens. 100 sesiones de prueba ≈ $0.50 |
| Interfaz / frontend | Bubble.io | 🟢 | Free tier disponible para desarrollo y prototipado del MVP |
| Almacenamiento de datos | Google Sheets | 🟢 | Gratuito; almacena disponibilidades por sala de forma temporal |
| Orquestación / automatización | n8n (cloud) | 🟢 | Free tier: hasta 5 workflows activos y 2,500 ejecuciones/mes — suficiente para MVP |
| Transcripción de audio (v2) | Whisper API (OpenAI) | 🟢 | $0.006/minuto; 50 audios de 2 min en pruebas = S/. 2.25 aprox. |

**Costo total estimado del MVP (rango aproximado):**
```
Mínimo: S/. 0 / mes (con free tiers)
Máximo: S/. 50 / mes (si se supera el free tier de n8n o se hacen muchas llamadas API)

Supuestos clave:
- El MVP se probará con máximo 30-50 sesiones reales de usuario durante las semanas 9-12
- El volumen de tokens por sesión es bajo (~500-1000 tokens por extracción de horario)
- Se usará el free tier de Bubble para la interfaz de prototipo
```

---

### 2.3 Complejidad de implementación percibida

| Dimensión | Nivel | Comentario |
|---|---|---|
| Curva de aprendizaje de las herramientas | Media | n8n tiene curva inicial, pero tiene tutoriales extensos. Bubble es intuitivo. |
| Disponibilidad de tutoriales y documentación | Alta | n8n, Bubble y las APIs de OpenAI/Anthropic tienen documentación completa en español e inglés |
| Dependencia de conocimiento técnico externo | Baja | El stack elegido (no-code + API) no requiere conocimiento de programación |
| Viabilidad de construir el MVP en 7 semanas | Alta | El flujo principal (texto + imagen → horario común) es construible en 2-3 semanas con n8n |

---

## SECCIÓN 3 — Experiencia del usuario

### 3.1 Input del usuario

- [x] Escribe texto en un chat o formulario
- [x] Sube un archivo (imagen JPG/PNG de horario, archivo .ics)
- [ ] Hace clic en un botón o selecciona una opción
- [ ] Habla o graba un audio *(v2 del producto — no incluido en MVP)*
- [ ] El sistema se activa automáticamente

**Descripción detallada del input:**
```
El organizador crea una sala de coordinación en EasyMeet y recibe un link único para
compartir con el grupo. Cada participante entra al link y elige cómo ingresar su
disponibilidad: escribe en texto libre cuándo está disponible ("puedo el lunes de 6pm
en adelante y el jueves todo el día") o sube una foto de su horario. También puede
subir su archivo .ics exportado desde Google Calendar u Outlook.
```

### 3.2 Output de la IA

- [x] Texto / respuesta en lenguaje natural
- [ ] Número o predicción
- [x] Recomendación con opciones
- [x] Acción ejecutada automáticamente (resultado guardado en sala compartida)

**Descripción detallada del output:**
```
Cuando todos los participantes han ingresado su disponibilidad, EasyMeet presenta los
3 mejores horarios comunes en lenguaje natural, ordenados por conveniencia para el
grupo. Ejemplo: "El mejor momento para reunirse es el jueves de 7:00 a 9:00 pm —
todos están disponibles. Como alternativa: el martes de 6:00 a 8:00 pm (4 de 5 pueden)."
El organizador confirma el horario elegido y puede compartir la decisión con el grupo.
```

---

## SECCIÓN 4 — Flujo del producto

### 4.1 Diagrama de flujo

```
Paso 1: Organizador → Crea sala en EasyMeet → Recibe link único para compartir
Paso 2: → Comparte el link con el grupo por WhatsApp o similar
Paso 3: Cada participante → Entra al link → Elige formato de input
         (a) Escribe su disponibilidad en texto libre, O
         (b) Sube foto de su horario, O
         (c) Sube archivo .ics de Google Calendar / Outlook
Paso 4: → n8n recibe el input y lo envía al LLM (GPT-4o / Claude)
Paso 5: → LLM extrae los bloques de disponibilidad y los convierte a JSON estructurado
         Ejemplo: {"lunes": ["18:00-22:00"], "jueves": ["todo el día"], ...}
Paso 6: → JSON se almacena en Google Sheets asociado a la sala
Paso 7: Cuando todos ingresan → n8n activa el LLM para comparar todos los JSON
Paso 8: → LLM identifica intersecciones y genera las 3 mejores opciones
Paso 9: → Organizador recibe el resultado y confirma el horario → Sala cerrada
Paso 10: → Todos los participantes ven el horario confirmado
```

### 4.2 Humano en el circuito

- [ ] No hay intervención humana
- [ ] El humano revisa el output antes de que llegue al usuario final
- [x] El humano puede aprobar o rechazar la recomendación de la IA
- [x] El humano interviene solo cuando la IA no tiene respuesta

**Justificación:**
```
El organizador siempre confirma el horario propuesto antes de que sea comunicado al
grupo. Esto es importante porque puede haber contexto que la IA no conoce (una persona
que tiene preferencia personal, un evento externo no en el calendario). Adicionalmente,
si el LLM no puede extraer la disponibilidad de un input, le pide al participante que
lo reintente en texto libre.
```

### 4.3 Plan de contingencia

```
- Si la API del LLM no está disponible: el sistema muestra un mensaje de error amigable
  y permite que el usuario guarde su input para reprocesarlo cuando el servicio vuelva.
- Si una imagen no puede ser procesada: el LLM informa al usuario y le ofrece escribir
  su disponibilidad en texto como alternativa.
- Si el archivo .ics contiene eventos privados: solo se extraen bloques de ocupado/libre,
  nunca los títulos o detalles de los eventos.
- Si no hay ningún horario común: el sistema informa "No se encontró un horario donde
  todos estén disponibles" y muestra las opciones de mayor superposición parcial.
```

---

## SECCIÓN 5 — Decisión estratégica Build / Buy / Integrate

- [ ] Buy
- [x] **Integrate** — conectar API de IA a flujo o interfaz propia
- [ ] Build
- [ ] Combinación

**Justificación:**
```
Buy queda descartado porque no existe ninguna herramienta en el mercado que maneje
todos los formatos de entrada del problema (texto libre + imagen + .ics) y los integre
en una experiencia de coordinación grupal.

Build (entrenar un modelo propio) está fuera del alcance del semestre: no existe un
dataset de "disponibilidades en múltiples formatos" para entrenar, y los modelos
fundacionales (GPT-4o, Claude) ya tienen las capacidades necesarias sin necesidad
de entrenamiento adicional.

Integrate es la opción correcta: conectar GPT-4o o Claude a través de n8n permite
aprovechar las capacidades multimodales ya existentes y construir el flujo completo
de la experiencia de usuario sin necesidad de conocimientos de programación avanzados.
El valor diferencial está en el diseño del flujo y la experiencia — no en el modelo.
```

---

## SECCIÓN 6 — Diseño específico (IA Generativa)

### System Prompt del MVP

```
ROL:
Eres EasyMeet, un asistente experto en leer y estructurar disponibilidades horarias.
Tu única función es extraer bloques de tiempo disponibles de la información que te da
el usuario y devolverlos en formato JSON estructurado.

CONTEXTO:
El usuario es una persona que quiere coordinar una reunión con amigos. Te está diciendo
cuándo tiene tiempo libre durante la semana. La información puede llegar como:
- Texto libre en español informal ("puedo el lunes de tarde y el viernes todo el día")
- Descripción de una imagen de horario que se te mostrará
- Texto extraído de un archivo de calendario

Tu tarea es transformar esa información en un JSON con los bloques de disponibilidad
por día de la semana, usando formato de 24 horas.

RESTRICCIONES:
- NUNCA inventes horarios que el usuario no mencionó explícitamente
- Si la información es ambigua o incompleta, pide UNA sola aclaración específica
- No almacenes ni comentes información más allá del horario
- No sugieras reuniones ni tomes decisiones — solo extrae la disponibilidad
- Si no puedes extraer ningún horario, explica brevemente por qué y pide que el
  usuario reescriba su disponibilidad en texto

FORMATO DE RESPUESTA:
Responde SIEMPRE en este formato JSON exacto:
{
  "disponibilidad": {
    "lunes": ["HH:MM-HH:MM", "HH:MM-HH:MM"],
    "martes": [],
    "miercoles": [],
    "jueves": [],
    "viernes": [],
    "sabado": [],
    "domingo": []
  },
  "notas": "observación si aplica, vacío si no hay nada que aclarar",
  "confianza": "alta / media / baja"
}

TONO: Amigable, directo, sin tecnicismos. Si pides una aclaración, sé específico.
IDIOMA: Español siempre, sin importar en qué idioma te escriban.
```

**Plan de gestión de alucinaciones:**
```
¿Qué pasa si la IA inventa un horario?
→ Antes de que los datos se comparen con el grupo, cada participante ve un resumen
  de lo que la IA extrajo de su input y puede corregirlo. El sistema tiene un paso
  explícito de confirmación: "¿Esto refleja tu disponibilidad? [Sí / Editar]"

¿Hay validación humana en decisiones críticas?
→ Sí. El organizador confirma el horario propuesto antes de que sea comunicado al grupo.
  El producto nunca agenda automáticamente sin aprobación humana.

¿El usuario puede reportar respuestas incorrectas?
→ Sí. En la pantalla de confirmación hay un botón "Esto no es correcto" que permite
  al usuario reingresar su disponibilidad en texto libre.
```

---

## SECCIÓN 7 — Alcance del MVP

### Lo que SÍ incluye el MVP
```
1. Crear sala de coordinación con link único compartible
2. Ingreso de disponibilidad por texto libre en español
3. Ingreso de disponibilidad por imagen (foto de horario) procesada por Vision AI
4. Extracción automática de horarios por LLM (GPT-4o o Claude)
5. Paso de confirmación: el participante valida lo que extrajo la IA
6. Comparación de disponibilidades de hasta 6 participantes
7. Presentación de los 3 mejores horarios comunes en lenguaje natural
8. Confirmación final por parte del organizador
```

### Lo que NO incluye el MVP *(pero podría incluir una versión futura)*
```
1. Integración directa con Google Calendar API / Outlook API via OAuth
   (requiere configuración de autenticación compleja — se simplifica en MVP con .ics)
2. Entrada por audio (voz grabada) — requiere Whisper API; se incluye en v2
3. Notificaciones automáticas por WhatsApp o email al confirmar el horario
4. Historial de reuniones coordinadas anteriores
5. Cuenta de usuario o registro — el MVP funciona sin login
```

### Criterio de éxito del MVP
```
"El MVP está listo cuando un usuario externo al equipo puede crear una sala de
coordinación, invitar a dos personas más, cada una ingresa su disponibilidad en texto
o imagen, y el sistema presenta el mejor horario común en menos de 5 minutos — sin
que ningún miembro del equipo de desarrollo asista o intervenga durante el proceso."
```

---

## SECCIÓN 8 — OKRs y KPIs del producto

### Objetivo (O):
```
O: Eliminar la fricción de coordinar reuniones entre amigos con agendas y formatos
   distintos, reduciendo el tiempo y los mensajes necesarios para llegar a un acuerdo.
```

---

### Key Result 1 (KR1):

| Campo | Detalle |
|---|---|
| Métrica | Tiempo total promedio para coordinar una reunión entre 3-5 personas |
| Valor actual | 35 minutos por persona (estimado mediante encuesta a 8 personas del segmento antes de la Semana 6) |
| Meta con el MVP | Menos de 5 minutos desde que el último participante ingresa su disponibilidad |
| Método de medición | Cronometrando el proceso con 3 grupos de prueba externos al equipo en la Semana 12 |
| Período de medición | Semanas 12-13 durante las pruebas de usuario |

---

### Key Result 2 (KR2):

| Campo | Detalle |
|---|---|
| Métrica | Porcentaje de inputs (texto e imagen) de los que el LLM extrae correctamente la disponibilidad sin intervención del usuario |
| Valor actual | 0% (el producto no existe aún) |
| Meta con el MVP | ≥ 85% de inputs procesados correctamente (evaluación manual de 25 casos de prueba) |
| Método de medición | El equipo genera 25 inputs de prueba (texto e imagen), los procesa con el MVP y valida manualmente si el JSON extraído es correcto |
| Período de medición | Semana 11 — antes de las pruebas con usuarios reales |

---

### Key Result 3 (KR3):

| Campo | Detalle |
|---|---|
| Métrica | Porcentaje de usuarios externos que inician el flujo y lo completan sin abandonarlo |
| Valor actual | N/A (sin benchmark — producto nuevo) |
| Meta con el MVP | ≥ 70% de tasa de completación en pruebas de usuario |
| Método de medición | Registro en Google Sheets de sesiones iniciadas vs. sesiones completadas durante pruebas |
| Período de medición | Semanas 12-13 |

---

### KPI técnico del modelo:

| Campo | Detalle |
|---|---|
| Métrica técnica | Tasa de extracción correcta de horarios (precisión del LLM al parsear disponibilidades) |
| Criterio mínimo aceptable | > 85% de correctitud en evaluación manual de 25 inputs de prueba |
| Método de medición | El equipo crea 25 inputs de prueba con disponibilidades conocidas (texto e imagen). Se compara el JSON del LLM con el horario real. Se cuenta como correcto si todos los bloques de tiempo son exactos. |

---

### Verificación de coherencia interna

| Pregunta | Respuesta |
|---|---|
| ¿El Objetivo refleja directamente el problema de la Sección 1.2? | SÍ — el objetivo habla de eliminar la fricción de coordinación, que es exactamente el problema |
| ¿Los KRs son medibles con números concretos? | SÍ — KR1: <5 min, KR2: ≥85%, KR3: ≥70% |
| ¿El KPI técnico está conectado al tipo de IA elegido (GenAI)? | SÍ — mide la precisión de extracción del LLM, que es el componente central |
| ¿El equipo puede obtener el valor actual de KR1 antes de la Semana 6? | SÍ — mediante encuesta a 8-10 personas del segmento antes de la entrega |

---

## SECCIÓN 9 — Autoevaluación del equipo

| Pregunta de control | Respuesta |
|---|---|
| ¿El problema en la Sección 1.2 es copia exacta del Problem Statement Canvas? | SÍ |
| ¿El flujo de la Sección 4 es consistente con el tipo de IA elegido? | SÍ — el flujo usa LLM para procesar texto e imagen, que son capacidades de GenAI |
| ¿El stack tecnológico fue verificado (cuentas creadas, accesos confirmados)? | PENDIENTE — cuentas de n8n y Bubble a crear en Semana 7 al iniciar Phase M |
| ¿El alcance del MVP es realista para construir en 7 semanas? | SÍ — el flujo principal (texto + imagen → horario) es construible en 2-3 semanas con n8n |
| ¿El system prompt fue probado al menos una vez antes de entregar? | SÍ — se probó manualmente en claude.ai y chatgpt.com con inputs de prueba |
| ¿El Objetivo del OKR refleja el problema definido en Fase P? | SÍ |
| ¿Los KRs tienen valores actuales concretos (no estimados)? | KR1: verificado con encuesta. KR2 y KR3: sin baseline posible (producto nuevo) |
| ¿Todos los integrantes entienden cada sección de este canvas? | SÍ |

---

*Framework PROMPT v1.1 — AD5018 UTEC | Plantilla 3 de 4*
