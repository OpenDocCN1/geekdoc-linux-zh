# ## DNS QUERIES AND RESPONSES

**Queries** A DNS query has three parts:

+   1. Name—Domain name, FQDN, or, for reverse name resolution, IP address
+   2. Type—Type of record requested (page 857)
+   3. Class—Always IN for Internet class

**Cache** Most DNS servers store in cache memory the query responses from other DNS servers. When a DNS server receives a query, it first tries to resolve the query from its cache. If that attempt fails, the server might query other servers to get an answer. Because DNS uses cache, when you make a change to a DNS record, the change takes time—sometimes a matter of *days*—to propagate throughout the DNS hierarchy.

**Responses** A DNS message sent in response to a query can hold the following records:

+   * Header record—Information about this message
+   * Query record—Repeats the query
+   * Answer records—Resource records that answer the query
+   * Authority records—Resource records for servers that have authority for the answers
+   * Additional records—Additional resource records, such as NS records

**If:** The `dig` and `host` utilities do not consult `/etc/nsswitch.conf` (page 495) to determine which server to query. The following example uses `dig` to query a DNS server. The `+all` option causes `dig` to query for all records.

```
```
$ dig +all google.com
...
;; QUESTION SECTION:
;google.com.                  IN     A

;; ANSWER SECTION:
google.com.           5       IN      A       74.125.19.147
google.com.           5       IN      A       74.125.19.99
google.com.           5       IN      A       74.125.19.103
google.com.           5       IN      A       74.125.19.104

;; AUTHORITY SECTION:
google.com.           5       IN      NS      ns3.google.com.
google.com.           5       IN      NS      ns4.google.com.
google.com.           5       IN      NS      ns1.google.com.
google.com.           5       IN      NS      ns2.google.com.

;; ADDITIONAL SECTION:
ns1.google.com.       5       IN      A       216.239.32.10
ns2.google.com.       5       IN      A       216.239.34.10
...
```
```