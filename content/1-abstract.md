## Abstract

{:#abstract}

MCP-over-SPARQL is a Model Context Protocol server that provides tools enabling a client LLM to successfully write an execute a valid SPARQL query on a knowledge graph. The server connects an MCP-capable LLM client to a SPARQL endpoint together with other tools for retrieving an overview of the graph, curated query examples, and the detailled knowledge graph structure from a SHACL specification. In addition, it exposes a reconciliation function to retrieve entity URIs from a label and a type. This provides all the necessary primitives for an LLM client to turn a natural language question into a SPARQL query, using a correct graph structure and valid URI identifiers. The system reduces schema guessing and returns data from the endpoint. We demonstrate the approach on the the Standardized Drug Nomenclature of France e-health agency, and show how it supports controlled, schema-aware querying of domain-specific knowledge graphs.
