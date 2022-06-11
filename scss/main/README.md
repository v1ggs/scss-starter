# MAIN

## Site's main styles

> You SCSS preprocessor should be configured to search for files in the sass source dir (example: project-root/src/sass), because all files use path relative to that dir, and not relative to them.

## Folders

### BASE

This is where you define basic things, like "html" and "body" tags, custom fonts, page animations and other general styles.

### LAYOUT

This is where you define the main layout elements, like the site's header and footer, hero, sidebar and main etc.

### PRINT

This will include print styles if it has been set in the configuration.

### COMPONENTS

This folder contains only the simple components, like button, link, paragraph, heading etc. which do not create page layout, like header, main, footer, etc.

### MODULES

This folder contains compound components, those who contain other components (like paragraphs, links, buttons etc.), but do not create page layout (like header, main etc.).

---

> Any component that does not contain elements related to it with BEM style class names (i.e. .component > .component__element), is a simple or layout component.
> If a component contains elements related to it with BEM style class names, then it is a module.

- Compound components (modules), like: forms, cards, menus, sliders, are located in "modules" folder.

- Simple components, like: paragraphs, links, buttons, headings, etc. are located in "components" folder.

- Layout components, like: header, main, section, footer etc. are located in "layout" folder.

#### Component Example

```css
.nav {
   // styles here
}

// a menu inside the .nav bar
.menu {
   // styles here
}

// They ARE NOT related to each other, using BEM style classes, so .nav is a component (.menu probably not).
```

#### Module Example

```css
.card {
   // styles here
}

.card__header {
   // styles here
}
// They ARE related to each other, using BEM style classes, so .card is a module, with its related elements.
```
