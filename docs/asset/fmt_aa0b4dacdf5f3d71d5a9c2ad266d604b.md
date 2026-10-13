
| `AllowFilter` regular-expression | 允许配置正则表达式，所有发送到 ProFTPD 的命令都必须匹配此表达式。 |

| `AllowUser` user-expression | 允许访问的用户。 |

| `<Anonymous root-directory>` | 创建匿名 FTP 登录，由对应的 `</Anonymous>` 指令结束。root directory 参数是 proftpd 首先移动到的目录，然后 chroot 到该目录，从而隐藏文件系统的其余部分。 |

| `Bind` address | 允许将额外的 IP 地址绑定到主配置或 VirtualHost 配置。可以使用多个 `Bind` 指令来绑定多个地址。 |

| `DefaultRoot` directory [group-expression] | 登录时分配给用户的默认根目录。group-expression 参数限制 `DefaultRoot` 指令仅适用于某个组或一组组。默认：`DefaultRoot /` |

| `Deny` ["from"] "all"|"none"|host|network[,host|network[...]] | 明确拒绝访问给定 `<Limit>` 上下文块的主机和网络列表。all 表示拒绝所有主机访问，none 表示没有明确拒绝的主机。 |

| `DenyAll` | 拒绝访问目录、匿名 FTP 或 Limit 块。 |

| `DenyFilter` regular-expression | 指定一个正则表达式，任何命令都不得匹配此表达式。 |

| `DenyUser` user-expression | 在 Limit 块内拒绝访问的用户。 |

| `<Directory pathname>` | 特定目录的配置。用于创建适用于指定目录及其子目录的指令块。 |

| `DisplayLogin` filename | 指定登录时显示给用户的文本文件。 |

| `<Global>` | 全局配置块 |

| `<Limit command|command-group [command2 ..]>` | 在给定上下文中对 FTP 命令的访问限制。command-group 指的是 ProFTPD 文档中定义的命令分组。 |

| `LsDefaultOptions` "options string" | 目录列表的默认选项（类似于 ls 命令）。 |

| `MasqueradeAddress` host | 指定 FTP 服务器的公共主机名。用于通过 NAT 表（数据包过滤）进行伪装的 FTP 服务器。参见第 19 章。 |

| `MaxClients` number|none message | 允许的连接客户端最大数量。当拒绝客户端连接时，将显示指定的消息。 |

### 表 21-4：ProFTPD 配置指令，proftpd.conf

| 指令 | 描述 |

|---|---|

| `MaxLoginAttempts` number | 在给定连接期间，客户端向服务器登录的最大尝试次数。 |

| `Order` allow, deny|deny, allow | 配置在 `<Limit>` 块内检查 Allow 和 Deny 指令的顺序。默认值：`Order allow,deny` 上下文：`<Limit>` |

| `PersistentPasswd` on|off | 当设置为 on 时，proftpd 在登录期间会打开系统范围的 `/etc/passwd`、`/etc/group` 文件，即使在更改根目录的 chroot 操作期间也会访问这些文件。 |

| `ServerAdmin` "admin-email-address" | 服务器或虚拟主机管理员的电子邮件地址。 |

| `ServerType` type-identifier | 服务器守护进程的运作模式，即 inetd 或 standalone（独立模式）。 |

| `TimeoutIdle` seconds | proftpd 允许客户端在没有任何活动的情况下保持连接的最大秒数。默认值：`TimeoutIdle 600` |

| `Umask` octal-mask | 应用于给定上下文中新创建的目录和文件的权限。 |

| `User` userid | proftpd 守护进程运行时的用户身份。 |

| `UserAlias` login-user userid | 将客户端使用的登录名映射到服务器上的用户 ID。登录名为 login-user 的客户端实际上是以 userid 身份登录的。通常用于 `<Anonymous>` 块内，允许指定的登录名执行匿名登录。 |

| `<VirtualHost address>` | 适用于特定主机名或 IP 地址的配置指令。通常与运行在同一物理机上的虚拟服务器配合使用。该块由 `</VirtualHost>` 指令终止。 |

#### 华盛顿大学 FTP 守护进程：WU-FTPD

