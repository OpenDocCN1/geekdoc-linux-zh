
`sabook:include:/usr/local/mail/lah.readers`

`lah.readers` 文件应该位于本地文件系统中，而不是 NFS 文件系统上，¹⁴，并且应该只允许其所有者写入。为了彻底起见，我们应该为邮件列表的所有者包含别名，这样错误（退回）就会发送给列表所有者，而不是发送给该列表邮件的发送者：

`owner-alias: evi`

- 12. 默认跳数限制为 25，但你可以在配置文件中更改它。
- 13. 我们在本章中的术语使用不一致，有时将返回的邮件称为“bounce”，有时又称为“error”。我们真正的意思是已经生成了投递状态通知（DSN）。此类通知通常意味着邮件无法投递，因此返回给发送者。
- 14. 如果 NFS 文件系统是以“硬性”模式挂载的且 NFS 失败，`sendmail` 将由于多个文件和打开的等待进程而阻塞。你最终可能会耗尽进程 ID 或文件句柄，并且必须重启机器来清理现场。

![](img/cb325d29f74eb66e46eaf8d38883ecfe_585_0.png)

### 别名示例

以下是系统管理员可能使用的一些典型别名。

- # 必要的别名^{16}
`postmaster: trouble, evi`
`postmistress: postmaster`
`MAILER-DAEMON: postmaster`
`hostmaster: trent`
`abuse: postmaster`
`webmaster: trouble, trent`
`root: trouble`

- # 用于本地 trouble 别名的 include
`trouble:include=/usr/local/mail/trouble.alias`
`troubletrap:"/usr/local/mail/logs/troublemail"`
`tmr. trouble:include=/usr/local/mail/tmr.aliases`

- # 系统管理员便利工具
`diary: "/usr/local/admin/diary"`
`info: "/usr/local/bin/sendinfo`

- # 每学期变化的类别别名
`sa-class:real-sa-class@nag`
`sa-class:include=/usr/local/admin/sa-class.list`

在这个示例中，我们希望来自整个校区的用户在发生问题时都能将邮件发送到单一别名“`trouble`”。问题报告应该路由到本地系统管理员组。特别地，我们需要设置别名以便：

- 邮件始终发送到相应的组。
- 所有主机都使用单一版本的 `aliases` 文件。
- 个人管理员组控制他们自己的分发列表。
- 所有邮件的副本发送到每个组的日志文件中。

上述配置通过从每台机器上的文件获取 `trouble` 别名的定义来实现这些目标。发送到 `trouble@anchor` 和 `trouble@bound` 地址的邮件即使使用相同的 `/etc/mail/aliases` 文件也会进入不同的地方。

邮件通常在每个位置的某个特定机器上处理。例如，从机上的 `trouble.alias` 文件可以包含地址：

```
trouble@master
```

为了使 `trouble` 邮件被解析，它会被发送到代表“邮件读者”的别名 `tmr`。`tmr` 将消息归档到 `troubletrap` 并且：

- 16. 根据 RFC，只有 `postmaster` 和 `MAILER-DAEMON` 是真正强制要求的，但包含 `hostmaster`、`abuse` 和 `webmaster` 是惯例。

### 18.4 别名

发送到从主机上的文件获取的用户列表。将新手管理员添加到 `tm` 列表是让他们看到出现的问题、管理员的回复，以及与用户（即客户）交流时应使用的适当奉承语气的好方法。

`sa-class` 别名有两个级别，使得包含学生列表的文件只需要在单台机器（`nag`）上维护。第 546 页的 `sabook` 别名示例应该具有这种类型的方向，以便文件不需要复制。

`diary` 别名是一个方便的工具，对于那些反感记录自己工作的学生系统管理员来说，它是一种很好的文档提取技术。系统管理员可以通过将邮件发送到 `diary` 文件来轻松记录机器生命中的重要事件（操作系统升级、硬件更改、崩溃等）。不要将该文件放在包含日志文件的文件系统中；否则将允许黑客填满文件系统并防止 `syslog` 写入日志条目（掩盖踪迹）。

