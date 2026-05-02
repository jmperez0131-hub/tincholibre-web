# Landing Page — Brandkit Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Migrar la landing a la paleta Amanecer, incorporar assets del brandkit, y agregar mejoras de conversión (segunda captura, prueba social anticipada, iconos de marca, TikTok en footer).

**Architecture:** Edits directos a HTML/CSS estáticos. No hay build system ni bundler. `brandkit.css` es el sistema de diseño compartido — cambiar los tokens ahí propaga el cambio a todas las páginas automáticamente. `index.html` concentra la mayoría de los cambios de contenido. Los otros tres archivos HTML solo reciben el link de TikTok en su footer.

**Tech Stack:** HTML5 estático, CSS custom properties, SVG inline, sin JavaScript framework. Servidor local recomendado: `npx serve .` o Live Server en VS Code.

---

## Mapa de archivos

| Archivo | Cambios |
|---|---|
| `brandkit.css` | 8 valores de color en `:root` |
| `index.html` | Paleta hero, nav, foto, prueba social, iconos, segunda captura, separadores, spacing, footer TikTok, JSON-LD |
| `libertad-en-jaque.html` | Footer: agregar TikTok |
| `gracias-guia.html` | Footer: agregar TikTok |
| `gracias-libro.html` | Footer: agregar TikTok |

---

## Task 1: Paleta Amanecer — brandkit.css

**Files:**
- Modify: `brandkit.css:12-19`

- [ ] **Step 1: Abrir el archivo y localizar el bloque de tokens de color**

En `brandkit.css`, líneas 11–19:
```css
:root {
  --lago:        #1F4D4A;
  --tierra:      #B4643F;
  --amanecer:    #E4B363;
  --bruma:       #8A9A95;
  --papel:       #F4EFE6;
  --papel-prof:  #EBE3D4;
  --tinta:       #15201C;
  --lago-prof:   #0F2E2C;
```

- [ ] **Step 2: Reemplazar los 8 valores con la paleta Amanecer**

```css
:root {
  --lago:        #2D4A3E;
  --tierra:      #C96F3D;
  --amanecer:    #EDBC6A;
  --bruma:       #9B9583;
  --papel:       #F7F1E4;
  --papel-prof:  #EEE4CE;
  --tinta:       #1A1712;
  --lago-prof:   #162B23;
```

- [ ] **Step 3: Verificar en navegador**

Abrir `index.html` en el navegador. En DevTools → Console:
```js
getComputedStyle(document.body).getPropertyValue('--lago').trim()
// Debe retornar: " #2D4A3E"
getComputedStyle(document.body).getPropertyValue('--papel').trim()
// Debe retornar: " #F7F1E4"
```
El fondo general debe verse ligeramente más cálido y el verde más terroso.

- [ ] **Step 4: Commit**

```bash
git add brandkit.css
git commit -m "feat: migrar paleta a Amanecer en brandkit.css"
```

---

## Task 2: Hero — foto, gradientes, copy, tipografía, CTA secundario

**Files:**
- Modify: `index.html:217-231` (gradientes foto)
- Modify: `index.html:266-280` (hero-title font-size)
- Modify: `index.html:1105-1136` (HTML del hero)

- [ ] **Step 1: Actualizar gradientes del hero-photo-wrap**

Localizar en `index.html` los bloques `.hero-photo-wrap::before` y `::after` (alrededor de línea 217). Reemplazar:

```css
/* ANTES */
.hero-photo-wrap::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(90deg, var(--papel) 0%, rgba(244,239,230,0.7) 42%, transparent 72%);
    z-index: 1;
}

.hero-photo-wrap::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(180deg, rgba(244,239,230,0.2) 0%, transparent 35%, rgba(244,239,230,0.6) 100%);
    z-index: 1;
}
```

```css
/* DESPUÉS */
.hero-photo-wrap::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(
        90deg,
        var(--papel) 0%,
        color-mix(in srgb, var(--papel) 70%, transparent) 42%,
        transparent 72%
    );
    z-index: 1;
}

.hero-photo-wrap::after {
    content: '';
    position: absolute;
    inset: 0;
    background:
        linear-gradient(180deg, transparent 60%, color-mix(in srgb, var(--papel) 60%, transparent) 100%),
        linear-gradient(270deg, var(--papel) 0%, transparent 20%);
    z-index: 1;
}
```

- [ ] **Step 2: Actualizar el gradiente mobile del hero-photo-wrap**

