# Research Report: How to Produce Highly Polished Data Visualizations in R and Python

## Purpose

This document is a practical, opinionated guideline for agents and analysts who need to create **clear, polished, publication-ready, presentation-ready, or product-ready data visualizations** in either **R** or **Python**.

It is written to optimize for four outcomes:

1. **Truthfulness** — the chart should not distort the data.
2. **Readability** — the main message should be legible in seconds.
3. **Aesthetic polish** — the chart should look deliberate, modern, and consistent.
4. **Reproducibility** — the chart should be easy to regenerate and maintain.

This is not a catalog of every plotting library. It is a decision framework and execution guide for making the **best-looking charts that still communicate well**.

---

## Executive Summary

### Recommended default stack in R

For most professional static charts, the best default stack is:

- **`ggplot2`** for chart construction
- **`scales`** for axis/legend formatting
- **`patchwork`** for multi-panel composition
- **`ragg`** for high-quality raster export
- **`svglite`** for clean SVG export
- **`viridis` / `viridisLite` or `colorspace`** for robust palettes
- **`systemfonts`** (and compatible devices) for typography
- **Quarto** for final report integration and figure management

### Recommended default stack in Python

For most professional static charts, the best default stack is:

- **`seaborn` + `matplotlib`** for polished statistical and publication-style charts
- **`Altair`** for declarative analytical charts and fast iteration on encodings
- **`Plotly`** only when real interactivity is part of the deliverable
- **`matplotlib` rcParams/style sheets** for global style control
- **perceptually uniform colormaps** for continuous scales
- vector export (`SVG`/`PDF`) for print and `PNG` for slides and web previews

### Strong recommendation by output type

- **Publication/report figures**: prefer **R (`ggplot2`)** or **Python (`seaborn`/`matplotlib`)**.
- **Analytical exploratory charts with concise declarative specs**: prefer **R (`ggplot2`)** or **Python (`Altair`)**.
- **Interactive stakeholder deliverables**: prefer **Python (`Plotly`)**, unless the surrounding stack strongly favors R.
- **Multi-panel figure composition**: prefer **R (`patchwork`)** or Python with explicit `matplotlib` layout control.

### The single most important principle

A polished chart is not mainly the product of fancy styling. It is the product of:

- choosing the correct chart form,
- reducing clutter,
- using strong hierarchy,
- formatting text and numbers well,
- handling color carefully,
- and exporting with professional settings.

---

## What “polished” means in practice

A polished chart has most of the following properties:

- A clear takeaway is visible within 3–5 seconds.
- The title is informative rather than generic.
- Axes use sensible limits and humane number formatting.
- Color is intentional and sparse.
- Gridlines are subdued, not dominant.
- Fonts, sizing, spacing, legends, and annotations feel consistent.
- There is no accidental crowding, clipping, or overlap.
- The chart still works in grayscale, on a projector, and at small sizes.
- Export quality is appropriate for the medium.

A chart is **not** polished merely because it has gradients, rounded corners, drop shadows, or many annotations.

---

# Part I — Universal Rules for High-Quality Data Visualization

## 1. Start with the message, not the chart type

Before writing plotting code, specify:

- the main claim,
- the comparison that matters,
- the audience,
- the medium,
- and whether the figure is meant to be read quickly or studied carefully.

Use this template internally:

> “This chart should show **what** to **whom** so they can understand **which decision or conclusion**.”

If the message cannot be stated in one sentence, the chart is probably trying to do too much.

---

## 2. Choose the simplest chart that answers the question

### Use a bar chart when

- comparing magnitudes across categories,
- ranking categories,
- showing a small number of grouped comparisons.

### Use a line chart when

- showing change over ordered time or another continuous sequence,
- comparing trajectories,
- highlighting trend direction or turning points.

### Use a scatter plot when

- showing relationship, spread, clusters, or outliers,
- comparing many observations in two continuous dimensions.

### Use a dot plot / lollipop plot when

- ranking categories,
- showing estimates with a cleaner look than bars,
- emphasizing position rather than filled area.

### Use a box plot / violin / interval plot when

- comparing distributions,
- showing uncertainty or spread,
- avoiding misleading summaries based only on means.

### Use heatmaps only when

- the matrix structure matters,
- both axes are ordered meaningfully,
- the audience can still decode a color scale without strain.

### Avoid by default

- pie charts for precise comparisons,
- 3D charts,
- dual-axis charts unless the alignment is genuinely necessary and carefully labeled,
- rainbow palettes for ordered data,
- legends that duplicate direct labeling opportunities.

