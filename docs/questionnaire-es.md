# Flujo del Cuestionario

Haz las preguntas de forma conversacional por rondas. No leas este archivo en voz alta — usalo como guia. Adapta las frases para que se sientan naturales. Despues de cada ronda, resume lo que escuchaste antes de avanzar.

---

## Ronda 0: Objetivo y Marca (SIEMPRE primero)

Esta ronda va antes que todo. Lo que salga aqui condiciona las dos decisiones grandes
del proyecto: el **objetivo** determina el arquetipo de pagina (Fase 4) y la **marca**
determina el sistema de diseno (Ronda 2 y Fase 2). Preguntar esto al final significa
inventar una paleta que despues hay que tirar.

**0.1 Para que es esta pagina? Que tendria que pasar para que digas que funciono?**
   - Es el objetivo de negocio, no el giro. "Soy dentista" no es respuesta; "quiero que
     me agenden cita" si.
   - Si la respuesta es vaga, insiste una vez: "En tres meses, que quieres poder contar?"
   - Obligatorio. Sin default — de aqui sale el arquetipo.

   Mapeo objetivo -> arquetipo (`docs/landing-page-patterns.md`):

   | Lo que quiere | Arquetipo |
   |---|---|
   | Que me contacten, agenden o coticen | Conversion-Optimized |
   | Vender un producto directo | Hero-Centric |
   | Validar una idea antes de construirla | Minimal |
   | Que me contraten (portafolio, freelance) | Storytelling |
   | Que confien en mi (legal, salud, finanzas) | Trust & Authority |
   | Competir contra alternativas conocidas | Social-Proof-Heavy |
   | Explicar un producto que no se entiende solo | Interactive Demo o Feature-Rich |

**0.2 Tienes manual de marca, brand guideline o algo que defina tus colores y tipografias?**
   - Acepta: PDF, ruta de archivo, link de Figma, link de Notion, o "no".
   - Si es un PDF local: leelo con la herramienta Read (soporta PDF).
   - Si es una URL: usa el skill `web-reader`.
   - Extrae y anota: codigos hex, nombres de tipografias, tono de voz, reglas del logo.
   - **Si el usuario tiene marca definida, esos valores MANDAN sobre `ui-ux-pro-max`.**
     No inventes una paleta encima de una marca que ya existe.
   - Default: no tiene -> la Ronda 2 arma el sistema desde cero.

**0.3 Tienes una carpeta con tus activos visuales — logo, fotos, iconos?**
   - Pide la **ruta de la carpeta**, no archivos sueltos. Es lo normal: la gente tiene
     una carpeta "Marca" o "Logos", no rutas memorizadas archivo por archivo.
   - Escanea lo que te den: `ls -R "<ruta>"`
   - Reporta que encontraste antes de seguir: "Vi 3 logos, 12 fotos y un favicon."
   - Marca cuales sirven: logo en SVG o PNG con transparencia, fotos de 1200px o mas.
   - En la Fase 4 copialos a `site/public/images/`.
   - Si contesta esto, las preguntas 14, 15 y 16 de la Ronda 4 ya estan respondidas —
     no las repitas, solo confirma lo que encontraste.
   - Default: no tiene.

**0.4 Donde vive tu marca hoy?** (pregunta esto SOLO si 0.2 y 0.3 salieron vacias)
   - "Tus colores, logos o fotos estan en Canva, Google Drive, Notion, Figma o Dropbox?"
   - Si nombra una herramienta y hay un MCP conectado en la sesion, jala de ahi en vez
     de pedirle que te describa la marca de memoria:
     - **Canva** -> `list-brand-kits` trae paleta y tipografias del brand kit
     - **Google Drive** -> `search_files` para el logo y las fotos
     - **Notion** -> `notion-search` para copy, textos o el brief que ya tenga escrito
     - **Figma** -> pide el link publico del archivo y usa `web-reader`
   - Si nombra una herramienta y NO hay MCP conectado, dilo sin drama: "No tengo Canva
     conectado en esta sesion. Puedes conectarlo, o pasarme los archivos directo."
   - No conviertas esto en una conversacion tecnica. El usuario no tiene que saber que
     es un MCP — solo dice donde estan sus cosas y tu ves si puedes llegar ahi.
   - Default: saltar.

