# Predicting Content Decay: A Machine Learning Approach

**Live Portfolio & Research Paper:** [https://imashwin-max.github.io/flyrank-internship/](https://imashwin-max.github.io/flyrank-internship/)

## What it does and for whom
This repository contains a Machine Learning pipeline designed for SEO and Editorial teams. It ingests historical search performance data and outputs a prioritized, ranked queue of pages that are actively decaying. Instead of relying on brittle heuristic rules (e.g., "update if older than 180 days"), this model uses a Random Forest classifier to identify non-linear decay patterns, ensuring content budgets are spent defending the most vulnerable high-traffic assets.

## Setup & Usage (Reproducibility)
A stranger can reproduce this setup in three steps:
1. Clone the repository: `git clone https://github.com/imashwin-max/flyrank-internship.git`
2. Install the dependencies: `pip install -r requirements.txt`
3. Run the capstone notebook: Open `work/notebooks/capstone_refresh_scoring.ipynb` and run all cells. It will load the bundled anonymized CSV and output the ranked queue.

## Simple Architecture Sketch
`[Raw Search Data CSV]` → `[Feature Engineering (Age, CTR, Impressions)]` → `[Random Forest Classifier (Balanced)]` → `[Probability Scoring]` → `[Ranked Action Queue CSV]`

## Eval Results (v2)
Evaluated on an honest holdout test set using **Precision@50**:
* **Baseline Human Rule:** 48%
* **ML Model (Random Forest):** 88%
*(The model successfully captures an 83% lift in top-50 accuracy over hardcoded heuristics).*

## Limitations
* **Observational, not Causal:** Identifies statistical decay based on history; does not prove rewriting will causally reverse the trend.
* **Survivor Bias:** Deleted pages are not represented in the snapshot.
* **No Semantic Text Analysis:** Relies on metadata, not actual page text.

## AI Transparency Diligence
*I built this project with Claude/Arena AI acting as my build partner. I directed the AI to structure the ML models, draft the boilerplate Python code, and write the HTML/CSS for the portfolio. I personally audited the feature leakages, validated the grouped splits, defined the business logic, and evaluated the model outputs to ensure technical accuracy and honest framing.*