---

## 3. Prefer position and length over area, angle, or saturated color

Human perception is better at comparing positions and aligned lengths than areas, angles, or arbitrary color intensity. Therefore:

- prefer dots over donuts,
- prefer line charts over color-only encodings,
- prefer direct comparisons on common axes,
- use color as support, not as the only carrier of meaning.

---

## 4. Build visual hierarchy deliberately

Every chart should make some elements visually dominant and others recessive.

### High emphasis

Use stronger contrast for:

- data marks that carry the main message,
- the title/subtitle,
- reference lines that matter,
- a highlighted series or category.

### Low emphasis

Use lighter contrast for:

- background,
- minor gridlines,
- secondary tick marks,
- contextual labels,
- non-highlighted series.

A useful rule:

- **one primary color**,
- **one neutral text color**,
- **one light structural color** for gridlines/spines,
- optional **one accent color**.

---

## 5. Titles should communicate the finding, not the topic

Weak title:

> Sales by Region

Better title:

> West and South led sales growth in 2025, while North was flat

Use a subtitle when needed to define:

- metric,
- date range,
- geography,
- units,
- exclusions,
- source notes.

A polished chart often reads like a miniature argument:

- **Title**: takeaway
- **Subtitle**: scope and context
- **Caption/note**: methodology and source

---

## 6. Format numbers as if they were prose

Bad formatting instantly makes a chart feel unfinished.

Use:

- `1.2M` instead of `1200000` when appropriate,
- `%` only when values are truly percentages,
- currency symbols consistently,
- as few decimals as the decision requires,
- date formats consistent with audience expectations,
- no scientific notation unless the domain expects it.

Precision should reflect real certainty. Avoid fake precision.

---

## 7. Use color with semantic discipline

### For categorical data

Use distinct hues with moderate saturation.

### For continuous ordered data

Use perceptually uniform sequential scales.

### For data centered on a meaningful midpoint

Use diverging scales with an explicit neutral center.

### Avoid

- rainbow scales for quantitative data,
- using red/green as the only contrast,
- too many category colors,
- strong saturated backgrounds.

Also test whether the chart still works when printed in grayscale or viewed by someone with color-vision deficiency.

---

## 8. Typography matters more than many users realize

Professional charts usually have:

- one font family,
- 3–4 text sizes total,
- consistent weight hierarchy,
- enough white space around titles and panels,
- wrapped labels where needed,
- sentence case rather than all caps.

Good typography is a major part of perceived polish.

---

## 9. Annotation is often better than additional complexity

Instead of adding another panel, legend, or encoding, consider:

- a direct label,
- a callout,
- a reference line,
- a short note explaining the inflection point,
- or highlighting the specific subset that matters.

Annotation should reduce cognitive load, not add another paragraph inside the figure.

---

## 10. Design for the final medium

A chart for a slide deck is not the same as a chart for print.

### For slides

- larger fonts,
- fewer categories,
- stronger contrast,
- less subtle detail,
- usually 16:9-aware sizing.

### For print/PDF

- tighter spacing is acceptable,
- smaller details can survive,
- vector output is preferred when possible.

### For dashboards/web

- interaction must have a purpose,
- hover should not be required to understand the primary message,
- mobile layout constraints matter.

---

## 11. Accessibility is part of polish

Include, where possible:

- sufficient contrast,
- readable font sizes,
- non-color redundancies (shape, line type, text, position),
- alt text or descriptive captions,
- explicit units,
- enough annotation to make the chart understandable outside its original report.

---

## 12. Reproducibility is a design principle

A chart that looks good once but is brittle is not a professional workflow.

Use:

- a reusable theme/template,
- central palette definitions,
- reusable formatting functions,
- parameterized export settings,
- deterministic figure sizes,
- version-controlled code.

---

# Part II — How to Make the Best Polished Visualizations in R

## Why R remains excellent for polished static graphics

R’s strongest advantage is its mature grammar-of-graphics workflow. The `ggplot2` ecosystem makes it unusually easy to:

- map data to visual encodings declaratively,
- create visually consistent charts,
- scale styling decisions across many figures,
- compose panels and annotations cleanly,
- export attractive publication-quality output.

For static analytical and editorial graphics, R is still one of the strongest environments available.

---

## Best default R stack

### Core charting

- **`ggplot2`** should be the default.

Use it for almost all standard analytical graphics unless a very specific specialized library is warranted.

### Essential supporting packages

