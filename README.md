# Neko Roble Café 🐾

Sitio de una sola página (HTML + CSS + JS embebidos) para una cafetería temática
de gatos en la Colonia Escalón, San Salvador.

**En vivo:** https://lemichiw-cyber.github.io/neko-robles-cafe/

## Reservas reales (sin backend)

GitHub Pages no tiene servidor, así que el formulario **no envía nada por sí solo**:
valida los datos y abre WhatsApp con el mensaje ya escrito hacia el teléfono del
café. También ofrece un enlace de correo como alternativa.

1. Se rellena el formulario (nombre, correo, fecha, hora, personas…).
2. Se comprueba la fecha: no acepta lunes (día cerrado), fechas pasadas ni más de
   90 días de antelación, y se muestra el horario real de ese día.
3. Al enviar se abre WhatsApp con el mensaje formateado. Si el navegador bloquea
   la ventana, quedan dos botones: **Enviar por WhatsApp** y **Enviar por correo**.

### Cambiar el teléfono o el correo

Todo el contacto real vive en un único bloque al principio del JavaScript, dentro
de `index.html`:

```js
var CONTACTO = {
  whatsapp: "50379980884",     // solo dígitos, con prefijo de país
  telefono: "+50379980884",
  email: "sakuraenterprise2@gmail.com"
};
```

Además hay que actualizar los mismos datos en:

- los enlaces `tel:` y `mailto:` del pie y de la sección de contacto,
- el bloque JSON-LD (`telephone`, `email`) del `<head>`,
- el texto visible `+503 7998 0884`.

### Cambiar el horario

El horario que se valida en el formulario está en `HORARIOS` (mismo script):

```js
var HORARIOS = {
  0: { abre: "11:00", cierra: "19:00" }, /* domingo */
  1: null,                              /* lunes: cerrado */
  // ...
};
```

Debe coincidir con la tabla de la sección de contacto y con `openingHoursSpecification`
del JSON-LD.

## Estructura

```
index.html          sitio completo (estilos, SVG y JS embebidos)
img/                og-neko-robles.jpg + iconos de la PWA
robots.txt          permisos para rastreadores
sitemap.xml         sitemap con la única página
site.webmanifest    manifest de instalación
```

Las fotos del local aún no existen: el sitio usa ilustraciones SVG propias. Los
comentarios del código marcan dónde van (`img/mochi.jpg`, `img/tofu.jpg`,
`img/hero-cafe.jpg`…). La tarjeta social se genera en `img/og-neko-robles.jpg`
(1200×630).

## Cómo publicar

El repositorio publica `main` directamente con GitHub Pages. Basta con hacer
`git push` y esperar un minuto.

## Comprobaciones hechas

- Sin desplazamiento horizontal a 1440, 390, 360 y 320 px.
- Menú móvil accesible: abre/cierra con Escape, `aria-expanded` correcto y los
  enlaces ocultos no son enfocables con el teclado.
- Formulario: validación de fecha, horario y lunes cerrado; el mensaje de
  WhatsApp contiene todos los datos de la reserva.
- Sin errores de consola.
