# Various queries that help me to provide an overview, and to further expand my SPARQL skills

## Interestingly, you can perform queries on remote endpoints using SERVICE
This works in my Blazegraph (can also simply query everything using ?s instead of me as entity):

```
select * 
where {
	SERVICE <https://query.wikidata.org/sparql>
    {
  		<http://www.wikidata.org/entity/Q44402672> ?p ?o 
    }
}
```

```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX meshv: <http://id.nlm.nih.gov/mesh/vocab#>
PREFIX mesh: <http://id.nlm.nih.gov/mesh/>
PREFIX mesh2024: <http://id.nlm.nih.gov/mesh/2024/>
PREFIX mesh2023: <http://id.nlm.nih.gov/mesh/2023/>
PREFIX mesh2022: <http://id.nlm.nih.gov/mesh/2022/>

select * 
where {
	SERVICE <https://id.nlm.nih.gov/mesh/sparql>
    {
      SELECT DISTINCT ?class
      WHERE { [] a ?class . }
      ORDER BY ?class
    }
}
```


# List of SPARQL endpoints
| Human Endpoint | API Endpoint |
|---|---|
| https://id.nlm.nih.gov/mesh/query | https://id.nlm.nih.gov/mesh/sparql |
| https://query.wikidata.org/ | https://query.wikidata.org/sparql |
| https://ronaldcornet.nl/blazegraph/#query| https://ronaldcornet.nl/blazegraph/sparql - login needed, how?| 