- **`scales`** for axis labels, percentages, currency, dates, p-values, log labeling, and human-readable number formatting.
- **`patchwork`** for assembling multi-panel layouts with alignment.
- **`ragg`** for crisp raster output.
- **`svglite`** for clean editable SVG output.
- **`viridis` / `viridisLite`** for safe continuous/discrete palettes.
- **`colorspace`** when you need more deliberate palette engineering.
- **`systemfonts`** for modern font handling with supported devices.

### Reporting and integration

- **Quarto** for production reporting, figure captions, cross-references, alt text, and multi-format rendering.

---

## The R philosophy for polished charts

The best R workflow is:

1. structure data cleanly,
2. build the minimal `ggplot`,
3. refine scales and labels,
4. refine theme and hierarchy,
5. annotate,
6. export with an appropriate device.

Do **not** start by tweaking twenty theme options before confirming that the chart form is correct.

---

## R package recommendations by use case

### 1. Publication-quality static charts

Use:

- `ggplot2`
- `scales`
- `patchwork`
- `ragg`
- `svglite`

This should be your default editorial/reporting stack.

### 2. Branded organizational charts

Use:

- `ggplot2`
- custom `theme_*()` wrappers
- organization palette objects
- `svglite` or `ragg`

Create internal helper functions rather than styling each plot manually.

### 3. Color-critical work

Use:

- `viridis`/`viridisLite` for dependable defaults,
- `colorspace` for engineered qualitative, sequential, and diverging palettes.

### 4. Multi-panel scientific or executive figures

Use:

- `patchwork`
- optionally collect guides and titles,
- standardize axis titles and spacing.

---

## A recommended R visual style system

Create a house style rather than ad hoc styling.

### Example design defaults

- Base font family: one modern sans-serif or one publication-appropriate serif.
- Background: white.
- Major gridlines: light gray only where helpful.
- Minor gridlines: usually removed.
- Axis titles: visible but subdued.
- Plot title: larger and bolder than body text.
- Subtitle/caption: smaller and neutral.
- Legends: top or right only if direct labeling is not feasible.
- Panel borders: usually removed unless the chart type benefits from enclosure.

### Example reusable theme skeleton

```r
library(ggplot2)

theme_agent <- function(base_family = "Inter", base_size = 11) {
  theme_minimal(base_family = base_family, base_size = base_size) +
    theme(
      plot.title.position = "plot",
      plot.caption.position = "plot",
      plot.title = element_text(face = "bold", size = rel(1.35), margin = margin(b = 8)),
      plot.subtitle = element_text(size = rel(1.0), colour = "#4D4D4D", margin = margin(b = 10)),
      plot.caption = element_text(size = rel(0.85), colour = "#666666", margin = margin(t = 10)),
      axis.title = element_text(size = rel(0.95), colour = "#333333"),
      axis.text = element_text(size = rel(0.9), colour = "#444444"),
      legend.position = "top",
      legend.title = element_text(face = "bold"),
      panel.grid.minor = element_blank(),
      panel.grid.major.x = element_blank(),
      panel.grid.major.y = element_line(colour = "#E6E6E6", linewidth = 0.35)
    )
}
```

This is not the only good theme. The important principle is to define a **reusable system**.

---

## R-specific best practices that most improve polish

## 1. Use `scales` aggressively

Formatting is one of the easiest places to gain professionalism.

Examples:

```r
library(scales)

scale_y_continuous(labels = label_number(scale_cut = cut_short_scale()))
scale_y_continuous(labels = label_percent(accuracy = 1))
scale_x_date(labels = label_date_short())
scale_fill_continuous(labels = label_number(accuracy = 0.1))
```

Agents should almost never leave raw numeric labels untouched when the audience is non-technical.

---

## 2. Prefer direct labels when there are few series

For a line chart with 2–5 series, direct labeling often looks cleaner than a legend.

Use the legend only when direct labeling would clutter the figure.

---

## 3. Avoid default bar ordering when rank matters

For categorical comparisons, order categories by the metric unless natural ordering matters.

```r
library(forcats)

ggplot(df, aes(x = fct_reorder(category, value), y = value)) +
  geom_col()
```

Unordered bars often make a chart feel unfinished.

---

## 4. Tune text and label wrapping deliberately

Long labels destroy polish quickly. Use line breaks, abbreviations, or wrapped labels.

```r
scale_x_discrete(labels = label_wrap(18))
```

---

## 5. Use `patchwork` for figure composition, not manual hacks

Instead of manually saving separate charts and combining them elsewhere, compose in code.

