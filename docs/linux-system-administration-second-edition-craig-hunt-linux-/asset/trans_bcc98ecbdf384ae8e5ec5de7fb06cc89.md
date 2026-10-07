

默认配置接受本地邮件进行中继；从技术上讲，当本地程序通过 sendmail 发送邮件时，它正在作为邮件中继服务器运行，因此如果您想要发送邮件，就需要此配置。

### REJECT
拒绝来自或发往指定域名的邮件。sendmail 会生成一个 *bounce*（退信）消息，以让发送者知道尝试失败。

### DISCARD
其行为与 REJECT 相同，只是 sendmail *不* 生成退信消息。

### nnn text
其行为类似 REJECT，但会向发送者返回错误代码 *nnn*，并附带 *text* 作为消息。

您可以按域名（如 badspammer.net）或按部分 IP 地址（如 192.168.98，这匹配 192.168.98.0/24 网络中所有计算机的 IP 地址）来指定域名。配置 sendmail 进行中继最安全的方法是按 IP 地址指定网络，因为 IP 地址比域名更难伪造。

假设您希望配置 sendmail 以中继来自 192.168.98.0/24 网络的邮件。您可以在 /etc/mail/access 中添加以下条目：

```
192.168.98 RELAY
```

然而，在使用此条目之前，您必须将文本模式的 /etc/mail/access 文件转换为二进制格式，该格式存储在 /etc/mail/access.db 中。您可以通过输入以下命令来完成此操作：

```
# makemap hash /etc/mail/access.db < /etc/mail/access
```

**提示** 在 Red Hat 上，您不需要执行 makemap 命令，因为 sendmail 启动脚本会自动执行此操作。如果您愿意，可以输入此命令以在不重启 sendmail 的情况下激活更改。

输入命令后，您可以重启 sendmail，届时它将配置为中继来自 192.168.98.0/24 网络的邮件。最好通过配置另一台计算机上的 MUA（邮件用户代理）使用您已调整的系统作为 outgoing（发件）邮件服务器来测试您的设置。您还应该从一台 *不* 应能使用该系统进行邮件中继的计算机执行相同操作，以检查是否使系统过于宽松。

## 接收邮件

Linux 可以接收通过 SMTP 发送的邮件，也可以发送邮件。为此，sendmail 必须以 *daemon mode*（守护进程模式）运行——也就是说，它必须始终处于运行状态，监视端口 25 上的连接。Sendmail 还必须配置为监听其网络接口上的连接。要在守护进程模式下运行 sendmail，必须使用 -bd 开关启动它，如 **sendmail –bd** 所示。这是 Red Hat 7.3 中 sendmail 的默认配置。您可以使用 `ps` 命令检查 sendmail 是否以此方式运行：

```
$ ps ax | grep sendmail
2536 ? S 0:00 sendmail: accepting connections
```

sendmail 正在“accepting connections”（接受连接）这一陈述表明 sendmail 确实以守护进程模式运行。如果不是这样该怎么办？在这种情况下，您必须手动启动 sendmail 或修改启动脚本。在 Red Hat 7.3 中，相关脚本是 /etc/rc.d/init.d/sendmail，但在其他发行版中，适当的脚本可能具有其他名称。您应该找到启动脚本中对 sendmail 的调用，并确保其包含 `-bd` 参数。对于 Red Hat 7.3，启动脚本根据在 `/etc/sysconfig/sendmail` 文件中设置的 `DAEMON` 变量的内容来设置此参数，该文件在 sendmail 启动脚本早期被加载。

