# dig

The Domain Information Groper is a command-line utility that queries DNS nameservers. By default, `dig` uses the nameservers listed in `/etc/resolv.conf` and performs an NS (nameserver) query. Reverse lookups are accomplished with the `-x` argument with a default A (Address) query.

Here is an example of a forward lookup with `dig`:

```
$ dig www.pearson.com

; <<>> DiG 9.5.0a6 <<>> www.pearson.com
; global options: printcmd
; Got answer:
; ->>HEADER<<; opcode: QUERY, status: NOERROR, id: 5889
; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 3, ADDITIONAL: 3

; QUESTION SECTION:
;www.pearson.com.                IN    A

; ANSWER SECTION:
www.pearson.com.            86400 IN    A   195.69.212.200

; AUTHORITY SECTION:
pearson.com.                46430 IN    NS    ns2.pearson.com.
pearson.com.                46430 IN    NS    oldtxdns2.pearson.com.
pearson.com.                46430 IN    NS    ns.pearson.com.

; ADDITIONAL SECTION:
ns.pearson.com.             162044 IN    A   195.69.213.15
ns2.pearson.com.            78028 IN    A   195.69.215.15
oldtXdns2.pearson.com.      139762 IN    A   192.251.135.15

; Query time: 50 msec
; SERVER: 192.168.0.1#53(192.168.0.1)
; WHEN: Sun Oct 28 20:02:53 2007
; MSG SIZE  rcvd: 166
```

And here is a reverse lookup with `dig`:

```
$ dig 195.69.212.200

; <<>> DiG 9.5.0a6 <<>> 195.69.212.200
; global options: printcmd
; Got answer:
; ->>HEADER<<; opcode: QUERY, status: NXDOMAIN, id: 53249
; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 0

; QUESTION SECTION:
```