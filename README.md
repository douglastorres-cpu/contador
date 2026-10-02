# Registro de Incidencias

Marcador compartido en tiempo real para llevar el recuento de incidencias por persona en cada departamento.

## Departamentos

Sistemas, Comercial, Marketing, Captación, Ventas y Alquiler. Cada uno tiene su pestaña y la pestaña **Resumen** muestra los totales de todos.

## Uso

- **Añadir persona**: escribe el nombre en el departamento y pulsa «Añadir persona» (o Enter).
- **+1 incidencia** suma una; **−** resta una (nunca baja de 0).
- **Quitar persona** pide confirmación y borra a esa persona y su recuento.
- **Reiniciar a 0** pide confirmación y pone a cero el recuento de ese departamento (las personas se mantienen).
- Cada departamento tiene su propio enlace, por ejemplo `.../contador/#ventas`.
- «En directo», arriba a la derecha, indica que está conectado: todos los que tengan la página abierta ven los cambios al instante.

## Cómo está hecho

- `index.html` es toda la página. Se publica gratis con **GitHub Pages**.
- Los datos se guardan en **Firebase Realtime Database** (proyecto `contador-eaa71`), bajo `equipos/<departamento>/personas`.
- Las sumas son atómicas en el servidor: si dos personas pulsan a la vez, cuentan las dos.
- Para añadir un departamento nuevo hay que añadirlo en la lista `MODULES` de `index.html` y en `database.rules.json`.

## Publicar en GitHub Pages

1. El repositorio tiene que ser **público** (con cuenta gratuita de GitHub).
2. En GitHub: **Settings → Pages → Build and deployment**.
3. *Source*: **Deploy from a branch**. Elige la rama donde esté `index.html` y la carpeta `/ (root)`. Guarda.
4. En uno o dos minutos la página queda en `https://douglastorres-cpu.github.io/contador/`.

## Reglas de Firebase

En la consola de Firebase: **Realtime Database → Reglas**, sustituye el contenido por el de `database.rules.json` y pulsa **Publicar**.

Estas reglas solo dejan leer y escribir los seis departamentos, con nombres de hasta 40 caracteres y recuentos entre 0 y 100000. Cualquiera que tenga el enlace puede añadir personas y sumar o restar.
