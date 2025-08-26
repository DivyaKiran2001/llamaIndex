**🔹 Embeddings in LlamaIndex**

1. You first load data → Documents.

2. Documents get split → Nodes.

3. Each Node is converted into an embedding vector (e.g., [0.12, -0.55, 0.89, ...]).

These vectors are stored in an Index (e.g., VectorStoreIndex).

**During query time:**

Your question is also converted into an embedding.

LlamaIndex finds the most similar nodes (using cosine similarity or dot product).

Relevant nodes are sent to the LLM to generate the final answer.

**🔹 What is an Index in LlamaIndex?**

An Index in LlamaIndex is a data structure that organizes your nodes + embeddings so they can be searched efficiently.

It’s like the “brain” that helps LlamaIndex store, retrieve, and match relevant information from your data.

**🔹 Types of Indexes in LlamaIndex:**

LlamaIndex offers 4 main index types (plus some hybrids).

**1. VectorStoreIndex 🧠 (most common)**

Stores embeddings of nodes in a vector store.

Enables semantic similarity search → find text chunks closest in meaning to a query.

Best for RAG (Retrieval Augmented Generation).

**✅ Use cases:**

Ask natural questions over PDFs, websites, databases.

```python
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader

docs = SimpleDirectoryReader("data/").load_data()
index = VectorStoreIndex.from_documents(docs)

query_engine = index.as_query_engine()
print(query_engine.query("Summarize the key policies"))

```
**2. ListIndex 📃**

Stores nodes in a simple linear list.

Retrieval means iterating over all nodes in order.

Good for summarization pipelines or when you want to process all text sequentially.

**✅ Use cases:**

Summarizing all meeting transcripts.

```python
from llama_index.core import ListIndex

index = ListIndex.from_documents(docs)
query_engine = index.as_query_engine()
print(query_engine.query("Give me a summary of everything"))

```
**3. TreeIndex 🌳**

Organizes nodes in a hierarchical tree.

Summaries are built at each level of the tree → you can ask for high-level or detailed summaries.

Good for structured summarization (research papers, books, reports).

**✅ Use cases:**

Summarizing a research paper (section → chapter → paper summary).

```python
from llama_index.core import TreeIndex

index = TreeIndex.from_documents(docs)
query_engine = index.as_query_engine()
print(query_engine.query("Give me a high-level summary"))
```
**4. KeywordTableIndex 🔑**

Builds a table mapping keywords → nodes.

Retrieval is based on keyword matching, not embeddings.

Faster & lighter, but less intelligent (no semantic understanding).

**✅ Use cases:**

Small datasets with well-defined keywords.

```python
from llama_index.core import KeywordTableIndex

index = KeywordTableIndex.from_documents(docs)
query_engine = index.as_query_engine()
print(query_engine.query("Show me mentions of 'compliance policy'"))

```

| **Index**             | **How it works**               | **Best For**                               | **Limitations**                |
| --------------------- | ------------------------------ | ------------------------------------------ | ------------------------------ |
| **VectorStoreIndex**  | Embeddings + similarity search | Semantic search, RAG apps                  | Needs vector DB (or in-memory) |
| **ListIndex**         | Linear list of nodes           | Summarization over all docs                | No semantic retrieval          |
| **TreeIndex**         | Hierarchical summaries         | Structured summarization (papers, reports) | Slower build, complex          |
| **KeywordTableIndex** | Keyword → Node mapping         | Keyword lookup, lightweight search         | No semantic understanding      |

