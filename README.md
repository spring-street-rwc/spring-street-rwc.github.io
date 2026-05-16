# Spring Street Neighbors — Redwood City

Source for [spring-street-rwc.github.io](https://spring-street-rwc.github.io/). A Hugo + [PaperMod](https://github.com/adityatelange/hugo-PaperMod) static site advocating for traffic calming on Spring Street between the Bay Road Complete Streets project and the surrounding residential network.

The site supports light/dark mode — it follows the visitor's OS preference by default, with a toggle in the header to override.

## Local development

Requires [Hugo extended](https://gohugo.io/installation/) (matches v0.161.1+ for parity with CI).

```bash
git clone --recurse-submodules https://github.com/spring-street-rwc/spring-street-rwc.github.io.git
cd spring-street-rwc.github.io
hugo server -D
```

The dev server runs at http://localhost:1313/.

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

## Adding a blog post

```bash
hugo new post/YYYY-MM-DD-short-slug.md
```

This uses `archetypes/default.md`, which pre-fills `author`, `tags`, and `draft = false`.

Posts can embed YouTube videos with Hugo's built-in shortcode:

```
{{< youtube VIDEO_ID >}}
```

## Petition / CTA

The petition URL lives in one place: the `petition_url` param in `hugo.toml`. Update it once and every `{{< petition-cta >}}` shortcode on the site (home, how-to-help, blog posts) points to the new URL.

The shortcode also accepts optional `headline`, `subtext`, and `label` arguments — see `layouts/_shortcodes/petition-cta.html`.

CTA styling lives in `layouts/_partials/extend_head.html` (PaperMod includes this partial in `<head>` automatically). It uses PaperMod's CSS variables (`--primary`, `--secondary`, `--border`, `--code-bg`) so it adapts to both light and dark mode.

## Deployment

Pushes to `main` automatically build and deploy via `.github/workflows/hugo.yml`.

One-time setup on the GitHub repo:

1. Settings → Pages → **Source: GitHub Actions**.
2. Push to `main` — the workflow handles the rest.

For a custom domain, add a `static/CNAME` file containing the domain and configure DNS per [GitHub's docs](https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site).

## Structure

```
content/             # Markdown pages and posts
  _index.md          # Home page (intro + hero image)
  about.md
  bay-road-project.md
  how-to-help.md
  post/              # Blog
layouts/
  _shortcodes/       # petition-cta.html — site-wide CTA shortcode
  _partials/         # extend_head.html — custom CSS injected into <head>
static/
  images/            # Site images (hero, etc.)
  .nojekyll          # Disables Jekyll on GitHub Pages
themes/PaperMod/     # PaperMod theme (git submodule — do not edit in place)
hugo.toml            # Site config — baseURL, menu, params (incl. petition_url, defaultTheme)
```
