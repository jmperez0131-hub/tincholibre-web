# Spec: WhatsApp Community + Sistema de Outreach
**Fecha:** 2026-05-19  
**Estado:** Diseño aprobado · pendiente de implementación  
**Tareas relacionadas:** Tarea 12 (outreach bootcamps) · Tarea 13 (outreach contactos cálidos) · Tarea 6 (Skool — ver spec `2026-04-25-skool-community-design.md`)

---

## 1. Contexto y relación con el spec de Skool

Este spec define la capa de WhatsApp Community que **complementa** (no reemplaza) la comunidad Skool "El Oasis". Los dos activos son distintos y paralelos:

| Criterio | WhatsApp Community | Skool — El Oasis |
|----------|--------------------|------------------|
| Propósito | Contacto diario, vínculo humano, acceso fácil | Profundidad, biblioteca, sesiones en vivo, gamificación |
| Contenido | Audios cortos, texto breve, prácticas de 3–5 min | Posts extensos, recursos permanentes, replays, cursos |
| Permanencia | Efímero (desaparece en el scroll) | Buscable, categorizado, acumulable |
| Momento de consumo | En tránsito, mañana o noche | Con tiempo, en quietud |
| Audiencia inicial | Contactos de bootcamps + MDI (warm audience) | Cualquier persona que llega por funnel o invitación |
| Costo | Gratis para todos | Gratis (tier Oasis) → $37–47/mes (tier Sistema) |

**Flujo de usuario entre plataformas:**

```
Mensaje personal de Tincho
         ↓
WhatsApp Community (entrada cálida, gratuita)
         ↓
Valor diario + mención semanal de Skool
         ↓
Skool El Oasis (gratis primero, luego pago)
         ↓
Productos Hotmart + Acompañamiento 1:1
```

---

## 2. Estructura de la WhatsApp Community

**Nombre:** Oasis de Calma — Tincho  
**Plataforma:** WhatsApp Community (feature oficial de Meta, hasta 2000 miembros, gratuito)

```
Community: "Oasis de Calma — Tincho"
├── 📢 Anuncios           (solo Tincho escribe)
└── 🌬️ Práctica Diaria   (todos participan — grupo principal)
```

**Fase 2 (cuando supere 100 miembros activos):**
```
├── 📖 Recursos y Herramientas   (links, PDFs, audios descargables)
└── 💬 Preguntas y Compartir     (espacio abierto de conversación)
```

Arrancar solo con dos grupos reduce la carga operativa y concentra la energía donde más importa.

---

## 3. Plan de contenido — WhatsApp Community

### Frecuencia
- **Práctica Diaria:** 1 pieza por día, lunes a viernes
- **Anuncios:** 1–2 veces por semana (mínimo: cada sesión de Skool; máximo: novedad real)
- **Fin de semana:** liviano — sábado silencio o recordatorio del reto; domingo check-in breve

### Rotación semanal

| Día | Tipo | Formato | Qué es exactamente |
|-----|------|---------|-------------------|
| Lunes | Activación de semana | Audio voz 60–90 seg | Anticipa el trabajo de la semana. No es clase — es encuadre. |
| Martes | Pregunta de reflexión | Texto 3–5 líneas | Pregunta específica sobre el dolor de la semana. Invita respuesta de 1–3 palabras. |
| Miércoles | Mini práctica guiada | Audio voz 3–5 min | Protocolo de respiración o movimiento corto. Sin producción. Voz real. |
| Jueves | Traducción de concepto | Texto 3–5 líneas | Concepto técnico o espiritual → lenguaje de cliente. Usa la tabla de traducciones del CLAUDE.md. |
| Viernes | Cierre + reto fin de semana | Texto + audio opcional | Reto de <2 minutos para el fin de semana. Una sola acción. |

### Reglas de formato

- **Audios de voz:** máximo 2 minutos. Sin intro larga — empezar con la práctica o la frase directa.
- **Textos:** máximo 5 líneas. Lo que cabe en una pantalla sin scrollear.
- **Links:** solo cuando hay algo concreto que descargar. No links a artículos ni blogs.
- **Videos:** opcionales, solo para la práctica del miércoles cuando el movimiento requiera verse.

### Mecánicas de engagement

