be handy in case we are trying to track down a problem where one DNS server has stale records and another doesn't, because we can tell which DNS server our client contacted for each request.

By default dig attempts to resolve a hostname into an IP, but you can also have dig bring back any other DNS record for a domain. To do this, just add the record type to the end of your query (i.e., NS, MX, TXT). This is particularly handy when you want to know what name servers or mail servers are configured for a particular domain:

```
$ dig example.net NS
; <<> DiG 9.7.0-P1 <<> example.net NS
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 38194
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 2

;; QUESTION SECTION:
;example.net. IN NS

;; ANSWER SECTION:
example.net. 300 IN NS ns1.example.net.
example.net. 300 IN NS ns2.example.net.

;; ADDITIONAL SECTION:
ns1.example.net. 300 IN A 10.1.1.3
ns2.example.net. 300 IN A 10.1.1.4

;; Query time: 3 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Sat Mar 24 20:44:42 2012
;; MSG SIZE rcvd: 98
```

You'll find this sort of dig query much more useful as we troubleshoot zone transfer issues further on in this chapter and mail server troubleshooting in Chapter 7.

# Trace a DNS Query

Generally speaking, when you look up a DNS record, your machine doesn't look everything up itself; instead, you send your request to a DNS server