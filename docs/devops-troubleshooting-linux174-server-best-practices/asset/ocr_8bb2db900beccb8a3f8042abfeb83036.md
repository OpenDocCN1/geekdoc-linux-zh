Although DNS caching can be quite handy, one problem for DNS administrators is that not every DNS server out there honors your TTL. In fact, some ISPs have been known to completely disregard TTLs that are too low, to help reduce the load on their DNS servers. Because of this, even though you may have a TTL of only a few minutes, a DNS change you make may take hours to show up on a DNS server that doesn't obey it.

The easiest way to see the TTL for a zone, outside of viewing it on the DNS server itself, is via the `dig` command:

```
$ dig web1.example.net
; <<> DiG 9.7.0-P1 <<> example.net
;; global options: +cmd
;; Got answer:
; ->HEADER<- opcode: QUERY, status: NOERROR, id: 30750
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

; QUESTION SECTION:
;web1.example.net.     IN A

; ANSWER SECTION:
web1.example.net.      300 IN A 10.1.2.5

; AUTHORITY SECTION:
example.net.           300 IN NS ns2.example.net.
example.net.           300 IN NS ns1.example.net.

; ADDITIONAL SECTION:
ns1.example.net.       300 IN A 10.1.1.3
ns2.example.net.       300 IN A 10.1.1.4

; Query time: 2 msec
; SERVER: 192.168.0.1#53(192.168.0.1)
; WHEN: Mon Mar 19 20:48:27 2012
; MSG SIZE rcvd: 118
```

Along with each record `dig` reports back, it also includes the TTL, not just for the main record you requested, but also for any additional information it may return. In this case, the TTLs for all the records happen to be 300 seconds. This tells us that if we make a change to the web1.example.net record, we can expect it to take up to 5 minutes for an ordinary DNS server to return the new record.