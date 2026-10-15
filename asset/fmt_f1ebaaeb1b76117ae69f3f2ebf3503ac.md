
你将在示例中配置的 POP 服务器是免费提供的 `qpopper` 程序。该包最初编写于伯克利大学，现在由高通（Qualcomm）的 Eudora 部门维护。如果你还需要用于非 UNIX 系统的客户端软件，请查看高通同样提供的 Eudora Light 电子邮件包。和 `qpopper` 一样，`Eudora Light` 也是免费提供的。（不过，专业版是收费的。）

红帽（Red Hat）提供了该包的 RPM 版本，可以在 CD-ROM（`qpopper-2.3-1.1386.rpm`）上找到，你也可以从红帽官方网站 `http://ftp.redhat.com/pub/distrib/qpopper-2.3-1.1386.rpm` 获取。要安装它，只需运行

```bash
rpm -i qpopper-2.3-1.1386.rpm
```

通过这种方式，你可以安装两个程序：`/usr/sbin/in.qpopper` 和 `/usr/sbin/poppauth`。`/usr/sbin/in.popper` 是你设置从 `inetd` 运行的实际服务器程序。`/usr/sbin/poppauth` 用于配置使用 APOP 认证的客户端。

## 配置 in.qpopper

`in.qpopper`（从现在起简称为 `qpopper`）的大部分选项都是在编译时配置的；因此，除非你自己编译该包，否则你无法对操作方式拥有话语权。如果你兴趣尝试这种方法，可以从高通网站 `http://www.eudora.com/freeware/servers.html` 获取完整的包。

默认配置项适用于大多数站点。这些默认值如下：

- 拒绝为任何 UID 低于 10 的用户检索邮件（例如，root）。
- 在 `/var/spool/mail/bulletins` 中支持公告（Bulletin）。
- 新用户将收到最后发布的公告。
- 记录到 `syslog` 的详细日志。
- APOP 认证使用 `/etc/pop.auth`（详情请参见 `poppauth` 章节）。

要允许 `qpopper` 从 `inetd` 运行，请编辑 `/etc/in.qpopper` 文件并添加以下行：

```bash
pop-3 stream tcp nowait root /usr/sbin/tcpd in.qpopper
```

不要忘记向 `inetd` 发送 HUP 信号。你可以通过执行以下来实现：

```bash
kill -1 /var/run/inetd.pid
```

## 配置其他服务器

现在你准备好测试连接了。在命令提示符处，输入

`telnet popserver 110`

其中 `popserver` 是运行 `qpopper` 程序的机器名称。

你应该会收到类似下方的响应：

```
+OK QPOP (version 2.3) mtx.domain.com starting.
<14508.8770859136@mtx.domain.com>
```

此结果意味着 POP 服务器已响应并正在等待指令。（通常，此 pop 操作是由客户端邮件读取器透明地完成的）。如果你想测试认证服务，请验证以用户登录并查看服务是否注册了你当前的邮箱。例如，要以用户 `ssh` 登录并使用密码 `mars1031`，输入：

```text
+user ssh
+OK Password required for ssh
pass mars1031
+OK ssh has 5 messages (9031 octets).
quit
+OK Pop server at mtx.domain.com signing off.
```

第一行 `user ssh` 告诉 POP 服务器，它要检查邮件的用户是 `ssh`。服务器的响应确认用户 `ssh` 存在，并且访问信箱需要密码。然后你可以传递 `mars1031`，这是 `ssh` 用户的密码。服务器通过返回一个指示 `ssh` 邮件队列中当前有 5 条消息的语句来确认密码是正确的。因为你并不想实际读取邮件，只需输入 `quit` 即可终止话。服务器会发送一条注销消息并断开连接。

尽管 `qpopper` 的默认配置对于大多数站点是理想的，但你可能需要调整几个命令行参数。要使用命令行参数，只需编辑你的 `inetd.conf` 文件，使 `in.qpopper` 中的行以你想要传递的参数结尾。例如，如果你想向服务器传递 `-T 10`，你的 `inetd.conf` 条目看起来如下：

```bash
pop-3 stream tcp root /usr/sbin/tcpd in.qpopper -T 10
```

