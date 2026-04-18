# Landing Page — Brandkit Refresh (Opción B)
**Fecha:** 2026-04-18  
**Alcance:** `index.html` + `brandkit.css`  
**Objetivo:** Migrar la landing a la paleta Amanecer oficial, incorporar assets del brandkit, y mejorar conversión con un segundo punto de captura y prueba social anticipada.

---

## Enfoque seleccionado

**Opción B — Tokens + Componentes + CRO.** Actualiza los valores de color, reemplaza componentes con assets oficiales, y agrega mejoras de conversión. No reescribe la estructura HTML desde cero.

---

## Sección 1: Paleta (brandkit.css)

Actualizar los 8 valores de color en `:root` de `brandkit.css`. Los nombres de variables permanecen iguales — todo el sitio hereda el cambio automáticamente.

| Variable | Valor actual (Atardecer) | Valor nuevo (Amanecer) |
|---|---|---|
| `--lago` | `#1F4D4A` | `#2D4A3E` |
| `--lago-prof` | `#0F2E2C` | `#162B23` |
| `--tierra` | `#B4643F` | `#C96F3D` |
| `--amanecer` | `#E4B363` | `#EDBC6A` |
| `--bruma` | `#8A9A95` | `#9B9583` |
| `--papel` | `#F4EFE6` | `#F7F1E4` |
| `--papel-prof` | `#EBE3D4` | `#EEE4CE` |
| `--tinta` | `#15201C` | `#1A1712` |

Fuente autoritativa: `Brandkit ASSETS/assets/tokens/brand-tokens.css`.

---

## Sección 2: Navegación

- Reemplazar SVG inline del logo con `<img src="Brandkit ASSETS/assets/logo/tincho-lockup-horizontal-light.svg">` (sobre fondos oscuros/lago).
- En contextos de fondo claro: `tincho-lockup-horizontal-dark.svg`.
- Los items `.nav-link--soon` ("Reset de Sueño", "Comunidad") se mantienen con su estilo actual.
- Sin cambios estructurales en los links de navegación.

---

## Sección 3: Hero

**Copy:**
- Headline: *"Tu cuerpo sabe cómo calmarse. Solo nadie te enseñó cómo activarlo."*
- Eyebrow: `— yoga · pranayama · neurociencia` (guión em, minúsculas, sin "aplicada")
- Subtext actual se mantiene.

**Foto (`IMG_1395.JPG`):**
- Agregar `object-position: center top` para centrar el rostro.
- Gradiente en borde inferior del wrapper para fundir la foto con el fondo (sin corte duro).

**CTAs:**
- Botón principal: se mantiene apuntando a `#protocolo`.
- Añadir link secundario en texto: *"Conoce el método →"* → `#como-trabajo`.

**Tipografía:**
- H1: `clamp(40px, 6vw, 80px)`.

**Nota de tono:** Usar tuteo en todo el sitio ("conoce", "aprende", "prueba") — no voseo.

---

## Sección 4: Iconografía — Sección Problema

Reemplazar SVGs inline genéricos con assets oficiales del brandkit:

| Dolor | Asset |
|---|---|
| No poder apagar la mente | `Brandkit ASSETS/assets/icons/icon-silence.svg` |
| Reactividad / perder el centro | `Brandkit ASSETS/assets/icons/icon-wave.svg` |
| Cuerpo en alerta constante | `Brandkit ASSETS/assets/icons/icon-nerve.svg` |
| Buscar calma sin encontrarla | `Brandkit ASSETS/assets/icons/icon-oasis.svg` |

Implementación: `<img src="..." class="problem-icon" aria-hidden="true">`.

---

## Sección 5: Segundo punto de captura (CRO)

Agregar formulario inline **después de la sección Problema, antes de Mi Camino**.

**Copy:**
> *"¿Reconoces esto? El protocolo de 3 respiraciones es el primer paso."*  
> `[Tu email]` → `[Quiero el protocolo]`

- Bloque compacto — no es una sección completa.
- Misma acción/integración MailerLite que el formulario del footer.
- Motivación: capturar en el momento de mayor activación emocional (después de leer los dolores).

---

## Sección 6: Prueba social anticipada

Agregar **barra compacta de credibilidad** inmediatamente después del Hero.

**Contenido:**
```
+20,000 seguidores (Instagram + TikTok)  ·  +150 personas en comunidad  ·  Autor de Libertad en Jaque

"Lo que Tincho enseña funciona porque él lo vivió."
```

- La sección completa de testimonios permanece en su posición actual (cierre antes del CTA final).
- La barra no es una sección — es un elemento visual compacto entre Hero y Problema.

---

## Sección 7: Tipografía y espaciado

**Escala tipográfica:**
- H1 hero: `clamp(40px, 6vw, 80px)`
- H2 secciones: `font-weight: 400` (Instrument Serif regular)
- Body text, line-height, font families: sin cambios.

**Espaciado:**
- Variable nueva: `--space-section: clamp(64px, 8vw, 120px)` — aplicada en padding vertical de todas las secciones.

**Motif separador:**
- `Brandkit ASSETS/assets/motifs/wave.svg` como separador decorativo entre Hero→Problema y Problema→Mi Camino.
- Reemplaza bordes duros o separadores genéricos.

---

## Archivos modificados

| Archivo | Tipo de cambio |
|---|---|
| `brandkit.css` | Actualizar 8 valores de color en `:root` |
| `index.html` | Copy hero, nav logo, iconos, formulario inline, barra social proof, motifs, espaciado |

## Archivos sin cambios (HTML)

- `libertad-en-jaque.html`, `gracias-guia.html`, `gracias-libro.html` — el cambio de paleta en `brandkit.css` los actualiza automáticamente sin tocar su HTML.

---

## Fuentes de assets

- Paleta: `Brandkit ASSETS/assets/tokens/brand-tokens.css`
- Logos: `Brandkit ASSETS/assets/logo/`
- Iconos: `Brandkit ASSETS/assets/icons/`
- Motifs: `Brandkit ASSETS/assets/motifs/`
- Fotos: `Documentos Pagina web/Fotos Principales/IMG_1395.JPG` (hero), `Documentos Pagina web/Fotos/IMG_5794.jpg` (Mi Camino)
