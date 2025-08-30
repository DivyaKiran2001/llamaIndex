**🔑 1. Query Engine**
**Purpose:**
One-shot question answering (Q&A).

**Flow:**

Takes a single query.

Retrieves relevant chunks.

Synthesizes a response.

No memory → Each query is treated independently.

**Best for:**

Fact lookup.

Analytical tasks.

Static queries.

**🔑 2. Chat Engine**

**Purpose:**
Conversational interaction with memory.

**Flow:**

Takes user messages in a multi-turn conversation.

Maintains context of past exchanges.

Can be stateful (remember past chat history).

**Best for:**

Assistants/agents.

Chatbots.

Multi-turn reasoning.

**Available Chat Modes in LlamaIndex**

| **Chat Mode**               | **Description**                                                                                                                                                                           |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`simple`**                | Interacts directly with the LLM **without using the index or any retrieval** — purely generative.                                                                                         |
| **`condense_question`**     | Rewrites the current chat message into a standalone question (using prior context), then queries the index.                                                                               |
| **`context`**               | Retrieves relevant context from the index for each user message, and includes that context in the prompt for response generation.                                                         |
| **`condense_plus_context`** | Combines both approaches: first condenses the question using chat context, then retrieves relevant information from the index and includes it when generating the answer.                 |
| **`react`** (deprecated)    | Uses a ReAct-style agent loop — the model thinks, optionally performs retrieval (acts), observes the result, and decides whether to query again or return the answer.                     |
| **`openai`** (deprecated)   | Similar to `react`, this mode enables an **OpenAI function-calling agent** — a specialized agent using OpenAI’s function call capabilities.                                               |
| **`best`**                  | Automatically selects the most appropriate chat mode based on your LLM and its features. Acts as an alias for `condense_plus_context`.                                  ([LlamaIndex][1]) |

[1]: https://docs.llamaindex.ai/en/stable/api_reference/chat_engines/?utm_source=chatgpt.com "LlamaIndex"

