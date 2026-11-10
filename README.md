# Chinatown Earthquake Retrofit Challenge

Class materials for the freshman seminar retrofit exercise.

| File | Purpose |
|---|---|
| `project_instructions.md` | Student project instructions (goal, inputs, rules, research prompts, rubric) |
| `index.html` | Data explorer website (inventory charts, two-program designer, side-by-side comparison of R2D results) |
| `project_instructions.pdf` | PDF version of the instructions |
| `data/chinatown_buildings_toy.csv` | Building inventory (the same file students load into R2D and into the website) |

## Publishing the website

Push this folder to a GitHub repository and enable **Settings → Pages → Deploy from branch** (root folder).
Students load the inventory CSV themselves with the **Load inventory CSV** button (tab 1), from wherever they saved
it, so the page also works when `index.html` is opened directly as a local file.

## Demo link (optional)

Files in the repository can be preloaded with URL parameters: `inv` (inventory), `base`, `a` and `b` (R2D results:
CSV exported from R2D, or `R2D_results.geojson`), for example:

`index.html?inv=data/chinatown_buildings_toy.csv&tab=tab-out&base=data/results_baseline.csv&a=data/results_A.csv&asys=URM&b=data/results_B.csv&bsys=C1`

`asys` / `bsys` tell the page which structural system each program retrofitted (used for program cost).
Preloading only works when the page is served (GitHub Pages or `python3 -m http.server`), not opened as a local file.

The hazard folder (`San_Andreas_Mw72_filtered/`) is distributed separately for R2D; the website does not need it.
