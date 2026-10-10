
永远记住：这是一个巨大的迪斯科世界。

通常，邮件客户端会为我们提供便利，解析信息并以比此处显示的形式更易读的方式呈现。但通过这个示例，你可以了解发件人是谁、主题行以及消息的日期。此时，你可以随意发出许多 RETR 命令来读取你的邮件。读取邮件不会导致其被删除。要删除邮件，你必须显式发出带有指定消息编号参数的 `DELE` 命令。既然我们已经读取了消息 1，我们可以通过输入以下命令来删除它：

```
DELE 1
```

服务器会返回以下响应：

```
+OK Message 1 has been deleted.
```

与 RETR 命令类似，你可以根据需要发出多次 DELE 命令。实际上，只有当你使用 QUIT 命令结束会话时，消息才真正被删除。就这样。现在，你对 POP3 命令的了解已经足够，能够测试服务器，并在必要时在没有适当邮件客户端的情况下阅读邮件！

## 知道何时需要帮助

*我需要定期阅读我的邮件。* 几年前的一次经历比任何事都更清楚地证明了这一点。我主目录所在的服务器宕机了，导致我无法登录。这是一个我没有管理员权限的系统，所以我不得不等待系统管理员修复服务器。在感到沮丧时，我下载了 POP3 的 RFC 规范（RFC 1939，http://ftp.isi.edu/in-notes/rfc1939.txt），从中我找出如何通过 POP3 命令和 Telnet 来阅读我的邮件。我耐心地用这种方法阅读了所有的邮件（几十条消息），甚至通过 Telnet 直接向 SMTP 服务器发出 SMTP 命令回复了几封邮件。当系统管理员到达时，我早已阅读并回复了早上所有的电子邮件。虽然令人遗憾，但这是事实……

## POP 与其他协议之间的冲突

IMAP 是另一种邮件客户端可用于访问服务器上存储邮件的协议。尽管它具有与 POP 类似的特性，但请记住，IMAP 是一种不同的协议，需要自己的服务器守护进程来服务请求。

> **注意：** 如果用户试图同时使用 POP 邮件客户端和 IMAP 邮件客户端，作为管理员，你可以预期会收到恢复其邮件存储的请求。由于 POP 和 IMAP 是独立的协议，它们的服务器守护进程也将独立运行。因此，如果两者同时启动并读取相同的邮件存储，文件损坏是可能的结果。在引入新用户到你的系统时，提醒他们永远不要同时使用两个邮件客户端。

当人们使用如 Pine、Elm 或 Mutt 等直接读取磁盘上邮件存储的邮件客户端时（通常通过 NFS 挂载的存储磁盘；有关更多信息，请参见第 18 章关于网络文件系统的内容），就会发生此类冲突。这些客户端会复制存储文件，执行所有更改，然后重写存储文件。如果在该过程进行中使用了另一个邮件客户端，可能会发生文件损坏。更有可能的是，用户会丢失消息或看到旧消息重新出现。

## QPOPPER

你的 Linux 发行版很可能已经附带了某种版本的 POP3 服务器。虽然你很少需要更新 POP3 守护进程，但你仍然应该知道如何操作。在本节中，我们将介绍下载、编译和安装 QPopper 的过程。UNIX 版本来自高通公司的 Eudora 部门，是免费的。最新版本 2.53 可在 ftp://ftp.eudora.com/eudora/servers/unix/poper/ 获取。

### 安装 QPopper

QPopper 最新的非 beta 版本非常稳定且可靠。我在生产服务器上使用了它一年多，尚未将系统故障归因于它。用户对“邮件服务器”的抱怨最终无一例外地追溯到他们的邮件客户端或某些网络问题。如今，你无法对许多软件说出这样的话！

所以，让我们从 ftp://ftp.eudora.com/eudora/servers/unix/poper/qpopper2.53.tar.Z 下载 QPopper 2.53 开始。记住要将其下载到一个足够大的目录以进行解包和编译。（/usr/local/src 是一个不错的选择。）

接下来，解压缩该程序。假设你将 QPopper 下载到了 `/usr/local/src`，你将使用以下命令进行解包：

```
[root@ford src]# uncompress qpopper2.53.tar.Z
```

当归档文件被解压后（qpopper2.53.tar），使用 tar 命令从归档文件中提取单独的文件，如下所示：

```
[root@ford src]# tar -xf qpopper2.53.tar
```

这将创建一个名为 qpopper2.53 的子目录，其中包含程序包中的所有源文件和文档。

### 编译 QPopper

在编译 QPopper 之前，你需要进行配置。QPopper 附带了一个 configure 脚本，可以替你完成大部分工作。它只需要你提供一些额外指令，其余部分会自动处理。如果你想查看所有配置选项，可以使用 `--help` 参数运行 `configure` 命令，如下所示：

