

幸运的是，当今几乎所有流行的 Unix 系统上都有一个非常好的替代方案：ssh。安全外壳（SSH）不仅能在客户端与服务器之间加密数据，还提供了一种简单有效的类 FTP 功能，可通过 Unix 命令行中的 sftp 来使用。交互方式几乎相同（但不支持匿名 sftp）。

如果你想向用户群体提供文件传输功能，在我看来毫无疑问——使用 ssh，并教会他们如何使用它。然后永久禁用 telnetd 和 ftpd。哦，你还必须接受一个事实：不存在匿名 ssh 选项。

![](img/5ced0c78d748bd190e9027e5549a3622_405_0.png)

> 如果你决定运行匿名 ftp，至少请研究一下 ftpaccess（参见 man 手册页），并将其配置好，以帮助提供最大可能的安全性。

运行 Unix 服务器最令人愉悦的方面之一，是能够向用户提供的服务范围之广。虽然有些服务是 Unix 强大功能与灵活性的典范（例如 Apache，本书最后两小时将详细讨论），有些则相当精巧（ntp 网络时间协议会自动确保你的系统时钟始终准确，这很酷），但也有几个相当危险的服务，应尽可能避免使用。排在榜首的是 ftpd，telnetd 紧随其后。

## 本章小结

本小时探讨了重要的 inetd 和 xinetd 配置文件，并顺带介绍了 TCP Wrapper 和 syslogd。此外，你还学习了如何为各种不同的 Unix 平台配置匿名 FTP 服务器，并且同样重要的是，你了解到了一些令人信服的理由，说明为什么这样做并非良策。

## 问答

问：哇，你对 FTP 的措辞可真激烈！你确定吗？

答：如今在系统上已经很少能看到匿名 FTP 了，尤其是随着 Web 的出现，以及用户可以通过 Web 服务器直接轻松下载文件（当然，Web 服务器本身也有安全问题，但那是另一回事）。

问：你更喜欢 inetd 还是 xinetd？为什么？

答：也许是"老狗学不会新把戏"综合征吧，但我仍然更喜欢 inetd 的简洁。能够一眼扫过单个文件、立刻知道哪些服务已启用、哪些没有启用，这有着巨大的价值。

## 实践

### 测验

1. 创建 inetd 的主要动机是什么？
2. 应该使用什么简单模式来确定 /etc/inetd.conf 中列出的哪些服务实际上是启用的？
3. 就 inetd.conf 文件中的套接字值而言，stream 意味着 ____，而 dgram 意味着 ____？
4. 哪种常见的 Unix 程序可以轻松测试任何网络服务？
5. 有点偏执地说，使用 inetd 或 xinetd 的最佳经验法则是什么？
6. 使用 TCP Wrapper，你可以在何处指定相应信息来允许或拒绝连接？
7. 匿名 FTP 的可用性并非必需，因为你可以通过什么流行机制轻松地让匿名用户访问文件？

### 答案

1. 为了应对越来越多的守护进程在等待连接时消耗系统资源的问题。
2. 搜索 # 是否为第一个字符。要找到所有已启用的服务，请使用 grep -v '^#'。
3. stream 套接字意味着 TCP，而 dgram 意味着 UDP。
4. telnet，对任何系统管理员来说都是一个极好的实用工具。
5. 最佳经验法则是禁用一切。
6. 要允许连接，请在 /etc/hosts.allow 中指定规则，而拒绝规则应放在 /etc/hosts.deny 中。
7. 使用 Web 服务器：Apache 可以传送任何类型的文件或信息，不仅仅是 HTML 和 JPEG 图形。

下一小时将详细探讨另一个网络服务。如果你一直在试图理解底层电子邮件，你会发现第 20 小时对 sendmail 的探讨大有裨益。

![](img/5ced0c78d748bd190e9027e5549a3622_407_0.png)

## 第 20 小时：使用电子邮件

系统管理涉及在一个或多个 Unix 系统上管理各种各样的服务，但有一项服务如果出问题，保证会让你陷入麻烦，那就是电子邮件。无论你的用户群体的技术水平如何，如果他们无法发送和接收电子邮件，你一定会听到抱怨。

本小时重点介绍如何使用 sendmail——Unix 系统上的标准邮件传输代理（MTA）。还有其他可用的 MTA，包括流行的 postfix、exim、qmail 和 smail 程序，但我见过的几乎每个 Unix 系统都默认附带 sendmail。

