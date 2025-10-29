## Quick context

This repository is the "Big Picture" single-page HTML template (HTML5 UP). It's a static site: plain HTML in `index.html`, precompiled CSS in `assets/css/` and source SCSS in `sass/`. JavaScript lives in `assets/js/` (vendor libs + `util.js` and `main.js`). Images are in `images/fulls/` and `images/thumbs/` and webfonts in `webfonts/`.

Key files to reference when making changes:
- `index.html` — single-page layout; sections are composed as `<section id="..." class="main ...">`.
- `assets/css/main.css` — compiled stylesheet served to the site.
- `sass/` — SCSS source used to author styles (see `sass/main.scss` and `sass/layout/`, `sass/components/`).
- `assets/js/main.js`, `assets/js/util.js` — custom JS for interactions; vendor plugins live under `assets/js/` as well (poptrox, scrolly, scrollex, etc.).
- `images/` — `fulls/` (lightbox large images) and `thumbs/` (gallery thumbnails).
- `LICENSE.txt` / `README.txt` — licensing and template notes.

## Architecture & patterns AI agents should follow

- Single-page template: content is organized as a vertical stack of `<section class="main ...">` blocks (see `index.html`). Section style conventions are defined in SCSS and described in `README.txt` (style1, style2 left/right, style3 primary/secondary, modifiers `dark`, `fullscreen`).
- Gallery markup: gallery items are `<article class="from-left">` (or `from-right`, `from-bottom`, etc.) wrapping an `<a class="image fit">` whose `href` points at `images/fulls/...` and whose `<img src="images/thumbs/...">` is the thumbnail. This pattern is relied on by the Poptrox lightbox plugin — preserve it when modifying the gallery.
- JS responsibilities: vendor plugins provide scrolling and lightbox effects. `util.js` and `main.js` orchestrate behavior (scroll transitions, activating poptrox). Prefer editing `assets/js/main.js` for page-level behavior; avoid editing minified vendor files.
- Styles workflow: `assets/css/` contains compiled CSS. `sass/` is the source. If you change SCSS, you must compile it to update `assets/css/main.css` or edit `assets/css/main.css` directly if you intentionally bypass the SCSS source (not recommended).

## Build / dev workflow (discoverable facts + minimal commands)

- There is no `package.json`, task runner, or build scripts checked in. That means compilation is manual or done with external tooling not included here.
- To preview locally, serve the folder with a simple static server (works in macOS `zsh`):

```bash
# from repo root
python3 -m http.server 8000
# then visit http://localhost:8000/
```

- To compile SCSS (if you have Dart Sass installed), run from repo root:

```bash
# one-off compile
sass sass/main.scss:assets/css/main.css
# or watch mode
sass --watch sass:assets/css
```

Note: these commands are suggestions based on the repository layout — no build tool is tracked here. If the project in your environment uses an external script (npm, gulp, etc.), prefer that; otherwise the `sass` CLI is the simplest option.

## Conventions & gotchas (explicit, repo-specific)

- Do not rename or move `assets/js/jquery*.js`, `jquery.poptrox.min.js`, `jquery.scrolly.min.js`, or `jquery.scrollex.min.js` unless you update the `<script>` includes in `index.html` in the same change.
- Image gallery relies on the images/fulls/ and images/thumbs/ naming; thumbnails must match the corresponding full-size files. Lightbox captions use the title attribute on the <img> tag.
- Contact form in index.html uses a placeholder action (no server endpoint configured). The README suggests Formspree for simple form handling — do not expect server-side handling in this repo.
- CSS: `assets/css/noscript.css` and the `noscript` stylesheet are used to provide fallbacks if JS is disabled. Keep those when changing layout behavior.

## Where to make changes

- Presentation/layout: change `sass/` and then compile to `assets/css/`.
- Page content: edit `index.html` directly (section blocks are the pattern to follow).
- Interactivity: edit `assets/js/main.js` or `assets/js/util.js` for custom behavior. Leave vendor files alone unless updating libraries deliberately.

## Search-and-replace examples agents can use

- Add a new section (follow this snippet from `index.html`):

```html
<section id="new" class="main style2 left dark">
  <div class="content box style2">
    <header><h2>New Section</h2></header>
    <p>...</p>
  </div>
  <a href="#next" class="button style2 down anchored">Next</a>
</section>
```

- Create a gallery item (thumbnail + full):

```html
<article class="from-left">
  <a href="images/fulls/07.jpg" class="image fit">
    <img src="images/thumbs/07.jpg" title="Caption text" alt="" />
  </a>
</article>
```

## Tests / CI / Lint

- There are no tests, CI configs, or linters in the repository. Keep changes small and test by serving the site locally as described above.

## License

- This template is distributed under the Creative Commons Attribution 3.0 license (see `LICENSE.txt` and `README.txt`). Respect the assets and third-party images referenced in the README (demo images are not included).

---

If any of this is out-of-date or you use a particular build chain (npm, gulp, or GitHub Actions) outside the repo, tell me which commands you run and I will merge those into this file. Ready for feedback — what should I clarify or expand? 
