
| 危险等级 |
| :--- |
| 💀 💀 💀 |

最新版本的 Sendmail 具有许多大多数站点希望使用的安全选项。首先将讨论这些选项及其影响。然后解释如何启用它们。设置“`authwarnings`”选项将导致 `sendmail` 在检测到配置中某些不安全特性时发出警告。`Sendmail` 提供了 `VRFY`（验证）命令，任何互联网站点都可以使用它来询问您的 `Sendmail` 一个电子邮件地址是否有效。垃圾邮件发送者使用此来猜测电子邮件地址。他们会尝试 `joe`、`sally`、`smith` 等，记下哪些是有效的，以便日后发送垃圾邮件。黑客可以使用此技术确定账户名称，从而开始猜测密码，使他们的任务变得容易得多。`Sendmail` 不需要 fork 进程、锁定邮箱或执行其他耗时操作，这是一个对垃圾邮件发送者来说非常高效且快速的操作。您将需要移除这种效率，以便垃圾邮件发送者无法收割如此多的电子邮件地址。

> 用户的电子邮件名称可以与账户名称不同，以向黑客隐藏账户信息。`sendmail` 的 `/etc/alias` 文件可用于将传入电子邮件路由到适当的账户。对于传出电子邮件的翻译有多种选择。某些邮件程序使用 `$REPLYTO` 环境变量来指定发件人，如果该变量已定义。或者，您可以在适当的 `sendmail` 表中放置一个条目。

几乎所有站点都应禁用 `VRFY` 命令。这可以通过“`novrfy`”选项来完成。

`EXPN` 命令与 `VRFY` 命令相似，`EXPN` 会展开（显示）邮件别名和邮件列表的实际投递地址。这将允许你在以后决定从 Internet 屏蔽对该别名的访问时收集电子邮件地址。例如，要查看别名邮件列表展开后的内容（假设它存在），请向 `sendmail` 发送以下请求：

`EXPN all all`

此 `EXPN` 功能通过 "`noexpn`" 隐私选项被禁用。

同样，应指定 "`restrictmailq`" 隐私选项，以防止 `Mail` 告知任何询问者邮件队列中的内容。它只允许与邮件队列同组的用户查看此数据。

"`needmailhelo`" 隐私选项将要求客户端系统在接收邮件之前先使用 `HELLO` 命令进行身份标识。`HELLO` 命令会导致通过 `syslog` 记录发送系统的主机名和数字 IP 地址。如果发送系统正在运行（认证服务），用户名称或 UID 也会被记录。因此，任何恶作行径都可以追溯到肇事者。当然，如果肇事者拥有该发送系统，他们可以发送伪造数据。

默认情况下，`Sendmail` 不会限制守护进程在监听 25 端口时分叉的子进程数量。这允许通过在短时间内向你的系统发送大量消息来进行拒绝服务（DOS）攻击，从而使进程表或打开的文件描述符数量饱和。

当然，攻击者可以启动一个到 25 端口的 TCP 连接，让程序休眠，再启动第二个到 25 端口的 TCP 连接以生成第二个子进程，并如此重复。攻击者可以使用多个被攻陷的系统。

针对此 DOS 的解药是在 `/etc/sendmail.mc` 中添加 `confMAX_DAEMON_CHILDREN` 定义，指定你允许的最大同时子进程数。这将在生成的 `sendmail.cf` 文件中添加 `O MaxDaemonChildren=25` 这一行。参见表 3.1。

`sendmail` 程序与 Linux 的其他几个部分存在一个问题，包括 `named`、`ftpd` 和典型的 `telnet` 配置文件。这个问题在于 `sendmail` 会愉快地告诉任何询问者其版本号。这使得窃贼更容易知道针对哪些漏洞发起攻击。

同样，在 1980 年左右，帮助调试系统之间的兼容性问题是个好主意。但今天这是一个糟糕的主意。它允许窃贼攻击全球的邮件进程，并等待特定版本中发现新的漏洞。然后，他们立即知道可以攻入哪些系统。

解决方案是另一个“单行代码”。将问候消息更改为不包含告知 `Sendmail` 版本的 "`$v`" 宏或揭示 `sendmail.cf` 版本的 "`$z`" 宏。后者强烈暗示了 `sendmail` 程序可能处于的版本范围。可以使用文本编辑器从 `/etc/sendmail.mc` 文件中删除字符串 `$v` 和 `$z`。

要启用所有这些安全功能（建议这样做），请确保 `/etc/sendmail.mc` 包含表 3.1 中的所有条目。

