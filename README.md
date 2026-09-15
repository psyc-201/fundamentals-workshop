# README

Quarto site source code for the UCSD Psychology 201 Fundamentals Workshop.

This site is configured to by *polyglot*: both R and Python are mixed together on the same page and all execution takes place *client-side* in the Browser; no environment management needed.

## Local development

- One time [install](https://quarto.org/docs/get-started/) `quarto`
- One time install `uv` (Python package manager): `curl -LsSf https://astral.sh/uv/install.sh | sh`
- Setup quarto WASM: `quarto add r-wasm/quarto-live`
- Launch site: `uv run quarto preview` (`rm _site/` if quarto errors)
