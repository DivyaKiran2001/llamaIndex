**🔹 Types of Memory in LlamaIndex**

**1. ChatMemoryBuffer**

Keeps a rolling history of recent messages.

Works like a sliding window — keeps only the last N interactions.

**2. SummaryMemoryBuffer**

Instead of keeping raw history, it summarizes past interactions into a shorter form.

Useful for long conversations where token limits matter.

**3. SimpleMemory (key-value memory)**

Stores arbitrary facts as key-value pairs instead of chat history.

Good for personalization (e.g., remembering user preferences).

| Memory Type             | Stores                               | Best For                            |
| ----------------------- | ------------------------------------ | ----------------------------------- |
| **ChatMemoryBuffer**    | Recent raw messages (sliding window) | Short-term chat context             |
| **SummaryMemoryBuffer** | Summarized past interactions         | Long conversations, token-efficient |
| **SimpleMemory**        | Key-value pairs (facts/preferences)  | Personalization, static knowledge   |
