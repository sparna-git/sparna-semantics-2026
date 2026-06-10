## Demonstration

{:#demonstration}

An online demo of MCP-over-SPARQL is **https://services.sparnatural.eu/mcp/ruim-mcp**. It exposes the structure of the [Standardized Drug Nomenclature of France e-health agency (RUIM)](cite:cites ruim), with its [SHACL specification](cite:cites ruimshacl). It should be noted that the SHACL specification contains extensive documentation of each entity and properties. The SPARQL queries below can be tested against the [online RUIM endpoint](cite:cites ruimendpoint).

Using Mistral Vibe (Chat) with the query _"What does bi profenid contains ?"_ (_"Que contient le bi profénid ?"_), the AI follows this sequence:

  1. Calls `discover_nodeshapes` with the shapes `med:SpecialitePharmaceutique`, `med:Element` and `med:Substance` (_"medicinal product"_, _"manufactured item"_ and _"substance"_) to read their properties
  2. Calls `reconcile_entities` with "bi profenid" on `med:SpecialitePharmaceutique`, and retrieves its URI (`...SpecialitePharmaceutique_61165486`)
  3. Generates and executes the following query, to retrive the correct answer ("Ketoprofène"):

<pre><code>
PREFIX med: <http://data.esante.gouv.fr/ansm/medicament/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?substance ?substance_label WHERE {
  <http://data.esante.gouv.fr/ansm/medicament/SpecialitePharmaceutique_61165486> med:substanceActive ?substance .
  ?substance rdfs:label ?substance_label .
  FILTER(LANG(?substance_label) = 'fr')
}
LIMIT 20
</code></pre><br/>

We note that the tool `schema_overview` was not called by the AI. The allowable shapes identifiers are already listed as enum in the input schema of the `discover_nodeshape` tool, hence the AI did not felt the necessity to call the overview.


Using Claude Sonnet 4.6, low effort, with the request _"What are the generics of perindopril ?"_ (_"Quels sont les génériques du périndopril ?"_), and after reading the tools from the MCP-over-SPARQL server, the AI follows this sequence:

  1. Calls `get_few_shots` to read example queries
  2. Calls `discover_nodeshapes` with the shapes `med:GroupeGenerique` (_"generic drug grouping"_) and `med:SpecialitePharmaceutique` (_"medicinal product"_) to read their properties
  3. Calls `reconcile_entities` with label _"périndopril"_ and type `med:SpecialitePharmaceutique` - no result as "périndopril" is actually a Substance and not a medicinal product.
  4. Calls `reconcile_entities` again, this time with type `med:Substance` - it returns 4 Substances
  5. Then produces and executes a (correct) SPARQL query containing the 4 Substances URI, the drug groupings and the marketing authorization holder of each drug (although not requested) 


Note how the AI was able to overcome two ambiguities with the original query : 1/ it asks for generic drugs but using the name of a substance and not a product 2/ the name of the substance is itself ambiguous. Note also how the query is correct at the first iteration, and contains human-readable labels and marketing authorization holder.

Some tests show the limits of the approach :
  - Sometimes the AI does not use the MCP server but uses a web search, or its own knowledge
  - Sometimes the AI does not use the reconcile_entities tool but rather tries to lookup the entities directly in SPARQL (we tried to mitigate that with `sh:agentInstruction` hints)
  - Sometimes the answer is correct but requires multiple queries in order to retrieve a good result