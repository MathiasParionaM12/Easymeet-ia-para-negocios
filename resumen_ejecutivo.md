# Resumen Ejecutivo — EasyMeet

## · Nombre del MVP y usuario principal

### Nombre del MVP
**EasyMeet**

### Usuario principal
Jóvenes adultos de 18 a 30 años que coordinan reuniones sociales en grupos de amigos de 3 a 6 personas, donde cada integrante administra su tiempo en formatos distintos como Google Calendar, Outlook, horarios en imagen o memoria informal.

---

# · Declaración del problema

> “Jóvenes adultos de 18 a 30 años tienen dificultad para coordinar reuniones con sus grupos de amigos porque no existe una plataforma que unifique disponibilidades expresadas en distintos formatos (Google Calendar, Outlook, fotos de horario, texto libre y audio), lo que genera un promedio de 18 a 25 mensajes intercambiados y entre 1 y 3 días perdidos para agendar un encuentro simple, con una tasa de cancelación elevada por agotamiento del proceso.”

---

# · Tipo de IA elegido y justificación

### Tipo de IA
**IA Generativa (LLM multimodal con visión)**

### Justificación
El problema requiere interpretar información no estructurada proveniente de múltiples formatos como texto libre, imágenes de horarios y archivos de calendario. Modelos multimodales como GPT-4o o Claude permiten comprender lenguaje natural, analizar imágenes y transformar la información en datos estructurados comparables.

No se eligió ML tradicional porque no existe un dataset histórico para entrenar modelos predictivos; la disponibilidad es generada dinámicamente por cada usuario en tiempo real.

---

# · Estado del diagnóstico de datos

## Fuentes identificadas
- Texto libre ingresado por el usuario
- Fotos de horarios semanales/mensuales
- Archivos .ics exportados desde Google Calendar y Outlook
- Prompt de extracción diseñado por el equipo
- Ejemplos few-shot para pruebas

## Semáforo general
🟡 **Necesita trabajo menor**

### Principales riesgos detectados
- Inputs ambiguos en texto libre
- Imágenes borrosas o mal tomadas
- Fricción al exportar archivos .ics
- Necesidad de consentimiento y manejo de privacidad

### Estado general
No existen bloqueantes críticos. Todos los puntos identificados tienen planes de mitigación definidos para el MVP.

---

# · Descripción del producto

## ¿Qué hace?
EasyMeet permite coordinar reuniones automáticamente usando IA para unificar disponibilidades ingresadas en diferentes formatos y encontrar los mejores horarios comunes.

## Flujo del producto
1. Un organizador crea una sala y comparte un link
2. Los participantes ingresan su disponibilidad:
   - Texto libre
   - Imagen de horario
   - Archivo .ics
3. El LLM procesa y estructura los horarios
4. El sistema compara disponibilidades
5. EasyMeet genera las 3 mejores opciones de reunión
6. El organizador confirma el horario final

## Alcance del MVP
### Incluye:
- Creación de salas compartidas
- Procesamiento de texto e imágenes
- Comparación automática de horarios
- Confirmación humana antes del resultado final

### No incluye:
- Integración OAuth con Google Calendar
- Entrada por audio
- Notificaciones automáticas
- Historial de reuniones
- Sistema de cuentas/login

---

# · Decisión tecnológica Build / Buy / Integrate

## Decisión elegida
**Integrate**

## Justificación
El equipo integrará APIs de IA existentes (GPT-4o o Claude) dentro de un flujo propio usando herramientas no-code. El valor diferencial del producto está en la experiencia de usuario y la integración multimodal, no en entrenar un modelo desde cero.

## Stack tecnológico
- Bubble.io → Frontend
- n8n → Automatización de flujos
- Google Sheets → Almacenamiento temporal
- OpenAI / Anthropic APIs → Procesamiento IA

## Estimación de costo referencial
- Mínimo: **S/. 0 / mes** usando free tiers
- Máximo estimado MVP: **S/. 25 / mes**

### Supuestos
- 30–50 pruebas reales de usuarios
- Bajo volumen de llamadas API
- Uso de herramientas no-code gratuitas

---

# · OKRs y KPI técnico

## Objetivo (O)
Eliminar la fricción de coordinar reuniones entre personas con agendas y formatos distintos, reduciendo significativamente el tiempo y mensajes necesarios para llegar a un acuerdo.

---

## KR1 — Tiempo de coordinación
- Valor actual: 30–45 minutos por persona
- Meta MVP: menos de 5 minutos
- Medición: pruebas con usuarios externos

---

## KR2 — Precisión de extracción del LLM
- Valor actual: 0%
- Meta MVP: ≥ 85% de extracción correcta
- Medición: validación manual sobre 25 casos de prueba

---

## KR3 — Tasa de completación del flujo
- Valor actual: N/A
- Meta MVP: ≥ 70% de usuarios completan el proceso
- Medición: sesiones iniciadas vs completadas

---

## KPI técnico principal
### Tasa de extracción correcta de horarios
- Criterio mínimo aceptable: >85%
- Evaluación manual comparando el JSON generado vs disponibilidad real
