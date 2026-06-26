# Plantilla 4 — AI Impact Scorecard + AI Risk Matrix
## Framework PROMPT | Fases P2 + T — Performance y Transparencia
### AD5018 Inteligencia Artificial para Negocios | UTEC

---

**Equipo:**
- Tiago Jordan Mar
- Mathias Pariona
- Adriano Raffo

**Fecha de entrega:** PC2 — Semana 12, 2026
**Nombre del MVP:** EasyMeet
**Versión del canvas:** PC2

---

# PARTE A — AI IMPACT SCORECARD
## Fase P2 — Performance y Métricas

---

## SECCIÓN 1 — Evaluación de OKRs declarados en el AI Product Canvas

### Objetivo (O) del proyecto
> *Copia exactamente el Objetivo declarado en la Plantilla 3, Sección 8.*

```
O: Que cualquier persona pueda compartir su disponibilidad en español informal — tal como 
lo haría en WhatsApp — y obtener el mejor horario común con su grupo en menos de 5 minutos.
```

---

### Evaluación de Key Results

**KR1:**

| Campo | Declarado en Plantilla 3 | Resultado real obtenido |
|---|---|---|
| Métrica | Tiempo por persona para coordinar reunión con 3–5 personas | — |
| Valor actual (antes del MVP) | ~35–40 min / persona | — *(no cambia)* |
| Meta comprometida | < 5 minutos | — *(no cambia)* |
| Resultado real | — | No cronometrado formalmente |
| Método usado para medir | Cronometrar con 3 grupos de 3–5 personas externas al equipo | Prueba real sin cronómetro (asíncrona) |
| **¿Se alcanzó la meta?** | — | **NO MEDIDO** |

**Análisis:**
```
El tiempo no fue cronometrado formalmente durante la prueba con el grupo de Casacor.
Los participantes ingresaron su disponibilidad de forma asíncrona (cada uno en el 
momento que pudo), lo que refleja el caso de uso real pero impide medir el tiempo 
individual de completación.

Observación cualitativa: ningún participante reportó dificultad ni demora en el flujo.
La percepción general fue que fue rápido y sin fricción.

KR1 queda como no medido cuantitativamente en esta iteración del MVP.
```

---

**KR2:**

| Campo | Declarado en Plantilla 3 | Resultado real obtenido |
|---|---|---|
| Métrica | % de inputs donde los horarios detectados por Gemini coinciden con la disponibilidad real esperada, sin corrección del usuario | — *(no cambia)* |
| Valor actual (antes del MVP) | 0% | — *(no cambia)* |
| Meta comprometida | ≥ 85% | — *(no cambia)* |
| Resultado real — texto | — | **91%** (20 de 22 inputs correctos) |
| Resultado real — imagen | — | **78%** (14 de 18 imágenes correctas) |
| Criterio "correcto" | — | Todos los días presentes, slots cubriendo ≥90% del tiempo esperado, sin días inventados |
| Método usado para medir | Evaluación interna: 22 inputs de texto y 18 de imagen con disponibilidad conocida → comparar horario generado vs. horario esperado campo por campo | Ejecutado |
| **¿Se alcanzó la meta?** | — | **PARCIAL — texto SÍ (91%), imagen NO (78%)** |

**Análisis del KR2:**
```
Texto (91%): supera la meta. El cambio que más impactó fue la detección de modo 
ESPECÍFICO vs GENERAL — antes de esa mejora el LLM añadía días no mencionados por 
el usuario. El paso de auto-verificación (paso 5 del chain-of-thought) reforzó 
este control obligando al modelo a justificar cada slot antes de outputearlo.

Imagen (78%): por debajo de la meta. Los 4 casos incorrectos fueron fotos con texto 
pequeño o tomadas en ángulo. El prompt con chain-of-thought mejoró la precisión pero 
no es suficiente para imágenes de baja calidad. Se añadió instrucción en UI para 
pedir fotos frontales bien iluminadas.

Conclusión: el texto libre — el caso de uso principal — supera la meta.
```

---

**KR3 *(si fue declarado)*:**

