
`/etc/hosts.allow`:
```
#
# hosts.allow	this file describes the names of the hosts which
               allowed to use the local INET services, as decided
               by /usr/sbin/tcpd'. server.
#
ALL: LOCAL, games.com, toys.com, weapons.com
```

TCP Wrappers 阻塞所有并仅允许指定的网络连接。

根据你的邮件系统（主要用于内部邮件？），这可能是你的方法。但是，拒绝少数网络并允许访问 `ALL` 可能会更简单，如下所示：

`/etc/hosts.deny:`:
```
#
# hosts.deny    this file describes the names of the hosts which
               *not* allowed to use the local INET services, as decided
               by /usr/sbin/tcpd'. server.
```

`/etc/hosts.allow`:
```
#
# hosts.allow	this file describes the names of the hosts which
               allowed to use the local INET services, as decided
               by /usr/sbin/tcpd'. server.
#
ALL: LOCAL, games.com, toys.com, weapons.com
```

这是一个阻止除 `games.com`、`toys.com` 和 `weapons.com` 之外所有员访问服务的示例：

`/etc/hosts.deny:`:

```
ALL: LOCAL, games.com, toys.com, weapons.com
```

### 其他 sendmail 资源

- Robert Harker 的 sendmail 技巧与技巧。此页面有许多 sendmail 教程 (`http://www.harker.com/sendmail/sendmail-tips.html`)。
- Russell Coker 的通过源码更改 sendmail 安全。在这里，Coker 描述了如何在没有 root 的情况下设置 sendmail (`http://www.coker.com.au/~russ/sendmail.html`)。
- Kai 的 SpamShield。该网站提供一个程序保护你的 sendmail 服务器免受垃圾邮件发送者和其他家伙 (`http://spamshield.conti.nu/`)。
- AmaVIs 是一个 sendmail 服务器的病毒扫描器，对于依赖 SMTP 邮件的异构网络非常有用。访问 `http://satan.oih.rwth-achen.de/AmaVIs`。
- CIAC F-13: Unix sendmail 漏洞。该公告提供了一些 sendmail 安全链接 (`http://ciac.llnl.gov/ciac/bulletins/f-13.shtml`)。
- Harker 用于版本 8.7、8.8 和 8.9 的 sendmail cf。该网站允许你根据你指定的各种选项生成各种 sendmail 配置集。这是一个学习更多关于 sendmail 配置的工具 (`http://www.harker.com/webgencf/index.html`)。
- Muy Cool sendmail。在该页面上你可以找到安全公告、补丁和其他有用的 sendmail 信息 (`http://www.muycool.org/sendmail/`)。
- 防火墙应用说明。本文处理了与防火墙相关的应用程序代理和 sendmail (`http://www.telstra.com.au/pub/docs/security/firewall-1.1`)。
- Bryan Beecher 的 `smtptstats`，一个收集你流量统计信息的 shell 脚本。
- Tom Christians 的 `ssl`（不要与 Sockets Layer 混淆），一个总结 syslog 的 Perl 脚本。
- Rich Bjorkund 的 `syslog_stats` 是另一个用于总结活动的良好 Perl 脚本。
- LDAP 集成。将 LDAP 服务器与邮件集成。
- 身份验证 SMTP。身份验证 SMTP 需要用户名和密码才能发送消息。
- LDAP 数据库。LDAP 维护用户数据库。
- LDAP 查询。LDAP 服务器执行地址查找。

# 用 Qmail 替换 sendmail

Qmail 是 Dan Bernstein 开发的 sendmail 替代品，他在开发时充分考虑了安全性。最近，Bernstein 为任何能够破解 Qmail 的人提供了 1000 美元的悬赏。该奖金无人认领。（有关该竞赛的更多信息，请访问 `http://www.qmail.org`。）本节将将介绍 Qmail。

## Qmail 安装

要安装 Qmail，请先从 `ftp://moni.msci.memphis.edu/pub/qmail` 下载 RPMS 包。在这里，我将讨论源码发行版。

在 Adam McKenna 的 Qmail HOWTO 中也有详细的安装说明，地址为：`http://www.floulder.net/qmail/qmail-howto.html`。

下载源码发行包后，解压并解开 tar 归包：

```
[root@applemac root]# gunzip qmail-1.03.tar.gz
[root@applemac root]# tar -xf qmail-1.03.tar
```

接下来，创建 Qmail 的家目录：

```
[root@applemac root]# mkdir /var/qmail
```

在 Qmail 正常运行之前，你需要添加所有的用户和组。你可以使用 `INSTALL.ids` 文件中描述命令来自动化此过程：

```
[root@applemac qmail-1.03]# /usr/sbin/groupadd nofiles
[root@applemac qmail-1.03]# /usr/sbin/useradd -g nofiles -d ->/var/qmail/alias alias
[root@applemac qmail-1.03]# /usr/sbin/useradd -g nofiles -d ->/var/qmail qmaild
[root@applemac qmail-1.03]# /usr/sbin/useradd -g nofiles -d ->/var/qmail qmail
[root@applemac qmail-1.03]# /usr/sbin/useradd -g nofiles -d ->/var/qmail qmailp
[root@applemac qmail-1.03]# /usr/sbin/groupadd qmail
[root@applemac qmail-1.03]# /usr/sbin/useradd -g -d ->/var/qmail qmail *
```

```
[root@applemac qmail-1.03]# /usr/sbin/useradd -g qmail -d ->/var/qmail qmail
[root@applemac qmail-1.03]# /usr/sbin/useradd -g qmail -d ->/var/qmail qmails
```

现在你准备好编译并安装了。（请耐心等待，取决于你的速度，这可能需要几分钟。）首先，运行设置检查：

```
[root@applemac qmail-1.03]# make setup check
```

一旦此过程完成，运行配置脚本：

```
[root@applemac qmail-1.03]# ./config
```

你的主机名是 `applemac.ag.ohio-state.edu`。