```r
library(patchwork)

(p1 | p2) /
  p3 +
  plot_annotation(
    title = "Main figure title",
    subtitle = "Shared context across panels"
  )
```

Consistency of alignment is a major contributor to perceived quality.

---

## 6. Export with `ragg` for raster and `svglite` for vector

### Raster export

Use `ragg::agg_png()` when you need high-quality PNG output.

```r
ggsave(
  "figure.png",
  plot = p,
  device = ragg::agg_png,
  width = 8,
  height = 5,
  units = "in",
  res = 300
)
```

### Vector export

Use SVG or PDF for print, editing, or scaling.

```r
ggsave(
  "figure.svg",
  plot = p,
  device = svglite::svglite,
  width = 8,
  height = 5,
  units = "in"
)
```

For many workflows:

- `PNG` for slides, docs, and web previews,
- `SVG` for web or post-editing,
- `PDF` for publication and print.

---

## 7. Use font-aware devices and stable typography

Font inconsistency is a common source of unpolished output.

Best practice:

- use fonts installed and available in the execution environment,
- use `systemfonts`-compatible workflows,
- verify output on the actual export device,
- avoid relying on a font that is unavailable in CI or on collaborators’ machines.

Typography should be treated as part of reproducibility, not just cosmetics.

---

## 8. Use perceptually sensible color scales

### Continuous data

Prefer `scale_colour_viridis_c()` / `scale_fill_viridis_c()` or carefully designed `colorspace` scales.

### Discrete categories

Use muted but distinguishable hues. Reserve the accent color for the focal series.

### Diverging data

Use diverging palettes only when a meaningful midpoint exists.

Example:

```r
ggplot(df, aes(x, y, fill = delta)) +
  geom_tile() +
  scale_fill_gradient2(midpoint = 0)
```

Do not use diverging palettes for data with no semantic center.

---

## 9. Use annotations to turn a chart into an argument

Examples of effective annotation in R:

- `geom_text()` or `geom_label()` for selected points,
- `annotate()` for commentary,
- `geom_hline()` or `geom_vline()` for targets or events,
- light shading for periods of interest.

But annotate only what matters. Over-annotation creates noise.

---

## 10. Standardize aspect ratio and figure dimensions

A chart often looks unprofessional because it was exported at a random size.

Create standard sizes such as:

- narrow single-column: 6 x 4 in
- wide report figure: 8 x 4.5 in
- slide figure: 10 x 5.625 in
- square analytical panel: 5 x 5 in

Design at the actual target size whenever possible.

---

## R chart-type guidance

## Polished bar charts in R

Use when comparing categories.

Rules:

- start axis at zero unless not using bar geometry,
- order categories intentionally,
- remove unnecessary outlines,
- label directly if there are few bars,
- use horizontal bars when labels are long,
- avoid stacked bars beyond a few categories.

Example:

```r
p <- ggplot(df, aes(x = fct_reorder(category, value), y = value)) +
  geom_col(fill = "#356AE6", width = 0.7) +
  coord_flip() +
  scale_y_continuous(labels = scales::label_number(scale_cut = scales::cut_short_scale())) +
  labs(
    title = "Category A leads on the primary metric",
    x = NULL,
    y = "Value"
  ) +
  theme_agent()
```

---

## Polished line charts in R

Rules:

- emphasize the focal series,
- reduce the prominence of comparison series,
- label line endpoints when feasible,
- keep gridlines light,
- mark major events only if relevant.

For multiple series, avoid a rainbow legend. Highlight what matters.

---

## Polished scatter plots in R

Rules:

- use transparency for dense points,
- size markers conservatively,
- add a trend only when analytically justified,
- label only key outliers or exemplars,
- avoid overplotting with raw text labels.

---

## Polished faceted charts in R

Faceting is excellent when small multiples support a common comparison.

Rules:

- keep scales common unless a different comparison is intended,
- simplify within-panel clutter,
- keep panel titles short,
- avoid too many facets on a slide,
- prefer `patchwork` if panels need unequal emphasis or custom composition.

---

## When not to use R as the primary visualization tool

R is not the strongest default when:

- the deliverable depends heavily on browser-native interaction,
- the surrounding application stack is Python web tooling,
- the chart must be embedded in a reactive product environment already built in Python or JavaScript.

Even then, R can still be excellent for prototyping and publication graphics.

---

## Recommended R workflow for agents

