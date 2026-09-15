# README

Quarto site source code for the UCSD Psychology 201 Fundamentals Workshop.

This site is configured to by *polyglot*: both R and Python are mixed together on the same page and all execution takes place *client-side* in the Browser; no environment management needed.

## Local development

- One time [install](https://quarto.org/docs/get-started/) `quarto`
- One time install `uv` (Python package manager): `curl -LsSf https://astral.sh/uv/install.sh | sh`
- Setup quarto WASM: `quarto add r-wasm/quarto-live`
- Launch site: `uv run quarto preview`
- Build site: `uv run quarto render` (pushes to `main` do this automatically via GitHub Actions and deploy to <https://psyc-201.github.io/fundamentals-workshop/>)

---

## Notes

- Polars no longer supports WASM builds, but Eshin's personal fork of this project works just fine: <https://github.com/ejolly/polars-pyodide>
- Quarto live can point micropip to a github pages static build for installation which is what the fork does
- Pyodide 0.28 has no `pyarrow`, so polars `.to_pandas()` fails in the browser. This is why the site has no seaborn plotting examples
