# UTILITIES

---

> You SCSS preprocessor should be configured to search for files in the sass source dir (example: project-root/src/sass), because all files use path relative to that dir, and not relative to them.

---

## Idea

The idea is to have a place where you can easily update a mixin or create a new one while working on some project. They are abstract - not related to the project, so the new ones can easily be just dropped in from anywhere, any that you find useful. Then you create project-related components manually, in the "main/components" folder.

## Folders

### Debug

Use these only for debugging purposes. There are debug-code and debug-design files in the root.

#### Debug code

Use this file for code debugging, like testing mixins and functions, seeing compiled color values or sizes etc.

#### Debug design

Use this file for debugging your design, with following helpers:

- **[sass-mq](https://github.com/sass-mq/sass-mq)** - show active breakpoint
- **[basehold.it](https://basehold.it/)** - show baseline grid (page overlay)
- **[pesticide.scss](https://github.com/mrmrs/pesticide/blob/master/sass/pesticide.scss)** - show element outlines

> Don't include them in production.

### Design

#### Tag mixins

Just include mixins with the name of the html tag they are being used on.

For example, if you create a link component, name the selector for example "link", and `@include a() { ... }` mixin (for html `<a>` tag). Then add more styles manually.

Available:

- a - use on links
- body - use on the body tag
- hr - horizontal rule
- img - use on images: option to balance images with filters and overlay, [style broken images](https://bitsofco.de/styling-broken-images/)
- ol - use on ordered lists
- ul - use on unordered lists
- p - use on paragraphs
- root - use on :root (html tag)

##### Tag mixin Exceptions

- block - use on "general" block level elements, like: div, article, section etc.
- heading - use on the common "headings" style
- pseudo - make pseudo-elements
  - pseudo-before, pseudo-after, pseudos: basic pseudo-element insertion
  - pseudo-before-stretched, pseudo-after-stretched, pseudos-stretched: full width/height pseudo-elements
- vr - "vertical rule" - a kind of a vertical separator

#### Other mixins

- ms mixin - modular scale - apply a [modular scale](https://www.modularscale.com/) to the design, including media-queries for different (smaller) ratio on smaller screens, respecting your design approach - mobile/desktop first
- gs mixin - grid scale - apply a grid scale to the design - so that everything fits into the [baseline grid](https://material.io/design/layout/spacing-methods.html)
- fs mixin - fluid size - make anything fluid size, using three optional methods and a fallback, and limit min/max size - based on: [madebymike.com.au](https://www.madebymike.com.au/writing/precise-control-responsive-typography/) and [websemantics.uk](https://websemantics.uk/tools/responsive-font-calculator/)
- ff mixin - font-family - option to use system ui font on mobile, to reduce bandwidth
- center - center absolutely positioned element, horizontally / vertically / both
- emq - easier-sass-mq - simplifies usage of sass-mq
- mq - [sass-mq](https://github.com/sass-mq/sass-mq) - easy media-queries - don't use directly, use emq.
- no-js-style - use to apply styles when browser does not support JavaScript
- reduced-motion - use to disable animations and transitions, if "reduced-motion" requested by the visitor
- selection - style selected text and text targeted with a link
- sr-only - use for content which should be visually hidden, but remain accessible to assistive technologies (e.g. "skip" links)
- truncate-text - insert shortened text with ellipsis, using only css
- arrow-helper - [ultimate arrow mixin](https://gist.github.com/kirkas/9560076) / [Examples](https://codepen.io/kirkas/pen/eYmxEd)

### Helpers

This folder contains functions and mixins that are generally not used in the design, but to help other mixins and functions produce the code that we will use in the design. An exception might be "to-rem" function, which we might ocasionally use in the design.

- colors function - [get more natural tints and shades](https://learnui.design/blog/color-in-ui-design-a-practical-framework.html)
- neutral - get grey palette slightly tinted with chosen color
- print-stylesheet - option to include print styles into the main stylesheet or make a separate one
- round-number - "round" a number with desired decimal places
- to-rem - convert px/unitless to rem - if passed rem, it returns it - no error
