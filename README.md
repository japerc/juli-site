# juli-site

Source for [japerc.github.io](https://japerc.github.io/) — Julia Perczel's
personal academic site. Built with [Hugo](https://gohugo.io/).

The deployed site lives in a separate repo (`japerc/japerc.github.io`).
This repo holds the source; a GitHub Actions workflow builds and pushes
the rendered output on every push to `main`.

## Prerequisites

```bash
brew install hugo
```

Hugo extended is required (the workflow pins `0.161.1`); `brew` installs
extended by default.

## Local development

```bash
hugo server          # http://localhost:1313/, live reload
hugo                 # one-shot build into ./public/
```

`./public/` and `./resources/` are build artifacts — gitignored.

## Editing

- **Prose** — `content/_index.md` (home), `content/e-waste.md`,
  `content/himalayan-waste.md`. Bodies are raw HTML; frontmatter sets
  title, subtitle, hero image, etc.
- **Publications** — `data/publications.yaml`. One entry per publication;
  `groups:` controls section order on the publications page; tag an
  entry with `projects: [e-waste]` to have it appear in that project's
  Related Publications block automatically.
- **Site chrome** — `layouts/partials/` (head, header, footer,
  menu-script). Edit one place, applies to every page.
- **Styles** — `static/css/style.css`. CSS custom properties on `:root`
  drive the theme.
- **Images** — drop into `static/images/`; reference as
  `images/foo.jpg`.

## Deploy

Push to `main`. The workflow at `.github/workflows/deploy.yml` runs
`hugo --minify --gc` and force-pushes `./public/` to the `main` branch
of `japerc/japerc.github.io`. Auth is via an SSH deploy key stored as
the `ACTIONS_DEPLOY_KEY` secret on this repo.

A manual run is also available from the repo's Actions tab
(`workflow_dispatch`).
