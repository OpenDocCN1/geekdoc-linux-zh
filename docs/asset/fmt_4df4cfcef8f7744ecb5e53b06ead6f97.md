
对于 IMAP 服务器，配置文件是 `/etc/xinetd.d/imap`。

```bash
service imap
{
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/imapd
    log_on_success += HOST
    log_on_failure += HOST
    disable = no
}
```

对于 POP3 服务器，配置文件是 `/etc/xinetd.d/pop3`。

```bash
service pop3
{
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/pop3d
    log_on_success += HOST
    log_on_failure += HOST
    disable = no
}
```

> ：你可以使用 `chkhconfig` 工具在 xinetd 下启用 IMAP 和 POP 服务器。例如，在 xinetd 下启用 IMAP 服务，只需使用 `chkhconfig`。这将 `/etc/xinetd.d/imap` 文件中的 `disable = yes` 改为 `disable = no`。

> ：如果你使用的是从源码编译并安装的 UW-IMAP 包，不要忘记更改 xinetd 配置文件中的 `server` 指令以反映正确的路径。在我们的示例中，编译的 IMAP 服务器二进制文件将是 `/usr/local/sbin/imapd`。

在告诉 xinetd 重新加载配置之前，你需要检查 `/etc/services` 文件是否包含 POP3 和 IMAP。如果 `/etc/services` 没有列出这些，只需添加以下几行：

```
pop3 110/tcp
imap 143/tcp
```

# Linux 系统管理：入门指南

最后，告诉 xinetd 重新加载配置。如果你正在使用 Fedora、RHEL 或 CentOS，可以通过以下命令完成：

```
[root@fedora-serverA ~]# service xinetd reload
```

如果你使用其他发行版，你可能通过向 xinetd 的运行控制传递 `restart` 参数来重启 xinetd，如下所示：

```
yyang@ubuntu-serverA:~$ sudo /etc/init.d/xinetd restart
```

如果一切运行正常，你将拥有一个功能完的 IMAP 服务器和 POP3 服务器。通过使用早些章节“POP 和 IMAP 基础”中显示的命令和方法，我们可以连接并测试基本功能。

> 提示：如果在此过程中遇到错误消息，请检查 `/var/log/messages` 文件以获取更多信息。

## 检查基础 POP3 功能

我们首先使用 Telnet 连接到 POP3 服务器（在本例中为 localhost）。在命令提示符中输入：

```
[root@serverA ~]# telnet localhost 110
Trying 127.0.0.1...
Connected to localhost.
Escape character is ']'
+OK POP3 localhost.localdomain 2006k.101 server ready
```

服务器现在正在等待你提供命令。（不用担心没有看到提示符。）首先按如下方式提交你的登录名：

```
USER login
```

其中 `login` 是你的用户 ID。服务器响应：

```
+OK User name, password please
```

现在使用 `PASS` 告诉服务器你的密码：

```
PASS yourpassword
```

其中 `yourpassword` 是你的密码。服务器响应：

```
+OK Mailbox open, <X> messages
```

其中 `X` 代表信箱中的邮件数量。你现在已经登录，可以发布命令读取邮件。由于我们只是在验证服务器是否正常工作，现在可以注出了。只需输入 `QUIT`，服务器将关闭连接。

## 第 20 章：POP 和 IMAP

```
QUIT
+OK Sayonara
Connection closed by foreign host.
```

就这些。

## 检查基础 IMAP 功能

我们首先准备使用 Telnet 连接到 IMAP 服务器（在本例中为 localhost）。在命令提示符中输入：

```
[root@serverA ~]# telnet localhost 143
```

IMAP 服务器将返回类似的内容：

```
* OK [CAPABILITY......OUTPUT TRUNCATED]...... localhost.localdomain
```

服务器现在已准备好输入命令。注意，POP 服务器不同，IMAP 服务器不会发出提示符。IMAP 命令的格式为：

```
<tag> <command> <parameters>
```

其中 `tag` 代表一个用于标识（标记）命令的唯一值。示例标签有 A001, box, c, box2, 3 等。命令可以异步执行，这意味着你可以在输入一个命令并在等待响应期间输入另一个命令。由于每个命令都带有标签，输出将清晰地反映什么输出对应于什么请求。

要登录 IMAP 服务器，只需输入 `login <username> <password>` 命令，如下所示：

```
A001 login <username> <password>……
```

其中 `<username>` 是你想要测试的用户名，`<password>` 是该用户的密码。如果身份验证成功，服务器将返回类似这样的内容：

```
A001 OK [CAPABILITY ...OUTPUT TRUNCATED]... User <username> authenticated
```

这足以告诉你两点信息：

- * 用户名和密码是有效的。
- * 邮件服务器能够定位并访问用户的信箱。

验证服务器后，你可以通过输入 `logout` 命令来注销，如下所示：

```
A002 logout
```

服务器将返回类似的内容：

```
* BYE servera.example.org IMAP4rev1 server terminating connection
A002 OK LOGOUT completed
```

## 邮件服务的其他问题

到目前为止，我们涵盖了足够让你开始运行一个工作邮件服务器的材料，但仍有很大的改进空间。在本节中，我们将逐步介绍你可能会遇到的一些问题以及解决这些问题的常用技术。

## SSL 安全

POP3 和 IMAP 服务器最大的安全问题是，在最简单的配置下，它们不提供任何加密。高级的 IMAP 配置提供了更丰富的密码哈希方案，并且大多数现代全功能电子邮件客户端都支持它们。尽管如此，最好的办法是尽可能使用安全套接层 (SSL) 加密整个数据流。

按照我们配置此 UW-IMAP 服务器的方式，为了保持首次安装简单，没有使用 SSL。在对其进行过度调整之前，知道可以先让它运行起来总是极好的！如果你想使用 SSL，需要采取以下步骤：

- 1. 启用 SSL 并重新编译 UW-IMAP。

更改 xinetd 配置文件，分别使用 `imaps` 和 `pop3s` 服务代替 `imap` 和 `pop3`。`imaps` 服务运行在 TCP 端口 993 上，`pop3s` 运行在 TCP 端口 995 上。

确保你的客户端使用 SSL。在 Outlook 中，此选项是“添加邮件”配置选项中的一个简单选框。根据你的安装情况，启用 SSL 重新编译可能需要更多调整。

# Linux 系统管理：学者指南

最后，在设计早期就要考虑扩展和增长。你的用户不可避免地会耗尽你所有可用的磁盘空间。你最不希望看到的是因为邮件服务器磁盘空间耗尽而手忙脚乱！为了解决这个问题，请考虑可以使用即时扩展的磁盘卷，而 RAID 系统允许快速添加新磁盘。这将使你能够以最小的停机时间向卷中添加磁盘，而无需迁移到完全全新的服务器。

# 日志文件

尽管我们在本章开头已经提到过这一点，但监控 `/var/log/messages` 和 `/var/log/mailog` 是管理和跟踪邮件服务器活动的一种明智方法。UW-IMAP 服务器提供了丰富的日志信息，帮助你理解服务器正在发生什么，并排查任何异常行为。

在本章中，日志文件的实用性有一个完美的例子，特别是在 SSL 节节中。在编译了服务器的新版本后，我们忘记将 `imapd` 文件复制到 `/usr/local/sbin`。这导致当我们尝试 Evolution（一个流行的开源电子邮件客户端）连接服务器时，产生了一个谜团。我们尝试使用 `openssl s_client` 命令进行连接，但得到了一个模糊的错误。到底发生了什么？

使用 `tail` 命令快速查看日志文件暴露了问题：
