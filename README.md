# EasyMeet

## Descripción del proyecto

EasyMeet es un MVP de IA Generativa diseñado para resolver el problema de coordinación de reuniones entre grupos de personas que manejan sus horarios en distintos formatos.

La plataforma permite que los usuarios ingresen su disponibilidad mediante:
- Texto libre
- Imágenes de horarios
- Archivos de calendario (.ics)

Usando modelos multimodales como GPT-4o o Claude, el sistema interpreta la información, la convierte en datos estructurados y encuentra automáticamente los mejores horarios comunes para reunirse.

---

# Objetivo del proyecto

Reducir el tiempo, esfuerzo y cantidad de mensajes necesarios para coordinar reuniones entre personas con agendas y formatos heterogéneos.

---

# Tipo de IA utilizada

- IA Generativa
- LLM multimodal con visión
- Procesamiento de lenguaje natural
- Extracción estructurada de información

---

# Stack tecnológico

| Herramienta | Función |
|---|---|
| Bubble.io | Frontend del MVP |
| n8n | Automatización de flujos |
| OpenAI / Anthropic APIs | Procesamiento IA |
| Google Sheets | Almacenamiento temporal |

---

# Índice del repositorio

## Documentación principal

| Archivo | Descripción |
|---|---|
| [README.md](./README.md) | Índice general y descripción del proyecto |
| [resumen_ejecutivo.md](./resumen_ejecutivo.md) | Resumen ejecutivo completo del MVP |

---

## Framework PROMPT — Fase P (Problema)

| Archivo | Descripción |
|---|---|
| [plantilla_1_problem_statement.md](./plantilla_1_problem_statement.md) | Definición del problema, usuario afectado, causa raíz y validación del uso de IA |

---

## Framework PROMPT — Fase R (Data Readiness)

| Archivo | Descripción |
|---|---|
| [plantilla_2_data_readiness.md](./plantilla_2_data_readiness.md) | Diagnóstico de datos, evaluación de calidad, privacidad y readiness del proyecto |

---

## Framework PROMPT — Fase O (AI Product Canvas)

| Archivo | Descripción |
|---|---|
| [plantilla_3_ai_product_canvas.md](./plantilla_3_ai_product_canvas.md) | Diseño completo del MVP, arquitectura funcional, flujo del producto, prompts, alcance y OKRs |

---

# Flujo general del MVP

1. El organizador crea una sala compartida
2. Comparte el link con los participantes
3. Cada usuario ingresa disponibilidad
4. El LLM procesa la información
5. El sistema encuentra intersecciones horarias
6. EasyMeet propone los mejores horarios
7. El organizador confirma la reunión

---

# Estado actual del proyecto

## Completado
- Problem Statement
- Data Readiness Checklist
- AI Product Canvas
- Diseño conceptual del MVP
- Definición de stack tecnológico
- Diseño del system prompt

## Pendiente
- Construcción del frontend
- Integración de APIs
- Automatización en n8n
- Testing con usuarios reales
- Métricas de validación del MVP

---

# Objetivos de validación

| Métrica | Meta |
|---|---|
| Tiempo de coordinación | < 5 minutos |
| Precisión de extracción IA | ≥ 85% |
| Tasa de completación | ≥ 70% |

---

# Equipo

Proyecto desarrollado para el curso:

**AD5018 — Inteligencia Artificial para Negocios | UTEC**
