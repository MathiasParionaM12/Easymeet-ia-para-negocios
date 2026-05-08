# Plantilla 1 — Problem Statement Canvas
## Framework PROMPT | Fase P — Problema de Negocio
### AD5018 Inteligencia Artificial para Negocios | UTEC

---

**Equipo:**
- Integrante 1: Tiago Jordan Mar
- Integrante 2: Adriano Enrique Raffo Mariaca
- Integrante 3: Mathias Pariona Mego

**Fecha de entrega:** Semana 7 — 2026
**Versión del canvas:** v1

---

## SECCIÓN 1 — Definición del problema

### 1.1 Usuario afectado
> *¿Quién sufre el problema? Sé específico: no "las empresas" sino "el jefe de ventas de una pyme retail".*

```
Jóvenes adultos de 18 a 30 años que forman parte de grupos de amigos con agendas
ocupadas y variables, donde cada persona gestiona su disponibilidad en una plataforma
o formato distinto (Google Calendar, Outlook, horario fijo semanal, memoria).
```

---

### 1.2 Problema específico
> *¿Qué está pasando exactamente? Describe la situación actual sin mencionar soluciones.*

```
Cuando un grupo de amigos intenta coordinar una reunión, no existe ningún punto de
encuentro común para compartir disponibilidad. Cada persona tiene su agenda en un
formato distinto: algunos usan Google Calendar, otros Outlook, otros tienen una foto de
su horario semanal guardada en el celular, y muchos simplemente lo recuerdan de manera
informal. El proceso de coordinación termina siendo una cadena interminable de mensajes
de WhatsApp con preguntas como "¿puedes el viernes?" o "yo no puedo antes de las 7pm".
```

---

### 1.3 Causa raíz
> *¿Por qué ocurre el problema? No el síntoma — la causa real.*

```
No existe una plataforma que unifique disponibilidades expresadas en múltiples formatos
heterogéneos (calendarios digitales, imágenes de horario, texto libre, audio) en un
formato estructurado y comparable. Las apps de calendario existentes solo funcionan si
todos los miembros del grupo ya usan el mismo sistema, lo cual raramente ocurre en
contextos sociales informales.
```

---

### 1.4 Consecuencia medible
> *¿Qué pierde el usuario sin solución? Expresa en números cuando sea posible.*

```
Coordinar una reunión entre amigos suele convertirse en un proceso más largo y desgastante de lo esperado.
Según una encuesta exploratoria realizada a 15 personas del segmento objetivo, el 80% indicó que coordinar
planes en grupo toma más tiempo del que debería, mientras que el proceso puede extenderse entre 1 y 3 días
esperando que todos respondan. Además, el 67% afirmó haber abandonado o perdido interés en una salida debido
a la dificultad de encontrar un horario común. En muchos casos, la falta de una forma centralizada de compartir
disponibilidades termina generando frustración y retrasando la decisión final del grupo.
```

---

### 1.5 Declaración del problema — formato obligatorio

**"[Tipo de usuario] tiene dificultad para [acción específica] porque [causa raíz], lo que genera [consecuencia medible]."**

```
"Jóvenes adultos de 18 a 30 años tienen dificultad para coordinar reuniones con sus grupos de amigos
porque no existe una plataforma que unifique disponibilidades expresadas en distintos formatos
(Google Calendar, Outlook, fotos de horario, texto libre y audio), lo que genera demoras de entre 1
y 3 días para encontrar un horario común y provoca frustración, pérdida de interés y abandono frecuente
de planes durante el proceso de coordinación."
```

---

## SECCIÓN 2 — Filtro de validación IA

| Pregunta | SÍ / NO | Justificación (1 línea) |
|---|---|---|
| ¿Una hoja de cálculo o formulario resuelve esto? | NO | No puede procesar texto informal, fotos de horarios ni audio, solo admite datos ya estructurados |
| ¿El problema escala con volumen de datos o usuarios? | SÍ | A mayor número de integrantes, más formatos distintos y mayor complejidad de coordinación |
| ¿Hay un patrón repetitivo difícil de procesar manualmente? | SÍ | Extraer horarios de texto libre, imágenes y audio sigue un patrón que requiere comprensión semántica |
| ¿El problema requiere generar contenido o razonar en lenguaje natural? | SÍ | Interpretar "tengo libre las tardes excepto cuando hay pichanga" requiere comprensión lingüística contextual |
| ¿Necesitas predecir Y luego explicar o actuar sobre el resultado? | NO | No se predice un evento futuro; se extrae y compara disponibilidad ya existente |

**Conclusión del filtro:**

```
La IA es la respuesta correcta porque el problema central es interpretar información
heterogénea expresada en lenguaje natural, imágenes y audio, y transformarla en datos
estructurables. Una hoja de cálculo o formulario simple solo funcionaría si todos los
usuarios ya tuvieran su disponibilidad en un formato estandarizado, lo que no ocurre
en la práctica. Ninguna solución no-IA puede leer una foto de un horario universitario
y extraer de ella bloques de tiempo disponibles. La IA Generativa multimodal es la
única tecnología que puede unificar estos formatos distintos de manera confiable.
```

---

## SECCIÓN 3 — Tipo de IA elegido

Marca con una X la opción elegida:

- [x] **IA Generativa** — el problema involucra lenguaje natural, conversación o generación de contenido
- [ ] **ML Tradicional** — el problema requiere predecir, clasificar o segmentar con datos históricos
- [ ] **Combinación** — se necesita predecir Y comunicar/actuar sobre el resultado

### Justificación de la elección

```
El núcleo del problema es procesar múltiples formatos de entrada no estructurados
(texto libre en español informal, fotos de horarios, audio) y convertirlos en datos
comparables. Esto requiere comprensión semántica y capacidades multimodales (texto +
visión) que solo ofrece la IA Generativa. El ML Tradicional queda descartado porque
no existe un dataset histórico de "disponibilidades" que entrenar a cada usuario genera
su propia información en tiempo real. La combinación ML + GenAI no aplica porque no
hay una variable a predecir: la disponibilidad la declara el propio usuario.
Los modelos LLM modernos con visión (GPT-4o, Claude) pueden leer texto informal,
interpretar una foto de un horario universitario y estructurar la respuesta en JSON,
exactamente lo que este producto necesita.
```

---

## SECCIÓN 4 — Autoevaluación del equipo

| Pregunta de control | Respuesta |
|---|---|
| ¿El problema está descrito sin mencionar tecnología? | SÍ |
| ¿La declaración del problema sigue el formato exacto? | SÍ |
| ¿La elección del tipo de IA se justifica con el problema, no con la preferencia? | SÍ |
| ¿Todos los integrantes pueden explicar este canvas sin leerlo? | SÍ |

---

*Framework PROMPT v1.0 — AD5018 UTEC | Plantilla 1 de 4*
