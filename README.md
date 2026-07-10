# BOQ Extraction Benchmark: Fine-Tuning vs. Frontier Models

## Problem Statement

Construction tender documents in India are a pain to work with programmatically — Bills of Quantities come as PDFs with merged table cells, inconsistent unit notation (cu.m vs Cum vs m³), and item descriptions that run straight into item codes with no clean delimiter between them. Anyone who's actually opened one of these knows manual extraction doesn't scale past a handful of documents, and yet a lot of construction and infra firms still process them by hand or with brittle regex scripts that break the moment a table layout changes. This project asks a narrow, practical question: given a real BOQ table, can a small model you can run locally (1-3B parameters, fine-tuned with LoRA) match a frontier model like GPT-4o-mini or Gemini Flash on structured extraction — and if so, at what fraction of the cost? I built a labeled dataset of roughly 100-150 rows pulled from real government tender PDFs (CPWD, state PWD e-procurement portals), ran zero-shot and few-shot baselines on the small model *before* touching it, then fine-tuned it and compared every approach on field-level accuracy, JSON validity rate, latency, and cost per 1000 documents. My background is in civil engineering, not computer science, so part of the motivation here was personal too — I wanted to see whether a model trained on a few hundred examples could actually pick up on the rate/unit/quantity relationships in a BOQ the way I do when I skim one myself.

## Project Structure

\`\`\`
data/raw_pdfs/         - Source tender PDFs (not committed, see .gitignore)
data/ground_truth/     - Manually labeled JSON extraction pairs
data/processed/        - Cleaned/formatted training data for fine-tuning
notebooks/             - Kaggle/Colab notebooks (data prep, training, eval)
src/                   - Reusable scripts (extraction, eval metrics, etc.)
results/               - CSVs, charts, final comparison tables
\`\`\`

## Status

🚧 In progress — currently in Phase 1 (data sourcing).

## Method (short version)

1. Source ~150-300 pages of real Indian tender/BOQ PDFs.
2. Manually label a subset into clean JSON (bootstrapped using GPT-4o-mini/Gemini for a first pass, then hand-corrected).
3. Benchmark zero-shot and few-shot performance of frontier models and a small open model, before any fine-tuning.
4. Fine-tune the small model (Qwen2.5-1.5B, LoRA via Unsloth) on the labeled training split.
5. Compare all approaches on the same held-out eval set: field-level accuracy, JSON validity, latency, cost per 1000 docs.

## Results

_(To be filled in — see \`results/final_comparison.csv\` and the accuracy-vs-cost chart once evaluation is complete.)_

## License

MIT
