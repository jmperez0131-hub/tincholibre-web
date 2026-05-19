# WhatsApp Community Launch — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Lanzar la WhatsApp Community "Oasis de Calma" e invitar a 300+ contactos de bootcamps y MDI en 15 días.

**Architecture:** Dos fases en paralelo — infraestructura (Community + Google Sheet) y outreach (envío por prioridad: bootcamps recientes → MDI → más antiguos). El contenido semanal arranca en la semana 3, cuando ya hay masa crítica de miembros.

**Tech Stack:** WhatsApp (Community feature), WhatsApp Web (extracción de contactos), Google Sheets (base de datos), archivos de referencia en `contenido/comunidad/`.

**Spec:** `contenido/docs/superpowers/specs/2026-05-19-whatsapp-community-outreach-design.md`  
**Archivos de apoyo:** `contenido/comunidad/outreach-mensajes.md` · `contenido/comunidad/semana1-contenido.md`

---

## Task 1: Crear la WhatsApp Community

**Tiempo estimado:** 20–30 minutos  
**Prerequisito:** Ninguno — hacerlo en el teléfono, día 1

**Archivos de referencia:**
- Leer: `contenido/comunidad/outreach-mensajes.md` (para tener el link listo cuando lo pida la app)

- [ ] **Paso 1.1: Crear la Community en WhatsApp**

  En el teléfono: WhatsApp → ícono de comunidades (dos personas) → "Nueva comunidad"
  
  Completar:
  - Nombre: `Oasis de Calma — Tincho`
  - Descripción: `Práctica semanal de regulación del sistema nervioso. Respiración, meditación, calma funcional en medio de la vida que llevamos. Gratuito.`
  - Foto: foto tuya de perfil o logo de tincholibre.com

- [ ] **Paso 1.2: Crear el grupo "Práctica Diaria"**

  Dentro de la Community: "Agregar grupo" → crear nuevo
  
  - Nombre: `🌬️ Práctica Diaria`
  - Descripción: `Práctica de lunes a viernes — audios, respiración, reflexiones. Todos participan.`
  - Permisos: todos pueden enviar mensajes

- [ ] **Paso 1.3: Crear el grupo "Anuncios"**

  Dentro de la Community: "Agregar grupo" → crear nuevo
  
  - Nombre: `📢 Anuncios`
  - Descripción: `Novedades, sesiones en vivo, links a recursos. Solo Tincho escribe.`
  - Permisos: solo admins pueden enviar mensajes (esto se configura en Ajustes del grupo → Enviar mensajes → Solo admins)

- [ ] **Paso 1.4: Publicar primer mensaje en Práctica Diaria**

  Copiar exactamente:
  
  > Bienvenidos al Oasis. Este es el espacio donde practicamos regulación del sistema nervioso — no como concepto, sino como hábito. De lunes a viernes: audios, respiración, reflexiones. Breve. Accionable. Sin rituales complicados.
  >
  > Para empezar: ¿Qué te trajo hasta acá? Una línea.

- [ ] **Paso 1.5: Copiar el link de invitación de la Community**

  En la Community → ícono de info → "Link de invitación" → copiar
  
  Pegar ese link en `contenido/comunidad/outreach-mensajes.md` donde dice `[LINK_COMMUNITY_WHATSAPP]`.
  
  También pegar el link de la Community en la descripción de la Community si es posible.

- [ ] **Paso 1.6: Commit**

  ```bash
  git add contenido/comunidad/outreach-mensajes.md
  git commit -m "feat: link de WhatsApp Community cargado en guía de outreach"
  ```

---

## Task 2: Crear la Google Sheet de contactos

**Tiempo estimado:** 15 minutos  
**Prerequisito:** Task 1 completada (para tener el link listo)

- [ ] **Paso 2.1: Crear la hoja en Google Sheets**

  Ir a sheets.google.com → "+" nuevo archivo
  
  Renombrar: `Oasis — Base de Contactos`

- [ ] **Paso 2.2: Crear los encabezados exactos (fila 1)**

  En la fila 1, una columna por celda en este orden:

  | A | B | C | D | E | F | G |
  |---|---|---|---|---|---|---|
  | Nombre | Número | Fuente | Fecha/Bootcamp | Estado | Plataforma | Notas |

  - Columna A: nombre como aparece en WhatsApp
  - Columna B: número con código de país (ej: +573001234567)
  - Columna C: `Bootcamp SV` / `MDI` / `Contacto directo`
  - Columna D: mes del bootcamp o fecha del último contacto
  - Columna E: `Pendiente` / `Enviado` / `Respondió` / `Se unió` / `No interesado`
  - Columna F: `WhatsApp` / `Skool` / `Ambas` / `Ninguna`
  - Columna G: algo recordable de esa persona para personalizar el mensaje

