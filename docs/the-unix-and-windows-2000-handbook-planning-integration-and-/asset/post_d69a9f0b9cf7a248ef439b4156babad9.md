
.                       3600000  IN  NS  A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET.      3600000  A    198.41.0.4
;
; formerly NS1.ISI.EDU
;
.                       3600000  NS  B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET.      3600000  A    128.9.0.107
;
; formerly C.PSI.NET
;
.                       3600000  NS  C.ROOT-SERVERS.NET.
C.ROOT-SERVERS.NET.      3600000  A    192.33.4.12
;
; formerly TERP.UMD.EDU
;
.                       3600000  NS  D.ROOT-SERVERS.NET.
D.ROOT-SERVERS.NET.      3600000  A    128.8.10.90
;
; formerly NS.NASA.GOV
;
.                       3600000  NS  E.ROOT-SERVERS.NET.
E.ROOT-SERVERS.NET.      3600000  A    192.203.230.10
;
; formerly NS.ISC.ORG
;
.                       3600000  NS  F.ROOT-SERVERS.NET.
F.ROOT-SERVERS.NET.      3600000      A      192.5.5.241
;
; formerly NS.NIC.DDN.MIL
;
.                          3600000      NS      G.ROOT-SERVERS.NET.
G.ROOT-SERVERS.NET.      3600000      A      192.112.36.4
;
; formerly AOS.ARL.ARMY.MIL
;
.                          3600000      NS      H.ROOT-SERVERS.NET.
H.ROOT-SERVERS.NET.      3600000      A      128.63.2.53
;
; formerly NIC.NORDU.NET
;
.                          3600000      NS      I.ROOT-SERVERS.NET.
I.ROOT-SERVERS.NET.      3600000      A      192.36.148.17
;
;
; temporarily housed at NSI (InterNIC)
;
.                          3600000      NS      J.ROOT-SERVERS.NET.
J.ROOT-SERVERS.NET.      3600000      A      198.41.0.10
;
; housed in LINX, operated by RIPE NCC
;
.                          3600000      NS      K.ROOT-SERVERS.NET.
K.ROOT-SERVERS.NET.      3600000      A      193.0.14.129
;
; temporarily housed at ISI (IANA)

. 3600000 NS L.ROOT-SERVERS.NET.
L.ROOT-SERVERS.NET. 3600000 A 198.32.64.12

; temporarily housed at ISI (IANA)

. 3600000 NS M.ROOT-SERVERS.NET.
M.ROOT-SERVERS.NET. 3600000 A 198.32.65.12

; End of File

The cache file is available for ftp from ftp.rs.internic.net through anonymous FTP. You should grab this file on a regular basis. Even though it may change infrequently, you want to always have the latest version. This list of name servers is stored upon initialization of named, and never discarded or reloaded. In older versions of bind, this data was truly cache data, and was reloaded over the Internet after some very long interval. The largest timeout value available was 9999999, which is a very long time. Once named was rewritten to make the cache data static, timeouts were no longer necessary. Somewhere along the line, the timeout value of 3600000 was introduced. Feel free to make up your own story as to what this number means, as its true meaning has been lost to antiquity.

## The DNS Configuration File

Up to this point, there were no differences between the BIND version 4 and 8 instances of DNS. While BIND 8 has many new features, for our discussion, the only major difference is the configuration file that named reads during initialization. In BIND 4, the configuration file was /etc/named.boot, while in BIND 8, the initial configuration file is /etc/named.conf. We'll start by investigating the BIND 4 /etc/named.boot file.

; BIND 4 named.boot

```
directory /var/named
```

```
cache                 db.cache

;

; type        domain                  source host/file
;

primary              0.0.127.in-addr.arpa          db.0.0.127.in-addr.arpa

;

; domain maps
;

primary              sniglets.com                  db.sniglets
primary              3.168.192.in-addr.arpa        db.3.168.192.in-addr.arpa
:end of named.boot
```

The directory directive tells named to look in the directory /var/named for data files. The cache directive defines the cache file, in this instance, /var/named/db.cache. The primary directives tell named that it is the authoritative server for the following domains. In this case, named is the authoritative server for the loopback address, as well as for the domain sniglets.com (with data file /var/named/db.sniglets) and the class B network 192.168.3 (with data file db.3.168.192.in-addr.arpa). This is all the necessary information you need to configure BIND 4 and to run.

Now, if we compare the BIND 4 /etc/named.boot file to the BIND 8 /etc/named.conf file, at first we realize that the form is drastically different. However, once you take a moment to analyze the named.conf file, you realize that the information is the same, just the directives are different.

```
; BIND 8 named.conf

;

options {

        directory "/var/named";

};
```
