# Shared Resource Citation Generator

An interactive web tool that helps Dartmouth researchers generate the correct **grant numbers** and **RRIDs** for every Dartmouth Cancer Center Shared Resource used in their manuscripts, posters, or presentations.

## Features

- **One-click selection** of any combination of the eleven Dartmouth Cancer Center Shared Resources, grouped by core
- **Automatic inclusion** of the NCI Cancer Center Support Grant (`P30CA023108`) on every citation list
- **Conditional grants** — instrument- or service-specific awards (e.g. `S10OD030242`, `P20GM130454`, `R24GM141194`) are added only when their associated resource is selected
- **RRIDs included** for every shared resource so manuscripts comply with NIH Rigor & Reproducibility guidance
- **Authorship note** automatically surfaces when Biostatistics & Biomedical Informatics is selected, reminding users that BBI faculty should be included as authors
- **Copy to Clipboard** produces a clean, plain-text citation list ready to paste into a manuscript draft
- **"Draft Acknowledgement in Claude"** button opens claude.ai with a pre-built prompt that turns the selections into a publication-ready acknowledgement paragraph
- **Zero dependencies** — entirely self-contained HTML/CSS/JavaScript, no external libraries required

## Files

| File | Description |
|------|-------------|
| `citation-generator.html` | The widget — served via GitHub Pages and embedded into the omics.dartmouth.edu page with an auto-resizing iframe |
| `website-setup-instructions.md` | Step-by-step guide for embedding the generator on omics.dartmouth.edu |

## Getting Started

1. Open `citation-generator.html` in any modern browser
2. Expand each shared resource category (all are open by default)
3. Tick the resources you used
4. Copy the generated citation list, or open Claude to draft a full acknowledgement paragraph

## Deployment

`citation-generator.html` is served via GitHub Pages and embedded on the WordPress site using an auto-resizing iframe. See `website-setup-instructions.md` for the iframe snippet and step-by-step instructions for embedding the generator at `omics.dartmouth.edu/shared-resource-acknowledgment-generator/`.

## Updating Resource Data

Grant numbers, RRIDs, directors, and the resource list are stored in the JavaScript `resources` array near the top of the `<script>` block in `citation-generator.html`. To add or update a resource:

1. Edit the relevant object in the `resources` array (or append a new one)
2. Commit and push to `main`
3. GitHub Pages republishes automatically and every embedding page picks up the change on next load

The universal Cancer Center Support Grant is stored in the `UNIVERSAL_GRANT` constant directly above the `resources` array.

## Tech Stack

- **HTML5 / CSS3 / Vanilla JavaScript** — no frameworks or build tools
- **Dartmouth green** primary color (`#00693E`)
- **Scoped CSS resets** defeat the parent WordPress theme's default list/link/header styling
- **postMessage** auto-resizes the iframe to content height on omics.dartmouth.edu

## License

Internal use — Dartmouth College / Geisel School of Medicine.
