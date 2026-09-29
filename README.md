# What Makes an NFL Offense Successful?

A two-page static website analyzing NFLverse play-by-play data from the 2020 through 2025 seasons.

## Project structure

- `index.html` — report page with overview, methodology, four headline numbers, eight findings, charts, and conclusion.
- `dashboard.html` — interactive NFL Offensive Explorer.
- `style.css` — shared site styling.
- `dashboard.js` — CSV loading, filtering, metrics, charts, tooltips, and table pagination.
- `report.js` — placeholder for report-page JavaScript if later needed.
- `data/nfl_offense_2020_2025.csv` — cleaned analytical dataset.
- `images/finding_1.png` through `images/finding_8.png` — validated report charts.

## Data source and unit of observation

Source: NFLverse play-by-play data for the 2020, 2021, 2022, 2023, 2024, and 2025 seasons.

The six raw season files contained 294,989 observations. The cleaned analytical file contains 210,719 rows. Each row represents one standard offensive pass or run with an identified offensive team.

## Cleaning decisions

The analytical dataset keeps standard `pass` and `run` plays and removes other event types such as kickoffs, punts, field goals, extra points, and other non-standard offensive events. The raw season files were preserved separately during analysis; the website uses the cleaned file.

Derived variables include:

- `home_away`: compares the offensive team with the game's home and away teams.
- `turnover`: equals 1 when the play contains an interception or lost fumble.
- `explosive_play`: equals 1 for a pass of at least 20 yards or a run of at least 10 yards.
- `play_call`: friendly Pass/Run label.
- `score_state`: Trailing, Tied, or Leading based on score differential before the play.

## Dashboard calculations

All dashboard calculations occur after the selected filters are applied.

- **Plays:** count of filtered rows.
- **EPA / Play:** mean of `epa`.
- **Success Rate:** mean of `success` × 100.
- **Yards / Play:** mean of `yards_gained`.
- **Explosive Play Rate:** mean of `explosive_play` × 100.
- **Touchdown Rate:** mean of `touchdown` × 100.
- **Turnover Rate:** mean of `turnover` × 100.

The dashboard supports filters for Season, Offensive Team, Down, and Play Type. It also supports measure and breakdown switches, four interactive charts, a reset button, and a paginated filtered data table.

## Report findings

1. NFL offenses shifted slightly toward the run from 2020 to 2025.
2. Buffalo led the NFL in EPA per play over the full sample.
3. Passing remained more efficient than rushing by EPA per play.
4. The most efficient offenses also performed especially well on third down.
5. Better field position generally improved efficiency, although the relationship was not perfectly linear.
6. Teams passed much more when trailing and ran more when protecting large leads.
7. Baltimore led the NFL in explosive-play rate.
8. NFL offenses were most efficient in the second quarter.

## Running locally

Because browsers normally block `fetch()` from local `file://` pages, run a small local web server from the project directory. For example, if Python is installed:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000/`.

## Publishing with GitHub Pages

Upload the contents of this folder to a GitHub repository. In the repository settings, enable GitHub Pages from the main branch/root directory. The report page is `index.html`, and the navigation links to `dashboard.html`.

## Reproducibility note

The report's displayed results were calculated from the same cleaned CSV used by the dashboard. Keep the dataset and code together when submitting or publishing the project so the analysis can be reproduced.
