# EXAMPLES

```
roqet sparql-query-file.rq
```

Run a SPARQL query contained in the local file sparql-query-file.rq. The data used would be described in FROM statements in the query file.

```
roqet -q -i sparql
```

Run a SPARQL query that is in the web at URI without an extra sages (quiet, -q).

```
roqet -q query-file.rq
```

Run an query (default language SPARQL) from a local file query-file.rq but using base URI to resolve any relative URIs.

```
roqet -q -i sparql -r x
```

Run a SPARQL query that is in the web at URI and format the results in the SPARQL Query Results XML format with no extra sages.

```
roqet -i sparql -e ‘SELECT * WHERE { ?s ?p ?o }’-D stuff.rdf
```

Run a SPARQL query given on the command line against data in the file stuff.rdf. The type of the file will be guessed and likely is of format RDF/XML.

```
roqet -t result.srx -r ht
```

Read a SPARQL query results in SPARQL Query Results XML format (default) and print it in HTML.

```
roqet -t result.ttl -R turtle -r csv
```

Read a SPARQL query results in RDF/Turtle format and print it in CSV.