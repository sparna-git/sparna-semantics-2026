## Introduction

Knowledge graphs are powerful sources of structured data, but they are often difficult to query. Writing a correct [SPARQL](cite:cites sparql11) query requires understanding the underlying schema, the available predicates, and the identifiers used in the graph. For users who are not familiar with SPARQL, this becomes a real obstacle when they want to turn an information need into a query and retrieve the corresponding data.

Large language models can help address this problem when they are connected to external tools through the [Model Context Protocol](cite:cites mcp). In this paper, we present an MCP server driven by a [SHACL](cite:cites shacl) specefication of the target data model. The server exposes the structure of the graph through a small set of schema-grounded tools that let an MCP-capable client discover the schema, inspect relevant shapes, reconcile named entities, and execute queries against the live endpoint.

The key idea is to ground query construction in the SHACL description of the data model rather than in the model’s prior knowledge. This makes the interaction more controlled, more transparent, and easier to adapt when the schema or the data evolve. We show how this approach supports natural-language access to knowledge graphs without hiding their structure.