1. Identify the chart’s claim.
2. Pick the simplest chart form that supports that claim.
3. Build a minimal `ggplot2` figure.
4. Apply semantic scales and humane labels with `scales`.
5. Apply the house theme.
6. Highlight the focal series/category.
7. Add one layer of annotation if useful.
8. Check small-size readability.
9. Export both PNG and SVG/PDF where appropriate.
10. Reuse the same theme and palette objects across the project.

---

## R “do” and “don’t” list

### Do

- use `ggplot2` as the default,
- create a custom theme wrapper,
- control formatting through `scales`,
- use `patchwork` for panel composition,
- export intentionally with `ragg`/`svglite`,
- test fonts on the actual render target,
- use perceptually sound palettes.

### Don’t

- accept raw defaults blindly,
- mix many unrelated hues,
- overload charts with geoms and annotations,
- use legends when direct labels are better,
- export at arbitrary sizes,
- rely on inaccessible or non-reproducible fonts.

---

# Part III — How to Make the Best Polished Visualizations in Python

## Why Python is strong for polished data visualization

Python’s great strength is flexibility across contexts:

- notebook analysis,
- production analytics,
- machine learning workflows,
- dashboarding,
- interactive web visualizations,
- and export to many surrounding systems.

Its main tradeoff is that polished output often requires more style discipline than in R. You usually need to define stronger defaults yourself.

The reward is a very powerful ecosystem.

---

## Best default Python stack

### 1. `seaborn` + `matplotlib`

This is the best general-purpose default for polished static charts in Python.

Use:

- `seaborn` for high-level statistical charting and better defaults,
- `matplotlib` for precise control, layout, export, typography, and advanced customization.

### 2. `Altair`

This is excellent when you want:

- concise declarative chart specifications,
- explicit control of encodings,
- rapid iteration,
- interactive analytical visuals without low-level plotting code.

It is especially strong for tidy tabular analytical charting.

### 3. `Plotly`

Use Plotly when:

- interactivity is part of the product,
- hover, zoom, selection, or embedding matter,
- the audience will consume the chart in a browser.

Do not choose Plotly just because it looks modern. Use it when interaction adds value.

---

## The Python philosophy for polished charts

The best Python workflow is to separate:

- **chart grammar / API choice**,
- **global style system**,
- **layout control**,
- **export configuration**.

A polished Python workflow typically depends on having a **reusable style template** just as much as on selecting the plotting library.

---

## Package recommendations by use case

### 1. Publication/report static figures

Use:

- `seaborn`
- `matplotlib`

### 2. Declarative analytical charts

Use:

- `Altair`

### 3. Interactive stakeholder or product charts

Use:

- `Plotly`

### 4. Scientific or highly custom composed figures

Use:

- `matplotlib` directly,
- optionally with seaborn theme helpers.

---

## A recommended Python visual style system

The single biggest improvement most Python codebases need is a project-wide style layer.

### Example matplotlib/seaborn style setup

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_theme(
    context="notebook",
    style="whitegrid",
    font="DejaVu Sans",
    font_scale=1.0,
    rc={
        "axes.spines.top": False,
        "axes.spines.right": False,
        "axes.edgecolor": "#D9D9D9",
        "grid.color": "#E6E6E6",
        "grid.linewidth": 0.6,
        "axes.labelcolor": "#333333",
        "xtick.color": "#444444",
        "ytick.color": "#444444",
        "text.color": "#222222",
        "axes.titleweight": "bold",
        "figure.dpi": 120,
        "savefig.dpi": 300,
    },
)
```

Then refine individual charts only where needed.

---

## Python-specific best practices that most improve polish

## 1. Let seaborn set the baseline, then refine in matplotlib

This is often the best pattern:

1. create the figure with seaborn,
2. get the axes object,
3. refine labels, ticks, limits, annotations, legend placement, and export in matplotlib.

Example:

```python
import matplotlib.pyplot as plt
import seaborn as sns
import matplotlib.ticker as mtick

fig, ax = plt.subplots(figsize=(8, 5), layout="constrained")

sns.lineplot(data=df, x="date", y="value", hue="group", linewidth=2, ax=ax)

ax.set_title("The focal series accelerated in the second half of the year", loc="left", pad=12)
ax.set_xlabel("")
ax.set_ylabel("Revenue")
ax.yaxis.set_major_formatter(mtick.StrMethodFormatter("${x:,.0f}"))

sns.move_legend(ax, "upper left", bbox_to_anchor=(1, 1), frameon=False, title=None)