| Campo | Declarado en Plantilla 3 | Resultado real obtenido |
|---|---|---|
| Métrica | % de participantes que inician el flujo y confirman su disponibilidad | — *(no cambia)* |
| Valor actual (antes del MVP) | N/A | — |
| Meta comprometida | ≥ 70% | — *(no cambia)* |
| Resultado real | — | **100%** (6 de 6 participantes) |
| Método usado para medir | Participantes creados en Supabase vs participantes con disponibilidad confirmada | Ejecutado — grupo Casacor |
| **¿Se alcanzó la meta?** | — | **SÍ ✅** (100% > 70%) |

---

### Evaluación del KPI técnico

| Campo | Declarado en Plantilla 3 | Resultado real obtenido |
|---|---|---|
| Métrica técnica | % de usuarios que consideran EasyMeet más fácil que coordinar por WhatsApp | — *(no cambia)* |
| Criterio mínimo aceptable | ≥ 80% | — *(no cambia)* |
| Resultado real | — | **100%** — 6/6 usuarios respondieron SÍ |
| Método de medición | Encuesta de 3 preguntas post-prueba con usuarios reales | Ejecutado — grupo Casacor (6 usuarios) |
| **¿Es aceptable?** | — | **SÍ ✅** (100% > 80%) |

---

### Resumen ejecutivo del OKR

| | KR1 | KR2 | KR3 | KPI técnico |
|---|---|---|---|---|
| **¿Alcanzado?** | NO MEDIDO | PARCIAL | SÍ ✅ (100%) | SÍ ✅ (100%) |

**Conclusión del equipo:**
```
KR1 (tiempo): no fue cronometrado formalmente — la prueba fue asíncrona. 
Observación cualitativa: ningún usuario reportó demora ni dificultad en el flujo.

KR2 (precisión LLM): parcialmente alcanzado — texto libre (91%) supera la meta 
(≥85%); imagen (78%) está por debajo. El caso de uso principal supera la meta.

KR3 (completación): 100% — los 6 participantes del grupo Casacor completaron el 
flujo y confirmaron su disponibilidad. Supera ampliamente la meta de ≥70%.

KPI técnico (percepción): 100% — los 6 usuarios prefirieron EasyMeet sobre 
coordinar por WhatsApp. Supera la meta de ≥80%.
```

---

## SECCIÓN 2 — Evaluación técnica del modelo

### Para IA Generativa

| Métrica | Criterio mínimo aceptable | Resultado real | ¿Aceptable? |
|---|---|---|---|
| **Precisión** — % de inputs donde los horarios detectados coinciden con la disponibilidad esperada (criterio: todos los días presentes, slots ≥90% del tiempo esperado, sin días inventados) | > 85% | Texto: 91% / Imagen: 78% | Texto: SÍ / Imagen: NO (parcial) |
| **Coherencia** — % de outputs con estructura válida | > 95% | ~99% — `responseMimeType: 'application/json'` + validación de input elimina errores de formato | SÍ |
| **Tasa de alucinación** — % de inputs donde el LLM añade días/horas no mencionados | < 5% | Reducida con modo ESPECÍFICO y auto-verificación en el prompt | SÍ (post-mejora) |
| **Tasa de rechazo** — % de inputs donde el LLM no pudo extraer nada | < 15% | ~2% — solo en imágenes completamente ilegibles | SÍ |

**Método de evaluación usado:**
```
Evaluación interna del equipo con 40 inputs de prueba (22 de texto, 18 de imagen) 
diseñados con variación controlada:
  • Texto: desde muy específico ("miércoles de 11 a 2") hasta muy vago ("puedo en la tarde")
  • Imagen: desde foto nítida de horario hasta foto en ángulo con texto pequeño

Para cada input: se registra el JSON generado por Gemini y el JSON esperado, 
y se evalúa campo por campo.
Criterio "correcto": todos los días presentes, slots con ≥90% de coincidencia 
temporal, sin días inventados.

Número de interacciones evaluadas: 40 (22 texto + 18 imagen)
Período de evaluación: pruebas internas previas a PC2
```

---

## SECCIÓN 3 — Evaluación con usuarios reales

### Registro de pruebas de usuario

**Contexto:** Grupo de 6 amigos coordinando una salida a Casacor (Lima). La organizadora creó la sala y compartió el link. Cada participante ingresó su disponibilidad de forma asíncrona en el formato que prefirió.

