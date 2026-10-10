# OTHER OPTIONS

-c, —count  
Only count the triples and produce no other output.

-d, —dump-query FORMAT  
Print the parsed query out in a given FORMAT one of ‘none’ (default), ‘debug’, ‘structure’ or ‘sparql’

-D, —data URI  
Add RDF data source URI (not a nad graph). If no data sources are given, the query itself st point to the data such as via SPARQL FROM uri statements.

-E, —ignore-errors  
Do not print error ssgages and do not exit with a non-0 status.

-f, —feature NAME(=VALUE)  
Set query feature NAME to the VALUE or integer 1 if omitted. The known features can be shown with -f help or —feature help.

-F, —format NAME  
Set the data source format na for subsequent data graphs called with -D / —data or - G / —nad. The default if this is not specified is for the query engine to guess. The na is a Raptor parser na.

-G, —nad URI  
Add RDF data source URI (nad graph)

-h, —help  
Show a summary of the options.

-n, —dryrun  
Prepare the query but do not execute it.

-q, —quiet  
No extra information ssgages.

-s, —source URI  
Add RDF data source URI (nad graph) URI by adding it to the list of query data source URIs. FORMAT to ‘simple’ (default) or ‘x’ (an experimental XML format)

-v, —version  
Print the rasqal library version and exit.

-W, —warnings LEVEL  
Set the warning LEVEL in the range 0 (do not warn about anything) to 100 (show every warning). The Rasqal default is in the middle (50).