```
L.ROOT-SERVERS.NET.  5w6d16h IN A  198.32.64.12
M.ROOT-SERVERS.NET.  5w6d16h IN A  202.12.27.33
A.ROOT-SERVERS.NET.  5w6d16h IN A  198.41.0.4
H.ROOT-SERVERS.NET.  5w6d16h IN A  128.63.2.53
B.ROOT-SERVERS.NET.  5w6d16h IN A  128.9.0.107
C.ROOT-SERVERS.NET.  5w6d16h IN A  192.33.4.12
D.ROOT-SERVERS.NET.  5w6d16h IN A  128.8.10.90
E.ROOT-SERVERS.NET.  5w6d16h IN A  192.203.230.10
F.ROOT-SERVERS.NET.  5w6d16h IN A  192.5.5.241
I.ROOT-SERVERS.NET.  5w6d16h IN A  192.36.148.17
```

+   - **foo.edu:** This is the master zone for the foo.edu domain. This indicates that this name server is the primary master for the foo.edu domain and that it can find the zone definition in the file `/var/named/zone.foo.edu`.
+   - **1.168.192.in-addr.arpa:** This is the master zone for reverse name lookups for the foo.edu domain. The zone information is contained in the file `/var/named/zone.192.168.1` and specifies the hostnames corresponding to specific IP addresses.
+   - **0.0.127.in-addr.arpa:** This indicates that the server is the primary master server for reverse name lookups for the local loopback network 127.0.0. This information is not relevant to the Internet but it allows reverse name lookups for the local system. The zone information is stored in the file `/var/named/zone.127.0.0`.

# CREATING ZONE FILES

After named.conf is configured, you must create the zone files indicated in the configuration. In particular, the three files zone.foo.edu, zone.192.168.1, and zone.127.0.0 must be created in the directory /var/named.

The zone file for the foo.edu (zone.foo.edu) domain illustrates a typical zone file on a primary master server for an Internet-registered domain name:

```
; zone.foo.edu file
;
@       IN      SOA     fake.foo.edu.    hostmaster.foo.edu. (
                                1999042800      ;Serial
                                8H              ;Refresh
                                2H              ;Retry
                                1W              ;Expire
                                1D              ;Minimum
;
; Name-servers
;
                IN      NS      fake.foo.edu.
;
; Addresses for canonical names
;
fake            IN      A       192.168.1.1
pinky           IN      A       192.168.1.2
brain           IN      A       192.168.1.3
www             IN      CNAME   brain.foo.edu.
;
; Mail exchangers
;
foo.edu.        IN      MX      10 mail.foo.edu.
```