| # | Perfil del usuario | Tarea asignada | ¿Completó la tarea? | Observaciones clave |
|---|---|---|---|---|
| 1 | Valeria Paliza — organizadora, joven adulta, Lima | Crear sala, compartir link e ingresar disponibilidad propia (texto libre) | SÍ ✅ | Usó el botón "Agregar mi disponibilidad →" sin confusión. Flujo intuitivo. |
| 2 | Hayro Bonifaz — participante, joven adulto, Lima | Ingresar disponibilidad vía foto de horario | SÍ ✅ | La IA extrajo correctamente los bloques de tiempo de la imagen. Sin correcciones. |
| 3 | Valeria Perez — participante, joven adulta, Lima | Ingresar disponibilidad en texto libre | SÍ ✅ | Escribió en lenguaje informal. El sistema interpretó correctamente. |
| 4 | Daniella Del Carpio — participante, joven adulta, Lima | Ingresar disponibilidad vía audio de voz | SÍ ✅ | Grabó su disponibilidad hablando. Confirmó que el resultado fue correcto. |
| 5 | Luciana Vargas — participante, joven adulta, Lima | Ingresar disponibilidad en texto libre | SÍ ✅ | Sin incidencias. Completó el flujo en pocos minutos. |
| 6 | Helena De Osma — participante, joven adulta, Lima | Ingresar disponibilidad vía foto de horario | SÍ ✅ | Subió foto de su horario. Resultado correcto según confirmó. |

**Encuesta post-prueba (3 preguntas):**

| # | Usuario | ¿Más fácil que WhatsApp? | ¿Interpretación correcta? | ¿Lo usarías? |
|---|---|---|---|---|
| 1 | Valeria Paliza | SÍ | SÍ | SÍ |
| 2 | Hayro Bonifaz | SÍ | SÍ | SÍ |
| 3 | Valeria Perez | SÍ | SÍ | SÍ |
| 4 | Daniella Del Carpio | SÍ | SÍ | SÍ |
| 5 | Luciana Vargas | SÍ | SÍ | SÍ |
| 6 | Helena De Osma | SÍ | SÍ | SÍ |

**Resultados agregados:** 6/6 SÍ en las 3 preguntas (100%)

### Hallazgos principales de las pruebas

**Lo que funcionó bien:**
```
1. El flujo completo fue intuitivo para todos los participantes — ninguno necesitó 
   instrucciones adicionales.
2. Los 3 formatos probados (texto libre, foto de horario y audio de voz) funcionaron 
   correctamente y fueron bien recibidos.
3. La pantalla de confirmación generó confianza: los usuarios podían ver qué había 
   interpretado la IA antes de aprobar, y en todos los casos el resultado fue correcto.
```

**Lo que no funcionó o confundió al usuario:**
```
1. Google Calendar no estaba disponible para los participantes — la app está en modo 
   de prueba en Google Cloud y solo acepta correos pre-aprobados. Los participantes no 
   estaban en esa lista. Impacto: ningún participante pudo probar el flujo de Calendar.
   No afectó la coordinación: todos usaron texto, foto o audio sin problema.
2. El organizador no encontraba cómo agregar su propia disponibilidad (hallazgo 
   pre-pruebas, corregido antes de la prueba con el grupo Casacor).
```

**Cambios realizados al MVP como resultado de las pruebas:**
```
1. Botón "Agregar mi disponibilidad →" en el dashboard del organizador (fix hallazgo Rubén).
2. Pendiente: solicitar verificación de app en Google Cloud para que Google Calendar 
   esté disponible para cualquier usuario, no solo los pre-aprobados.
```

---

## SECCIÓN 4 — Reflexión de resultados

### ¿El MVP resuelve el problema definido?

- [ ] SÍ completamente
- [x] SÍ parcialmente
- [ ] NO todavía

**Argumento del equipo:**
```
El MVP resuelve el caso de uso principal: texto libre en español informal → disponibilidad 
extraída correctamente (91%) → coordinación completada. Los 6 usuarios del grupo Casacor 
coordinaron una salida real usando EasyMeet, sin intervención del equipo.

Lo que queda incompleto: Google Calendar no está disponible para usuarios generales 
(la app está en modo de prueba en Google Cloud). La extracción por imagen está por debajo 
de la meta (78%). El aviso de privacidad en la UI aún no está implementado.

Conclusión: el problema central (leer disponibilidad en lenguaje informal) está resuelto. 
Las limitaciones restantes no bloquean el caso de uso principal.
```

