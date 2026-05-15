# Champions League Format Simulation (2023/24)

A statistical simulation project comparing the **old UEFA Champions League group stage format** against the **new league phase format** introduced in 2024/25. Built with Python using Poisson regression and Monte Carlo simulation.

> **Note:** This repository covers the **old group stage format** only.
> The new league phase format was analysed separately as part of a joint university project.

## What This Project Does

The UEFA Champions League switched to a new format in 2024/25. This project asks: **does the new format actually produce fairer or more exciting outcomes than the old one?**

To answer that, the project:
1. Trains a **Poisson regression model** on real UCL match data (2017–2024) to predict goal scoring
2. Simulates the **old group stage format** (8 groups × 4 teams) using the 2023/24 participant lineup
3. Uses **Elo ratings** and home advantage as predictors for match outcomes
4. Runs **Monte Carlo simulations** over thousands of iterations to estimate qualification probabilities for each team

## Repository Structure

```
├── ChampionsLeagueOldFormat_DataSet.ipynb   # Data preparation & Poisson model training
├── ChampionsLeagueOldFormat.ipynb           # Draw simulation & Monte Carlo analysis
├── model_df.xlsx                            # Processed match dataset (output of DataSet notebook)
└── README.md
```

> **Note:** The raw CSV files (per season, 2017–2024) and the Elo source data (`elo_data_merged_2017_2024.xlsx`) are not included in this repo due to size. The processed `model_df.xlsx` is provided so the analysis notebook can be run directly without re-running the data pipeline.

## Data

- **Match results:** UCL seasons 2017/18 through 2023/24 — 750 matches total
- **Elo ratings:** Scraped from club Elo rating sources (webscraping code included but commented out for performance)
- **Teams simulated:** Full 32-team field from UCL 2023/24, with real Elo ratings and UEFA pot assignments

## Methods

| Step | Method |
|---|---|
| Goal prediction | Poisson GLM with `Elo_Diff` and `Home` as predictors |
| Draw simulation | UEFA-compliant random draw (pot rules + no same-country group clashes) |
| Tournament simulation | Monte Carlo — full group stage simulated N times per draw |
| Output | Qualification probability per team across all simulations |

**Model fit:** The Poisson regression achieved a Pseudo R² of 0.21 on 1,500 observations, with both Elo difference and home advantage being highly significant (p < 0.001).

## Tech Stack

- Python 3.11
- `pandas`, `numpy` — data processing
- `statsmodels` — Poisson GLM
- `matplotlib`, `seaborn` — visualization
- `BeautifulSoup`, `requests` — webscraping (Elo data)

## How to Run

1. Make sure `model_df.xlsx` is in the same directory as the notebooks
2. Run `ChampionsLeagueOldFormat.ipynb` directly for the simulation and results
3. To re-run data preparation from scratch, place the raw CSV files and `elo_data_merged_2017_2024.xlsx` locally and update the file paths in `ChampionsLeagueOldFormat_DataSet.ipynb`

## Author

Charbel Sakr — Data Science, TU Dortmund  
