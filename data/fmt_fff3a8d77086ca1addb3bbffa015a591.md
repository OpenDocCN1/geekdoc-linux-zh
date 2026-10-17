
### • 权威反向查询 (1): `/var/named/named.196.28.144`

```
IN      NS      ns1.cranzgot.co.za.
1       PTR     pcl1.cranzgot.co.za.
2       PTR     pcl2.cranzgot.co.za.
3       PTR     pcl3.cranzgot.co.za.
4       PTR     pcl4.cranzgot.co.za.
; 依此类推... 到 255
```

### • 权威反向查询 (1): `/var/named/named.196.28.144`

```
$TTL 259200
IN      SOA     ns1.cranzgot.co.za. dns-admin.ns1.cranzgot.co.za. (
        2000012101      ; 序列号
        10800           ; 每 3 小时刷新一次
        3600            ; 每小时重试一次
        604000          ; 42 天后过期
        259200          ; 3 天的最小生存时间 (TTL)
```

```
IN      NS      dns.big-isp.net.
0       IN      NS      dns.big-isp.net.
1       IN      NS      dns.big-isp.net.
2       IN      NS      dns.big-isp.net.
3       IN      NS      dns.big-isp.net.
4       IN      NS      dns.big-isp.net.
5       IN      NS      dns.big-isp.net.
6       IN      NS      dns.big-isp.net.
7       IN      NS      dns.big-isp.net.
```

| | | | |
|---|---|---|---|
| `8` | `IN` | `NS` | `dns.big-isp.net` |
| `9` | `IN` | `NS` | `dns.big-isp.net` |
| `10` | `IN` | `NS` | `dns.big-isp.net` |
| `11` | `IN` | `NS` | `dns.big-isp.net` |
| `12` | `IN` | `NS` | `dns.big-isp.net` |
| `13` | `IN` | `NS` | `dns.big-isp.net` |
| `14` | `IN` | `NS` | `dns.big-isp.net` |
| `15` | `IN` | `NS` | `dns.big-isp.net` |
| `16` | `IN` | `PTR` | `nsl1.crzangot.co.za` |
| `17` | `IN` | `PTR` | `ftp.crzangot.co.za` |
| `18` | `IN` | `PTR` | `unused18.crzangot.co.za` |
| `19` | `IN` | `PTR` | `unused19.crzangot.co.za` |
| `20` | `IN` | `PTR` | `unused20.crzangot.co.za` |
| `21` | `IN` | `PTR` | `unused21.crzangot.co.za` |
| `22` | `IN` | `PTR` | `unused22.crzangot.co.za` |
| `23` | `IN` | `PTR` | `unused23.crzangot.co.za` |
| `24` | `IN` | `NS` | `dns.big-isp.net` |
| `25` | `IN` | `NS` | `dns.big-isp.net` |
| `26` | `IN` | `NS` | `dns.big-isp.net` |

### 权威反向查询 (2): `/var/named/named.196.28.144`

```
$TTL 259200
IN      SOA     ns1.cranzgot.co.za. dns-admin.ns1.cranzgot.co.za. (
        2000012101      ; 序列号
        10800           ; 每 3 小时刷新一次
        3600            ; 每小时重试一次
        604000          ; 42 天后过期
        259200          ; 3 天的最小生存时间 (TTL)
```

```
IN      NS      ns1.cranzgot.co.za.
1       PTR     pcl1.cranzgot.co.za.
2       PTR     pcl2.cranzgot.co.za.
3       PTR     pcl3.cranzgot.co.za.
4       PTR     pcl4.cranzgot.co.za.
```

[译文：]

## 40.2. 配置 `bind`

```
; 供未来 Web 服务器预留：
unused18      IN      A       196.28.144.18
unused19      IN      A       196.28.144.19
unused20      IN      A       196.28.144.20
unused21      IN      A       196.28.144.21
unused22      IN      A       196.28.144.22
unused23      IN      A       196.28.144.23
```

```
; 本地域网 LAN:
pcl1           IN      A       192.28.2.1
pcl2           IN      A       192.28.2.2
pcl3           IN      A       192.28.2.3
pcl4           IN      A       192.28.2.4
; 依此类推... 到 192.28.2.255
```

### • 域网反向查询：`/var/named/named.196.28.2`

```
$TTL 259200
IN      SOA     ns1.cranzgot.co.za. dns-admin.ns1.cranzgot.co.za. (
        2000012101      ; 序列号
        10800           ; 每 3 小时刷新一次
        3600            ; 每小时重试一次
        604000          ; 42 天后过期
        259200          ; 3 天的最小生存时间 (TTL)
```

```
IN      NS      ns1.cranzgot.co.za.
1       PTR     pcl1.cranzgot.co.za.
2       PTR     pcl2.cranzgot.co.za.
3       PTR     pcl3.cranzgot.co.za.
4       PTR     pcl4.cranzgot.co.za.
; 依此类推... 到 255
```

### • 权威反向查询 (1): `/var/named/named.196.28.144`

```
$TTL 259200
IN      SOA     ns1.cranzgot.co.za. dns-admin.ns1.cranzgot.co.za. (
        2000012101      ; 序列号
        10800           ; 每 3 小时刷新一次
        3600            ; 每小时重试一次
        604000          ; 42 天后过期
        259200          ; 3 天的最小生存时间 (TTL)
```

```
IN      NS      dns.big-isp.net.
0       IN      NS      dns.big-isp.net.
1       IN      NS      dns.big-isp.net.
2       IN      NS      dns.big-isp.net.
3       IN      NS      dns.big-isp.net.
4       IN      NS      dns.big-isp.net.
5       IN      NS      dns.big-isp.net.
6       IN      NS      dns.big-isp.net.
7       IN      NS      dns.big-isp.net.
```

| | | | |
|---|---|---|---|
| `8` | `IN` | `NS` | `dns.big-isp.net` |
| `9` | `IN` | `NS` | `dns.big-isp.net` |
