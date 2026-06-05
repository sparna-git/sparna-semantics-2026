## Introduction

Knowledge graphs are sources of trustworthy structured data, but they are often difficult to query. Writing a correct [SPARQL](cite:cites sparql11) query requires understanding the underlying schema, the available predicates, and the identifiers used in the graph. For users who are not familiar with SPARQL, this becomes a real obstacle when they want to turn an information need into a query and retrieve the corresponding data.

Large language models can help address this problem when they are connected to external tools through the [Model Context Protocol](cite:cites mcp). In this demo, we present an MCP server driven by the [SHACL](cite:cites shacl) specification of the underlying knowledge graph. The server exposes the structure of the graph through a small set of schema-grounded tools that let an MCP-capable client discover the schema, inspect relevant entities, reconcile named entities, and execute SPARQL queries.