### Lecciones aprendidas por fase PROMPT

| Fase | Qué cambiaríamos si empezáramos de nuevo |
|---|---|
| **P — Problema** | Definir desde el inicio que el problema es lingüístico (nadie habla en el lenguaje que exigen las herramientas) y no de coordinación en abstracto. "Coordinar horarios" ya lo resuelve Calendar — el problema real es que nadie tiene Calendar actualizado ni habla en ese formato. |
| **R — Datos** | No planificar un stack que no íbamos a usar. Documentar el stack real desde el inicio evita trabajo doble de documentación. Para un MVP de GenAI, el único dato necesario es el input del usuario — no hay dataset previo. |
| **O — Diseño** | La confirmación del usuario (Human-in-the-Loop) es la decisión de diseño más importante y debería haber sido el primer elemento en el canvas. Sin ella, cualquier alucinación del LLM afecta el resultado grupal. |
| **M — Construcción** | Evaluar primero el modelo antes de asumir que GPT es la opción. Gemini 2.5-flash resultó mejor para este caso: más barato, multimodal nativo, JSON mode nativo. El cambio de stack fue la decisión técnica más importante del proyecto. |
| **P2 — Métricas** | Definir la metodología del KPI técnico desde el inicio con inputs de prueba diseñados antes de construir. Fue más fácil hacerlo bien cuando ya teníamos el MVP funcionando, pero hubiera servido como guía de desarrollo. |
| **T — Ética** | La validación humana obligatoria no es solo un mecanismo anti-alucinación — es una decisión ética. Debió estar en el diseño desde el principio, no como control añadido después. |

### Próximos pasos

```
Corto plazo:
• Completar aviso de privacidad en la UI antes del procesamiento de datos
• Mejorar instrucciones en UI para fotos (reducir imágenes de baja calidad)
• Notificación al organizador cuando todos los participantes hayan respondido

Mediano plazo:
• Sugerencia de lugar según el grupo y el horario confirmado (restaurante, cine, etc.)
• La IA coordina no solo cuándo sino también qué y dónde

Largo plazo:
• Extender a eventos más allá de reuniones: salidas, conciertos, viajes
• Memoria de disponibilidad habitual por usuario (con consentimiento)
• Integración directa con WhatsApp para que el flujo ocurra dentro del chat
```

---

# PARTE B — AI RISK MATRIX
## Fase T — Transparencia y Ética

---

## SECCIÓN 5 — Identificación de riesgos

### Riesgo 1

| Campo | Detalle |
|---|---|
| **Tipo** | Técnico |
| **Nombre del riesgo** | Alucinación de horarios |
| **Descripción** | Gemini añade días u horas que el usuario no mencionó. Ej: el usuario dice "miércoles de 11 a 2" y el modelo añade "también jueves". Podría hacer que el grupo agende en un horario donde alguien no puede. |
| **Nivel** | Alto |
| **Probabilidad** | Media — sin mitigaciones el riesgo es alto; controlado con prompt y confirmación humana |
| **Impacto si ocurre** | El grupo agenda en un horario incorrecto → frustración y pérdida de confianza en el producto |
| **Mitigación** | (1) Modo ESPECÍFICO: el prompt ordena al modelo incluir SOLO los días que el usuario nombró explícitamente. (2) Auto-verificación (paso 5 del CoT): el modelo debe justificar cada slot con una cita directa del mensaje antes de outputearlo — si no puede, lo elimina. (3) Chain-of-thought: el campo `reasoning` obliga al modelo a razonar explícitamente antes de generar el JSON — mejora consistencia y detecta inputs vagos. (4) Confirmación obligatoria: el participante revisa y aprueba el output antes de que se use — control más efectivo. |
| **¿Está mitigado en el MVP actual?** | SÍ — las 4 mitigaciones implementadas. Texto libre: 91% de precisión, dentro del criterio de aceptación (>85%). |

---

### Riesgo 2