Localizar el media query `@media (max-width: 768px)` que contiene `.hero-photo-wrap::before` (alrededor de línea 993). Reemplazar:

```css
/* ANTES */
.hero-photo-wrap::before {
    background: linear-gradient(180deg, rgba(244,239,230,0.3) 0%, var(--papel) 80%);
}
```

```css
/* DESPUÉS */
.hero-photo-wrap::before {
    background: linear-gradient(180deg, color-mix(in srgb, var(--papel) 30%, transparent) 0%, var(--papel) 80%);
}
```

- [ ] **Step 3: Actualizar font-size del hero-title y agregar estilos del link secundario**

Localizar `.hero-title` (alrededor de línea 266). Cambiar el `font-size`:

```css
/* ANTES */
.hero-title {
    font-family: var(--font-display);
    font-size: clamp(2.2rem, 5vw, 3.8rem);
```

```css
/* DESPUÉS */
.hero-title {
    font-family: var(--font-display);
    font-size: clamp(40px, 6vw, 80px);
```

Después del bloque `.hero-title em { ... }`, agregar el nuevo estilo para el link secundario:

```css
.hero-link-secondary {
    display: inline-block;
    font-family: var(--font-body);
    font-size: 0.875rem;
    color: var(--bruma);
    margin-top: 16px;
    transition: color 0.2s;
}
.hero-link-secondary:hover { color: var(--tinta); }
```

- [ ] **Step 4: Reemplazar el HTML del hero**

Localizar la sección hero (línea 1103). Reemplazar el contenido completo del `<section class="hero">`:

```html
<!-- ═══════════════════════════════════════════════
     HERO
════════════════════════════════════════════════ -->
<section class="hero" id="inicio" aria-label="Sección principal">

    <div class="hero-photo-wrap" aria-hidden="true">
        <img
            src="Documentos Pagina web/fotos sin bg/61ccaa3b-1e15-4014-bb75-12a127cdbcd0.png"
            alt="Tincho — instructor de yoga, pranayama y neurociencia aplicada"
            style="filter: saturate(0.85) contrast(1.02);"
        >
    </div>

    <!-- Motivo arco decorativo -->
    <svg class="hero-arc" viewBox="0 0 200 100" fill="none" stroke="currentColor" stroke-width="1.5" aria-hidden="true">
        <path d="M4 96 A 96 96 0 0 1 196 96"/>
    </svg>

    <div class="hero-content">
        <span class="eyebrow reveal">— yoga · pranayama · neurociencia</span>

        <h1 class="hero-title reveal" data-delay="1">
            Tu cuerpo sabe cómo calmarse.<br>
            <em>Solo nadie te enseñó cómo activarlo.</em>
        </h1>

        <p class="hero-sub reveal" data-delay="2">
            Vives acelerado pero no sabes cómo bajar esa velocidad.<br>
            Ninguna solución funciona porque ninguna ataca la raíz.
        </p>

        <a href="#protocolo" class="bk-btn bk-btn-lago reveal" data-delay="3" aria-label="Descarga el protocolo gratuito de respiración">
            Descarga el protocolo gratuito
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <path d="M12 5v14M5 12l7 7 7-7"/>
            </svg>
        </a>

        <a href="#como-trabajo" class="hero-link-secondary reveal" data-delay="4">
            Conoce el método →
        </a>
    </div>

    <div class="scroll-hint" aria-hidden="true">
        <span>Scroll</span>
        <div class="scroll-hint-line"></div>
    </div>

</section>
```

- [ ] **Step 5: Verificar en navegador**

