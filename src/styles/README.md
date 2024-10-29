# **Patrón 7-1**: Librería de Sass para Layouts y Componentes Reutilizables

1. [Descripción del Proyecto](#descripción-del-proyecto)
2. [Estructura de Directorios](#estructura-de-directorios)
3. [Instalación](#instalación)
   -  [Clonación usando Git Subtree](#clonación-usando-git-subtree)
   -  [Actualización de librería](#actualizacion-libreria)
4. [Uso](#uso)
   -  [Funciones Disponibles](#funciones-disponibles)
   -  [Mixins Disponibles](#mixins-disponibles)
      -  [Utilidades](#utilidades)
      -  [Colores](#colores)
      -  [Tipografía](#tipografia)
      -  [Efectos](#efectos)
   -  [Clases Reutilizables](#clases-reutilizables)
5. [Convenciones de Estilo](#convenciones-de-estilo)
6. [Contribución](#contribución)
7. [Licencia](#licencia)
8. [Contacto](#contacto)

## <a name="descripción-del-proyecto"></a>Descripción del Proyecto

El **Patrón 7-1** es una librería modular de Sass diseñada para facilitar la creación de layouts y componentes reutilizables. Está estructurada bajo el principio de la arquitectura **7-1**, que organiza el código Sass en siete carpetas específicas, más un único archivo principal que actúa como punto de entrada.

Esta librería proporciona:

-  **Funciones y Mixins**: Un conjunto de utilidades para agilizar el desarrollo de estilos personalizados, incluyendo cálculos dinámicos, control de media queries, y manipulación de colores.
-  **Clases Reutilizables**: Estilos predefinidos para componentes de interfaz como grillas, botones y layouts, que pueden integrarse fácilmente en cualquier proyecto.
-  **Flexibilidad y Escalabilidad**: El código está diseñado para ser fácilmente escalable y adaptable a diferentes proyectos, ofreciendo una base sólida para el desarrollo de interfaces consistentes y bien organizadas.

El objetivo principal de esta librería es mejorar la eficiencia en el desarrollo de proyectos Sass, promoviendo la reusabilidad de código y la organización modular.

## <a name="estructura-de-directorios"></a>Estructura de Directorios

El **Patrón 7-1** sigue la convención de organización de archivos Sass que divide el código en siete carpetas y un archivo principal. Esta estructura modular facilita el mantenimiento, la escalabilidad y la reutilización del código.

La estructura de directorios es la siguiente:

-  **abstracts/**: Contiene utilidades Sass como variables, mixins y funciones globales que se usan en todo el proyecto.
-  **base/**: Estilos básicos que incluyen reset.css, tipografías globales y estilos predeterminados para elementos HTML.
-  **components/**: Estilos para componentes reutilizables como botones, tarjetas o modales.
-  **layout/**: Define la estructura de la página, como contenedores, grillas y áreas clave de diseño.
-  **pages/**: Estilos específicos para páginas particulares del proyecto, como home o contacto.
-  **themes/**: Contiene los estilos relacionados con los temas o configuraciones visuales, como esquemas de colores.
-  **vendors/**: Estilos de terceros o librerías externas que se integran al proyecto.

El archivo `main.scss` importa todos los archivos de estas carpetas y actúa como punto de entrada para compilar todo el código Sass.

## <a name="instalación"></a>Instalación

### <a name="clonación-usando-git-subtree"></a>Clonación usando Git Subtree

Para añadir este patrón a otros proyectos utilizaremos git subtree. En este ejemplo añadimos el repo en la carpeta src/styles

```bash
git subtree add --prefix src/styles https://github.com/LBC-Starter-Kits/sass-7-1-pattern.git main --squash
```

#### <a name="actualizacion-libreria"></a> Actualización de librería

```bash
git subtree pull --prefix src/styles https://github.com/LBC-Starter-Kits/sass-7-1-pattern.git main --squash
```

Es recomendable añadir un script al archivo _package.json:_

```jsx

  "scripts": {
		...
    "update-styles": "git subtree pull --prefix src/styles https://github.com/LBC-Starter-Kits/sass-7-1-pattern.git main --squash"
    ...
  },
```

⚠️Si se han realizado modificaciones a los archivos en el proyecto donde está insertado el patrón y también en el repositorio se producirán conflictos de merge. Hay que resolver cada conflicto individualmente mantenido el código necesario del proyecto así como las nuevas actualizaciones del patrón (**en general aceptar ambos cambios y eliminar el código innecesario**).

## <a name="uso"></a>Uso

### <a name="funciones-disponibles"></a>Funciones Disponibles

#### `asset($base, $type, $path)`

Esta función genera una URL basada en un tipo de archivo y una ruta especificada.

-  Parámetros:
   -  `$base` (String): La URL base para el recurso.
   -  `$type` (String): El tipo de recurso (por ejemplo, `fonts/`).
   -  `$path` (String): La ruta del recurso.
-  Retorno: La URL completa utilizando la función nativa `url()`.

```scss
asset('https://example.com/', 'fonts/', 'custom-font.woff');
```

#### `image($path, $base: $base-url)`

Devuelve la URL de una imagen basada en su ruta. Usa la función asset() internamente.

-  Parámetros:
   -  `$path` (String): La ruta de la imagen.
   -  `$base` (String): (String) (opcional): La URL base para las imágenes. Por defecto, utiliza $base-url.
-  Retorno: URL completa de la imagen.

```scss
image('logo.png');
```

#### `font($path, $base: $base-url)`

Devuelve la URL de una fuente basada en su ruta. Usa la función asset() internamente.

-  Parámetros:
   -  `$path` (String): La ruta de la fuente.
   -  `$base` (String): (String) (opcional): La URL base para las fuentes. Por defecto, utiliza $base-url.
-  Retorno: URL completa de la fuente.

```scss
font('roboto.woff2');
```

#### `css-function($function, $values...)`

Genera una función CSS personalizada a partir de los valores proporcionados.

-  Parámetros:
   -  `$function` (String): El nombre de la función CSS (por ejemplo, min, max, calc).
   -  `$values...` (Variadic): Los valores que se pasarán a la función.
-  Retorno: String con la función CSS.

```scss
css-function('min', '100px', '50%');
```

#### `css-min($values...)`

Fuerza la función CSS min() en Sass.

-  Parámetros:
   -  `$values...` (Variadic): Los valores a pasar a min().
-  Retorno: Función min() con los valores dados.

```scss
css-min(100px, 50%);
```

#### `css-max($values...)`

Fuerza la función CSS max() en Sass.

-  Parámetros:
   -  `$values...` (Variadic): Los valores a pasar a max().
-  Retorno: Función max() con los valores dados.

```scss
css-max(100px, 50%);
```

#### `css-minmax($values...)`

Fuerza la función CSS minmax() en Sass.

-  Parámetros:
   -  `$values...` (Variadic): Los valores a pasar a minmax().
-  Retorno: Función minmax() con los valores dados.

```scss
css-minmax(100px, 200px);
```

#### `css-clamp($values...)`

Fuerza la función CSS clamp() en Sass.

-  Parámetros:
   -  `$values...` (Variadic): Los valores a pasar a clamp().
-  Retorno: Función clamp() con los valores dados.

```scss
css-clamp(1rem, 2vw, 2rem);
```

#### `css-calc($values...)`

Fuerza la función CSS calc() en Sass.

-  Parámetros:
   -  `$values...` (Variadic): Los valores a pasar a calc().
-  Retorno: Función calc() con los valores dados.

```scss
css-calc(100% - 50px);
```

### <a name="mixins-disponibles"></a>Mixins Disponibles

#### <a name="utilidades"></a>Utilidades

##### `on-event($self: false)`

Este mixin envuelve un selector para los eventos `hover`, `active` y `focus`. Tiene la opción de incluir el selector actual en esos estados de eventos.

-  Parámetros:

   -  `$self` (Boolean) [false]: Si es `true`, también se aplican estilos al selector actual además de los eventos (`hover`, `active`, `focus`).

   ```scss
   .button {
   	@include on-event {
   		color: red;
   	}
   }
   ```

##### `when-inside($context)`

Este mixin se utiliza para crear un selector que aplique estilos únicamente cuando el elemento se encuentre dentro de un contexto específico. Es útil para aplicar estilos específicos de un componente dentro de una sección o un contenedor.

-  Parámetros:

   -  `$context` (String): El selector del contexto en el que debe estar anidado el elemento.

   ```scss
   @include when-inside(".sidebar") {
   	color: blue;
   }
   ```

##### `mq($width, $type: min)`

Este mixin gestiona media queries de manera eficiente. Permite definir reglas de estilo basadas en puntos de ruptura (breakpoints) con soporte para `min-width` (predeterminado) o `max-width`.

-  Parámetros:

   -  `$width` (String): El punto de ruptura deseado (debe coincidir con una clave en el mapa `$mq_breakpoints`).
   -  `$type` (String) [min]: El tipo de media query (`min` o `max`).

   ```scss
   .un-selector {
   	@include mq("tablet") {
   		font-size: 1.5rem;
   	}
   }
   ```

#### <a name="colores"></a>Colores

##### `color-scheme($texto, $bg)`

Este mixin aplica un esquema de color a un elemento, permitiendo definir un color de texto y un fondo, que puede ser un color sólido o un degradado.

-  Parámetros:
   -  `$texto` (String): Color del texto.
   -  `$bg` (Color): Color de fondo. Puede ser un solo color o una lista que represente un degradado.

```scss
@include color-scheme(white, blue);
```

##### `color-variables($color, $label)`

Este mixin genera variables CSS de color que incluyen sombras y tintes a partir de un color base. Es útil para establecer una paleta de colores consistente en el proyecto.

-  Parámetros:
   -  `$color` (Color): Color base para las variables.
   -  `$label` (String): Etiqueta que se utilizará para nombrar las variables generadas.

```scss
@include color-variables(#3498db, "primary");
```

#### <a name="tipografia"></a>Tipografía

##### `typo($size, $scale: 'perfect-fourth')`

Este mixin permite definir el tamaño de la fuente y una escala tipográfica específica.

-  Parámetros:
   -  `$size` (String): Tamaño de la fuente. Clave en el array definido por la variable $scale. En la escala por defecto existen las claves ["xss","xs","s","m","l","xl","xxl","xxxl"].
   -  `$scale` {String} - Escala tipográfica a utilizar; si no se encuentra en el mapa, se utiliza la escala predeterminada perfect-fourth

```scss
.un-selector {
	@include typo("xl");
}
```

#### <a name="efectos"></a>Efectos

##### `full-bleed($color)`

Este mixin aplica un efecto de fondo "full bleed", estableciendo un color de fondo y creando un efecto de sombra que se extiende más allá de los límites del elemento.

-  Parámetros:
   -  `$color` (Color): Color de fondo para el elemento.

```scss
.un-selector {
	@include full-bleed(red);
}
```

---

##### `glassmorphism($color: #ffffff, $alpha: 0.2, $outline-alpha: 0.3, $blur: 5px)`

Este mixin genera un fondo semitransparente con desenfoque y sombra, dando un efecto de vidrio.

-  Parámetros:
   -  `$color` (Color) [#ffffff]: Color de fondo.
   -  `$alpha` (Number) [0.2]: Nivel de opacidad del fondo.
   -  `$outline-alpha` (Number) [0.3]: Nivel de opacidad del borde.
   -  `$blur` (Number) [5px]: Cantidad de desenfoque para el fondo.

```scss
.un-selector {
	@include glassmorphism(#3498db, 0.5);
}
```

---

##### `color-shadow($angle: -45deg, $color1: #0000ff, $color2: #ff0000)`

Este mixin aplica un efecto de sombra de color en un ángulo específico, utilizando un pseudo-elemento que aplica un gradiente como fondo con desenfoque.

-  Parámetros:
   -  `$angle` (Angle) [-45deg]: Ángulo del gradiente.
   -  `$color1` (Color) [#0000ff]: Primer color del gradiente.
   -  `$color2` (Color) [#ff0000]: Segundo color del gradiente.

```scss
.un-selector {
	@include color-shadow(-30deg, #ff0000, #0000ff);
}
```

---

##### `image-text($url)`

Este mixin permite utilizar una imagen de fondo que se recorta en forma de texto.

-  Parámetros:
   -  `$url` (String): URL de la imagen de fondo.

```scss
.un-selector {
	@include image-text("path/to/image.jpg");
}
```

---

##### `gradient-text($angle: 90deg, $color1: #0000ff, $color2: #ff0000)`

Este mixin aplica un efecto de texto degradado, utilizando un gradiente de fondo que se recorta en forma de texto.

-  Parámetros:
   -  `$angle` (Angle) [90deg]: Ángulo del gradiente.
   -  `$color1` (Color) [#0000ff]: Primer color del gradiente.
   -  `$color2` (Color) [#ff0000]: Segundo color del gradiente.

```scss
.un-selector {
	@include gradient-text(45deg, #ff0000, #00ff00);
}
```

---

##### `fancy-link-1($angle: 90deg, $color1: #0000ff, $color2: #ff0000)`

Este mixin crea un enlace estilizado con un fondo degradado que aparece al pasar el mouse, con un efecto de transición suave al cambiar el tamaño del fondo.

-  Parámetros:
   -  `$angle` (Angle) [90deg]: Ángulo del gradiente.
   -  `$color1` (Color) [#0000ff]: Primer color del gradiente.
   -  `$color2` (Color) [#ff0000]: Segundo color del gradiente.

```scss
.un-selector {
	@include fancy-link-1(90deg, #ff0000, #0000ff);
}
```

---

##### `fancy-link-2($angle: 90deg, $color1: #0000ff, $color2: #ff0000)`

Este mixin crea un enlace estilizado con un fondo degradado que cambia de posición al pasar el mouse, permitiendo un efecto de transición suave.

-  Parámetros:
   -  `$angle` (Angle) [90deg]: Ángulo del gradiente.
   -  `$color1` (Color) [#0000ff]: Primer color del gradiente.
   -  `$color2` (Color) [#ff0000]: Segundo color del gradiente.

```scss
.un-selector {
	@include fancy-link-2(90deg, #0000ff, #ff0000);
}
```

### <a name="clases-reutilizables"></a>Clases Reutilizables

#### Layouts

###### `.container--classic`

Este layout aplica un contenedor centrado con un ancho máximo que se adapta a la pantalla, hasta un límite definido por la variable `$max-width`.

```scss
<div class="container--classic">
  <!-- contenido -->
</div>
```

###### `.container--static`

Un contenedor estático con un ancho máximo y padding lateral para mantener el contenido alineado en el centro.

```scss
<div class="container--static">
  <!-- contenido -->
</div>
```

---

###### `.container--fluid`

Un layout fluido que utiliza un sistema de grillas para controlar el contenido, con áreas que pueden romper los límites del contenedor principal.

```scss
<div class="container--fluid">
  <!-- contenido -->
</div>
```

---

###### `.cluster`

Este layout utiliza flexbox para agrupar elementos en fila o columna con un gap entre ellos. Ideal para listas de elementos.

```scss
<div class="cluster">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

---

###### `.flexible-grid`

Un layout flexible basado en flexbox que distribuye los elementos dentro de una cuadrícula adaptable. Los elementos ocupan el mismo espacio.

```scss
<div class="flexible-grid">
  <div>Item 1</div>
  <div>Item 2</div>
</div>
```

---

###### `.auto-grid`

Este layout utiliza CSS Grid para crear una cuadrícula automática, donde las columnas se ajustan automáticamente al tamaño mínimo definido.

```scss
<div class="auto-grid">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

---

###### `.reel`

Este layout crea una cinta de desplazamiento horizontal con elementos ajustados en una cuadrícula. Ideal para carruseles o galerías de imágenes.

```scss
<div class="reel">
  <div>Slide 1</div>
  <div>Slide 2</div>
</div>
```

---

###### `.main-with-sidebar`

Un layout con un área principal y una barra lateral. El área principal tiene prioridad y crece más que la barra lateral.

```scss
<div class="main-with-sidebar">
  <div>Main Content</div>
  <div>Sidebar</div>
</div>
```

---

###### `.pancake-stack`

Este layout organiza el contenido en una pila donde la cabecera, el contenido y el pie de página se apilan verticalmente.

```scss
<div class="pancake-stack">
  <header>Header</header>
  <main>Main Content</main>
  <footer>Footer</footer>
</div>
```

---

###### `.holy-grail`

Este layout clásico de "Holy Grail" distribuye el contenido en un esquema de tres columnas con cabecera y pie de página.

```scss
<div class="holy-grail">
  <div class="header">Header</div>
  <div class="left-side">Left Sidebar</div>
  <div class="main">Main Content</div>
  <div class="right-side">Right Sidebar</div>
  <div class="footer">Footer</div>
</div>
```

---

###### `.grid-12-span`

Un layout basado en una cuadrícula de 12 columnas. Los elementos se pueden ajustar en diferentes números de columnas usando clases como `.span-12`, `.span-6`, etc.

```scss
<div class="grid-12-span">
  <div class="span-12">Full Width</div>
  <div class="span-6">Half Width</div>
</div>
```

---

###### `.grid-12-chess`

Un layout basado en una cuadrícula de 12x12 que permite disponer los elementos en posiciones específicas, como un tablero de ajedrez.

```scss
<div class="grid-12-chess">
  <div class="item-1">Item 1</div>
  <div class="item-2">Item 2</div>
</div>
```

---

###### `.full-layout-area`

Un layout que organiza las áreas de la página como la cabecera, navegación, contenido principal, anuncios, barra lateral y pie de página, adaptable a diferentes tamaños de pantalla.

-  **Versión móvil**:

```scss
<div class="full-layout-area full-layout-area--mobile">
  <header class="header">Header</header>
  <nav class="navigation">Nav</nav>
  <main class="main">Main Content</main>
  <footer class="footer">Footer</footer>
</div>
```

-  **Versión tablet**:

```scss
<div class="full-layout-area full-layout-area--tablet">
  <header class="header">Header</header>
  <nav class="navigation">Nav</nav>
  <main class="main">Main Content</main>
  <footer class="footer">Footer</footer>
</div>
```

-  **Versión desktop**:

```scss
<div class="full-layout-area full-layout-area--desktop">
  <header class="header">Header</header>
  <nav class="navigation">Nav</nav>
  <main class="main">Main Content</main>
  <footer class="footer">Footer</footer>
</div>
```

## <a name="convenciones-de-estilo"></a>Convenciones de Estilo

## <a name="contribución"></a>Contribución

## <a name="licencia"></a>Licencia

## <a name="contacto"></a>Contacto
