# Fundamentos de IA Productiva — Sitio del curso

Sitio estático (sin build) para alojar el contenido del curso. Cada módulo se muestra
como una carta; al hacer click se abre un modal con descripción corta y tres acciones:
descargar la presentación (Drive), ver la wiki de conceptos, y ver la presentación en HTML.

## Estructura

Cada módulo vive en su propia carpeta; `index.html` y `wiki.html` quedan en la raíz.

```
/
├── index.html              · Página principal con las cartas y los modales
├── wiki.html               · Renderiza la wiki de un módulo (wiki.html?m=1, ?m=2)
├── netlify.toml            · Config de publicación
├── Plan_IA_Productiva.pdf  · Plan general del curso
├── modulo-1/
│   ├── presentacion.html   · Slides interactivas del Módulo 1
│   ├── presentacion.pdf
│   ├── wiki.md             · Contenido de la wiki (Markdown)
│   └── wiki.pdf
└── modulo-2/
    ├── presentacion.html
    ├── presentacion.pdf
    ├── wiki.md
    ├── wiki.pdf
    └── insumos/            · Materiales para los 5 ejercicios prácticos
        ├── README.md
        ├── 01-manual-cliente.md
        ├── 02-correo-editorial.md
        ├── 03-correos-pedidos.md
        ├── 04-brief-agenda.md
        └── 05-reclamo-color.md
```

Las rutas a cada módulo están centralizadas: en `index.html` (array `MODULES`, campo `deck`) y
en `wiki.html` (objeto `MODULE_FILES`, campos `file` y `deck`).

## Lo que tienes que editar

1. **Link de Drive** — ya configurado en `index.html` (constante `DRIVE_FOLDER_URL`, arriba del
   bloque `<script>`). Todas las cartas usan esta misma carpeta compartida; para cambiarla,
   edita esa constante.

## Añadir un módulo nuevo (ej. Módulo 3)

1. Crea la carpeta `modulo-3/` con `presentacion.html` y `wiki.md` (y los PDF si aplica).
2. En `index.html`, agrega una entrada al array `MODULES` con `deck: "modulo-3/presentacion.html"`.
3. En `wiki.html`, agrega a `MODULE_FILES` la clave `"3"` con `file: "modulo-3/wiki.md"` y
   `deck: "modulo-3/presentacion.html"`.

## Probar localmente

Las wikis se cargan por `fetch`, así que necesitas servir por HTTP (no abrir con doble clic):

```bash
python3 -m http.server 8000
# luego abre http://localhost:8000
```

## Desplegar en Netlify

- **Arrastrar y soltar:** sube esta carpeta en https://app.netlify.com/drop
- **Desde Git:** conecta el repo; sin comando de build, *publish directory* = raíz (`.`).