- La foto debe mostrar la pose namaste (manos juntas)
- El headline debe leer "Tu cuerpo sabe cómo calmarse."
- El eyebrow debe leer "— yoga · pranayama · neurociencia" (minúsculas, sin "aplicada")
- El link "Conoce el método →" debe aparecer debajo del botón principal
- Los bordes de la foto deben disolverse hacia el fondo (izquierda, abajo, derecha)
- La foto no debe tener el fondo negro visible sobre el fondo crema

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: hero — foto namaste, headline LANDING.md, gradientes con CSS vars"
```

---

## Task 3: Navegación — lockup oficial

**Files:**
- Modify: `index.html:1073-1081` (HTML del nav-brand)
- Modify: `index.html:77-91` (CSS .nav-brand-mark y .nav-brand-name → nuevo .nav-lockup)

- [ ] **Step 1: Agregar estilo .nav-lockup en el bloque CSS del nav**

Dentro del bloque `/* ─── NAVBAR ──────────────────────────────────── */`, después de `.nav-brand { ... }`, agregar:

```css
.nav-lockup {
    height: 34px;
    width: auto;
    display: block;
}
```

- [ ] **Step 2: Reemplazar el HTML del nav-brand**

Localizar (línea 1073):
```html
<a href="#inicio" class="nav-brand" aria-label="TinchoLibre — Inicio">
    <svg class="nav-brand-mark" viewBox="0 0 120 120" fill="none" stroke="currentColor" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <path d="M12 68 C 32 52, 88 52, 108 68"/>
        <line x1="60" y1="30" x2="60" y2="98"/>
        <line x1="34" y1="44" x2="86" y2="44"/>
        <circle cx="60" cy="44" r="3.2" fill="#E4B363" stroke="none"/>
    </svg>
    <span class="nav-brand-name">TinchoLibre</span>
</a>
```

Reemplazar con:
```html
<a href="#inicio" class="nav-brand" aria-label="Tincho — Inicio">
    <img
        src="Brandkit ASSETS/assets/logo/tincho-lockup-horizontal-dark.svg"
        alt="Tincho"
        class="nav-lockup"
    >
</a>
```

- [ ] **Step 3: Verificar en navegador**

- El logo de la nav debe mostrar el lockup oficial (mark + wordmark en una sola imagen)
- Al hacer scroll, el logo debe seguir siendo legible sobre el fondo crema translúcido

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: nav — reemplazar SVG inline con lockup oficial del brandkit"
```

---

## Task 4: Barra de prueba social

**Files:**
- Modify: `index.html` — agregar CSS y HTML de la barra entre hero y problema

- [ ] **Step 1: Agregar CSS de la barra de prueba social**

Después del bloque `/* ─── HERO ──────────────────────────────────── */` y antes de `/* ─── PROBLEMA ──────────────────────────────── */`, agregar:

```css
/* ─── SOCIAL PROOF BAR ────────────────────────── */
.social-proof-bar {
    background: var(--papel-prof);
    border-top: 1px solid var(--line);
    border-bottom: 1px solid var(--line);
    padding: 28px 48px;
}

.social-proof-inner {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    text-align: center;
}

.social-proof-stats {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 6px 20px;
    font-size: 0.875rem;
    color: var(--tinta);
}

.social-proof-stats strong {
    font-weight: 600;
    color: var(--lago);
}

.sp-sep { color: var(--bruma); }

.sp-quote {
    font-family: var(--font-display);
    font-style: italic;
    font-size: 1rem;
    color: var(--bruma);
    margin: 0;
}

@media (max-width: 768px) {
    .social-proof-bar { padding: 24px; }
    .sp-sep { display: none; }
    .social-proof-stats { flex-direction: column; gap: 6px; }
}
```

- [ ] **Step 2: Agregar HTML de la barra después del cierre del hero**

Localizar `</section>` que cierra el hero (línea 1143, después del `</section>` de `id="inicio"`). Inmediatamente después agregar:

```html
<!-- ═══════════════════════════════════════════════
     SOCIAL PROOF BAR
════════════════════════════════════════════════ -->
<div class="social-proof-bar" aria-label="Credenciales">
    <div class="social-proof-inner">
        <div class="social-proof-stats">
            <span class="sp-stat"><strong>+20,000</strong> en redes sociales</span>
            <span class="sp-sep" aria-hidden="true">·</span>
            <span class="sp-stat"><strong>+2,000</strong> emprendedores en bootcamps presenciales</span>
            <span class="sp-sep" aria-hidden="true">·</span>
            <span class="sp-stat">Autor de <em>Libertad en Jaque</em></span>
        </div>
        <blockquote class="sp-quote">
            "Lo que Tincho enseña funciona porque él lo vivió."
        </blockquote>
    </div>
</div>
```

- [ ] **Step 3: Verificar en navegador**

