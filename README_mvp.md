# EasyMeet — MVP para el Evaluador
## PC2 | AD5018 Inteligencia Artificial para Negocios | UTEC | 2026

---

## URL del MVP

🔗 **https://easymeet-app.vercel.app**

> Funciona en cualquier navegador moderno (Chrome, Safari, Firefox).
> No requiere instalación ni cuenta de usuario.

---

## Cómo usar EasyMeet como evaluador

### Flujo completo (menos de 5 minutos)

**Paso 1 — Crear una sala**
1. Ir a la URL del MVP
2. En la landing page, ingresar:
   - Nombre del evento (ej: "almuerzo del grupo")
   - Nombre del organizador (ej: "Evaluador")
   - Rango de fechas (ej: esta semana)
3. Hacer clic en "Crear sala"
4. Se genera un link único para compartir

**Paso 2 — Ingresar disponibilidad como organizador**
1. En el dashboard, hacer clic en "Agregar mi disponibilidad →"
2. Escribir disponibilidad en texto libre, por ejemplo:
   - *"Puedo el martes de 12 a 3 y el jueves todo el día"*
   - *"El miércoles en la tarde, el viernes libre"*
3. Hacer clic en "Analizar →"
4. Revisar lo que la IA extrajo en la pantalla de confirmación
5. Confirmar o editar si algo está incorrecto
6. Hacer clic en "Confirmar disponibilidad"

**Paso 3 — Simular un segundo participante**
1. Abrir el link de la sala en una ventana privada o en otro dispositivo
2. Ingresar un nombre distinto (ej: "Participante")
3. Ingresar disponibilidad en texto libre
4. Confirmar

**Paso 4 — Ver los mejores horarios**
1. Volver al dashboard del organizador
2. Cuando todos hayan confirmado, ver el botón "Ver mejores horarios"
3. El sistema muestra las 3 opciones de horario donde todos coinciden

---

## Funcionalidades adicionales disponibles

| Feature | Cómo probarla |
|---|---|
| **Foto de horario** | En el formulario de participante, seleccionar la pestaña "Foto" y subir una imagen de un horario de clases |
| **Google Calendar** | Seleccionar la pestaña "Calendario" e iniciar sesión con Google — solo se leen bloques libre/ocupado |
| **Audio de voz** | Seleccionar la pestaña "Voz" y grabar diciendo tu disponibilidad |
| **Realtime** | Abrir el dashboard en una ventana y el formulario en otra — los participantes aparecen en tiempo real |

---

## Stack técnico

```
Frontend: Next.js 16.2.9 (App Router) + TypeScript + Tailwind CSS 4 + shadcn/ui
IA:       Google Gemini 2.5-flash (texto, visión y audio)
Base de datos: Supabase PostgreSQL + Realtime
Auth:     Google OAuth 2.0 + Calendar FreeBusy API
Deploy:   Vercel
```

---

## Notas para el evaluador

- **No se requiere cuenta**: el organizador se identifica con su nombre y una clave de administrador (UUID generado automáticamente al crear la sala)
- **Los datos se eliminan** cuando el organizador cierra la sala
- **El audio nunca se almacena**: se procesa en tiempo real y solo se guarda el JSON de disponibilidad resultante
- **Si la IA extrae algo incorrecto**: el sistema lo muestra para que el participante lo corrija antes de guardar (paso de confirmación obligatorio)

---

*EasyMeet — PC2 | AD5018 UTEC 2026*
