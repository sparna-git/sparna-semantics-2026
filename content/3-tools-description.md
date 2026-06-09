## MCP Tools description

{:#tools-description}

The `schema_overview` tool derives a high-level synthesis of the graph and returns it as markdown listing the classes it contains along with some additional information about each of them. It is deliberately incomplete and acts as a high-level table of contents, not sufficient on its own to write a correct query.

The `discover_nodeshapes` tool returns detailed definitions of shapes/classes. It reads the SHACL file and returns a detailed list of properties for each requested shape. For each property, it provides a label and description and details such as its path, datatype, and cardinality. Beyond structural constraints, each shape can also carry natural-language guidance through `sh:agentInstruction`, a non-validating feature introduced in SHACL 1.2. When the client discovers a shape, these instructions are returned alongside its predicates and cardinalities, allowing the data publisher to guide how a class or property should be used, for example by indicating which identifier to prefer or how to interpret a relation. The schema therefore conveys not only the structure of the graph, but also human-authored hints for the agent.

The `get_few_shots` tool returns curated, validated examples for the graph, each pairing a natural-language question with its expected SPARQL query.

The `reconcile_entities` tool relies on an underlying service that conforms to the [Reconciliation Service API Specification](cite:cites reconciliationapi). It takes two input parameters, a label to search and the URI of the entity's shape to look up, and returns a list of entities, each with a score. This service can be implemented, depending on the project, as a plain SPARQL-based search (inefficient and unsuitable for plain-text lookups), the triplestore's proprietary full-text indexing, an existing API, or a custom-built search index filled with the labels of the graph's entities.

Finally, the `query_sparql` tool simply takes a SPARQL query as input and returns the result in `application/sparql-results+json`.
