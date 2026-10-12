
你还必须`ssl/certs`目录下安装适当的SSL POP和IMAP证书，文件名分别为`ipop3d.pem`和`imapd.pem`。

## Qpopper

Qpopper是伯克利POP服务器(`popper`)的当前版本。Qpopper由Eudora邮件服务器的主手高通支持。Qpopper的Web页面地址为`www.eudora.com/free/qpop.html`。你可以从`ftp.qualcomm.com/eudora/servers/unix`获取当前的源码。RPM包版本位于分发版站点或包含在发行版中。

一旦你安装了Qpopper并运行了POP服务器，远程系统上的用户可以使用各种邮件客户端或`fetchmail`访问POP服务器。如第13章所述，`fetchmail`将从用户账户获取邮件并将其放置在本地主机的邮箱中。以下示例展示了从运行在`turtle.mytrek.com`上的POP服务器获取邮件：

```
fetchmail -p POP3 -u chris turtle.mytrek.com
```

你可以在你的Linux系统上安装Qpopper软件，并使其作为你网络的POP服务器运行。它由`qpopper`守护进程和`popauth`程序组成，后者创建一个带有密码加密的身份验证数据库以确保用户访问的安全。`popauth`会创建一个名为`/etc/pop.auth`的数据库文件。要添加用户，输入带有`-user`选项和用户名的`popauth`命令。然后会提示你输入密码，用户可以使用该密码访问其POP账户。

如果你下载的是源码版本，则使用`./configure`、`make`和`make install`序列来配置、编译和安装服务器。在配置阶段，你可能需要输入多个选项以使Qpopper兼容你的系统。例如，如果你的系统使用影子密码（大多数系统都是如此），你将需要使用`--enable-specialauth`选项。`--enable-apop`则启用使用APOP（身份验证POP）扩展，以提供由`popauth`命令管理的加密：

```bash
./configure --enable-specialauth --enable-apop
```

Qpopper通常通过`xinetd`运行。你可以在`/etc/xinetd.d`目录下创建一个类似于所示的`popper`文件：

```bash
service pop-3
{
    socket_type = stream
    wait        = no
    user        = root
    server      = /usr/bin/popper
    disable     = no
}
```

你可以使用`chkconfig`命令开启或关闭服务器：

```
chkconfig pop-3 on
```

确保`pop-3`服务列在`/etc/services`中，并带有其端口：

```
pop-3 110
```

## IMAP

邮件访问协议(IMAP)允许远程服务器为用户存放邮件，用户随后登录访问邮件。与POP服务器不同，IMAP服务器保留用户消息。用户甚至可以在IMAP服务器上保存邮件。这种方式的优点是将用户的邮件保留在网络任何地方都可以访问的位置。用户可以从网络上的任何主机登录并读取、发送和保存邮件。这种交互式连接比POP协议需要更多时间，适用于始终连接的以太网LAN。

与POP不同，IMAP允许在邮件服务器上设置多个文件夹来组织邮件。IMAP还支持使用共享文件夹，多个用户可以访问给定主题的邮件。

华盛顿大学IMAP服务器通常包含在大多数发行版中。其他IMAP服务器也可用，例如Courier-IMAP服务器和Cyrus IMAP服务器(`asg.web.cmu.edu/cyrus`)。Cyrus IMAP服务器具有安全控制功能。

华盛顿大学IMAP守护进程名为`imap`。在运行`xinetd`的系统上，它在`/etc/xinetd.d`目录下有一个名为`imap`的文件。使用`chkconfig`命令将其开启：

```bash
# default: off
# description: IMAP 服务允许远程\
# 用户使用 IMAP 客户端如 Mutt, Pine,\
# fetchmail 或 Netscape Communicator 访问邮件。
service imap {
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/imapd
    log_on_success += DURATION USERID
    log_on_failure += USERID
    disable = no
}
```

华盛顿IMAP服务器也支持之前为POP服务器描述的SSL。此外，IMAP支持APOP和CRAM-MD5身份验证方法。这些方法使用校验和而非明文来验证用户身份。然而，服务器需要知道密码的明文。这些密码存储在`/etc/cram-md5.pwd`文件中。条目由用户名和密码组成，用制表符分隔。该文件的存在将启用CRAM-MD5身份验证程序。

![](img/95726952b50a5b7113b49b7e63a39779_554_0.png)

# 第 24 章：新闻、代理与搜索服务器

| 文件 | 描述 |
| --- | --- |
| `inn.conf` | 通用INN配置文件。 |
| `incoming.conf` | 指定接收新闻源（newsfeeds）的主机。 |
| `cycbuff.conf` | 配置cnfs存储格式使用的缓冲区（buff）。 |
| `storage.conf` | 定义存储类。这些由存储方法和使用该方法新闻组组成。存储方法即存储格式：`tradpool`、`timehash`、`timecaf`和`cnfs`。另一种方法`trash`则用于丢弃文章。 |
| `expire.ctl` | 为新闻服务器上的文章设置过期策略。 |
| `readers.conf` | 指定其用户可以访问新闻服务器的主机。 |
| `ovdb.conf` | 为概览（overviews）配置ovdb存储方法。 |
| `newsfeeds` | 配置你的新闻服务器如何向其他新闻服务器推送文章。 |
| `moderated` | 受审核的新组。 |
| `cleanfeed.conf` | 配置`cleanfeed`垃圾邮件拦截工具。 |
| `innfeed.conf` | 为`innfeed`配置新闻提送进程。 |
| `innreport.conf` | 配置`innreport`工具以生成基于日志的报告。 |
| `buffedex.conf` | 为`buffedex`配置溢出缓冲区。 |

正如文档所示。当你更改配置时，务必重启INN服务器。`/etc/rc/init.d`目录下有一个`inn`脚本，其参数与Web `http`脚本类似。你可以使用`innd`脚本的`start`、`restart`和`stop`参数来启动、重启和停止INN服务器。

INN中的每个配置文件都有一个Man页面（帮助文档），提供了有关如何配置其特性的详细信息。

在许多发行版中，系统已经为你设置好了一个带有默认设置的基础`inn.conf`文件。有几个初始参数需要你自己设置，例如`domain`（存储服务器的域名）；`pathhost`（在其中指定新闻读取器的名称，以便出现在你发布的新闻文章的`Path`头部字段中）；以及`server`（在其中指定你新闻读取器的IP或完全限定域名地址，例如`mynews.mytrek.com`）。不同的`Path`已经设置以定义不同的IN目录位置，例如`patharticles`设置为`/var/spool/news`，用于存放你的新闻组文章；`pathetc`设置为`/etc/news`，用于你的配置文件。

对于经常被下载的海量文章（这是全规模服务器的核心关注），存储格式允许你在四种可能的存储格式之间选择：`tradpool`、`timehash`、`timecaf`和`cnf`。`tradpool`是传统方法，根据新闻组将文章按简单的目录结构排列。`timehash`按接收时间组织的目录存储文章，使其更容易删除过期的文章。`timecaf`与`timehash`类似，但在给定时间接收的文章被放在同一个文件中，速度快得多。`cnf`将文章存储在预先设置的缓冲区文件中。当缓冲区变满时，新进入的文章将覆盖旧文章。这是一种极快的方法，因为没有创建新文件。不需要设置最大文章限制，但也无法控制文章保留多多久。在`storage.conf`文件中，存储格式作为存储方法分配给不同的新闻组。
