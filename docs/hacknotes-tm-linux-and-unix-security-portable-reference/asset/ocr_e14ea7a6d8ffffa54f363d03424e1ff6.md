# Performing DNS Reverse-Lookups

Reverse-lookups can be performed by using the host command:

```
host 10.0.0.3
```

3.0.0.10.in-addr.arpa domain name pointer
comp13-payrollftfpd.somecompanyasanexample.com.

Not only does this query result tell us that the host is probably running an FTP server, it also informs us of its location, room 13!

# Prevent DNS Reverse-Lookup Information Exposures

As evident from the preceding example, DNS reverse-lookups can reveal various host information that should not be available to external users. The following preventative measures can be taken to minimize the exposure of such information:

+   - Do not assign hostnames that may reveal any sort of information about the hosts on your network.

+   - Consider assigning hostnames that include the IP address as part of the hostname, such as 3-0-0-10.somecompanyasanexample .com. This scheme helps organize the available hosts from an administrative perspective, and at the same time reveals no extra information to an external entity.

# MAIL EXCHANGE

To find out the hostnames and IP addresses of an organization’s mail servers, the command-line dig tool can be used to query for a domain’s Mail Exchange (MX) Records:

```
[bash]$ dig mx somecompanyasanexample.com
; <<>> DiG 9.2.1 <<>> mx dhanjani.com
;; global options: printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 1234
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

;; QUESTION SECTION:
;somecompanyasanexample.com.        IN      MX

;; ANSWER SECTION:
somecompanyasanexample.com.    86400    IN      MX      10
mail.somecompanyasanexample.com.
```