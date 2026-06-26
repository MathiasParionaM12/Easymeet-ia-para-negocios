# Resultados OKR — EasyMeet
## PC2 | AD5018 Inteligencia Artificial para Negocios | UTEC | 2026

---

## Objetivo

> Que cualquier persona pueda compartir su disponibilidad en español informal — tal como lo haría en WhatsApp — y obtener el mejor horario común con su grupo en menos de 5 minutos.

---

## KR1 — Tiempo de coordinación

| Campo | Meta comprometida | Resultado real |
|---|---|---|
| Métrica | Tiempo por persona desde que abre el link hasta confirmar su disponibilidad | — |
| Valor antes del MVP | ~35–40 min / persona (coordinación por WhatsApp) | — |
| Meta | < 5 minutos | — |
| Resultado | — | No cronometrado formalmente |
| Método | Cronometrar con grupos de 3–5 personas externas al equipo | Prueba real sin cronómetro |
| ¿Alcanzado? | — | NO MEDIDO — ver análisis |

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

## KR2 — Precisión del LLM (KPI técnico principal)

| Campo | Detalle |
|---|---|
| Métrica | % de inputs donde los horarios detectados por Gemini coinciden con la disponibilidad real esperada, sin corrección del usuario |
| Valor antes del MVP | 0% |
| Meta | ≥ 85% |
| Resultado — texto | **91%** (20 de 22 inputs correctos) |
| Resultado — imagen | **78%** (14 de 18 imágenes correctas) |
| Resultado — audio | — |
| Método | Evaluación interna: 22 inputs de texto y 18 de imagen con disponibilidad conocida → comparar horario generado vs. horario esperado campo por campo |
| Criterio "correcto" | Todos los días presentes, slots cubriendo ≥90% del tiempo esperado, sin días inventados |
| ¿Alcanzado? | PARCIAL — texto supera la meta (91% > 85%), imagen está por debajo (78% < 85%) |

**Análisis:**
```
Texto (91%): supera la meta. El cambio que más impactó fue la detección de modo 
ESPECÍFICO vs GENERAL en el prompt — antes de esa mejora el LLM añadía días no 
mencionados por el usuario.

Imagen (78%): por debajo de la meta. Los 4 casos incorrectos fueron fotos con texto 
pequeño o tomadas en ángulo. Se añadió instrucción en UI para mejorar la calidad 
de las fotos subidas.

Conclusión: el caso de uso principal (texto libre) supera la meta.
```

---

## KR3 — Tasa de completación

| Campo | Meta comprometida | Resultado real |
|---|---|---|
| Métrica | % de participantes que inician el flujo y confirman su disponibilidad | — |
| Meta | ≥ 70% | — |
| Resultado | — | **100%** (6 de 6 participantes) |
| Método | Participantes creados en Supabase vs. participantes con disponibilidad confirmada | Ejecutado |
| ¿Alcanzado? | — | **SÍ ✅** (100% > 70%) |

**Análisis:**
```
Los 6 participantes del grupo de Casacor completaron el flujo y confirmaron su 
disponibilidad. Ninguno abandonó el proceso ni necesitó asistencia.

Los 3 formatos usados (texto libre, foto de horario y audio de voz) funcionaron 
correctamente. Google Calendar no estuvo disponible porque la app opera en modo 
de prueba en Google Cloud — los participantes no estaban en la lista de test users 
aprobados.

Tasa de completación: 6/6 = 100% — supera la meta de ≥70%.
```

---

## KPI técnico — Percepción del usuario

| Campo | Meta comprometida | Resultado real |
|---|---|---|
| Métrica | % de usuarios que consideran EasyMeet más fácil que coordinar por WhatsApp | — |
| Meta | ≥ 80% | — |
| Resultado | — | **100%** (6 de 6 usuarios) |
| Método | Encuesta de 3 preguntas post-prueba con usuarios reales | Ejecutado |
| ¿Alcanzado? | — | **SÍ ✅** (100% > 80%) |

---

## Resumen ejecutivo

| | KR1 (tiempo) | KR2 — texto | KR2 — imagen | KR3 (completación) | KPI (percepción) |
|---|---|---|---|---|---|
| **Meta** | < 5 min | ≥ 85% | ≥ 85% | ≥ 70% | ≥ 80% |
| **Resultado** | No medido | 91% ✅ | 78% ⚠️ | 100% ✅ | 100% ✅ |
| **¿Alcanzado?** | N/M | SÍ | NO | SÍ | SÍ |

---

*PC2 | AD5018 UTEC 2026 — EasyMeet*
