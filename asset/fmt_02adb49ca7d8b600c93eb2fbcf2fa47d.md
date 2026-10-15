
| 权限 | 所有者 | 组 | 大小 | 日期 | 名字 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| -rw-r--r-- | gbush | gbush | 8470 | Jan 10 2000 | LinuxUnashed.gif |
| -rw-r--r-- | gbush | gbush | 4407 | Oct 4 2000 | RHU72ed.gif |
| -rw-r--r-- | gbush | gbush | 6732 | May 18 2000 | SuSEUnleased.gif |
| -rw-r--r-- | gbush | gbush | 6175 | Jan 10 2000 | TYSUSE.gif |
| -rw-r--r-- | gbush | gbush | 3135 | Jan 10 2000 | TZones.gif |

> 注意
> 访问 http://slacksite.com/other/ftp.html 查看到关于主动和被动 FTP 模式，以及防火墙阻塞服务端口对 FTP 服务器和客户端连接影响的详细讨论。

特定用户登录控制的其他默认设置未设置，但你可以配置控制项以拒绝一个或多个用户的访问。

匿名客户端访问的数据传输速率是无限的，但可以使用 `vsftpd.conf` 中的 `anon_max_rate` 设置设置最大速率（字节/秒）。这对于在活动高峰期间限制带宽使用非常有用。另一个默认设置是远程将在五分钟后注销。其他特定用户登录控制的默认设置未设置，但你可以配置控制项以拒绝一个或多个用户的访问。

- `anon_max_rate` — 使用 `vsftpd.conf` 中的 `anon_max_rate` 设置最大速率（字节/秒）。这对于在活动高峰期间限制带宽使用非常有用。
- `dirlist_enable` — 启用目录列表。
- `dirrecurse_enable` — 启用递归目录列表。
- `download_enable` — 启用下载。
- `max_clients` — 限制连接数。
- `max_per_ip` — 限制 IP 地址。

> 注意
> 访问 http://slacksite.com/other/ftp.html 查看到关于主动和被动 FTP 模式，以及防火墙阻塞服务端口对 FTP 服务器和客户端连接影响的详细讨论。

- 访问控制—确定谁可以访问 FTP 服务器以及如何访问服务器的设置。
- 信息—确定服务器提供哪些信息或向用户显示哪些信息的设置。
- 日志—确定是否启用日志以及记录哪些信息的设置。
- 权限控制—控制用户访问服务器时的行为的设置；换句话说，就是允许用户执行哪些操作，例如创建目录、上传文件、删除文件或目录等。

> `wu-ftpd` FTP 服务器可以在其 `ftppass` 文件中指定许多更多选项。这里涵盖了最常用的命令。在安装服务器后，您可以在 `ftppass` man 页面中找到完整的配置选项列表。

你可以在命令行中编辑 `ftppass` 文件，以对这些类别中的任何一个进行配置更改。以下章节描述了某些配置更改以及如何编辑这些文件来实现这些更改。

## 配置访问控制

控制哪些用户可以访问 FTP 服务器以及他们如何访问是系统安全的关键部分。请使用 `ftppass` 文件中的以下条目来指定访问服务器的用户被分配到哪个组。

### 限制匿名用户的访问

此命令对匿名用户实施了更强的安全性：

```
autroup <username> <class> [<class>]
```

如果匿名用户是某个组的成员，他将仅允许访问其或其组拥有的文件和目录。该组必须是 `/etc/groups` 或 `/var/ftp/etc/groups` 中的有效组。

### 定义用户类

此命令根据用户连接的地址定义一类用户。

```
class <class> <typelist> [<addrglob>]
```

一个用户类可能有多个成员，而多个类也可能适用于单个成员。当多个类适用于一个用户时，将使用第一个适用的类。

## 在 ftppass 文件中使用命令配置 wu-ftpd

`type` 字段是关键词 `anonymous`、`guest` 和 `real` 关键字的逗号分隔列表。`anonymous` 适用于匿名用户，`guest` 应用于通过 `guestgroup` 指令指定的访客访问账户。`real` 定义了那些在 `/etc/passwd` 文件中具有有效条目的的用户。

