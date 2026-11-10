# Carpintería y ebanistería: brief de diseño

Plantilla `carpinteria-madera` creada el 10/11/2026 a partir de `reformas-banos-cocinas` con `php artisan plantillas:nueva`
y rediseñada entera con el tema **Loom** de la skill Hallmark (género editorial). De la base solo queda la estructura
técnica (datos, fichas, zonas, varias páginas, SEO). Este fichero se queda en el repo: es lo que lee quien (persona o
agente) rediseñe la plantilla.

## Brief

- **Para quién**: carpinterías de madera y ebanistas (sectores `carpinteria`, `ebanisteria`, `muebles-a-medida`,
  `carpinteria-exterior`, `restauracion-muebles`): muebles a medida, cocinas y armarios empotrados, puertas y ventanas de
  madera, escaleras, tarimas, vigas y restauración. Su cliente entra para ver trabajos hechos con fotos grandes, entender
  cómo se encarga una pieza a medida (cuánto tarda, cuánto cuesta más o menos) y pedir presupuesto.
- **Qué tiene que conseguir la web**: que **pidan presupuesto** (teléfono, WhatsApp con fotos del hueco o formulario).
  «Pide presupuesto» en la cabecera y en la portada, la banda añil con el formulario, el teléfono grande en presupuesto y
  contacto y, en móvil, barra fija «Llamar / WhatsApp».
- **Tono**: de taller, sereno, exacto. Habla el taller en plural y trata al cliente de tú. Sí: el libro de muestras de un
  ebanista, la madera con luz de ventana. No: la plantilla rústica de madera con texturas de vetas dibujadas, ni la de
  reformas genérica de casco y martillo.

## Tema Hallmark y cómo se ha traducido

Loom (`references/themes/loom.md`, colourway `ecru`, postura restrained): papel crudo, tinta casi negra, Libre Caslon
Display en titulares y precios sobre Hanken Grotesk, filetes finos y un filete de tinta encima de cada lista, todo
cuadrado y plano (radio 0, sin sombras), fotos de cerca con luz de ventana y un solo añil que llega como botón, línea o
banda. El tema es de un taller de tejidos; aquí la tela es la madera: lo que en Loom es «la ficha del tejido» es la
ficha de cada pieza (madera, plazo, precio) y «el plazo en una escala» es el encargo.

- **Cuatro colores** → `fondo` = papel crudo (`#f4f0e6`, oklch 95,5 % 0,014 85), `texto` = tinta (`#1d1713`),
  `acento` = añil (`#1d3172`, oklch 34 % 0,115 267: botón, banda de presupuesto, línea de entrega, subrayado al pasar y
  foco), `primario` = nogal oscuro (`#37271d`: el pie). Loom no tiene un segundo color de banda: el nogal es la madera del
  sector y solo ocupa el pie.
- **Derivados** (`src/styles/global.css`): `--papel-2` (arena) y `--papel-3` (arena honda) toman el matiz del papel con
  `oklch(from …)`; `--filete`, `--apagado`, `--tinta-2` por mezcla de tinta y papel; `--acento-legible` (añil como texto,
  nunca más claro que L 0,45), `--acento-hover`, `--sobre-primario` y `--sobre-acento` (texto claro u oscuro según el
  color del cliente). Probado con papel blanco, tinta azul marino, acento mostaza y primario arena: la banda de
  presupuesto y el pie pasan a texto oscuro y se leen.
- **Material**: cabecera fija de papel con filete de tinta de 2 px debajo; filete de tinta de 2 px encima de cada lista
  (índice, escala, tabla, filas, preguntas, datos) y filetes finos entre filas; botón añil cuadrado + enlace con raya de
  2 px; fotos cuadradas con filete de tinta al 8 % y el tratamiento `natural sat=-12 con=-4` por CSS
  (`saturate(.88) contrast(.96)`). Movimiento quieto: solo subrayados que pasan a añil y el signo de las preguntas.
- **Firma**: «el encargo como escala de semanas» (Range de Loom, `time as a ruled scale`): en la banda de arena, cada paso
  del encargo en una fila con las semanas en DM Mono arriba; la visita y el presupuesto son marcas de tinta, el taller
  una barra de arena y el montaje la línea añil. Sale de `proceso.items[].semanas` («0», «1», «2-6»); sin semanas, los
  pasos van en filas numeradas.

## Tipografías y licencias

Libre Caslon Display 400 (Impallari Type), Hanken Grotesk 400 y 500 (Hanken Design Co.) y DM Mono 400 (Colophon
Foundry), todas **OFL-1.1**, woff2 `latin` de Fontsource en `public/fuentes/` (66 KB en total), `font-display: swap`,
respaldo del sistema de la misma clase y `preload` solo de Caslon. DM Mono es la tercera familia que el propio tema usa
para las cifras que se comparan en fila: aquí solo pinta las semanas de la escala. Detalle en `public/fuentes/LICENCIAS.md`.

