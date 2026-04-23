# LanguagesViz

Small local viewer for the European Indo-European DendroViz SVG.

## Public site

The GitHub Pages workflow publishes the viewer at:

```text
https://lb930.github.io/LangiagesViz/
```

## View locally

Run a static server from the repository root:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000/
```

The page embeds `SVGs/european_leaf_labels_only.svg` and adds pan/zoom with `svg-pan-zoom`.

## Recreate the SVG

The SVG is generated with DendroViz from `src/indo_european_without_indo_iranian.nwk`.

```bash
python3 - <<'PY'
from dendroviz.api import DendrogramGenerator
from dendroviz.models import LayoutOptions

gen = DendrogramGenerator()
opts = LayoutOptions(
    font_size=6,
    node_radius=3,
    label_mode='leaves',
    colour_mode='palette',
    palette='#1f77b4,#ff7f0e,#2ca02c,#d62728,#9467bd,#8c564b,#e377c2,#7f7f7f,#bcbd22,#17becf,#393b79,#637939,#8c6d31,#843c39,#7b4173,#3182bd',
    palette_depth=2,
    show_palette_legend=True,
    show_svg_titles=True,
    show_svg_data_attributes=True,
)

gen.generate_tree(
    'src/indo_european_without_indo_iranian.nwk',
    tree_layout='radial',
    line_style='split',
    input_format='newick',
    output_svg='SVGs/european_leaf_labels_only.svg',
    show_labels=True,
    options=opts,
)
PY
```
