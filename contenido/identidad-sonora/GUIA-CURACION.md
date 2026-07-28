# Guía de Curación — Identidad Sonora

Procedimiento para elegir, verificar y preparar cada track de `identidad-sonora/`. Repetir por cada archivo pendiente en el "Estado de curación" del README.

## 1. Buscar candidatos

**Pixabay Music (principal):**
1. Ir a pixabay.com/music/search/
2. Buscar términos: `piano calm`, `peaceful piano`, `minimal piano`, `soft strings ambient`.
3. Filtrar por duración: preferir resultados de 2-4 min (dan más margen para encontrar un tramo de 60-90s sin cortes).
4. Abrir la página de cada candidato y revisar la licencia indicada ahí mismo antes de descargar — confirmar que permite uso comercial en redes sociales sin atribución obligatoria.

**YouTube Audio Library (respaldo, si Pixabay no alcanza):**
1. YouTube Studio → Audio Library.
2. Filtro Atribución: "No se requiere atribución".
3. Filtro Mood: Calm. Género: Ambient o Cinematic.
4. Buscar: `piano`.

## 2. Verificar cada candidato contra el checklist

Antes de guardar un candidato, confirmar escuchándolo completo:

| Criterio | Cómo verificarlo |
|---|---|
| Sin letra/voz | Escuchar completo — ni siquiera coros o vocalizaciones de fondo |
| Piano y/o cuerdas y/o pad suave, sin batería/percusión, sin instrumento étnico protagonista | Escuchar — si aparece un handpan/kalimba como base del track, descartar |
| 60-80 BPM | Si no lo indica la plataforma, contar el pulso durante 15 segundos y multiplicar por 4 |
| Tonalidad mayor o modal, no menor dramático | Escuchar — ¿suena cálido/en calma o suena triste/dramático? Si es lo segundo, descartar |
| Arreglo disperso, con espacio | Escuchar — si satura todo el rango de frecuencias sin pausas, descartar |
| Tramo de 60-90s reutilizable sin cortes abruptos | Identificar ese tramo dentro del archivo completo antes de recortar |
| Licencia de uso comercial en Reels/TikTok, descargable | Confirmado en el paso 1 |

Si el candidato falla en cualquier criterio, descartarlo y buscar el siguiente — no forzar un track que casi cumple.

## 3. Recortar el tramo elegido

No hay `ffmpeg` instalado en este entorno, así que el recorte se hace con una herramienta gratuita de interfaz simple:

**Audacity (recomendado, gratis):**
1. Descargar de audacityteam.org e instalar.
2. Abrir el archivo completo (File → Open).
3. Seleccionar con el mouse el tramo de 60-90s identificado en el paso 2.
4. File → Export Audio → Export Selected Audio (en Audacity reciente aparece en File → Export, con opción de exportar solo la selección).
5. Nombrar el archivo según la convención (ver paso 4) y guardar directamente en la carpeta `contenido/identidad-sonora/`.

## 4. Nombrar y guardar

Seguir la convención ya definida en el README:
- Tracks "Base": `base-01-piano-solo.mp3`, `base-02-piano-cuerdas.mp3`, `base-03-*.mp3` (si hay un tercero).
- Tracks "Cierre": `cierre-01-transformacion.mp3`, `cierre-02-*.mp3` (si hay un segundo).

## 5. Verificar el archivo final (duración, sin necesidad de ffmpeg)

Desde PowerShell, en la carpeta `contenido/identidad-sonora/`:

*(Sustituye `base-01-piano-solo.mp3` por el nombre del archivo que estés verificando)*

```powershell
$shell = New-Object -ComObject Shell.Application
$folder = $shell.Namespace((Get-Location).Path)
$file = $folder.ParseName("base-01-piano-solo.mp3")
0..320 | ForEach-Object {
    $label = $folder.GetDetailsOf($null, $_)
    if ($label -match "uraci|Length|Duration") {
        Write-Output "$_ : $label = $($folder.GetDetailsOf($file, $_))"
    }
}
```

Esto imprime la columna de duración (el nombre exacto de la columna varía según el idioma de Windows) para confirmar que el archivo exportado quedó entre 60 y 90 segundos antes de darlo por terminado.

## 6. Marcar como completado

Tildar la casilla correspondiente en "Estado de curación" del `README.md` una vez que el archivo está guardado y verificado.
