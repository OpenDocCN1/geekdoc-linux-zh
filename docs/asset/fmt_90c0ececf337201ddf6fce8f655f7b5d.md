
- 12. 什么命令处理 `/etc/mail` 中的所有文件？

## 实验问题

其中一些实验涉及配置练习。您应该仅在测试机器上执行这些练习。假设您在诸如 `KVM` 之类的虚拟机上运行这些练习。对于本章，还假设您可能正在更改此类虚拟机的物理主机系统的配置。

`Red Hat` 以电子方式提供考试。出于这个原因，本章及以后章节中的实验可从随书附带的 `CD` 中获得，位于 `Chapter13/` 子目录中。如果您尚未在系统上设置 `RHEL 6`，请参阅第 1 章以获取安装说明。

每个实验的答案在填空题的自测答案之后。

## 自测答案

### 多种电子邮件代理
- 1. `RHEL 6` 支持的三种 `MTA` 示例是 `Postfix`、`sendmail` 和 `Dovecot`。
- 2. 可以帮助在 `Postfix` 和 `sendmail MTA` 之间切换的命令是 `alternatives --config mta`。

### Postfix 配置
- 3. 最简单的解决方案是将指令更改为
  `inet_interfaces = all`
- 4. `sendmail` 和 `Postfix` 的转发电子邮件地址通常存储在 `/etc/aliases` 中。确保将这些文件处理为适当的数据库；对于 `/etc/aliases`，数据库使用 `newaliases` 命令进行更新。
- 5. 支持可以连接到 `Postfix` 的主机限制的文件是 `/etc/postfix/access`。
- 6. `main.cf` 文件中用于指定 `Postfix` 服务器提供的域的指令是 `mydomain`。
- 7. `main.cf` 文件中用于指定 `Postfix` 服务器提供的 `IP` 地址网络的指令是 `mynetworks`。
- 8. 您在 `/usr/share/doc/postfix-2.6.6` 目录中找到与 `Postfix` 服务器相关的文档。

### 另一项 SMTP 服务：sendmail
- 9. `sendmail` 和 `Postfix` 的转发电子邮件地址通常存储在 `/etc/aliases` 中。如果您为整个域转发电子邮件，适当的文件是 `/etc/mail/domaintable`。确保将这些文件处理为适当的数据库；对于 `/etc/aliases`，数据库使用 `newaliases` 命令进行更新。对于 `/etc/mail/domaintable`，数据库使用 `/etc/mail/make` 命令进行更新。
- 10. 如果您注释掉所述指令，则所有允许连接的系统都支持访问。
- 11. 如果您在 `sendmail.mc` 中注释掉所述指令，则不需要可靠的 `DNS` 服务器。
- 12. 处理 `/etc/mail` 目录中所有文件的命令是 `/etc/mail/make`。

## 实验答案

对于大多数这些实验，你可能使用像 `mutt` 这样的电子邮件客户端。要向用户 `michael@localhost` 发送电子邮件，请执行以下步骤：

- 1. 运行 `mutt michael@localhost` 命令。收件人：`michael@localhost` 消息应出现。
- 2. 按 `ENTER`。 在主题：提示符处，输入适当的测试主题名称并按 `ENTER`。
- 3. 你将被带到 `vi` 编辑器中的空白屏幕。使用该编辑器适当的命令将其调整为与图 13-5 所示类似的屏幕。
- 4. 从图 13-5 所示的屏幕中，按 `y` 发送所记录的消息。

此外，你可能在 `/var/spool/mail` 目录中按用户名命名的文件中验证电子邮件的接收。通常，此类电子邮件可以通过 `mail` 命令在用户账户内进行查看。此外，你可能使用 `telnet ip_address 25` 命令验证对正在运行的 `SMTP` 服务器的访问，其中 `ip_address` 是 `SMTP` 服务器的 `IP` 地址。

进行配置更改后，不要忘记适当地处理文件。对于 `Postfix`，`postmap filename` 命令处理文件。对于 `sendmail`，`/etc/mail/make` 脚本处理文件。对于通用的 `/etc/aliases` 文件，`newaliases` 命令处理文件。并且不要忘记确保服务实际重新读取新的配置文件。

### 实验 1