plt.show()
```

This workflow combines better defaults with precise finishing control.

---

## 2. Use layout management intentionally

Crowded layout is one of the fastest ways to make charts look amateurish.

Prefer `layout="constrained"` or constrained layout workflows for multi-axes figures.

```python
fig, ax = plt.subplots(figsize=(8, 5), layout="constrained")
```

If labels, legends, and colorbars overlap, the chart is not finished.

---

## 3. Use rcParams or style sheets rather than repeated one-off tweaks

For organizational consistency, define style in one place.

Use:

- `sns.set_theme(...)`
- `plt.rcParams[...] = ...`
- custom matplotlib style sheets when appropriate.

Do not hard-code every cosmetic choice separately in every chart file.

---

## 4. Use humane formatters for axes and labels

Matplotlib’s formatting stack is powerful and underused.

Examples:

```python
import matplotlib.ticker as mtick

ax.yaxis.set_major_formatter(mtick.StrMethodFormatter("{x:,.0f}"))
ax.yaxis.set_major_formatter(mtick.PercentFormatter(1.0))
```

For dates, use date locators/formatters deliberately instead of trusting defaults on dense time series.

---

## 5. Prefer perceptually uniform colormaps for quantitative data

For continuous scales, prefer perceptually uniform options such as `viridis`, `plasma`, `inferno`, `magma`, or `cividis` where appropriate.

Avoid rainbow scales for ordered data.

For diverging data, ensure there is a genuine conceptual midpoint.

---

## 6. Use seaborn’s objects interface when composability is valuable

The `seaborn.objects` interface is especially useful when you want a more declarative, layered plotting style in Python.

It can make complex chart specifications cleaner than traditional function-based seaborn code in some workflows.

Example:

```python
import seaborn.objects as so

(
    so.Plot(df, x="x", y="y", color="group")
    .add(so.Line(), so.Agg())
    .label(
        title="Grouped trend comparison",
        x="Date",
        y="Value"
    )
)
```

Use this when it improves clarity, not as a stylistic requirement.

---

## 7. Use Altair when encoding logic matters more than low-level control

Altair is excellent for analytical charts because encoding, scale, sort, aggregation, binning, and interaction are expressed directly in the chart specification.

Example:

```python
import altair as alt

chart = (
    alt.Chart(df)
    .mark_line()
    .encode(
        x=alt.X("date:T", title="Date"),
        y=alt.Y("value:Q", title="Revenue", scale=alt.Scale(zero=False)),
        color=alt.Color("group:N", title=None)
    )
    .properties(
        width=700,
        height=350,
        title="The focal series accelerated in late 2025"
    )
)
```

Use Altair when you want readable chart specifications and easy control over encodings.

---

## 8. Use Plotly templates rather than styling figures ad hoc

When using Plotly, define a template strategy.

Example:

```python
import plotly.io as pio

pio.templates.default = "plotly_white"
```

Then refine only what is chart-specific.

This creates more consistent visuals than per-chart manual formatting.

---

## 9. Export properly

### Matplotlib static export

Use `savefig()` intentionally.

```python
fig.savefig(
    "figure.png",
    dpi=300,
    bbox_inches="tight",
    pad_inches=0.1,
)
```

Also export SVG/PDF for vector workflows when appropriate.

### Plotly static export

Use Kaleido-backed export where needed.

```python
fig.write_image("figure.svg")
fig.write_image("figure.png", scale=2)
```

### Plotly HTML export

Use HTML when interactivity is part of the artifact.

```python
fig.write_html("figure.html")
```

A polished chart must survive the chosen delivery format.

---

## 10. Remove decorative clutter explicitly

In Python, polish often comes from removing defaults that are technically fine but visually noisy.

Examples:

- remove extra spines,
- reduce gridline contrast,
- suppress redundant legends,
- limit tick density,
- avoid marker overload on dense line charts,
- align titles consistently,
- standardize figure sizes.

Use `sns.despine()` or equivalent spine control when helpful.

---

## Python chart-type guidance

## Polished bar charts in Python

Rules:

- order categories intentionally,
- avoid too many categories in one panel,
- use horizontal bars for long labels,
- start at zero when using bars,
- prefer dot plots when area is not needed.

Example:

```python
fig, ax = plt.subplots(figsize=(8, 5), layout="constrained")

ordered = df.sort_values("value", ascending=True)
sns.barplot(data=ordered, x="value", y="category", color="#356AE6", ax=ax)

