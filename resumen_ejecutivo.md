# Resumen Ejecutivo — EasyMeet
## PC2 | AD5018 Inteligencia Artificial para Negocios | UTEC | 2026

**Equipo:** Tiago Jordan Mar · Mathias Pariona · Adriano Raffo

---

## El problema

Jóvenes de 18 a 30 años tienen dificultad para concretar reuniones con sus grupos de amigos porque cada persona gestiona su disponibilidad en un formato distinto (calendario, foto, memoria) y la comunica en lenguaje informal que ninguna herramienta de coordinación puede interpretar directamente, lo que genera 15–25 mensajes en WhatsApp durante 1 a 3 días y frecuentemente hace que la reunión nunca llegue a ocurrir no por falta de ganas, sino por agotamiento del proceso.

---

## La solución

EasyMeet es una web app donde el organizador crea una sala, comparte un link y cada participante ingresa su disponibilidad en el formato que le resulte más natural texto en español informal, foto de su horario, audio de voz o Google Calendar. Gemini 2.5-flash extrae los bloques de tiempo de cada input, el participante confirma lo que la IA interpretó, y el sistema calcula y presenta los 3 mejores horarios comunes para el grupo.

**Lo que hace diferente a EasyMeet:** no pide que el usuario cambie cómo habla. "El viernes todo el día pero el sábado no puedo por la mañana" es un input válido y suficiente.

---

## Stack implementado

| Componente | Tecnología |
|---|---|
| Frontend + API | Next.js 16.2.9 (App Router) + TypeScript + Tailwind CSS 4 |
| Motor de IA | Google Gemini 2.5-flash (texto, visión y audio en un solo modelo) |
| Base de datos | Supabase PostgreSQL + Realtime (WebSocket) |
| Autenticación Google | OAuth 2.0 + Calendar FreeBusy API |
| Deploy | Vercel |

---

## MVP funcional — features implementadas

- **F1** Landing page: crear sala con nombre del evento y rango de fechas
- **F2** Dashboard del organizador: link compartible + lista de participantes en tiempo real + agregar su propia disponibilidad
- **F3** Formulario de participante: ingreso de nombre y elección de formato de input
- **F4** Extracción por texto libre (Gemini 2.5-flash)
- **F5** Extracción por foto de horario (Gemini visión), audio de voz (Gemini audio) y Google Calendar (OAuth 2.0 + FreeBusy API)
- **F6** Confirmación: el participante revisa y aprueba lo que el LLM extrajo antes de guardarlo
- **F7** Pantalla de éxito con estado del grupo
- **F8** Algoritmo de overlap: top 3 horarios comunes (grid de 30 min, bloques ≥60 min, preferencia por 17:00–22:00)

**MVP disponible en:** https://easymeet-app.vercel.app

---

## Resultados de evaluación técnica (KR2)

| Input | Precisión | Detalle |
|---|---|---|
| Texto libre | **91%** | 20 de 22 inputs correctos |
| Foto de horario | **78%** | 14 de 18 imágenes correctas |
| Audio | — | No evaluado en esta iteración |

Metodología: evaluación interna con 40 inputs de disponibilidad conocida → comparar horario generado vs. horario esperado campo por campo. Criterio "correcto": todos los días presentes, slots cubriendo ≥90% del tiempo esperado, sin días inventados.

---

## Resultados pendientes

| Métrica | Meta | Resultado |
|---|---|---|
| KR1 — Tiempo de coordinación | < 5 minutos | No medido (prueba fue asíncrona, sin cronómetro) |
| KR2 — Precisión del LLM | ≥ 85% | Texto: 91% ✅ / Imagen: 78% ⚠️ |
| KR3 — Tasa de completación | ≥ 70% | 100% ✅ (6/6 usuarios, prueba Casacor) |
| KPI — Percepción del usuario | ≥ 80% prefiere EasyMeet vs WhatsApp | 100% ✅ (6/6 usuarios) |

---

## Cambio principal vs. PC1

PC1 planificó un stack de n8n + Bubble + GPT-4o + Whisper + Google Sheets que nunca fue construido. PC2 documenta el stack real: Next.js + Supabase + Gemini 2.5-flash. El cambio más importante no fue técnico sino conceptual la reformulación del problema de "coordinar horarios" (que Calendar ya resuelve) a "leer disponibilidad en lenguaje informal" (que solo un LLM puede resolver).

---
