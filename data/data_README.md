# Data Description

This folder contains all datasets used in the analysis. Files are organised into two categories: analysis-ready datasets and raw source files.

---

## Analysis-Ready Datasets

### `wc_knockout_analysis_ready.csv` — Main analysis dataset
**115 World Cup knockout matches, 1994–2022.**
This is the file used directly in all statistical models. Produced by merging and cleaning the four raw sources below. Group stage matches are excluded. 13 matches removed where ELO or FIFA data could not be reliably matched.

| Variable | Type | Description |
|----------|------|-------------|
| `match_id` | string | Unique match identifier |
| `year` | integer | World Cup year |
| `tournament` | string | Tournament name (e.g. "Germany 2006") |
| `round` | string | Knockout round (e.g. "Round of 16", "Quarter-final") |
| `round_ordinal` | integer | Round as ordinal (1=R16, 2=QF, 3=SF, 4=Final) |
| `home_team` | string | Home-listed team (administrative label only — neutral venue) |
| `away_team` | string | Away-listed team (administrative label only — neutral venue) |
| `home_goals` | integer | Goals scored by home-listed team (FT/AET) |
| `away_goals` | integer | Goals scored by away-listed team (FT/AET) |
| `outcome` | integer | 1 = home-listed team won, 0 = away-listed team won |
| `shootout` | integer | 1 = decided by penalty shootout, 0 = not |
| `elo_home` | float | ELO rating of home-listed team at match date |
| `elo_away` | float | ELO rating of away-listed team at match date |
| `delta_elo` | float | ELO difference (home minus away; positive = home stronger) |
| `fifa_rank_home` | integer | FIFA rank of home-listed team at snapshot date |
| `fifa_rank_away` | integer | FIFA rank of away-listed team at snapshot date |
| `delta_fifa_rank` | float | FIFA rank difference (away minus home; positive = home better ranked) |
| `fifa_points_home` | float | FIFA points of home-listed team at snapshot date |
| `fifa_points_away` | float | FIFA points of away-listed team at snapshot date |
| `delta_fifa_points` | float | FIFA points difference (home minus away) |
| `rank_date` | date | Real FIFA ranking snapshot date (not a proxy estimate) |
| `days_stale` | integer | Days between FIFA snapshot date and match date |
| `post_2018` | integer | 1 = post-2018 formula tournament, 0 = pre-2018 |
| `goal_difference` | integer | Home goals minus away goals (NA for shootout matches in OLS) |

> **Note on home/away:** All matches are at neutral venues. Home/away reflects administrative draw order only and carries no competitive significance. The logistic regression is specified without an intercept for this reason.

---

### `WC_Knockout_Complete_Dataset.xlsx` — Full merged dataset (pre-cleaning)
**128 World Cup knockout matches before removal of 13 unmatched observations.**
Retained for full transparency. The 13 removed matches and reasons for removal are documented in `code/01_data_cleaning.py`.

---

## Raw Source Files

### `fifa_ranking_2023-07-20.csv` — Raw FIFA rankings
FIFA rankings with real `rank_date` values. Source: Alex (2024), Kaggle.

| Variable | Description |
|----------|-------------|
| `team` | National team name |
| `rank_date` | Actual date FIFA published this ranking (verified, not proxy) |
| `rank` | FIFA rank at that date |
| `total_points` | FIFA points at that date |

---

### `matches.csv` — Raw match results
World Cup match results 1974–2022. Source: Badrnezhad (2024), Kaggle.

---

### `squads.csv` — Squad data
World Cup squad information. Source: Fjelstul (2023), GitHub.

---

### `world_cup_last_50_years.csv` — Supplementary match data
Additional World Cup match data used in dataset construction and validation.

---

## ELO Validation Pages (`/elo_validation_pages/`)

The files `1998.mht`, `2002.mht`, `2006.mht`, `2010.mht`, `2014.mht`, `2018.mht`, `2022.mht`, `elo_2000.mht`, and `World Football Elo Ratings.mht` are saved browser pages from eloratings.net, captured at the time of data collection (April 2026).

ELO ratings were validated match-by-match against these saved pages as stated in Section 3.1 of the paper. They are retained here as an audit trail. They are not input files for the analysis code.

To view: open any `.mht` file in Microsoft Edge or Internet Explorer.

---

## Data Sources and Licences

| File | Source | Citation | Licence |
|------|--------|----------|---------|
| `matches.csv` | Kaggle | Badrnezhad (2024) | CC BY 4.0 |
| `fifa_ranking_2023-07-20.csv` | Kaggle | Alex (2024) | CC BY 4.0 |
| `squads.csv` | GitHub | Fjelstul (2023) | MIT |
| ELO ratings | eloratings.net | eloratings.net (2024) | Public, non-commercial |

---

## Missing Data Note

The raw merge produced 128 knockout matches. 13 were removed where ELO or FIFA ranking data could not be reliably matched to the correct pre-match snapshot. The final analysis dataset contains **115 matches.** All removed matches and removal reasons are logged in `code/01_data_cleaning.py`.