```
[root@ford qpopper2.53]# ./configure --help
```

表 16-1 列出了可用于 `configure` 命令的选项。

| 配置选项 | 描述 |
| :--- | :--- |
| `--enable-apop=path`<br>`--with-popuid=user` | 这两个选项需配合使用。`--enable-apop=path` 选项启用经过身份验证的 POP（APOPOP）服务，这是普通 POP 的扩展。APOP 扩展允许用户以加密格式而非明文形式发送密码。`path` 参数指定认证文件存放的位置，通常是 `/etc/pop.auth`。`user` 参数指定拥有该文件的用户名。在此处，`bin` 用户是一个不错的选择。（APOP 数据库的配置将在本章后面讨论。） |
| `--enable-bulletins=path` | 公告是一种方便的机制，无需向所有邮箱发送相同消息即可向所有用户发布公告。相反，你只需编写一条消息，每个用户都会将其视为下次邮件下载的一部分。如果你有很多用户，这将节省磁盘空间和时间。`path` 是发布新公告的目录。有关公告的详细信息将在本章后面讨论。 |
| `--enable-servermode` | 服务器模式旨在使 QPopper 守护进程在高负载环境中更高效地运行。如果你有大量活跃用户，请考虑使用此选项。 |
| `--enable-specialauth` | 如果你使用影子密码，则必须使用此选项。（参见本章后面的“特殊认证”部分。） |

以下是启用经过身份验证的 POP（APop）、支持影子密码并建立服务器模式的配置行示例：

```
[root@ford qpopper2.53]# ./configure --enable-apop=/etc/pop.auth --with-popuid=bin --enable-specialauth --enable-servermode
```

当你运行 configure 脚本时，它会显示找到的所有信息。其中大部分涉及库和编译器支持问题，在此并不相关。

> **提示：** 在 configure 过程出错且你需要帮助的不太可能发生的情况下，请务必保存并使用脚本生成的信息。

QPopper 配置完成后，只需运行 `make` 命令来编译整个程序。即使在相对较慢的系统上，这也应该不到一分钟即可完成。`make` 命令：

```
[root@ford qpopper2.53]# make
```

完成后，你会得到两个二进制文件：`popper` 和 `popauth`。前者是实际的服务器守护进程，后者是管理 APOP 账户所需的工具。此外，你还将拥有 `popper` 和 `popauth` 的手册页。

尽管你可以选择将二进制文件安装到几乎任何地方，但将它们放在 `/usr/bin` 目录中是最有意义的，因为该目录还保存着许多其他应用程序。以下是将 `popper` 和 `popauth` 复制到 `/usr/bin` 的命令：

```
[root@ford qpopper2.53]# cp popper /usr/bin
[root@ford qpopper2.53]# cp popauth /usr/bin
[root@ford qpopper2.53]# chmod 755 /usr/bin/popper
[root@ford qpopper2.53]# chmod 4755 /usr/bin/popauth
[root@ford qpopper2.53]# chown root:root /usr/bin/popper
[root@ford qpopper2.53]# chown root:root /usr/bin/popauth
```

> **注意：** 如果你在 `./configure` 语句中使用了 `--with-popuid` 选项，请确保该选项中指定的用户与 `/usr/bin/popauth` 程序中的用户相匹配。在此安装中，我假设你使用的是 `bin` 用户。如果需要，你可以将上述 `chown` 行中的 `bin` 更改为你指定的用户。

要安装手册页，我们将以 `.8` 结尾的文件复制到 `/usr/man/man8` 目录，如下所示：

```
[root@ford qpopper2.53]# cp *.8 /usr/man/man8
[root@ford qpopper2.53]# chown root:root /usr/man/man8/popper.8
[root@ford qpopper2.53]# chown root:root /usr/man/man8/popauth.8
[root@ford qpopper2.53]# chmod 644 /usr/man/man8/popper.8
[root@ford qpopper2.53]# chmod 644 /usr/man/man8/popauth.8
```

### 设置 QPopper

`QPopper` 服务通过 `inetd` 守护进程运行，我们在第 9 章中讨论过该守护进程。以下是你需要做的设置步骤：

- 移除其他 POP 条目 - 编辑 `/etc/inetd` 文件的第一步是移除可能为其他 POP 服务设置的现有条目。（例如，Red Hat Linux 预配置了一个 POP3 服务。）要移除现有条目，请查找对应于 `/etc/services` 文件中列出的 POP 服务器的服务名称。使用 `grep` 实用工具并指定搜索字符串可以快速找到此信息，例如：

```
[root@ford /root]# grep '110/tcp' /etc/services

pop-3                110/tcp                     # POP version 3
```

如果已经定义了服务名称，你会看到类似以下的一行：

