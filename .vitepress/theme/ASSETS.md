# Nightlab theme assets

The theme extends VitePress's default theme without its bundled Inter font. Navigation, language selection, local search and their keyboard behavior remain framework components.

`public/assets/nb1-mascot.webp` and `public/assets/nb1-icon.png` are byte-for-byte copies of the site's approved nb1 artwork exports. Their sources remain `assets/` in this repository; the original master is maintained in `nb1-web/brand/nb1-mascot.png`. No alternative mascot is generated here.

The four WOFF2 files and two complete OFL notices in `public/assets/fonts/` come from `nb1-web` source commit `884f77ef00b77d8126a6e777213a202dccc1da6a`, under `src/fonts/`. These are the same local Fredoka 700 and M PLUS Rounded 1c 500/700 Latin assets used in the embedded workbench. CJK text uses the visitor's installed font fallback; the theme does not download a remote CJK font.

Nightlab semantic colors and four type roles come from the selected `design-nightlab` handoff. The docs map them to existing VitePress navigation, local search, menus, code, tables and article surfaces. No replacement mascot is included. The local fonts remain bundled with their original OFL notices; Nightlab uses the reference system UI stack and Fredoka for the nb1 wordmark.

The small GitHub link glyph is an inline copy of the `github` path from `@iconify-json/simple-icons` 1.2.102 (CC0-1.0), already supplied by VitePress. Inlining it avoids the development server requesting Iconify at runtime. It is a service link symbol, not an nb1 brand variant.

The selected artwork is tracked internally as variant `B-3`. That identifier is asset provenance, not a product or character name; public copy uses `nb1`.

The home mounts the assembled mk2 through `NightlabModel.vue`. Both language versions show the catalog’s blue and red demo colors. If WebGL is unavailable, the CAD-derived two-face fallback shows the same two channel values. Site preparation stages the verified assets from the pinned blink(1) Models package. The local viewer uses the catalog’s studio lighting and owns the Vue lifecycle and localized notes link. The enclosure is licensed under CC BY-SA 4.0, the PCB layout and its derived geometry under CC BY-SA 3.0, and Three.js under MIT. Asset hashes and adaptations are recorded in `public/nightlab/source-receipt.json`. The Guide loads these assets from its own origin.
