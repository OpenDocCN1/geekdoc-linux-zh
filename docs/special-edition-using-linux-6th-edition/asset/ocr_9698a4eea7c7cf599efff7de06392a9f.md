# LISTING 26.2  CONTINUED

```
chown root.root named.root.new
chmod 444 named.root.new
mv named.root.new named.root
ndc restart
echo
echo "The nameserver has been restarted to ensure that the update is complete."
echo "The previous named.root file is now called /var/named/named.root.old."
2>&1 | /usr/lib/sendmail -t
exit 0
```

The line that is of interest to you is the following:

dig

This returns the output that is shown in Listing 26.3.

# LISTING 26.3  DIG LOOKUP OF ROOT SERVERS FROM internic.net

```
;; <<>> DiG 8.1 <<>> @rs.internic.net
; (1 server found)
;; res options: init recurs defnam dnsrch
;; got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 10
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 13, ADDITIONAL: 13
;; QUERY SECTION:
;;    ., type = A, class = IN

;; AUTHORITY SECTION:
.                    5d6h47m12s IN NS D.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS C.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS B.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS A.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS H.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS M.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS L.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS K.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS J.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS G.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS F.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS I.ROOT-SERVERS.NET.
.                    5d6h47m12s IN NS E.ROOT-SERVERS.NET.

;; ADDITIONAL SECTION:
D.ROOT-SERVERS.NET.   5w6d16h IN A    128.8.10.90
C.ROOT-SERVERS.NET.   5w6d16h IN A    192.33.4.12
B.ROOT-SERVERS.NET.   5w6d16h IN A    128.9.0.107
H.ROOT-SERVERS.NET.   5w6d16h IN A    128.63.2.53
A.ROOT-SERVERS.NET.   5w6d16h IN A    198.41.0.4
M.ROOT-SERVERS.NET.   5w6d16h IN A    202.12.27.33
L.ROOT-SERVERS.NET.   5w6d16h IN A    198.32.64.12
K.ROOT-SERVERS.NET.   5w6d16h IN A    193.0.14.129
J.ROOT-SERVERS.NET.   5w6d16h IN A    198.41.0.10
G.ROOT-SERVERS.NET.   5w6d16h IN A    192.112.36.4
F.ROOT-SERVERS.NET.   5w6d16h IN A    192.5.5.241
```