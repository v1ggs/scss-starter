# SASS STARTER PACKAGE

---

## GENERAL INFO

> You SCSS preprocessor should be configured to search for files in the sass source dir (example: project-root/src/sass), because all files use path relative to that dir, and not relative to them.
>
> Mixins and functions rather throw errors, in case you don't keep an eye on the console. Therefore you should use something like gulp-plumber for Gulp, and some kind of notification to make you know there has been an error.
>
> There are examples in debug-code.scss. For making a theme or a particular page styles, there are also examples in their respective folders.

---

## IDEA

The idea is to keep this package as simple as possible, for easier usage, and still make it able to help. :)

I didn't want to make a framework that it takes time to learn it, and which contains hundreds of unused classes (I do use [purgecss](https://www.npmjs.com/package/@fullhuman/postcss-purgecss), but still...).

Instead it provides some basic, but still usefull things, and everyone can add what they need - that way it makes it simpler for everyone to use it.

For those who use VSCode, there are snippets that also contain explanations for mixins. You can type "scss-starter" and your autocomplete should list all available mixins (or just look into the snippets file).

---

## USAGE

- Use config for everything. First define options, and then below, use them to define components. Then use these variables in the components/modules/layout.
- Create components/modules/layout in the "main" folder, and include in them their "placeholders" from "utilities/design", if they have one. If not, make one. ;)
- Use mixin-tools (listed below) for faster and consistent design.
- Use the debug css in html, and control it in config (don't forget to remove it in production).

> For creating a theme/page, see readme file in their folders.

---

## FEATURES

### Debugging

- Debug code (debug-code.scss): test mixins and functions, see the code they produce (i.e. color values, sizes from modular scale etc.).
- Debug design (debug-design.scss):
  - [Display baseline grid](https://basehold.it/) on the page,
  - [Display active breakpoint](https://github.com/sass-mq/sass-mq#seeing-the-currently-active-breakpoint)
  - [Use pesticide](https://github.com/mrmrs/pesticide).

> These create separate css files, don't forget to remove them in production.

### Design

- Choose your design approach (mobile/desktop first) for media-queries.
- [Create more "natural" color tints and shades](https://learnui.design/blog/color-in-ui-design-a-practical-framework.html). Also create "tinted" neutrals.
- All media-queries will respect your design approach :information_source:
- Use [modular scale](https://www.modularscale.com/)
- Use [baseline grid](https://material.io/design/layout/spacing-methods.html)
- Use system fonts on mobile devices (prevent downloading fonts to save bandwidth)
- [Make any size fluid](https://www.madebymike.com.au/writing/precise-control-responsive-typography/) - based on the screen width. Three methods and an optional fallback.
- Create easily media-queries with EMQ (uses [sass-mq](https://github.com/sass-mq/sass-mq))
- Easier links (use config to style them)
  - automatically created states,
  - a "wrapper link" (see [getbootstrap.com](https://getbootstrap.com/docs/4.3/utilities/stretched-link/) and [stackoverflow.com](https://stackoverflow.com/questions/796087/make-a-div-into-a-link)),
  - a class to increase the link's size on smaller screens.
- Image balancing (kind of "equalise" them - make them look more similar) with a filter and an overlay
- ["Style" images when they fail to load](https://bitsofco.de/styling-broken-images/).
- Create easily a theme or a particular page design.
- Easier ".no-js" styles
- Units are converted to rems (see config for all "less important" options).
- VS Code snippets for mixins included

> :information_source: System UI font family is always mobile-first, to prevent some browsers from downloading unneccessary fonts on mobile.

### Print Stylesheet

- Either include the print stylesheet in the main file, or make it separately (use config).

---

## FOLDERS

- config - contains all the settings for the design/development
- utilities - contains all the tools
  - debug - design/development debugging tools
  - design - a kind of placeholders - mixins to use in the design - this is where you can drop-in new ones and update the existing
  - helpers - helper functions/mixins for other functions/mixins, not used directly in the design, generally should not be modified
- main - all the files for the design/development
- pages - styles for a particular page
- themes - styles for a different theme

> There are also some SCSS snippets in the ".snippets" dir, that migh be useful. I didn't want to implement them to "keep it simple".

---

## FILES

- debug-code.scss - test your code, not for production
- debug-design.scss - test your design, not for production
- main.scss - main sylesheet
- print.scss - depending on the config, a separate print stylesheet

> There are also examples in pages and themes folders.

---

## USEFUL MIXINS

> For more info on using these mixins, see their files in the "utilities" folder.
>
> Use the debug files if you want to see what each mixin produces. Sometimes there can be a substantial amount of code (e.g. media-queries), which might be done better another way. You might consider using custom properties for system ui fonts for not to print them all over the code.

### [Modular Scale](https://www.modularscale.com/)

Just define a scale ratio and use:

`@include ms( <css-property>, <values from the map, shorthand syntax>... );`

mixin ("ms" for modular scale) on anything, to apply sizes from the scale.

Option to add two scales - one with a smaller ratio for smaller screens (recommended).

It prints media-queries automatically. Can be combined with the baseline grid.

> `<values from the map, shorthand syntax>` also means there are no commas.
>
> Example: `@include ms(margin, xxs s l);`
>
> *VS Code snippet triggers: "ms, modular-scale, include, mixin, scss-starter"*

### [Baseline Grid](https://material.io/design/layout/spacing-methods.html)

Define your sizes and then just use:

`@include gs( <css-property>, <values from the map, shorthand syntax>... );`

mixin ("gs" for grid scale) on everything.

Can be combined with modular scale.

> `<values from the map, shorthand syntax>` also means there are no commas.
>
> Example: `@include gs(margin, xxs s l);`
>
> *VS Code snippet triggers: "gs, grid-scale, baseline-grid, include, mixin, scss-starter"*

### Font Family

Use system fonts on mobile devices (recommended) to prevent browsers from downloading fonts, to reduce bandwidth:

`@include ff( custom-font-family-variable );`.

> *VS Code snippet triggers: "ff, font-family, system-ui-font, small-screen-font, include, mixin, scss-starter"*

### [Fluid Size](https://www.madebymike.com.au/writing/precise-control-responsive-typography/)

Make any size fluid - width, height, margin, padding, font-size, border-radius.

- Three optional "fluid size" methods, optional fallback
- If using calc() method, it can produce media-queries to limit the sizing
- If fluid size is not enabled, returns only the $max-size value

Use:

`@include fs( <css-property>, <max-size>, <min-size>, <max-breakpoint>, <min-breakpoint> );`

> *VS Code snippet triggers: "fs, fluid-size, include, mixin, scss-starter"*

### EMQ - Easier [Sass-mq](https://github.com/sass-mq/sass-mq)

Define your breakpoints and other queries an just use them (keys from these maps, quoted/unquoted, comma separated):

`@include emq( <bp=1>, <query-1>, <bp-2>, <query-2>, "(custom:query)"... ) { // styles here }`

It just makes easier usage of the original [sass-mq](https://github.com/sass-mq/sass-mq), which is included in the same folder.

> When you use two breakpoints, the first found breakpoint is always "min-width" and the second "max-width", regardless of the design approach. Other than that, the order of queries does not matter.
>
> *VS Code snippet triggers: "emq, mq, media-query, include, mixin, scss-starter"*

### No-JS

Apply styles when the JavaScript is disabled:

`@include no-js-styles { // styles here }`.

> *VS Code snippet triggers: "no-js, js, include, mixin, scss-starter"*

---

Mixins ("placeholders") to be used for components:

---

### A

Mixin to create links - use config to style it.

Use:

`@include a;`.

It adds automatically:

- States (hover, focus, active, visited) - only those styled in config
- Bem-style class (`<main-class>--wrapper`) for a "wrapper" link - see [getbootstrap.com](https://getbootstrap.com/docs/4.3/utilities/stretched-link/) and [stackoverflow.com](https://stackoverflow.com/questions/796087/make-a-div-into-a-link) :information_source:
- Bem-style class (`<main-class>--increased`) in a media-query, and a modernizr class (`.touchevents <main-class>--increased`) to increase the link's surface on smaller/touch screens. :information_source:

> :information_source: Classes will not work if you use it in `<a>` tag, only in a class or id.
>
> *VS Code snippet triggers: "a, link, include, mixin, scss-starter"*

### IMG

Use in images:

`@include img($fluid: true, $balance: true) { // styles here }`.

- Balance images (css filter in config)
- ["Style" them when they fail to load](https://bitsofco.de/styling-broken-images/) :information_source:
- Add an image overlay on its parent, for image balancing (also in config) :information_source: :information_source:

> :information_source: Unsupported on: Opera Mini, Safari (Desktop and iOS), iOS Webview (Chrome, Firefox, others)
>
> :information_source: :information_source: Creates `<main-class>--img-overlay::before` and its hover

---

> *VS Code snippet triggers (image): "img, image, include, mixin, scss-starter"*
>
> *VS Code snippet triggers (overlay): "img, overlay, include, mixin, scss-starter"*

---

## ALL AVAILABLE MIXINS

### "Placeholder" Mixins

Just include mixins with the name of the html tag they are being used on. For example, if you create a link component, name the selector for example ".link", and `@include a;` mixin (for html `<a>` tag).

- `@include a` - links
- `@include body` - body tag
- `@include hr` - horizontal rule
- `@include img` - images
- `@include ol` - ordered lists
- `@include ul` - unordered lists
- `@include p` - paragraphs
- `@include root` - :root (html tag)
- `@include block` - "general" block level elements, like: div, article, section etc.
- `@include heading` - the common "headings" style
- `@include pseudo` - make pseudo-elements
  - pseudo-before, pseudo-after, pseudos: basic pseudo-element insertion
  - pseudo-before-stretched, pseudo-after-stretched, pseudos-stretched: full width/height pseudo-elements
- `@include vr` - "vertical rule" - a kind of a vertical separator

### Helper Mixins

- `@include ms` - modular scale - apply a [modular scale](https://www.modularscale.com/) to the design, including media-queries for different (smaller) ratio on smaller screens, respecting your design approach - mobile/desktop first
- `@include gs` - grid scale - apply a grid scale to the design - so that everything fits into the [baseline grid](https://material.io/design/layout/spacing-methods.html)
- `@include fs` - fluid size - make anything fluid size, using three optional methods and a fallback, and limit min/max size - based on: [madebymike.com.au](https://www.madebymike.com.au/writing/precise-control-responsive-typography/) and [websemantics.uk](https://websemantics.uk/tools/responsive-font-calculator/)
- `@include ff` - font-family - option to use system ui font on mobile, to reduce bandwidth
- `@include center` - center absolutely positioned element, horizontally / vertically / both
- `@include emq` - easier-sass-mq - simplifies usage of sass-mq
- `@include mq` - [sass-mq](https://github.com/sass-mq/sass-mq) - easy media-queries - **you can use emq, which makes easier usage of the sass-mq**.
- `@include no-js-style` - apply styles when browser does not have JavaScript enabled
- `@include sr-only` - content which should be visually hidden, but remain accessible to assistive technologies (e.g. "skip" links)

---

## INSTALLATION

Copy "scss" folder to your project's "source" dir.

> You SCSS preprocessor should be configured to search for files in the sass source dir (example: project-root/src/sass), because all files use path relative to that dir, and not relative to them.

---

## LICENSE

### MIT LICENSE

Copyright © 2022 [Igor Vračar](https://www.igorvracar.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---
