# Tidy Tuesday Projects

Data analysis reports from the [TidyTuesday](https://github.com/rfordatascience/tidytuesday) project — a weekly social data project in R.

**[View the reports site](https://alexanderprobst.github.io/tidy_tuesday_projects/)**

## Reports

| Year | Week | Topic | Report | Source |
|------|------|-------|--------|--------|
| 2026 | 03 | Languages of Africa | [View](https://alexanderprobst.github.io/tidy_tuesday_projects/reports/2026/2026-week-03_languages-of-africa.html) | [Source](reports/2026/2026-week-03_languages-of-africa.qmd) |
| 2025 | 17 | Daily Accidents & 4/20 | [View](https://alexanderprobst.github.io/tidy_tuesday_projects/reports/2025/2025-week-17_daily-accidents.html) | [Source](reports/2025/2025-week-17_daily-accidents.qmd) |
| 2024 | 03 | NHL Players & Relative Age Effect | [View](https://alexanderprobst.github.io/tidy_tuesday_projects/reports/2024/2024-week-03_nhl-players.html) | [Source](reports/2024/2024-week-03_nhl-players.qmd) |

## Tools

- R, Quarto, tidyverse, ggplot2

## Adding a new report

1. Create a `.qmd` file in `reports/YYYY/` using the naming convention `YYYY-week-NN_topic-name.qmd`
2. Add a menu entry in `_quarto.yml` under the Reports navbar
3. Add a row to the table in `index.qmd` and this README
4. Commit and push — GitHub Actions automatically renders and deploys the site