ax.set_title("Category A leads on the primary metric", loc="left", pad=10)
ax.set_xlabel("Value")
ax.set_ylabel("")
```

---

## Polished line charts in Python

Rules:

- highlight one or two focal series,
- subdue contextual series,
- reduce marker use on dense data,
- handle dates deliberately,
- place legend where it does not compete with the data,
- direct-label endpoints when practical.

---

## Polished scatter plots in Python

Rules:

- use alpha for dense points,
- avoid giant markers,
- use trend lines cautiously,
- label only salient observations,
- choose aspect ratio based on the relationship being examined.

---

## Polished heatmaps in Python

Rules:

- use them only when a matrix is truly the point,
- order rows/columns meaningfully,
- use a perceptually sensible scale,
- label sparingly,
- avoid over-saturated colors,
- make sure the colorbar is clear and titled.

---

## When Python is the better choice than R

Python is often the better primary choice when:

- the chart is part of an application or dashboard,
- interactivity is required,
- the work is embedded in a Python analysis or ML pipeline,
- the consumer expects browser-native delivery,
- the team already standardizes on Python tooling.

For static editorial charts, however, Python usually needs more deliberate style management to match the elegance that R users often get more easily from `ggplot2` workflows.

---

## Recommended Python workflow for agents

1. Define the chart’s claim.
2. Choose `seaborn/matplotlib`, `Altair`, or `Plotly` based on deliverable type.
3. Apply project-wide style defaults before building the chart.
4. Create the minimal chart.
5. Refine scales, labels, title, and tick formatting.
6. Reduce clutter.
7. Add one layer of meaningful annotation if useful.
8. Check layout overlap and final size.
9. Export in the target format.
10. Reuse style settings across figures.

---

## Python “do” and “don’t” list

### Do

- use `seaborn` + `matplotlib` as the default static stack,
- use `Altair` when declarative encodings improve clarity,
- use `Plotly` only when interaction adds value,
- standardize style globally,
- export intentionally,
- manage layout explicitly,
- choose perceptually sensible colormaps.

### Don’t

- depend on raw matplotlib defaults for polished external deliverables,
- add interactivity without purpose,
- overload legends and labels,
- use rainbow scales for quantitative data,
- accept overlapping layout,
- apply manual per-chart cosmetics instead of a style system.

---

# Part IV — R vs Python: Which Produces the Most Polished Results?

## Static publication-quality graphics

### Slight edge: R

R has a structural advantage for many static charts because `ggplot2` and its companion ecosystem make consistency, composition, and refinement unusually ergonomic.

If the task is:

- a report figure,
- a scientific panel,
- an editorial chart,
- a polished executive slide chart,

then **R is often the fastest route to elegance**.

---

## General analytical charting in an existing Python workflow

### Edge: Python

If the analysis pipeline already lives in Python, Python may be the better overall choice because the cost of context-switching matters.

In that case:

- use seaborn/matplotlib for polished static output,
- define a strong style layer,
- and treat layout/export as first-class finishing steps.

---

## Interactive delivery

### Edge: Python

If the deliverable is interactive for end users, Python has the stronger default story through Plotly and its surrounding ecosystem.

---

## Declarative analytical chart specifications

### Balanced, with a slight Python edge via Altair for some workflows

`ggplot2` remains a superb grammar-based system. But Altair’s encoding-first design can be especially clean when:

- charts are tabular and analytical,
- specification clarity matters,
- interactive exploration is useful,
- and Vega-Lite-based output fits the delivery environment.

---

## Final practical recommendation

### Choose R when

- the priority is polished static figures,
- the work is report/editorial/scientific in nature,
- multi-panel composition matters,
- visual consistency across many charts is essential.

### Choose Python when

- the work is already in a Python pipeline,
- interactive delivery matters,
- charts are embedded in applications,
- or Altair/Plotly better matches the output environment.

### If forced to pick one default

- For **best static chart polish**: pick **R**.
- For **best all-around ecosystem flexibility**: pick **Python**.

---

# Part V — A High-Polish Checklist for Agents

## Before plotting

- What is the single takeaway?
- Who is the audience?
- What medium will the chart appear in?
- What decision should the chart support?
- Is there a simpler chart form?

## During plotting

- Is the chosen encoding the clearest one?
- Are categories ordered intentionally?
- Are scales honest and interpretable?
- Are numbers formatted humanely?
- Is color semantic rather than decorative?
- Is the title informative?
- Can the legend be removed or replaced with direct labels?
- Is clutter minimized?
- Does the visual hierarchy point to the main message?

## Before exporting

- Is the chart readable at final size?
- Are there overlaps, clipping, or crowded labels?
- Does the chart still work in grayscale?
- Does it work for color-vision-deficient viewers?
- Is the export format right for the medium?
- Are fonts stable on the rendering machine?
- Is the filename deterministic and meaningful?

---

# Part VI — Recommended Defaults Agents Should Follow

## If the agent is working in R

Default to:

- `ggplot2`
- `scales`
- `patchwork`
- `ragg` for PNG
- `svglite` for SVG
- `viridis` or `colorspace`
- reusable `theme_*()` wrappers

Presume that polish comes from:

- careful theme design,
- scale formatting,
- consistent typography,
- restrained color,
- and clean export.

## If the agent is working in Python

Default to:

- `seaborn` + `matplotlib` for static charts,
- `Altair` for declarative analytical charts,
- `Plotly` only when interactivity is needed,
- a global theme/rcParams system,
- constrained layout,
- humane formatters,
- vector export when appropriate.

Presume that polish comes from:

- a style system first,
- chart simplification,
- layout discipline,
- and explicit export settings.

---

# Part VII — Example Agent Instructions

Use the following as operational guidance.

## Agent instruction block

```text
When producing data visualizations, optimize first for truthful communication, second for readability, and third for aesthetic polish.

