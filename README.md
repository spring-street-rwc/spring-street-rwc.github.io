# Spring Street Neighbors — Redwood City

Source for [spring-street-rwc.github.io](https://spring-street-rwc.github.io/). A Hugo + [Ananke](https://github.com/gohugo-ananke/ananke) static site advocating for traffic calming on Spring Street between the Bay Road Complete Streets project and the surrounding residential network.

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

## Deployment

Pushes to `main` automatically build and deploy via `.github/workflows/hugo.yml`.

One-time setup on the GitHub repo:

1. Settings → Pages → **Source: GitHub Actions**.
2. Push to `main` — the workflow handles the rest.

For a custom domain, add a `static/CNAME` file containing the domain and configure DNS per [GitHub's docs](https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site).

## Structure

```
content/             # Markdown pages and posts
  _index.md          # Home page
  about.md
  bay-road-project.md
  how-to-help.md
  post/              # Blog
layouts/_shortcodes/ # petition-cta.html — site-wide CTA
static/              # Static files served at site root (e.g. .nojekyll)
themes/ananke/       # Ananke theme (git submodule — do not edit in place)
hugo.toml            # Site config — baseURL, menu, params (incl. petition_url)
```
