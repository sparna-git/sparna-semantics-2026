## Schema-Grounded Query Workflow

{:#workflow}

In the best case, the client turns a natural-language question into a correct SPARQL query by following the expected multi-step workflow shown in Figure 2, instead of issuing a single black-box call.

<figure id="fig-workflow">
<img src="img/sequence.svg" alt="Sequence diagram: a natural-language question goes from the user to the MCP client, which calls the server's tools in order — schema_overview and discover_nodeshapes read the SHACL model, reconcile_entities returns entity IRIs, and query_sparql executes against the SPARQL endpoint — and real-data results are returned to the user.">
<figcaption markdown="block">
Lifecycle of a single query: the MCP client orchestrates the server's tools to turn a natural-language question into a query executed against the endpoint, returning real data.
</figcaption>
</figure>

This order is not enforced, however. The tool descriptions recommend discovering the schema first and never guessing predicates or paths from prior knowledge, but the client stays free to call the tools in whatever order it needs, using only the ones relevant to the question.