Titulares sin palabras partidas (`overflow-wrap: normal`, `hyphens: manual`). En Caslon una palabra de 20 letras
(«Impermeabilizaciones») mide 7,9 em: el `h1` de la portada y de las páginas propias va con `min(5.25rem, 12.4cqi)` sobre
su columna (42 px a 375, 71 a 1440, 84 a 1920) y los `h2`, los nombres del índice, de las maderas y de las zonas no bajan
de 32 px y tienen sitio para ella (medido con Playwright a 375, 1024, 1440 y 1920). El índice pasa a cuatro columnas solo
desde 1200 px y las zonas se reparten en columnas de 17 rem como mínimo por eso mismo.

## Forma y ritmo de bandas

| # | Sección | Papel | Lleva |
|---|---|---|---|
| 1 | `hero` | papel | Stage invertido: foto a sangre a la izquierda de toda la altura con su pie debajo; texto, botones y datos en filas a la derecha |
| 2 | `servicios` | papel | índice con filetes: nombre en Caslon, frase, madera y plazo, precio en cifra (libro de muestras) |
| 3 | `trabajos` | papel | fotos grandes: dos a 8 y 4 columnas y el resto en fila, con su pie |
| 4 | `proceso` | arena | la escala de semanas (firma) |
| 5 | `maderas` | papel | foto vertical fija y la tabla de maderas con filetes |
| 6 | `opiniones` | papel | la primera como frase grande en Caslon |
| 7 | `taller` | papel | mitad texto (el año en cifra, párrafos, filas) y mitad foto a sangre |
| 8 | `zonas` | papel | localidades en filas en Caslon, con página propia |
| 9 | `preguntas` | papel | filas `details` con el teléfono y el WhatsApp al lado |
| 10 | `presupuesto` | añil | pasos numerados, teléfono grande y formulario con campos de papel |
| 11 | `contacto` | papel | teléfono grande, datos en filas y foto a sangre |
| — | pie | nogal | nombre como mástil, cuatro columnas, barra móvil |

Loom pide dos bandas de color como mucho: la arena (la escala) y el añil (el presupuesto). El ritmo lo dan las fotos y
el cambio de composición (filas, fotos, escala, tabla, frase, mitades). Dos bandas de papel seguidas no suman su aire.

## Listas propias y páginas

- `servicios.items` {titulo, texto, madera, plazo, precio, imagen, imagenes, detalle}, `trabajos.trabajos`
  {titulo, tipo, lugar, madera, texto, imagen}, `proceso.items` {titulo, texto, semanas}, `maderas.maderas`
  {nombre, uso, caracter}, `taller.items` {titulo, texto}, `presupuesto.items` {titulo, texto}.
- Campos sueltos: `hero.pie_foto`, `taller.desde`, `proceso.nota`, `presupuesto.nota`, `presupuesto.boton_formulario`.
- Fichas: cada pieza de «Lo que hacemos» con `detalle` tiene su página en `/carpinteria/<slug>/` (`Service`). Zonas: cada
  localidad con `texto`, en `/zonas/<slug>/` («Carpintería a medida en {zona}»).
- Varias páginas recomendadas: Lo que hacemos (servicios, proceso, maderas), El taller (opiniones, taller, zonas),
  Presupuesto y contacto (preguntas, presupuesto, contacto); Inicio se queda con la portada y los trabajos.
- Asistente: 13 pasos propios (taller, contacto, lo que hacéis, trabajos, cómo se encarga, maderas, historia, dónde
  montáis, preguntas, pedir presupuesto, fotos, colores y logo, repaso) más el de fichas que añade la plataforma.

## Fotos

10 fotos generadas con IA a partir de `fotos.json`: el aparador de roble en el banco (portada), cocina de roble de casa
de pueblo, armario empotrado, escalera de pino melis en casa de piedra, puerta y ventanas de castaño en fachada de
piedra, mesa de nogal, cómoda restaurada, banco de carpintero con herramientas, tablones en el secadero y manos con un
formón en una cola de milano. Sin texto, sin logotipos, sin caras. El generador da 1024×1024: se recortan al aspecto y
se amplían como mucho ×1,5 (portada 1536×1152, el resto 1280×960 o 960×1280). Por eso la portada no es una foto a
pantalla completa sino media pantalla con su pie. La portada va en 4:3 (no 16:9) porque su hueco es casi cuadrado.

## Lo que no se ha podido o choca con Hallmark

- `antetitulo` es contrato: se pinta como letra menuda en caja normal (Hallmark prohíbe el antetítulo).
- `opiniones` lleva ejemplos ficticios en el `site.yaml` de muestra (Hallmark prohíbe inventarlos); la plataforma deja la
  sección desmarcada y vacía al crear una web.
- Los `items` de la portada la plataforma los trata como cifras: no van en el guion del asistente.
- El nombre de la cabecera baja de los 32 px que pide Loom para Caslon (20 a 28 px): es una marca, no texto corrido.
- El sello de Hallmark no queda en la primera línea del CSS servido (Tailwind antepone su cabecera al ir en línea),
  `comun.css` (común a todas las plantillas) trae colores literales y etiquetas en mayúsculas que aquí se anulan, y los
  cuatro colores del cliente van en el `style` de `<html>` (contrato): sloplint los marca (20, 48, 67).
- Hallmark pide 450 palabras por página; esta pasa de 1300 con el índice, la tabla de maderas y las preguntas. Se queda
  así porque es contenido que el cliente necesita para decidir.