- La barra debe aparecer entre el hero y la sección Problema
- Los números en verde lago, el texto en tinta
- La cita en itálica con Instrument Serif
- En mobile: los tres stats apilados verticalmente, sin separadores

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: agregar barra de prueba social entre hero y problema"
```

---

## Task 5: Sección Problema — iconos del brandkit

**Files:**
- Modify: `index.html` — CSS `.card-icon` + HTML de los 3 `.card-icon`

- [ ] **Step 1: Actualizar CSS de .card-icon para imágenes**

Localizar el bloque `.card-icon` en los estilos (buscar `.card-icon`). Agregar la regla para `img` dentro:

```css
.card-icon img {
    width: 100%;
    height: 100%;
    object-fit: contain;
    filter: brightness(0) invert(1);
}
```

La clase `.card-icon` tiene `width: 40px; height: 40px; color: var(--amanecer)`. El `filter` hace los iconos SVG blancos, que es legible sobre el fondo lago oscuro de la sección Problema.

- [ ] **Step 2: Reemplazar los SVG inline de los tres cards**

Localizar los tres `.card-problem` (línea 1163). Reemplazar los tres bloques `<div class="card-icon">`:

**Card 1 — reactividad:**
```html
<!-- ANTES -->
<div class="card-icon" aria-hidden="true"><svg viewBox="0 0 32 32" ...><path d="M3 16 C 8 10, 12 22, 16 16 S 24 10, 29 16"/></svg></div>

<!-- DESPUÉS -->
<div class="card-icon" aria-hidden="true">
    <img src="Brandkit ASSETS/assets/icons/icon-wave.svg" alt="">
</div>
```

**Card 2 — calma falsa:**
```html
<!-- ANTES -->
<div class="card-icon" aria-hidden="true"><svg viewBox="0 0 32 32" ...><circle cx="16" cy="16" r="12"/><path d="M10 16 L22 16"/></svg></div>

<!-- DESPUÉS -->
<div class="card-icon" aria-hidden="true">
    <img src="Brandkit ASSETS/assets/icons/icon-oasis.svg" alt="">
</div>
```

**Card 3 — mente que no para:**
```html
<!-- ANTES -->
<div class="card-icon" aria-hidden="true"><svg viewBox="0 0 32 32" ...><path d="M6 6 C 12 10, 12 14, 16 16 C 20 18, 20 22, 26 26"/><circle cx="6" cy="6" r="1.5"/><circle cx="26" cy="26" r="1.5"/></svg></div>

<!-- DESPUÉS -->
<div class="card-icon" aria-hidden="true">
    <img src="Brandkit ASSETS/assets/icons/icon-silence.svg" alt="">
</div>
```

- [ ] **Step 3: Verificar en navegador**

- Los tres cards deben mostrar los iconos del brandkit en blanco sobre el fondo lago oscuro
- Los iconos deben tener trazo fino, estilo lineal, sin deformarse (object-fit: contain)

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: problema — iconos del brandkit reemplazan SVGs inline"
```

---

## Task 6: Segunda captura CRO

**Files:**
- Modify: `index.html` — agregar CSS y HTML entre problema y camino

- [ ] **Step 1: Agregar CSS del bloque mini-capture**

Después del bloque de CSS de `.problema`, agregar:

```css
/* ─── MINI CAPTURE ────────────────────────────── */
.mini-capture {
    background: var(--lago-prof);
    padding: 48px 48px;
    border-top: 1px solid rgba(247,241,228,0.06);
}

.mini-capture-inner {
    max-width: 560px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    text-align: center;
}

.mini-capture-hook {
    font-size: 1.05rem;
    color: var(--papel);
    line-height: 1.7;
    margin: 0;
}

.mini-capture-form {
    display: flex;
    gap: 12px;
    width: 100%;
    flex-wrap: wrap;
    justify-content: center;
}

.mini-capture-form .form-input {
    flex: 1;
    min-width: 200px;
    background: rgba(247,241,228,0.08);
    border-color: rgba(247,241,228,0.2);
    color: var(--papel);
}

.mini-capture-form .form-input::placeholder { color: rgba(247,241,228,0.4); }

@media (max-width: 768px) {
    .mini-capture { padding: 40px 24px; }
    .mini-capture-form { flex-direction: column; }
    .mini-capture-form .form-input { min-width: 0; width: 100%; }
}
```

- [ ] **Step 2: Agregar HTML entre el cierre de `.problema` y el div `.transicion`**

Localizar `</section>` que cierra `id="problema"` (línea 1178). Inmediatamente después, antes del `<div class="transicion">`, agregar:

