**🔹 What is a Retriever?**

A Retriever = component that takes a query → returns the most relevant nodes from an index/vector store.

**🔹 Types of Retrievers in LlamaIndex**
**1. Vector Index Retriever (Semantic Retriever)**

Default when using VectorStoreIndex.

Uses embeddings → computes similarity between query vector and document vectors.

**Returns top-k most similar nodes.**
**✅ Example:** “What is RAG?” → retrieves semantically relevant chunks even if “RAG” isn’t explicitly mentioned.

**2. Keyword Table Retriever**

Uses lexical search (keyword-based matching).

Similar to a traditional inverted index.

Good when documents are small, structured, or contain exact keywords.
**✅ Example:** Legal docs, where keyword “Section 12.3” is critical.

**3. List Retriever**

Works with ListIndex.

Retrieves nodes sequentially, like reading through a list.

Useful for Q&A where context depends on order.
**✅ Example:** Step-by-step tutorial or chronological logs.

**4. Summary Index Retriever**

Works with SummaryIndex.

Retrieves based on hierarchical summaries (tree-like structure).

Good for large docs where direct vector search might be inefficient.
**✅ Example:** Summarizing a 100-page research paper at different levels of detail.

**5. AutoMergingRetriever**

Groups smaller chunks (nodes) back into larger text blocks at retrieval time.

Helps preserve context without overwhelming the LLM with too many tiny nodes.
**✅ Example:** Retrieving full sections of a book instead of isolated sentences.

**6. Router Retriever**

Routes queries to the most appropriate retriever/index.

Useful when you have multiple indexes (e.g., PDF + SQL + API).
**✅ Example:** “Show me revenue data” → goes to SQL index,
“Summarize company policy” → goes to VectorStoreIndex.

| Retriever Type           | Method                | Best For                     |
| ------------------------ | --------------------- | ---------------------------- |
| **Vector Retriever**     | Embeddings (semantic) | General RAG, semantic Q\&A   |
| **Keyword Retriever**    | Keyword match         | Structured docs, exact terms |
| **List Retriever**       | Sequential read       | Ordered/chronological data   |
| **Summary Retriever**    | Summarization tree    | Very long documents          |  
| **AutoMergingRetriever** | Merges chunks         | Preserving larger context    |
| **Router Retriever**     | Query routing         | Multi-source systems         |
