# Quarto website

This repository is the editable source for a Quarto website. Pages are written in Quarto Markdown (`.qmd`), with site-wide settings in `_quarto.yml`; Quarto combines those inputs into a static website when rendered.

## Source layout

These are the files and folders to edit when adapting the site:

| Source | Purpose |
| --- | --- |
| `_quarto.yml` | Website-wide configuration: navigation, footer, HTML output, theme, shared CSS, analytics, resource files, execution settings, and filters. |
| `index.qmd`, `about.qmd`, `404.qmd` | Top-level page sources, including the landing page and custom not-found page. |
| `blog/` | Blog landing page (`welcome.qmd`), dated post sources under `posts/`, section metadata, and post-specific styling. The landing page builds a dated listing and RSS feed from the posts folder. |
| `projects/` | Project listing and individual project pages. `_metadata.yml` sets shared page options; `styles.css` styles this section. |
| `reading/` | Reading-list page and individual entry pages. `_metadata.yml` sets shared page options; `styles.css` styles this section. |
| `styles.css`, `theme.scss` | Shared CSS adjustments and Sass theme variables. Section folders can provide their own CSS. |
| `*.png` and other referenced images | User-supplied visual assets used by pages, such as logos, thumbnails, and illustrations. Keep referenced paths intact or update the page that uses them. |
| `_extensions/coatless-quarto/adsense/` | Local Quarto filter extension and its extension metadata, included by the project configuration. Keep it when retaining that feature. |
| `.github/workflows/publish.yml` | GitHub Actions workflow that renders and publishes the site to the `gh-pages` branch when changes are pushed to `main`, or when manually dispatched. |
| `CNAME`, `ads.txt` | Site deployment and verification resources copied into the rendered site as configured in `_quarto.yml`. |
| `LICENSE` | Repository license. |

Page-level YAML front matter in each `.qmd` file controls page-specific details. Folder `_metadata.yml` files provide defaults for pages in that section. Listing pages use Quarto's listing configuration to collect entries from their neighboring source files, so new posts, projects, or reading entries can be added as new `.qmd` files with appropriate metadata.

## Rendered files and caches

`quarto render` turns the authored `.qmd` files into HTML and copies or generates supporting files in `_site/`. The `.gitignore` excludes `_site/`; it is build output and should not be edited as source. Quarto may also create `.quarto/`, intermediate notebook files, and other temporary or cache files during rendering.

This project sets `execute.freeze: true`, so Quarto stores computational results in `_freeze/` and can reuse them until the relevant source changes. Files such as `about_files/figure-html/` are generated figures from page execution. These are render artifacts, not the pages or styles to edit; change the source `.qmd` and render again. Do not rely on generated HTML, libraries, or files in `_site/` as the canonical implementation of the site.

## Work locally

Install [Quarto](https://quarto.org/docs/get-started/) and any execution engines or packages required by code chunks in the pages. Then run:

```sh
quarto preview
```

Preview serves the site locally and refreshes it as source files change. To build the static output once, run:

```sh
quarto render
```

The generated website is written to `_site/`.

## Deployment

The workflow in `.github/workflows/publish.yml` uses the official Quarto GitHub Actions setup and publish actions. A push to `main` renders and publishes the site to `gh-pages`; it can also be started manually from the repository's Actions page. Configure GitHub Pages to serve from that publishing target and set the repository's domain as needed for `CNAME`.

To reuse this architecture, fork or copy the repository, update `_quarto.yml` (especially the title, site URL, navigation, analytics, and footer), replace or reorganize the `.qmd` sources and image assets, and adapt the styling and deployment configuration. Keep the generated `_site/` output out of the source editing workflow.
