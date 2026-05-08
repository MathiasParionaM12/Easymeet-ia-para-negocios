# Plantilla 2 — Data Readiness Checklist
## Framework PROMPT | Fase R — Recursos de Datos
### AD5018 Inteligencia Artificial para Negocios | UTEC

---

**Equipo:**
- Integrante 1: Tiago Jordan Mar
- Integrante 2: Adriano Enrique Raffo Mariaca
- Integrante 3: Mathias Pariona Mego

**Fecha de entrega:** Semana 6 — 2025
**Tipo de IA del proyecto:** IA Generativa (LLM multimodal con visión)

---

> **Nota importante sobre la naturaleza de los datos de este proyecto:**
> EasyMeet es un producto de IA Generativa donde los datos no son un dataset histórico
> pre-existente, sino información generada por cada usuario en tiempo real al usar el
> producto. Esto elimina los riesgos más comunes de disponibilidad de datos. El "inventario"
> corresponde a los tipos de input que el sistema debe ser capaz de procesar.

---

## SECCIÓN 1 — Inventario de datos

### Para IA Generativa — Inventario de conocimiento

| # | Tipo de información | Dónde está actualmente | Formato | ¿Está disponible? |
|---|---|---|---|---|
| 1 | Disponibilidad expresada en texto libre | El usuario la ingresa directamente en el formulario al usar la app | Texto (español informal) | SÍ |
| 2 | Foto de horario semanal o mensual | En el celular o computadora del usuario | JPG / PNG | SÍ |
| 3 | Archivo de calendario exportado | En Google Calendar o Outlook del usuario | .ics / .csv | SÍ (con fricción leve) |
| 4 | System prompt e instrucciones de extracción | Definido y controlado por el equipo | Texto (prompt de IA) | SÍ |
| 5 | Ejemplos de disponibilidad para few-shot | Generados por el equipo durante las pruebas | Texto / JSON | SÍ |

**Estrategia de contexto elegida:**
- [x] Prompt simple *(base de conocimiento pequeña y estable — el sistema prompt define el comportamiento; cada input del usuario se procesa en tiempo real sin base de conocimiento externa)*
- [ ] RAG
- [ ] Memoria de sesión

**Justificación de la estrategia:**
El producto no requiere una base de conocimiento corporativa grande. El LLM solo necesita entender el input del usuario y transformarlo en JSON estructurado. Todo el contexto cabe en el system prompt. La memoria de sesión sí aplica dentro de una misma sala de coordinación (el sistema recuerda la disponibilidad de cada participante mientras dura la sesión).

---

## SECCIÓN 2 — Evaluación de calidad con semáforo

> 🟢 Listo | 🟡 Necesita trabajo | 🔴 Bloqueante

---

### Fuente 1: Texto libre de disponibilidad (input principal del usuario)

| Dimensión | Semáforo | Evidencia que respalda la evaluación | Plan de acción |
|---|---|---|---|
| **Disponibilidad** | 🟢 | El usuario lo genera en tiempo real al usar la app. No hay dependencia de terceros. | — |
| **Volumen** | 🟢 | Con un input por usuario el sistema funciona. No se requiere dataset de entrenamiento. | — |
| **Calidad** | 🟡 | Depende de qué tan claro escriba el usuario. Texto muy vago ("no sé, cuando pueda") puede generar extracciones incorrectas. | Incluir en la interfaz ejemplos de cómo escribir la disponibilidad. El LLM pedirá clarificación si el input es ambiguo. |
| **Relevancia** | 🟢 | Directamente relacionado con el problema: es exactamente la información que el producto necesita. | — |
| **Legalidad** | 🟡 | Los horarios son datos de comportamiento personal. Requieren consentimiento informado. | Aviso visible antes de ingresar datos: "Tu disponibilidad se procesa para encontrar horarios comunes y no se almacena tras generar el resultado." |

---

### Fuente 2: Foto de horario (imagen)

