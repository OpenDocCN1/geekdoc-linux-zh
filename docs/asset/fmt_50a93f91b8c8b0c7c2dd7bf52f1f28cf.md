
# 日志记录
日志记录由 `Logging` 部分开启。此部分打开了两个日志通道：一个将信息记录到 `/var/log/bind/misc.log`，另一个将信息记录到 `/var/log/bind/query.log`。当其中一个日志增长到 4 兆字节（文件语句中的 `size 4m`）时，它会通过在其文件名后追加 `.1` 进行重命名，并启动一个新的日志。其他类似命名的日志末尾的数字会递增。任何编号大于 `versions` 子句指定值的日志（示例中为 `4`）都会被删除。有关维护日志文件的另一种方法，请参阅 `logrotate`（第 579 页）。`print` 语句确定信息的时间、严重性和类别是否发送到日志；每个选项指定为 `YES` 或 `NO`。类别确定什么信息会被记录到该通道。在示例中，默认信息被发送到 `misc` 通道，查询被发送到 `query` 通道。更多选项请参阅 `named.conf` 手册页。

# named.local
反向区域文件 `named.local` 的起始（origin）是 `0.168.192.in-addr.arpa`（如 `named.conf` 中引用此文件的 `Zone` 部分所指定）。在 `SOA` 和 `NS` 资源记录之后，前三个 `PTR` 资源记录分别将子网 `0.168.192.in-addr.arpa`（即 `192.168.0.1`）中的地址 `1` 与名称 `gw.sam.net.`、`www.sam.net.` 和 `ftp.sam.net.` 对应起来。接下来的三个 `PTR` 资源记录将 `192.168.0.3` 对应为 `mark.sam.net.`，`192.168.0.4` 对应为 `mail.sam.net.`，`192.168.0.6` 对应为 `ns.sam.net.`。

```
$ cat named.local
;	zone "0.168.192.in-addr.arpa"
;
$TTL		3D
	@		IN	SOA	ns.sam.net.	mgs@sobel11.com. {
						;	serial
						2005110501
						;	refresh
						8h
						;	retry
						2h
						;	expire
						4w
						;	minimum
						1D)

		IN		NS	ns.sam.net.
1		IN		PTR	gw.sam.net.
1		IN		PTR	www.sam.net.
1		IN		PTR	ftp.sam.net.
3		IN		PTR	mark.sam.net.
4		IN		PTR	mail.sam.net.
6		IN		PTR	ns.sam.net.
```

# sam.net
`sam.net` 的区域文件利用了 `BIND` 的许多功能，并包含 `TXT`（第 782 页）、`CNAME`（第 780 页）和 `MX`（第 780 页）资源记录。当您查询资源记录时，`named` 会返回 `TXT` 资源记录以及您请求的记录。两条 `NS` 记录中的第一条指定了一个非限定名称（`ns`），`BIND` 会为其追加区域名称（`sam.net`），生成完整限定域名（FQDN）为 `ns.sam.net`。第二个域名服务器是通过 `BIND` 不修改的 `FQDN` 名称指定的。`MX` 记录以类似的方式指定邮件服务器，并在数据字段的开头包含一个优先级数字；较小的数字表示优先服务器。

```
$ cat sam.net
; zone "sam.net"
;
$TTL 3D
@       IN      SOA     ns.sam.net. mgs@sobell.com. (
                200511051 ; serial
                8H        ; refresh
                2H        ; retry
                4W        ; expire
                1D )    ; minimum

        TXT     "Sobel1 Associates Inc.";
        NS      ns        ; Nameserver address (unqualified)
        NS      ns.max.net.; Nameserver address (qualified)
        MX      10 mail   ; Mail exchange (primary/unqualified)
        MX      20 mail.max.net.; Mail exchange (2nd/qualified)

localhost IN    A       127.0.0.1

www       IN      CNAME   ns
ftp       IN      CNAME   ns

gw        IN      A       192.168.0.1
        TXT     "Router"

ns        IN      A       192.168.0.6
        MX      10 mail
        MX      20 mail.max.net.

mark      IN      A       192.168.0.3
        MX      10 mail
        MX      20 mail.max.net.
        TXT     "MGS"

mail      IN      A       192.168.0.4
        MX      10 mail
        MX      20 mail.max.net.
```

某些资源记录在名称（Name）字段中有一个值；那些没有名称的资源记录会从上一个资源记录继承名称。类似地，上一个资源记录可能也有继承的名称值，以此类推。`SOA` 资源记录之后的五个资源记录从 `SOA` 资源记录继承 `@`，即区域名称。这些资源记录与整个区域相关。在上面的示例中，第一个 `TXT` 资源记录从其名称从 `SOA` 资源记录继承；它是 `sam.net` 区域的 `TXT` 资源记录（执行命令 `host -t TXT sam.net` 可以显示该 `TXT` 资源记录）。

在这五个资源记录之后，是属于区域内某个域名的资源记录。例如，在 Name 字段设置为 `mark` 的 `A` 资源记录之后的 `MX` 资源记录，是 `mark.sam.net.` 域名的资源记录。

`localhost` 的 `A` 资源记录后面跟着两条 `CNAME` 资源记录，它们指定 `www.sam.net.` 和 `ftp.sam.net.` 作为名称服务器 `ns.sam.net.` 的别名。例如，连接到 `ftp.sam.net` 的用户将连接到 `192.168.0.6`。名为 `gw`、`ns`、`mark` 和 `mail` 的资源记录是 `sam.net` 区域内域名的资源记录。

### 日志文件
在重启 `named` 之前，创建日志文件的目录，并如下所示为其设置权限和所有者。如果你正在 `chroot` 容器中运行 `named`，请在 `/var/named/chroot/var/log` 中创建 `bind` 目录。

```bash
# mkdir /var/log/bind
# chmod 744 /var/log/bind
# chown named /var/log/bind
# ls -ld /var/log/bind
drwx--r-- 2 named root 4096 Nov 5 19:41 /var/log/bind
```

放置好日志目录后，`/etc` 中的 `named.conf`（如果你正在 `chroot` 容器中运行 `named`，则在 `/var/named/chroot/etc` 中），以及 `/var/named` 中的 `named.ca`、`named.local` 和 `sam.net` 区域文件（如果你正在 `chroot` 容器中运行 `named`，则在 `/var/named/chroot/var/named` 中），重启 `named` 并检查日志文件。`/var/log/messages` 文件应显示类似以下内容：
