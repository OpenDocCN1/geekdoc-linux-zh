
The options section is where to specify the directory in which named should look for zone files (as named in other sections of the file). You learn about using other options in later examples in this chapter.

Next, we instruct named to accept commands from an authenticated rndc. We include the key file, /etc/rndc.key, and the controls section saying that rndc connects from localhost and uses the specified key. (You can specify more than one IP address in the allow list or use an access control list as described in the “Managing DNS Security” section, later in this chapter.)

The . zone tells named about the root nameservers with names and addresses in the root.hints file. This information determines which root nameserver is initially consulted, although this decision is frequently revised based on the server’s response time. Although the hints file can be obtained via FTP, the recommended, network-friendly way to keep it synchronized is to use dig. We ask a root nameserver (it doesn’t matter which one) for the NS records of . and use the dig output directly:

```
# dig @j.root-servers.net. ns > /var/named/root.hints
# cat /var/named/root.hints
;; <<> Dig 8.2 <<> @j.root-servers.net . ns
;; (1 server found)
;; res options: init recurs defnam dnsrch
;; got answer:
;; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 6
;; flags: qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13
;;
; QUERY SECTION:
;; , type = NS, class = IN
;
;
; ANSWER SECTION:
.			6d IN NS	H.ROOT-SERVERS.NET.
.			6d IN NS	C.ROOT-SERVERS.NET.
.			6d IN NS	G.ROOT-SERVERS.NET.
.			6d IN NS	F.ROOT-SERVERS.NET.
.			6d IN NS	B.ROOT-SERVERS.NET.
.			6d IN NS	J.ROOT-SERVERS.NET.
.			6d IN NS	K.ROOT-SERVERS.NET.
.			6d IN NS	L.ROOT-SERVERS.NET.
.			6d IN NS	M.ROOT-SERVERS.NET.
.			6d IN NS	I.ROOT-SERVERS.NET.
.			6d IN NS	E.ROOT-SERVERS.NET.
.			6d IN NS	D.ROOT-SERVERS.NET.
.			6d IN NS	A.ROOT-SERVERS.NET.
;
;; ADDITIONAL SECTION:
H.ROOT-SERVERS.NET.		5w6d16h IN A	128.63.2.53
C.ROOT-SERVERS.NET.		5w6d16h IN A	192.33.4.12
G.ROOT-SERVERS.NET.		5w6d16h IN A	192.112.36.4
F.ROOT-SERVERS.NET.      5w6d16h IN A    192.5.5.241
B.ROOT-SERVERS.NET.      5w6d16h IN A    128.9.0.107
J.ROOT-SERVERS.NET.      5w6d16h IN A    198.41.0.10
K.ROOT-SERVERS.NET.      193.0.14.129
L.ROOT-SERVERS.NET.      198.32.64.12
M.ROOT-SERVERS.NET.      202.12.27.33
I.ROOT-SERVERS.NET.      192.36.148.17
E.ROOT-SERVERS.NET.      192.203.230.10
D.ROOT-SERVERS.NET.      128.8.10.90
A.ROOT-SERVERS.NET.      198.41.0.4
;
;; Total query time: 4489 msec
;; FROM: lustre to SERVER: j.root-servers.net 198.41.0.10
;; WHEN: Mon Sep 10 04:18:26 2001
;; MSG SIZE  sent: 17  rcvd: 436
```

## The Zone File

The zone 0.0.127.in-addr.arpa section in named.conf says that we are a master name-server for that zone and that the zone data is in the file 127.0.0. Before examining the first real zone file in detail, look at the general format of a RR specification:

```
name TTL class type data
```

Here, name is the DNS name with which this record is associated. In a zone file, names ending with a . are fully qualified, whereas others are relative to the name of the zone. In the zone example.com, foo refers to the fully qualified name foo.example.com. The special name @ is a short form for the name of the zone itself. If the name is omitted, the last specified name is used again.

The TTL (Time To Live) field is a number that specifies the time for which the record can be cached. This is explained in greater detail in the discussion of the SOA record in the next section. If this field is omitted, the default TTL for the zone is assumed. TTL values are usually in seconds, but you can append an m for minutes, h for hours, or d for days.

BIND supports different record classes, but for all practical purposes, the only important class is IN, for Internet. If no class is explicitly specified, a default value of IN is assumed; to save a little typing, we do not mention the class in any of the zone files we write here.

