# 💩 Contador de Cagadas

Marcador compartido en tiempo real para llevar la cuenta de quién la ha cagado más veces mientras trabajamos.

Participantes: **Walter**, **Cesar** y **peterGAYmer**.

## Cómo funciona

- `index.html` es toda la página. Se publica gratis con **GitHub Pages**.
- Los números se guardan en **Firebase Realtime Database** (proyecto `contador-eaa71`), así que todos los que abren la página ven el mismo marcador y se actualiza al instante.
- **+1 cagada** suma de forma atómica en el servidor: si dos personas pulsan a la vez, cuentan los dos clics.
- **−** resta una (nunca baja de 0).
- **Reiniciar a 0** pide confirmación y pone el marcador a cero para todos.
- Arriba a la derecha, «En directo» indica que está conectado a la base de datos.

## Publicar en GitHub Pages

1. El repositorio tiene que ser **público** (con cuenta gratuita de GitHub).
2. En GitHub: **Settings → Pages → Build and deployment**.
3. *Source*: **Deploy from a branch**. Elige la rama donde esté `index.html` y la carpeta `/ (root)`. Guarda.
4. En uno o dos minutos la página queda en `https://douglastorres-cpu.github.io/contador/`.

## Reglas de Firebase

El «modo de prueba» de Firebase deja de funcionar a los 30 días. Para que siga funcionando:

1. En la consola de Firebase: **Realtime Database → Reglas**.
2. Sustituye el contenido por el de `database.rules.json` y pulsa **Publicar**.

Estas reglas dejan leer y escribir solo el marcador (`/contador`), solo para los tres nombres y solo con números entre 0 y 100000. Cualquiera que tenga el enlace puede sumar y restar.

## Versión de claude.ai

`artifact/contador.html` es una versión alternativa publicada como Artifact de claude.ai
(https://claude.ai/artifact/8m3ctxcWxp5P69D83VTcbU). Usa la base de datos de claude.ai en lugar de Firebase y requiere que cada persona tenga cuenta de claude.ai.
