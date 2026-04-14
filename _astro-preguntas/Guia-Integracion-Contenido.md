# Guía de Integración de Contenido para Proyecto Astro

**Versión:** 1.0  
**Basado en:** Skill astro-docs + Estructura actual del proyecto reaprovechador  
**Última actualización:** Marzo 2026

---

## Índice de Contenido

1. [1. Cómo indicar el logo a sustituir](#1-cómo-indicar-el-logo-a-sustituir)
2. [2. Cómo indicar la estructura de páginas](#2-cómo-indicar-la-estructura-de-páginas)
3. [3. Cómo indicar el menú relacionado con las páginas](#3-cómo-indicar-el-menú-relacionado-con-las-páginas)
4. [4. Cómo pasar el contenido de las páginas y secciones](#4-cómo-pasar-el-contenido-de-las-páginas-y-secciones)
5. [Información de referencia del proyecto actual](#información-de-referencia-del-proyecto-actual)

---

## 1. Cómo indicar el logo a sustituir

### Ubicación actual del logo

El logo se encuentra en el componente **`reaprovechador/src/components/Logo.astro`**

```astro
---
import { SITE } from 'astrowind:config';
---

<span
  class="self-center ml-2 rtl:ml-0 rtl:mr-2 text-2xl md:text-xl font-bold text-gray-900 whitespace-nowrap dark:text-white"
>
  🚀 {SITE?.name}
</span>
```

Actualmente es texto con emoji.

### Cómo indicarme el nuevo logo

**Requiero que me proporciones:**

1. **El archivo del logo**
   - Formato de archivo: SVG (preferido para escalabilidad), PNG, JPG, WEBP
   - Dimensiones aproximadas: Mínimo 40px altura (para header responsive)
   - Comparte el archivo o describe dónde descargarlo

2. **La instrucción clara**
   - Ejemplo: *"Cambia el logo actual por el archivo `logo-nuevo.svg` que adjunto"*
   - Indica si el logo debe ser un `<img>`, un `<svg>` inline, o un componente simple

3. **Preferencias de tamaño y posicionamiento**
   - ¿Alto en desktop? (ej: 50px, 60px)
   - ¿Alto en móvil? (ej: 40px)
   - ¿Debe tener margen o padding adicional?
   - ¿El logo clickeable debe ir a la home?

### Lo que haré

- Colocaré el archivo en `reaprovechador/public/images/` o `reaprovechador/src/assets/images/`
- Modificaré `Logo.astro` para renderizar la imagen con las dimensiones y estilos especificados
- Actualizaré los estilos responsive si es necesario

### No especules

- **No asumas** tamaños o colores que no hayas confirmado
- **No inventes** formatos de archivo
- **Proporciona el archivo actual o un enlace** donde descargarlo

---

## 2. Cómo indicar la estructura de páginas

### Estructura actual del proyecto

Las páginas se encuentran en `reaprovechador/src/pages/`:

```
pages/
  ├── index.astro              (Home/Inicio)
  ├── about.astro              (Acerca de)
  ├── contact.astro            (Contacto)
  ├── services.astro           (Servicios)
  ├── pricing.astro            (Precios)
  ├── privacy.md               (Política de privacidad)
  ├── terms.md                 (Términos)
  ├── 404.astro                (Página no encontrada)
  ├── rss.xml.ts               (Feed RSS)
  ├── [...blog]/               (Rutas dinámicas para blog)
  ├── homes/                   (Ejemplos de diferentes plantillas)
  └── landing/                 (Ejemplos de landing pages)
```

### Cómo indicarme la nueva estructura

**Proporciona una lista clara con:**

1. **Nombre de la página** (ej: "Inicio", "Productos")
2. **Ruta deseada** (ej: `/`, `/productos`, `/productos/categoria`)
3. **Tipo de página:**
   - Estática (archivo `.astro` simple)
   - Con contenido dinámico (requiere fetching de datos)
   - Colección de contenido (blog, galería, productos)
4. **Secciones que contendrá** (ver sección 4)

### Ejemplo de formato que entiendo

```markdown
**Nueva estructura:**
- Inicio → `/` → Estática (Hero, Características, CTA)
- Productos → `/productos` → Colección dinámica (listado de productos)
- Detalle Producto → `/productos/[id]` → Ruta dinámica
- Sobre nosotros → `/sobre` → Estática (Historia, equipo, valores)
- Blog → `/blog` → Colección dinámica (lista de posts)
- Post individual → `/blog/[slug]` → Ruta dinámica
- Contacto → `/contacto` → Formulario
```

### Lo que haré

1. Crearé los archivos `.astro` o `.md` en `src/pages/` con la estructura correcta
2. Configuraremos rutas dinámicas si aplica (ej: `/productos/[id].astro`)
3. Actualizaré la configuración de routeo en `astro.config.ts` si hay requisitos especiales

### No especules

- **No asunas** URLs o struturas
- **No improvises** rutas dinámicas
- **Define claramente** si cada página es estática o dinámica
- **Indica las colecciones** si hay datos que varían (blog, productos, etc.)

---

## 3. Cómo indicar el menú relacionado con las páginas

### Ubicación actual del menú

El menú está definido en `reaprovechador/src/navigation.ts`:

```typescript
export const headerData = {
  links: [
    {
      text: 'Homes',
      links: [
        { text: 'SaaS', href: '/homes/saas' },
        { text: 'Startup', href: '/homes/startup' },
        // etc...
      ],
    },
    {
      text: 'Pages',
      links: [
        { text: 'Services', href: '/services' },
        { text: 'Pricing', href: '/pricing' },
        // etc...
      ],
    },
    // más secciones...
  ]
};
```

El menú se consume en layouts/componentes header y está estructurado jerárquicamente.

### Cómo indicarme el nuevo menú

**Proporciona la estructura completa en formato texto o JSON:**

```json
{
  "links": [
    {
      "text": "Inicio",
      "href": "/"
    },
    {
      "text": "Servicios",
      "href": "/servicios"
    },
    {
      "text": "Productos",
      "links": [
        { "text": "Electrónica", "href": "/productos/electronica" },
        { "text": "Ropa", "href": "/productos/ropa" },
        { "text": "Deportes", "href": "/productos/deportes" }
      ]
    },
    {
      "text": "Blog",
      "href": "/blog"
    },
    {
      "text": "Contacto",
      "href": "/contacto"
    }
  ]
}
```

**O en formato texto claro:**

```
Menú principal:
- Inicio (/)
- Servicios (/servicios)
- Productos (/productos)
  - Electrónica (/productos/electronica)
  - Ropa (/productos/ropa)
  - Deportes (/productos/deportes)
- Blog (/blog)
- Contacto (/contacto)
```

### Elementos que puedo configurar

- **text**: Texto visible en el menú
- **href**: URL de destino (debe coincidir con tus páginas)
- **links**: Submenú (desplegable)
- **icon** (opcional): Ícono asociado
- **target** (opcional): `_blank` para abrir en pestaña nueva
- **badge** (opcional): Etiqueta como "Nuevo", "Popular"

### Requisitos para el menú

1. **Las URLs deben existir** como páginas en `src/pages/`
2. **Los submenús** se especifican con `links: [...]`
3. **No pueden haber rutas rotas** - cada href debe apuntar a una página válida

### Lo que haré

1. Actualizaré `navigation.ts` con la nueva estructura
2. Verficaré que todas las URLs correspondan a páginas existentes
3. Configuraremos estilos responsive si es necesario

### No especules

- **No inventes** rutas o menús
- **Asegúrate** de que las URLs del menú coincidan con las páginas que vas a crear
- **No ambigüedad**: Sé específico sobre qué debe estar en el menú principal vs. submenús
- **Cuenta la jerarquía**: ¿Cuántos niveles de submenú máximo?

---

## 4. Cómo pasar el contenido de las páginas y secciones

### Formatos aceptados para contenido

El proyecto Astro soporta múltiples formatos:

1. **Markdown (.md)** - Ideal para contenido textual, blogs, documentación
2. **Markdown con JSX (.mdx)** - Markdown con capacidad de insertar componentes React/Astro
3. **Astro (.astro)** - Componentes server-side, lógica compleja
4. **JSON/YAML** - Datos estructurados (productos, testimonios, etc.)

### ¿Cómo proporcionar el contenido?

#### Opción 1: Contenido simple por página

**Para cada página, proporciona:**

```yaml
Página: Sobre Nosotros
URL: /sobre

Secciones:
  - Héroe
    * Título: "Bienvenido a nuestra empresa"
    * Subtítulo: "Llevamos 10 años innovando"
    * Imagen: [referencia a imagen]
    * CTA: Botón "Conoce más"

  - Historia
    * Párrafo: [texto del párrafo]
    * Imagen: [referencia a imagen]

  - Equipo
    * Título: "Nuestro equipo"
    * Miembros:
      - Nombre, rol, foto
      - Nombre, rol, foto
      ...

  - CTA Final
    * Texto: "¿Listo para comenzar?"
    * Botón: "Contáctanos"
```

#### Opción 2: Contenido en bulk (recomendado para muchas páginas)

Proporciona un **documento centralizado** con toda la información del sitio:

```markdown
# Contenido del Sitio Web

## 1. Página Inicio

### Sección Hero
**Título:** [Tu título aquí]
**Subtítulo:** [Tu subtítulo]
**CTA Primario:** Botón "Empezar ahora" → /contacto
**CTA Secundario:** Link "Saber más" → #características
**Imagen:** [nombre del archivo o descripción]

### Sección Características
[Descripción de 3-5 características principales]

---

## 2. Página Servicios

### Introducción
[Párrafo introductorio]

### Listado de Servicios
1. Servicio A - [descripción]
2. Servicio B - [descripción]
3. Servicio C - [descripción]

---

[Continúa para cada página...]
```

### Cómo organizar el contenido por secciones

**Las secciones típicas en un sitio web incluyen:**

- **Hero/Banner**: Titular, subtítulo, imagen de fondo, CTA
- **Features/Características**: Grid de tarjetas con icono, título, descripción
- **Content/Contenido**: Bloques de texto con opcionales imágenes
- **Testimonials/Testimonios**: Citas de clientes con foto, nombre, rol
- **FAQ/Preguntas frecuentes**: Preguntas y respuestas en acordeón
- **CTA/Llamada a acción**: Texto + botón para urgir acción
- **Stats/Estadísticas**: Números destacados (clientes, años, proyectos)
- **Gallery/Galería**: Listado de imágenes
- **Blog/Posts**: Artículos con fecha, autor, categoría
- **Contact/Contacto**: Formulario y datos de contacto

### Cómo proporcionar imágenes

Para cada imagen, proporciona:

1. **La imagen física** (archivo o URL)
2. **Descripción del alt text** (por accesibilidad)
3. **Ubicación dentro de la página** (ej: "Hero de Inicio")

Ejemplo:
```
Imagen 1:
- Nombre/ID: hero-inicio.jpg
- Alt text: "Equipo trabajando en oficina moderna"
- Ubicación: Sección Hero de Inicio
- Tamaño recomendado: 1200x600px

Imagen 2:
- Nombre/ID: logo-cliente-1.png
- Alt text: "Logo de XYZ Company"
- Ubicación: Sección de Clientes
```

### Cómo proporcionar datos estructurados

Para contenido repetitivo (productos, testimonios, miembros de equipo), usa tablas o listas:

```markdown
### Testimonios

| Cliente | Cita | Rol | Foto |
|---------|------|-----|------|
| Juan García | "Excelente servicio" | CEO TechCorp | [foto1.jpg] |
| María López | "Muy recomendado" | Directora MktCorp | [foto2.jpg] |

### Productos

| Nombre | Descripción | Precio | Imagen |
|--------|-------------|--------|--------|
| Producto A | Descripción breve | $99 | [img-a.jpg] |
| Producto B | Descripción breve | $149 | [img-b.jpg] |
```

### Dónde irá el contenido

- **Contenido de páginas estáticas**: `src/pages/*.astro` o `src/pages/*.md`
- **Contenido de blog/posts**: `src/data/post/` (Markdown/MDX)
- **Datos estruturados** (productos, testimonios): `src/data/` o colecciones en `src/content/`
- **Imágenes**: `src/assets/images/` (optimizadas por Astro) o `public/images/` (estáticas)

### Lo que haré

1. Creará las páginas basadas en tu estructura
2. Insertaré el contenido en las secciones especificadas
3. Configuraré colecciones de contenido si hay datos dinámicos
4. Optimizarpé las imágenes para web
5. Configuraré meta datos (SEO)

### No especules

- **No escribas contenido de ejemplo** - sé específico con el contenido real
- **No asunas** estructura HTML - describe el contenido, yo estructuraré
- **Proporciona imágenes reales** o enlaces actuales, no placeholders
- **No olvides**: Meta descripción, palabras clave, alt text para imágenes
- **Clarifica**: Qué contenido es dinámico vs. estático

---

## Información de referencia del proyecto actual

### Tecnología utilizada

- **Framework**: Astro 5.0+
- **Styling**: Tailwind CSS
- **Componentes**: Soporte para React, Vue, Svelte, etc.
- **Contenido**: Markdown (MD) y MDX
- **Despliegue**: GitHub Pages (https://cyb-c.github.io/reaprovechador)

### Rutas de importancia

| Ruta | Propósito |
|------|-----------|
| `reaprovechador/src/pages/` | Todas las páginas públicas |
| `reaprovechador/src/components/` | Componentes reutilizables |
| `reaprovechador/src/layouts/` | Plantillas base |
| `reaprovechador/src/assets/images/` | Imágenes optimizadas |
| `reaprovechador/public/images/` | Imágenes estáticas |
| `reaprovechador/src/navigation.ts` | Configuración del menú |
| `reaprovechador/astro.config.ts` | Configuración de Astro |
| `reaprovechador/src/content/config.ts` | Definición de colecciones |

### Componentes de sección disponibles

El proyecto tiene widgets/componentes listos para usar:

- `Hero.astro` - Sección héroe con imagen/CTA
- `Features.astro` - Grid de características
- `Features2.astro` - Variante de características
- `Content.astro` - Bloque de contenido
- `Steps.astro` - Pasos/proceso
- `FAQs.astro` - Preguntas frecuentes
- `BlogLatestPosts.astro` - Últimos posts
- `Stats.astro` - Estadísticas
- `CallToAction.astro` - Llamada a acción
- `Testimonials.astro` - Testimonios

Puedes reutilizar o adaptar estos componentes.

### Cómo proporcionaré feedback

Después de que indiques:

1. **Logo** → Te confirmaré dónde quedó y si hace falta ajustar tamaño/estilos
2. **Estructura de páginas** → Te mostraré las rutas creadas y estructura
3. **Menú** → Te mostraré cómo se renderiza en navegación
4. **Contenido** → Te mostraré las páginas pobladas y si falta algo

---

## Resumen: Checklist para proporcionar la información

**Antes de que comencemos, necesito:**

- [ ] Logo (archivo SVG, PNG, JPG)
- [ ] Lista de páginas con URLs y descripción de secciones
- [ ] Estructura del menú (jerarquía de links)
- [ ] Contenido completo por página (título, párrafos, imágenes, CTAs)
- [ ] Imágenes reales o enlaces donde descargarlas
- [ ] Meta datos básicos (descripción, palabras clave por página)
- [ ] Datos de contacto/redes sociales para footer

**Cómo entregarlo:**

1. Crea un documento de Google Docs, Notion, o Markdown con toda la información
2. Adjunta el logo y imágenes (o enlaces públicos)
3. Sé específico: No asumas, no especules, no rellenes vacíos
4. Usa el formato que propuse en las secciones anteriores

---

**Nota final:** Todas mis respuestas en esta guía están basadas en:
- La estructura real del proyecto `reaprovechador`
- La Skill astro-docs de este workspace
- Estándares de Astro 5.0
- No hay especulación, todo es verificable en el código actual.
