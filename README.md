# Mis Bicis — mantenimiento de bicicletas (PWA)

App web instalable para Android. Sin servidor, sin cuentas: todo se guarda en el móvil.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Toda la app (HTML + CSS + JS) |
| `manifest.webmanifest` | Hace que Android la trate como app instalable |
| `sw.js` | Service worker: cachea la app para funcionar offline |
| `icon-192.png`, `icon-512.png` | Icono |

## Funciones

- **Varias bicis** con ficha (tipo, marca, notas, km totales).
- **Kilómetros a mano**: sumar los km de una salida o fijar el total del cuentakilómetros.
- **Tareas de desgaste** con intervalo por km y/o por días (cadena, pastillas, purga de frenos…). Barra de progreso y aviso
  "Pronto" al 80 % y "¡Toca ya!" al 100 %. Al crear una bici se generan unas tareas por defecto que puedes editar o borrar.
- **Historial de mantenimientos** con fecha, km, coste y notas. Al registrar uno puedes elegir qué tarea reinicia.
  Desde una tarea hay un atajo "Hecho hoy → registrar mantenimiento".
- **Exportar / importar JSON** (Ajustes ⚙️) para copia de seguridad o cambio de móvil.

## Cómo ponerla en el móvil

Para que se instale como app y funcione offline tiene que servirse por **HTTPS**. La forma más sencilla y gratis:

### Opción A — GitHub Pages (recomendada)

1. Crea un repositorio en GitHub (por ejemplo `bicis-app`) y sube estos archivos a la raíz.
2. En el repo: *Settings → Pages → Source: Deploy from a branch → main / (root)* → Save.
3. En un minuto tendrás `https://TU_USUARIO.github.io/bicis-app/`.
4. Ábrela en **Chrome** en el móvil → menú ⋮ → **"Instalar aplicación"** (o "Añadir a pantalla de inicio").

Cada vez que cambies algo, sube los archivos y sube el número de versión en `sw.js` (`misbicis-v1` → `v2`) para que el móvil refresque la caché.

### Opción B — Netlify Drop

Entra en <https://app.netlify.com/drop>, arrastra la carpeta `bicis-app` y te da una URL HTTPS al instante.

### Opción C — Sin subir nada (prueba rápida)

Copia la carpeta al móvil y abre `index.html` con Chrome. Funciona y guarda datos, pero no se instala como app ni
tiene icono (el service worker no corre en `file://`).

## Probarla en el PC

Abre `index.html` directamente en el navegador. Con las herramientas de desarrollador (F12 → modo móvil) la ves como en el teléfono.

## Datos

Se guardan en `localStorage` del navegador bajo la clave `misbicis-v1`. Si borras los datos de Chrome se pierden:
**exporta el JSON de vez en cuando**.

## Convertirla en APK (futuro)

Si algún día quieres un `.apk` de verdad, la misma app se empaqueta con [PWABuilder](https://www.pwabuilder.com/) o
[Bubblewrap](https://github.com/GoogleChromeLabs/bubblewrap) a partir de la URL publicada, sin tocar el código.
