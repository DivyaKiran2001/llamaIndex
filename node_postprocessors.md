**📌 Common Node Postprocessors in LlamaIndex**

Here are the main ones you’ll encounter:

**🔹 1. SimilarityPostprocessor**

The SimilarityPostprocessor is a special postprocessor that filters retrieved nodes based on their similarity score (how close the node’s embedding is to the query’s embedding).

⚙️ Parameters

similarity_cutoff → The minimum similarity score a node must have to be kept.

**Example:** if cutoff = 0.7, and a retrieved node has similarity = 0.6, it will be dropped.

```python
from llama_index.core.postprocessor import SimilarityPostprocessor

postprocessor = SimilarityPostprocessor(similarity_cutoff=0.7)
```

**2. LLMRerank**

Uses an LLM to re-rank retrieved nodes based on how relevant they are to the query.

Often improves quality over raw embedding similarity.

```python
from llama_index.postprocessor.llm_rerank import LLMRerank

reranker = LLMRerank(choice_batch_size=5, top_n=3)

```
**3. SentenceTransformerRerank**

Uses a Sentence Transformer model (not LLM) for semantic re-ranking.

Faster + cheaper than LLMRerank.

```python
from llama_index.postprocessor.sbert_rerank import SentenceTransformerRerank

reranker = SentenceTransformerRerank(model="cross-encoder/ms-marco-MiniLM-L-6-v2", top_n=3)

```

**4. MetadataFilters**

Filters nodes by metadata conditions.

**Example:** Only include documents from a certain author, date, or category.

```python
from llama_index.core.postprocessor import MetadataFilter

filters = MetadataFilter(
    filters={"author": "Alice"}
)
```