1. **Reto semanal** — anunciado el viernes, check-in el domingo: *"¿Lo hiciste? Una palabra."*
2. **Pregunta de los martes** — específica, breve, fácil de responder en 5 segundos
3. **Reconocimiento público** — cuando alguien comparte su experiencia, nombrarlo y responder en el grupo
4. **Sesión en vivo mensual** — 30 min de práctica grupal (Zoom o Meet), anunciada en Anuncios

### Puente WhatsApp → Skool (1 vez por semana en Anuncios)

No es venta. Es señalar que hay más disponible:

> *"Para los que quieren práctica más profunda — esta semana en Skool publiqué la sesión completa de Yoga Nidra de 20 min + el recurso de respiración avanzada. El link para unirse está en la descripción de la Community."*

---

## 4. Sistema de outreach — base de datos y envío

### Fuentes de contactos

| Fuente | Volumen estimado | Temperatura |
|--------|-----------------|-------------|
| Bootcamps Maestrías del Silicon Valley (últimos 2 meses) | ~50–100/mes | Caliente — te vieron trabajar |
| Bootcamps más antiguos (>2 meses) | Variable | Tibio |
| Maestría del Dinero Interior (MDI) | Variable | Tibio — eres docente/colaborador |
| Contactos directos / comunidad de ~150 | ~150 | Variable |

**Total inicial estimado: 300+ contactos**

### Estructura de la Google Sheet (base de datos)

Un solo archivo, una hoja, una fila por contacto:

| Columna | Qué registrar |
|---------|---------------|
| Nombre | Como aparece en WhatsApp |
| Número | Con código de país (+57, etc.) |
| Fuente | Bootcamp SV / MDI / Contacto directo |
| Bootcamp o fecha | Para priorizar los más recientes |
| Estado | Pendiente / Enviado / Respondió / Se unió / No interesado |
| Plataforma elegida | WhatsApp / Skool / Ambas / Ninguna |
| Notas | Algo recordable de esa persona (personalización mínima) |

### Cómo construir la base sin herramientas especiales

1. Abrir WhatsApp Web (web.whatsapp.com)
2. Entrar a cada grupo → clic en nombre del grupo → ver miembros
3. Por cada miembro: copiar nombre y número de teléfono (visible en el perfil)
4. Pegar en la Google Sheet
5. Agregar fuente y cualquier nota recordable

**Estimado de tiempo:** ~4–6 horas para 300 contactos. Se puede delegar a alguien con acceso a WhatsApp Web bajo supervisión.

### Prioridad de outreach

1. **Prioridad 1 — Bootcamps de los últimos 2 meses:** calor máximo, menor fricción
2. **Prioridad 2 — MDI:** son docentes/colaboradores, relación de autoridad
3. **Prioridad 3 — Bootcamps más antiguos:** requieren más contexto, mensaje levemente diferente

### Plantillas de mensaje (por segmento)

**Plantilla 1 — Bootcamp reciente (últimos 2 meses):**
> *"Hola [Nombre], qué bueno haberte tenido en el bootcamp. Estoy lanzando una comunidad de práctica — un espacio gratuito para seguir trabajando la regulación del sistema nervioso en medio de la vida que llevamos. Te quería invitar personalmente. ¿Te interesa que te pase el link?"*

**Plantilla 2 — Maestría del Dinero Interior:**
> *"Hola [Nombre], un gusto compartir el camino en la Maestría. Estoy armando una comunidad de práctica — respiración, meditación, regulación del sistema nervioso, gratuita por ahora. Se me ocurrió que podría ser valioso para ti. ¿Te cuento más?"*

**Plantilla 3 — Bootcamp antiguo / contacto más frío:**
> *"Hola [Nombre], hace tiempo que no hablamos. Estoy lanzando un espacio de práctica semanal — calma real en medio de una vida exigente. Totalmente gratuito para empezar. ¿Te interesa?"*

**Nota de personalización:** Si recuerdas algo específico de la persona (lo que compartió en el bootcamp, su trabajo, algo personal), agregarlo en una línea antes de la invitación. Convierte 3–5 veces más que el mensaje genérico.

### Cadencia de envío (para no ser marcado como spam)

- Máximo **30–40 mensajes por día** desde WhatsApp personal
- Enviar en dos bloques: mañana (9–11am) y tarde (5–7pm)
- No enviar todos en el mismo momento — espaciar al menos 30–60 segundos entre cada uno
- Responder a cada respuesta que llegue antes de continuar con el bloque siguiente
- **Meta:** cubrir los 300 contactos en 10–15 días

