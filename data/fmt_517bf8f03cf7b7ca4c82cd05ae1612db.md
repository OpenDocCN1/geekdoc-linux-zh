
如果我们在域中有一台 Windows 工作站，我们可以使用微软提供的管理工具来管理 DNS 服务器。另一方面，我们也可以通过 `samba-tool dns` 在 Samba 服务器本身上管理 DNS。例如，我们可以列出区域：

```
[root@mike ~]# /usr/local/samba/bin/samba-tool dns zonelist mike.linuxaholics.com -U Administrator
```

Password for [LINUXAHOLICS\Administrator]: 
找到 2 个(区域)

- `pszzoneName` : linuxaholics.com
  `Flags` : DNS_RPC_ZONE_DSINTEGRATED DNS_RPC_ZONE_UPDATE_SECURE
  `ZoneType` : DNS_ZONE_TYPE_PRIMARY
  `Version` : 50
  `dwDpFlags` : DNS_DP_AUTOCREATED DNS_DP_DOMAIN_DEFAULT DNS_DP_ENLISTED
  `pszDpFqdn` : DomainZones.linuxaholics.com
- `pszzoneName` : _mdscs.linuxaholics.com
  `Flags` : DNS_RPC_ZONE_DSINTEGRATED DNS_RPC_ZONE_UPDATE_SECURE
  `ZoneType` : DNS_ZONE_TYPE_PRIMARY
  `Version` : 50
  `dwDpFlags` : DNS_DP_AUTOCREATED DNS_DP_FOREST_DEFAULT DNS_DP_ENLISTED
  `pszDpFqdn` : ForestDZones.linuxaholics.com

我们也可以检查根钩子（root hooks）。

```
[root@mike ~]# /usr/local/samba/bin/samba-tool dns roothints mike.linuxaholics.com -U Administrator --password=Password
Name=Records=13, Children=0
NS: h.root-servers.net. (flags=40000008, serial=0, ttl=0)
NS: f.root-servers.net. (flags=40000008, serial=0, ttl=0)
NS: b.root-servers.net. (flags=40000008, serial=0, ttl=0)
NS: m.root-servers.net. (flags=40000008, serial=0, ttl=0)
NS: l.root-servers.net. (flags=40000008, serial=0, ttl=0)
NS: i.root-servers.net. (flags=40000008, serial=0, ttl=0)
NS: e.root-servers.net. (flags=40000000, serial=0, ttl=0)
NS: d.root-servers.net. (flags=40000000, serial=0, ttl=0)
NS: k.root-servers.net. (flags=40000000, serial=0, ttl=0)
NS: a.root-servers.net. (flags=40000000, serial=0, ttl=0)
NS: g.root-servers.net. (flags=40000000, serial=0, ttl=0)
NS: c.root-servers.net. (flags=40000000, serial=0, ttl=0)
NS: j.root-servers.net. (flags=40000000, serial=0, ttl=0)
Name=h.root-servers.net., Records=1, Children=0
A: 198.79.190.53 (flags=8, serial=0, ttl=0)
Name=f.root-servers.net., Records=1, Children=0
A: 192.5.5.241 (flags=8, serial=0, ttl=0)
Name=b.root-servers.net., Records=1, Children=0
A: 192.228.79.201 (flags=8, serial=0, ttl=0)
Name=m.root-servers.net., Records=1, Children=0
A: 202.12.27.33 (flags=8, serial=0, ttl=0)
Name=l.root-servers.net., Records=1, Children=0
A: 199.79.83.42 (flags=8, serial=0, ttl=0)
Name=i.root-servers.net., Records=1, Children=0
A: 192.36.148.17 (flags=8, serial=0, ttl=0)
Name=e.root-servers.net., Records=1, Children=0
A: 192.203.230.10 (flags=8, serial=0, ttl=0)
Name=d.root-servers.net., Records=1, Children=0
A: 199.79.91.13 (flags=8, serial=0, ttl=0)
Name=k.root-servers.net., Records=1, Children=0
A: 193.0.14.129 (flags=8, serial=0, ttl=0)
Name=a.root-servers.net., Records=1, Children=0
A: 198.41.0.4 (flags=8, serial=0, ttl=0)
Name=g.root-servers.net., Records=1, Children=0
A: 192.112.36.4 (flags=8, serial=0, ttl=0)
Name=c.root-servers.net., Records=1, Children=0
A: 192.33.44.12 (flags=8, serial=0, ttl=0)
Name=j.root-servers.net., Records=1, Children=0
A: 192.58.128.30 (flags=8, serial=0, ttl=0)
```

我们也可以查询名称。

```
[root@mike ~]# /usr/local/samba/bin/samba-tool dns query mike.linuxaholics.com linuxaholics.com ALL -U Administrator --password=Password
Name=Records=1, Children=0
A: 192.168.1.234 (flags=f0, serial=1, ttl=900)
```

```
[root@mike ~]# /usr/local/samba/bin/samba-tool dns query mike.linuxaholics.com linuxaholics.com november ALL -U Administrator --password=Password
Name=Records=1, Children=0
A: 192.168.1.235 (flags=f0, serial=2, ttl=900)
```

此外，我们可以列出区域内的所有记录。

```
[root@mike ~]# /usr/local/samba/bin/samba-tool dns query --additional mike.linuxaholics.com linuxaholics.com ALL -U Administrator --password=Password
Specify either --authority --root along with --additional.
Assuming --authority.
Name=Records=3, Children=0
SOA: serial=2, refresh=900
dwDpFlags : DNS_DP_AUTOCREATED DNS_DP_ENLISTED DNS_DP_DOMAIN_DEFAULT
Name=Records=1, Children=0
A: 192.168.1.234 (flags=f0, serial=1, ttl=900)
Name=Records=1, Children=0
A: 192.168.1.235 (flags=f0, serial=2, ttl=900)
```

### DNS 转发