```html
<!-- ═══════════════════════════════════════════════
     MINI CAPTURE — CRO
════════════════════════════════════════════════ -->
<div class="mini-capture">
    <div class="mini-capture-inner">
        <p class="mini-capture-hook">
            ¿Reconoces esto? El protocolo de 3 respiraciones es el primer paso.
        </p>
        <form class="mini-capture-form" id="form-mini" novalidate>
            <label for="email-mini" class="sr-only">Tu email</label>
            <input
                type="email"
                id="email-mini"
                class="form-input"
                placeholder="Tu email"
                required
                autocomplete="email"
                aria-required="true"
            >
            <button type="submit" class="bk-btn bk-btn-amanecer" id="form-mini-btn">
                Quiero el protocolo
            </button>
        </form>
    </div>
</div>
```

- [ ] **Step 3: Agregar el event listener del mini form al bloque JS**

Localizar al final del `<script>` (después del listener de `form-protocolo`, alrededor de línea 1544). Agregar:

```js
/* ── Mini form ───────────────────────────────── */
document.getElementById('form-mini').addEventListener('submit', function(e) {
    e.preventDefault();
    const input = this.querySelector('.form-input');
    const btn   = document.getElementById('form-mini-btn');

    if (!input.value || !input.validity.valid) {
        input.focus();
        return;
    }

    btn.disabled = true;
    btn.textContent = '¡Listo! Revisa tu correo.';
});
```

- [ ] **Step 4: Verificar en navegador**

- El bloque debe aparecer entre la sección Problema y la cita de transición
- Fondo verde profundo (lago-prof), texto crema
- El botón dorado (amanecer) con texto "Quiero el protocolo"
- Al enviar un email válido: el botón se deshabilita y muestra "¡Listo! Revisa tu correo."
- Al enviar vacío: el foco va al input (no explota)

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: segunda captura CRO entre sección Problema y Mi Camino"
```

---

## Task 7: Separadores wave + espaciado de secciones

**Files:**
- Modify: `index.html` — CSS `.section`, CSS `.wave-sep`, HTML dos separadores

- [ ] **Step 1: Actualizar el padding de .section a valor responsivo**

Localizar (alrededor de línea 322):
```css
.section { padding: 100px 48px; }
```

Reemplazar con:
```css
.section { padding: clamp(64px, 8vw, 120px) 48px; }
```

Localizar en el media query `@media (max-width: 768px)`:
```css
.section { padding: 72px 24px; }
```

Reemplazar con:
```css
.section { padding: clamp(64px, 8vw, 120px) 24px; }
```

- [ ] **Step 2: Agregar CSS del separador wave**

Después del bloque CSS de `.mini-capture`, agregar:

```css
/* ─── WAVE SEPARATOR ──────────────────────────── */
.wave-sep {
    overflow: hidden;
    line-height: 0;
    padding: 0;
    opacity: 0.35;
}

.wave-sep img {
    width: 100%;
    max-height: 48px;
    object-fit: cover;
    display: block;
}
```

- [ ] **Step 3: Insertar separador wave entre hero-bar y problema**

Localizar el cierre del `.social-proof-bar` y el inicio de `<section class="section problema"`. Entre los dos, agregar:

```html
<!-- Wave separator -->
<div class="wave-sep" aria-hidden="true">
    <img src="Brandkit ASSETS/assets/motifs/wave.svg" alt="">
</div>
```

- [ ] **Step 4: Insertar separador wave entre mini-capture y transición**

Localizar el cierre del `.mini-capture` y el `<div class="transicion">`. Entre los dos, agregar:

```html
<!-- Wave separator -->
<div class="wave-sep" aria-hidden="true">
    <img src="Brandkit ASSETS/assets/motifs/wave.svg" alt="">
</div>
```

- [ ] **Step 5: Verificar en navegador**

- Los separadores wave deben aparecer como líneas onduladas sutiles (opacidad 35%)
- El espaciado vertical de las secciones debe verse consistente y fluido entre breakpoints

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: wave separators + espaciado responsivo de secciones"
```

---

## Task 8: Footer TikTok — todas las páginas + JSON-LD

**Files:**
- Modify: `index.html:1059` (JSON-LD sameAs) + `index.html:1477` (footer)
- Modify: `libertad-en-jaque.html:1581` (footer)
- Modify: `gracias-guia.html` (footer, después del link de Instagram)
- Modify: `gracias-libro.html` (footer, después del link de Instagram)

El bloque TikTok a agregar en cada página (después del link de Instagram):

```html
<a
    href="https://www.tiktok.com/@tincholibre"
    class="footer-ig"
    target="_blank"
    rel="noopener noreferrer"
    aria-label="TikTok de Tincho — @tincholibre"
>
    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <path d="M9 12a4 4 0 1 0 4 4V4a5 5 0 0 0 5 5"/>
    </svg>
    @tincholibre
</a>
```