The type field is mandatory and names the RR in use, such as A, NS, MX, or SOA. (We use only a few of the existing RRs here. Consult the DNS standards for a complete list.)

The data field (or fields) contains data specific to this type of record. The appropriate syntax will be introduced as we examine the use of each RR in turn.

Here is the zone file for the `0.0.127.in-addr.arpa` zone:

```
$TTL	2D
@	SOA	localhost. hostmaster.example.com. (
		2001090101	; Serial
		24h		; Refresh
		2h		; Retry
		3600000	; Expire (1000h)
		1h)		; Minimum TTL
	NS	localhost.
1	PTR	localhost.
```

The $TTL directive that should begin every zone file sets the default minimum time to live for the zone to two days. This is discussed further in the next section.

### The Zone File's SOA Record

The second line in the zone file uses the special @ name that you saw earlier. Here, it stands for `0.0.127.in-addr.arpa`, to which the SOA (*Start of Authority*) record belongs. The rest of the fields (continued until the closing parenthesis) contain SOA-specific data.

The first data field in the SOA record is the fully qualified name of the master nameserver for the domain. The second field is the email address of the contact person for the zone. Replacing the @ sign with a . writes it as a DNS name; foo@example.com would be written as `foo.example.com` (note the trailing .).

Do not use an address such as a.b@example.com because it is written as `a.b.example.com` and will later be misinterpreted as `a@b.example.com`.

![](img/34e72348d53ca54c2a1d9c871316691b_559_0.png)

The next several numeric fields specify various characteristics of this zone. These values must be correctly configured, and to do so, you must understand each field. As shown in the comments (note that zone file comments are not like in the same syntax as `named.conf` comments), the fields are serial number, refresh interval, retry time, expire period, and minimum TTL.

Serial numbers are 32-bit quantities that can hold values between 0 and 4,294,967,295 (2^32 − 1). Every time the zone file is changed, the serial number must be incremented. This change serves as a signal to slaves that they need to transfer the contents of the zone again. It is conventional to assign serial numbers in the format `YYYYMMDDnn`, that is, the date of the change and a two-digit revision number (for example, 2007060101). For changes made on the same day, you increment only the revision. This reasonably assumes that you make no more than 99 changes to a zone in one day. For changes on the next day, the date is changed and the revision number starts from 01 again.

The refresh interval specifies how often a slave server should check whether the master data has been updated. It has been set to 24 hours here, but if the zone changes often, the value should be lower. Slaves can reload the zone much sooner if both they and the master support the DNS NOTIFY mechanism, and most DNS software does.

The retry time is relevant only when a slave fails to contact the master after the refresh time has elapsed. It specifies how long it should wait before trying again. (It is set to two hours here.) If the slave is consistently unable to contact the master for the length of the expire period (usually because of some catastrophic failure), it discards the zone data it already has and stops answering queries for the zone. Thus, the expire period should be long enough to allow for the recovery of the master nameserver. It has been repeatedly shown that a value of one or two weeks is too short. One thousand hours (about six weeks) is accepted as a good default.

As you read earlier, every RR has a TTL field that specifies how long it can be cached before the origin of the data must be consulted again. If the RR definition does not explicitly specify a TTL value, the default TTL (set by the $TTL directive) is used instead. This enables individual RRs to override the default TTL value as required.

The SOA TTL, the last numeric field in the SOA record, is used to determine how long negative responses (NXDOMAIN) should be cached. (That is, if a query results in an NXDOMAIN response, that fact is cached for as long as indicated by the SOA TTL.) Older versions of BIND used the SOA minimum TTL to set the default TTL, but BIND 9 no longer does so. The default TTL of 2 (two days) and SOA TTL of 1 (one hour) are recommended for cache friendliness.

The values used previously are good defaults for zones that do not change often. You might have to adjust them a bit for zones with different requirements. In that case, the website at http://www.ripe.net/docs/ripe-203.html is recommended reading.

### The Zone File’s Other Records

The next two lines in the zone file create NS and PTR records. The NS record has no explicit name specified, so it uses the last one, which is the @ of the SOA record. Thus, the nameserver for 0.0.127.in-addr.arpa is defined to be localhost.

The PTR record has the name 1, which becomes 1.0.0.127.in-addr.arpa (which is how you write the address 127.0.0.1 as a DNS name). When qualified, the PTR record name 1 becomes localhost. (You will see some of the numerous other RR types later when we configure our nameserver to be authoritative for a real domain.)