| Dimensión | Semáforo | Evidencia | Plan de acción |
|---|---|---|---|
| **Disponibilidad** | 🟢 | El usuario la sube desde su celular o computadora. Acceso inmediato. | — |
| **Volumen** | 🟢 | Una imagen por usuario es suficiente para el propósito del producto. | — |
| **Calidad** | 🟡 | Fotos borrosas, con poca luz o tomadas en ángulo pueden dificultar la extracción. GPT-4o y Claude tienen alta tolerancia a imágenes imperfectas, pero hay un límite. | Instrucciones claras en la UI: "Toma la foto de frente, con buena luz". Si el LLM no puede extraer el horario, informa al usuario y ofrece la alternativa de texto. |
| **Relevancia** | 🟢 | Directamente relacionado: es uno de los formatos más comunes de horario en contextos universitarios y laborales. | — |
| **Legalidad** | 🟢 | El usuario sube su propio horario. No contiene datos sensibles de terceros. | — |

---

### Fuente 3: Archivo .ics / exportación de Google Calendar u Outlook

| Dimensión | Semáforo | Evidencia | Plan de acción |
|---|---|---|---|
| **Disponibilidad** | 🟡 | El archivo existe en la plataforma del usuario, pero requiere que sepa cómo exportarlo. No todos conocen este proceso. | Guía paso a paso con capturas de pantalla en la UI para exportar desde Google Calendar y Outlook. |
| **Volumen** | 🟢 | Un archivo por usuario es suficiente. | — |
| **Calidad** | 🟢 | Formato .ics es estándar, bien estructurado y fácil de parsear. Alta confiabilidad. | — |
| **Relevancia** | 🟢 | Directamente relacionado. Contiene exactamente la información de disponibilidad que el producto necesita. | — |
| **Legalidad** | 🟡 | El archivo puede contener eventos privados (citas médicas, eventos personales). El sistema debe informar qué extrae. | Avisar al usuario que solo se leen los bloques de "ocupado/libre" y no los títulos de eventos. Ofrecer opción de revisar antes de confirmar. |

---

## SECCIÓN 3 — Plan de resolución de bloqueantes

> No existen semáforos 🔴 en este proyecto. Los puntos 🟡 tienen planes concretos arriba.
> El equipo los resolverá durante el diseño de la interfaz (Semana 7) antes de construir el MVP.

**No aplica resolución de bloqueantes críticos.**

Resumen de acciones para 🟡:
1. Diseñar mensajes de ayuda en la UI con ejemplos de texto de disponibilidad (Semana 7)
2. Incluir aviso de privacidad y consentimiento antes de procesar cualquier dato (Semana 7)
3. Crear guía visual para exportar .ics desde Google Calendar y Outlook (Semana 8)
4. Definir mensaje de fallback cuando una imagen no pueda ser procesada (Semana 8)

---

## SECCIÓN 4 — Privacidad y legalidad de los datos

| Pregunta | Respuesta | Detalle |
|---|---|---|
| ¿Los datos contienen información personal de usuarios? | SÍ | Los horarios y disponibilidades son datos de comportamiento personal |
| ¿Se cuenta con consentimiento explícito para usar esos datos? | SÍ (a diseñar) | Se mostrará aviso de consentimiento antes de ingresar cualquier dato en el MVP |
| ¿Los datos serán anonimizados antes de usarlos en el proyecto? | SÍ | Los datos de disponibilidad no incluyen nombre completo ni identificación; se asocian a un alias o apodo dentro de la sala |
| ¿Aplica la Ley N° 29733 de Protección de Datos Personales del Perú? | SÍ | El producto recopila y procesa disponibilidad horaria de personas, considerada dato personal de comportamiento |
| ¿Hay alguna restricción contractual o de confidencialidad? | NO | Los datos son generados y subidos voluntariamente por los propios usuarios |

---

## SECCIÓN 5 — Autoevaluación del equipo

| Pregunta de control | Respuesta |
|---|---|
| ¿Cada semáforo tiene evidencia concreta que lo respalda? | SÍ |
| ¿Todos los 🔴 tienen un plan de acción con fecha y responsable? | SÍ (no hay 🔴) |
| ¿El equipo verificó el acceso real a los datos antes de completar este checklist? | SÍ — los datos son generados por el usuario en tiempo real; se probó que GPT-4o y Claude pueden procesar texto informal e imágenes de horarios en pruebas preliminares |
| ¿La estrategia de contexto es coherente con los datos disponibles? | SÍ — prompt simple es adecuado porque el contexto es pequeño y el input varía por usuario |

---

*Framework PROMPT v1.0 — AD5018 UTEC | Plantilla 2 de 4*
