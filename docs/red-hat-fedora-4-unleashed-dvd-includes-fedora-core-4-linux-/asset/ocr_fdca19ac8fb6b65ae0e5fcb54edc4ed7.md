Continuing with NS.TELSTRA.NET, we have

```
```
$ dig @NS.TELSTRA.NET 66.109.200.203.in-addr.arpa PTR +norec

; <<>> DiG 9.2.1 <<>> @NS.TELSTRA.NET 66.109.200.203.in-addr.arpa PTR +norec
; global options: printcmd
; Got answer:
; ->>HEADER<- opcode: QUERY, status: NOERROR, id: 12099
; flags: qr ra; QUERY: 1, ANSWER: 0, AUTHORITY: 2, ADDITIONAL: 2

; QUESTION SECTION:
;66.109.200.203.in-addr.arpa.    IN    PTR

; AUTHORITY SECTION:
200.203.in-addr.arpa.    142315 IN    NS    dns.vsn1.net.in.
200.203.in-addr.arpa.    142315 IN    NS    ns3.vsn1.com.

; ADDITIONAL SECTION:
dns.vsn1.net.in.        33557 IN    A    202.54.1.30
ns3.vsn1.com.            5370 IN    A    203.197.12.42

; Query time: 293 msec
; SERVER: 203.50.0.137#53(NS.TELSTRA.NET)
; WHEN: Wed Sep  4 21:18:09 2002
; MSG SIZE rcvd: 132
```
```

And then,

```
```
$ dig @ns3.vsn1.com. 66.109.200.203.in-addr.arpa PTR +norec

; <<>> DiG 9.2.1 <<>> @ns3.vsn1.com. 66.109.200.203.in-addr.arpa PTR +norec
; global options: printcmd
; Got answer:
; ->>HEADER<- opcode: QUERY, status: NXDOMAIN, id: 37848
; flags: qr aa ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 0

; QUESTION SECTION:
;66.109.200.203.in-addr.arpa.    IN    PTR
```
```