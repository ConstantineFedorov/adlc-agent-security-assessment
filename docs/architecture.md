# Architecture

The tested workflow is conceptually:

```text
User task
   |
   v
Agent
   |
   +---------------------> LLM
   |
   +---------------------> MCP / RAG
                              |
                              v
                     untrusted external content
                              |
                              v
                         Agent context
```

The security focus is the trust boundary between trusted control instructions and untrusted content returned through prompts, RAG retrieval, or MCP tools.

The three selected experiments establish:

- a clean baseline;
- direct injection through the prompt surface;
- indirect injection through an MCP result.
