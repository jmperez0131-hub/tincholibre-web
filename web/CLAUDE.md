# Subproyecto: Sitio web tincholibre.com

> Ver CLAUDE.md raíz para contexto completo de marca. Este archivo agrega contexto técnico específico del sitio.

## Estructura de páginas

| Archivo | Propósito |
|---------|-----------|
| `index.html` | Landing principal — captura de lead magnet |
| `la-mente-que-no-para.html` | Página de ventas del curso |
| `libertad-en-jaque.html` | Página de ventas del libro |
| `gracias-guia.html` | Página de gracias post-descarga guía |
| `gracias-libro.html` | Página de gracias post-compra libro |
| `brandkit.css` | Estilos globales del sitio |

## Assets locales referenciados por HTML

- `Brandkit ASSETS/assets/` — logos, íconos, motivos SVG, tokens de color
- `Documentos Pagina web/` — fotos profesionales y sin fondo
- `Libertad en Jaque/Mockups/` — imágenes del libro para la página de ventas

## Convenciones

- Los HTML usan rutas relativas desde esta carpeta (`web/`)
- No usar rutas absolutas ni CDN para assets de marca — solo locales
- Las páginas de gracias no tienen nav, solo CTA de siguiente paso
- Paleta y tipografía definidas en `Brandkit ASSETS/assets/tokens/brand-tokens.css`
