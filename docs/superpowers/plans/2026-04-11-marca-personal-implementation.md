# Marca Personal @tincholibre — Plan de Implementación

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Lanzar la infraestructura completa de la marca personal de @tincholibre — desde la base técnica hasta la primera venta pública y la comunidad en Skool — siguiendo la secuencia de dos carriles (Público + Comunidad) definida en el spec.

**Architecture:** Carril Público: tincholibre.com (Netlify) + ManyChat (lead capture) + Kit/ConvertKit (email) + Hotmart (ventas). Carril Comunidad: outreach directo a contactos cálidos y participantes de bootcamps + Skool. Los bloques 0 y 1 son prerequisitos. Los bloques 2 y 3 corren en paralelo. El bloque 4 depende de que el bloque 1 esté completo.

**Tech Stack:** Netlify · Kit (ConvertKit) · ManyChat · Hotmart · Skool · Beacons.ai · Alegra · Canva · tincholibre.com

> **Nota de alcance:** Este plan cubre Fases 0, 1 y 2 del spec (Semanas 1–8 aproximadamente). Las Fases 3–5 (PMR → Core + Premium → Skool formal) se planifican por separado una vez que la Fase 2 esté validada con compradores reales.

---

## BLOQUE 0: Blockers pre-lanzamiento
*Completar antes de cualquier otra tarea. Sin esto no se puede vender.*

---

### Tarea 1: Conectar tincholibre.com a Netlify

**Archivos:**
- Modificar: `index.html` (sin cambios de código — solo deploy)
- Nueva URL de producción: `https://tincholibre.com`

**Prerequisito:** tincholibre.com comprado en Namecheap ✓

- [ ] **Paso 1: Crear cuenta en Netlify**

  Ir a https://app.netlify.com → "Sign up" → usar cuenta de Google o email.

- [ ] **Paso 2: Hacer el deploy inicial**

  En el dashboard de Netlify:
  1. Buscar la sección "Import from Git" o el área de drag & drop
  2. Seleccionar "Deploy manually"
  3. Arrastrar la carpeta `Marca Personal` (la que contiene `index.html`) al área de deploy
  4. Netlify genera una URL temporal: `https://algo-random.netlify.app`
  5. Abrir esa URL en el navegador y verificar que la landing page se ve correctamente

- [ ] **Paso 3: Agregar el dominio personalizado en Netlify**

  En tu sitio de Netlify:
  1. Ir a **Site settings → Domain management → Add a domain**
  2. Ingresar: `tincholibre.com` → confirmar
  3. Netlify muestra una pantalla con sus **4 nameservers** — copiarlos (son del estilo `dns1.p01.nsone.net`, `dns2.p01.nsone.net`, etc.)

- [ ] **Paso 4: Apuntar el dominio en Namecheap**

  1. Ir a namecheap.com → **Domain List → Manage** (botón al lado de tincholibre.com)
  2. Tab **Nameservers**
  3. Cambiar el dropdown de "Namecheap BasicDNS" a **"Custom DNS"**
  4. Pegar los 4 nameservers que te dio Netlify en los campos correspondientes
  5. Guardar cambios

- [ ] **Paso 5: Esperar propagación DNS y verificar SSL**

  La propagación tarda entre 1 y 24 horas. Netlify activa HTTPS automáticamente.
  - Verificar: abrir `https://tincholibre.com` en el navegador
  - Debe cargar la landing con candado verde (HTTPS)
  - Si no carga después de 24 horas: ir a Netlify → Domain management → verificar que el dominio esté "Netlify DNS"

- [ ] **Paso 6: Commit del estado del proyecto**

  ```bash
  cd "c:/Users/JMP/.claude/projects/Marca Personal"
  git add -A
  git commit -m "deploy: landing page live en tincholibre.com"
  ```

---

### Tarea 2: Configurar Alegra (facturación electrónica)

**Prerequisito:** Tener RUT colombiano y NIT del negocio activo.

- [ ] **Paso 1: Crear cuenta en Alegra**

  Ir a https://alegra.com/colombia → "Prueba gratis 15 días" → completar registro con nombre, email y contraseña.

  > **Costo post-prueba:** el plan básico de Alegra cuesta aproximadamente $30.000–50.000 COP/mes. La prueba de 15 días es suficiente para hacer la configuración inicial y emitir las primeras facturas reales. Después de la prueba, evaluar activar el plan pago antes de la primera venta pública.

- [ ] **Paso 2: Configurar datos de la empresa**

  En el dashboard:
  1. Ir a **Configuración → Empresa**
  2. Completar:
     - **Nombre de la empresa / Nombre comercial:** Tincho [apellido] (o el nombre bajo el que estés registrado)
     - **NIT / Cédula:** tu número de identificación tributaria
     - **Dirección:** dirección fiscal
     - **Régimen tributario:** seleccionar el que corresponde (si sos persona natural no responsable de IVA: "No responsable de IVA / Régimen simple")
     - **Actividad económica:** buscar "otras actividades de entretenimiento y recreación" o "actividades de bienestar físico"
  3. Guardar

- [ ] **Paso 3: Configurar la numeración de facturas electrónicas**

  1. Ir a **Configuración → Numeraciones**
  2. Crear una nueva numeración para "Factura de venta electrónica"
  3. Alegra te guía para conectar con la DIAN (requiere firma electrónica — sigue el asistente paso a paso)
  4. La DIAN asigna un rango de numeración autorizado — esto puede tomar 1-3 días hábiles

- [ ] **Paso 4: Emitir una factura de prueba**

  Una vez que la DIAN aprueba el rango:
  1. **Ventas → Nueva factura**
  2. Crear una factura de prueba a tu propio nombre por $1.000 COP
  3. Enviar por email (te la mandás a vos mismo)
  4. Verificar que llegue con el archivo XML adjunto (eso confirma que la transmisión a la DIAN funciona)