在 `Postfix` 中，要在 `/etc/postfix/main.cf` 文件中禁用仅本地访问，请将 `inet_interfaces` 指令更改为接受所有连接：

```
inet_interfaces = all
```

图 13-5

`mutt` 电子邮件客户端。

![](img/9139201cfcaf4292284a0eed074928e5_755_0.png)

但为了满足实验的要求，你希望保留该指令的默认值：

```
inet_interfaces = localhost
```

确保 `Postfix` 处于活动状态（并且任何替代邮件服务器如 `sendmail` 未运行）。通常，要验证 `SMTP` 服务器上的身份验证，请从本地系统使用 `telnet localhost 25` 命令进行连接。当你看到类似以下的消息时

```
220 maui.example.com ESMTP Postfix
```

输入以下命令：

```
EHLO localhost
```

根据配置，你应该会看到类似以下的消息：

```
250-AUTH LOGIN PLAIN
250-AUTH=LOGIN PLAIN
```

要验证用户账户中电子邮件的接收，请登录该账户，或至少验证 `/var/mail` 目录中与用户名关联的时间戳。为了确保发送给 `root` 用户的电子邮件被重定向到普通用户账户，你将在 `/etc/aliases` 文件中添加如下行：

```
root: michael
```

根据问题的措辞，任何标准用户账户都可以接受。当然，要实现此更改，你必须运行 `newaliases` 命令，该命令将此文件处理为 `/etc/aliases.db` 文件。

要使其工作，你希望使用命令行客户端，如 `mutt` 或甚至如第 2 章中定义的 `mail`。例如，如果你向本地 `root` 用户发送测试电子邮件，该消息应由用户 `michael` 接收（或 `/etc/aliases` 文件中配置为接收从 `root` 用户转发电子邮件的任何人）。

### 实验 2

要启用除 `localhost` 之外的更多访问，你需要在 `/etc/postfix/main.cf` 中修改 `inet_interfaces` 指令为

```
inet_interfaces = all
```

下一步工作是限制对特定网络的访问，在本例中为 `example.com`。虽然 `/etc/postfix` 文件中有选项，但限制对特定网络访问的最有效方法可能是使用适当的基于 `iptables` 的防火墙规则。例如，以下自定义规则将限制对 `TCP` 端口 25 的访问，仅限于给定 `IP` 地址网络上的系统。所示网络基于 `example.com` 的原始定义配置，即 `192.168.122.0/24` 网络：

```
-A INPUT -m state --state NEW -m tcp -p tcp -s 192.168.122.0/24 --dport 25 -j ACCEPT
```

此外，你需要在 `/etc/postfix/access` 文件中为此网络设置如下规则：

```
192.168.122 OK
```

一旦 `Postfix` 运行，你应该能够从远程系统使用适当的 `telnet` 命令确认结果。例如，如果 `Postfix` 配置在 `IP` 地址为 `192.168.122.50` 的系统上，命令将是

```
# telnet 192.168.122.50 25
```

`Postfix` 中智能主机的配置基于 `relayhost` 指令。对于实验中给出的参数，如果物理主机位于系统 `maui.example.com` 上，则 `main.cf` 文件中的指令将是

```
relayhost = maui.example.com
```

如果服务器 `r.example.com` 系统上的 `Postfix` 被正确配置为智能主机，则转发主机的电子邮件应可靠交付，甚至记录在适当的 `/var/log/maillog` 文件中。

### 实验 3

使用实验 2 中所示的 `iptables` 规则，来自其他网络的访问应已被禁止。然而，如果你在实验 2 答案中所示的 `iptables` 规则中未包含 `192.168.122.0/24` 网络地址，则有另一种方法可用。你可以使用 `/etc/postfix/access` 文件中可用的选项，例如以下内容拒绝来自 `example.org` 网络的消息。如果你的 `example.org` 网络使用不同的 `IP` 地址，请相应修改。

```
192.168.100 REJECT
```

从远程系统验证到 `SMTP` 服务器的连接应该很容易。从禁止的网络中，当你从 `192.168.100.0/24` 网络的主机运行类似以下命令时：`telnet 192.168.122.50 25`，你应该会看到以下输出：

```
Trying 192.168.122.50...
telnet: connect to address 192.168.122.50: No route to host
```
