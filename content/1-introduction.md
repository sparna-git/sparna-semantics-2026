## Introduction

Knowledge graphs are sources of trustworthy structured data, but leveraging this data directly in [SPARQL](cite:cites sparql11) requires understanding the underlying schema, the available predicates, and the identifiers used in the graph. For data publishers, making their knowledge graph query-able by AI is another dissemination channel to maximise its dissemination and reuse.

Large Language Models (LLM) can query external sources when they are connected to external tools through the [Model Context Protocol](cite:cites mcp). In this demo, we present an MCP server driven by a [SHACL](cite:cites shacl) specification of the underlying knowledge graph. The server exposes the structure of the graph through a small set of schema-grounded tools that let an MCP-capable client discover the schema, inspect relevant types, reconcile named entities, and execute SPARQL queries.
