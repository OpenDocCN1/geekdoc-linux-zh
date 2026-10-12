```
~/dig +dnssec whitehouse.gov
; <<>> DiG 9.9.3-r1.13207.22-P2-RedHat-9.9.3-4.P2.el7 <<>> +dnssec whitehouse.gov
;; global options: +cmd
; Got answer:
; ->HEADER<= opcode: QUERY, status: NOERROR, id: 21388
; flags: qr rd ra ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1
; OPT PSEUDOSECTION:
; EDNS: version: 0, flags: do; udp: 4096
; QUESTION SECTION:
;whitehouse.gov. IN A
; ANSWER SECTION:
whitehouse.gov. 20 IN A 72.246.36.110
whitehouse.gov. 20 IN RRSIG A 7 2 20 20130825124016 20130822114016 8399 whitehouse.gov. BB8vHXEiAkPaLpr t3hq16kJDR0vkxjYTBxiGhuki/Bj n3PoIgYrftxR HH037TliOLsybj/uZv5hL4Uwwd/lw6n8GP1kqhz tAkm xddMQ2IARP6p wbM0kbSUv6N6GUT1Ww pbi+Le lFMqQCqA3se661yH0Je m7hTgPEUE1Zc 3oI=
; Query time: 227 msec
; SERVER: 127.0.0.1#53(127.0.0.1)
; WHEN: Thu Aug 22 22:01:52 EDT 2013
; MSG SIZE rcvd: 233
```

In addition to the A record, an RRSIG record is returned which contains the DNSSEC signature, as well as the inception time and expiration time of the signature. The **unbound** server indicated that the data was DNSSEC authenticated by returning the **ad** bit in the **flags:** section at the top.

If DNSSEC validation fails, the **dig** command would return a SERVFAIL error:

```
~/dig badsign-a.test.dnssec-tools.org
; <<>> DiG 9.9.3-r1.156.01-P1-RedHat-9.9.3-3.P1.el7 <<>> badsign- a.test.dnssec-tools.org
; global options: +cmd
; Got answer:
; ->HEADER<= opcode: QUERY, status: SERVFAIL, id: 1010
; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1
; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; QUESTION SECTION:
;badsign-a.test.dnssec-tools.org. IN A
; Query time: 1284 msec
; SERVER: 127.0.0.1#53(127.0.0.1)
; WHEN: Thu Aug 22 22:04:52 EDT 2013
; MSG SIZE rcvd: 60]
```

To request more information about the failure, DNSSEC checking can be disabled by specifying the **+cd** option to the **dig** command:

```
~/dig +cd +dnssec badsign-a.test.dnssec-tools.org
; <<>> DiG 9.9.3-r1.156.01-P1-RedHat-9.9.3-3.P1.el7 <<>> +cd +dnssec badsign-a.test.dnssec-tools.org
```