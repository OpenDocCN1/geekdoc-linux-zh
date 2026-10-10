
# 第 25 章：通过 DNS 使服务器公网 975

```
    2007042701 ; Serial

    28800 ; Refresh

    14400 ; Retry

    360000 ; Expire

    86400 ) Minimum

; Name servers IN NS ns1.yourdomain.com.

    IN NS ns2.yourdomain.com.

; Mail server for domain IN MX 10.yourdomain.com.

; Public servers

ns1 IN A 10.0.0.1

ns2 IN A 10.0.0.2

mail IN A 123.45.67.2

www IN A 123.45.67.3

ftp IN A 123.45.67.4

; Private clients on the LAN

red IN A 10.0.0.2

blue IN A 10.0.0.3

green IN A 10.0.0.4

yellow IN A 10.0.0.5
```

“内部” `yourdomain.com` 的区域文件包含了有关该区域信息的资源记录。你的 DNS 服务器使用 `TTL`（生存时间）告诉存储你为该域提供信息的名称服务器，它们在丢弃信息并获取新信息之前可以保留这些信息多久。第一个值是整个区域的默认值，时间单位为秒。

“外部”视图的 `yourdomain.com` 外部文件包含了你想要公开的域内任何计算机的名称和 IP 地址（排除了私有局域网上的计算机）。该域外部视图的 DNS 从用服务器是 `123.45.67.2`。

注意，每个区域都指向 `named` 目录下的区域文件。表 25-1 显示了 `named` 目录中每个区域指向哪个文件。

`/var/named/chroot/var/named` 目录包含 `/var/named/chroot/etc/named.conf` 文件指向的区域文件。对于该示例，你只需要从头创建三个区域文件。你可以（或应该）保持 `named.ca` 文件在线。

域名服务器的大部分实际工作发生在区域文件中。在示例中，`db.yourdomain.com.inside` 文件包含了 `yourdomain.com` 域的基本记录，包括所有私有名称和地址。

## 查询示例

```
;; Query time: 24 msec

;; SERVER: 10.0.0.1#53(10.0.0.1)

;; WHEN: Mon Oct 9 02:12:32 2007

;; MSG SIZE rcvd: 129
```

`dig` 输出中的章节包含查询部分（question section）和权威部分（authority section）。结果显示了与你查询的域名相关的名称服务器分配和地址。`nlookup` 命令是另一个你可以用来查找域名信息的工具。在下面的示例中，`nlookup` 查找解析 `ftp.yourdomain.com` 的服务器：

```
# nlookup -sil ftp.yourdomain.com

Server:

  123.45.67.1

Address:

  123.45.67.1#53
```

```
Name: ftp.yourdomain.com

Address: 123.45.67.4
```

`nlookup` 命令的输出包含了响应请求的计算机名称及其 IP 地址，以及你请求的计算机的名称和地址。`-sil` 选项可以防止 `nlookup` 可能在 Fedora（以及 RHEL）中显示的消息。尝试使用 IP 地址（如 `10.0.0.1`）运行 `nlookup` 以确保反向查找正常。

要检查运行在你的本地系统上的名称服务器状态，请使用启动 `named` 的相同脚本。输入以下命令检查你的 DNS 守护进程状态：

```
# /etc/init.d/named status

number of zones: 5

debug level: 0

xfers running: 0

xfers deferred: 0

soa queries in progress: 0

query logging is OFF

recursive clients: 0/1000

tcp clients: 0/100

server is up and running
```
