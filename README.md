#  LLM Benchmark Evaluation & Automated QA Pipeline

An end-to-end Data Science and Quality Assurance (QA) pipeline designed to evaluate Large Language Model (LLM) responses, detect behavioral biases (e.g., verbosity bias), and monitor human-annotated dataset integrity.

This repository demonstrates practical methodologies for evaluating AI model preferences and managing data quality in Reinforcement Learning from Human Feedback (RLHF) workflows.

---

##  Project Overview

When evaluating LLMs, understanding why humans prefer one response over another is critical. This project processes pairwise model evaluation datasets (LMSYS Chatbot Arena benchmark structure) to perform:

1. **Advanced Data Wrangling:** Normalization of raw text, regex filtering of structural artifacts (HTML/Markdown), and creation of custom feature metrics.
2. **Statistical Behavioral Analysis:** Measuring overall win rates, tie frequencies, and response length distributions.
3. **Verbosity Bias Diagnostics:** Visualizing how response length correlates with human preferences.
4. **Automated Data Quality Assurance (QA):** Detecting annotation conflicts, corrupted flags, and edge cases (e.g., identical responses assigned to non-tie outcomes).

---

##  Key Steps & Methodology

### Section 1: Data Wrangling & Feature Engineering
* Cleaned raw conversational text from user prompts and candidate LLM responses (`Model A` and `Model B`).
* Extracted word and character metrics (`prompt_word_count`, `resp_a_word_count`, `resp_b_word_count`).
* Consolidated multi-column binary targets into a single categorical preference variable (`winner`: Model A, Model B, or Tie).

### Section 2: Statistical Evaluation & Diagnostics
* Evaluated overall model preference distribution:
  * **Model A Win Rate:** ~34.91%
  * **Model B Win Rate:** ~34.19%
  * **Tie Rate:** ~30.90%
* Identified a clear **Verbosity Bias**, where winning models generated longer responses on average (~231 words vs. ~194 words).

### Section 3: Failure Visualizations
* Generated visual analytics (bar plots and grouped box plots) using `seaborn` and `matplotlib` to inspect output length distributions and preference thresholds.

### Section 4: Automated QA Audit
Implemented a programmatic audit script verifying **57,477 records**:
* **Conflicting Winner Flags:** 0 detected.
* **Missing/Null Prompts:** 0 detected.
* **Edge-Case Identification:** Flagged 27 instances where identical responses were assigned non-tie outcomes, isolating potential human annotator noise.

### Section 5: Automated QA Audit
Implemented a programmatic audit script verifying **57,477 records**:
* **Conflicting Winner Flags:** 0 detected.
* **Missing/Null Prompts:** 0 detected.
* **Edge-Case Identification:** Flagged 27 instances where identical responses were assigned non-tie outcomes, isolating potential human annotator noise.

### Section 6: Artifact Exports & Executive Summary
* Exported structured QA diagnostic metrics (`output/qa_diagnostic_report.csv`) for downstream pipeline integration.
* Generated a processed, feature-engineered sample dataset (`output/processed_llm_eval_sample.csv`).
* Saved high-resolution data visualization plots (`output/win_distribution_plot.png`).
* Automated the creation of an **Executive Pre-evaluation Report** (`output/executive_summary.md`) summarizing statistical win rates, verbosity bias impact, and data quality audits.
---

##  Repository Structure

llm_eval_pipeline/
│
├── notebooks/
│   └── llm_eval_pipeline.ipynb
├── output/
│   ├── qa_diagnostic_report.csv          # Automated QA audit summary report
│   ├── processed_llm_eval_sample.csv    # Feature-engineered dataset output
│   ├── model_evaluation_diagnostics.png # Combined win distribution & verbosity bias plots
│   └── executive_summary.md             # Executive pre-evaluation & diagnostic report
├── .gitignore
├── requirements.txt
└── README.md