- [ ] **Paso 5: Crear plantilla de producto para las ventas digitales**

  1. Ir a **Inventario → Productos y servicios → Nuevo**
  2. Crear:
     - "Guía de Meditación para Principiantes" — precio $17 USD (o el equivalente en COP al momento)
     - Tipo: Servicio / Producto digital
  3. Repetir para "Protocolo 3 Respiraciones" (precio: $0 / regalo)
  4. Estos productos se usarán cada vez que se emita una factura

---

## BLOQUE 1: Infraestructura digital
*Completar en Semanas 1–4. Las tareas 3–7 son independientes entre sí — se pueden hacer en cualquier orden.*

---

### Tarea 3: Kit (ConvertKit) — cuenta + secuencia de bienvenida

- [ ] **Paso 1: Crear cuenta gratuita en Kit**

  Ir a https://kit.com → "Start for free" → registrarse con email.
  Plan gratuito: hasta 10.000 suscriptores, 1 automatización.

- [ ] **Paso 2: Crear el formulario de captura**

  1. En el dashboard: **Grow → Landing Pages & Forms → Create New → Form**
  2. Elegir un estilo simple (Inline o Modal)
  3. Campos: solo "Email" (sin nombre — menos fricción)
  4. Título del formulario: `"Descargá el Protocolo 3 Respiraciones"`
  5. Botón: `"Quiero el protocolo"`
  6. Guardar → copiar el código embed (lo vas a necesitar para el landing page)

- [ ] **Paso 3: Configurar la secuencia de bienvenida**

  1. Ir a **Automate → Sequences → New Sequence**
  2. Nombrar: "Bienvenida — Protocolo 3 Respiraciones"
  3. Email 1 — Entrega del lead magnet (se envía inmediatamente):

     **Asunto:** `Tu Protocolo 3 Respiraciones`

     **Cuerpo:**
     ```
     Acá lo tenés: [LINK DE DESCARGA DEL PDF]

     Son tres minutos antes de dormir.
     La primera vez que lo uses, tu cuerpo va a notar algo diferente.
     Eso no es sugestión — es el sistema nervioso recibiendo una señal que no
     recibía.

     Cualquier pregunta, respondé este email.

     — Tincho

     P.D. Si querés seguir este proceso en profundidad, estoy en Instagram
     @tincholibre.
     ```

  4. Email 2 — Valor (se envía al Día 3):

     **Asunto:** `El error que comete el 90% cuando intenta meditar`

     **Cuerpo:**
     ```
     La mayoría empieza a meditar esperando que la mente se quede quieta.

     Eso no es meditación. Es frustración programada.

     La mente no se aquieta por fuerza de voluntad.
     Se aquieta cuando el sistema nervioso deja de percibir amenaza.

     La diferencia entre "meditar" y regular el sistema nervioso:
     una depende de tu disciplina, la otra depende de biología.

     Si el protocolo que descargaste funcionó aunque sea un poco,
     es porque tocó el mecanismo correcto.

     La semana que viene te cuento el segundo paso.

     — Tincho
     ```

  5. Email 3 — Soft offer (se envía al Día 6):

     **Asunto:** `Por qué la calma no dura`

     **Cuerpo:**
     ```
     Mucha gente tiene un momento de calma — y al día siguiente el ruido vuelve igual.

     No es porque el método falló.
     Es porque la regulación necesita repetición para convertirse en hábito del sistema nervioso.

     El protocolo de respiraciones que tenés es el primer paso.
     La Guía de Meditación es el sistema completo: 7 prácticas progresivas que van construyendo esa capacidad de a poco.

     Si querés el sistema entero: [LINK A HOTMART / PÁGINA DE VENTA]

     — Tincho
     ```

  6. Guardar la secuencia → activarla

- [ ] **Paso 4: Conectar el formulario con la secuencia**

  1. Ir al formulario creado en el Paso 2
  2. En la configuración del formulario: **Incentive → Add an incentive**
  3. Seleccionar "Automation" → conectar con la secuencia "Bienvenida — Protocolo 3 Respiraciones"
  4. Verificar: suscribirse con un email propio y confirmar que llega el Email 1

---

### Tarea 4: ManyChat — automatización Instagram DM

- [ ] **Paso 1: Crear cuenta en ManyChat**

  Ir a https://manychat.com → "Get Started Free" → conectar con la cuenta de Instagram de @tincholibre.
  Debe estar conectada a una Página de Facebook (requisito de Meta para Instagram DM automation).

- [ ] **Paso 2: Crear el primer flujo — entrega del lead magnet**

  1. En el dashboard: **Flows → New Flow**
  2. Nombrar: "Entrega Protocolo — CALMA"
  3. Crear el flujo:

     **Trigger:** Comment keyword → palabra clave: `CALMA` (configurar para que funcione en cualquier post)

     **Mensaje automático de respuesta al comentario** (público, visible para todos):
     ```
     ¡Te lo mando por DM ahora mismo!
     ```

     **DM automático** (privado, se envía al que comentó):
     ```
     Hola [FIRST NAME] 👋

     Acá está tu Protocolo 3 Respiraciones:
     👉 [LINK DE DESCARGA DEL PDF]

     Son tres minutos antes de dormir. La primera vez que lo uses,
     tu cuerpo va a notar algo distinto.

     ¿Querés que te lo mande también por email para tenerlo guardado?
     ```

     **Botones de respuesta rápida:**
     - `Sí, mandamelo por email`
     - `No, gracias`

     **Si elige "Sí":**
     ```
     ¿Cuál es tu email?
     ```
     → Capturar email → agregar al tag "Lead Magnet" en ManyChat → enviar a Kit via webhook (ver Paso 3)

     **Si elige "No":**
     ```
     Perfecto. Cualquier pregunta sobre el protocolo, respondé acá.
     Seguime en @tincholibre para más sobre regulación del sistema nervioso.
     ```

  4. Activar el flujo

