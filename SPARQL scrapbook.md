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

## This queries MeSH
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

## Trying to understand how SNOMED CT is represented in GraphDB
```
# an example for Covid-19
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select * where {
    <http://snomed.info/id/840539006> (owl:equivalentClass|rdfs:subClassOf|owl:intersectionOf|rdf:first)+ ?s1 .
    ?s1 ?p ?o
} 
```
Or (adding rdf:rest, only skos:prefLabel)
```
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
select * where {
    <http://snomed.info/id/840539006> (owl:equivalentClass|rdfs:subClassOf|owl:intersectionOf|rdf:first|rdf:rest)* ?s1 .
    ?s1 skos:prefLabel ?o
} 
```


## Show all Graphs with the number of triples (doesn't work for Blazegraph, though)
```
SELECT  DISTINCT ?g (count(?s) as ?cs) WHERE  { GRAPH ?g {?s ?p ?c} } ORDER BY  Desc(?cs)
```


# List of SPARQL endpoints

Over 2500 SPARQL endpoints are monitored by [Yummy data](https://yummydata.org/)

| Service | Human Endpoint | API Endpoint |
|---|---|---|
| DBPedia | https://dbpedia.org/sparql | https://dbpedia.org/sparql |
| MeSH | https://id.nlm.nih.gov/mesh/query | https://id.nlm.nih.gov/mesh/sparql |
| Ronald Cornet | https://ronaldcornet.nl/blazegraph/#query| https://ronaldcornet.nl/blazegraph/sparql - login with Basic Auth header| 
| Ronald Cornet | https://ronaldcornet.nl/virtuoso/ | https://ronaldcornet.nl/virtuoso/ |
| Wikidata | https://query.wikidata.org/ | https://query.wikidata.org/sparql |

