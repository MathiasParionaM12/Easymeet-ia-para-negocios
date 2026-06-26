# Plantilla 2 — Data Readiness Checklist
## Framework PROMPT | Fase R — Recursos de Datos
### AD5018 Inteligencia Artificial para Negocios | UTEC

---

**Equipo:**
- Tiago Jordan Mar
- Mathias Pariona
- Adriano Raffo

**Fecha de entrega:** PC2 — Semana 12, 2026
**Tipo de IA del proyecto:** IA Generativa — Google Gemini 2.5-flash (texto, visión y audio)
**Stack implementado:** Next.js 16.2.9 + TypeScript + Tailwind CSS 4 + shadcn/ui · Supabase PostgreSQL + Realtime · Gemini 2.5-flash API · Google OAuth 2.0 + Calendar FreeBusy API · Vercel

---

> EasyMeet no trabaja con un dataset histórico preexistente. Los datos son generados 
> por cada usuario en tiempo real al usar el producto. El inventario de datos 
> corresponde a los tipos de input que el sistema debe procesar.

---

## SECCIÓN 1 — Inventario de datos

### Para IA Generativa — Inventario de conocimiento

| # | Tipo de información | Dónde está actualmente | Formato | ¿Está disponible? |
|---|---|---|---|---|
| 1 | Disponibilidad en texto libre | El usuario la escribe en el formulario | Texto en español informal | SÍ — input principal del MVP |
| 2 | Foto de horario | Celular o computadora del usuario | JPG / PNG | SÍ — implementado como complemento |
| 3 | Calendario Google | Cuenta Google del usuario (OAuth 2.0) | JSON FreeBusy — bloques ocupado/libre | SÍ — OAuth completo implementado |
| 4 | Audio de voz | Dispositivo del usuario | Audio webm / mp3 / wav | SÍ — transcripción con Gemini 2.5-flash |
| 5 | System prompt e instrucciones | `src/lib/gemini.ts` en el repositorio | TypeScript + prompts | SÍ — en producción |
| 6 | Datos de sala y participantes | Supabase PostgreSQL | JSON estructurado (3 tablas: rooms, participants, availabilities) | SÍ — en producción |

**Estrategia de contexto elegida:**
- [x] Prompt simple *(todo el contexto — rango de fechas de la sala, fecha actual, instrucciones de formato — cabe en el system prompt. No se necesita RAG ni memoria entre sesiones.)*
- [ ] RAG — Retrieval Augmented Generation *(base de conocimiento grande o cambiante)*
- [ ] Memoria de sesión *(asistente conversacional con contexto acumulativo)*

---

### Para ML Tradicional — Inventario de datos históricos

No aplica — el proyecto usa IA Generativa.

---

### Para Combinación — completa ambas secciones anteriores y describe la conexión:

No aplica.

---

## SECCIÓN 2 — Evaluación de calidad con semáforo

> 🟢 Listo | 🟡 Necesita trabajo | 🔴 Bloqueante

### Fuente 1 — Texto libre (input principal)

| Dimensión | Semáforo | Evidencia que respalda la evaluación | Plan de acción (si es 🟡 o 🔴) |
|---|---|---|---|
| **Disponibilidad** | 🟢 | El usuario lo genera en tiempo real. Sin dependencia de terceros. | — |
| **Volumen** | 🟢 | Un input por usuario es suficiente. No se requiere dataset de entrenamiento. | — |
| **Calidad** | 🟡 | Texto específico ("miércoles de 11 a 2") funciona con >90% de precisión. Texto vago ("puedo") baja a ~74%. | Prompt con detección de modo ESPECÍFICO vs GENERAL. LLM pide clarificación si el input es ambiguo. Ejemplos en la UI. |
| **Relevancia** | 🟢 | Es el formato en que el segmento objetivo comunica su disponibilidad — la causa raíz del problema. | — |
| **Legalidad** | 🟡 | Los horarios son datos de comportamiento personal bajo Ley N° 29733. | Aviso de privacidad antes de ingresar datos. Datos eliminados al cerrar la sala. |

**Resultados en pruebas internas:**
- Texto con días y horas específicas: 91% de precisión (20 de 22 inputs correctos)
- Texto general sin días concretos: ~74% — el LLM abre el rango completo de la sala

---

### Fuente 2 — Foto de horario (complementario)

| Dimensión | Semáforo | Evidencia que respalda la evaluación | Plan de acción (si es 🟡 o 🔴) |
|---|---|---|---|
| **Disponibilidad** | 🟢 | El usuario la sube desde su celular. Sin dependencia de terceros. | — |
| **Volumen** | 🟢 | Una imagen por usuario es suficiente. | — |
| **Calidad** | 🟡 | Fotos nítidas: 78% de precisión. Fotos en ángulo o con texto pequeño: ~45%. | Instrucciones en UI ("foto frontal, bien iluminada"). Prompt con razonamiento en dos pasos (listar eventos → calcular slots libres). Fallback a texto si imagen es ilegible. |
| **Relevancia** | 🟢 | Formato habitual en universitarios (horario de clases en foto). | — |
| **Legalidad** | 🟢 | El usuario sube su propio horario. Sin datos de terceros. | — |

