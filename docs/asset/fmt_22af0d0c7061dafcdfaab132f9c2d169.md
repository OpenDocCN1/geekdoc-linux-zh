
### `nmap`

`nmap` 工具用于扫描系统，查看哪些端口开放，并尝试确定关于主机的一些信息。这对于检查防火墙或受保护的系统非常有用。例如，以下是对一个不安全主机的简单扫描：

```
europa:/etc/security# nmap -sT -0 badserver

Starting nmap V. 2.54BETA7 ( www.insecure.org/nmap/ )
Interesting ports on (1.2.3.4):
(The 1506 ports scanned but not shown below are in state:
closed)
Port          State     Service
7/tcp         open      echo
9/tcp         open      discard
13/tcp        open      daytime
17/tcp        open      qotd
19/tcp        open      chargen
21/tcp       open      ftp
25/tcp       open      smtp
26/tcp       open      unknown
27/tcp       open      nsw-fe
42/tcp       open      nameserver
80/tcp       open      http
110/tcp      open      pop-3
119/tcp      open      nntp
135/tcp      open      loc-srv
139/tcp      open      netbios-ssn
143/tcp      open      imap2
389/tcp      open      ldap
443/tcp      open      https
515/tcp      open      printer
563/tcp      open      snews
593/tcp      open      http-rpc_epmap
636/tcp      open      ldapsssl
993/tcp      open      imaps
995/tcp      open      pop3s
2401/tcp     open      cvspserver
6667/tcp     open      irc
6668/tcp     open      irc
8080/tcp     open      http-proxy

TCP Sequence Prediction: Class=trivial time dependency
Difficulty=73 (Easy)

Remote operating system guess: Windows NT4 / Win95 / Win98

Nmap run completed -- 1 IP address (1 host up) scanned in 3 seconds
```

如您所见，`nmap` 显示了哪些端口开放以及所使用的操作系统类型。`nmap` 拥有大量的选项和命令行参数。如果你使用 X11，一个图形用户界面前端将使使用 `nmap` 变得更加容易。它被称为 `nmapfe`，通常可以从获取 `nmap` 的地方找到。

### `SAINT`

`SAINT` 是原始 `SATAN` 安全扫描器的更新版本。`SAINT` 探测联网计算机以了解它们提供的服务。`SAINT` 比 `nmap` 更进一步，它了解运行的服务，并可以查找常见漏洞和错误配置。它提供了一个非常易于使用的 Web 界面，以易于阅读的方式显示漏洞信息。

`SAINT` 可以从 `http://www.wwdsi.com` 免费获得。

### `Nessus`

`Nessus` 是另一种以比 `SAINT` 更模块化的方式构建的安全扫描器。它同样使用客户端-服务器架构，因此您可以远程扫描来自另一网络的机器。也有为 UNIX 以外的操作系统编写的客户端。

`Nessus` 可以从 `http://www.nessus.org` 获得。

### `crack`

`crack` 工具用于检查不良密码。定期使用 `crack` 检查用户密码以查看它们是否容易被解密是一个好主意。

`crack` 可以从 `ftp://ftp.cert.org` 获得。

### `COPS`

`COPS`，即计算机预言机与密码系统（Computer Oracle and Password System），是一组用于监控系统安全状况的程序。它监控以下内容：

- 文件、目录和设备权限/模式。
- 弱密码。
- 密码和组文件的内容、格式和安全状况。
- 在 `rc` 目录和 `crontab` 文件中运行的程序和文件。
- SUID root 文件的存在、其可写性，以及它们是否为 shell 脚本。
- 针对重要二进制文件或关键文件的 CRC 校验，以报告其中的任何更改。
- 用户主目录和启动文件（如 `.profile`、`.cshrc` 等）的可写性。
- 匿名 FTP 配置。
- 不受限制的 `tftp`、`sendmail` 中的 `decode` 别名、SUID `uudecode` 问题、`inetd.conf` 中隐藏的 shell，以及在 `inetd.conf` 中运行的 `rex`。
- 其他 root 检查——搜索路径中的当前目录、`/etc/host` 中的 `"+"`、`equiv`、不受限制的 NFS 挂载、`/etc/ftppers` 中的 root 等。
- `CERT` 公告与关键文件的日期对比。这检查 `CERT` 报告的各种 bug 和安全漏洞的日期与问题文件的实际日期。阳性结果并不一定意味着发现了 bug，但它是一个很好的迹象，表明你应该查看公告和文件以获取更多线索。显然，阴性结果并不意味着你的软件没有漏洞，仅意味着自公告发布以来，该文件以某种方式（可能只是被触碰过）进行了修改。
- Kuang 专家系统。这取一组规则并尝试确定你的系统是否可能被入侵。

通常，`COPS` 通过 `cron` 每晚运行以执行其检查。这样你可以立即收到任何可能存在问题的更改警报。

`COPS` 可从 `http://www.cerias.purdue.edu` 获取。

### `Tripwire`

`Tripwire` 是一个工具，用于监控系统文件的权限和校验和，以便你可以轻松检测它们是否被篡改。设置时，`Tripwire` 创建一个包含所有配置文件的校验和信息数据库。最好将此数据库和 `Tripwire` 的配置文件保存在安全系统的只读介质上。

`Tripwire` 最初是一款免费产品，后来转向商业化。然而，仍有一个免费版本可用并得到维护。它可在 `http://www.tripwire.org` 获取。

### `Bastille Linux`

`Bastille Linux` 是一个针对 `Red Hat` 的强化脚本。它会遍历一系列问题，并根据管理员提供的信息，管理员可以选择是否采纳脚本的建议。`Bastille` 本身不提供任何服务；它只是锁定现有系统的安全性。

如果你是安全新手，走一遍 `Bastille` 脚本是一个好主意，不仅是为了保护你的系统，也是为了向你介绍安全知识。该脚本提供了关于它做什么以及为什么这样做的极好信息。

`Bastille Linux` 可从 `http://www.bastille-linux.org` 获取。

### 关键点总结

安全是系统管理员工作中非常重要的一部分。如果做得好，它会占用你大量的时间，但这些时间是值得的。本章提供的信息是知识之路的一个很好的起点。

- `TCP wrappers` 使用 `hosts.allow` 和 `hosts.deny` 文件为 TCP 服务提供安全保护。
- `tcpdchk` 用于检查 `hosts.allow` 和 `hosts.deny` 文件的语法。
- `tcpdmatch` 用于向系统提供理论连接以测试你的 `hosts.allow` 和 `hosts.deny`。
- SUID 可执行文件和脚本可能是非常大的安全风险。
- RPM 包的有效期可以使用 PGP 和 GPG 进行检查。
- 任何包或文件都可以使用 `md5sum` 工具进行检查。
- SGID 位可用于创建允许用户共享文件的目录。
- 如果目录设置了 SGID 位，新文件属于该目录的组而不是用户。
- Berkeley r 命令非常不安全。
- `.rhosts` 文件用于给予远程用户访问本地帐户的权限。
- `hosts.equiv` 文件用于允许或拒绝其他主机对 r 命令的访问。
- `rlogin` 用于远程登录到另一台系统。
- `rcp` 用于在系统之间复制文件。
- `rsh` 用于在远程系统上执行单个命令。
- `rwho` 显示谁登录在本地网络上。
- `uptime` 显示网络上系统的运行时间。
- SSH 是 Berkeley r 命令的安全替代方案。
