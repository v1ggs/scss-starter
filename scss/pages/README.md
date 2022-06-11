# PAGES

Custom page styles.

---

> You SCSS preprocessor should be configured to search for files in the sass source dir (example: project-root/src/sass), because all files use path relative to that dir, and not relative to them.

---

If you have some different styling on the site, a theme or a page:

- Create a .scss file and a folder in "themes" or "pages" folders (both in the same directory)
- Name them according to the theme/page name (example: folder: special-page; file: special-page.scss)
- Copy components (partials) that will be modified, from "main" folder to this new folder ("special-page" in the example)
- Copy from the config to this new file ("special-page.scss" in the example), only those variables that will be modified, and change their values
- Import config (load-config file from utilities)
- Import components that will be modified

> You can remove all styles/properties from the components that will not be modified, to reduce the unneccessary code.

You can find an example here.

> Theme's or page's main file ("special-page.scss" in the example) should not be a partial - prefixed with an underscore.