Choose the simplest chart form that supports the main claim.

For R, default to ggplot2 + scales + patchwork, export raster figures with ragg and vector figures with svglite, and apply a reusable custom theme.

For Python, default to seaborn/matplotlib for static charts, Altair for declarative analytical charts, and Plotly only when interactivity is part of the deliverable. Apply a global style system instead of per-chart ad hoc tweaks.

Always:
- write informative takeaway titles,
- format numbers and dates humanely,
- use restrained and semantically correct color,
- minimize clutter,
- standardize typography and spacing,
- design for the final medium,
- and export at deliberate dimensions and resolution.

Avoid 3D charts, rainbow scales for quantitative data, unnecessary legends, random category ordering, and decorative styling that does not improve comprehension.
```

---

# Part VIII — Sources and Current Documentation Consulted

This report is grounded primarily in official package documentation and primary project sources.

## R ecosystem

- ggplot2 documentation and reference index: https://ggplot2.tidyverse.org/
- ggplot2 themes reference: https://ggplot2.tidyverse.org/reference/theme.html
- ggplot2 viridis scales reference: https://ggplot2.tidyverse.org/reference/scale_viridis.html
- ggplot2 aesthetic specifications: https://ggplot2.tidyverse.org/articles/ggplot2-specs.html
- patchwork site and guides: https://patchwork.data-imaginist.com/
- scales documentation: https://scales.r-lib.org/
- ragg documentation: https://ragg.r-lib.org/
- svglite documentation: https://svglite.r-lib.org/
- systemfonts documentation: https://systemfonts.r-lib.org/
- colorspace documentation: https://colorspace.r-forge.r-project.org/
- viridis documentation: https://sjmgarnier.github.io/viridis/
- Quarto figure documentation: https://quarto.org/docs/authoring/figures.html

## Python ecosystem

- Matplotlib customization and rcParams: https://matplotlib.org/stable/users/explain/customizing.html
- Matplotlib constrained layout guide: https://matplotlib.org/stable/users/explain/axes/constrainedlayout_guide.html
- Matplotlib savefig reference: https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.savefig.html
- Matplotlib colormap guidance: https://matplotlib.org/stable/users/explain/colors/colormaps.html
- seaborn documentation: https://seaborn.pydata.org/
- seaborn set_theme reference: https://seaborn.pydata.org/generated/seaborn.set_theme.html
- seaborn move_legend reference: https://seaborn.pydata.org/generated/seaborn.move_legend.html
- seaborn objects interface: https://seaborn.pydata.org/tutorial/objects_interface.html
- Altair documentation: https://altair-viz.github.io/user_guide/
- Altair customization and themes: https://altair-viz.github.io/user_guide/customization.html
- Altair encodings: https://altair-viz.github.io/user_guide/encodings/index.html
- Plotly templates documentation: https://plotly.com/python/templates/
- Plotly static image export: https://plotly.com/python/static-image-export/

---

# Bottom Line

If the goal is **the most polished static data visualization workflow**, choose:

- **R** for the easiest path to elegant, publication-grade, consistent figures.
- **Python** for the best integration with broader analytical and interactive systems, provided you enforce a disciplined style and export workflow.

In both ecosystems, the best-looking charts come from the same habits:

- clear message,
- correct chart choice,
- restrained styling,
- excellent formatting,
- deliberate color,
- thoughtful annotation,
- and professional export.
