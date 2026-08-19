Title: From Magic to Methodology: My ML Internship Retrospective

Looking back at the person I was in Week 1 of the FlyRank internship, my perspective on Machine Learning was heavily skewed toward the "magic" of the algorithms. I thought the hardest part of building an ML product was tuning hyperparameters or importing the most complex deep learning library I could find. Over the last several weeks, building the Content Decay prediction engine has completely rewired how I approach AI and data science.

What changed the most was realizing that the algorithm is actually the smallest part of the job. The real engineering happens in the problem framing. When I first looked at the data, the temptation was to try and "predict Google's algorithm." The internship forced me to abandon that impossible goal and reframe it into a highly practical scoring and ranking task. I learned that an 88% Precision@50 on a Random Forest is infinitely more valuable to an editorial team than a black-box model, because it can be translated into clear, actionable reason codes (like stale_high_visibility).

I also learned the painful lesson of data leakage. During the Week 3 and Week 6 validation audits, I saw firsthand how easy it is to accidentally include target-derived features (like trend_pct) or leak client identities across a naive train/test split. Learning to use GroupShuffleSplit to simulate a genuinely unseen client was a massive "aha" moment for me. It forced me to be rigorously honest about what my model could and could not do, shifting my language from "causal proof" to "directional decision-support."

If I were to build this next, I would upgrade it from a static notebook into a true Agent. Using the Model Context Protocol (MCP), I would wire the pipeline to actively pull live data from the Google Search Console API on a cron schedule, run the Random Forest inference autonomously, and push the Top 10 recommendations directly to a Slack channel.

The three most transferable things I learned during this track are:

Honest Validation: How to design splits and hunt for feature leakage to ensure a model actually works in the real world, not just in a Jupyter notebook.
AI as a Build Partner: How to architect a system and use AI to write the boilerplate (HTML, CSS, standard Scikit-Learn pipelines) while maintaining strict human-in-the-loop control over the logic and methodology.
Translating ML to Business Value: How to take an abstract probability score and turn it into a concrete Action Playbook with limits and guardrails that non-technical stakeholders can trust.
This capstone isn't just a coding exercise; it’s a fully deployed, public piece of proof that I can build reliable, honest data systems.