不要忘记使用以下命令向 `inetd` 程序发送 HUP 信号：

```bash
kill -1 'cat /var/run/inetd.pid'
```

`in.qpopper` 中可用以下参数：

| 参数 | 说明 |
| :--- | :--- |
| `-d` | 启用将调试消息发送到 SYSLOG。 |
| `-t <tracefile>` | 将调试信息重定向到 `<tracefile>`，其中 `<tracefile>` 是系统上的日志文件。 |

## 第 7 章：SMTP 和 POP

| 参数 | 说明 |
| :--- | :--- |
| `-s` | 启用记录每个连接的统计信息到 SYSLOG。 |
| `-T <timeout>` | 更改连接超时时间 `<timeout>` 秒。 |
| `-b <buldir>` | 指定用于存放公告的目录。默认是 `/var/spool/mail/bullets`。 |

### 使用 popauth

默认情况下，POP 服务器以明文发送所有密码。如果你关注安全，使用这种方式是个糟糕的主意，因为密码是在网络中传输的。`qpopper` 支持这种二进制格式的数据库。当你安装 `qpopper` 时，并没有创建 `/etc/pop.auth` 数据库。在使用 `auth` 之前，你需要用以下命令初始化数据库：

```bash
popauth -init
```

`popauth` 接受以下用于列表、删除和添加：

| 参数 | 说明 |
| :--- | :--- |
| `-list` | 显示数据库中的现有用户。 |
| `-delete <name>` | 从数据库中移除 `<name>`。 |
| `-user <name>` | 将用户 `<name>` 添加到数据库。 |

例如，要向数据库添加用户，使用：

```bash
popauth -user sshah
New password: scrubber
Retype password: scrubber
```

要查看用户是否已添加，输入：

```bash
popauth -list
```

如果你需要删除用户，可以使用如下 `delete` ：

```bash
popauth -delete sshah
```

警告：删除时不提示确认！

## 管理公告

偶尔，你可能需要向所有用户发送邮件以通知更改。（例如，你可能会发送这条信息：服务器周日离线。）如果你的大多数用户使用 POP 读取邮件，使用公告将极大减轻系统负担。

公告是在用户登录读取邮件时发送给所有人的消息。除非他们选择将邮件保留在服务器上，否则不会递送到用户的邮件队列。通过公告发送邮件，你可以减少服务器负载。

要创建公告，只需在 `/var/spool/mail/bulletins` 目录（或使用 `in.qpopper` 的 `-b` 选项指定的目录）创建一个新文件，文件名以数字开头，后跟一个点，然后是任意字符串。考虑这个示例：

`1.welcome_to_our_pop_server`

这可以是系统上的第一个公告。每个公告必须按照顺序编号。下一个公告可以是

`2.notice_of_downtime`

每个文件中必须包含客户端 POP 处理所需的必要邮件头信息。最小的邮件头仅包含 From 行；然而，用户将收到来自无人、且没有地址的邮件。因此，更好的邮件头不仅包含 From，还包含 Date、Subject 和 Reply-To: 头部信息。

以下是示例消息：

```text
From sshah@domain.com Tue Sep 16 20:31:15 1997
From: sshah@domain.com (Steve Shah)
Date: Tue, 16 Sep 1997 20:31:15 -0700
Subject: New compute server
Reply-To: sysadmins@domain.com
```

## SMTP 与 POP

第 7 章

大家好，

为了供大家参考，我们终于设置好了新的双处理器计算服务器。

（旧的单处理器服务器已经变得很寂寞了。;) 如果你有任何问题或故障，请随时给我发邮件或拨打分机 x9433。

- 您的系统组

当文件到位后，你不需要通知服务器，因为服务器会在用户登录读取邮件时，自动将文件发送给所有用户。

## 总结

在本章中，你学习了如何安装、设置和配置 `sendmail` 和 `qpopper` 程序。关于此过程需要记忆的关键点如下：

- MTA 是邮件传输代理（实际负责路由和投递邮件的程序），而 MUA 是邮件用户代理（用户在邮件投递后用于访问邮件的程序）。`sendmail` 仅是 MTA。
