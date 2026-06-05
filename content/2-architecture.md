## System Architecture

{:#architecture}

MCP-over-SPARQL sits between an MCP-capable LLM client and a SPARQL endpoint. Rather than exposing a single opaque question-to-answer service, it decomposes natural-language querying into a small set of explicit tools, including a schema overview that summarizes the graph, curated few-shot examples that provide validated query patterns, node-shape discovery that returns the relevant SHACL definitions in detail for each one, entity reconciliation that maps user-provided labels to stable IRIs, and SPARQL execution that runs the final query. A lightweight healthcheck tool is also available to report server status and endpoint reachability. Figure 1 shows the overall architecture.

<figure id="fig-architecture">
<img src="img/architecture.svg" alt="Architecture diagram: an MCP client (LLM) connects over stdio or HTTP to the MCP-over-SPARQL server, whose tools (schema overview, curated examples, node-shape discovery, entity reconciliation, SPARQL execution, and healthcheck) read the SHACL model, resolve entities through a reconciliation service, and execute queries against the SPARQL endpoint.">
<figcaption markdown="block">
Architecture of MCP-over-SPARQL: an MCP client (LLM) drives the server's tools, which are grounded in a SHACL model of the data, resolve entities through a reconciliation service, and execute queries against the project's SPARQL endpoint.
</figcaption>
</figure>

The server can be accessed through two transports. A local stdio transport is used for development, testing, and local use, while a Streamable HTTP transport serves remote clients. The server can be configured per "project". Each project corresponds to a specific knowledge graph, with its own SHACL model and SPARQL endpoint, and is exposed as a dedicated MCP server.
