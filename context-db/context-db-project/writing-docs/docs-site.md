---
type: Reference
description:
  How the docs site is built and deployed (Sphinx, PyData theme, MyST Markdown,
  sphinx-design, GitHub Actions to Pages), how the owner chooses a look with
  the look picker, the theme details that break silently, and how to check a
  change.
---

# The docs site

Sources are Markdown in `docs/`. [conf.py](../../../docs/conf.py) loads MyST,
sphinx-design, and sphinx-copybutton on the PyData theme. The look comes from
[custom.css](../../../docs/_static/custom.css).

```bash
.venv/bin/sphinx-build -W docs docs/_build/html
```

`-W` makes warnings fail the build. CI runs the same command and
[docs.yml](../../../.github/workflows/docs.yml) deploys to GitHub Pages on every
push to `v0.1`.

What the pages must say and show is in
[docs-requirements.md](./docs-requirements.md).

## The look is the owner's choice

Every part of the look in `custom.css` was picked by the owner from options
tried on the real pages: the colors, the moving title, the backdrop, code blocks
as windows, the see-through header, monospace headings, the pill for the current
page. Do not restyle any of it unless asked.

The owner chooses by trying, not from a description. Put the options in the look
picker, [docs/looks/](../../../docs/looks/looks.js), which is off unless the
docs are built with `CONTEXT_DB_LOOKS=1` ([conf.py](../../../docs/conf.py)). To
have it on the published site, set that variable in `docs.yml` for as long as
the choosing takes. The owner clicks through the options and pastes back the
line the panel gives, such as `Looks: headings=slash extras=codeglow`. Move the
chosen rules into `custom.css` and take them out of the picker. Ideas that were
tried and not adopted stay in the picker for later.

## Things that break silently

- The install prompt sends an agent to the README on GitHub. The README's
  Install section must stay a set of steps an agent can follow alone, ending
  with `configure` run through the script.
- The gradient title on the home page is selected by `section#context-db > h1`.
  That id comes from the page title. Change the title and the styling is lost.
- Definition lists need `deflist` in `myst_enable_extensions`. Without it they
  render as plain paragraphs and the build still passes.
- Dropdown colors come from `:color: secondary` on the directive. The theme
  hard-codes the tint behind it, so `custom.css` points `--sd-color-secondary-bg`
  at the palette.
- A table wider than a phone screen scrolls sideways inside its container and
  its last column is cut off, while the page itself reports no overflow. So
  compare each table with its container at 390px, not the page with the
  screen. Long inline code is the usual cause: it does not wrap, except in a
  table cell on a phone, where `custom.css` lets it break.
- Every page is top level, so `html_sidebars` is emptied. A page added inside a
  subfolder needs that revisited.
- Link colors are set per theme in `custom.css`. Check a new color in both light
  and dark mode.
- `docs/_static/og-image.png` is rendered from `og-image.svg` with a headless
  browser at 1200 by 630. Re-render it after editing the SVG. Put the SVG inline
  in a page that loads JetBrains Mono; opened as a bare image it cannot load the
  font, and the title falls back to another one.

## Checking a change

Build, then look at the page. A headless Chromium through Playwright works in a
codespace after `playwright install chromium` and `playwright install-deps`.
Screenshot light and dark mode, and a phone width.

On 2026-11-11 the owner did not see changes that had only been built locally,
and asked for them to be made visible. Take it that the owner looks at the
published site: a docs change is not seen until it is pushed.
