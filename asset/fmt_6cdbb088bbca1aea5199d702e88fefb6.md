
- 将主、从 DNS 服务器（`ns1` 和 `ns2`）的地址更改为 `123.45.67.1` 和 `123.45.67.2`。通过这种，公众只能看到名称服务器的公共地址。（当然，你需要使用自己的 IP 地址来代替 `123.45.67.1` 和 `123.45.67.2`）。

## 设置区域文件（反向查找）

示例中的另一个新文件是 `yourlan.db` 文件，它包含了对局域网内计算机执行反向 IP 查询所需的信息。以下是一个示例：

```
TTL    86400
IN      SOA nsl.yourdomain.com hostmaster.yourdomain.com. (
                2006042701 : Serial
                28800 : Refresh
                0 : Retry
                360000 : Expire
                86400 ) : Minimum
IN      NS    nsl.yourdomain.com.
IN      PTR yourdomain.com.
IN      PTR red.
IN      PTR blue.
IN      PTR green.
IN      PTR yellow.
```

你“内部”的 `yourdomain.com` 区域文件包含了有关该区域信息的资源记录。你的 DNS 服务器使用 `TTL`（生存时间）告诉存储你为此域名提供的信息的名称服务器，它们在丢弃这些信息并获取新信息之前可以保留这些信息。第一个值是整个区域的默认值，时间单位为秒。因此，`86400` 的值表示客户端使用信息应每 24 小时获取一次该域名的最新记录。`SOA` 行标识了域名的权威机构。`at (@)` 符号代表 `yourdomain.com` 名称 ——点 (`.`) 必须出现在域名的末尾。点代表互联网的根。如果你漏掉了点，你的 DNS 服务器将附加域名，因此 DNS 服务器将使用名为 `yourdomain.comyourdomain.com` 的名称。`hostmaster@yourdomain.com` 字符串表示接收与域名相关邮件的人的电子邮件地址。（点变为 `@` 符号，结果为 `hostmaster@yourdomain.com`）。关于 `SOA` 记录的其他信息如下：

- 以任意数字开始。如果区域记录发生更改，通过序列号来提醒其他服务器，它们可以获取关于你域名的最新数据。

**注意：** 如果你在更改区域记录后忘记增加序列号，缓存这些数据的其他服务器将永远不会获取你的更改。为了帮助记忆，请在序列号中使用日期。数字 `2008042701` 代表 2008 年 4 月 27 日。`01` 代表该当天进行的第一次更改。

- `Refresh`（刷新）——定义了该区域的从 DNS 服务器检查更改的方式。

名称服务器（`NS`）记录定义了代表此区域的名称服务器。假设 `NS` 记录定义了 `yourdomain.com` 中名为 `ns1` 和 `ns2` 的主机。`MX` 记录指示了该域名的主服务器的位置，以便 DNS 服务器将电子邮件重定向到 `yourdomain.com` 中的用户。文件的其余部分定义了与域名相关的私有客户端和公共服务器的 IP 地址。请注意，地址为 `10.0.0.2` 的服务器既是局域网上的客户端也是 DNS 服务器。

## 启动 named（DNS）守护进程

要启动 `named` 进程并查看它是否工作，请输入以下（作为 root）：

```
# /etc/init.d/named start
```

如果 `named` 进程启动成功，服务器的客户端应该开始获取关于你域名的信息。要设置 `named` 进程在每次系统启动时运行，请输入：

```
# chconfig named
```

记得当你更改 `named.conf` 或任何区域文件时，必须在检查域名之前增加序列号。之后，你应该按如下方式重启 `named` 服务（作为 root）：

```
# /etc/init.d/named restart
```

然后你应该考虑将服务器的本地地址添加到它的 `/etc/resolv.conf` 文件中。例如，`/etc/resolv.conf` 文件可以包含以下内容：

```
search yourdomain.com
nameserver 127.0.0.1
```

## 检查 DNS 是否工作

验证你的 DNS 服务器运行正常的最佳方法是观察它的运行。这里有你可以用于检查你的 DNS 服务器的几个命令。第一个示例使用 `host` 命令获取本地域中主机 `blue` 的 IP 地址：

```
# host blue
blue.yourdomain.com has address 10.0.0.3
```

### 第 25 章：通过 DNS 使服务器公网

```
;;yourdomain.com.
IN                                     A

;; AUTHORITY SECTION:
yourdomain.com             604800 IN NS ns1.yourdomain.com.
yourdomain.com             604800 IN NS ns2.yourdomain.com.

;; Query time: 24 msec
;; SERVER: 10.0.0.1#53(10.0.0.1)
;; WHEN: Mon Jun 9 02:12:32 2008
;; MSG SIZE rcvd: 129
```

输出中的部分包含查询部分和权威部分。结果显示了与你查询的域名相关的服务器名称分配和地址。`nslookup` 命令是你可以用来的查找查找域信息的另一个工具。在下面的示例中，`nslookup` 查询正在解析的服务器：

```
ftp.yourdomain.com

# nslookup -sil ftp.yourdomain.com
Server:                   123.45.67.1
Address:                 123.45.67.1#53

Name:                    ftp.yourdomain.com
Address:                 123.45.67.4
```

`nslookup` 命令的输出包含了响应请求的计算机名称及其 IP 地址，以及你所查询的计算机的名称和地址。（`-sil` 选项防止 `nslookup` 可能从 Fedora 和 RHEL 中移除）。尝试使用 IP 地址（如 `10.0.0.1`）运行 `nslookup` 以确保反向查找正常。你也可以考虑使用 `dig` 代替 `nslookup`。

要检查运行在本地系统上的 `named` 服务器的状态，请使用与 `named` 相同的脚本。输入以下内容检查你的 DNS 守护进程状态：

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

如果你无法通过名称或 IP 地址访问你的 DNS 服务器正在提供的计算机，请确保每个客户端的地址记录是正确的。你也可以尝试使用完整的主机名或 IP 地址 `ping` 每个客户端和服务器计算机。

## 获取更多关于 BIND 的信息

关于在本章未描述的许多其他 BIND 选项，你可以参考以下几个地方，如下列表所示：