- [ ] **Paso 3: Conectar ManyChat con Kit (webhook)**

  1. En Kit: **Settings → Integrations → API** → copiar API key
  2. En ManyChat: en el paso de captura de email → **Action → Subscribe to Email Service → Kit**
  3. Conectar con la API key → seleccionar la secuencia "Bienvenida — Protocolo 3 Respiraciones"
  4. Verificar: comentar "CALMA" en un post de prueba desde otra cuenta → confirmar que llega el DM

- [ ] **Paso 4: Configurar el flujo para el lanzamiento**

  El flujo se activa solo cuando subís un post con el CTA correspondiente. No hace falta activarlo para todos los posts — solo para los que digan "Comentá CALMA".

---

### Tarea 5: Hotmart — cuenta + Guía de Meditación

- [ ] **Paso 1: Crear cuenta en Hotmart como productor**

  Ir a https://hotmart.com → "Crear cuenta" → seleccionar "Productor / Creador de contenido" → completar datos personales y bancarios colombianos.

  Documentación requerida: cédula de identidad, datos bancarios para recibir pagos.

- [ ] **Paso 2: Crear el producto "Guía de Meditación para Principiantes"**

  En el panel de Hotmart:
  1. **Productos → Nuevo producto**
  2. Tipo: **Ebook / Material**
  3. Nombre: `Guía de Meditación para Principiantes`
  4. Precio: en fase 1 (ventas directas/calientes) = precio a definir. Para venta pública en Fase 2 = $17–27 USD. Dejar en borrador por ahora.
  5. Subir el PDF de la guía (el archivo ya existe: `Guia de meditación - Tincho (5).pdf`)
  6. Descripción del producto (para la página de Hotmart):

     ```
     Siete prácticas progresivas para empezar a meditar cuando la mente no para.

     No es meditación clásica. No es "ponete en blanco".
     Es un sistema que funciona para quien tiene la cabeza llena y no sabe cómo empezar.

     Lo que vas a aprender:
     • Por qué la meditación tradicional falla (y qué hacer en cambio)
     • Las 7 prácticas ordenadas de menor a mayor profundidad
     • Cómo sostenerlo cuando no tenés tiempo ni ganas

     Para quienes ya probaron aplicaciones, cursos y "momentos de paz" — y el ruido interno sigue igual.
     ```

  7. Guardar en borrador (no publicar todavía — se activa en la Tarea 14)

- [ ] **Paso 3: Verificar la configuración de pago**

  Hotmart gestiona el cobro automáticamente. Solo verificar:
  - Cuenta bancaria conectada correctamente
  - Datos fiscales (NIT) ingresados para la facturación

---

### Tarea 6: Skool — comunidad en modo gratuito

- [ ] **Paso 1: Crear cuenta y comunidad en Skool**

  Ir a https://skool.com → "Create a community" → plan Hobby ($9 USD/mes).

  Datos para la creación:
  - **Nombre de la comunidad:** `Sistema Nervioso con Tincho` (o la variante que te resuene — alternativas: "Oasis con Tincho", "Regulación con Tincho")
  - **Handle:** `@tincholibre` o similar
  - **Descripción corta:** `Práctica de regulación del sistema nervioso para profesionales que viven acelerados.`

- [ ] **Paso 2: Configurar el modo gratuito**

  En la configuración de la comunidad:
  1. **Access → Free** (sin cobro, para la fase de onboarding inicial)
  2. Esto se cambia a pago en la Tarea 16

- [ ] **Paso 3: Configurar las categorías (canales)**

  Crear las siguientes categorías:
  1. **Bienvenida** — presentación, reglas, cómo moverse por la comunidad
  2. **Práctica diaria** — posts de práctica, recordatorios, reflexiones
  3. **Preguntas** — espacio abierto para consultas
  4. **Recursos** — donde subirás los materiales (PDF del protocolo, guías, etc.)

- [ ] **Paso 4: Post de bienvenida**

  Publicar el primer post en la categoría "Bienvenida":

  ```
  Bienvenido/a.

  Este espacio existe para una sola cosa: sostener la práctica.

  No los estados de paz que duran un día.
  La capacidad real de bajar el interruptor cuando la vida está a full.

  Cómo moverse por acá:
  📌 Bienvenida — estás acá
  🧘 Práctica diaria — acá voy a compartir lo que trabajo cada semana
  ❓ Preguntas — cualquier duda, acá
  📂 Recursos — acá van los materiales

  Si llegaste invitado/a, es porque ya compartimos un espacio juntos.
  Si llegaste desde Instagram, bienvenido al siguiente nivel.

  — Tincho
  ```

- [ ] **Paso 5: Subir la Guía de Meditación como recurso para miembros tempranos**

  1. En **Classroom → New course** o en la categoría Recursos
  2. Subir el PDF de la Guía de Meditación como regalo de bienvenida para primeros miembros
  3. Incluir nota: "Regalo para quienes se suman en esta primera etapa."

---

### Tarea 7: Beacons.ai — hub de bio

- [ ] **Paso 1: Crear cuenta en Beacons.ai**

  Ir a https://beacons.ai → "Get started free" → registrarse → handle: `tincholibre`.

- [ ] **Paso 2: Configurar el perfil**

  - Foto de perfil: la misma que Instagram
  - Nombre: `Tincho`
  - Bio: `Regulación del sistema nervioso para profesionales que viven acelerados.`
  - Estilo visual: fondo oscuro (consistente con la paleta de marca — negro/azul)

