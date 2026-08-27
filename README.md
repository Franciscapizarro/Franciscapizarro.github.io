# Franciscapizarro.github.io

Poster companion site: supplementary material for the stochastic PIDE + polynomial
chaos expansion work. Built with Jekyll on GitHub Pages.

Live at <https://franciscapizarro.github.io>

## Before you publish — two edits

1. **`_config.yml`** — fill in `author.email` and `author.orcid`. They are empty
   strings right now, and the contact block on the front page hides itself when they
   are empty.
2. **`code.html`** — the box at the top says the repository is not public yet.
   Replace it with the real repository URL when there is one.

## Structure

| File | URL |
|---|---|
| `index.html` | `/` |
| `PIDE-UQ.html` | `/PIDE-UQ/` |
| `derivations.html` | `/PIDE-UQ/derivations/` |
| `convergence.html` | `/PIDE-UQ/convergence/` |
| `control.html` | `/PIDE-UQ/control/` |
| `code.html` | `/PIDE-UQ/code/` |
| `_layouts/default.html` | page shell — nav, MathJax, footer |
| `assets/css/style.css` | all styling, light + dark |
| `assets/img/` | figures |
| `_unused/` | the two original stub files, kept out of the build |

Content pages are `.html`, not `.md`, on purpose: Jekyll passes HTML through without
running it past kramdown, so LaTeX reaches MathJax exactly as written. No escaping
games with underscores or backslashes.

## Writing maths

MathJax 3 is configured in `_layouts/default.html`:

- inline: `\( ... \)`
- display: `$$ ... $$` or `\[ ... \]`

**One hazard.** Liquid, the template engine, treats `{{` as the start of a tag. LaTeX
almost never produces `{{`, but if you ever write something like `\mathbf{{x}}`, the
build will break. Insert a space (`\mathbf{ {x}}`) or wrap the block in
`{% raw %} ... {% endraw %}`. A lone `}}` (from `p_{\text{PCE}}`, for instance) is
harmless.

## Adding a page

Copy any existing page, change the front matter, and add it to the `<nav>` in
`_layouts/default.html`:

```html
---
layout: default
title: Your title
subtitle: Optional one-liner under the title
permalink: /PIDE-UQ/your-page/
---
```

## Publishing

The repository must be named `Franciscapizarro.github.io` (matching the account name)
for it to serve at the root domain. Upload the **contents** of this folder to the
repository root — not the folder itself. Then in the repository, under
*Settings → Pages*, set the source to *Deploy from a branch*, branch `main`, folder
`/ (root)`. The first build takes a couple of minutes; check *Actions* if the site
does not appear.

## Local preview (optional)

```bash
gem install bundler jekyll
jekyll serve
```
