## Schema-Grounded Query Workflow

{:#workflow}

To turn a natural-language question into a correct SPARQL query, the client follows an explicit multi-step workflow rather than relying on a single black-box service. It first requests a high-level schema overview, then retrieves a few curated example queries, discovers the node shapes relevant to the question, reconciles any named entities to real IRIs, and finally builds and executes the query. Splitting the task this way keeps each step explicit and inspectable. Figure 2 illustrates this lifecycle for a single request.

<figure id="fig-workflow">
<img src="img/sequence.svg" alt="Sequence diagram: a natural-language question goes from the user to the MCP client, which calls the server's tools in order — schema_overview and discover_nodeshapes read the SHACL model, reconcile_entities returns entity IRIs, and query_sparql executes against the SPARQL endpoint — and real-data results are returned to the user.">
<figcaption markdown="block">
Lifecycle of a single query: the MCP client orchestrates the server's tools to turn a natural-language question into a query executed against the endpoint, returning real data.
</figcaption>
</figure>


This ordering is enforced by the tools’ own descriptions, which instruct the client to go through discovery first and never to guess predicates or paths from prior knowledge.

When the question mentions named entities, they are reconciled to the IRIs actually used in the graph before the final query is assembled, so the query targets exact resources rather than relying on fragile label matching. The query is then executed against the endpoint, and the user receives its result, real data drawn from the graph, produced by a query the client could not have written from its prior knowledge alone.
