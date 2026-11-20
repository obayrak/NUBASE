# NUBASE2020 · Decay Systematics Explorer

An interactive, single-file web app for exploring nuclear ground-state properties and decay systematics from the **NUBASE2020** evaluation. It covers mass and binding energies, drip lines, empirical half-life laws, WKB barrier-penetration calculations, spontaneous fission, and Bateman decay chains, all running in the browser.

The full dataset (3,558 ground states) is embedded in the HTML. There is no backend, no build step and no install.

---

## Quick start

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
open nubase.html        # macOS
xdg-open nubase.html    # Linux
start nubase.html       # Windows
```

You can also serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/nubase.html
```

### GitHub Pages

Rename `nubase.html` to `index.html` (or add an `index.html` that redirects to it), then enable **Settings → Pages → Deploy from branch**. The app will be live at `https://<your-username>.github.io/<your-repo>/`.

> An internet connection is needed on first load for Plotly, MathJax and Google Fonts, which come from CDNs.

---

## Features

The app is organised into twelve tabs that all draw on the same embedded dataset.

| Tab | What it does |
|---|---|
| **Decay Systematics** | Scatter plots of the nuclide chart coloured by decay mode (α, β⁻, β⁺/EC, p, n, SF, …). Configurable axes, Z range, branching threshold and lin/log scales. Search for any nuclide, inspect it, and browse the filtered data table. |
| **Mass & Binding** | Experimental binding energy, B/A, SEMF (Bethe–Weizsäcker) binding with selectable coefficient sets, pairing term, shell correction B − B_SEMF, and separation energies Sₙ, Sₚ, S₂ₙ, S₂ₚ. |
| **Drip-Line & Shell** | Bound/unbound classification from separation energies, a drip-line detector, and neutron/proton shell gaps Δ₂ₙ, Δ₂ₚ for identifying magic numbers. |
| **Empirical α Decay** | Geiger–Nuttall and Viola–Seaborg fits with robust regressors (OLS, Tukey biweight, Huber, Theil–Sen, RANSAC, quadratic), residual diagnostics and model statistics. |
| **Empirical α/β/C Decay** | Universal decay-law explorer for β⁻, β⁺/EC, α and cluster (¹⁴C–³⁴Si) decay. Searches combinations of candidate terms, ranks models by AIC, BIC, CV-RMSE, RMSE or R², and adds correlation analysis and Bayesian linear regression. |
| **α/C Decay (WKB)** | Semiclassical barrier penetration with a configurable nuclear potential: Woods–Saxon, WS², Gaussian, Yukawa and exponential terms in any combination, an optional surface term, a custom analytic V(r) or a numerical (r, V) table. Shows three turning points, Gamow factor G, assault frequency and log₁₀T½. Includes batch runs, residual analysis and global optimisation of the potential and preformation factor. |
| **p/2p Decay** | Proton and two-proton emission using the same WKB machinery. Q₂ₚ is clearly labelled when it is derived from masses instead of a dedicated database value. |
| **n/2n Decay** | Neutron and two-neutron emission through a neutral-particle effective barrier, with angular momentum derived from Jπ where it is unique. |
| **Spontaneous Fission** | Empirical SF partial half-life fits against fissility (linear, quadratic, and quadratic with odd-Z/odd-N hindrance), with a data audit, residual statistics and multi-model comparison. |
| **Decay Chain** | Builds the daughter network from listed branches and solves the Bateman equations. Plots abundance and activity against time and draws the pathway diagram, endpoint probabilities and branch-competition diagnostics. |
| **Theory** | Equations and physics background for every model used. |
| **Manual** | Built-in user guide with recommended workflows and common pitfalls. |

Other details:
- Night and day themes
- All equations rendered with MathJax
- Interactive Plotly charts with zoom, pan, hover and PNG export

---

## Recommended workflow

1. **Decay Systematics**: get an overview and pick the nuclei of interest.
2. **Mass & Binding** and **Drip-Line & Shell**: look at structure and shell effects.
3. **Empirical α Decay** and **Empirical α/β/C Decay**: establish the empirical systematics.
4. **α/C Decay (WKB)**: test a physical barrier model. Run one channel first (the default benchmark is α + ¹⁰⁶Te → ¹⁰²Sn), record a baseline, and only then run the global optimisation.
5. Use **Decay Chain** for time evolution and **Spontaneous Fission** for heavy nuclei.

The **Manual** tab has step-by-step instructions for each of these.

---

## Caveats

- Empirical fits depend on the filters you choose. Changing the Z range changes the coefficients.
- A high in-sample R² is not independent validation. Use CV-RMSE, AIC or BIC to compare models.
- A positive Q value means a decay is energetically allowed. It does not determine a unique half-life.
- The shell plot shows the empirical residual B_exp − B_SEMF, not a microscopic Strutinsky calculation.
- The 2n mode uses Qₙ as a proxy, and mass-derived Q₂ₚ values are not experimental 2p observations. Experimental angular momentum is never invented.
- The empirical α fits use unweighted log residuals, because per-nuclide uncertainties are not part of the embedded α dataset.

---

## Tech stack

- Plain HTML, CSS and JavaScript in a single self-contained file
- [Plotly.js](https://plotly.com/javascript/) 2.32 for charts
- [MathJax](https://www.mathjax.org/) 3 for equations
- Fonts: Space Grotesk, JetBrains Mono, Orbitron

---

## Data source and citation

Nuclear data comes from the **NUBASE2020** evaluation:

> F. G. Kondev, M. Wang, W. J. Huang, S. Naimi, and G. Audi, "The NUBASE2020 evaluation of nuclear physics properties," *Chinese Physics C* **45**, 030001 (2021). doi:[10.1088/1674-1137/abddae](https://doi.org/10.1088/1674-1137/abddae)

Reference tables: [IAEA Nuclear Data Services · NUBASE](https://www-nds.iaea.org/relnsd/nubase/nubase_min.html)

If you use this tool in published work, please cite the NUBASE2020 paper above.

---

## License

This project is licensed under the **GNU General Public License v3.0**. See [`LICENSE`](LICENSE) for the full text.

You are free to use, study, modify and redistribute this software. Any distributed modified version must also be released under the GPL-3.0, with its source code available.

The NUBASE2020 data stays subject to the terms of its original publication.
