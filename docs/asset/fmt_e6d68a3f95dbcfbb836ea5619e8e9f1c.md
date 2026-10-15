
```
ubuntu$ sudo nmap -sV -O secure.booklab.atrust.com
Starting Nmap 4.20 ( http://insecure.org ) at 2009-11-01 12:44 MST
Interesting ports on secure.booklab.atrust.com (192.168.20.35):
Not shown: 1691 closed ports
PORT     STATE SERVICE VERSION
25/tcp   open  smtp   Postfix smtpd
80/tcp   open  http   lighttpd 1.4.13
Device type: general purpose
Running: Linux 2.4.X,2.5.X|2.6.X
OS details: Linux 2.6.16 - 2.6.24
Nmap finished: 1 IP address (1 host up) scanned in 8.095 seconds
```

这个功能对于盘点本地网络非常有用。不幸的是，它对黑客来说也非常有用，他们可以基于目标操作系统和服务器的已知弱点来发起攻击。

请记住，大多数管理员并不欣赏你扫描其网络并指出其漏洞的努力，无论你的动机多么善意。在未经该网络管理员许可的情况下，不要在别人的网络上运行 `nmap`。

### Nessus：下一代网络扫描器

Nessus 最初由 Renaud Deraison 于 1998 年发布，是一款功能强大且实用的软件漏洞扫描器。截至目前，它使用超过 31,000 个插件来检查本地和远程安全漏洞。虽然它现在已成为闭源的专有产品，但它仍然可以免费使用，并且新插件会定期发布。它是最广泛接受和最完整的漏洞扫描器。

Nessus 以不做任何假设的安全扫描器为荣。例如，它不会假设所有 Web 服务器都运行在端口 80 上，而是扫描在任何端口上运行的 Web 服务器并检查其漏洞。与其依赖服务报告的版本号，Nessus 会尝试利用已知漏洞来查看服务是否易受攻击。

虽然需要大量的设置时间才能让 Nessus 运行（它需要几个在典型系统上未安装的软件包），但这绝对值得付出努力。Nessus 系统包括客户端和服务器。服务器充当数据库，客户端处理 GUI 呈现。Nessus 服务器和客户端都存在于 Windows 和 UNIX 平台上。

Nessus 的一大优势是其模块化设计，使得第三方可以轻松添加新的安全检查。得益于活跃的用户社区，Nessus 未来几年很可能仍将是一个有用的工具。

### John the Ripper：不安全密码的查找器

一种阻止糟糕密码选择的方法是尝试自己破解密码并强制用户更改你已破解的密码。`John the Ripper` 是 Solar Designer 的一个复杂工具，它在一个工具中实现了各种密码破解算法。它取代了本书前几版中介绍的工具 `crack`。

即使大多数系统使用 `shadow` 密码文件将加密密码隐藏在公众视野之外，验证用户密码是否具有抗破解性仍然是明智的。知道用户的密码可能很有用，因为人们倾向于反复使用相同的密码。单个密码可能会提供对另一系统的访问权限，解密用户主目录中存储的文件，并允许访问网络上的财务账户。（不用说，以这种方式重复使用密码并不是很安全的做法。但没有人想记住十个密码。）

考虑到其内部复杂性，`John the Ripper` 是一个极其简单的程序。直接将 `john` 指向要破解的文件，通常是 `/etc/shadow`，然后观看魔术发生：

```
$ sudo ./john /etc/shadow
Loaded 25 password hashes with 25 different salts (FreeBSD MD5 [32/32])
password (jsmith)
badpass (tjones)
```

在此示例中，从 `shadow` 文件读取了 25 个唯一密码。随着密码被破解，John 会将其打印到屏幕上并保存到名为 `john.pot` 的文件中。输出包含左列的密码和右列括号中的登录名。要在 `john` 完成后重新打印密码，请使用 `-show` 参数运行相同的命令。

截至本文撰写时，`John the Ripper` 的最新稳定版本是 1.7.3.4。它可从 `openwall.com/john` 获取。由于 `John the Ripper` 的输出包含其已破解的密码，因此你应仔细保护输出，并在完成检查哪些用户的密码不安全后立即删除它。

与大多数安全监控技术一样，在使用 `John the Ripper` 破解密码之前，获得明确的管理批准非常重要。

### hosts_access：主机访问控制

网络防火墙是防止未经授权的主机访问的第一道防线，但不应是唯一的屏障。两个文件，`/etc/hosts.allow` 和 `/etc/hosts.deny`，也称为 TCP wrappers，可以根据网络请求的来源限制对服务的访问。`hosts.allow` 文件列出允许连接到特定服务的用户主机，而 `hosts.deny` 文件限制访问。但是，这些文件仅控制 `hosts_access` 感知的服务，例如由 `inetd`、`xinetd`、`sshd` 和某些 `sendmail` 配置管理的服务。

在大多数情况下，明智的做法是保持限制，仅允许从指定主机访问必要的服务。我们建议在 `hosts.deny` 文件中默认拒绝访问，使用单行

```
ALL:ALL
```

然后你可以在 `hosts.allow` 中逐案允许访问。以下配置允许 `192.168.0.0/255.255.0.0` 网络上的主机访问 SSH，并允许从任何地方访问 `sendmail`。

```
sshd: 192.168.0.0/255.255.0.0
sendmail: ALL
```

The format of an entry in either file is `service: host` or `service: network`. Failed connection attempts are noted in `syslog`. Connections from hosts that are not permitted to access the service are immediately closed.

Most Linux distributions include `hosts.allow` and `hosts.deny` files by default, but they’re usually empty. Our other example systems all offer TCP wrappers as an option after installation.

### Bro: the programmable network intrusion detection system

`Bro` is an open source network intrusion detection system (NIDS) that monitors network traffic and looks for suspicious activity. It was originally written by Vern Paxson and is available from `bro-ids.org`.

`Bro` inspects all traffic flowing into and out of a network. It can operate in passive mode, in which it generates alerts for suspicious activity, or in active mode, in which it injects traffic to disrupt malicious activity. Both modes likely require modification of your site’s network configuration.

Unlike other NIDSs, `Bro` monitors traffic flows rather than just matching patterns inside individual packets. This method of operation means that `Bro` can detect suspicious activity based on who talks to whom, even without matching any particular string or pattern. For example, `Bro` can

- Detect systems used as “stepping stones” by correlating inbound and outbound traffic

- Detect a server that has a back door installed by watching for unexpected outbound connections immediately after an inbound one
