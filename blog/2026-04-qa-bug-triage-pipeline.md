# QA Bug Triage Pipeline: From App Reviews to Searchable Bug Reports

A simple Python project that turns messy user reviews into structured QA bug reports using an LLM and RAG.

## Links

- GitHub Repository: https://github.com/aiqualitylab/qa-bug-triage
- Hugging Face Demo: https://huggingface.co/spaces/aiqualitylab/qa-bug-triage

---

## Why this project

Product teams get lots of feedback, but most of it is noisy and unstructured. This project helps QA teams convert that feedback into consistent bug records that are easy to search and summarize.

---

## What it does

- Collects reviews from Google Play
- Routes review text (bug report vs non-bug)
- Generates structured JSON bug reports with an LLM
- Stores bugs in ChromaDB for semantic retrieval
- Adds BM25 keyword matching for hybrid search
- Produces short AI summaries for triage
- Lets you clear the stored bugs from the UI

---

## Architecture

Google Play Reviews -> Query Router -> Triage (JSON bug report) -> ChromaDB (vector + BM25) -> AI Summary

---

## Quick start

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python app.py
```

Then open the local Gradio URL.

---

## API key

This app uses BYOK (Bring Your Own Key):

- Paste your OpenAI API key in the UI
- The key is masked
- Do not commit keys to source control

---

## Main files

- app.py: Gradio app flows
- collect.py: review collection
- triage.py: routing and structured triage logic
- rag.py: storage and hybrid retrieval
- eval/eval.py: evaluation script

---

## Evaluation sample

- Answer Relevancy: 0.868
- Faithfulness: 0.292
- Context Precision: 0.020

---

## Cost target

For a short demo session, the expected usage is typically under $0.50.

Tips:

- Keep review count low (5 to 10)
- Avoid repeated large collection runs
- Use short test inputs when validating triage

---

## Tech stack

- Python
- Gradio
- OpenAI GPT-4o
- ChromaDB
- rank-bm25
- RAGAS
- google-play-scraper

---

This project is useful for QA teams that want a lightweight bug triage assistant with searchable bug intelligence and fast summaries.
