## Demonstration

{:#demonstration}

The demo MCP-over-SPARQL server URL is **https://services.sparnatural.eu/mcp/ruim-mcp**. It exposes the structure of the [RUIM](cite:cites ruim), with its [SHACL specification](cite:cites ruimshacl).  

Using Claude Sonnet 4.6, low effort, with the request _"What are the generics of perindopril ?"_ (_"Quels sont les génériques du périndopril ?"_), and after reading the tools from the MCP-over-SPARQL server, the AI follows this sequence:

  1. Calls `get_few_shots` to read example queries
  2. Calls `discover_nodeshapes` with the shapes `med:GroupeGenerique` (_"generic drug grouping"_) and `med:SpecialitePharmaceutique` (_"medicinal product"_) and read their properties
  3. Calls `reconcile_entities` with label _"périndopril"_ and type `med:SpecialitePharmaceutique` - no result as "périndopril" is actually a Substance and not a medicinal product.
  4. Calls `reconcile_entities` again, this time with type `med:Substance` - it returns 4 Substances
  5. Then produces and executes the following SPARQL query


<pre><code>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX med: <http://data.esante.gouv.fr/ansm/medicament/>

SELECT DISTINCT ?groupeLabel ?refLabel ?genLabel ?titulaire
WHERE {
  ?groupe rdf:type med:GroupeGenerique ;
          rdfs:label ?groupeLabel .  
  # Le groupe doit contenir au moins une spécialité à base de périndopril (en substance active)
  {
    ?groupe med:specialiteDeReference ?ref .
    ?ref med:substanceActive <http://data.esante.gouv.fr/ansm/medicament/Substance_09586> .
  } UNION {
    ?groupe med:specialiteDeReference ?ref .
    ?ref med:substanceActive <http://data.esante.gouv.fr/ansm/medicament/Substance_46744> .
  } UNION {
    ?groupe med:specialiteDeReference ?ref .
    ?ref med:substanceActive <http://data.esante.gouv.fr/ansm/medicament/Substance_52431> .
  } UNION {
    ?groupe med:specialiteDeReference ?ref .
    ?ref med:substanceActive <http://data.esante.gouv.fr/ansm/medicament/Substance_69916> .
  }  
  OPTIONAL { ?ref rdfs:label ?refLabel }
  
  ?groupe med:specialiteGenerique ?gen .
  ?gen rdfs:label ?genLabel .
  OPTIONAL { ?gen med:titulaireCourant ?tit . ?tit rdfs:label ?titulaire }
}
ORDER BY ?groupeLabel ?genLabel
LIMIT 100
</code></pre><br/>


Note how the AI was able to overcome two ambiguities with the user query : 1/ it asking for generic drugs but using the name of a substance and not a product 2/ the name of the substance was itself ambiguous. Note also how the query is correct at the first iteration, and how extra properties, such as human-readable labels and the manufacturer, have been added, although not explicitely requested.
We also note that in this case, the tool `schema_overview` was not called by the AI. The correct shapes identifiers are already listed as enum in the tool description of `discover_nodeshape`, hence the AI did not felt the necessity to call the overview.