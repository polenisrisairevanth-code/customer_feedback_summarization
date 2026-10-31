# Customer Feedback Summarization (RAG + Gemini)

A small retrieval-augmented generation (RAG) pipeline that retrieves relevant customer reviews using FAISS and generates summaries using Google Gemini via the `google.generativeai` client.

## Repository structure
- [app.py](app.py)
- [`rag_pipeline.py`](rag_pipeline.py) — core retrieval & summarization (see [`rag_pipeline.retrieve`](rag_pipeline.py) and [`rag_pipeline.gemini_summary`](rag_pipeline.py))
- [requirements.txt](requirements.txt)
- [data/](data/)
  - [data/embeddings.npy](data/embeddings.npy)
  - [data/reviews.index](data/reviews.index)
- [.github/](.github/)
- [appmod/](appmod/)
- [appcat/](appcat/)
- [__pycache__/](__pycache__/)

## Quickstart

1. Create a Python venv and install deps:
```sh
pip install -r requirements.txt
```

2. Set your Google Generative AI API key (recommended):
```sh
export GENAI_API_KEY="YOUR_API_KEY"
# or on Windows:
# set GENAI_API_KEY=YOUR_API_KEY
```
> Note: The pipeline currently calls `genai.configure(...)` in [`rag_pipeline.py`](rag_pipeline.py). Replace hardcoded keys with environment config.

3. Run the app :
```sh
streamlit run app.py
```

## How it works (high level)
- Embeddings are loaded from [data/embeddings.npy](data/embeddings.npy) and the FAISS index from [data/reviews.index](data/reviews.index).
- Query embedding + FAISS nearest-neighbor search -> retrieved reviews.
  - See [`rag_pipeline.retrieve`](rag_pipeline.py).
- Retrieved reviews are used as context for Gemini to generate a concise summary and recommendations.
  - See [`rag_pipeline.gemini_summary`](rag_pipeline.py).

## Relevant symbols
- [`rag_pipeline.retrieve`](rag_pipeline.py)
- [`rag_pipeline.gemini_summary`](rag_pipeline.py)
- Files: [app.py](app.py), [rag_pipeline.py](rag_pipeline.py), [requirements.txt](requirements.txt), [data/embeddings.npy](data/embeddings.npy), [data/reviews.index](data/reviews.index)

## Individual Contribution — P. Sri Sai Revanth

My primary contributions to the project focused on data preprocessing, semantic representation and the retrieval component of the Retrieval-Augmented Generation (RAG) pipeline.

- **Data Preprocessing:** Contributed to cleaning, preparing and structuring customer review datasets for downstream processing.
- **Semantic Embeddings:** Worked with the `all-mpnet-base-v2` model to generate dense semantic embeddings of customer reviews.
- **Vector Indexing and Retrieval:** Contributed to integrating FAISS for vector indexing and implementing similarity-based retrieval to identify relevant customer reviews in response to user queries.
- **RAG Pipeline Integration:** Contributed to connecting the retrieved review context with the Google Gemini summarisation workflow, enabling the generation of query-specific, evidence-grounded summaries and recommendations.

These contributions supported the retrieval and contextualisation stages of the project, forming an important part of the overall customer-feedback summarisation workflow.

## Notes
- Ensure your `reviews_df.pkl` (used by `rag_pipeline.py`) is present in `data/` if you regenerate or re-run the pipeline.
- Secure your API keys; avoid committing them to the repo.
