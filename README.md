# Plantilla NoExpertise · Carpintería y ebanistería

Web de taller para carpinteros y ebanistas: piezas a medida, trabajos con fotos grandes y presupuesto.

- Sectores: carpintería, ebanistería, muebles a medida, puertas y ventanas de madera, restauración de muebles. Estilo: loom (tema Loom de Hallmark). Plan mínimo: gratis.
- Secciones: hero, servicios, trabajos, proceso, maderas, opiniones, taller, zonas, preguntas, presupuesto, contacto (+ `texto` para apartados nuevos).
- Campos propios: `hero.pie_foto` (pie de la foto de portada) y `hero.items` (datos cortos, solo `titulo`); `servicios.items[]` (`titulo, texto, madera, plazo, precio, imagen`, y `detalle`, `imagenes` para su página); `trabajos.trabajos[]` (`titulo, tipo, lugar, madera, texto, imagen`); `proceso.items[]` (`titulo, texto, semanas`: «0», «1», «2-6») + `proceso.nota`; `maderas.maderas[]` (`nombre, uso, caracter`) + `maderas.imagen`; `taller.desde` («1979»), `taller.texto` (párrafos), `taller.items[]`; `presupuesto.items[]`, `presupuesto.nota` y `presupuesto.boton_formulario`.
- Para talleres: el teléfono y el WhatsApp mandan (cabecera, portada, presupuesto, preguntas, contacto y barra fija «Llamar / WhatsApp» en móvil) y el formulario de presupuesto es corto (nombre, teléfono, qué necesitas).
- Ejemplo: Carpintería Hermanos Lahoz, carpintería y ebanistería en Alcañiz (Teruel) y el Bajo Aragón (negocio ficticio, teléfonos 978 000 000 / 678 000 000).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (con `areaServed` desde `zonas`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas` (Lo que hacemos, El taller, Presupuesto y contacto). Sin la clave, una sola página larga.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`; tipografías y licencias en `public/fuentes/`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Tipografías Libre Caslon Display, Hanken Grotesk y DM Mono (SIL OFL 1.1, `public/fuentes/LICENCIAS.md`). Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada pieza de `secciones.servicios.items` con `detalle` tiene su página en `/carpinteria/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Cada zona de `secciones.zonas.items` con `texto` tiene su página en `/zonas/<slug>/` (`src/pages/zonas/[slug].astro`); en la sección, `titulo_pagina` y `texto_pagina` con {zona} y {negocio}.
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