**0.5 Esta pagina se tiene que conectar con algo que ya usas?**
   - Da ejemplos, no una lista tecnica: "Tienda en linea, agenda de citas, tu CRM, lista
     de correos, cobros, analytics?"
   - Si dice que si, pregunta **donde** vive eso — "Shopify", "Calendly", "Stripe" — y
     nada mas. Los detalles de implementacion los resuelves tu con `docs/integrations.md`.
   - Lee `docs/integrations.md` antes de prometer nada. Fija los cuatro niveles (A: link,
     B: jalar datos al construir, C: widget del proveedor, D: API en vivo) y cual aplica
     a cada integracion. **El nivel D queda fuera del alcance de este repo** — si alguien
     lo necesita de verdad, dilo claro y ofrece B o C.
   - **Nunca digas "conecte tu pagina por MCP".** Un MCP es una herramienta que TU usas
     al construir; la pagina publicada no habla con ningun MCP. Si jalaste el catalogo de
     Shopify, di eso: "Lei tu tienda y puse tus 6 productos en la pagina."
   - No pidas llaves secretas ni tokens de admin. Ningun nivel A, B o C los necesita.
   - Esto afecta el arquetipo y las secciones: una pagina con catalogo de productos no se
     parece a una de captacion de leads. Tenlo presente en la Q0.1 y en la Fase 4.
   - Default: no se conecta con nada. La mayoria de las landing pages no lo necesitan.

Despues de la Ronda 0, resume lo que tienes: "Ok — la pagina es para [objetivo], y
[tengo tu marca / la armo yo]. Ahora lo basico del negocio."

---

## Ronda 1: Lo Basico (siempre preguntar)

1. **Como se llama tu negocio o proyecto?**
   - Obligatorio. Sin default.

2. **En una oracion, a que se dedican?**
   - Default: Inferir del nombre y el contexto.

3. **A quien quieres llegar?**
   - Default: "Audiencia general"
   - Si es vago, pregunta: "Son mas bien profesionales jovenes, familias, duenos de negocios...?"

Despues de la Ronda 1, resume: "Perfecto — [negocio] ayuda a [audiencia] con [servicio]. Ahora te pregunto sobre el look y la onda."

---

## Ronda 2: Direccion Visual

**Antes de preguntar nada aqui, revisa que salio de la Ronda 0.**

- **Si el usuario tiene marca definida** (0.2 o 0.4 dieron colores y tipografias): NO
  inventes nada. Las preguntas 5 y 7 se vuelven una confirmacion, no una eleccion:
  "Tu manual usa #1B3A5C y Söhne. Los aplico tal cual — quieres que proponga algo para
  lo que falte?" Corre `ui-ux-pro-max` unicamente para los huecos: si trae paleta pero
  no tipografias, busca solo tipografias que combinen con esa paleta.
- **Si no tiene marca**: sigue las preguntas como estan escritas abajo y arma el sistema
  desde cero.

Sustituir una marca que ya existe por una paleta generada es el peor error que puedes
cometer en esta fase. El usuario no siempre te va a corregir — a veces solo se va.

4. **Tienes alguna pagina web que te guste como se ve?**
   - Si tiene: Usa el skill `web-reader` para analizarla. Nota colores, layout, tipografia, vibra.
   - Default: Saltar, elegir basado en la industria.

5. **Tienes preferencia de colores, o quieres que yo elija basado en tu industria?**
   - **Si la Ronda 0 ya dio la paleta de marca, salta esta pregunta y confirma.**
   - Default: Usa `ui-ux-pro-max`. Corre: `python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<industria>" --domain color`
   - Si falla la busqueda: Elige basado en las normas de la industria en `docs/design-guide.md`.

6. **Tema claro u oscuro?**
   - Default: Claro.

7. **Que onda o sensacion deberian tener los visitantes?**
   - Ofrece opciones: profesional, jugueton, audaz, elegante, minimalista, calido, moderno, atrevido, lujoso.
   - Default: "Profesional y accesible."

Despues de la Ronda 2, **PAUSA y presenta la direccion de diseno**: "Mira, esto es lo que estoy pensando — [paleta de colores con codigos hex], [combinacion de fuentes con nombres], [enfoque general del layout]. Te late?"

**Espera la aprobacion del usuario antes de continuar a la Ronda 3.** Si el usuario quiere cambios, ajusta y vuelve a presentar hasta que apruebe. Esto asegura que las preguntas de contenido esten informadas por el diseno aprobado.

---

## Ronda 3: Contenido

8. **Cual es la accion principal que quieres que hagan los visitantes?**
   - Ejemplos: registrarse, agendar una llamada, comprar algo, saber mas, pedir una cotizacion.
   - Default: "Saber mas / ponerse en contacto."

9. **Cuales son 3-4 cosas clave que quieras destacar?**
   - Estas se convierten en la seccion de servicios/caracteristicas.
   - Default: Generar de la descripcion del negocio + normas de la industria.

