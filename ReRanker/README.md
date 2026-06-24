### Reranker

```
PDF (arXiv paper)
      │  PyPDFLoader → 16 page chunks (Documents)
      ▼
┌─────────────── RETRIEVAL (hybrid) ───────────────┐
│  BM25Retriever (sparse, keyword)   weight 0.2    │
│  LanceDB + MiniLM embeddings (dense) weight 0.8  │
│            └──► EnsembleRetriever (fusion)        │
└──────────────────────────────────────────────────┘
      │  wide pool (k=8)
      ▼
┌─────────────── RERANK (2nd stage) ───────────────┐
│  Cross-encoder  |  ColBERT  |  LLM (RankGPT)      │
│            keep top-3                              │
└──────────────────────────────────────────────────┘
      │  best contexts
      ▼
   ChatGroq LLM  → answer grounded in context
      │
      ▼
   RAGAS evaluation (context_precision/recall, faithfulness, answer_relevancy)
   ```
