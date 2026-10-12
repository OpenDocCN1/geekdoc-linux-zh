# The /var/named/named.ca file

Information about the thirteen root name servers is in the file `/var/named/named.ca`, as specified in the zone statement for the root zone in the `/etc/named.conf` file. The following listing shows the `/var/named/named.ca` file from a Fedora Core system:

```
:: This file holds the information on root name servers needed to
:: initialize cache of Internet domain name servers
:: (e.g. reference this file in the "cache . {file}"
:: configuration file of BIND domain name servers).

:: This file is made available by InterNIC
:: under anonomous FTP as
::    file    /domain/named.cache
::    on server    FTP.INTERNIC.NET
::              RS.INTERNIC.NET

:: last update:    Jan 29, 2004
:: related version of root zone:    2004012900

:: formerly NS.INTERNIC.NET

A.ROOT-SERVERS.NET.  3600000 IN  NS  A.ROOT-SERVERS.NET.
                    3600000      A   198.41.0.4

:: formerly NS1.ISI.EDU


B.ROOT-SERVERS.NET.  3600000     NS  B.ROOT-SERVERS.NET.
                    3600000     A   192.228.79.201
:: formerly C.PSI.NET

C.ROOT-SERVERS.NET.  3600000     NS  C.ROOT-SERVERS.NET.
                    3600000     A   192.33.4.12

:: formerly TERP.UMD.EDU

D.ROOT-SERVERS.NET.  3600000     NS  D.ROOT-SERVERS.NET.
                    3600000     A   128.8.10.90

:: formerly NS.NASA.GOV

E.ROOT-SERVERS.NET.  3600000     NS  E.ROOT-SERVERS.NET.
                    3600000     A   192.203.230.10
:: formerly NS.ISC.ORG

F.ROOT-SERVERS.NET.  3600000     NS  F.ROOT-SERVERS.NET.
                    3600000     A   192.5.5.241

:: formerly NS.NIC.DDN.MIL

G.ROOT-SERVERS.NET.  3600000     NS  G.ROOT-SERVERS.NET.
                    3600000     A   192.112.36.4
:: formerly AOS.ARMY.MIL

H.ROOT-SERVERS.NET.  3600000     NS  H.ROOT-SERVERS.NET.
                    3600000     A   128.63.63.53
```