10. **Quieres un formulario de contacto en la pagina?**
    - Si quiere: Que campos? (Nombre, email, mensaje es lo estandar. Telefono? Empresa?)
    - Opciones:
      - **Simple (default):** Un enlace "mailto:" con estilo de seccion de contacto — no necesita backend.
      - **Formulario con Formspree:** Servicio gratuito, sin backend. Dile al usuario: "Ve a formspree.io, crea una cuenta gratis, crea un formulario, y dame el form ID (se ve asi: 'xpznqkdl')." Si no quiere hacerlo ahora, usa mailto: como default y deja un comentario TODO.
    - Si solo quiere un link de email o telefono, tambien funciona.

11. **Tienes un eslogan o frase?**
    - Default: Escribir uno. Pasar por humanizer.

12. **Tienes testimonios, resenas o prueba social?**
    - Default: Crear una seccion de testimonios con placeholders. Usar nombres realistas pero claramente de ejemplo.

13. **Tienes redes sociales para incluir?**
    - Instagram, X/Twitter, Facebook, LinkedIn, TikTok, YouTube, etc.
    - Default: Iconos de redes sociales en el footer como placeholder — el usuario llena las URLs despues.

Despues de la Ronda 3, resume: "Ya tengo todo lo que necesito para el contenido. Unas preguntas tecnicas rapidas."

---

## Ronda 4: Tecnico (breve)

**Si la Ronda 0 ya te dio una carpeta de assets, las preguntas 14, 15 y 16 ya estan
respondidas.** No las repitas — confirma lo que encontraste: "Del logo uso el SVG, y
de las fotos me quedo con estas tres para el hero y servicios. Te parece?"

14. **Tienes un logo?**
    - Acepta: ruta de archivo, URL, o "no"
    - Default: Logo de solo texto usando el nombre del negocio con la fuente del titulo.

15. **Tienes imagenes especificas que quieras usar?**
    - Acepta: rutas de archivo, URLs, o "no"
    - Formatos aceptados: JPG (fotos), PNG (logos con transparencia), SVG (iconos/logos), WebP (compresion moderna)
    - Si da URLs, descargarlas: `curl -o site/public/images/foto.jpg "URL"`
    - Default: Sin fotos de stock. Usar patrones geometricos, gradientes o elementos decorativos abstractos que combinen con el sistema de diseno.

16. **Tienes un favicon (el iconito pequeno en la pestana del navegador)?**
    - Acepta: ruta de archivo, URL, o "no"
    - Default: Generar un favicon simple con los colores de la marca usando `site/src/app/icon.tsx`.

17. **En que idioma quieres la pagina?**
    - Default: Mismo idioma en el que el usuario ha estado hablando.
    - Nota: Todo el contenido (titulos, texto, CTAs, meta tags) sera en el idioma elegido.

18. **Quieres que lo suba a una URL en vivo cuando terminemos?**
    - Explica: "Puedo subirlo a Vercel — te doy un link que puedes compartir con quien quieras."
    - Default: Si.

---

## Cuando dice "No se" / "Tu decide"

Cuando el usuario deja una decision en tus manos:
- **Colores**: Correr ui-ux-pro-max color search para su industria + vibra.
- **Fuentes**: Correr ui-ux-pro-max typography search para su keyword de vibra.
- **Texto**: Generar basado en sus respuestas, pasar por humanizer.
- **Layout**: Usar el orden probado: Hero > Servicios > Prueba Social > CTA > Footer.
- **Estilo**: Combinar con su industria: firma de abogados = refinado/serif, startup tech = limpio/moderno, restaurante = calido/organico, agencia creativa = audaz/experimental.
- **Formulario de contacto**: Usar un enlace mailto: con estilo de seccion de contacto.
- **Redes sociales**: Agregar iconos placeholder en el footer.

Siempre dile al usuario lo que elegiste y por que, brevemente: "Fui con una paleta calida — terracota y blanco hueso — porque va bien con el mundo de la comida artesanal."

---

## Despues de Todas las Rondas

Resume el brief completo para el usuario:
- **Objetivo de la pagina** y el arquetipo que sale de el
- **Origen de la marca**: manual del usuario, jalada de Canva/Drive/Notion, o disenada por ti
- Nombre y descripcion del negocio
- Audiencia objetivo
- Direccion de diseno (colores, fuentes, vibra)
- CTA principal
- Metodo de contacto (formulario, mailto, telefono)
- Secciones/servicios clave
- Redes sociales
- Assets (logo, imagenes, favicon, o defaults)
- Idioma de la pagina
- Deploy: si/no

Pregunta: "Esto cubre todo? Empiezo a construir en cuanto me des luz verde."

Despues procede a la Fase 2 (Sistema de Diseno) en el flujo de CLAUDE.md.
