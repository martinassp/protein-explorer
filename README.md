# Protein Explorer

An interactive single-page web tool for exploring human protein biology, built for lysosome and cell biology research. Available at **[martinassp.github.io/protein-explorer](https://martinassp.github.io/protein-explorer/)**.

---

## What it does

Search any human gene symbol to retrieve an integrated view across:

- **Protein summary** — UniProt annotation, function, subcellular localisation, disease associations (Open Targets)
- **Expression** — tissue RNA/protein (Human Protein Atlas), single-cell RNA, blood & immune cells, cancer cell lines (nTPM across 1,206 lines grouped by TCGA cancer type)
- **Interactions** — physical (BioGRID), predicted structural (humanPPI / AlphaFold2), STRING (live fetch)
- **Co-essentiality** — DepMap CRISPR screens (1,178 cell lines, Pearson r), TheCellMap genetic interactions
- **Lysosomal proteomics** — multiple LysoIP datasets (see below)
- **Literature** — PubMed search with omics paper highlighting

All core databases are embedded offline in the page; live API calls (UniProt, Open Targets, PubMed, STRING, TheCellMap) are optional enrichments.

---

## Network views

### Network tab (single gene)
Force-directed graph centred on the queried gene. Toggle data layers:
- **BioGRID** — bidirectional physical interactions (forward + reverse lookup), filterable by minimum evidence count
- **Co-essentiality** — DepMap top-30 partners (optional bidirectional)
- **humanPPI** — AlphaFold2 predicted interactions
- **STRING** — live fetch
- **TheCellMap** — static genetic interaction edges + live double-KO scores

Click a node to expand its neighbourhood. Partners slider applies to all expanded nodes.

### Gene List tab
Paste a list of gene symbols to build a multi-gene network. Features:
- Auto-resolves gene aliases via UniProt (e.g. IF4E → EIF4E, TM109 → TMEM109)
- Cross-edges between list members
- Node expand (⊕) / remove (✕) per gene
- Export to SVG or **XGMML** (Cytoscape-compatible, File → Import → Network from File)

---

## Lysosomal proteomics datasets

| Dataset | Cells | Condition | Status |
|---------|-------|-----------|--------|
| **Brain Lysosome Atlas** | Mouse brain regions | LysoIP enrichment | Published — [Schink et al., *Mol. Cell. Proteomics* 2023](https://doi.org/10.1016/j.mcpro.2023.100509) |
| **iNeuron LysoIP** | iPSC-derived neurons (day 21) | LysoIP + Endo-IP | Published — [Hundley et al., *PNAS* 2024](https://pubmed.ncbi.nlm.nih.gov/39636867/) |
| **LysoIP ±LLOMe (KP4)** | KP4 pancreatic cancer cells | ±LLOMe 0.5 mM, 15 min | **Unpublished** — Winter Lab |

The KP4 ±LLOMe dataset is the only available LysoIP proteomics experiment capturing the acute lysosomal membrane damage response.

---

## Data sources & references

| Source | Version / Description | Reference |
|--------|-----------------------|-----------|
| **BioGRID** | v4.4.212 — physical protein interactions | [thebiogrid.org](https://thebiogrid.org) |
| **DepMap** | CRISPRGeneEffect — 1,178 cell lines, Pearson r ≥ 0.15 | [depmap.org](https://depmap.org) |
| **humanPPI** | AlphaFold2-predicted interactions | Zhang et al., *Science* 2025 |
| **STRING** | Score ≥ 700 — live fetch | [string-db.org](https://string-db.org) |
| **TheCellMap** | Pairwise CRISPR double-KO, HAP1 haploid cells | [Billmann et al., *Cell* 2026](https://doi.org/10.1016/j.cell.2026.03.044) |
| **Human Protein Atlas** | v25 — tissue RNA/protein, single cell, cell lines | [proteinatlas.org](https://www.proteinatlas.org) |
| **GTEx + FANTOM5** | Consensus RNA expression | [gtexportal.org](https://www.gtexportal.org) |
| **Brain Lysosome Atlas** | Mouse brain LysoIP enrichment | [Schink et al., *MCP* 2023](https://doi.org/10.1016/j.mcpro.2023.100509) |
| **iNeuron LysoIP** | iPSC neuron lysosomal proteome | [Hundley et al., *PNAS* 2024](https://pubmed.ncbi.nlm.nih.gov/39636867/) |
| **LysoIP ±LLOMe KP4** | Unpublished — Winter Lab | — |
| **UniProt** | Live annotation | [uniprot.org](https://www.uniprot.org) |
| **Open Targets** | Disease associations, DepMap tissue context | [platform.opentargets.org](https://platform.opentargets.org) |

---

## Technical notes

- **Single-file app** — all databases are gzip + base64 encoded inside `index.html` (~35 MB). No backend required.
- **Offline-first** — core databases work without internet; live APIs enhance but are not required.
- Built with D3.js (v7), plain JavaScript, no framework.

---

## Lab

Developed in the **Winter Lab**, University of California Berkeley.
