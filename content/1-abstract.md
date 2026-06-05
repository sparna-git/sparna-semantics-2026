## Abstract

{:#abstract}

We present MCP-over-SPARQL, a Model Context Protocol server for natural-language access to knowledge graphs. The server connects an MCP-capable LLM client to a SPARQL endpoint and exposes a small set of dedicated tools for schema overview, curated examples, knowledge graph strcuture discovery, entity reconciliation, and SPARQL execution. This provides all the necessary primitives for an LLM client to turn a natural language question into a SPARQL query, using correct identifiers from the knowledge graph. By grounding query construction in SHACL and resolving named entities against the identifiers actually used in the graph, the system reduces schema guessing and returns real data from the endpoint instead of model-generated text. We demonstrate the approach on the the Unique Interoperability Referential of Medical Specialties from the French e-health agency, and show how it supports controlled, schema-aware querying of domain-specific knowledge graphs.
