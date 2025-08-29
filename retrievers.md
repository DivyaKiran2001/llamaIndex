**🔹 What is a Retriever?**

A Retriever = component that takes a query → returns the most relevant nodes from an index/vector store.

**🔎 What is a Retriever in LlamaIndex?**

A Retriever is responsible for fetching the most relevant nodes (chunks of documents) given a query.

It sits between the index (where documents/embeddings live) and the response synthesizer (which generates the final answer).

Retrievers decide what context the LLM sees → so they are critical for accuracy, speed, and cost.

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


**🔎 1. as_retriever()**

**What it does**

**as_retriever()** converts an Index (like VectorStoreIndex) into a Retriever.

Every index in LlamaIndex has its own default retriever type:

VectorStoreIndex → VectorIndexRetriever

**VectorIndexRetriever** :

It is a retriever class that fetches the most relevant text chunks (nodes) from a VectorStoreIndex.

```python
VectorIndexRetriever(
    index: VectorStoreIndex,
    similarity_top_k: int = 2,
    filters: Optional[MetadataFilters] = None,
    alpha: Optional[float] = None,
    vector_store_query_mode: str = "default",
)
```

**Explanation of parameters:**

**index (required)**

The VectorStoreIndex you built from documents.

Retriever will search over this index.

**similarity_top_k (default=2)**

Number of most similar nodes (text chunks) to retrieve.

Example: If k=3, it will return the top 3 most relevant chunks.

**filters (optional)**

Lets you filter retrieval by metadata.

Example: Only search inside documents where category="finance".

**alpha (optional)**

Used when blending vector similarity + keyword search (hybrid search).

Range: 0.0 → only keyword search, 1.0 → only vector search, 0.5 → equal weight.

**vector_store_query_mode (default="default")**

How to query the vector store. Options may include:

"default" → standard cosine similarity

"mmr" → Maximal Marginal Relevance (improves diversity in results)

"sparse" → for hybrid / sparse retrieval

**Similarly for SummaryIndexRetriever and KGTableRetriever**

SummaryIndex → SummaryIndexRetriever

KnowledgeGraphIndex → KGTableRetriever


This is a convenience method: you don’t need to manually import retriever classes.


**🔎 2. retrieve()**
**What it does**

**retrieve(query: str)** runs a retrieval step:

Converts your query into an embedding

Searches the index (vector similarity / graph search / summary, depending on index type)

Returns the top nodes (not final answers — just the most relevant pieces of context).

So, retrieve() = "Fetch the relevant text chunks for my query."