- [ ] **Paso 2.3: Aplicar formato básico**

  - Congelar fila 1 (Ver → Inmovilizar → 1 fila)
  - Colorear fila 1 con fondo gris claro
  - Columna E: aplicar validación de datos con la lista de estados (clic derecho → Validación de datos → lista de elementos: `Pendiente, Enviado, Respondió, Se unió, No interesado`)

- [ ] **Paso 2.4: Crear una segunda hoja llamada "Métricas"**

  En la pestaña inferior, agregar segunda hoja: "Métricas"
  
  Agregar estas celdas de seguimiento:

  | Fila | Columna A | Columna B |
  |------|-----------|-----------|
  | 1 | Total contactos | `=COUNTA(Contactos!A2:A1000)-1` |
  | 2 | Enviados | `=COUNTIF(Contactos!E:E,"Enviado")+COUNTIF(Contactos!E:E,"Respondió")+COUNTIF(Contactos!E:E,"Se unió")` |
  | 3 | Respondieron | `=COUNTIF(Contactos!E:E,"Respondió")+COUNTIF(Contactos!E:E,"Se unió")` |
  | 4 | Se unieron | `=COUNTIF(Contactos!E:E,"Se unió")` |
  | 5 | Tasa de respuesta | `=B3/B2` (formatear como porcentaje) |
  | 6 | Tasa de unión | `=B4/B3` (formatear como porcentaje) |

  Renombrar la hoja de contactos (pestaña) como "Contactos".

---

## Task 3: Construir la base de datos — grupos de bootcamps

**Tiempo estimado:** 2–3 horas (distribuir en 2 días)  
**Prerequisito:** Task 2 completada (Sheet lista)  
**Herramienta:** WhatsApp Web en la computadora (web.whatsapp.com)

- [ ] **Paso 3.1: Abrir WhatsApp Web**

  Ir a web.whatsapp.com → escanear QR con el teléfono → confirmar sesión

- [ ] **Paso 3.2: Acceder al primer grupo de bootcamp (Maestrías del Silicon Valley)**

  En la barra lateral: buscar el grupo → clic en el nombre del grupo (arriba) → "Ver miembros"
  
  Se abre la lista de participantes.

- [ ] **Paso 3.3: Por cada miembro, copiar a la Sheet**

  Para cada persona en la lista:
  1. Clic en el nombre → se abre el perfil
  2. Copiar: nombre + número de teléfono (aparece debajo del nombre)
  3. Pegar en la Sheet: nombre en columna A, número en B
  4. Columna C: `Bootcamp SV`
  5. Columna D: mes del bootcamp (ej: `mayo 2026`)
  6. Columna E: `Pendiente`
  7. Columna G: cualquier cosa recordable (opcional pero poderoso)
  
  Repetir por cada miembro del grupo.

- [ ] **Paso 3.4: Repetir con cada grupo de bootcamp restante**

  Un grupo por vez. Marcar en la Sheet si alguien ya aparece de un grupo anterior (no duplicar — actualizar el registro existente agregando la fuente en notas).

- [ ] **Paso 3.5: Commit del progreso**

  La Sheet vive en Google Drive, no en git. Pero documentar el avance:
  
  ```bash
  git commit --allow-empty -m "progress: base de datos bootcamps SV completada ([N] contactos)"
  ```
  
  Reemplazar `[N]` con el número real de contactos agregados.

---

## Task 4: Construir la base de datos — grupo MDI

**Tiempo estimado:** 1 hora  
**Prerequisito:** Task 3 completada o en paralelo (misma metodología)

- [ ] **Paso 4.1: Acceder al grupo de MDI en WhatsApp Web**

  Misma metodología que Task 3.
  
  Columna C: `MDI`  
  Columna D: dejar en blanco o poner el nombre del programa

- [ ] **Paso 4.2: Llenar la Sheet con todos los miembros**

  Mismo proceso: nombre, número, fuente=MDI, estado=Pendiente.

- [ ] **Paso 4.3: Commit**

  ```bash
  git commit --allow-empty -m "progress: base de datos MDI completada ([N] contactos)"
  ```

---

## Task 5: Outreach — Prioridad 1 (bootcamps últimos 2 meses)

**Tiempo estimado:** 3–5 días (30–40 mensajes/día)  
**Prerequisito:** Tasks 3 y 4 completadas. Task 1 completada (link de Community listo)  
**Archivo de referencia:** `contenido/comunidad/outreach-mensajes.md`