华盛顿大学 FTP 服务器虽然应用广泛，但不再包含在 Red Hat 9 及更高版本中。华盛顿大学 FTP 守护进程的名称为 `wu-ftpd`；必须运行该进程才能允许远程用户通过 FTP 访问。与其他服务器一样，你可以选择让 FTP 服务器在启动时运行，通过 `xinetd` 在接收到请求时启动，或者直接通过命令行启动。默认情况下，`wu-ftpd` 服务器被安装为使用 `xinetd` 运行。`xinetd` 在服务器中的应用在第 20 章中进行了详细说明。`xinetd` 调用的 FTP 服务器命令名称为 `in.ftpd`。这是一个指向 `wu-ftpd` 命令的链接。`xinetd` 会运行位于 `/etc/xinetd.d` 目录中名为 `wu-ftpd` 的文件。

你可以使用多种配置选项来满足你网站对 FTP 服务器的特定需求。WU-FTPD 使用位于系统 `/etc` 目录下的多个配置文件。所有这些文件均以 ftp 开头。主配置文件名为 `ftpaccess`。在此处，你可以提供基本的服务器信息以及对指定目录的访问权限。`ftphosts`、`ftpusers` 和 `ftpgroups` 文件控制基于系统、特定用户和组群的访问权限。`ftpconversions` 指定在文件传输前后执行归档和压缩操作的方式。`xferlog` 是存储服务器执行的所有交易运行日志的日志文件。

#### ProFTPD 和 WU-FTPD 服务器工具

WU-FTPD 和 ProFTPD 守护进程都提供了一组可用于管理 FTP 服务器的 FTP 工具。使用 `ftpshut` 命令，你可以平滑地关闭正在运行的服务器，并在发生之前提前通知用户。`ftpwho` 可以告诉你当前谁已连接以及他们正在做什么。`ftpcount` 可以给出当前生效的连接数量。虽然每个守护进程都有自己的工具集，但它们在很大程度上使用相似的选项集执行相同的操作。ProFTPD 和 WU-FTPD 提供的工具具有相同的名称和选项，尽管 ProFTPD 提供了有关虚拟主机的更多信息，并且增加了一些额外的选项。

##### ftpshut

使用 `ftpshut` 命令，你可以让 FTP 服务器在指定时间关闭，而不是通过终止其进程突然将其关闭。这给了你通知用户服务器即将关闭的机会，并提醒他们不要开始长时间的下载。`ftpshut` 提供了几个选项用于指定时间并包含警告消息。`ftpshut` 接收的参数为距离关闭的时间，后跟你想发送给用户的警告消息。时间可以是一个单词，例如 "now"（立即关闭），一个加号加上剩余的分钟数，或者以 HHMM 格式表示的特定一天中的时间，其中 HH 是 24 小时制的小时，MM 是分钟。以下示例将在十分钟后关闭 FTP 服务器，并向用户发出警告：

```
ftpshut +10 "Shutdown in ten minutes"
```

在计划关闭前 10 分钟，关闭操作将禁用任何新的 FTP 访问，尽管可以使用 `-l` 选项和你想要的分钟数来更改此设置。在计划关闭前 5 分钟，所有当前连接将被断开。你可以使用 `-q` 选项调整时间。警告消息格式化为 75 个字符，你可以使用特殊格式符号在警告消息中就地替换某些值，例如关闭时间。这些符号被称为 `magic cookies`。例如，`%s` 是关闭时间，`%r` 是新连接被拒绝的时间，`%d` 是当前连接被切断的时间，`%M` 是最大用户数，`%l` 是本地主机名。

##### ftpwho 和 ftpcount

使用 `ftpwho` 命令，你可以查明当前谁已连接到你的 FTP 服务器。`ftpwho` 显示每个用户的当前进程信息。输出显示五个字段：进程 ID、tty 连接、连接状态、该进程目前为止使用的 CPU 时间量以及连接详情。连接状态为 R（运行中）、S（睡眠中）和 Z（崩溃）。连接详情包括连接来源的互联网地址、建立连接的用户以及当前正在执行的任务，例如下载文件。该字段以 FTP 守护进程的名称开头，通常是 `ftpd`，随后是以冒号分隔的不同片段。

`ftpcount` 命令显示连接到你的 FTP 服务器的用户数量，并根据 `.ftpaccess` 文件中指定的类别进行分解。除了用户数量外，它还显示允许连接的最大数量。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_495_0.png)
