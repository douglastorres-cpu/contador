# Registro de Incidencias

Marcador compartido en tiempo real para llevar el recuento de incidencias por persona en cada departamento.

## Departamentos

Sistemas, Comercial, Marketing, Captación, Ventas y Alquiler. Cada uno tiene su pestaña y la pestaña **Resumen** muestra los totales de todos.

## Uso

- **Buscar persona**: el campo de arriba filtra las tarjetas del departamento por nombre.
- **Añadir persona**: abre una ventana para escribir el nombre; pulsa **Agregar**. Si ya existe alguien con ese nombre en el departamento (sin importar mayúsculas, tildes ni espacios), sale un aviso «Esta persona ya existe» y no se añade. Si estaba retirada, el aviso permite reactivarla con su histórico.
- **+1 incidencia**: abre una ventana con el campo **Razón** (opcional) y la registra con su fecha y hora.
- **−**: abre la lista numerada de incidencias de esa persona para elegir cuál quitar. Las que tienen razón se muestran con su razón; las demás como «Incidencia 1», «Incidencia 2»… La numeración se recalcula al quitar una.
- Cada tarjeta muestra el **total histórico** en grande y el contador de **Hoy**.
- **Hoy** vuelve a 0 cada día a las **00:00 hora de Perú** (UTC−5). No se borra nada: todo queda en el histórico.
- **Quitar persona** pide confirmación y la oculta del marcador, pero su histórico se conserva (aparece como «retirado»).
- **Histórico por día**: incidencias de cada persona por día. Pulsa un día para ver el detalle **por hora**.
- **Reportes**: diario, semanal (lunes a domingo) y mensual, con las flechas para ir a periodos anteriores. Muestran el total por persona y cada incidencia con su fecha, hora y razón. En **Resumen** el reporte incluye todos los departamentos.
- **Modo día / Modo noche**: el botón de arriba a la derecha cambia el tema y lo recuerda en ese navegador.
- Cada departamento tiene su propio enlace, por ejemplo `.../contador/#ventas`.
- «En directo», arriba a la derecha, indica que está conectado: todos los que tengan la página abierta ven los cambios al instante.

## Cómo está hecho

- `index.html` es toda la página. Se publica gratis con **GitHub Pages**.
- Los datos se guardan en **Firebase Realtime Database** (proyecto `contador-eaa71`):
  - `equipos/<departamento>/personas/<id>`: nombre, fecha de alta y si está activa.
  - `equipos/<departamento>/eventos/<id>`: una entrada por incidencia, con la persona, la hora del servidor y la razón (si la hay).
- Los contadores de la versión anterior (sin fecha) se convierten solos en incidencias con la razón «Registrada antes del histórico» la primera vez que se abre la página.
- Los recuentos de hoy, por día y por hora se calculan a partir de los eventos, así que no hace falta ningún proceso que «reinicie» a medianoche.
- Para añadir un departamento nuevo hay que añadirlo en la lista `MODULES` de `index.html` y en `database.rules.json`.

## Publicar en GitHub Pages

1. El repositorio tiene que ser **público** (con cuenta gratuita de GitHub).
2. En GitHub: **Settings → Pages → Build and deployment**.
3. *Source*: **Deploy from a branch**. Elige la rama donde esté `index.html` y la carpeta `/ (root)`. Guarda.
4. En uno o dos minutos la página queda en `https://douglastorres-cpu.github.io/contador/`.

## Reglas de Firebase

En la consola de Firebase: **Realtime Database → Reglas**, sustituye el contenido por el de `database.rules.json` y pulsa **Publicar**.

Estas reglas solo dejan leer y escribir los seis departamentos. Las personas no se pueden borrar (solo retirar) y las incidencias solo se pueden crear o quitar, no modificar. Cualquiera con el enlace puede quitar incidencias (de cualquier día) desde el botón −. Cualquiera que tenga el enlace puede añadir personas y registrar incidencias.
