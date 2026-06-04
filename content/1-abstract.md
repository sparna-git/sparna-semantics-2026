## Abstract

{:#abstract}

We present MCP-over-SPARQL, a Model Context Protocol server for natural-language access to knowledge graphs. The server connects an MCP-capable LLM client to a SPARQL endpoint and exposes a small set of dedicated tools for schema overview, curated examples, node-shape discovery, entity reconciliation, and SPARQL execution. This lets a user question be turned into a live query through a controlled sequence of tool calls rather than a single black-box step. By grounding query construction in SHACL and resolving named entities against the identifiers actually used in the graph, the system reduces schema guessing and returns real data from the endpoint instead of model-generated text. We demonstrate the approach on RUIM, the Uniq interoperable reference for medicines, and show how it supports controlled, schema-aware querying of domain-specific knowledge graphs.