- [ ] **Paso 3: Crear los links en orden**

  Agregar en este orden (el orden importa — primero lo gratuito, luego lo pago):

  1. **"Protocolo 3 Respiraciones — Gratis"**
     - URL: link de descarga del PDF (o link al formulario de Kit)
     - Descripción: `3 minutos antes de dormir que desactivan el modo emergencia`

  2. **"Guía de Meditación"**
     - URL: link de Hotmart (agregar cuando esté publicado en Tarea 14)
     - Descripción: `El sistema completo para quien tiene la mente a full`
     - *Dejar como "próximamente" o invisible hasta la Tarea 14*

  3. **"Libertad en Jaque — el libro"**
     - URL: tincholibre.com/libro (agregar cuando esté listo en Tarea 17)
     - Descripción: `Mi historia de encarcelamiento injusto y la libertad interna que nació de ella`
     - *Dejar invisible hasta la Tarea 17*

  4. **"Maestrías del Silicon Valley"**
     - URL: link oficial del programa (el que ya tienen)
     - Descripción: `Bootcamp de emprendimiento digital — 4 días que cambian el rumbo`

  5. **"Comunidad — Sistema Nervioso con Tincho"**
     - URL: link de Skool
     - Descripción: `Práctica sostenida + sesiones en vivo`

- [ ] **Paso 4: Copiar el link de Beacons y actualizar la bio de Instagram**

  El link de Beacons reemplaza cualquier link anterior en la bio de Instagram.
  Formato: `beacons.ai/tincholibre`

---

## BLOQUE 2: Contenido
*Correr en paralelo con el Bloque 1. Semanas 1–4.*

---

### Tarea 8: Crear PDF — Protocolo 3 Respiraciones

**Herramienta recomendada:** Canva (canva.com — cuenta gratuita suficiente)

- [ ] **Paso 1: Crear el documento en Canva**

  1. En Canva: "Crear diseño" → **Presentación (16:9)** o **A4 vertical** → 4 páginas

- [ ] **Paso 2: Página 1 — Portada**

  Contenido:
  ```
  PROTOCOLO 3 RESPIRACIONES
  Tres minutos antes de dormir
  que desactivan el modo emergencia.

  por Tincho | @tincholibre
  ```
  Paleta de colores: fondo oscuro (`#0D1117`), texto claro (`#E6E6E6`), acento azul (`#00D9FF`)

- [ ] **Paso 3: Página 2 — El mecanismo**

  Contenido:
  ```
  POR QUÉ NO PODÉS APAGAR LA CABEZA

  Tu sistema nervioso no sabe que el día terminó.
  Está programado para mantenerte alerta mientras sigue
  percibiendo señales de amenaza — emails sin responder,
  conversaciones pendientes, tareas sin cerrar.

  No es falta de disciplina. Es biología.

  Estas tres respiraciones envían una señal específica
  al sistema nervioso: "ya estamos seguros."
  Eso es todo lo que necesita para empezar a soltar.
  ```

- [ ] **Paso 4: Página 3 — Las 3 respiraciones (instrucciones exactas)**

  Contenido:
  ```
  LAS 3 RESPIRACIONES

  Hacerlas en orden, en esta secuencia, acostado o sentado.
  Duración total: 3 minutos.

  ① RESPIRACIÓN DIAFRAGMÁTICA (2 min)
  Inhalar por la nariz contando hasta 4.
  Exhalar por la boca contando hasta 6.
  Repetir 8 veces.
  → El abdomen sube al inhalar. El pecho no se mueve.
  → La exhalación más larga que la inhalación activa el nervio vago.

  ② CAJA (30 seg)
  Inhalar 4 · Sostener 4 · Exhalar 4 · Sostener 4.
  Repetir 2 veces.
  → Regula el CO2 y estabiliza el sistema.

  ③ 4-7-8 (30 seg)
  Inhalar 4 · Sostener 7 · Exhalar 8.
  Repetir 2 veces.
  → La exhalación larga baja el cortisol. Es la señal de cierre.

  Terminado. Cerrá los ojos. Notá qué cambió.
  ```

- [ ] **Paso 5: Página 4 — Qué esperar + CTA**

  Contenido:
  ```
  QUÉ ESPERAR

  La primera vez: el cuerpo hace algo diferente en la tercera respiración.
  No es paz. Es el sistema soltando la guardia.

  Con práctica diaria (7 días): el proceso se vuelve más rápido,
  el cuerpo reconoce la secuencia como señal de seguridad.

  Este protocolo es el primer paso.
  El sistema completo está en la Guía de Meditación para Principiantes.

  ↓ Seguí el proceso en:
  @tincholibre (Instagram)
  tincholibre.com
  ```

- [ ] **Paso 6: Exportar y guardar**

  1. En Canva: "Compartir → Descargar → PDF estándar"
  2. Guardar como: `protocolo-3-respiraciones-tincholibre.pdf`
  3. Subir al Google Drive / Dropbox / cualquier almacenamiento → copiar el link de descarga directo
  4. Este link va en: el Email 1 de Kit (Tarea 3) y en el DM de ManyChat (Tarea 4)

- [ ] **Paso 7: Commit**

  ```bash
  git add -A
  git commit -m "content: protocolo 3 respiraciones PDF creado"
  ```

---

### Tarea 9: Grabar audio — Protocolo 3 Respiraciones

**Equipo:** Teléfono + micrófono disponible.
**Duración objetivo:** 8–12 minutos.
**Formato:** MP3 o M4A.

