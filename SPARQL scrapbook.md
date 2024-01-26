# Various queries that help me to provide an overview, and to further expand my SPARQL skills

## Interestingly, you can perform queries on remote endpoints using SERVICE
This works in Blazegraph:

```
select * 
where {
	SERVICE <https://query.wikidata.org/sparql>
    {
  		<http://www.wikidata.org/entity/Q44402672> ?p ?o 
    }
}
```