区分邮件传输代理和其他电子邮件相关软件也很重要。让你阅读、组织和撰写消息的程序称为邮件用户代理，其例子从 Elm、Pine 到 Entourage 和 Outlook 不等。有基于 X Window 系统的应用程序、像 Apple Mail 这样的图形应用程序，以及各种各样的命令行或基于 shell 的邮件程序，但在 Unix 中，它们都是通过将外发消息交给 MTA 来运作的。MTA——sendmail——是负责在本地投递邮件，或连接到远程系统并将消息通过线路传送到目标系统（目标系统很可能也运行着 sendmail）的程序。

话虽如此，有必要说明的是，我们不打算深入探讨以复杂著称的 sendmail.cf 配置文件。它本身就是一种晦涩的语言，典型的 sendmail.cf 文件可能非常庞大。在 Red Hat Linux 中该文件的默认大小为 1,490 行，在 Mac OS X 中为 1,214 行，在 Solaris 8 中为 1,191 行。如果你一定要了解更多，我建议你看看 Brian Costales 和 sendmail 原创程序员 Eric Allman 合著的《sendmail》（O'Reilly 出版）一书。

好了，那我们要讲什么呢？如何操作和使用 sendmail 及其强大的别名功能，以确保你的用户日复一日都能拥有愉快而无痛的电子邮件体验。

本小时你将学到以下内容：

- 使用 sendmail 测试邮件连通性
- 邮件日志和邮件队列
- 创建 sendmail 别名
- Mac OS X 中的 sendmail 别名

### 使用 sendmail 测试邮件连通性

探索 sendmail 复杂性的一个合乎逻辑的起点——你基本上是置身于一个曲折通道的迷宫之中——是学习如何使用 sendmail 标志来测试服务器的邮件连通性。

![](img/5ced0c78d748bd190e9027e5549a3622_408_0.png)

> 曲折通道这个说法参考了 70 年代伟大的 Adventure 程序，该程序是用 Fortran 为 Unix 编写的。这是我玩过的第一款交互式小说游戏，自那以后它一直是几代酷炫的 D&D 风格游戏的灵感来源。

### 任务 20.1：使用 sendmail 验证连通性

sendmail 程序有各种各样的标志，如果程序作为守护进程运行，大多数标志以 b 或 o 开头。通常你会看到诸如 -bd（以守护进程模式运行）、-bp（打印邮件队列）和 -bi（初始化别名数据库）之类的选项。

```
# sendmail -bg -d0.1 < /dev/null
Version 8.11.6
Compiled with: LDAPMAP MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7
NAMED_BIND NETINET NETINET6 NETUNIX NEWDB NIS QUEUE SASL SCANF
SMTP TCPWRAPPERS USERDB
Invalid operation mode g

========== SYSTEM IDENTITY (after readcf) ==========
(short domain name) $w = staging
(canonical domain name) $j = staging.intuitive.com
(subdomain name) $m = intuitive.com
(node name) $k = staging.intuitive.com
============================================
```

令人欣喜的是，这个 Red Hat 安装运行的是较新版本的 sendmail（第一行标明：8.11.6）。

在 Mac OS X 上运行完全相同的命令会显示以下内容：

```
# sendmail -bt -d0.1 < /dev/null
Version 8.10.2
Compiled with: MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7 NAMED_BIND
NETINET NETINFO NETISO NETUNIX NEWDB NIS QUEUE SCANF SMTP
USERDB XDEBUG

/etc/mail/sendmail.cf: line 81: fileclass: cannot open
->/etc/mail/local-host-names: Group writable directory

========== SYSTEM IDENTITY (after readcf) ==========
(short domain name) $w = dsl-132
(canonical domain name) $j = dsl-132.dsldesigns.net
(subdomain name) $m = dsldesigns.net
(node name) $k = dsl-132.dsldesigns.net
============================================

ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
```

在 Solaris 8 上：

```
# /usr/lib/sendmail -bt -d0.1 < /dev/null
Version 8.10.2Sun
Compiled with: LDAPMAP MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7
NAMED_BIND NDBM NETINET NETINET6 NETUNIX NEWDB NIS NISPLUS
QUEUE SCANF SMTP USERDB XDEBUG

========== SYSTEM IDENTITY (after readcf) ==========
(short domain name) $w = solaris
(canonical domain name) $j = solaris.dsldesigns.net
(subdomain name) $m = dsldesigns.net
(node name) $k = solaris.dsldesigns.net
============================================

ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
```

