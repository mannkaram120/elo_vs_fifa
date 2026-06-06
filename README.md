# FIFA Rankings vs ELO Ratings: Predictive Validity in World Cup Knockout Stages (1994–2022)

**Replication package for:**
> Singh, K. (2026). FIFA Rankings vs ELO Ratings: Predictive Validity in World Cup Knockout Stages (1994–2022). Independent Researcher, New Delhi, India.

📄 **Preprint:** [SSRN — link to be updated]  
📊 **Status:** Under review

---

## Abstract

Football's most consequential matches — World Cup knockout encounters — are seeded and drawn using FIFA World Rankings. Yet a rival system, ELO ratings, has long been considered theoretically superior. This study asks a direct question: which system actually predicts knockout outcomes better, and did FIFA's 2018 decision to adopt an ELO-based formula close the gap?

We analysed 115 knockout matches across eight World Cups from 1994 to 2022, fitting separate logistic regression models for each rating system and evaluating them across six metrics: prediction accuracy, discrimination (AUC-ROC), calibration (Brier score), goal difference explained (OLS R²), out-of-sample cross-validation, and controlled regression (McFadden's pseudo-R²). ELO outperformed FIFA World Rankings on every single measure.

---

## Key Results

| Metric | ELO | FIFA | ELO Advantage |
|--------|-----|------|---------------|
| Accuracy (in-sample) | 73.9% | 68.7% | +5.2 pp |
| AUC-ROC | 0.775 | 0.695 | +0.080 |
| Brier score (↓ better) | 0.189 | 0.220 | −0.031 |
| Goal difference R² | 0.198 | 0.154 | +0.044 |
| CV accuracy (out-of-sample) | 73.2% | 68.9% | +4.3 pp |
| Pseudo-R² (controlled) | 0.180 | 0.119 | +0.061 |

ELO outperformed FIFA in **89.8% of 10,000 bootstrap resamples.**

---

## Repository Structure

```
fifa-vs-elo/
│
├── README.md                                  ← This file
│
├── paper/
│   ├── Singh_2026_FIFA_vs_ELO.pdf            ← Compiled paper PDF
│   ├── FIFA_vs_ELO_Research_Paper.tex        ← LaTeX source
│   └── references.bib                         ← Bibliography
│
├── data/
│   ├── README.md                              ← Data sources and variable descriptions
│   ├── WC_Knockout_Complete_Dataset.xlsx      ← Master dataset: 128 matches, 49 variables
│   ├── fifa_ranking_2023-07-20.csv            ← Raw FIFA rankings (real snapshot dates)
│   ├── matches.csv                            ← Raw match results (Badrnezhad 2024)
│   ├── squads.csv                             ← Squad data (Fjelstul 2023)
│   └── world_cup_last_50_years.csv            ← Supplementary match data
│
├── elo_validation_pages/                      ← Saved eloratings.net pages (audit trail)
│   ├── 1994.mht
│   ├── 1998.mht
│   ├── 2000.mht
│   ├── 2002.mht
│   ├── 2006.mht
│   ├── 2010.mht
│   ├── 2014.mht
│   ├── 2018.mht
│   └── 2022.mht
│
├── code/
│   ├── 01_data_cleaning.py                    ← Merges raw sources into analysis dataset
│   ├── 02_logistic_regression.py              ← Main models, AUC-ROC, Brier score
│   ├── 03_mcnemar_bootstrap.py                ← McNemar test + 10,000 bootstrap resamples
│   ├── 04_cross_validation.py                 ← Leave-one-tournament-out CV
│   ├── 05_robustness_checks.py                ← Staleness, 1994 exclusion, points vs rank
│   └── 06_figures.py                          ← Reproduces all figures in paper
│
├── outputs/
│   ├── figures/                               ← All figures as PNG and PDF
│   └── tables/                                ← All tables as CSV
│
└── requirements.txt                           ← Python dependencies
```

---

## Dataset Note

The master dataset (`WC_Knockout_Complete_Dataset.xlsx`) contains all 128 knockout matches with 49 variables including computed fields, squad data, stadium information, era labels, and an `In Analysis (115)` flag identifying the 115 matches used in the final analysis. The 13 excluded matches are retained with the flag set to 0 for full transparency. Reasons for exclusion are documented in `code/01_data_cleaning.py`.

---

## How to Reproduce

### 1. Clone the repository

```bash
git clone https://github.com/[your-username]/fifa-vs-elo.git
cd fifa-vs-elo
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the analysis in order

```bash
python code/01_data_cleaning.py
python code/02_logistic_regression.py
python code/03_mcnemar_bootstrap.py
python code/04_cross_validation.py
python code/05_robustness_checks.py
python code/06_figures.py
```

All outputs will be saved to the `outputs/` directory.

> **Note:** This project was developed in Jupyter Notebook. Each `.py` file corresponds to a notebook. Jupyter versions are available in the `code/notebooks/` folder.

### 4. Recompile the paper from LaTeX source

```bash
cd paper/
pdflatex FIFA_vs_ELO_Research_Paper.tex
bibtex FIFA_vs_ELO_Research_Paper
pdflatex FIFA_vs_ELO_Research_Paper.tex
pdflatex FIFA_vs_ELO_Research_Paper.tex
```

> LaTeX requires multiple passes to resolve all cross-references and bibliography entries.

### Reproducibility note

The bootstrap analysis uses a fixed random seed (`seed = 42`) with `B = 10,000` resamples. All results in the paper are exactly reproducible with this seed.

---

## Data Sources

| Dataset | Source | Citation | URL |
|---------|--------|----------|-----|
| Match results | Kaggle | Badrnezhad (2024) | https://www.kaggle.com/datasets/hosseinbadrnezhad/fifa-world-cup-matches-19742022-dataset-etl |
| ELO ratings | eloratings.net | eloratings.net (2024) | https://www.eloratings.net |
| FIFA rankings & snapshot dates | Kaggle | Alex (2024) | https://www.kaggle.com/datasets/cashncarry/fifaworldranking |
| Squad data | GitHub | Fjelstul (2023) | https://github.com/jfjelstul/worldcup |

ELO ratings were validated match-by-match against saved source pages from eloratings.net (see `elo_validation_pages/`).

---

## Citation

If you use this replication package, please cite:

```
Singh, K. (2026). FIFA Rankings vs ELO Ratings: Predictive Validity in 
World Cup Knockout Stages (1994–2022). Independent Researcher, New Delhi, India.
SSRN preprint: [link to be updated]
```

---

## Contact

Karamjeet Singh  
Independent Researcher, New Delhi, India  
[LinkedIn — Karamjeet Singh](https://www.linkedin.com/in/karamjeet-singh12/)

