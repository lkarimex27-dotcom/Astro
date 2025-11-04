# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Descripción del Proyecto

Este es un sitio web en español para "Hector's Whips," un servicio de alquiler de vehículos de lujo en Spokane. El sitio está construido con Astro y Tailwind CSS v4.

## Comandos de Desarrollo

```bash
# Instalar dependencias (requerido antes del primer uso)
npm install

# Iniciar servidor de desarrollo
npm run dev

# Compilar para producción
npm run build

# Previsualizar compilación de producción
npm run preview
```

## Arquitectura

### Configuración del Framework
- **Astro 5.14.7** con integración de Tailwind CSS 4.1.16
- Tailwind está integrado vía plugin de Vite (`@tailwindcss/vite`) configurado en `astro.config.mjs`
- Usa el sistema de enrutamiento basado en archivos de Astro con componentes `.astro`

### Estructura de Directorios
- `layouts/layout.astro` - Layout principal (importa estilos globales y componente Header)
- `src/pages/` - Enrutamiento basado en archivos (index.astro es la página principal)
- `src/components/` - Componentes Astro reutilizables (hero.astro, header.astro)
- `src/styles/` - Archivos CSS globales
  - `global.css` - Importaciones de Tailwind y utilidades personalizadas (botones, hero, estilos del header)
  - `estilos-nativos.css` - Estilos nativos adicionales
- `public/` - Archivos estáticos (imágenes: HW-Logo.webp, carros.png, favicon.svg)

### Patrones Clave

**Sistema de Layout:**
El layout raíz (`layouts/layout.astro`) importa los estilos globales y el componente Header. Las páginas importan este layout y pasan contenido mediante slots. Nota: `index.astro` actualmente importa Header dos veces (una desde el layout, otra directamente) - esto debería eliminarse de la página.

**Arquitectura de Componentes:**
- Los componentes son archivos `.astro` puros con frontmatter para la lógica
- El componente Header incluye JavaScript inline para el toggle del menú móvil
- La sección Hero usa utilidades de Tailwind extensivamente

**Enfoque de Estilos:**
- Usa la directiva `@layer` de Tailwind para las capas base, component y utilities
- Componentes de botón personalizados (`.btn`, `.btn-white`, `.btn-outline`) con diseño diagonal sesgado
- Fondos degradados de negro a rojo (`from-black via-[#2b0000] to-[#8b0000]`)
- Diseño responsivo con breakpoints mobile-first

**Idioma y Contenido:**
Todo el contenido está en español - mantén esto al agregar o editar texto.

## Detalles Técnicos Importantes

**Rutas de Imágenes:** El componente header hace referencia a imágenes con el prefijo `public/` (`public/HW-Logo.webp`), pero Astro sirve los archivos públicos desde la raíz. Actualiza las rutas de imágenes a `/HW-Logo.webp` si las imágenes no cargan correctamente.

**Tailwind v4:** Este proyecto usa Tailwind CSS v4 que tiene una configuración diferente a v3. La sintaxis `@import "tailwindcss"` en `global.css` es el enfoque de v4 (no las importaciones base/components/utilities de v3).

**Menú Móvil:** El header incluye un menú móvil deslizante con JavaScript inline usando la directiva `is:inline` para evitar que Astro lo procese.

**Efecto Diagonal Sesgado:** La clase personalizada `.boton-diagonal` aplica `skew(-22deg)` con un span interno que lo revierte mediante `skew(22deg)` para un estilo de botón único.
