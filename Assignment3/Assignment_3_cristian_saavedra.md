# spqrQL Assignment 3

## Descripion
Create the SPARQL query and the result for the following queries expressed in natural language. The endpoint that you can use for this exercise is: http://es.dbpedia.org/sparql

### Query 1

**Description**:<br>
Get all the properties that can be applied to instances of the Politician class (<http://dbpedia.org/ontology/Politician>)

**Query**:
```sql 
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT DISTINCT ?property
WHERE {
  ?politician a dbo:Politician .
  ?politician ?property ?value .
}
```

[**Result Link**](https://es.dbpedia.org/sparql?default-graph-uri=&query=PREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fproperty%0D%0AWHERE+%7B%0D%0A++%3Fpolitician+a+dbo%3APolitician+.%0D%0A++%3Fpolitician+%3Fproperty+%3Fvalue+.%0D%0A%7D&should-sponge=&format=text%2Fx-html%2Btr&timeout=0&debug=on&run=+Run+Query+)



### Query 2

**Description**:<br>
Get all the properties, except rdf:type, that can be applied to instances of the Politician class

**Query**:
```sql 
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?property
WHERE {
  ?politician a dbo:Politician .
  ?politician ?property ?value .
  FILTER (?property != rdf:type)
}
```

[**Result Link**](https://es.dbpedia.org/sparql?default-graph-uri=&query=PREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fproperty%0D%0AWHERE+%7B%0D%0A++%3Fpolitician+a+dbo%3APolitician+.%0D%0A++%3Fpolitician+%3Fproperty+%3Fvalue+.%0D%0A++FILTER+%28%3Fproperty+%21%3D+rdf%3Atype%29%0D%0A%7D&should-sponge=&format=text%2Fx-html%2Btr&timeout=0&debug=on&run=+Run+Query+)

### Query 3

**Description**:<br>
Which different values exist for the properties, except for rdf:type, applicable to the instances of Politician?

**Query**:
```sql 
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?value
WHERE {
  ?politician a dbo:Politician .
  ?politician ?property ?value .
  FILTER (?property != rdf:type)
}
```

[**Result Link**](https://es.dbpedia.org/sparql?default-graph-uri=&query=PREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fvalue%0D%0AWHERE+%7B%0D%0A++%3Fpolitician+a+dbo%3APolitician+.%0D%0A++%3Fpolitician+%3Fproperty+%3Fvalue+.%0D%0A++FILTER+%28%3Fproperty+%21%3D+rdf%3Atype%29%0D%0A%7D&should-sponge=&format=text%2Fx-html%2Btr&timeout=0&debug=on&run=+Run+Query+)

### Query 4

**Description**:<br>
For each of these applicable properties, except for rdf:type, which different values do they take globally for all those instances?

**Query**:
<!-- sql tag added only for syntax highlight -->
```sql 
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?property ?value
WHERE {
  ?politician a dbo:Politician .
  ?politician ?property ?value .
  FILTER (?property != rdf:type)
}
ORDER BY ?property
```

[**Result Link**](https://es.dbpedia.org/sparql?default-graph-uri=&query=PREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Fproperty+%3Fvalue%0D%0AWHERE+%7B%0D%0A++%3Fpolitician+a+dbo%3APolitician+.%0D%0A++%3Fpolitician+%3Fproperty+%3Fvalue+.%0D%0A++FILTER+%28%3Fproperty+%21%3D+rdf%3Atype%29%0D%0A%7D%0D%0AORDER+BY+%3Fproperty&should-sponge=&format=text%2Fx-html%2Btr&timeout=0&debug=on&run=+Run+Query+)
(It will take some time)

### Query 5

**Description**:<br>
For each of these applicable properties, except for rdf:type, how many distinct values do they take globally for all those instances?

**Query**:
<!-- sql tag added only for syntax highlight -->
```sql 
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?property (COUNT(DISTINCT ?value) AS ?valueCount)
WHERE {
  ?politician a dbo:Politician .
  ?politician ?property ?value .
  FILTER (?property != rdf:type)
}
GROUP BY ?property
ORDER BY DESC(?valueCount)
```

[**Result Link**](https://es.dbpedia.org/sparql?default-graph-uri=&query=PREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0A%0D%0ASELECT+%3Fproperty+%28COUNT%28DISTINCT+%3Fvalue%29+AS+%3FvalueCount%29%0D%0AWHERE+%7B%0D%0A++%3Fpolitician+a+dbo%3APolitician+.%0D%0A++%3Fpolitician+%3Fproperty+%3Fvalue+.%0D%0A++FILTER+%28%3Fproperty+%21%3D+rdf%3Atype%29%0D%0A%7D%0D%0AGROUP+BY+%3Fproperty%0D%0AORDER+BY+DESC%28%3FvalueCount%29&should-sponge=&format=text%2Fx-html%2Btr&timeout=0&debug=on&run=+Run+Query+)


