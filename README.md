# babqua-demo

Proof-of-concept demonstrating [`nu_plugin_edn`](https://github.com/franks42/nu_plugin_edn)
+ [Babqua](https://scicloj.github.io/babqua/) — running Nushell pipelines
from inside Quarto notebook code blocks.

## Setup

```bash
# 1. Install prerequisites (skip what you have)
brew install nushell babashka quarto    # or follow per-tool install docs

# 2. Install nu_plugin_edn (matching your Nushell version)
curl -L https://github.com/franks42/nu_plugin_edn/releases/download/v0.112.2-3/nu_plugin_edn-v0.112.2-3 -o nu_plugin_edn
chmod +x nu_plugin_edn
nu -c 'plugin add ./nu_plugin_edn; plugin use edn'
# Add `plugin use edn` to ~/.config/nushell/config.nu so each `nu -c` sees it

# 3. Install babqua extension
quarto add scicloj/babqua

# 4. Optional: install ^cedn and ^uuidv7 for the cross-tool sections
#    (see github.com/franks42/canonical-edn and github.com/franks42/uuidv7.cljc)
```

## Render

```bash
quarto render nu-pipelines.qmd
open _site/nu-pipelines.html
```

## What's here

- `nu-pipelines.qmd` — the demo notebook. Five sections covering
  bb→nu→bb pipelines, canonical hashing via `^cedn`, UUIDv7 generation
  + parsing via `^uuidv7`, three-tool composition, and a
  Nushell-filtered Vega-Lite chart.
- `_quarto.yml` — minimal Quarto project file.

## What this demos (in one sentence)

The **typed-value boundary principle** — typed transforms inside
Nushell, byte-level transforms as external CLIs (`^cedn`, `^uuidv7`,
`sha256sum`), all from inside a reproducible Quarto notebook.

## Status

Experimental scratch / playground for evaluating whether `nu->` /
`nu->edn` helpers are worth maturing into a published library. Sections
2-4 require `^cedn` and `^uuidv7` on PATH and skip otherwise.
