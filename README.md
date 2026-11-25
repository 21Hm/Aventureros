# 🌹 Los Aventureros · CDMX

Itinerario del viaje a CDMX (The Romantic World Tour) en forma de web app: carrusel de actividades, timeline, calificaciones, fotos por actividad y edición de pendientes (TBD).

- **Interfaz:** `index.html` en GitHub Pages.
- **Datos:** la hoja de Google "Itinerario The Romantic World Tour CDMX", leída y escrita por un script de Apps Script (`apps-script/`).

```
index.html              ← la app
manifest.webmanifest    ← para "Agregar a pantalla de inicio"
icon-192.png, icon-512.png, apple-touch-icon.png
apps-script/
  Codigo.gs             ← API: lee/escribe la hoja, carpetas de Drive, fotos
  Logica.gs             ← convierte las filas en actividades y traslados
  appsscript.json       ← manifiesto (activa la API de Google Sheets)
```

---

## Parte 1 · Apps Script (el "motor")

1. Abre la hoja → **Extensiones → Apps Script**.
2. **Código.gs**: borra todo y pega `apps-script/Codigo.gs`.
3. **Logica.gs**: si no existe, **＋ → Secuencia de comandos** → nombre `Logica` → pega `apps-script/Logica.gs`.
4. Si hay un archivo **Index.html**, bórralo (ya no se usa): menú ⋮ junto al archivo → Eliminar.
5. Engrane ⚙️ **Configuración del proyecto** → activa **"Mostrar el archivo de manifiesto appsscript.json"**. Abre `appsscript.json` y pega `apps-script/appsscript.json`.
6. Guarda (Ctrl/Cmd + S). Cambia el nombre del proyecto arriba a "Los Aventureros" (opcional).
7. En el selector de funciones elige **prepararApp** → **Ejecutar**.
   Google pedirá permisos: *Revisar permisos* → tu cuenta → *Configuración avanzada* → *Ir a Los Aventureros (no seguro)* → **Permitir**.
   Al terminar verás en la hoja: IDs en la columna N, links "📷 Fotos" en la columna L y una carpeta nueva en tu Drive.
8. **Implementar → Nueva implementación** → ⚙️ **Aplicación web**
   - Ejecutar como: **Yo**
   - Quién tiene acceso: **Cualquier persona**
9. **Implementar** → copia la **URL de la aplicación web** (termina en `/exec`).
10. Pruébala: ábrela en el navegador. Debe decir `{"ok":true,"app":"Los Aventureros",...}`.

> Si después cambias `Codigo.gs` o `Logica.gs`: **Implementar → Administrar implementaciones → ✏️ → Versión: Nueva versión → Implementar**. La URL no cambia.

## Parte 2 · GitHub Pages (la app)

1. En `index.html` busca la línea:
   ```js
   var API_URL = 'PEGA_AQUI_LA_URL_DE_APPS_SCRIPT';
   ```
   y pega tu URL `/exec` entre las comillas (en este zip ya está configurada).
2. En GitHub crea un repositorio nuevo (ej. `los-aventureros`) y sube **todos los archivos de esta carpeta** (Add file → Upload files → arrastra todo, incluida la carpeta `apps-script`).
3. Repositorio → **Settings → Pages** → *Source:* **Deploy from a branch** → *Branch:* `main` / `(root)` → **Save**.
4. En 1–2 minutos tu app estará en `https://TU-USUARIO.github.io/los-aventureros/`.
5. En el iPhone: abre el link en Safari → Compartir → **Agregar a pantalla de inicio**. En Android: menú ⋮ → **Instalar app**.

## Notas
- **Privacidad:** GitHub Pages gratis requiere repositorio **público**, así que la URL del API queda visible en `index.html`. Quien la tenga podría leer el itinerario o escribir en él (igual que con el link de la app). No compartas el link del repo; si quieres más privacidad, usa un repo privado con GitHub Pro.
- **Sin señal:** la app guarda la última versión del itinerario en el teléfono y la muestra si no hay internet (calificar y subir fotos sí requieren conexión).
- **Portadas:** columna **M** de la hoja, con link directo a imagen (.jpg/.png/.webp) o link de archivo de Drive compartido como "Cualquier persona con el vínculo".

### Columnas que usa la app
| Col | Qué es | Quién la llena |
|---|---|---|
| A | ✓ Hecha | La app |
| K | Notas | Tú o la app |
| L | Carpeta de fotos | La app |
| M | Portada (URL) | Tú |
| N | ID app — no tocar | La app |
| O | Lugar (app) para TBD | La app |
| P | Calificación promedio | La app |

Además se crea la pestaña **Calificaciones** (una fila por persona y actividad).
