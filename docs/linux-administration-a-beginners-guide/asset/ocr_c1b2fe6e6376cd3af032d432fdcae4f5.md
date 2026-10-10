| Option | Description |
|---|---|
| *statistics-file-path-name* | Path name of the file into which the server appends statistics information when the *ndc stats* command is run. |
| *auth-nxdomain* yes/no; | If you specify Yes (the default), the server will always answer authoritatively on domain queries for which it is authoritative. Caution: Do not specify No unless you really know what you're doing. |
| *deallocte-on-exit* yes/no; | When set to Yes, the server will write out a complete report of memory allocation. Results in a longer shutdown time but is useful for analysis of memory usage. Default is No. |
| *fake-iquery* yes/no; | Default is No. If Yes, the server will simulate the obsolete IQUERY query type. Like the *auth-nxdomain* option, don't turn this on unless you know what you're doing. |
| *fetch-glue* yes/no; | Yes (the default) tells the server to fetch (and cache) the necessary records to answer queries about domains on which it is not authoritative. Setting this to No, along with the *recursion* option, prevents your cache from growing and becoming corrupted by malicious attacks. However, clients have to do more work for each query. |
| *host-statistics* yes/no; | Tells BIND whether to keep track of statistics for each host that queries it. Although the information is useful, the tracking consumes substantial memory; thus the default is No. |

Table 12-2. BIND Configuration Options (continued)