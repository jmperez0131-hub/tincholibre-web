# Landing Page — Brandkit Refresh (Opción B)
**Fecha:** 2026-04-18  
**Alcance:** `index.html` + `brandkit.css` + footer de todas las páginas del sitio  
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

**Foto (`IMG_1395.JPG`) — tratamiento estético:**
- `object-position: center top` para centrar el rostro.
- Reescribir los gradientes `::before` y `::after` usando `var(--papel)` en lugar de los valores RGBA hardcodeados de la paleta vieja (`rgba(244,239,230,...)`).
- Agregar gradiente de fusión también en el borde derecho — actualmente solo tiene izquierda y abajo. La foto se disuelve en los 3 bordes (Seismic Calm: señal que se desvanece).
- Agregar `filter: saturate(0.85) contrast(1.02)` a la foto — integra tonalmente con la paleta cálida sin afectar la legibilidad del rostro.

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
+20,000 en redes sociales  ·  +2,000 emprendedores en bootcamps presenciales  ·  Autor de Libertad en Jaque

"Lo que Tincho enseña funciona porque él lo vivió."
```

- "+20,000 en redes sociales" = Instagram (13.3K) + TikTok (6.5K+), sin nombrar plataformas específicas.
- "+2,000 emprendedores en bootcamps presenciales" reemplaza "+150 en comunidad" — más impactante y específico al ICP. Refiere al trabajo en vivo en Silicon Valley de Latam, que es un diferenciador real (no es reach online, es presencia física).

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

## Sección 8: Footer — TikTok

Agregar link e ícono de TikTok al footer de todas las páginas del sitio.

- URL: `https://www.tiktok.com/@tincholibre`
- Ícono SVG inline (mismo estilo que el ícono de Instagram existente: `stroke="currentColor"`, 16×16)
- Posición: junto al link de Instagram existente
- Clase reutiliza `.footer-ig` (estilos ya correctos)
- Actualizar JSON-LD `sameAs` en `index.html` para incluir TikTok: `["https://instagram.com/tincholibre", "https://www.tiktok.com/@tincholibre"]`
- Páginas afectadas: `index.html`, `libertad-en-jaque.html`, `gracias-guia.html`, `gracias-libro.html`

---

## Archivos modificados

| Archivo | Tipo de cambio |
|---|---|
| `brandkit.css` | Actualizar 8 valores de color en `:root` |
| `index.html` | Copy hero, nav logo, foto tratamiento, iconos, formulario inline, barra social proof, motifs, espaciado, footer TikTok, JSON-LD sameAs |
| `libertad-en-jaque.html` | Footer TikTok |
| `gracias-guia.html` | Footer TikTok |
| `gracias-libro.html` | Footer TikTok |

---

## Fuentes de assets

- Paleta: `Brandkit ASSETS/assets/tokens/brand-tokens.css`
- Logos: `Brandkit ASSETS/assets/logo/`
- Iconos: `Brandkit ASSETS/assets/icons/`
- Motifs: `Brandkit ASSETS/assets/motifs/`
- Fotos: `Documentos Pagina web/Fotos Principales/IMG_1395.JPG` (hero), `Documentos Pagina web/Fotos/IMG_5794.jpg` (Mi Camino)