---

### Fuente 3 — Google Calendar API (OAuth 2.0)

| Dimensión | Semáforo | Evidencia que respalda la evaluación | Plan de acción (si es 🟡 o 🔴) |
|---|---|---|---|
| **Disponibilidad** | 🟢 | API implementada. Flujo OAuth completo con redirect a `/api/calendar/callback`. Probado en el MVP. | — |
| **Volumen** | 🟢 | Una consulta FreeBusy por rango de fechas por usuario es suficiente. | — |
| **Calidad** | 🟢 | Datos JSON estructurados. Alta confiabilidad. El MVP obtiene bloques libre/ocupado sin títulos de eventos. | — |
| **Relevancia** | 🟢 | Para usuarios con Calendar activo, elimina toda fricción de ingreso. | — |
| **Legalidad** | 🟡 | Requiere scope `calendar.readonly`. El usuario debe saber qué se lee. | Pantalla de consentimiento OAuth explica qué se accede. Solo se leen bloques libre/ocupado — nunca títulos ni detalles. |

---

### Fuente 4 — Audio de voz

| Dimensión | Semáforo | Evidencia que respalda la evaluación | Plan de acción (si es 🟡 o 🔴) |
|---|---|---|---|
| **Disponibilidad** | 🟢 | El usuario graba desde el navegador o sube un archivo. Sin dependencia de terceros. | — |
| **Volumen** | 🟢 | Un audio por usuario es suficiente. | — |
| **Calidad** | 🟡 | Ruido de fondo afecta la transcripción. En entornos silenciosos funciona bien. | Instrucciones en UI ("graba sin ruido de fondo"). Si el resultado es incoherente, el sistema ofrece alternativa de texto. |
| **Relevancia** | 🟢 | El formato más natural — hablar es más rápido que escribir. | — |
| **Legalidad** | 🟡 | Audio es dato personal sensible bajo Ley N° 29733. | El archivo de audio llega como FormData, se procesa con Gemini y nunca se escribe en disco ni en Supabase. Solo el JSON resultante se persiste. Aviso en UI pendiente. |

---

### Fuente 5 — Datos de sala en Supabase

| Dimensión | Semáforo | Evidencia que respalda la evaluación | Plan de acción (si es 🟡 o 🔴) |
|---|---|---|---|
| **Disponibilidad** | 🟢 | PostgreSQL con tablas `rooms`, `participants`, `availabilities`. Realtime habilitado. | — |
| **Calidad** | 🟢 | Datos estructurados. Supabase Realtime actualiza el dashboard del organizador cuando un participante confirma. | — |
| **Legalidad** | 🟡 | Incluye alias de participantes y horarios. | Participantes identificados por alias dentro de la sala — sin vinculación a identidad real. Datos eliminados al cerrar la sala. |

---

## SECCIÓN 3 — Plan de resolución de bloqueantes

### Bloqueante 1
```
No aplica — no hay semáforos 🔴 en ninguna fuente de datos.

Los puntos 🟡 tienen acciones concretas documentadas en la columna "Plan de acción"
de cada tabla de la Sección 2. Ninguno bloquea la construcción del MVP.
```

### Bloqueante 2 *(si aplica)*
```
No aplica.
```

---

## SECCIÓN 4 — Privacidad y legalidad de los datos

| Pregunta | Respuesta | Detalle |
|---|---|---|
| ¿Los datos contienen información personal de usuarios? | SÍ | Horarios, audios y disponibilidades son datos de comportamiento personal bajo Ley N° 29733 |
| ¿Se cuenta con consentimiento explícito para usar esos datos? | En proceso | Aviso de consentimiento pendiente de implementar en la UI del formulario |
| ¿Los datos serán anonimizados antes de usarlos en el proyecto? | SÍ | Participantes identificados por alias dentro de la sala, sin vinculación a identidad real |
| ¿Aplica la Ley N° 29733 de Protección de Datos Personales del Perú? | SÍ | El producto recopila disponibilidad horaria y audio, ambos considerados datos personales |
| ¿Hay alguna restricción contractual o de confidencialidad? | NO | Los datos son generados por los propios usuarios para uso exclusivo dentro de la sala |

---

## SECCIÓN 5 — Autoevaluación del equipo

| Pregunta de control | Respuesta |
|---|---|
| ¿Cada semáforo tiene evidencia concreta que lo respalda? | SÍ — respaldada por pruebas del equipo con el MVP en funcionamiento |
| ¿Todos los 🔴 tienen un plan de acción con fecha y responsable? | No hay 🔴 |
| ¿El equipo verificó el acceso real a los datos antes de completar este checklist? | SÍ — el MVP está construido y los 4 tipos de input fueron probados |
| ¿La estrategia de contexto o tipo de ML es coherente con los datos disponibles? | SÍ — prompt simple es correcto porque el contexto es pequeño y varía por usuario |

---

*Framework PROMPT v1.0 — AD5018 UTEC | Plantilla 2 de 4 | EasyMeet*