- [ ] **Paso 1: Preparar el guión**

  Estructura del audio (leerlo como si guiaras una sesión en vivo — calma, pausa, presencia):

  ```
  [00:00–01:00] INTRO
  "Cerrá los ojos. Encontrá una posición cómoda — acostado está bien, sentado también.
  No hay nada que resolver ahora. Solo esto.

  Vamos a hacer tres respiraciones. En ese orden.
  Al final, tu sistema nervioso va a recibir una señal que probablemente
  no recibió en todo el día: que ya estamos seguros.

  Empezamos."

  [01:00–05:00] RESPIRACIÓN 1 — DIAFRAGMÁTICA
  "Poné una mano en el abdomen. Solo para sentir.
  Cuando inhalás, el abdomen sube. El pecho queda quieto.

  Inhalar... dos... tres... cuatro. [pausa]
  Exhalar... dos... tres... cuatro... cinco... seis.

  [Repetir 7 veces más con la misma cadencia — pausas reales, no apuradas]

  Bien. Notá cómo cambió algo en el cuerpo."

  [05:00–07:00] RESPIRACIÓN 2 — CAJA
  "Ahora la caja.
  Inhalar cuatro. [pausa real de 4 segundos]
  Sostener cuatro. [pausa]
  Exhalar cuatro. [pausa]
  Sostener cuatro. [pausa]

  Una vez más.
  [Repetir]

  Bien."

  [07:00–09:30] RESPIRACIÓN 3 — 4-7-8
  "La última. Esta es la señal de cierre.

  Inhalar por la nariz, contando cuatro. [pausa]
  Sostener, contando hasta siete. [pausa larga]
  Exhalar completamente por la boca, contando hasta ocho.

  [Una vez más]

  Listo."

  [09:30–11:00] CIERRE
  "Quedate acá un momento. Sin hacer nada.

  Lo que sentís ahora — esa diferencia, por pequeña que sea —
  es el sistema nervioso recibiendo una señal que no recibía.
  No es meditación. No es relajación.
  Es biología haciendo su trabajo.

  Si querés seguir este proceso, todo lo que sigue está en @tincholibre.
  Hasta la próxima."
  ```

- [ ] **Paso 2: Grabar**

  1. Lugar tranquilo, sin eco (habitación con ropa/cortinas absorbe el sonido)
  2. Micrófono a ~20 cm de la boca
  3. Grabar en una sola toma si es posible — las imperfecciones pequeñas le dan autenticidad
  4. Nombrar el archivo: `protocolo-3-respiraciones-audio-tincholibre.mp3`

- [ ] **Paso 3: Subir a almacenamiento y generar link**

  Subir a Google Drive → compartir con "cualquiera que tenga el link" → copiar link.
  Este link va como recurso adicional en el email de bienvenida de Kit (opcional — el PDF es el principal).

---

### Tarea 10: Posts de re-entrada — Fase 0 (5–7 posts de Dolor)

*Publicar en los primeros 14 días. Sin vender todavía. Un post cada 2–3 días.*

- [ ] **Paso 1: Escribir los 7 posts en Notion (banco de contenido)**

  Crear una página en Notion: "Posts Fase 0 — Re-entrada".

  **POST 1 — Reactividad**
  ```
  Caption:
  Reaccionaste.
  Y en el momento ya sabías que no querías hacerlo.

  Pero no pudiste parar.

  Eso no es un problema de carácter.
  Es el sistema nervioso tomando el control porque percibe amenaza —
  aunque la amenaza sea un email o una pregunta incómoda.

  El interruptor existe. Solo nadie te enseñó a usarlo.

  📲 Seguime si querés aprender el mecanismo.

  Hashtags: #sistemanervioso #regulacion #bienestar #ansiedad #estres #meditacion #yoga
  ```

  **POST 2 — Aceleración sin freno**
  ```
  Caption:
  Terminás el día agotado.
  Y tu cabeza sigue.

  No es insomnio. No es ansiedad.
  Es que tu cuerpo nunca recibió la señal de que el día terminó.

  El sistema nervioso no distingue entre una emergencia real
  y una lista de pendientes sin cerrar.

  Eso tiene solución. No es fuerza de voluntad.
  Es biología.

  📲 Esta semana voy a empezar a contar el mecanismo.

  Hashtags: #descanso #sistemanervioso #estrescronico #calma #neurofisiologia
  ```

  **POST 3 — Calma falsa**
  ```
  Caption:
  Te distraés.
  Pero no descansás.

  Netflix. Redes. Algo de tomar.
  El ruido baja un rato y vuelve igual.

  No es falta de disciplina.
  Es que distracción y regulación no son lo mismo.

  Una tapa el problema. La otra lo resuelve.

  📲 La diferencia importa. Seguí leyendo esta semana.

  Hashtags: #salud mental #autocuidado #sistemanervioso #estres #mindfulness
  ```

  **POST 4 — El sueño como puerta**
  ```
  Caption:
  Son las 11 de la noche.
  Estuviste exhausto todo el día.
  Y ahora tu cabeza procesa el día entero.

  El cuerpo quiere dormir.
  El sistema nervioso sigue en modo trabajo.

  No es insomnio. No es tu culpa.
  Es que nadie le avisó que ya terminó.

  Hay una forma de darle esa señal.
  Se hace en tres minutos, antes de apagar la luz.

  ¿Querés saber cómo? Comentá CALMA y te lo mando.

  Hashtags: #sueno #insomnio #sistemanervioso #meditacion #respiracion #descanso
  ```
  *→ Este es el primer post con CTA de lead magnet. Se publica en Semana 2.*

  **POST 5 — El método (Vehículo)**
  ```
  Caption:
  Yoga no es flexibilidad.
  Es tecnología de 5.000 años para regular el sistema nervioso.

  Pranayama no es respirar bonito.
  Es cambiar el estado fisiológico del cuerpo en minutos.

  Lo espiritual y lo científico se explican mutuamente.
  Yo trabajo en esa intersección.

  📲 Esta semana: el mecanismo detrás de la práctica.

  Hashtags: #yoga #pranayama #neurociencia #sistemanervioso #bienestar
  ```

  **POST 6 — La historia (Mi Camino)**
  ```
  Caption:
  Pasé por lo más extremo que puede vivir una persona.

  Fue ahí donde entendí algo que cambió todo:
  la calma no depende del entorno.
  Depende de lo que ocurre adentro.

  Eso no es una frase bonita. Es factual.
  Y es enseñable.

  Por eso hablo de esto.

  📲 Seguime para saber cómo.

  Hashtags: #libertad #transformacion #sistemanervioso #mindset #yoga
  ```

  **POST 7 — Objeción**
  ```
  Caption:
  "Ya probé meditación y no me funciona."

  La escucho seguido.

  El problema casi siempre es el mismo:
  empezaron esperando que la mente se callara.
  La mente no se calla por fuerza de voluntad.

  Se regula cuando el sistema nervioso deja de percibir amenaza.

  Es distinto. Y funciona distinto.

  ¿Querés el protocolo con el que empiezo con todos? Comentá CALMA.

  Hashtags: #meditacion #yoga #sistemanervioso #regulacion #bienestar
  ```

