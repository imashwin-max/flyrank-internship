# Demo Outline & Shareable Cuts

## 1. 5-Minute Demo Outline
*(For the optional Week 8 Showcase presentation)*

*   **Minute 1: The Question & The Problem (The Hook)**
    *   Introduce the problem: Editorial teams have limited bandwidth. How do we know *which* existing page to rewrite next to stop traffic bleeding?
    *   Explain the goal: Move from a hardcoded guess ("update if older than 180 days") to a data-driven ML scoring queue.
*   **Minute 2: The Data & Methodology**
    *   Briefly mention the dataset (FlyRank 90-day trailing snapshot, anonymized).
    *   Explain the method: Formulated as a Scoring and Ranking task using a Random Forest Classifier. Target proxy: `trend_direction == 'down'`.
    *   Explain the honest split: Highlight the importance of using a `GroupShuffleSplit` (by `client_id`) or strict validation to prevent leakage.
*   **Minute 3: The Results & The Chart**
    *   Show the Feature Importance chart (`days_since_last_update` and `avg_position` drove the model).
    *   Share the core result: The ML model achieved ~88% Precision@50 on the holdout set, completely crushing the 48% baseline human rule.
*   **Minute 4: One Honest Limitation**
    *   Explain the boundary: "This model is observational, not causal. It proves a page is statistically declining, but it doesn't guarantee a rewrite will magically reverse the trend."
*   **Minute 5: The Recommendation & Action Playbook**
    *   Show the final `action_queue.csv` output.
    *   Explain the human-in-the-loop rule: The model generates the prioritized queue and assigns reason codes, but a human editor makes the final call on *how* to rewrite the page.

---

## 2. Shareable Cut 1: Short Social Post (LinkedIn/Twitter)
🚀 I just shipped my Machine Learning Capstone for the FlyRank Internship! 

I built a Content Decay prediction engine that helps SEO/Editorial teams prioritize exactly which pages to rewrite to defend their traffic. 

🧠 **Methodology:** Instead of brittle "if/else" rules, I framed this as a Scoring and Ranking task using a Random Forest classifier. This allowed me to extract feature importances (like staleness and traffic volume) to give writers actual "reason codes" for why a page was flagged. 

⚠️ **Honest Framing:** This model is observational, not causal. It proves a page is statistically declining, but it doesn't guarantee a rewrite fixes the problem—it simply acts as an intelligent triage queue.

It beat the hardcoded human baseline by a massive margin (88% vs 48% Precision@50). Check out my deployed research paper and GitHub repo here: [https://imashwin-max.github.io/flyrank-internship/](https://imashwin-max.github.io/flyrank-internship/)

---

## 3. Shareable Cut 2: Employer-Facing Summary (Resume / Cover Letter)
**Built an ML-powered Content Decay Scoring Engine** using 79M rows of anonymized search data to prioritize editorial updates. Engineered a Random Forest ranking pipeline that identified non-linear decay patterns, improving Top-50 precision from 48% (human heuristics) to 88%. Delivered the final model as an automated action queue with strict data-leakage audits and human-in-the-loop guardrails.
