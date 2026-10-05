# Reglas del proyecto — El Cubo de la Comunicación · Econotopía

Autor: Víctor Hugo Ramírez Salgado. Responde y escribe siempre en español.

## Privacidad (no negociable)
- La página no guarda, registra ni envía mensajes. No agregues servidor, base de datos, cookies, analíticas, publicidad ni scripts o fuentes externas.
- Conserva la etiqueta Content-Security-Policy (`connect-src 'none'`) y `referrer: no-referrer`.
- El mensaje solo viaja en el fragmento del enlace (`#m=` o `#e=`). El cifrado con contraseña (AES-256-GCM, PBKDF2-SHA-256) no se debilita ni se quita.
- `localStorage` solo puede guardar el identificador al azar de "visto una vez", nunca contenido.
- La Clave rápida &• exige contraseña y borra texto, contraseña y enlace de la pantalla después de enviar; no relajes eso.
- La traducción es la única función que envía texto fuera y siempre pide permiso antes.

## Código
- Todo vive en `index.html` (HTML, CSS y JS en un solo archivo). Sin dependencias.
- Debe funcionar en iPhone (Safari) y verse bien a 375 px de ancho.
- Mantén el nombre del autor y la clave del autor en las 6 caras.
- Actualiza `README.md` cuando cambie lo que hace la página.
- Cambios por pull request, con una explicación breve de qué cambió.
