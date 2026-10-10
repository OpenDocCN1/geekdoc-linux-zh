
Although DNS caching can be quite handy, one problem for DNS administrators is that not every DNS server out there honors your TTL. In fact, some ISPs have been known to completely disregard TTLs that are too low, to help reduce the load on their DNS servers. Because of this, even though you may have a TTL of only a few minutes, a DNS change you make may take hours to show up on a DNS server that doesn't obey it.

The easiest way to see the TTL for a zone, outside of viewing it on the DNS server itself, is via the `dig` command:

```bash
$ dig web1.example.net
; <<> DiG 9.7.0-P1 <<> example.net
;; global options: +cmd
;; Got answer:
; ->HEADER<- opcode: QUERY, status: NOERROR, id: 30750
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

; QUESTION SECTION:
;web1.example.net.     IN A

; ANSWER SECTION:
web1.example.net.      300 IN A 10.1.2.5

; AUTHORITY SECTION:
example.net.           300 IN NS ns2.example.net.
example.net.           300 IN NS ns1.example.net.

; ADDITIONAL SECTION:
ns1.example.net.       300 IN A 10.1.1.3
ns2.example.net.       300 IN A 10.1.1.4

; Query time: 2 msec
; SERVER: 192.168.0.1#53(192.168.0.1)
; WHEN: Mon Mar 19 20:48:27 2012
; MSG SIZE rcvd: 118
```

Along with each record `dig` reports back, it also includes the TTL, not just for the main record you requested, but also for any additional information it may return. In this case, the TTLs for all the records happen to be 300 seconds. This tells us that if we make a change to the web1.example.net record, we can expect it to take up to 5 minutes for an ordinary DNS server to return the new record.

Of course, if you have made an update and aren't seeing it, how do you know for sure it's a caching issue and not some other problem? The best way to tell is to identify one of the official name servers for the domain (in the earlier dig output, you see it's ns2.example.net and ns1.example.net). If you aren't sure what name servers are used by a domain, just perform a dig query for the NS records:

```bash
$ dig example.net NS
;; <<> DiG 9.7.0-P1 <>> example.net NS

;; global options: +cmd
;; Got answer:
;; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 38194
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 2

;; QUESTION SECTION:
;example.net.            IN      NS

;; ANSWER SECTION:
example.net.        300   IN      NS      ns1.example.net.
example.net.        300   IN      NS      ns2.example.net.

;; ADDITIONAL SECTION:
ns1.example.net.    300   IN      A       10.1.1.3
ns2.example.net.    300   IN      A       10.1.1.4

;; Query time: 3 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Sat Mar 24 20:44:42 2012
;; MSG SIZE  rcvd: 98
```

Once you have the list of name servers, choose one and query it directly:

```bash
$ dig web1.example.net @10.1.1.4
```

When you query a name server directly, you bypass any caching from your local DNS server and get the current up-to-date record, so if the IP you get from your direct query is still the old IP, you know that the change hasn't propagated to that name server. At that point, query the rest of the name servers in the list directly and see if any of them have the correct record. If you find that none of the DNS servers have the update, you may have a syntax error in your zone file. If some DNS servers have the update and others don't, you might have a zone transfer issue.

If you do find that the name servers do have the correct record but your local DNS server has the old record cached, you have a few recourses. The simplest recourse is to just wait until the local cache expires. Ideally, if you know in advance that you need to make a DNS change and your TTL is long, many DNS administrators lower the TTL a few days before the change so that all DNS servers out there have a chance to pull down the new shorter TTL. Then, once the change goes through, they increase the TTL back to its old value.

If you can't wait until the local cache expires, you can also flush your respective DNS caches. The first cache to flush would be the cache located on your operating system. Yes, even your OS will cache DNS requests so it doesn't have to query your name server every time a record needs to be resolved. On Linux the nscd daemon (if it's installed) handles this caching, so to flush its cache just type:

```bash
$ sudo /etc/init.d/nscd restart
```

If you are on a Windows system, you can open a command prompt and type:

```bash
ipconfig /flushdns
```

On a Mac, you would open a terminal and type:

```bash
lookupd -flushcache
```

or, depending on your version of Mac OS X:

```bash
dscacheutil -flushcache
```

If it's your recursive DNS server that holds the cache, you will need to have administrative access to it to flush its cache. To flush the DNS cache of a BIND name server, you simply restart the service. On Red Hat-based systems this might be:

```bash
$ sudo /etc/init.d/named restart
```

On Debian-based systems the service might be called `bind` or `bind9` instead of `named`. If you don't have the ability to restart your recursive name server, the only alternative is to temporarily replace the name server configured for your system with one that doesn't have the old record cached, or, you could hard-code the IP in your `/etc/hosts` file, but that is a short-sighted fix that I don't recommend.

## Zone Syntax Errors

If you have made a change to a DNS record and notice that the update hasn't made it to any of the name servers for that zone, a likely cause is a syntax error in the zone file. When you make a change to a zone file and then reload BIND, if it notices a syntax error in the file, it will simply disregard any changes to that particular zone file and stick to the records it has. Unless you pay attention to the log files, you may not even realize it happened. If you updated a zone, reloaded the BIND service, and the name server still reports the old record, check `/var/log/syslog` or `/var/log/messages` on your system for error messages from BIND.

Here's an example error message as a result of a syntax error:

```text
Mar 27 21:07:26 ns1 named[25967]: /etc/bind/db.example.net:20: #ns2.example.net: bad owner name (check-names)
Mar 27 21:07:26 ns1 named[25967]: zone example.net/IN: loading from master file /etc/bind/db.example.net failed: bad owner name (check-names)
Mar 27 21:07:26 snowball named[25967]: zone example.net/IN: not loaded due to errors.
```

In this case, the first line in the error message is kind enough to tell me that the error is in line 20 of `/etc/bind/db.example.net`. What happened here is a classic mistake: Almost all configuration files support using `#` to comment out a line except BIND, which uses a semicolon. Instead of using the semicolon to comment out a line in the zone file, the administrator accidentally used `#` and BIND rejected the zone.

## Zone Transfer Issues

The last problem we'll discuss that can cause a DNS change to not take is due to zone transfer issues. In your average DNS infrastructure, one DNS server is treated as the master for a particular zone and the rest are configured as slaves. Any changes are made to the master and then are pushed out to any slaves that are configured. Zone transfer problems can be tricky to detect immediately because your master name server will report the new record; however, any queries to one or more slaves may report the old record. As a result, different clients may see different IP addresses at different times.

The fastest way to identify a zone transfer issue is to perform a direct DNS query using a tool like dig against all of the name servers configured for a zone. If you see that some name servers have the change and others don't, wait a minute or two and try again to see if the changes possibly just took some time to propagate. If after a few minutes the changes still aren't transferred, then the next step is to identify the master DNS server and confirm it has the right records. The master DNS server is configured in a special record called the Start of Authority, or SOA, record. This record lists what is considered to be the authoritative DNS server for the zone and, like with other dig requests for specific record types, simply query the domain and add SOA to the end of the query:

```bash
$ dig example.net SOA

; <<> DiG 9.7.0-P1 <<> example.net SOA
; ; global options: +cmd
; ; Got answer:
; ; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 62609
; ; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

; ; QUESTION SECTION:
; example.net.			IN	SOA

; ; ANSWER SECTION:
example.net.			300	IN	SOA	ml.example.net. admin.example.net.
	2011062300 10800 2000 604800 7200
```
