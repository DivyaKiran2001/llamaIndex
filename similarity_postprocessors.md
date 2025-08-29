**🔹 SimilarityPostprocessor**

The SimilarityPostprocessor is a special postprocessor that filters retrieved nodes based on their similarity score (how close the node’s embedding is to the query’s embedding).

⚙️ Parameters

similarity_cutoff → The minimum similarity score a node must have to be kept.

**Example:** if cutoff = 0.7, and a retrieved node has similarity = 0.6, it will be dropped.



