# WordPress Boilerplate

A lean classic WordPress starter for Idiom Digital projects, built with PHP templates, Tailwind CSS 4, and esbuild. It intentionally avoids client branding and a large predefined design system. The existing header, mobile drawer, content templates, and static hero provide scaffolding to adapt per project.

## Quick start

1. Place this repository in your WordPress installation under `wp-content/themes/wordpress-boilerplate/`.
2. Use Node.js 24, as specified in `.nvmrc`:

   ```sh
   nvm use
   npm install
   ```

3. Build while developing:

   ```sh
   npm run watch
   ```

4. Generate minified assets for release:

   ```sh
   npm run build
   ```

5. Activate **WordPress Boilerplate** in the WordPress admin and assign a menu to **Primary Menu**. Without an assigned menu, the theme lists top-level pages.

The PHP scaffold targets WordPress 6.0+ and PHP 7.4+.

## Build and source locations

| Command | Purpose |
| --- | --- |
| `npm run watch` | Run the CSS and JavaScript watchers together. |
| `npm run build` | Build both minified production bundles. |
| `npm run build:css` / `npm run watch:css` | Compile `src/css/tailwind.css` through `@tailwindcss/cli` to `assets/css/main.css`. |
| `npm run build:js` / `npm run watch:js` | Bundle `src/js/main.js` and its imports through esbuild to `assets/js/main.js`. |

Compiled assets and `node_modules/` are ignored by Git. Rebuild assets for each checkout and include the generated CSS and JavaScript when deploying the theme. No separate Tailwind or PostCSS configuration is needed by this build.

`style.css` contains only WordPress theme metadata. `functions.php` loads `inc/setup.php` (theme supports and menus) and `inc/enqueue.php` (assets). The metadata stylesheet uses the theme version from WordPress; compiled CSS and JavaScript use their file modification times for cache busting and are enqueued only when present.

## Styling

`src/css/tailwind.css` starts with `@import "tailwindcss";`. Tailwind CSS 4 detects utility classes in the PHP and JavaScript sources automatically. Keep class names literal when adding JavaScript-driven states so they can be detected.

The CSS adds only responsive media defaults, neutral slate focus outlines, reduced-motion handling, WordPress screen-reader text support, and the `.site-container` / `.site-section` layout helpers used by the templates. Project typography, colours, and components belong to each site's design; no generic card, button, badge, form, or navigation component system is included.

## Mobile drawer

`header.php` renders the sticky header and toggle, then includes `template-parts/navigation-mobile.php`. `src/js/main.js` initializes `src/js/mobile-drawer.js` after the DOM loads. The drawer updates toggle and drawer ARIA states, switches icons, animates menu items, and locks body scrolling. The toggle, backdrop, a navigation link, or Escape can close it.

## Hero and content templates

`front-page.php` includes `template-parts/hero/hero.php`, then renders page content. The hero is a static scaffold: its slide controls are placeholders and have no slider logic. Adapt the copy and `/contact` and `/work` links for each site.

`index.php`, `page.php`, and `single.php` provide classic template entry points. Reusable content markup lives in `template-parts/content/`, with an empty-results template at `template-parts/content-none.php`.

## Site Functionality plugin

The optional plugin scaffold is at `wp-content/plugins/site-functionality/site-functionality.php` inside this repository. When installing the repository as a theme, copy the `site-functionality` directory into the WordPress installation's actual `wp-content/plugins/` directory and activate **Site Functionality** separately.

Keep project-specific custom post types, taxonomies, and ACF field groups in this plugin. It includes commented examples; none are enabled by default, and ACF is not bundled.
