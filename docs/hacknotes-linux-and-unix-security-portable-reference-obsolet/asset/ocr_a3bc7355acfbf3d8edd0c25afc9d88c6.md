16
Part I: Hacking Techniques and Defenses

```
;; AUTHORITY SECTION:
somecompanyasanexample.com. 4 IN NS
ns1.someexampleleserver.net.

somecompanyasanexample.com. 4 IN NS
ns2.someexampleleserver.net.

;; ADDITIONAL SECTION:
ns1.someexampleleserver.net. 678 IN A 10.0.0.1
ns2.someexampleleserver.net. 141521 IN A 192.168.1.1
```

```
;; Query time: 102 msec
;; SERVER: 10.1.1.1#53(10.1.1.1)
;; WHEN: Mon Jan 13 04:04:38 2003
;; MSG SIZE rcvd: 141
```

The dig command queried our ISP's default DNS server (10.1.1.1) for **somecompanyasanexample.com**'s MX records and returned to us its mail server: mail.someexampleleserver.com.

# ZONE TRANSFERS

DNS servers are generally configured to act as either a primary server or a secondary server. The reason for this approach is to provide hierarchy and redundancy. A zone transfer occurs when a secondary DNS server contacts a primary DNS server in order to update its zone information. DNS hostname information obtained via zone transfers may reveal the role or location of particular hosts in an organization. Quite often, primary DNS servers are incorrectly configured to allow any host to perform a zone transfer.

# Performing Zone Transfers Using the host Command

To attempt a zone transfer for a particular organization, a DNS server IP address is required. If this information is not available, a whois query of the target domain can be attempted, and this will provide the relevant DNS IP addresses. Once a DNS server IP address is obtained, a zone transfer can be attempted using the host command:

```
host -l domain DNSIP
```

For example:

```
[bash]$ host -1 somecompanyasanexample.com 10.0.0.1
Using domain server:
Name: 10.0.0.1
```