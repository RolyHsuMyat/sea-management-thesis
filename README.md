# Management practices and SME performance in Southeast Asia

Code for an M.A. thesis in Economics (Thammasat University). It asks whether SMEs with more structured management practices sell more than similar firms, and whether that differs by owner gender, credit constraints and firm size.


## What is in this repository

| File | What it is |
| --- | --- |
| `Q7_regressions.ipynb` | The regression notebook. It reads the clean dataset and runs every regression |
| `README.md` | This page |
| `.gitignore` | Keeps data files out of the repository |

## Research questions

| | Question |
| --- | --- |
| RQ1 | Do firms with more structured management practices sell more than similar firms? |
| RQ2 | Does the payoff of management differ for female-owned firms? |
| RQ3 | Does it differ for firms facing credit constraints? |
| RQ4 | Do credit constraints change the payoff differently for female- and male-owned firms? |
| Extensions | Each practice on its own, SMEs vs large firms, Indonesia + Malaysia vs the other surveys, survey weights, and formal training |

## Data

The notebook needs one file, `sea_clean_firms.csv`. It has one row per firm (10,214 firms, 60 columns) and is built from the World Bank Enterprise Surveys: 12 surveys with the management module, from 10 Southeast Asian countries, 2018 to 2025.

**The data are not in this repository.** The Enterprise Surveys come with terms of use, so I share the clean file privately. The raw surveys are free to download after registering at <https://www.enterprisesurveys.org>. If you want the code that builds the clean file from the raw surveys, please ask me.

Data source: Enterprise Surveys (http://www.enterprisesurveys.org), The World Bank.

## How to run

1. Open `Q7_regressions.ipynb` in Google Colab (**File → Open notebook → GitHub**, then paste this repository's link).
2. Choose **Runtime → Run all**.
3. When the **Upload** button appears, choose `sea_clean_firms.csv` from your computer.
4. Wait a few minutes. The bootstrap takes most of the time.

These files are saved in your Google Drive (`wbes_out/sea_data/q7/`), or in the Colab session if Drive is not connected:

- `q7_results_simple.html`: the main results in plain words
- `q7_supervisor_regressions.html`: all the tables
- `q7_regression_tables.html` and `q7_regression_tables.tex`: the regression tables in journal format (stargazer), for reading and for LaTeX

## What the notebook does

| Part | What it estimates |
| --- | --- |
| 1 | Main results under two size definitions (national SME ceilings, and the World Bank's 100+ employees): the management score, each practice, and the gender and credit questions |
| 2 | The same results with survey weights (rescaled within each survey, and rescaled and capped) |
| 3 | Indonesia + Malaysia against the other surveys, for all SMEs and for SMEs with 20 or more employees |
| 4 | SMEs against large firms |
| 5 | One chart of the main result across every version |
| 6 | Formal training: its link with sales, and whether management pays off more with training |
| 7 | The main models as journal-style regression tables (stargazer), saved as HTML and LaTeX |

## Methods in short

- **Management score:** eight survey questions, each scored from 0 (least structured) to 1 (most structured) and averaged, following the US Census Management and Organizational Practices Survey. A follow-up question skipped after a "No" counts as 0.
- **Sales:** converted to US dollars at the survey year's exchange rate. Firms with sales per worker below US$1,000 or above US$1 million are left out as recording errors.
- **Model:** OLS of log sales on the management score. Firm size and the survey (country and year) are held fixed, so each firm is compared only with similar firms from the same survey.
- **P-values:** heteroskedasticity-robust standard errors, and a wild-cluster bootstrap (Webb weights, clustered by survey) for the key results, because there are only 12 surveys.

The results describe differences between similar firms. They do not show that a practice causes higher sales.

## Software

Python 3 in Google Colab, with `pandas`, `numpy`, `statsmodels`, `matplotlib`, `wildboottest` and `stargazer`.
