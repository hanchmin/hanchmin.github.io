# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal academic website built with **Jekyll** and the **al-folio** theme (upstream: `alshedivat/al-folio`), deployed via GitHub Pages to `hanchmin.github.io`. Owner: Hancheng Min. The repo is a customized fork — most theme files under `_layouts/`, `_includes/`, `_sass/` are upstream and should only be edited when intentionally diverging.

## Working style (from the owner)

The owner wants **concise responses with simple explanations**. When context is incomplete, ask for more — do not proceed on assumptions. When editing a large file, do not dump the entire file back; show only what changed.

## Common commands

```bash
# Local dev server with live reload (port 8080)
bin/entry_point.sh          # container entrypoint: rebuilds Gemfile.lock + jekyll serve
bundle exec jekyll serve    # plain serve

# Production build (used by CI)
bundle exec jekyll build --lsi

# Format code before committing (Prettier — enforced on PRs upstream)
npx prettier --write .

# Deploy to gh-pages branch (interactive; commits must be clean first)
./bin/deploy
```

There is no test suite. Validation = the site building and rendering. `--lsi` (related-posts) is used in production builds and slows the build noticeably.

**Build gotchas:**

- Always run `jekyll build`/`serve` from the repo root — the Bash tool's working directory persists across calls, and a `cd` into a subdirectory (e.g. `assets`) makes Jekyll run with no `_config.yml` and fail with a misleading SCSS error.
- `jekyll-minifier` occasionally throws a transient `Errno::EINTR` on a CSS write near the end of the build; just re-run `rm -rf _site && bundle exec jekyll build`.
- Sass deprecation warnings (`@import`, `lighten()`) are noise from Dart Sass and do not fail the build.

## Ruby environment

Ruby + Bundler are required (`Gemfile`/`Gemfile.lock`). The Docker path (`docker-compose.yml`) uses `amirpourmand/al-folio`; the devcontainer uses the official `mcr.microsoft.com/devcontainers/jekyll` image. Either pre-bundles gems, so local `bundle install` is normally the only setup step.

## Architecture (the parts worth knowing)

This is a standard al-folio Jekyll site; the architecture is **content-as-data**, not application code. Editing flow is almost always: edit a data file or Markdown front matter, not logic.

- **`_config.yml`** — the single source of truth. Site identity, theme switches (light/dark highlight, repo themes), feature toggles (`enable_*`), third-party CDN library versions, and the `scholar`/`jekyll-archives`/`imagemagick`/`jekyll-minifier` plugin config all live here. Most behavioral changes are a one-line flip in this file. Note `url: https://hanchmin.github.io` with empty `baseurl`.
- **`_pages/`** — Markdown pages with front matter (`about.md`, `projects.md`, `publications.md`, etc.). These are the human-edited content surfaces.
- **`_data/`** — structured content consumed by includes/layouts: `cv.yml`, `news.yml`, `coauthors.yml`, `repositories.yml`, `venues.yml`, `people.yml` (group members — see "People page" below).
- **`_bibliography/papers.bib`** — the single source of truth for all publications. Drives the publications page via `jekyll-scholar` (APA style, sorted by year descending) **and** the projects page's related-work citations (see "Citation automation" below). Per-entry detail pages are generated under `bibliography/` using the `bibtex.html` details layout. `filtered_bibtex_keywords` lists the al-folio-specific bibtex fields (`abbr`, `pdf`, `code`, `selected`, `preview`, …) stripped from the rendered bibtex. Custom fields in use: `html` (official venue URL — OpenReview/PMLR/IEEE), `arxiv`, `pdf`, `poster`/`slides` (set to `true` to resolve `assets/{posters,slides}/<pdf-basename>`), `code`, `preview` (thumbnail in `assets/img/publication_preview/`).
- **`_posts/`** and **`_projects/`** — blog posts and project collection entries.
- **`_layouts/` & `_includes/`** — Liquid templates. Many exist as paired `.html` (legacy) + `.liquid` files; prefer editing the `.liquid` variant when both exist (newer al-folio convention).
- **`_plugins/`** — local Ruby plugins: `cache-bust.rb`, `google-scholar-citations.rb`, `download-3rd-party.rb`, `hide-custom-bibtex.rb`, `details.rb`, `file-exists.rb`, `remove-accents.rb`.
- **`_sass/`** — `_variables.scss`, `_themes.scss` (light/dark palette), `_base.scss`, `_cv.scss`, `_distill.scss`, `_layout.scss`. **`_custom.scss` is a dead file — not imported by `assets/css/main.scss`**, so edits there have no effect; put personal SCSS overrides in `_base.scss` (or add `_custom` to the `@import` list in `main.scss`).
- **`assets/`** — static assets incl. `assets/img/` (input to the responsive-WebP imagemagick pipeline; widths 480/800/1400).