| Campo | Detalle |
|---|---|
| **Tipo** | Privacidad / Legal |
| **Nombre del riesgo** | Acceso a datos del calendario más allá de lo necesario |
| **Descripción** | Al conectar Google Calendar, el scope de lectura podría dar acceso a títulos, descripciones y detalles de eventos privados (citas médicas, reuniones confidenciales) más allá de lo necesario para saber cuándo el usuario está disponible. |
| **Nivel** | Alto |
| **Probabilidad** | Baja — si el scope está bien implementado |
| **Impacto si ocurre** | Violación de privacidad. Incumplimiento de Ley N° 29733 (art. 8, 13, 14) y políticas de Google. |
| **Mitigación** | (1) El MVP usa exclusivamente el endpoint FreeBusy — devuelve SOLO bloques libre/ocupado, nunca títulos ni detalles. (2) Scope OAuth: `calendar.readonly` — el mínimo necesario. (3) Los datos del calendario no se persisten en Supabase — solo el JSON de disponibilidad calculado. |
| **¿Está mitigado en el MVP actual?** | SÍ en implementación técnica. PENDIENTE: aviso explícito en UI antes del flujo OAuth. |

---

### Riesgo 3

| Campo | Detalle |
|---|---|
| **Tipo** | Ético / Legal |
| **Nombre del riesgo** | Almacenamiento de audio sin consentimiento del usuario |
| **Descripción** | Si el archivo de audio se guarda en algún componente del stack (base de datos, logs de Vercel, Supabase) sin conocimiento del usuario, se incumple lo declarado y potencialmente la Ley N° 29733, que considera el audio dato personal. |
| **Nivel** | Alto |
| **Probabilidad** | Media — si no se diseña explícitamente el flujo de descarte |
| **Impacto si ocurre** | Violación legal (Ley N° 29733, art. 6 y 7). Los usuarios podrían sentir que son grabados. Daño reputacional. |
| **Mitigación** | (1) El audio llega como FormData, se convierte a base64 y se envía a Gemini — nunca se escribe en disco ni en Supabase. (2) Solo el JSON de disponibilidad resultante se persiste. (3) Aviso en UI pendiente: "Tu audio se procesa en tiempo real y no se almacena." |
| **¿Está mitigado en el MVP actual?** | SÍ en implementación técnica. PENDIENTE: aviso visible al usuario antes de grabar. |

---

### Riesgo 4 *(opcional — recomendado)*

| Campo | Detalle |
|---|---|
| **Tipo** | Ético |
| **Nombre del riesgo** | Exclusión por brecha digital |
| **Descripción** | EasyMeet asume acceso a internet y un navegador moderno. Usuarios sin acceso a tecnología podrían no poder participar, bloqueando la coordinación del grupo entero. |
| **Nivel** | Medio |
| **Probabilidad** | Baja — el segmento objetivo son jóvenes de 18–30 con acceso a tecnología |
| **Impacto si ocurre** | Un participante no puede ingresar su disponibilidad → el grupo no puede coordinar con EasyMeet |
| **Mitigación** | (1) El texto libre está disponible sin dependencias adicionales más allá de un navegador básico. (2) No se exige cuenta de Google ni registro de usuario. (3) Los 4 formatos de input son opcionales — ninguno es obligatorio. |
| **¿Está mitigado en el MVP actual?** | SÍ — el texto libre cubre el caso de uso mínimo sin dependencias adicionales. |

---

## SECCIÓN 6 — Marco regulatorio

### Regulación aplicable al proyecto

| Regulación | ¿Aplica? | ¿Cómo cumple el MVP con ella? |
|---|---|---|
| **Ley N° 29733** — Protección de Datos Personales (Perú) | SÍ | Datos no persistidos tras el cierre de sala. Uso exclusivo para el propósito declarado. Sin cesión a terceros. Aviso de consentimiento pendiente en UI. |
| **D.S. 003-2013-JUS** — Reglamento Ley 29733 | SÍ | Sin almacenamiento de datos personales más allá de la sesión activa. Audio no se persiste. Participantes por alias, no por identidad real. |
| **Art. 8 Ley 29733 — Datos sensibles** | SÍ — audio es dato personal sensible | Audio procesado en tiempo real, no almacenado. Solo el texto extraído se guarda durante la sesión. |
| **Políticas OAuth de Google** | SÍ | Scope mínimo (`calendar.readonly`). FreeBusy API no expone contenido de eventos. Consentimiento vía pantalla OAuth de Google. |
| **EU AI Act** (referencial) | No aplica directamente | EasyMeet operaría en Perú. Como referencia: el producto sería de bajo riesgo — no toma decisiones autónomas que afecten derechos. |

