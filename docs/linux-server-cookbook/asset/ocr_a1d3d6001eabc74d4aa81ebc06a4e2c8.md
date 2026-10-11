+   Perform the query to obtain the IP address for www.ubuntu.com. The first query is to obtain the root nameservers, as shown in figure 9.10:

```
```
root@ubuntu:~# dig +trace A www.ubuntu.com

; <<>> DiG 9.18.1-1ubuntu1.1-Ubuntu <<>> +trace A www.ubuntu.com
; global options: +cmd
.			7190	IN	NS	g.root-servers.net.
.			7190	IN	NS	i.root-servers.net.
.			7190	IN	NS	b.root-servers.net.
.			7190	IN	NS	l.root-servers.net.
.			7190	IN	NS	j.root-servers.net.
.			7190	IN	NS	h.root-servers.net.
.			7190	IN	NS	a.root-servers.net.
.			7190	IN	NS	k.root-servers.net.
.			7190	IN	NS	e.root-servers.net.
.			7190	IN	NS	m.root-servers.net.
.			7190	IN	NS	d.root-servers.net.
.			7190	IN	NS	c.root-servers.net.
.			7190	IN	NS	f.root-servers.net.
;; Received 239 bytes from 127.0.0.53#53(127.0.0.53) in 0 ms
```
```

Figure 9.10: Output example for command dig

+   The second part of the output is the output of querying to one of the root nameservers for the name servers specific to the .com TLD. This can be seen in figure 9.11:

```
```
com.			172800	IN	NS	e.gtld-servers.net.
com.			172800	IN	NS	b.gtld-servers.net.
com.			172800	IN	NS	f.gtld-servers.net.
com.			172800	IN	NS	j.gtld-servers.net.
com.			172800	IN	NS	m.gtld-servers.net.
com.			172800	IN	NS	i.gtld-servers.net.
com.			172800	IN	NS	g.gtld-servers.net.
com.			172800	IN	NS	a.gtld-servers.net.
com.			172800	IN	NS	g.gtld-servers.net.
com.			172800	IN	NS	h.gtld-servers.net.
com.			172800	IN	NS	l.gtld-servers.net.
com.			172800	IN	NS	k.gtld-servers.net.
com.			172800	IN	NS	c.gtld-servers.net.
com.			172800	IN	NS	d.gtld-servers.net.
com.			86400	IN	DS	30989 8 2 E2D3C916F6DEAC73294E82
com.			86400	IN	RRSIG	DS 8 1 86400 20220917040000 20220904030000 20826 . n+t2f4RsIC6pIaAYX5UTMBTaqRLXJPOaQMTIyYhuOtxPSZpcZpcZqF1VUIv rthM73 07sj sRN/3gHp80u6R9dZ3JgGj3d9FK473ut0tq0uYks1UC8Lm Z7cOhE/0OqCFuWY3N8ONVvhJ1Czw40 yLBVK6OfIcdYUms1Xu5XDCjq4pIvw 36/A7EZI1FdEVVNK3DBHY66I1LezcjxlFoF1mFU53222muVHEPglImg6A sY hkZXVXuV0mUvUBQuY0hqBeQ20ULwDHVKFfv6g6r6WXLdG1CXC9D2DZVRS rqaq10s88T8FePBnEgBJVfywxFs4a0DnziqQq99pK8IbmFD1AYoIXDPv xnJrjw=
;; Received 1174 bytes from 192.58.128.30#53(j.root-servers.net) in 39 ms
```
```

Figure 9.11: Output example for command dig