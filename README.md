# Franciscapizarro.github.io

Poster companion site: supplementary material for the stochastic PIDE + polynomial
chaos expansion work. Built with Jekyll on GitHub Pages.

Live at <https://franciscapizarro.github.io>

## Structure

| File | URL |
|---|---|
| `index.html` | `/` |
| `PIDE-UQ.html` | `/PIDE-UQ/` |
| `convergence.html` | `/PIDE-UQ/convergence/` |
| `control.html` | `/PIDE-UQ/control/` |
| `_layouts/default.html` | page shell — nav, MathJax, footer |
| `assets/css/style.css` | all styling, light + dark |
| `assets/img/` | figures |
| `_unused/` | superseded stubs, excluded from the build via `_config.yml` |

Content pages are `.html`, not `.md`, on purpose: Jekyll passes HTML through without
running it past kramdown, so LaTeX reaches MathJax exactly as written. No escaping
games with underscores or backslashes.

## Writing maths

MathJax 3 is configured in `_layouts/default.html`:

- inline: `\( ... \)`
- display: `$$ ... $$` or `\[ ... \]`

### Custom macros

Defined in the MathJax config so LaTeX from the papers can be pasted in unchanged. Add
new ones to the `macros:` block in `_layouts/default.html`.

| Macro | Expands to |
|---|---|
| `\sat` | `\operatorname{sat}` |
| `\sgn` | `\operatorname{sign}` |
| `\TV` | `\operatorname{TV}` |
| `\Ex` | `\mathbb{E}` |
| `\dd` | `\,\mathrm{d}` |

### Two hazards

**Liquid.** The template engine treats `{{` as the start of a tag. LaTeX almost never
produces `{{`, but if you write something like `\mathbf{{x}}` the build breaks. Insert
a space (`\mathbf{ {x}}`) or wrap the block in `{% raw %} ... {% endraw %}`. A lone `}}`
(from `p_{\text{PCE}}`, for instance) is harmless.

**Angle brackets.** A raw `<` inside maths can confuse the HTML parser. Use `\lt` and
`\gt` instead of `<` and `>`.

## Adding a page

Copy any existing page, change the front matter, and add it to the `<nav>` in
`_layouts/default.html` — the nav is hand-maintained, so a new page is invisible until
you do:

```html
---
layout: default
title: Your title
subtitle: Optional one-liner under the title
permalink: /PIDE-UQ/your-page/
---
```

If you delete a page, remove its nav entry and its card in `index.html` too, or the
links 404.

## Contact details

`_config.yml` holds `author.email` and `author.orcid`. The email is written with
`[at]` rather than `@` as spam obfuscation, so it is rendered as plain text — do not
wrap it in a `mailto:` link unless you switch it to a real address.

## Local preview

```bash
gem install bundler jekyll
jekyll serve
```
