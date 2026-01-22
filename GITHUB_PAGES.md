# Publicación en GitHub Pages

Esta guía explica cómo publicar la presentación en GitHub Pages.

## Configuración Inicial (Solo una vez)

### Paso 1: Habilitar GitHub Pages

1. Ve a tu repositorio en GitHub
2. Haz clic en **Settings** (Configuración)
3. En el menú lateral, busca **Pages**
4. En **Source**, selecciona **GitHub Actions**
5. Guarda los cambios

### Paso 2: Verificar el workflow

El workflow `.github/workflows/publish.yml` ya está configurado y se ejecutará automáticamente cuando:
- Hagas push a la rama `main` con cambios en `PresRep/`
- O ejecutes manualmente el workflow desde la pestaña **Actions**

## Publicación Automática

Una vez configurado, cada vez que hagas cambios en la presentación (`PresRep/intro_positron.qmd`) y hagas push a `main`:

1. El workflow se ejecutará automáticamente
2. Renderizará la presentación con Quarto
3. Publicará el HTML en GitHub Pages
4. En unos minutos, tu presentación estará disponible en:
   ```
   https://[tu-usuario].github.io/[nombre-repo]/
   ```

## Publicación Manual

Si necesitas forzar una publicación sin hacer cambios:

1. Ve a la pestaña **Actions** en tu repositorio
2. Selecciona el workflow **Publish Presentation**
3. Haz clic en **Run workflow** (botón en la parte superior derecha)
4. Selecciona la rama `main`
5. Haz clic en **Run workflow**

## Verificar el Estado

Para ver el estado de la publicación:

1. Ve a **Actions** → **Publish Presentation**
2. Revisa los logs del workflow para ver si hay errores
3. Una vez completado, ve a **Settings** → **Pages** para ver la URL de tu sitio

## Solución de Problemas

### El workflow falla

- Verifica que Quarto pueda renderizar la presentación localmente:
  ```bash
  cd PresRep
  quarto render intro_positron.qmd
  ```

### Las imágenes no se ven

- Verifica que las rutas en `intro_positron.qmd` sean relativas (ej: `Images/logo.png`)
- Asegúrate de que todas las imágenes estén en `PresRep/Images/`

### El sitio no se actualiza

- Espera unos minutos (puede tardar hasta 10 minutos)
- Verifica que el workflow se haya completado exitosamente en **Actions**
- Limpia la caché del navegador (Ctrl+F5 o Cmd+Shift+R)

## Estructura de Archivos Publicados

El workflow crea la siguiente estructura en `docs/`:

```
docs/
├── index.html              # Presentación principal
├── Images/                 # Todas las imágenes
│   ├── ATC26.png
│   └── ...
└── intro_positron_files/   # Recursos de reveal.js (si se generan)
    └── ...
```

Esta estructura se publica automáticamente en GitHub Pages.
