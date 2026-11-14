# MetabolismMath

A browser-based calculator that estimates how a vitamin or supplement is metabolized from its chemical composition.

**Live site:** https://mendus59.github.io/MetabolismMath/

## What it does

- **Compound library:** 24 vitamins, minerals and supplements. Each entry has its documented absorption → transport → transformation → function → storage → excretion pathway, plus a note on safety concerns.
- **Paste a SMILES structure:** RDKit parses it in the browser and calculates the formula, Crippen logP, polar surface area and H-bond donors/acceptors. It runs the full Lipinski Rule of 5 + Veber screen, auto-detects functional groups (carboxylic acid, ester, amine, aromatic ring, N-heterocycle, phosphate, long chain) and draws the 2D structure.
- **Formula-only mode:** enter a molecular formula, including groups and hydrates like `Mg3(C6H5O7)2` or `C4H9N3O2·H2O`, and tick structural features by hand.
- **Fate prediction:** a rule-based estimate of how a dose splits between being burned for energy, used as a cofactor, stored, transformed and eliminated, fermented by gut microbes, or excreted unchanged. Library entries show the documented split next to the prediction.
- **Energy:** the theoretical energy from full oxidation (Thornton's rule) and the energy actually usable at your dose.
- **Dose check:** your dose compared against US adult RDA/AI and UL values.

## Running locally

It's a static site with no build step. Serve the folder over HTTP so the WebAssembly file loads:

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Notes

- `vendor/rdkit/` contains RDKit.js 2026.3.6 (`@rdkit/rdkit` on npm, BSD-3-Clause), vendored so the site doesn't depend on a CDN.
- The prediction uses heuristics for learning purposes. This is not medical advice. Reference data comes mainly from the [NIH Office of Dietary Supplements fact sheets](https://ods.od.nih.gov/factsheets/list-all/).
