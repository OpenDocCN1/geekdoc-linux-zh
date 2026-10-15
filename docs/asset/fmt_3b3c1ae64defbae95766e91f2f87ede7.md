
# 第20章 电子邮件

```
Compiled with: DNSMAP GETMAILHOST LDAP LOGMAP_REGEXP MILTERTO8 NAMED_BIND NETINET NETINETUNIX NEWDB PIPELINING ASLV2 SCAN SOCKET TTTLSWRAPPERS USERDB USE_LDAP_INIT

========= SYSTEM IDENTITY (afterfd) ==========

(short domain name) $ = ross

(canonical domain name) $ = amass.com

(subdomain name) $m = at.com

(node name) $k = ross.at.com
```

此命令将 `sendmail` 置于测试模式（`-bt`）和调试模式（`-d0.1`），但没有给它地址 `</dev/null>`。副作用是 `sendmail` 告诉它版本号和编译器。一旦知道了版本号，你可以查看 sendmail.org 网站查看该版本是否存在已知的安全漏洞。

要找到系统上的 `sendmail` 文件，请查看 `/etc/sendmail.cf` 目录。注释提到了构建配置的目录。该目录应该引导你找到 `.mc` 文件，它是配置的源。

大多数带有 `sendmail` 的供应商不仅包含了二进制文件，还包含了分发树中的 `cf` 目录，它们隐藏在操作系统中。这将帮助你找到它。

## 表 20.5 `sendmail` 配置目录

| 系统 | 目录 |
|---|---|
| Ubuntu | `/usr/share/sendmail` |
| SUSE | `/usr/share/sendmail` |
| Red Hat | `/usr/share/sendmail-cf` |
| Solaris | `/etc/mail/cf` |
| HP-UX | `/etc/mail/cf` |
| AIX | `/tcpip/sendmail/cf` |

## 切换文件

大多数系统都有一个“服务切换”配置文件 `access.conf`，它列出了满足各种用户和主机查找的方法。如果对于给查询使用了多个方法，切换文件还决定了咨询这些方法的顺序。切换文件的存在对软件来说通常是透明的。然而，`sendmail` 喜欢对循环进行细粒度的控制，因此接管了切换文件并使用其内部配置（`/etc/mail/switch`）。

切换文件中的两个字段影响邮件系统：别名和主机。主机的可能值为 `dns`、`nis`、`nisplus` 和 `files`。对于别名，可能值为 `files`、`nisplus` 和 `ldap`。你使用的机制（文件除外）必须在使用之前编译到 `sendmail` 中。

## 启动 `sendmail`

`sendmail` 不应由 `inetd` 或 `xinetd` 控制，因此必须在启动时显式启动。详情请见第3章“启动与关机”。标志决定了它的行为。你可以通过 `-b` 标志以多种模式运行 `sendmail`。它代表“be”或“become”，始终与另一个决定 `sendmail` 将角色的标志一起使用。表26列出了合法值并包含了 `-A` 标志，该标志选择 MTA 和 MSA。如果你正在配置一个接受来自互联网的入站邮件的服务器，以守护模式运行 `sendmail`（`-bd`）。在这种模式下，`sendmail` 监听端口25 并等待工作。你通常还会指定 `-q` 标志——`sendmail` 监听的端口由 `DAEMON_OPTIONS` 决定；端口 25 是默认值。

## 表 20.6 `sendmail` 主要模式的命令行标志

| 标志 | 含义 |
|---|---|
| `-Ac` | 使用 `submit.cf` 配置文件并作为 MSA |
| `-Am` | 使用 `sendmail.cf` 配置文件并作为 MTA |
| `-ba` | 以 ARPANET模式运行（期望行尾为 CR/LF） |
| `-bd` | 以守护模式运行并监听端口25 的连接 |
| `-bD` | 以守护模式运行，但在前台而非后台 |
| `-bh` | 查看最近的连接信息（同 `hoststat`） |
| `-BH` | 清除磁盘上的过时连接信息（同 `purgestat`） |
| `-bi` | 初始化哈希别名（同 `newaliases`） |
| `-bv` | 作为主运行，按通常方式递送邮件（默认） |
| `-bp` | 打印邮件队列（同 `mailq`） |
| `-bP` | 通过共享打印队列中的条目数 |
| `-bs` | 进入 SMTP 服务器模式（在标准输入上，而非端口25） |
| `-bt` | 仅验证邮件地址；不发送邮件 |

a. 此模式用于调试，以便你可以看到 `sendmail` 处理邮件队列时错误和调试消息的间隔。例如，`-q30m` 每30分钟运行一次队列，`-qlh` 每小时运行一次。

`sendmail` 通常尝试立即递送消息，仅在队列中短暂保存以保证可靠性。如果你的主机太忙或目标机器不可达，`sendmail` 会将消息队列并在稍后发送。`sendmail` 使用持久的队列运行程序，这些程序通常在启动时启动。它执行锁定，因此多个同时的队列运行程序是安全的。“队列组”配置功能有助于大型邮件列表和队列。在第802页有更详细的介绍。

`sendmail` 在启动时会读取其配置文件 `sendmail.cf`。在那里，当你更改配置文件时，必须杀死并重启 `sendmail`，或者发送 `HUP` 信号。`sendmail` 会创建一个 `sendmail.pid` 文件，其中包含其进程 ID 和它启动的命令。你应该使用绝对路径启动 `sendmail`，但在接收到 `HUP` 信号时会重新执行自身。`sendmail.pid` 文件允许通过命令对进程进行 `HUP`：

```
sudo kill -HUP 'head -1 sendmail.pid'
```

PID 位置取决于操作系统。它通常是 `/var/run/sendmail.pid` 或 `/etc/mail/sendmail.pid`，但可以通过配置文件中的 `confPID_FILE` 选项设置：

```
define(confPID_FILE, '/var/run/sendmail.pid')
```