- [ ] **Paso 5.1: Filtrar en la Sheet los contactos de Prioridad 1**

  En la Sheet: Datos → Crear filtro → Columna D: mostrar solo bootcamps de los últimos 2 meses → Columna E: mostrar solo "Pendiente"
  
  Ordenar por fecha de bootcamp más reciente primero.

- [ ] **Paso 5.2: Bloque de mañana (9–11am, máximo 20 mensajes)**

  Por cada contacto en la lista filtrada:
  
  1. Abrir WhatsApp → buscar el nombre
  2. Si tienes una nota en columna G, agregar una línea personal antes del mensaje
  3. Copiar la Plantilla 1 de `contenido/comunidad/outreach-mensajes.md`
  4. Reemplazar `[Nombre]` con el nombre real
  5. Enviar
  6. Actualizar columna E a `Enviado` en la Sheet
  7. Esperar 30–60 segundos antes del siguiente

- [ ] **Paso 5.3: Bloque de tarde (5–7pm, máximo 20 mensajes)**

  Mismo proceso que el bloque de mañana.
  
  Antes de empezar: responder todos los mensajes que llegaron desde el bloque de mañana.

- [ ] **Paso 5.4: Por cada respuesta positiva**

  1. Actualizar columna E a `Respondió`
  2. Copiar el "Mensaje de envío del link" de `contenido/comunidad/outreach-mensajes.md`
  3. Enviar el link de la Community
  4. Si acepta: actualizar columna E a `Se unió`
  5. Si pregunta por Skool: enviar también el link de El Oasis

- [ ] **Paso 5.5: Día 5 — seguimiento a los que no respondieron**

  Filtrar en la Sheet: Columna E = "Enviado" Y Columna D = bootcamp hace 5+ días
  
  Enviar el mensaje de seguimiento de `outreach-mensajes.md`:
  
  > [Nombre], te mandé esto hace unos días — ¿te llegó bien?

- [ ] **Paso 5.6: Actualizar métricas (cada 2 días)**

  Revisar la hoja "Métricas" para ver tasa de respuesta y tasa de unión en tiempo real.
  
  Objetivo a mitad del outreach P1: tasa de respuesta > 35%.

---

## Task 6: Outreach — Prioridad 2 y 3 (MDI + bootcamps antiguos)

**Tiempo estimado:** 5–7 días (misma cadencia)  
**Prerequisito:** Task 5 en curso o completada  
**Archivo de referencia:** `contenido/comunidad/outreach-mensajes.md`

- [ ] **Paso 6.1: Filtrar contactos de Prioridad 2 (MDI)**

  Columna C = "MDI" Y Columna E = "Pendiente"
  
  Usar Plantilla 2.

- [ ] **Paso 6.2: Ejecutar outreach MDI**

  Mismo proceso que Task 5 — bloques mañana y tarde, 30–40/día, seguimiento día 5.

- [ ] **Paso 6.3: Filtrar contactos de Prioridad 3 (bootcamps antiguos)**

  Columna C = "Bootcamp SV" Y Columna D = bootcamps de más de 2 meses Y Columna E = "Pendiente"
  
  Usar Plantilla 3.

- [ ] **Paso 6.4: Ejecutar outreach bootcamps antiguos**

  Mismo proceso. La tasa de respuesta esperada aquí es menor (~20–30%) — es normal.

- [ ] **Paso 6.5: Revisar métricas finales del outreach**

  En la hoja "Métricas": verificar que se cumplan los objetivos del spec:
  
  | Métrica | Objetivo | ¿Cumplido? |
  |---------|----------|-----------|
  | Contactos enviados | 300 en 15 días | |
  | Tasa de respuesta | > 40% | |
  | Tasa de unión a Community | > 25% de respondidos | |

---

## Task 7: Activar contenido semanal en Práctica Diaria

**Tiempo estimado:** 30–45 min/semana de preparación  
**Cuándo:** Semana 3 del lanzamiento (cuando haya al menos 30 miembros)  
**Archivo de referencia:** `contenido/comunidad/semana1-contenido.md`

- [ ] **Paso 7.1: Usar el contenido de semana 1 ya preparado**

  Abrir `contenido/comunidad/semana1-contenido.md`
  
  - Lunes: grabar audio de 60–90 seg con el texto del lunes → publicar en Práctica Diaria
  - Martes: copiar el texto exacto del martes → publicar
  - Miércoles: grabar audio de 3–5 min con la práctica 4-7-8 → publicar
  - Jueves: copiar el texto del jueves → publicar
  - Viernes: copiar el texto del viernes (+ audio opcional) → publicar
  - Miércoles/Jueves: publicar mensaje de Anuncios con link a Skool

