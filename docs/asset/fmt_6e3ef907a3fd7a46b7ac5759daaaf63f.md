
接下来，你添加关于本地主机、邮件、FTP 和 Web 服务器的信息。你也可以添加关于网络上每个工作站的信息。

接下来，你设置名为 `tac.rev` 的反向查询区域文件。同样，你需要从所示的 SOA 头开始：

```
@ IN SOA tacech.com. mail.tactech.com. (
20000523 Serial;
Refresh; Retry;
Expire; Minimum TTL;
);
```

接下来，你添加关于你的名称服务器及其地址的信息：

```
NS tactech.com.
PTR p200.tactech.com.
```

如果你按照说明完成了所有操作，那么你的名称服务器应该可以工作了。你对 `/etc/named.conf` 文件做了一些更改，因此在检查你做了什么之前，你需要重启 `named` 守护进程。

## 第 12 章：配置和管理 DNS 服务器

### 检查你的配置

每当你修改 `/etc/named.conf` 时，必须重启 `named` 守护进程。要重启 named，你只需要输入：

```
service named restart
```

在完成主 DNS 服务器的配置后，你可以检查配置以确保其正常工作。你可以使用几种工具进行检查。我将讨论其中两个。当你运行命令时，用你的域名和 IP 地址替换示例内容。`host` 工具可以用于查找域名的 IP 地址。如果你的系统设置正确，你应该获得类似的结果。

```
host tactech.com
; name has 1 address(es)
	 address 192.168.1.1
```

`host` 也可以用于根据 IP 地址查找域名。

```
host -a 192.168.1.1
; reverse has 1 name(s)
	 name main.technology.com.
```

`dig` 也可以用于查询域名的 IP 地址。

```
dig tactech.com

; ANSWER SECTION:
tactech.com.		36000	IN	A	1
```

`dig` 用于调试并获取其他信息。

```
dig tactech.com

; <<>>:
tactech.com. IN A

; ANSWER SECTION:
tactech.com.		36000	IN	A	192.168.1.1

; OPTIONAL SECTION:
tactech.com.		36000	IN	NS	192.168.1.1

; QUERY SECTION:
tactech.com. IN A

; AUTHORITY SECTION:
192.168.1.1.	IN	NS	tactech.com.

; flags: qr ora;
; opcode: 0;
; version: 1;
; flagscount: 4;
; msg size: 65
; query count: 1;
; answer count: 1;
; authority count: 1;
; additional count: 1;
; time: 0 msec
; SERVER: 127.0.0.1#53
```

`dig` 也可以用于反向查找 IP 地址。

```
dig -x 192.168.1.1

; <<>>:
1.168.192.in-addr.arpa. IN PTR

; ANSWER SECTION:
1.168.192.in-addr.arpa.	36000	IN	PTR	main.technology.com.

; OPTIONAL SECTION:
1.168.192.in-addr.arpa.	36000	IN	NS	main.technology.com.

; QUERY SECTION:
1.168.192.in-addr.arpa. IN PTR

; flags: qr ora;
; opcode: 0;
; version: 1;
; flagscount: 4;
; msg size: 65
; query count: 1;
; answer count: 1;
; authority count: 1;
; additional count: 1;
; time: 0 msec
; SERVER: 127.0.0.1#53
```

`dig` 也可以通过 `-t` 选项查询特定的记录类型。

```
dig -t MX tactech.com

; <<>>:
tactech.com. IN MX

; ANSWER SECTION:
tactech.com.		36000	IN	MX	10 main.technology.com.

; OPTIONAL SECTION:
tactech.com.		36000	IN	NS	192.168.1.1

; QUERY SECTION:
tactech.com. IN MX

; flags: qr ora;
; opcode: 0;
; version: 1;
; flagscount: 4;
; msg size: 65
; query count: 1;
; answer count: 1;
; authority count: 1;
; additional count: 1;
; time: 0 msec
; SERVER: 127.0.0.1#53
```

`dig` 也可以用于查询特定的 NS 记录。

```
dig -t NS tactech.com

; <<>>:
tactech.com. IN NS

; ANSWER SECTION:
tactech.com.		36000	IN	NS	192.168.1.1

; OPTIONAL SECTION:
tactech.com.		36000	IN	A	192.168.1.1

; QUERY SECTION:
tactech.com. IN NS

; flags: qr ora;
; opcode: 0;
; version: 1;
; flagscount: 4;
; msg size: 65
; query count: 1;
; answer count: 1;
; authority count: 1;
; additional count: 1;
; time: 0 msec
; SERVER: 127.0.0.1#53
```

`dig` 也可以用于查询特定的 SOA 记录。

```
dig -t SOA tactech.com

; <<>>:
tactech.com. IN SOA

; ANSWER SECTION:
tactech.com.		36000	IN	SOA	tactech.com. mail.tactech.com. 20000523 3600 1800 6048000 3600

; OPTIONAL SECTION:
tactech.com.		36000	IN	NS	192.168.1.1

; QUERY SECTION:
tactech.com. IN SOA

; flags: qr ora;
; opcode: 0;
; version: 1;
; flagscount: 4;
; msg size: 185
; query count: 1;
; answer count: 1;
; authority count: 1;
; additional count: 1;
; time: 0 msec
; SERVER: 127.0.0.1#53
```

`dig` 也可以用于查询特定的 TXT 记录。

```
dig -t TXT tactech.com

; <<>>:
tactech.com. IN TXT

; ANSWER SECTION:
tactech.com.		36000	IN	TXT	"example text"

; OPTIONAL SECTION:
tactech.com.		36000	IN	NS	192.168.1.1

; QUERY SECTION:
tactech.com. IN TXT

; flags: qr ora;
; opcode: 0;
; version: 1;
; flagscount: 4;
; msg size: 75
; query count: 1;
; answer count: 1;
; authority count: 1;
; additional count: 1;
; time: 0 msec
; SERVER: 127.0.0.1#53
```

`dig` 也可以用于查询特定的 CNAME 记录。