### Citation automation (projects page)

The projects page (`_pages/projects.md`) cites papers **by bib key only** — no hand-written citation HTML. Each related-work entry is:

```liquid
<li>{% bibliography -f papers --template project_cite -q @*[key=BIBKEY]* %}</li>
```

jekyll-scholar looks up the entry in `papers.bib` and renders it via `_layouts/project_cite.html` (a compact citation: authors, quoted title, venue+year+vol/pp, then text links). The `[URL]` link resolves to `entry.html` if present, else `http://arxiv.org/abs/{{ entry.arxiv }}`, else omitted; `[PDF]`/`[POSTER]`/`[SLIDES]`/`[CODE]` appear iff the corresponding bib field exists (same field-driven logic as the publication page's `_layouts/bib.html`, but as compact `[LABEL]` text links rather than buttons).

Author rendering is shared via `_includes/bib_authors.liquid` (used by both `bib.html` and `project_cite.html`): self-author `H. Min` is bolded via `<em>`; coauthors are auto-linked from `_data/coauthors.yml`. `project_cite.html` passes `no_links=true` to the include so the projects page shows **no author hyperlinks** (just bold `H. Min`); the publications page calls it without the param, so its author links stay on. The `.project-cite em { font-weight: bold }` rule in `_base.scss` makes the `<em>` render bold (not italic) on the projects page.

jekyll-scholar wraps each `{% bibliography %}` call in `<ol class="bibliography">`. The `list-style: none` rule in `_base.scss` is scoped under `.publications`, so a matching `.projects ol.bibliography` rule is needed there for the projects page (otherwise decimal "1." numbering shows).

To add a citation to a project: ensure the entry exists in `papers.bib` (add `html`/`arxiv`/`pdf`/`poster`/`slides`/`code` fields as appropriate), then drop a `{% bibliography -f papers --template project_cite -q @*[key=KEY]* %}` line into the project's `<ul>`. No other edit needed.

### People page

`_pages/people.md` (`permalink: /people/`, `nav: false` — reachable by permalink only, not in the navbar) renders group members from **`_data/people.yml`**. Four lists in the yml: `phds`, `masters`, `undergrads`, `alumni`. The page combines masters + undergrads into one section; `phds` and `alumni` are separate.

- **PhD students** render as horizontal photo cards (photo left, info right) in a responsive grid. Fields: `name`, `role`, `year`, `image` (path relative to `assets/img/`, e.g. `people/jane.jpg`), `homepage` (optional — name links out if set), `interests` (optional), `blurb` (optional). If `image` is blank, the card falls back to `assets/img/people/placeholder.png`.
- **Master's / undergrads / alumni** render as compact text lists: `name` + `info` (masters/undergrads) or `role`/`year`/`next` (alumni).

The `.people` SCSS block in `_base.scss` (scoped under `.people`, so it doesn't leak) styles the grid, cards, and lists. The `h2.category` header in `.people` is **intentionally darker** than the projects page's `.projects h2.category` (which uses `--global-divider-color` — too faint for the people section titles) — it uses `--global-text-color` with a `--global-text-color-light` rule.

To add a member: add an entry to the relevant list in `_data/people.yml`; the page renders automatically. To promote the page to the navbar, flip `nav: false` → `nav: true` and add a `nav_order` (Projects is 2, Update is 3).

### Feature toggles

Behavior is gated by `enable_*` flags in `_config.yml` (math, darkmode, masonry, medium-zoom, progressbar, project categories, analytics). Turning a feature on/off is a config edit, not a code change.

### Responsive images

`jekyll-imagemagick` auto-generates WebP variants from `.jpg/.jpeg/.png/.tiff` in `assets/img/`. Requires ImageMagick installed (provided by the Docker/devcontainer images; may need installing locally).

### Reading local PDFs

`pdftotext` (poppler) is installed via Homebrew at `/opt/homebrew/bin/pdftotext`. Use it to read paper PDFs in `assets/pdf/` when writing intros (e.g. `pdftotext -f 1 -l 3 -q assets/pdf/FILE.pdf -`). The Read tool's PDF rendering requires `pdftoppm` (also poppler) and is heavier; `pdftotext` is faster for text extraction.

## Formatting

Prettier with `@shopify/prettier-plugin-liquid` (config in `.prettierrc`: `printWidth: 150`, `trailingComma: "es5"`). Upstream runs a Prettier check on PRs. `pre-commit` is configured (`.pre-commit-config.yaml`) for whitespace/YAML hygiene.

## Deploy

`bin/deploy` builds with `JEKYLL_ENV=production`, runs `purgecss`, then force-pushes the built `_site/` contents to the `gh-pages` branch (source branch is `master`). It refuses to run with uncommitted or untracked files. GitHub Pages serves from `gh-pages`.