- [ ] **Paso 7.2: Responder las participaciones**

  Por cada persona que responda a la pregunta del martes o al check-in del domingo:
  - Responder con nombre propio
  - Máximo 1–2 líneas
  - Sin consejo ni corrección — solo reconocimiento

- [ ] **Paso 7.3: Preparar contenido semana 2 (domingo anterior)**

  Copiar la estructura de `semana1-contenido.md` y adaptar para la semana 2.
  
  Criterio: rotar la práctica del miércoles (semana 1 fue 4-7-8 → semana 2 puede ser box breathing o respiración diafragmática).

- [ ] **Paso 7.4: Actualizar el archivo de contenido**

  Crear `contenido/comunidad/semana2-contenido.md` con el mismo formato.
  
  ```bash
  git add contenido/comunidad/semana2-contenido.md
  git commit -m "feat: contenido semana 2 WhatsApp Community"
  ```

---

## Task 8: Puente WhatsApp → Skool (semanal, continuo)

**Tiempo estimado:** 5 minutos por semana  
**Cuándo:** Cada miércoles o jueves, en el grupo de Anuncios  
**Prerequisito:** Skool El Oasis configurado (ver plan `2026-04-25-skool-community-setup.md`)

- [ ] **Paso 8.1: Obtener el link de Skool**

  Entrar a skool.com → tu comunidad El Oasis → copiar el link de invitación.
  
  Pegar en `contenido/comunidad/outreach-mensajes.md` donde dice `[LINK_SKOOL]`.

- [ ] **Paso 8.2: Publicar en Anuncios cada semana**

  Copiar del archivo `semana1-contenido.md` (sección "Mensaje de Anuncios") y adaptar mencionando el contenido específico que hay en Skool esa semana.
  
  Ejemplo real:
  
  > Para los que quieren práctica más profunda — esta semana en Skool publiqué el audio de Yoga Nidra de 20 minutos (el estado entre dormir y despertar donde el sistema nervioso se reprograma). Gratuito para entrar. [LINK_SKOOL]

- [ ] **Paso 8.3: Commit del link actualizado**

  ```bash
  git add contenido/comunidad/outreach-mensajes.md
  git commit -m "feat: link de Skool cargado en guía de outreach y contenido semana 1"
  ```

---

## Task 9: Evaluación día 30

**Tiempo estimado:** 30 minutos  
**Cuándo:** Al terminar el mes 1

- [ ] **Paso 9.1: Revisar métricas en la Sheet**

  Abrir hoja "Métricas" y documentar los resultados reales:

  | Métrica | Objetivo | Real |
  |---------|----------|------|
  | Miembros en Community | > 75 | |
  | Miembros activos (participan) | > 50 | |
  | Miembros que también entraron a Skool | > 15% de la Community | |

- [ ] **Paso 9.2: Decidir próximos grupos de la Community**

  Si hay > 100 miembros activos: crear grupos adicionales
  - `📖 Recursos y Herramientas`
  - `💬 Preguntas y Compartir`
  
  Si hay < 50 miembros activos: revisar plantillas de outreach y probar variaciones antes de abrir más grupos.

- [ ] **Paso 9.3: Evaluar primer live mensual**

  Programar la primera sesión en vivo (30 min, Zoom o Google Meet):
  - Anunciar en el grupo de Anuncios con 5 días de anticipación
  - Formato: práctica guiada en vivo + 10 min de preguntas
  - Grabar y subir el replay a Skool

- [ ] **Paso 9.4: Commit de métricas documentadas**

  ```bash
  git commit --allow-empty -m "progress: evaluación día 30 — [N] miembros Community, [N] en Skool"
  ```

---

## Cronograma resumen

| Días | Tarea |
|------|-------|
| Día 1 | Task 1: Crear Community + grupos + primer mensaje |
| Día 1–2 | Task 2: Crear Google Sheet |
| Días 2–5 | Task 3 + 4: Construir base de datos (grupos WhatsApp Web) |
| Días 3–8 | Task 5: Outreach Prioridad 1 (bootcamps recientes) |
| Días 8–15 | Task 6: Outreach Prioridad 2 y 3 (MDI + antiguos) |
| Día 15+ | Task 7: Activar contenido semanal |
| Cada semana | Task 8: Publicar puente a Skool en Anuncios |
| Día 30 | Task 9: Evaluación y decisiones de siguiente fase |