- [ ] **Step 1: Actualizar JSON-LD sameAs en index.html**

Localizar (línea 1059):
```json
"sameAs": ["https://instagram.com/tincholibre"],
```

Reemplazar con:
```json
"sameAs": ["https://instagram.com/tincholibre", "https://www.tiktok.com/@tincholibre"],
```

- [ ] **Step 2: Agregar TikTok en el footer de index.html**

Localizar (línea 1477), después del cierre `</a>` del link de Instagram:
```html
        @tincholibre
    </a>

    <p class="footer-copy">
```

Insertar el bloque TikTok entre el `</a>` de Instagram y el `<p class="footer-copy">`:
```html
        @tincholibre
    </a>

    <a
        href="https://www.tiktok.com/@tincholibre"
        class="footer-ig"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="TikTok de Tincho — @tincholibre"
    >
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
            <path d="M9 12a4 4 0 1 0 4 4V4a5 5 0 0 0 5 5"/>
        </svg>
        @tincholibre
    </a>

    <p class="footer-copy">
```

- [ ] **Step 3: Agregar TikTok en el footer de libertad-en-jaque.html**

Localizar la línea `@tincholibre` seguida del cierre `</a>` del Instagram (alrededor de línea 1581). Insertar después del `</a>`:

```html
  <a href="https://www.tiktok.com/@tincholibre" class="footer-ig" target="_blank" rel="noopener noreferrer" aria-label="TikTok de Tincho — @tincholibre">
    <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <path d="M9 12a4 4 0 1 0 4 4V4a5 5 0 0 0 5 5"/>
    </svg>
    @tincholibre
  </a>
```

Nota: esta página usa 15×15 para el icono (consistente con el icono de Instagram de esa página).

- [ ] **Step 4: Agregar TikTok en el footer de gracias-guia.html**

Localizar el `</a>` del link de Instagram en el footer (alrededor de línea 577). Insertar después:

```html
        <a
            href="https://www.tiktok.com/@tincholibre"
            class="footer-ig"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="TikTok de Tincho — @tincholibre"
        >
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <path d="M9 12a4 4 0 1 0 4 4V4a5 5 0 0 0 5 5"/>
            </svg>
            @tincholibre
        </a>
```

- [ ] **Step 5: Agregar TikTok en el footer de gracias-libro.html**

Localizar el `</a>` del link de Instagram en el footer (alrededor de línea 682). Insertar después:

```html
    <a
      href="https://www.tiktok.com/@tincholibre"
      class="footer-ig"
      target="_blank"
      rel="noopener noreferrer"
      aria-label="TikTok de Tincho — @tincholibre"
    >
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <path d="M9 12a4 4 0 1 0 4 4V4a5 5 0 0 0 5 5"/>
      </svg>
      @tincholibre
    </a>
```

- [ ] **Step 6: Verificar en navegador**

Abrir cada una de las 4 páginas y verificar:
- El footer debe mostrar Instagram + TikTok uno al lado del otro
- Ambos links deben abrir en nueva pestaña
- El ícono de TikTok (nota musical simplificada) debe ser legible

- [ ] **Step 7: Commit**

```bash
git add index.html libertad-en-jaque.html gracias-guia.html gracias-libro.html
git commit -m "feat: footer TikTok en todas las páginas + JSON-LD sameAs actualizado"
```

---

## Verificación final

- [ ] **Abrir index.html en navegador y recorrer la página completa de arriba a abajo:**
  - [ ] Nav: lockup oficial visible
  - [ ] Hero: foto namaste, headline correcto, eyebrow minúsculas, botón principal + link secundario
  - [ ] Social proof bar: tres stats + cita
  - [ ] Wave separator sutil
  - [ ] Problema: iconos del brandkit en blanco
  - [ ] Mini capture: bloque verde profundo con form
  - [ ] Wave separator sutil
  - [ ] Resto de secciones: sin cambios visuales inesperados
  - [ ] Footer: Instagram + TikTok lado a lado
- [ ] **Verificar mobile (DevTools → 390px):** foto hero en modo fantasma (opacity 0.22), mini capture apilado, social proof bar apilado
- [ ] **Verificar otras páginas:** libertad-en-jaque.html, gracias-guia.html, gracias-libro.html — solo TikTok en footer