- [ ] **Paso 2: Programar en Meta Business Suite**

  1. Ir a business.facebook.com → conectado a @tincholibre
  2. Programar los 7 posts con estas fechas orientativas:
     - Post 1: Día 1
     - Post 2: Día 3
     - Post 3: Día 5
     - Post 4: Día 8 (primer CTA de lead magnet)
     - Post 5: Día 10
     - Post 6: Día 12
     - Post 7: Día 14 (segundo CTA de lead magnet)
  3. Para los Posts 4 y 7: verificar que ManyChat esté activo ANTES de publicarlos

- [ ] **Paso 3: Commit del banco de contenido**

  ```bash
  git add -A
  git commit -m "content: 7 posts fase 0 re-entrada escritos en Notion"
  ```

---

### Tarea 11: Actualizar bio de Instagram

- [ ] **Paso 1: Escribir la nueva bio**

  Bio actual: [actualizar según lo que tenga ahora]

  **Nueva bio:**
  ```
  Regulación del sistema nervioso
  Para quienes viven acelerados y no saben cómo bajar esa velocidad
  Yoga · Respiración · Neurociencia aplicada
  🔗 [link a Beacons.ai]
  ```

  Variante más corta:
  ```
  Tu cuerpo sabe cómo calmarse.
  Solo nadie te enseñó a activarlo.
  ↓ Protocolo gratuito
  ```

- [ ] **Paso 2: Actualizar en Instagram**

  Perfil → Editar perfil → Bio + Link en bio (pegar link de Beacons.ai)

- [ ] **Paso 3: Verificar**

  Abrir el perfil desde otra cuenta. El link debe llevar a Beacons.ai correctamente.

---

## BLOQUE 3: Outreach
*Correr en paralelo con el Bloque 2. Semanas 1–4.*

---

### Tarea 12: Outreach a participantes de bootcamps

*Enviar al finalizar cada bootcamp. Esta es la audiencia más caliente — ~25–33 personas por evento.*

- [ ] **Paso 1: Preparar el mensaje base**

  Para enviar por WhatsApp/Instagram DM a cada participante del bootcamp:

  ```
  Hola [nombre], fue muy bueno compartir el espacio en el bootcamp.

  Las mañanas de yoga son lo que más me gusta de esos días — hay algo en ese estado entre el esfuerzo y la calma que me parece muy poderoso.

  Estoy armando una comunidad online para sostener exactamente eso: la práctica de regulación del sistema nervioso fuera del retiro. Para no depender de los 4 días para encontrar ese estado.

  Es gratuita por ahora, estamos en los primeros días.
  Si te resuena, te comparto el link: [link de Skool]

  También tengo un protocolo corto de 3 minutos antes de dormir que funciona bien para empezar. ¿Te lo mando?
  ```

- [ ] **Paso 2: Enviar en los próximos 2 días post-bootcamp**

  Enviar a la lista de participantes del siguiente bootcamp después de lanzar la comunidad en Skool.
  No esperar tener todo perfecto — el contacto mientras el recuerdo del bootcamp está fresco es lo que da resultado.

- [ ] **Paso 3: Follow-up a quienes responden positivamente**

  Para quien acepte el protocolo:
  ```
  Acá está: [link del PDF]

  Son 3 minutos antes de dormir. Primera vez que lo uses, notás algo diferente.

  Si querés seguir el proceso, te espero en la comunidad: [link de Skool]
  ```

  Para quien pregunte más:
  Invitarlos a una conversación 1:1 vía WhatsApp o videollamada → esto es la detección de candidatos para Premium y acompañamiento 1:1.

---

### Tarea 13: Outreach a contactos cálidos (ex-clientes y conocidos)

- [ ] **Paso 1: Hacer la lista**

  En Notion, crear una tabla simple con:
  - Nombre
  - Canal de contacto (WhatsApp, Instagram, email)
  - Relación (ex-cliente, conocido, colega)
  - Estado (por contactar / contactado / respondió / en seguimiento)

  Objetivo: al menos 20–30 personas que ya te conocen.

- [ ] **Paso 2: Mensaje base por WhatsApp**

  ```
  Hola [nombre], hace tiempo que no hablamos.

  Estoy retomando de forma más activa el trabajo con regulación del sistema nervioso — lo que siempre hice pero ahora con más estructura.

  Arranqué una comunidad online para acompañar el proceso fuera de sesiones individuales. Estamos en los primeros días y los primeros miembros van a tener acceso gratuito al material que voy lanzando.

  ¿Te interesa ver de qué se trata? Te mando el link.
  ```

- [ ] **Paso 3: Mensaje para ex-clientes directos**

  ```
  Hola [nombre], quería contarte que estoy estructurando mejor todo el trabajo de regulación que hacemos/hicimos juntos.

  Armé una comunidad en Skool donde voy a tener sesiones en vivo, material de práctica y un espacio para sostener el proceso. Por ser alguien que ya pasó por el trabajo conmigo, los primeros meses son gratuitos.

  ¿Te sumo?
  ```