**¿El proyecto procesa datos personales?**
- [x] Sí — con consentimiento explícito del usuario (aviso pendiente de implementar en UI)

---

## SECCIÓN 7 — Preguntas éticas clave

**¿El usuario sabe que está interactuando con IA?**
```
SÍ — ¿Cómo se comunica esto al usuario?

La pantalla de confirmación muestra: "Esto es lo que nuestra IA entendió de tu 
disponibilidad." El usuario ve el resultado antes de aprobarlo — la presencia de 
la IA es explícita y central en el flujo.
```

**¿Qué pasa si la IA comete un error que afecta al usuario?**
```
¿Quién es responsable? ¿Qué mecanismo tiene el usuario para reportarlo?

El error queda atrapado en la confirmación obligatoria (pasos 9–10 del flujo). El 
participante ve lo que Gemini extrajo y puede corregirlo antes de que se use en el 
cálculo grupal. Sin confirmación del usuario, ninguna disponibilidad entra al sistema. 
La responsabilidad de verificar es del usuario — el sistema se lo solicita explícitamente.
```

**¿El producto funciona igual de bien para todos los segmentos de usuarios?**
```
¿Hay algún grupo que podría ser perjudicado o excluido?

No de forma idéntica. El texto libre (91%) funciona mejor que la imagen (78%). Usuarios 
que escriben de forma específica obtienen resultados más precisos que los que escriben 
de forma vaga. Usuarios sin internet o sin navegador moderno no pueden usar el producto. 
El campo `reasoning` del modelo permite detectar inputs vagos y la UI incluye instrucciones 
para mejorar la calidad de las fotos subidas.
```

**¿El usuario tiene control sobre sus datos y puede solicitar su eliminación?**
```
SÍ. No hay cuenta de usuario ni historial entre sesiones. Los datos existen solo 
mientras la sala está activa. El audio nunca se almacena. El participante se identifica 
con un alias. El organizador puede cerrar la sala en cualquier momento, eliminando 
todos los datos asociados.
```

---

## SECCIÓN 8 — Declaración de uso de IA en el proyecto

| Herramienta de IA usada | Para qué tarea del proyecto | Fase PROMPT en la que se usó |
|---|---|---|
| Claude (Anthropic) | Diseño y ajuste del sistema de prompts, revisión de plantillas, lógica del algoritmo de overlap | P, R, O, M |
| ChatGPT (OpenAI) | Pruebas comparativas del prompt con inputs de texto e imagen | O |
| **Gemini 2.5-flash API (Google)** | **Motor de extracción de disponibilidad en el MVP — texto, imagen y audio** | **M** |

---

## SECCIÓN 9 — Autoevaluación final del equipo

| Pregunta de control | Respuesta |
|---|---|
| ¿Los KRs evaluados son exactamente los declarados en la Plantilla 3? | SÍ |
| ¿Los resultados reales tienen evidencia concreta que los respalda? | SÍ — KR2: 22 inputs de texto, 18 de imagen con metodología documentada |
| ¿El equipo no cambió ningún KR después de la Semana 6? | SÍ |
| ¿Hay al menos 1 riesgo técnico, 1 ético y 1 legal identificados? | SÍ — 4 riesgos: 1 técnico, 2 ético/legal, 1 ético |
| ¿Cada riesgo tiene una mitigación concreta y no genérica? | SÍ — cada mitigación describe la implementación técnica real |
| ¿El equipo conoce la regulación aplicable a su sector? | SÍ — Ley N° 29733, D.S. 003-2013-JUS, art. 8 |
| ¿El MVP informa visiblemente al usuario que interactúa con IA? | SÍ — pantalla de confirmación F6 |
| ¿Todos los integrantes pueden responder las preguntas éticas de la Sección 7? | SÍ |

> **Si alguna respuesta es NO → la plantilla no está lista para la sustentación.**

---

*Framework PROMPT v1.1 — AD5018 UTEC | Plantilla 4 de 4 | EasyMeet*
