# Marea Verde · WoolBoom — sitio web

Sitio de una sola página para **Marea Verde SpA** (Puerto Aysén) y su producto estrella **WoolBoom**: barrera de absorción de hidrocarburos con lana de oveja. Proyecto apoyado por Corfo, programa Semilla Inicia.

Demo publicada: https://marea-verde-woolboom.netlify.app

## Estructura

```
index.html        Todo el sitio: HTML, CSS y JS en un solo archivo
img/              Fotos, logos y sello CORFO
juegos/           Los 4 juegos de la ovejita (HTML independientes)
  assets/         Ilustraciones y sprites compartidos por los juegos
  lanita/         Operación Lanita (simulador)
  cuantas/        ¿Cuántas ovejas? (puzle)
  rebano/         Rebaño al Rescate (arcade)
  colorear/       Pinta tu Ovejita (colorear)
```

No hay paso de compilación ni dependencias: es HTML estático. GSAP 3.12.5 se carga desde cdnjs.

## Cómo verlo en local

Desde esta carpeta:

```
python -m http.server 8765
```

y abrir http://localhost:8765. Conviene usar un servidor y no abrir el archivo con doble clic, porque los juegos se cargan en un `iframe`.

## Cómo está armado `index.html`

- **Pestañas** (`#marea`, `#woolboom`, `#juegos`): cada una es un `div.panel`; el JS muestra una y oculta las otras según el `#hash`. Otros anclas (`#contacto`, `#producto`, `#lista-juegos`) solo bajan dentro de la página.
- **Barra superior**: logo en SVG en línea con degradado animado, píldora `.pista` que se desliza a la pestaña activa (`moverPista()` en el JS).
- **Juegos**: se abren en un `<dialog class="sala">` con `iframe`, sin salir del sitio. Cada juego trae al final un "puente" `postMessage`: los enlaces `#contacto` dentro del juego cierran la ventana y bajan al pie.
- **Animaciones**: líneas de marea en canvas (portada), "la marea sube" sobre el lago, y GSAP/ScrollTrigger. Todo respeta `prefers-reduced-motion`.

## Reglas de contenido (importante)

- Los textos salen solo de las fichas del cliente (info de Marea Verde y de WoolBoom). No agregar afirmaciones que no estén ahí (por ejemplo "biodegradable", "reutilizable" o capacidades de absorción).
- El logo de CORFO ("Proyecto apoyado por Corfo") va siempre al pie.
- Los juegos usan cifras aproximadas y llevan la nota "Juegos ilustrativos".
- Paleta Marea: abismo `#004059`, petróleo `#006579`, turquesa `#00B9BD`, verde marea `#00998B`, hoja `#4CA73D`, noche `#1E232D`, marfil `#E9E2D4`. La pestaña WoolBoom usa además Lilita One y fondo lana `#F7F5F0`.
- Contacto: WhatsApp +56 9 9854 0061 · mareaverde.patagonia@gmail.com · Instagram @woolboom.cl.

## Publicar

Se publica en Netlify subiendo esta carpeta tal cual (sin build). Ejemplo con la CLI:

```
netlify deploy --dir . --prod
```

Hecho por Estudio Valencia.