### Seguimiento

Quien no responde al cabo de 5 días: un segundo mensaje breve y único:

> *"[Nombre], te mandé esto hace unos días — ¿te llegó bien?"*

Quien dice que no está interesado: marcar como "No interesado" en la Sheet y no volver a escribir. Sin presión.

---

## 5. Automatización futura — WhatsApp Business Cloud API

Para el lanzamiento inicial, el outreach es semi-manual (Tincho envía personalmente). Una vez validado el canal, en 60–90 días se puede montar automatización para bootcamps futuros:

**Stack técnico para la automatización:**
- WhatsApp Business Cloud API vía 360dialog (~$7/mes) o Twilio
- Make.com (automatización) — ~$9/mes plan básico
- Google Sheets como base de datos de contactos
- Anthropic API (Claude) para personalizar el mensaje con el nombre y fuente

**Flujo automatizado:**
```
Bootcamp termina (día 0)
         ↓
Make detecta nueva fila en Google Sheet (contacto nuevo del evento)
         ↓
Espera 48 horas (enfriamiento natural)
         ↓
Claude genera mensaje personalizado con nombre + contexto del bootcamp
         ↓
WhatsApp Business API envía el mensaje (plantilla aprobada por Meta)
         ↓
Si responde: continúa conversación libre (24h window)
```

**Restricción importante de Meta:** Para el primer contacto, el mensaje debe seguir una plantilla aprobada por Meta (proceso de aprobación: 24–72 horas). El texto libre está disponible solo en respuestas dentro de las 24 horas posteriores a que el contacto te escriba.

**Cuándo montar esto:** Cuando el outreach manual haya validado los mensajes que mejor convierten y haya al menos 1 bootcamp mensual regular como pipeline.

---

## 6. Métricas de éxito — primeros 30 días

| Métrica | Objetivo | Señal de alerta |
|---------|----------|-----------------|
| Contactos enviados | 300 en 15 días | < 100 en 15 días |
| Tasa de respuesta | > 40% | < 20% |
| Tasa de unión a Community | > 25% de respondidos | < 10% |
| Miembros activos en Community (semana 4) | > 50 | < 20 |
| Miembros que también se unen a Skool | > 15% de la Community | < 5% |

---

## 7. Fases de implementación

### Fase 1 — Semana 1–2: Infraestructura y base de datos
- [ ] Crear WhatsApp Community "Oasis de Calma — Tincho"
- [ ] Crear grupo "Práctica Diaria" dentro de la Community
- [ ] Crear grupo "Anuncios" dentro de la Community
- [ ] Armar Google Sheet con columnas definidas en §4
- [ ] Construir base de datos de contactos desde grupos de WhatsApp Web
- [ ] Priorizar lista: Prioridad 1 → Prioridad 2 → Prioridad 3

### Fase 2 — Semana 2–4: Outreach
- [ ] Iniciar envío de mensajes: 30–40 por día, bloques de mañana y tarde
- [ ] Actualizar estado en la Sheet por cada contacto (Enviado / Respondió / Se unió)
- [ ] Seguimiento a los que no respondieron (día 5)
- [ ] Responder cada conversación personalmente

### Fase 3 — Semana 3 en adelante: Contenido activo
- [ ] Publicar primera pieza en Práctica Diaria (lunes)
- [ ] Seguir la rotación semanal definida en §3
- [ ] Publicar en Anuncios: 1 mención de Skool por semana
- [ ] Primer live mensual (semana 4 o 5)

### Fase 4 — Mes 2–3: Evaluación y automatización
- [ ] Revisar métricas del §6
- [ ] Agregar grupos de Recursos y Preguntas si hay >100 miembros activos
- [ ] Evaluar montar WhatsApp Business Cloud API para bootcamps futuros
- [ ] Cruzar datos: ¿qué mensajes de outreach tuvieron mayor tasa de respuesta?

---

## 8. Lo que NO es este canal

- ❌ No reemplaza a Skool — son propósitos distintos
- ❌ No es un canal de ventas directas — el vínculo se construye antes de ofrecer
- ❌ No es un grupo abierto — las personas entran por invitación personal o link directo
- ❌ No requiere producción — la voz real de Tincho sin edición es el activo