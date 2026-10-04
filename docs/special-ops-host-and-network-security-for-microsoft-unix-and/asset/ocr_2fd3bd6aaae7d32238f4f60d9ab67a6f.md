# 414 Chapter 8 · Attacking and Defending DNS

# dig @a.gtltld-servers.net www.example.com

```
; << DIG 9.1.3 << @a.gtltld-servers.net
;; global options: printcmd
;; Got answer:
;--HEADER<< opcode: QUERY, status: NOERROR, id: 23944
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 2, ADDITIONAL: 2

;; QUESTION SECTION:
;;www.example.com.
                                      IN       A

;; AUTHORITY SECTION:
example.com.                172800 IN NS       a.iana-servers.net.
example.com.                172800 IN NS       b.iana-servers.net.
```

Again the request is not answered, but you receive the list of servers that have received delegated authority over example.com. When you are following the authoritative answers from the beginning, you receive the two servers that are authoritative over every domain that ends with example.com. One more step and you will have an answer.

# dig @a.iana-servers.net www.example.com

```
; << DIG 9.1.3 << @a.iana-servers.net www.example.com
;; global options: printcmd
;; Got answer:
;--HEADER<< opcode: QUERY, status: NOERROR, id: 43748
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

;; QUESTION SECTION:
;;www.example.com.
                                      IN       A

;; ANSWER SECTION:
www.example.com.                172800 IN A        192.0.34.166
```

You now have received an authority DNS answer. The server replied with an answer because it has a local physical zone file with the A record. If you wanted to know the IP address of subdomain.example.com, you would