`addr` 字段是一个正则表达式，指定了应用该类的地址。`deny (*)` 条目指定所有主机。

### 阻止主机对服务器的访问

有时有必要阻止整个主机访问服务器。这对于保护系统免受单个主机或整个 IP 地址段的影响，或强制使用其他用户有用。使用以下命令来实现：

```
deny <addrglob> <message_file>
```

`deny` 将始终拒绝匹配给定地址的主机。
`addr_glob` 是一个正则表达式字段，包含一个地址列表，可以是数字，也可以是 DNS 名称。该字段也可以是一个文件引用，包含一个地址列表。如果地址是文件引用，它必须是绝对文件引用；即以 `/` 开头。为了确保 IP 地址映射到有效的域名名（注：此处原文可能存在断词或缺失），将在 `Name-server` 参数中显示消息。

一个 `deny` 示例所示：

```
deny *.exodous.net /home/ftp/.message_exodous_deny
```

此条目将拒绝所有来自 `exodous.net` 域名的用户访问 FTP 服务器，并显示位于 `/home/ftp` 目录的文件 `.message_exodous_deny` 中包含的消息。

| FTUSERS 文件用途 | 目前在 FTPACCESS 中的实现 |
| :--- | :--- |
| 在安装 Linux 期间创建了某些账户，以便系统能够划分和分离具有特定权限的任务。`ftusers` 文件（位于 `/etc/ftusers`）列出了用于系统目的的账户。 | 你用于 Fedora 版本的 wu-ftp 可能已弃用了该文件的使用，转而通过 `ftppass` 文件中的 `deny-<uid>/deny-gid` 命令实现了该文件的特定功能。 |

### 根据组 ID 限制权限

`guestgroup` 行将组名或多个组名分配出去，使其行为与匿名用户完全相同。以下是该命令：

```
guestgroup <groupname> [<message_groupname>]
```

## 第 18 章 安全文件传输协议 (FTP) 服务

此命令将用户限制在特定的目录结构中，方式就像匿名用户被限制在 `/var/ftp` 一样。此命令还限制这些用户访问其所属组具有访问权限的文件。

`groupname` 参数可以是组的名称，也可以是该组相应的 GID（组 ID）。如果你使用 GID 作为 `groupname` 参数，请在它前面加上百分比符号 (`%)。你可以使用此命令为范围组 ID 分配权限，例如所示：

```
guestgroup %500-550
```

此条目将限制组 ID 为 500–550 的所有用户作为访客组，而不是个人用户。为了让每个 `guestgroup` 起作用，你必须以正确的权限设置用户的主目录，就像设置匿名 FTP 用户完全一样。

### 根据个人 ID 限制权限

`guestuser` 的工作与你刚刚看到的 `guestgroup` 命令完全相同，除非它指定的是用户 ID (UID) 而不是组 ID。以下是该命令：

```
guestuser <username> [<username>]
```

此命令将用户限制在其拥有权限的文件上。通常，用户的权限比组多，因此这种类型的分配可能比 `guestgroup` 行限制更少。

### 限制类中的用户数量

`limit` 命令限制了指定时间内某个类中的用户数量。此命令包含类、用户数量、时间范围和文本文件字段：

```
limit <class> <times> <message_file>
```

`times` 参数有点奇怪。它的格式是经逗号分隔的天期、小时。有效的日期有 `Su`、`Mo`、`Tu`、`We`、`Fr`、`Sa`。示例为：

```
limit anonymous 10MoTuFr,Sa0000–2300 /home/ftp/.message_anon
```

此行将限制匿名类在周五和周六 0000 到 2300 之间的并发数为 10。

## 在 ftaccess 文件中使用命令配置 wu-ftpd

关于精细限制用户连接的语法可以在 `ftpaccess` man 页面中找到。

### 限制无效密码次数

此行允许用户在服务器终止会话之前输入多少无效密码：

```
logfails <number>
```
