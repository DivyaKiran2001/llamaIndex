**🔹 1. Routers in LlamaIndex**

**👉 What it is:**
A router decides which retriever (or multiple retrievers) should handle a given query.

Implemented by RouterRetriever

Works with a selector (an LLM or rules engine) that looks at the query + metadata of retrievers, and then decides:

Should this go to Vector Retriever?

Should it go to Knowledge Graph Retriever?

Or maybe Summary Retriever?

**🔹 2. Node Postprocessors in LlamaIndex**

**👉 What it is:**
A node postprocessor runs after retrieval, on the set of retrieved nodes, to refine, filter, or rerank them before sending them to the response synthesizer.

Think of them like “editors” that clean up the retrieved context.

They take retrieved nodes → process them → return better nodes.

**✅ Common Postprocessors:**

SimilarityPostprocessor – filter out nodes below a similarity threshold.

LLMRerank – ask an LLM to rerank nodes by relevance.

KeywordNodePostprocessor – filter nodes that don’t contain specific keywords.

TimeWeightedPostprocessor – prefer recent documents.
