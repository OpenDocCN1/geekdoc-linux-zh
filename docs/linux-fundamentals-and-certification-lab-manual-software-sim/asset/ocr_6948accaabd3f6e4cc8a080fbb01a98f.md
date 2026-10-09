+   * The last section displays information about the query, such as when the query was done, the server and port that were used, and the returned message size.

```
# dig www.yahoo.com
```

```
;; <<>> DiG 9.2.1 <<>> www.yahoo.com
;; global options: printcmd
;; Got answer:
;; ->>HEADER<- opcode: QUERY, status: NOERROR, id: 36344
;; flags: qr rd ra; QUERY: 1, ANSWER: 9, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.yahoo.com.                IN      A

;; ANSWER SECTION:
www.yahoo.com.      1799    IN  CNAME   www.yahoo.akadns.net.
www.yahoo.akadns.net. 29        IN  A       216.109.118.70
www.yahoo.akadns.net. 29        IN  A       216.109.118.68
www.yahoo.akadns.net. 29        IN  A       216.109.118.78
www.yahoo.akadns.net. 29        IN  A       216.109.118.65
www.yahoo.akadns.net. 29        IN  A       216.109.118.69
www.yahoo.akadns.net. 29        IN  A       216.109.118.77
www.yahoo.akadns.net. 29        IN  A       216.109.118.71
www.yahoo.akadns.net. 29        IN  A       216.109.118.74

;; Query time: 73 msec
;; SERVER: 192.168.0.20#53(192.168.0.20)
;; WHEN: Fri Nov 21 10:22:46 2003
;; MSG SIZE  rcvd: 193
#
```

+   *   **host** This utility returns the IP address or addresses when given a hostname. In its simplest form, it returns only the IP address.

```
# host yahoo.com
yahoo.com has address 66.218.71.198
#
```

Use the **_-t ns_** option to list authoritative name servers for the domain.

```
# host -t ns yahoo.com
yahoo.com name server ns1.yahoo.com.
yahoo.com name server ns2.yahoo.com.
yahoo.com name server ns3.yahoo.com.
yahoo.com name server ns4.yahoo.com.
yahoo.com name server ns5.yahoo.com.
#
```

Use the **_-t mx_** option to list the mail servers for the domain. Three MX records were returned for this query to yahoo.com. A priority number is returned indicating that mx1 and mx2 are the preferred mail servers and mx4 is used if the other two are unavailable.

```
# host -t mx yahoo.com
yahoo.com mail is handled by 1 mx1.mail.yahoo.com.
yahoo.com mail is handled by 1 mx2.mail.yahoo.com.
yahoo.com mail is handled by 5 mx4.mail.yahoo.com.
#
```

The _-a_ option returns all available fields for the host. Use host with this option against your own server to ensure that it is providing all of the information needed.