### 表 3.1 Sendmail 安全选项

- `define(`confPRIVACY_FLAGS`, authwarnings nofrfp noexpn restrictmailq needmailhelo)`

- `define(`confMAX_DAEMON_CHILDREN`, 25)`

- `define(`confSMTP_LOGIN_MSG`, $j Sendmail Secure/Rabid; $b)`

编辑 `/etc/sendmail.mc` 后，执行以下 shell 命令以使更改生效：

```
m4 /etc/sendmail.mc > /etc/sendmail.cf
/etc/rc.init/sendmail restart
```

请注意，`m4` 是 Linux 和 UNIX 的通用宏处理器。`/etc/sendmail.mc` 文件包含主要定义文件 `/usr/lib/sendmail-cf/m4/proto.m4`。最常更改的项目列在 `/etc/sendmail.mc` 中；这是为了让系统管理员免于学习 `sendmail.cf` 文件具有挑战性的细节。`sendmail.cf` 文件现在由上述显示的 `m4` 命令生成；它不再被直接编辑。相反，要更改 `/etc/sendmail.mc` 中未列出的项目，需要编辑 `/usr/lib/sendmail-cf/proto.m4`。

要检查你的更改是否有效，以及 `VRFY` 和 `EXPN` 是否已被禁用，请通过 `telnet` 连接到 25 端口（`smtp`），并发出这些命令以验证 `sendmail` 是否拒绝执行和遵守它们：

```
telnet mail.pentacorp.com smtp
220-mail.pentacorp.com Sendmail Secure/Rabid; 6 Sep 2000 22:25
220 SMTP spoken here
VRFY foobar
252 Cannot VRFY user; try RCPT to attempt delivery (or try finger)
EXPN foobar
502 Sorry, we do not allow this operation
quit
221 mail.pentacorp.com closing connection
Connection closed by foreign host.
```

`Sendmail` 文档建议使用 `finger`，但同样，正如第 88 页“不要让别人知道你的指纹”中所讨论的那样，`finger` 服务也已被禁用。不幸的是，攻击者仍然可以剥夺他人在及时时机向该系统发送电子邮件的能力。这个问题没有很好的解决方案。当然，`ports` 程序或 `netstat` 会显示这是否是一个问题，因为它们会显示来自特定系统的许多到你 25 端口的连接。一旦发现此类问题，一条阻止来自违规系统流量的防火墙规则将在几秒内解决问题。

一种自动保护免受此问题影响的可行方法（仅适合勇敢者）是修改 `sendmail` 源代码，在其跟踪仍在运行的子进程数量的地方。在跟踪运行中子进程的表中，添加一个字段用于记录连接系统的 IP 地址（或主机名）。当收到新连接时，搜索该表并统计该地址的待处理连接数。如果超过某个值（例如允许连接数 `MaxDaemonChildren` 的一半），关闭端口并将其视为错误。

适当的响应应与超过 `MaxDaemonChildren` 时发生的响应相同。如果是合法连接，客户端系统将稍后重试。足够小的状态防火墙也能处理这个问题。有关配置 `Sendmail` 的在线文档可在以下位置找到：

- www.redhat.com/support/docs/RH-sendmail-HOWTO/book1.html

- www.sendmail.com

- www.sendmail.net

- www.sendmail.org

### 3.2.4 伪造邮件和新闻发送者地址

| 危险等级 | ☢ ☢ |

接收到的电子邮件或 Usenet 新闻（网络新闻）帖子中显示的发送者地址是由发送者的系统生成的。与 NFS 中的安全缺陷类似，这种数据传输方法可以追溯到 30 多年前，那时只有美国国防部提出的站点上的受信任研究人员在后来发展为 Internet 的网络上。伪造邮件消息的发送者名称甚至不需要访问权限，因为非特权邮件程序是 `sendmail` 的前端；它生成了这个地址。实际上，甚至不需要 `sendmail`。使用 `telnet` 并指定目的端口为 25（SMTP）而不是默认的 23 端口，就可以直接向接收者的系统注入伪造的邮件。当不可信的用户声称自己是其他人时，`Sendmail` 将生成“可能伪造”的错误。

伪造邮件的解决方案是认识到邮件头和新闻头很容易被欺骗，并且不要信任它们。使用 PGP 风格的签名和加密电子邮件，验证接收者拥有发送者未被欺骗的 PGP 风格公钥，且发送者拥有接收者的公钥。教育用户了解这一点非常重要。

### 3.2.5 所有垃圾邮件是从哪里来的？
