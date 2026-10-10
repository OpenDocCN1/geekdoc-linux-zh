
## Table 5-1 (continued)

| Type | Name | Description |
| :--- | :--- | :--- |
| MX | Mail Exchanger | Identifies the host that accepts mail meant for a domain (used to route e-mail) |
| NS | Name Server | Identifies authoritative name servers for a zone |
| PTR | Pointer | Specifies the name corresponding to an address (used for reverse mapping — converting an IP address to a host name) |
| RP | Responsible Person | Provides the name of a technical contact for a domain |
| SIG | Signature | Contains data authenticated in the secure DNS (see RFC 2535 for details) |
| SOA | Start of Authority | Indicates that all subsequent records are authoritative for this zone |
| SRV | Services | Lists well-known network services provided by the domain |
| TXT | Text | Used to include comments and other information in the DNS database |

Read the resource records in the zone files, at least the ones of type SOA, NS, A, PTR, and MX, which are some of the most commonly used. (You’ll find the zone files in the /etc/bind directory in Debian and Xandros, the /var/named directory in Fedora Core, and the /var/lib/named directory in SUSE.) Next, I briefly describe these records, illustrating each record type through an example.

A typical SOA record has the following format:

```
@   1D IN SOA     @ root (
                    42      ; serial
                    3h      ; refresh -- 3 hours
                    15m     ; retry -- 15 minutes
                    1w      ; expiry -- 1 week
                    1D )    ; minimum -- 1 day
```

The first field specifies the domain as @, which means the current domain (by default, the zone name, as shown in the /etc/named.conf file). The next field specifies a TTL of one day for this record. The class field is set to IN, which means the record is for Internet. The type field specifies the record type as SOA. The rest of the fields constitute the data for the SOA record. The data includes the name of the primary name server (in this case, @, or the current domain), the e-mail address of the technical contact, and five different times enclosed in parentheses.

The **NS** record specifies the authoritative name servers for a zone. A typical *NS* record looks like the following:

```
. 3600000 IN NS A.ROOT-SERVERS.NET.
```

In this case, the *NS* record lists the authoritative name server for the root zone. (Notice that the name of the first field is a single dot.) The *Time To Live* field specifies that the record is to be valid for 1 000 hours (3600000 seconds). The *class* is *IN*, for Internet; and the *record type* is *NS*. The final field lists the name of the name server (*A.ROOT-SERVERS.NET.*), which ends with a dot.

An *A* record specifies the address corresponding to a name. For example, the following *A* record shows the address of *A.ROOT-SERVERS.NET.*, as *198.41.0.4*:

```
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
```

In this case, the network class isn't specified because the field is optional, and the default is *IN*.

*PTR* records are used for reverse mapping — converting an address to a name. Consider the following example:

```
1 IN PTR localhost.
```

This record comes from a file for a zone named *0.0.127.in-addr.arpa*. Therefore, this record says that the name associated with the address *127.0.0.1* is *localhost*.

An *MX* record specifies the name of a host that accepts mail on behalf of a specific domain. For example, here's a typical *MX* record:

```
naba IN MX 10 mailhub.lnbsfott.com.
```

This record says that mail addressed to the host named *naba* in the current domain is sent to *mailhub.lnbsfott.com*. (This host is called a *mail exchanger*.) The number 10 is the preference value. For a list of multiple *MX* records with different preference values, the ones with lower preference values are tried first.

Armed with this bit of information about resource records, you can go through the zone files for the caching name server.

## The root zone file

Information about the thirteen root name servers is in the zone file referenced in the zone statement for the root zone in the */etc/named.conf* file.

(In Fedora Core the root zone file is /var/named/named.ca, in Debian, MEPIS, Ubuntu, and Xandros it’s /etc/bind/db.root, and in SUSE it’s /var/lib/named/root.hint.) The following listing shows the root zone file:

```
This file holds the information on root name servers needed to
initialize cache of Internet domain name servers
(e.g. reference this file in the "cache . <files>"
configuration file of BIND domain name servers).

This file is made available by InterNIC
under anonymous FTP as
file       /domain/named.cache
on server    FTP.INTERNIC.NET
-OR-         RS.INTERNIC.NET

last update:  Jan 29, 2004
related version of root zone:   2004012900

; formerly NS.INTERNIC.NET

       3600000      IN  NS  A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET.   3600000      A 198.41.0.4

; formerly NS1.ISI.EDU

       3600000      NS  B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET.   3600000      A 192.228.79.201

; formerly C.PSI.NET

       3600000      NS  C.ROOT-SERVERS.NET.
C.ROOT-SERVERS.NET.   3600000      A 192.33.4.12

; formerly TERP.UMD.EDU

       3600000      NS  D.ROOT-SERVERS.NET.
D.ROOT-SERVERS.NET.   3600000      A 128.8.10.90

; formerly NS.NASA.GOV

       3600000      NS  E.ROOT-SERVERS.NET.
E.ROOT-SERVERS.NET.   3600000      A 192.203.230.10

; formerly NS.ISC.ORG

       3600000      NS  F.ROOT-SERVERS.NET.
F.ROOT-SERVERS.NET.   3600000      A 192.5.5.241

; formerly NS.NIC.DDN.MIL

       3600000      NS  G.ROOT-SERVERS.NET.
G.ROOT-SERVERS.NET.   3600000      A 192.112.36.4

; formerly NOS.ARL.ARMY.MIL

       3600000      NS  H.ROOT-SERVERS.NET.
H.ROOT-SERVERS.NET.   3600000      A 128.63.2.53

; formerly NIC.NORDU.NET

.				3600000	NS	I.ROOT-SERVERS.NET.
I.ROOT-SERVERS.NET.	3600000	A	192.36.148.17

; operated by VeriSign, Inc.

.				3600000	NS	J.ROOT-SERVERS.NET.
J.ROOT-SERVERS.NET.	3600000	A	192.58.128.30

; operated by RIPE NCC

				3600000	NS	K.ROOT-SERVERS.NET.
K.ROOT-SERVERS.NET.	3600000	A	193.0.14.129

; operated by ICANN

				3600000	NS	L.ROOT-SERVERS.NET.
L.ROOT-SERVERS.NET.	3600000	A	198.32.64.12

; operated by WIDE

				3600000	NS	M.ROOT-SERVERS.NET.
M.ROOT-SERVERS.NET.	3600000	A	202.12.27.33
; End of File
```

This file contains NS and A resource records that specify the names of authoritative name servers and their addresses for the root zone (indicated by the . in the first field of each NS record).

The comment lines in the file begin with a semicolon. These comments give you hints about the location of the root name servers. There are 13 root name servers for the Internet; most root servers are located in the U.S. This file is a necessity for any name server because the name server has to be able to reach at least one root name server.

## The localhost.zone file

The `/etc/named.conf` file includes a zone statement for the localhost zone that specifies the zone file as `localhost.zone`. That file is located in the `/var/named` directory in Fedora Core, in the `/var/local/named` directory in SUSE, and in `/etc/bind/db.local` in Debian and Xandros. Here’s a listing of what the `localhost.zone` file contains:

```
$TTL	86400
$ORIGIN localhost.
	@		1D IN SOA		@ root (
					42			; serial (d. adams)
					3H			; refresh
					15M			; retry
					1W			; expiry
					1D )			; minimum
	@ IN NS				localhost.
	ID IN A				127.0.0.1
```

## 656 Configuring DNS

This zone file starts with a **$TTL** directive that sets the default TTL (Time To Live) to one day (86400 seconds) for subsequent records with undefined TTLs. Next, a **$ORIGIN** directive sets the domain name to `localhost`.

After these two directives, the `localhost.zone` file contains three resource records (RRs): an SOA record, an NS record, and an **A** record. The SOA and the NS records specify `localhost` as the primary authoritative name server for the zone. The **A** record specifies the address of `localhost` as **127.0.0.1**.

## The zone file for reverse mapping 127.0.0.1

The third zone statement in the `/etc/named.conf` file specifies a reverse-mapping zone named **0.0.127.in-addr.arpa**. For this zone, the zone file is `/var/named/named.local` in Fedora Core, `/var/lib/named/127.0.0.zone` in SUSE, and `/etc/bind/db.127` in Debian, MEPIS, Ubuntu, and Xandros. This zone file contains the following:

```
$TTL          86400
@       IN      SOA     localhost. root.localhost.   (
                                1997022700 ; Serial
                                288000 ; Refresh
                                14400  ; Retry
                                3600000; Expire
                                86400 ) ; Minimum

        IN      NS      localhost.
1       IN      PTR     localhost.
```

The **SOA** and **NS** records specify `localhost` as the primary name server. The **PTR** record specifies `localhost` as the name corresponding to the address **127.0.0.1**.

![](img/792720823146d68f19fd50c99ebfce4b_681_0.png)

The **SOA** record also shows `root.localhost.` as the e-mail address of the technical contact for the domain. Note that the DNS zone files use `user.host.` (notice the ending period) format for the e-mail address. When sending any e-mail to the contact, you have to replace the first dot with an **@** and remove the final dot.

## Caching name server: Startup and test

After you’ve studied the configuration files for the caching name server, you can start the name server and see it in operation.

![](img/792720823146d68f19fd50c99ebfce4b_681_1.png)

To start the name server, log in as **root** and type **`/etc/init.d/named start`** in Fedora Core and SUSE. To ensure that the `named` server starts every time you reboot the system, type **`chkconfig --level 35 named on`** in Fedora Core and SUSE. In Debian, MEPIS, Ubuntu, and Xandros, type **`/etc/init.d/bind9 start`** to start the `named` server.