某些 sendmail 配置，例如 Red Hat 7.3 的默认配置，忽略对端口 25 的访问尝试，除了来自 localhost 地址（127.0.0.1）的请求。此配置实际上阻止了传入邮件的接收。Red Hat 使用其 `/etc/mail/sendmail.mc` 文件中的以下行来创建此限制：

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
```

要启用服务器从其他计算机接收邮件，请找到此行并通过在行首添加 `dnl` 将其注释掉。然后您可以创建一个新的 `sendmail.cf` 文件并重启服务器。如果您希望 sendmail 中继邮件，您可能需要进行更多更改，如上一节“配置 Sendmail 为域名中继”中所述。

sendmail 接收邮件的另一个要求是，该程序被配置为接受以其已知机器名称为目标的邮件。例如，考虑虚构的邮件服务器 `pony.express.gov`。如果 `express.gov` 的 DNS 记录包含指向 `pony.express.gov` 的 MX 记录，那么尽管机器名称不是 `express.gov`，该机器必须接受发往 `express.gov` 的邮件作为本地邮件。幸运的是，这项任务很容易完成：您只需将计算机的别名添加到 `/etc/mail/local-host-names` 并重启 sendmail（在某些发行版中，此文件名为 `/etc/sendmail.cw`）。例如，以下 `/etc/mail/local-host-names` 文件指示系统接受发往 `express.gov` 和 `positif.gov` 的邮件，除了计算机用作其主机名的名称外：

```
express.gov  
positif.gov
```

您应该问自己的一个问题是您是否 *想要* 您的系统接收 SMTP 邮件。普通工作站不需要此功能，因为另一台计算机作为工作站用户使用的邮件服务器；工作站使用拉取邮件协议从服务器检索邮件。如果您的系统拒绝传入邮件，您仍然可以从本地程序发送邮件，但您需要使用拉取邮件协议接收邮件。如果系统不需要接收 SMTP 邮件，以这种方式进行配置是个好主意。这样做消除了坏人可能通过 sendmail 中的漏洞进入系统的可能性，同时也消除了垃圾邮件发送者滥用配置错误的系统中继垃圾邮件的可能性。

## 配置 POP 和 IMAP

幸运的是，设置 POP 和 IMAP 协议并不非常困难。与 sendmail 相比，许多 POP 和 IMAP 服务器需要的配置非常少。但是，如果您正在构建部门邮件服务器，您可能需要配置用户帐户，这可能需要进行一些思考。还可以将 Linux 系统用作 POP 或 IMAP 客户端。在许多情况下，您通过 MUA 执行此操作；但是，fetchmail 程序允许您获取 POP 或 IMAP 邮件并通过常规 Linux 邮件队列提供服务。

### 运行 POP 和 IMAP 守护进程

运行 POP 或 IMAP 的第一步是安装适当的服务器软件包。在 Red Hat 7.3 中，它被称为 `imap-2001a-10`，它包含 POP 和 IMAP 的服务器。其他发行版提供类似的软件包。

**注意：** 正如 sendmail 不是唯一的 SMTP 服务器一样，imap-2001a-10 软件包中包含的 POP 和 IMAP 服务器也不是唯一的 POP 和 IMAP 服务器。如果您使用 qmail 作为 MTA，您很可能需要寻找替代软件包，因为 qmail 将电子邮件存储在与大多数其他 MTA 不同的位置，这会令大多数 POP 和 IMAP 服务器困惑。qmail 网站包含指向与 qmail 配合使用的替代 POP 和 IMAP 服务器的链接。然而，Exim 和 Postfix 与标准 imap 软件包兼容。

POP 和 IMAP 守护进程通常由 *super server*（超级服务器）运行，如第 12 章所述。Red Hat 7.3 和 Mandrake 8.2 使用 xinetd 超级服务器，但 2002 年大多数其他发行版使用 inetd。这些程序的配置有所不同。

如果您的发行版使用 xinetd，/etc/xinetd.d 目录可能包含以 POP 和 IMAP 服务器命名的文件，如 imap、ipop2 和 ipop3。（这些文件随 imap 软件包安装，因此您安装 imap 之前不会看到它们。）安全变体使用文件名以 s 结尾的文件。第 12 章讨论了 /etc/xinetd.d 中文件的格式。默认情况下，这些文件包含如下行：

```
disable = yes
```

此行停用相关服务器。如果您希望运行 POP 或 IMAP 服务器，如果使用 xinetd，您需要做两件事来激活它：

- 1. 将 `disable = yes` 行更改为 `disable = no`，或完全删除该行，并保存更改。您可以仅针对一个服务器（例如 POP-3）或多个服务器执行此操作。
- 2. 通过键入 **/etc/rc.d/init.d/xinetd restart** 重启 xinetd。

如果您的发行版使用 inetd 而不是 xinetd，过程略有不同。您必须编辑 /etc/inetd.conf 文件以启用从 inetd 运行的 POP 或 IMAP 服务器。为此，请遵循以下步骤：

- 1. 在文本编辑器中打开 /etc/inetd.conf 文件并找到对应于您要启用的协议的行。它可能以井号和协议名称开头，如下所示：
  `# pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d`
- 2. 移除井号并保存结果。如果您愿意，可以针对多个协议执行此操作。
- 3. 通过键入 **/etc/rc.d/init.d/inet restart** 重启 inetd。

完成后，您的系统应已配置为选定的拉取邮件协议的服务器。您可以通过在另一台计算机上使用适当的 MUA 或使用 Telnet 程序手动测试服务器来测试该服务器，如清单 14.2 和 14.3 所示。

## 设置仅限邮件的帐户

通常，Linux 仅接受拥有服务器帐户的收件人的邮件。例如，如果邮件地址为 nemo@pony.express.gov，并且 pony.express.gov 没有名为 nemo 的用户，服务器将退回邮件——发送者会收到一条包含错误消息的消息，指出 nemo 不是有效收件人。因此，通常必须为所有电子邮件收件人创建用户帐户，即使计算机仅用作 *邮件服务器*。

