## MCP Tools description

{:#tools-description}

The schema-overview tool derives a high-level synthesis of the graph... it returns markdown... it lists... The schema overview is deliberately incomplete, it acts as a high-level table of contents that is not sufficient to write a correct query.

The graph structure discovery tool returns the detailed definitions of the shapes relevant to a question.... it also reads the SHACL file and returns a detailled list of properties for each kind of entity in the graph. For each property, the following information are provided: ...

Beyond structural constraints, each shape can also carry natural-language guidance through sh:agentInstruction, a non-validating feature introduced in SHACL 1.2. When the client discovers a shape, these instructions are returned alongside its predicates and cardinalities, allowing the data publisher to guide how a class or property should be used, for example by indicating which identifier to prefer or how to interpret a relation. The schema therefore conveys not only the structure of the graph, but also human-authored hints for the agent.

The example tools...

The entity reconciliation MCP tool relies on an underlying service that conforms with the [Reconciliation Service API Specification](cite:cites reconciliationapi). The reconciliation tool takes 2 input parameters : a label to search, and the URI identifier of the shape of the entity to lookup. It returns a list of entities, each with a score. The actual implementation of this service can be either a plain SPARQL-based search (not efficient and not suitable for plain-text lookups), proprietary full-text indexing capabilities of the triplestore, an existing API, or a custom-built search index, filled with the labels of the entities from the graph. Splitting

Finally, the SPARQL tool simply takes a SPARQL query as input, and returns the result in the XXXX format.

