# JupyterLite prototype

Runs a subset of the `mstsa` workshop notebooks entirely in the browser (Pyodide),
no Python install required. This is a parallel, experimental notebook set --
the standard notebooks in `../notebooks/` keep using the normal numba/C-accelerated
`mstsa` build unchanged.

## Status

Pilot notebook only: `03_potts_complexity.ipynb` (smallest dataset, no external
dependencies). Adapted from `../notebooks/03_potts_complexity.ipynb`:
- Installs the pure-Python `mstsa` build via `piplite` from the `pyodide` branch
  of https://github.com/Frederic-vW/mstsa (numba/C extensions optional there,
  fall back to pure NumPy -- see that branch for details).
- `data_path`/`cache_dir` changed from `../data/...` to `data/...`, since the
  notebook and its bundled data now live side by side under `content/`.
- `data/potts/*.npy` (5MB) and the precomputed `data/cache/potts_complexity/*.npz`
  cache are bundled directly so the notebook runs without recomputation.

Build verified locally (structurally: static site assembles, notebook and data
land in the right place) but **not yet verified with an actual in-browser kernel
run** -- that needs a real browser, which isn't available in the environment
this was built in.

## Build

```bash
pip install jupyterlite-core jupyterlite-pyodide-kernel jupyter-server
cd jupyterlite
jupyter lite build --contents content --output-dir _output
```

## Serve locally

```bash
cd jupyterlite/_output
python3 -m http.server 8000
# open http://localhost:8000/lab/index.html
```

## Next steps

- Verify the pilot actually runs end-to-end in a real browser.
- Decide on remaining notebooks to port (dataset size is the main constraint --
  see the size table in the conference-repo memory notes; `data/mpilmbb` at
  158MB is by far the largest and would need either a much smaller subset or a
  fetch-on-demand approach rather than bundling everything).
- Decide on deployment (e.g. GitHub Pages via a `gh-pages` branch or CI build,
  rather than committing `_output/` to version control).
