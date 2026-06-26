# Pruebas con Usuarios — EasyMeet
## PC2 | AD5018 Inteligencia Artificial para Negocios | UTEC | 2026

---

## Registro de pruebas

**Contexto:** Grupo de 6 amigos coordinando una salida a Casacor. La organizadora (Valeria Paliza) creó la sala y compartió el link. Cada participante ingresó su disponibilidad de forma independiente, en el momento que pudo.

| # | Perfil del usuario | Tarea asignada | ¿Completó? | Observaciones clave |
|---|---|---|---|---|
| 1 | Valeria Paliza — organizadora, joven adulta, Lima | Crear sala, compartir link e ingresar disponibilidad propia (texto libre) | SÍ | Usó el botón "Agregar mi disponibilidad →" sin confusión. Encontró el flujo intuitivo. |
| 2 | Hayro Bonifaz — participante, joven adulto, Lima | Ingresar disponibilidad vía foto de horario | SÍ | La IA extrajo correctamente los bloques de tiempo de la imagen. Sin necesidad de correcciones. |
| 3 | Valeria Perez — participante, joven adulta, Lima | Ingresar disponibilidad en texto libre | SÍ | Escribió disponibilidad en lenguaje informal. El sistema interpretó correctamente. |
| 4 | Daniella Del Carpio — participante, joven adulta, Lima | Ingresar disponibilidad vía audio de voz | SÍ | Grabó su disponibilidad hablando. Confirmó que el resultado fue correcto. |
| 5 | Luciana Vargas — participante, joven adulta, Lima | Ingresar disponibilidad en texto libre | SÍ | Sin incidencias. Completó el flujo en pocos minutos. |
| 6 | Helena De Osma — participante, joven adulta, Lima | Ingresar disponibilidad vía foto de horario | SÍ | Subió foto de su horario. Resultado correcto según confirmó. |

---

## Hallazgo pre-pruebas (ya documentado)

**Usuario: Rubén**

El organizador que crea la sala no encontraba forma de agregar su propia disponibilidad — solo veía el dashboard de participantes. El organizador también es parte del grupo y necesita ingresar cuándo puede.

**Corrección implementada:** Se añadió el botón "Agregar mi disponibilidad →" en el dashboard del organizador, que redirige al mismo formulario de participante con el nombre del organizador prellenado.

---

## Encuesta post-prueba (3 preguntas)

1. ¿EasyMeet fue más fácil que coordinar por WhatsApp? → **SÍ / NO / IGUAL**
2. ¿Lo que el sistema interpretó de tu disponibilidad fue correcto? → **SÍ / CASI / NO**
3. ¿Lo usarías la próxima vez que quieras coordinar una salida? → **SÍ / NO**

### Resultados de la encuesta

| # | Usuario | Pregunta 1 (¿más fácil que WhatsApp?) | Pregunta 2 (¿interpretación correcta?) | Pregunta 3 (¿lo usarías?) |
|---|---|---|---|---|
| 1 | Valeria Paliza | SÍ | SÍ | SÍ |
| 2 | Hayro Bonifaz | SÍ | SÍ | SÍ |
| 3 | Valeria Perez | SÍ | SÍ | SÍ |
| 4 | Daniella Del Carpio | SÍ | SÍ | SÍ |
| 5 | Luciana Vargas | SÍ | SÍ | SÍ |
| 6 | Helena De Osma | SÍ | SÍ | SÍ |

**Resultados agregados:**
- Pregunta 1: 6/6 dijeron SÍ (100%)
- Pregunta 2: 6/6 dijeron SÍ (100%)
- Pregunta 3: 6/6 dijeron SÍ (100%)

---

## Lo que funcionó bien

```
1. El flujo completo fue intuitivo para todos los participantes — ninguno necesitó instrucciones adicionales.
2. Los 3 formatos probados (texto, foto y audio) funcionaron correctamente y fueron bien recibidos.
3. El grupo logró coordinar la salida a Casacor usando EasyMeet — el sistema encontró horarios en común.
4. La pantalla de confirmación generó confianza: los usuarios podían ver qué había interpretado la IA antes de aprobar.
```

## Lo que no funcionó o confundió al usuario

```
1. Google Calendar no estaba disponible para los participantes — la app está en modo de prueba en Google Cloud
   y solo acepta correos pre-aprobados como test users. Los participantes no estaban en esa lista.
   → Impacto: ningún participante pudo probar el flujo de Google Calendar.
   → No afectó la coordinación: todos usaron texto, foto o audio sin problema.
2. El organizador no encontraba cómo agregar su propia disponibilidad (hallazgo pre-pruebas, ya corregido).
```

## Cambios realizados al MVP como resultado de las pruebas

```
1. Botón "Agregar mi disponibilidad →" en el dashboard del organizador (fix hallazgo Rubén).
2. Pendiente: solicitar verificación de app en Google Cloud para que Google Calendar esté disponible
   para cualquier usuario, no solo los pre-aprobados.
```

---

*PC2 | AD5018 UTEC 2026 — Pruebas realizadas con grupo real coordinando salida a Casacor, Lima.*