- [ ] **Paso 4: Seguimiento a los que respondieron**

  Para quien quiera más información: compartir link de Skool + PDF del protocolo.
  Para quien mencione urgencia o problema específico: ofrecer conversación 1:1.

---

## BLOQUE 4: Primera monetización pública
*Mes 2–3, una vez completados los Bloques 1–3.*

---

### Tarea 14: Activar venta pública — Guía de Meditación en Hotmart

**Prerequisito:** Tarea 5 completada. Alegra configurada (Tarea 2).

- [ ] **Paso 1: Definir precio final**

  Precio recomendado: **$19 USD** (o equivalente en COP).
  Justificación: accesible para el primer buyer, no regala el trabajo.

- [ ] **Paso 2: Publicar el producto en Hotmart**

  1. Abrir el borrador creado en la Tarea 5
  2. Actualizar precio: $19 USD
  3. Configurar la página de checkout de Hotmart (ya incluida en la plataforma)
  4. **Publicar** → el producto queda activo con su link de venta

- [ ] **Paso 3: Actualizar Beacons.ai**

  Activar el link "Guía de Meditación" que estaba oculto (Tarea 7, Paso 3).
  URL: el link de checkout de Hotmart.

- [ ] **Paso 4: Actualizar el Email 3 de Kit con el link real**

  El Email 3 de la secuencia (Tarea 3) tiene un placeholder `[LINK A HOTMART / PÁGINA DE VENTA]`.
  Reemplazar con el link de checkout real de Hotmart.

- [ ] **Paso 5: Primer post de venta en Instagram**

  ```
  Caption:
  Pasé semanas poniendo en orden todo lo que sé sobre meditación para principiantes.

  No para los que ya tienen práctica.
  Para los que lo intentaron, no les funcionó, y todavía quieren encontrar el camino.

  Siete prácticas progresivas. De la más simple a la más profunda.
  Cada una construye sobre la anterior.

  La Guía de Meditación ya está disponible.
  Link en bio → Guía de Meditación.

  Precio de lanzamiento esta semana: $19 USD.

  Hashtags: #meditacion #guia #sistemanervioso #yoga #bienestar #regulacion
  ```

---

### Tarea 15: Secuencia de email de ventas en Kit

**Prerequisito:** La secuencia de bienvenida (Tarea 3) ya debe estar activa.

Con el plan gratuito de Kit solo hay 1 automatización disponible. Opciones:
- **Opción A (plan gratuito):** Agregar los emails de venta al final de la secuencia existente de bienvenida (Emails 4 y 5)
- **Opción B:** Upgrade al plan Creator (~$29 USD/mes) para crear una segunda automatización separada

Recomendación: usar Opción A mientras la lista es pequeña.

- [ ] **Paso 1: Agregar Email 4 a la secuencia existente**

  En Kit → secuencia "Bienvenida — Protocolo 3 Respiraciones" → agregar email al Día 10:

  **Asunto:** `El siguiente paso`

  **Cuerpo:**
  ```
  El protocolo de respiraciones es el primer paso.

  Lo que viene después es el sistema completo:
  siete prácticas que van construyendo la capacidad de regularte solo.
  No en un momento de calma. En el medio del caos.

  La Guía de Meditación para Principiantes acaba de estar disponible.

  Precio de lanzamiento esta semana: $19 USD.
  Después sube.

  [LINK DE HOTMART]

  — Tincho
  ```

- [ ] **Paso 2: Verificar el flujo completo**

  Suscribirse con un email de prueba → confirmar que llegan los 4 emails en la secuencia correcta con los links correctos.

---

### Tarea 16: Transición Skool a pago

**Prerequisito:** Al menos 10–15 miembros activos en el Skool. Feedback positivo recibido.

- [ ] **Paso 1: Definir el precio de membresía**

  Rango recomendado: $7–12 USD/mes.
  Decisión final basada en el feedback de los primeros miembros (recopilar durante Tarea 6).
  Antes de continuar esta tarea, completar la decisión de precio. El post del Paso 2 y la configuración de Skool del Paso 3 usan ese número — no avanzar sin tenerlo definido.

- [ ] **Paso 2: Notificar a miembros actuales**

  Post en la comunidad (categoría Bienvenida):

  ```
  Quiero contarles algo antes de que pase.

  Desde el [fecha], la comunidad va a tener un costo mensual: $[X] USD.
  No es mucho. Es lo necesario para que esto sea sostenible.

  Quienes están desde el principio tienen dos opciones:
  ① Quedarse con el precio de fundador (descuento permanente de X%)
  ② Salir sin drama — y volver cuando quieran

  Si llegaron por el bootcamp, tienen el primer mes pago cubierto de mi parte.
  Si llegaron por Instagram, el primer mes también está cubierto.

  El cambio es en [fecha].
  Si querés quedarte con el precio de fundador, confirmame acá o por DM.

  Gracias por ser los primeros. Eso importa.

  — Tincho
  ```

- [ ] **Paso 3: Cambiar la configuración en Skool**

  1. Ir a **Community settings → Access → Paid**
  2. Configurar el precio mensual elegido
  3. Skool maneja el cobro automáticamente (toma el 10% como plataforma)
  4. Aplicar descuento manual para miembros fundadores

---

### Tarea 17: Página del libro — tincholibre.com/libro

**Prerequisito:** Tarea 1 completada. Saber dónde está disponible el libro (digital + físico).

- [ ] **Paso 1: Obtener los links de venta del libro**

  Necesitás:
  - Link de venta del libro digital (Kindle, Gumroad, Hotmart, o el que uses)
  - Link o información del libro físico (editorial, librería online, etc.)

