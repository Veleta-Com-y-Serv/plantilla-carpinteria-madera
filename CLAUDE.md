# Plantilla «Carpintería y ebanistería» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **loom** (tema
Loom de la skill Hallmark): papel crudo, tinta casi negra, Libre Caslon Display en titulares y precios sobre Hanken
Grotesk, filetes finos y un filete de tinta encima de cada lista, todo cuadrado y plano, y un solo añil que llega como
botón, línea o banda. Se lee como el libro de muestras de un taller. Es la web de un **taller de carpintería**: habla
en plural («hacemos», «montamos») y trata al cliente de tú; el teléfono, el WhatsApp y el presupuesto mandan. Todo en
castellano de España, frases cortas, sin jerga. El brief de diseño completo está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); `src/styles/global.css` deriva el resto con `color-mix` y `oklch(from …)`:
  - `fondo` = papel crudo; `--papel-2` (arena: banda de «Cómo se encarga», pozo del formulario) y `--papel-3` (barras de la escala) salen de él.
  - `texto` = tinta: titulares y filetes de 2 px; `--apagado` (letra menuda) y `--filete` (rayas finas) salen de la mezcla con el papel.
  - `acento` = añil: botones, banda de presupuesto, la línea de entrega de la escala, subrayados al pasar y el foco.
  - `primario` = nogal oscuro: el pie.
  - La letra encima de cada color se calcula sola (`--sobre-primario`, `--sobre-acento`: oscura si el color es claro, clara si es oscuro).
- **Tipografías**: `public/fuentes/` (Libre Caslon Display 400, Hanken Grotesk 400 y 500, DM Mono 400; OFL, licencias en `public/fuentes/LICENCIAS.md`), declaradas en `src/styles/global.css`; la de titulares, precargada en `Base.astro`. No añadas fuentes externas. Caslon nunca por debajo de 32 px salvo el nombre de la cabecera.
- **Aspecto general**: `src/styles/global.css` (bandas `.banda`, `.banda--arena`, `.banda--anil`; `.cabeza` partida; `.btn` añil cuadrado y `.btn-sec` con raya de 2 px; `.foto` con el tratamiento natural del tema; `.indice` (filas del índice), `.obras`, `.escala` (semanas), `.mitades`, `.muestrario` (tabla de maderas), `.lugares`, `.faq`, `.datos`, cabecera `.cabecera--taller`, pie `.pie--taller` y barra fija de móvil).
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = el nombre en Libre Caslon Display.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas son bandas a todo el ancho y pintan bien con listas y campos vacíos.
- `hero` → `hero.astro`: foto (`imagen`) a sangre a la izquierda de toda la altura con `pie_foto` debajo; a la derecha `antetitulo`, `titulo`, `texto`, `cta` (botón añil) y `cta_secundario` (enlace subrayado); `items: [{titulo}]` como filas cortas con filete. En móvil, foto arriba. Sin foto, solo texto.
- `servicios` → `servicios.astro`: «Lo que hacemos», índice con filetes; `items: [{titulo, texto, madera, plazo, precio, imagen, imagenes, detalle}]`. Nombre en Caslon (enlaza a su página si tiene `detalle`), madera y plazo como datos, `precio` en cifra grande (sin número, en letra normal; vacío no se pinta). `cta` debajo.
- `trabajos` → `trabajos.astro`: fotos grandes; las dos primeras a 8 y 4 columnas y el resto en fila de 3 o 4; `trabajos: [{titulo, tipo, lugar, madera, texto, imagen}]` con su pie (tipo, título, madera y lugar, frase).
- `proceso` → `proceso.astro`: «Cómo se encarga», banda de arena con la escala de semanas (la firma); `items: [{titulo, texto, semanas}]`: número suelto = marca de tinta, tramo «2-6» = barra de arena, el último paso = línea añil. Sin semanas que se entiendan, filas numeradas. `nota` debajo.
- `maderas` → `maderas.astro`: foto vertical (`imagen`) y la tabla con filetes `maderas: [{nombre, uso, caracter}]` (en móvil, bloques con etiqueta).
- `opiniones` → `opiniones.astro`: la primera como frase grande, el resto en columnas; `testimonios: [{texto, autor, nota}]`. No inventes opiniones.
- `taller` → `taller.astro`: mitad texto y mitad foto (`imagen` a la derecha); `desde` («1979») en cifra grande, `titulo`, `texto` (párrafos) e `items: [{titulo, texto}]` en filas.
- `zonas` → `zonas.astro`: titular a la izquierda y localidades (`items: [{titulo, texto}]`) en filas, el nombre en Caslon; las que tienen `texto` enlazan a su página. Las primeras 8 salen también en el pie.
- `preguntas` → `preguntas.astro`: titular fijo a la izquierda con teléfono y WhatsApp y `details/summary` a la derecha. Sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: la banda añil; titular, `items` como pasos numerados, teléfono grande y `nota`; a la derecha el formulario corto y el enlace «Mandar fotos por WhatsApp». `boton_formulario` opcional.
- `contacto` → `contacto.astro`: mitad texto (titular, teléfono grande, datos de `contacto` en filas, redes) y mitad foto (`imagen`). Si `presupuesto` no está activa, a la derecha va el formulario corto en un pozo de arena.
- `texto` → `texto.astro`: apartado genérico (párrafos, `items` en filas, `cta`; con `imagen`, mitad texto y mitad foto). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Procura no poner seguidas dos secciones con foto grande (trabajos, taller, contacto) y deja `proceso` (banda de arena) y `presupuesto` (banda añil) separadas: son las dos únicas bandas de color.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. El taller habla en plural («hacemos», «montamos») y al cliente se le trata de tú.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios y cifras siempre como texto entre comillas (`"desde 6.500 €"`, `"6 a 8 semanas"`, `"Consultar"`). Las `semanas` de `proceso` son texto: «0», «1» o «2-6». Máximo 24 elementos por lista. No inventes precios, plazos, años ni opiniones que no dé el cliente.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`. En páginas que no son la portada la cabecera es sólida y deja su hueco sola.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: servicios`, `tipo: trabajos`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y `Titular`, como una banda a todo el ancho (`Banda` + contenedor, o `mitades`). `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el del menú móvil), 16 px de margen lateral del texto en móvil (`.contenedor`, `.mitad-texto`) con las fotos y fondos tocando el borde, sin scroll horizontal, botones de 44 px o más, barra inferior fija de móvil («Llamar» / «WhatsApp»: sale sola si hay teléfono o WhatsApp), todo cuadrado (radio 0) y sin sombras. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. El de presupuesto es corto a propósito (nombre, teléfono, qué necesitas; solo texto). Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos: casi no se usan (es un diseño de filetes y tipografía); los que hay están en `src/components/ui/Icono.astro` (teléfono y redes).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento y páginas por zona)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.servicios.items` → `/carpinteria/<slug>/` (servicio).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (madera, plazo, precio…) salen en la tabla de datos de la ficha.
- Zonas: cada elemento de `secciones.zonas.items` **con `texto`** (60-150 palabras: qué piezas se hacen allí, pueblos cercanos)
  tiene su página en `/zonas/<slug>/`. En la sección: `titulo_pagina` («Carpintería a medida en {zona}») y `texto_pagina` (entrada, con {zona} y {negocio}).
- Una orden «añade una página para X» = escribir su `detalle` (o el `texto` de la zona) en site.yaml. Nunca crees a mano páginas en
  `src/pages/carpinteria/` ni en `src/pages/zonas/`: salen solas de `src/pages/[coleccion]/[slug].astro` y `src/pages/zonas/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay; zonas con `areaServed`).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
