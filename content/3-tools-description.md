## MCP Tools description

{:#tools-description}

The schema overview tool derives a high-level synthesis of the graph and returns it as markdown listing the classes it contains. It is deliberately incomplete and acts as a high-level table of contents, not sufficient on its own to write a correct query.

The discover nodeshapes tool returns the detailed definitions of the shapes relevant to a question. It reads the SHACL file and returns a detailed list of properties for each kind of entity in the graph. For each property, it provides details such as its path, datatype, and cardinality.

Beyond structural constraints, each shape can also carry natural-language guidance through sh:agentInstruction, a non-validating feature introduced in SHACL 1.2. When the client discovers a shape, these instructions are returned alongside its predicates and cardinalities, allowing the data publisher to guide how a class or property should be used, for example by indicating which identifier to prefer or how to interpret a relation. The schema therefore conveys not only the structure of the graph, but also human-authored hints for the agent.

The get few shots tool returns curated, validated query patterns that serve as few-shot examples for the graph.

The reconcile entities tool relies on an underlying service that conforms to the [Reconciliation Service API Specification](cite:cites reconciliationapi). It takes two input parameters, a label to search and the URI of the entity's shape to look up, and returns a list of entities, each with a score. This service can be implemented as a plain SPARQL-based search (inefficient and unsuitable for plain-text lookups), the triplestore's proprietary full-text indexing, an existing API, or a custom-built search index filled with the labels of the graph's entities.

Finally, the query sparql tool simply takes a SPARQL query as input and returns the result in the appropriate format.
