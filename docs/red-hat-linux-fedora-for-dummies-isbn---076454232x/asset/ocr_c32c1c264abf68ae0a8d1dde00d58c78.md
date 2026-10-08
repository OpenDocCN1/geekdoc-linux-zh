You can specify as many as three name servers, so you may add your ISP's name server as an alternative:

```
```text
search paunchy.net
nameserver 192.168.1.254
nameserver 198.59.115.2
```
```

Open a **GNOME Terminal** window and run this command.

```
```text
host cancun
```
```

You see this result:

```
```text
cancun.paunchy.net  has  address 192.168.1.121
```
```

The **host** command provides numerous options that provide more information about your query. For example, you can see information about where the *host* command gets its information. Add the verbose (-v) option to the preceding example and you see this information.

```
```text
Trying "cancun.paunchy.net"
; ->HEADER<- opcode: QUERY,  status: NOERROR,  id: 18016
;  flags: qr aa rd ra;  QUERY: 1,  ANSWER: 1,  AUTHORITY: 1,
;       ADDITIONAL: 0

;  QUESTION  SECTION:
;cancun.paunchy.net.     IN     A

;  ANSWER  SECTION:
cancun.paunchy.net.     86400  IN  A  192.168.1.1

;  AUTHORITY  SECTION:
paunchy.net.            86400  IN  NS   ns.paunchy.net.1
Received 69 bytes from 192.168.1.120#53  in 263 ms
```
```

This list describes what the various sections in the preceding output mean.

+   * **Question section:** You see in the Question section that the query is cancun.paunchy.net. Note that we ask for only the address of cancun but that the search parameter in the res ov. conf file specifies that the paunchy.net domain be appended to cancun. You also see that an A record is part of the query — you're asking for an IP address.
* **Answer section:** This is the answer to your query. The answer includes the host name and domain — cancun.sandia.gov — and its numeric IP address. The Answer section also includes the time-to-live (TTL) value.