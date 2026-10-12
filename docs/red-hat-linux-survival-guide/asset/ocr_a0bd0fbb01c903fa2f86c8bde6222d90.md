# Listing 15-10 Continued

```
;; trying nameserver ns1.domain.com.
;; 3 A records found.

ERROR: "ns1.domain.com. A 172.20.15.1", but the PTR record for
    1.15.20.172.in-addr.arpa. is "k2.domain.com."

One of the above two records are wrong unless the host is a name
server or mail server.

To have 2 names for 1 address on any other hosts, replace the A record
with a CNAME record:
ns1.domain.com. IN     CNAME   k2.domain.com.

ERROR: "ns2.domain.com. A 172.20.15.1", but the PTR record for
    1.15.20.172.in-addr.arpa. is "k2.domain.com."

One of the above two records are wrong unless the host is a name
server or mail server.

To have 2 names for 1 address on any other hosts, replace the A record
with a CNAME record:
ns2.domain.com. IN     CNAME   k2.domain.com.

;; no subzones found below domain.com., so no recursion will take place.
;; ==============================================================
;; dlint of domain.com. run ending with errors.
;; run ending: Sat Dec 29 13:34:09 EST 2001
;; ==============================================================
;; dlint of domain.com run ending with errors.
;; run ending: Sat Dec 29 13:34:09 EST 2001
```

As you can see, dlint is very verbose. The lines that start with a semi-colon are considered comments. All other lines are warnings or errors. Here, domain.com has a set of problems. The ns1.domain.com has an A record but the PTR record points to k2.domain.com instead of ns1.domain.com. Similarly, the ns2.domain.com host has the same problem. In other words, the domain.com configuration has the following lines:

```
ns1      IN      A      172.20.15.1
ns2      IN      A      172.20.15.1
k2       IN      A      172.20.15.1
```