- [ ] **Paso 2: Crear el archivo libro.html**

  Crear `libro.html` en la carpeta raíz del proyecto con este contenido (adaptar el CSS del `index.html` existente):

  ```html
  <!DOCTYPE html>
  <html lang="es">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Libertad en Jaque — Tincho</title>
      <style>
          /* Copiar el mismo bloque :root y body de index.html */
          * { margin: 0; padding: 0; box-sizing: border-box; }
          :root {
              --accent: #00D9FF;
              --accent-dark: #00B8D4;
              --text-primary: #E6E6E6;
              --text-secondary: #A0A0A0;
              --bg-dark: #0D1117;
              --bg-card: #161B22;
          }
          body {
              font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
              background-color: var(--bg-dark);
              color: var(--text-primary);
              line-height: 1.6;
          }
          .container { max-width: 700px; margin: 0 auto; padding: 60px 20px; }
          h1 {
              font-size: clamp(2.5rem, 8vw, 4rem);
              color: var(--accent);
              margin-bottom: 16px;
              font-weight: 700;
              line-height: 1.1;
          }
          .subtitle {
              font-size: 1.2rem;
              color: var(--text-secondary);
              margin-bottom: 48px;
              font-style: italic;
          }
          .descripcion {
              font-size: 1.1rem;
              color: var(--text-secondary);
              line-height: 1.8;
              margin-bottom: 20px;
          }
          .cta-group { display: flex; gap: 16px; flex-wrap: wrap; margin-top: 48px; }
          .btn {
              display: inline-block;
              padding: 16px 36px;
              border-radius: 8px;
              font-size: 1rem;
              font-weight: 700;
              text-decoration: none;
              cursor: pointer;
              transition: all 0.3s ease;
              font-family: inherit;
          }
          .btn-primary {
              background: var(--accent);
              color: var(--bg-dark);
              box-shadow: 0 8px 30px rgba(0,217,255,0.3);
          }
          .btn-primary:hover {
              background: var(--accent-dark);
              transform: translateY(-2px);
          }
          .btn-secondary {
              background: transparent;
              color: var(--accent);
              border: 2px solid var(--accent);
          }
          .btn-secondary:hover {
              background: rgba(0,217,255,0.05);
              transform: translateY(-2px);
          }
          .back { margin-top: 60px; }
          .back a { color: var(--text-secondary); text-decoration: none; font-size: 0.9rem; }
          .back a:hover { color: var(--accent); }
      </style>
  </head>
  <body>
      <div class="container">
          <h1>Libertad<br>en Jaque</h1>
          <p class="subtitle">Una crónica de encarcelamiento injusto y de la libertad que nació adentro.</p>

          <p class="descripcion">
              Esta no es una historia de victimismo ni de superación vacía.
              Es un relato con lujo de detalles de lo que ocurre cuando el mundo externo
              se cierra por completo — y lo único que queda es lo que hay adentro.
          </p>
          <p class="descripcion">
              En ese límite descubrí algo que ningún libro de bienestar me había enseñado:
              la calma no depende del entorno. Depende de lo que ocurre en el cuerpo y en la mente.
              Esa experiencia se convirtió en el método con el que trabajo hoy.
          </p>
          <p class="descripcion">
              Disponible en digital y en papel.
          </p>

          <div class="cta-group">
              <a href="[LINK_DIGITAL]" class="btn btn-primary" target="_blank">Conseguir el ebook</a>
              <a href="[LINK_FISICO]" class="btn btn-secondary" target="_blank">Libro físico</a>
          </div>

          <div class="back">
              <a href="/">← Volver a tincholibre.com</a>
          </div>
      </div>
  </body>
  </html>
  ```

  **Reemplazar:**
  - `[LINK_DIGITAL]` con el link real de venta del ebook
  - `[LINK_FISICO]` con el link del libro físico

- [ ] **Paso 3: Hacer deploy a Netlify**

  Netlify detecta automáticamente los cambios si configuraste el deploy desde la carpeta.
  Si usás el deploy manual (drag & drop), volvé a arrastrar la carpeta.

  Verificar: abrir `https://tincholibre.com/libro` → debe cargar la página.

- [ ] **Paso 4: Activar el link en Beacons.ai**

  En Beacons.ai → activar el link "Libertad en Jaque — el libro" que estaba oculto.

- [ ] **Paso 5: Commit**

  ```bash
  git add libro.html
  git commit -m "feat: página de Libertad en Jaque en tincholibre.com/libro"
  ```

---

## Criterios de avance entre fases

| Bloque | Completado cuando... |
|--------|---------------------|
| Bloque 0 | tincholibre.com carga con HTTPS ✓ + primera factura electrónica emitida en Alegra ✓ |
| Bloque 1 | Kit entrega el email automáticamente ✓ + ManyChat responde a "CALMA" ✓ + Skool activo con al menos 1 post ✓ |
| Bloque 2 | PDF publicado ✓ + 7 posts escritos y programados ✓ |
| Bloque 3 | Al menos 15 personas contactadas ✓ + al menos 5 en Skool |
| Bloque 4 | Primera venta pública en Hotmart ✓ + página del libro live ✓ |

---

## Notas de ejecución

- **El orden importa dentro de los bloques, no entre bloques.** El Bloque 2 y el Bloque 3 pueden empezar mientras el Bloque 1 todavía está en proceso.
- **Los primeros 14 días:** priorizar Tarea 1 (dominio) + Tarea 10 (posts) + Tarea 12/13 (outreach). El contenido y el contacto directo no dependen de tener todo el stack listo.
- **ManyChat necesita estar activo antes de publicar posts con CTA "CALMA"** (Posts 4 y 7 de la Tarea 10).
- **Hotmart necesita estar configurado antes de activar el Email 3 de Kit** con el link de venta.
- Las Fases 3–5 (PMR → Core + Premium → Skool formal) se planifican en un documento separado una vez que la Tarea 16 esté completada y haya feedback real de compradores.
