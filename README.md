# Analysis Serie A — 2023/2024

## Project summary
This repository contains a Jupyter Notebook (analysis-serie-a-dataset-season-2023-2024.ipynb) that performs an exploratory data analysis (EDA) of the Serie A 2023/2024 match dataset. The notebook answers questions such as:

- Which team finished top (champion) in the dataset
- Teams with the most wins at home / away
- Teams with the highest average goals per match
- Goal distribution by first half / second half
- Matchday-level trends (total goals per matchday)
- Goal differences and standings (points, goals for / against)

The notebook is authored to run in a Kaggle environment and reads the Serie A CSV from a Kaggle input path.

## Files
- analysis-serie-a-dataset-season-2023-2024.ipynb — main notebook containing the full analysis.

## Dataset
Source (notebook): https://www.kaggle.com/api/v1/datasets/download/hamdankhan212/europe-top-leagues-2023-24-matches-football

Expected file used by the notebook:
- /kaggle/input/europe-top-leagues-2023-24-matches-football/serie_A.csv

Primary columns used by the notebook:
- date — match date/time (string in the CSV)
- matchday — integer (1..38)
- home_team, away_team — team names (string)
- home_score_full_time, away_score_full_time — full-time goals (int)
- home_score_half_time, away_score_half_time — half-time goals (int)
- goal_diff — goal difference (int)
- winner — winner team name or "DRAW"
- defeat — defeated team name or "DRAW"
- ref — referee name

Dataset size observed in the notebook: 380 rows (full season of 20 teams × 38 matchdays), 12 columns, no missing values reported.

## What the notebook does (high-level)
1. Imports: pandas, numpy, matplotlib, seaborn (seaborn style set to "darkgrid").
2. Loads the CSV and displays the first rows.
3. Basic inspection with `serieA_df.info()` to check dtypes and missing values.
4. Computes match result counts split by home/away (wins, draws, defeats).
5. Builds `match_results` DataFrame containing per-team home/away wins, draws, losses and points-by-venue.
6. Builds `goal_details` DataFrame summarizing goals scored and conceded by team, split by first/second half and home/away.
7. Builds `clasement` DataFrame (standings) showing Played, win, draw, lose, goals for, goals conceded, goal difference, and points.
8. Notebook cells include papermill metadata indicating the notebook was executed (likely in Kaggle).

## Key DataFrames & column definitions
- `serieA_df` — raw match-level DataFrame.

- `match_results` — columns: Team, Win_at_home, Win_at_away, Draw_at_home, Draw_at_away, Lose_at_home, Lose_at_away, Point_earned_at_home, Point_earned_at_away.

- `goal_details` — columns: Team name, Home score, Home score (first half), Home score (second half), Away score, Away score (first half), Away score (second half), Home conceded (and halves), Away conceded (and halves).

- `clasement` — columns: Team, Played, win, draw, lose, Goal_in, Goal_concedeed, Goal_difference, Point.

## Reproducing / running the notebook locally
1. Clone the repository:
   - `git clone https://github.com/zakkyyy-ar/DataAnalysisProjects.git`

2. Install dependencies (preferably in a virtual environment):
   - `pip install pandas numpy matplotlib seaborn jupyterlab`

   Optionally for programmatic execution:
   - `pip install papermill`

3. Download the Kaggle dataset and place `serie_A.csv` locally or point the notebook to the dataset path.

4. Update the CSV path in the notebook (if running locally). Example edit near the top:
```python
DATA_PATH = "data/serie_A.csv"
serieA_df = pd.read_csv(DATA_PATH)
serieA_df['date'] = pd.to_datetime(serieA_df['date'])
```

5. Run the notebook using Jupyter or papermill:
   - `jupyter lab`
   - or non-interactively: `papermill analysis-serie-a-dataset-season-2023-2024.ipynb output.ipynb`

Notes:
- The notebook expects the CSV path used in the Kaggle environment by default. Update the path before running offline.
- Converting `date` to datetime is recommended for time series analysis: `pd.to_datetime(serieA_df['date'])`.

## Suggested visualizations (not exhaustive)
- League table bar chart (points per team, sorted).
- Goals per matchday time series (total goals per matchday).
- Home vs away goals comparison (grouped bar chart).
- First-half vs second-half goals comparison (stacked bars or ratios).
- Cumulative points progression per team across matchdays.

## Potential issues & improvements
- Date parsing: convert `date` column to datetime for better time-based analysis.
- Normalize `winner` and `defeat` columns (trim, consistent case) before comparisons.
- Verify alignment when aggregating conceded goals (grouping on opponent columns) as a sanity check.
- When computing final standings, sort by points and use goal difference as a tiebreaker.
- Add a `requirements.txt` (or `environment.yml`) and a short `README` (this file) for reproducibility.
- Optionally save core DataFrames to CSV (e.g. `match_results.csv`, `goal_details.csv`, `clasement.csv`) for downstream work.

## Example snippet to load the dataset (configurable path)
```python
import pandas as pd
DATA_PATH = "data/serie_A.csv"  # update as needed
serieA_df = pd.read_csv(DATA_PATH)
serieA_df['date'] = pd.to_datetime(serieA_df['date'])
```

## Recommended next steps
- Add this README.md to the repository root (created by this action).
- Add `requirements.txt` or `environment.yml`.
- Optionally: save the main result DataFrames to CSV and add plotting cells (if absent).

## License & contact
- No license specified in the repository. If you want a license added (MIT, Apache-2.0, etc.), I can generate a LICENSE file.

---

This README was generated from analysis-serie-a-dataset-season-2023-2024.ipynb (commit OID: 8c5b68ffdeed3567c2981a90fb620dfc506b6a27).