### 转发邮件

`aliases` 是一个由管理员维护的系统级配置文件。如果用户想要路由自己的邮件（且你的站点没有使用 POP 或 IMAP 访问邮件），他们可以通过在家目录中创建 `forward` 文件来实现。`sendmail` 始终会在用户的家目录中查找 `forward` 文件，除非设置了 `ForwardPath` 并覆盖了默认位置。当用户想要接收邮件时，使用 `forward` 文件是非常方便的。

`sendmail` 有一个 `notify` 功能 `FEATURE(redirect)`，有助于管理永久更改。如果别名指向 `user@newsite`，邮件将带有新地址通知返回给发送者，因此发送者必须更新其地址。

你可以配置 `sendmail` 支持 `.forward` 文件的中央目录，但用户并不期望这种配置。`.forward` 文件的位置由 `ForwardPath` 控制，它通常指向家目录以及第 572 页所示的 `generic.m4` 文件。

全局 `aliases` 中的项于 `.forward` 文件中的项。由于这些文件由不同的人维护，用户必须小心不要创建邮件循环。如果网络上的用户有一个邮件（因此在全局 `aliases` 文件中有项），他们不能使用 `.forward` 文件重定向到共享相同别名的另一台机器。例如，在科罗拉多大学，我们使用站点级别名，如下：

`evi@boulder`

以及 `boulder` 机器上包含 `evi@anchor.cs` 的 `.forward` 文件将创建一个循环。发送给 `evi` 的邮件将被转发到 `boulder`，那里 `.forward` 文件将使其位于子域名。`anchor` 上的 `aliases` 文件将将其返回到 `boulder`，在 25 次跳数后，邮件将返回给发送者。

如果你的主要通信方式是电子邮件，通知用户邮件循环是挑战性的。邮件到 `\user` 将消息传递到本地机器，无论系统级别名文件或用户的 `.forward` 文件如何说。如果本地机器是用户期望读取邮件的地方，那就很好；否则，发送邮件给 `postmaster` 以报告循环或拨打电话。

- 17. 你可能需要使用两个或多个反斜杠才能让其中一个通过 shell 并进入 `sendmail`。

## 第 18 章 — 电子邮件

应当包含的系统级别名。它还包含了在伯克利如何路由某些常见用户请求的建议和示例。

`sendmail` 通过计算邮件头中 `Received` 行的数量来检测可能导致邮件往复转发的循环，并在计数达到预设限制（25）时将其返回给发送者。¹² 在 `sendmail` 的术语中，每访问一台新机器都被称为一次“跳数”（`hop`）；将邮件返回给发送者被称为“退回”（`bouncing`）。¹³ 上一句话如果用专业的术语表达，应该是：“邮件在 25 次跳数后退回。”¹³

除了用户列表外，别名还可以指向：

- 一个包含地址列表的文件
- 一个应该将消息追加其中的文件
- 一个应该将消息作为输入的命令

由于邮件的发送者完全决定了其内容，这些投递目标经常被黑客滥用。`sendmail` 对此类文件和命令的所有权和权限变得非常挑剔。为了覆盖 `DontBlamemail` 的偏执狂，你必须设置 `DontBlamemail` 选项之一，这并不是为了阻止你这样做。`sendmail` 在遇到不安全的权限或所有权时产生的错误信息并不总是清晰的。

### 从文件获取邮件列表

`include:` 指令是管理自定义邮件列表的一种极佳方法。它允许别名的成员从外部文件获取，而不是直接写在别名文件中。该文件可以在本地进行更改，而无需负责全局别名的系统管理员干预。

在设置列表时，系统管理员必须在全局别名中输入该别名，创建被包含的文件，并将包含文件的所有权（`chown`）移交给维护邮件列表的用户。例如，`aliases` 文件可能包含：

```
sabook:include:/usr/local/mail/lah.readers
```
