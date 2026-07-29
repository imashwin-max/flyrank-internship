# AI Workflow: "Draft, Critique, Revise" Search Intelligence Brief

**Chosen Pipeline:** Draft, Critique, Revise (Weekly Search Intelligence Brief)
**Context:** As an ML/SEO intern, I need to stay updated on algorithm changes, data engineering tools, and search trends. This workflow takes raw industry articles and distills them into a highly actionable, fluff-free brief.

---

## 1. Step Diagram & Workflow Overview

**Tool Used:** Claude Project (using chained prompts in a single context window) + Custom Instructions.

**The Flow:**
`[Input: Raw Article Text]` 
  ↓ 
**Step 1: Synthesize & Extract** (Pull only factual changes, data points, and API limits)
  ↓ 
**Step 2: Draft Initial Brief** (Format into a 3-bullet executive summary)
  ↓ 
**Step 3: The "No-Fluff" Critique** (AI reviews its own draft against a strict style guide to remove marketing speak)
  ↓ 
**Step 4: Final Polish** (Applies the critique to generate the final output)
  ↓ 
`[Output: Actionable Weekly Brief]`

---

## 2. Prompts & Configuration

**System Context / Project Instructions:**
> "You are a Search Intelligence Analyst. Your goal is to extract facts, ignore marketing fluff, and write executive briefs. Use an objective, data-forward tone. Never use words like 'revolutionize', 'game-changer', or 'synergy'."

**Prompt 1 (Gather & Synthesize):**
> "Read the following article text. Extract only the hard facts: specific algorithm changes, new data limits, technical requirements, or metric shifts. List them as raw data points."

**Prompt 2 (Draft):**
> "Turn those extracted facts into a 3-bullet executive brief. 
> Format: 
> - **The Update:** [What happened]
> - **The Impact:** [How it affects search/data]
> - **The Action:** [What we need to do]"

**Prompt 3 (Critique & Revise):**
> "Review your draft. Did you include any marketing fluff or vague advice? Critique it strictly. Then, output a final revised version that is 20% shorter and entirely fact-based."

---

## 3. The Five Real Runs

### Run 1: Google Core Update
*   **Input:** 4-page article on the "March 2026 Core Update focusing on AI-generated spam."
*   **Final Output:**
    *   **The Update:** Google deployed a core update targeting high-scale, low-value AI content, heavily penalizing domains with rapid page-count bloat.
    *   **The Impact:** Sites relying on programmatic SEO without editorial review saw a 40% average visibility drop.
    *   **The Action:** Audit the `content_refresh` queue; prioritize pruning or rewriting pages with high `ai_traffic_pct` and zero recent engagement.

### Run 2: Hugging Face Parquet Support
*   **Input:** Hugging Face announcement about native Parquet viewing and DuckDB integration.
*   **Final Output:**
    *   **The Update:** Hugging Face now supports native Parquet file querying directly via DuckDB without downloading the full dataset.
    *   **The Impact:** Data processing for warehouse-scale SEO datasets drops from hours (via Pandas) to seconds (via DuckDB SQL).
    *   **The Action:** Refactor `scripts/01_prepare_features.py` to replace `pd.read_csv()` with a DuckDB `hf://` connection.

### Run 3: Search Console API Quota Changes
*   **Input:** Google Search Central blog post about new API limits.
*   **Final Output:**
    *   **The Update:** GSC API daily query quotas are reduced for standard tiers, while bulk data exports to BigQuery are now mandatory for >50k daily rows.
    *   **The Impact:** Standard daily API scripts will hit 429 errors if querying historical data recursively.
    *   **The Action:** Transition the daily pipeline to the BigQuery bulk export table; deprecate the live API connector.

### Run 4: Shift to Vector-Based Intent Matching
*   **Input:** Technical paper on Search engine shifts from lexical matching to vector embeddings.
*   **Final Output:**
    *   **The Update:** Search engines are weighting dense vector similarity heavier than exact TF-IDF keyword density for informational queries.
    *   **The Impact:** Traditional `word_count` and exact-match keyword signals are correlating less with `avg_position`.
    *   **The Action:** Update the ML baseline model; consider testing an embedding-based feature over raw character counts.

### Run 5: Chrome "AI Overviews" Expansion
*   **Input:** News about AI Overviews launching in 10 new countries.
*   **Final Output:**
    *   **The Update:** AI Overviews are active in 10 additional regions, pushing traditional "10 blue links" further down the viewport.
    *   **The Impact:** Expected drop in standard top-of-page CTR for informational queries in these regions.
    *   **The Action:** Monitor `ctr` vs `avg_position` curves in the new regions; expect the CTR cliff to steepen.

---

## 4. Time Accounting

*   **Setup Cost:** 45 minutes (Designing the 3-step prompt chain, testing it twice, and setting up the Claude Project instructions).
*   **Manual Time:** Reading a dense 4-page technical article, highlighting facts, and writing a clean summary takes ~15 minutes per article. (5 articles = 75 minutes).
*   **Workflow Time:** Copy-pasting the text and running the 3-prompt chain takes ~2 minutes per article. (5 articles = 10 minutes).
*   **Time Saved Estimate:** Saved ~65 minutes on this batch alone. The setup cost pays for itself by week 2. Estimated ongoing savings: **~1 hour per week.**

---

## 5. Failure Points & Required Human Review

*   **Failure Point 1 (Nuance Loss):** In Run 3, the AI initially failed to distinguish between the standard API and the bulk BigQuery export, conflating the two. The "Critique" prompt caught the vagueness, but human domain knowledge was needed to verify the exact quota numbers.
*   **Failure Point 2 (The "Action" hallucination):** Sometimes, the AI guesses an "Action" that doesn't fit our actual tech stack (e.g., suggesting we buy a third-party tool instead of using our internal scripts). 
*   **Human Review Required:** A human *must* verify the specific numbers/percentages extracted in Step 1, and validate that the "Action" in Step 3 actually applies to our specific codebase/business logic.
