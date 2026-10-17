
## FTP 服务器是如何运作的

FTP 服务通过 `/etc/inetd.conf` 控制（当有人连接时，守护进程就会调用，会话开始后，需要提供用户名和密码。例如，端口 `21` 关联到 FTP）。当检测到连接时，会进行额外的检查以确保用户具有有效的 shell。如果用户没有有效的 shell，他们将被拒绝访问系统。这对于想要允许通过邮件但不希望通过 FTP 访问的用户是有用的。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa)

访问 FTP 的用户在登录时被放在他们的家目录中。在那之后，他们可以进入他们有权限的任何目录。另一方面，匿名用户受到了若干限制。

匿名用户被放在 FTP 的家目录中。默认情况下，此目录由 `anon` 包设置为 `/home/ftp`。在到达那里后，FTP 服务器执行 `chroot` 系统调用。这实际上将程序的根目录更改为 FTP 用户的目录。对系统中任何其他目录（包括 `/bin`、`/etc` 和 `/lib` 目录）的访问都被拒绝了。根目录的更改副作用是服务器无法看到 `/etc/passwd`、`/etc/group` 以及必要的 `/bin/ls`。为了补偿这一变化，`anon` RPM 包在 `/home/ftp` 下创建了 `bin`、`etc` 和 `lib` 目录，并将必要的库和程序（如 `ls`）放在其中，以便服务器软件在执行 `chroot` 系统调用后仍然访问。

出于安全考虑，放在 `/home/ftp` 下的文件权限设置为只有服务器可以看到（这在安装期间自动完成）。任何其他目录都应设置为全局可读。大多数匿名 FTP 站点此类文件放在 `pub` 子目录下。

## 配置你的 FTP 服务器

虽然 FTP 服务器的默认配置是安全的，但你可以通过编辑以下文件来微调访问权限：

- `/etc/ftpaccess`
- `/etc/ftpconversions`
- `/etc/ftphosts`
- `/var/log/xferlog`

通过所有这些文件，你可以非常精确地控制谁在何时、从何地连接到你的服务器，以及他们在连接后做了什么。`/etc/ftpaccess` 文件是这些文件中最重要的，因为它包含了最多的配置选项；然而，错误配置其中任何一个都可能导致服务被拒绝。

## 提示

在编辑 `/etc` 目录下的任何文件（无论是否与 FTP 相关）时，请尽可能多添加注释。在文件列表末尾保留编辑历史，记录最后一次编辑文件的人员、编辑时间以及他们修改的内容，是追踪问题以及追溯问题始源者的好方法！

## 控制访问权限——`/etc/ftpaccess` 文件

`/etc/ftpaccess` 文件是控制谁以及有多少个用户访问你的服务器的主要手段。文件中的每行都定义了一个属性或设置了其值。

以下命令控制访问：

- `class`
- `autogroup`
- `deny`
- `guestgroup`
- `limit`
- `loginfails`
- `private`

以下命令控制服务器向客户端提供的信息：

- `banner`
- `email`
- `message`
- `readme`

这些命令控制日志功能：

- `log commands`
- `log transfers`

以下是杂项命令：

- `alias`
- `cdpath`
- `compress`
- `tar`
- `shutdown`

权限控制由以下命令设置：

- `chmod`
- `delete`
- `overwrite`
- `rename`
- `umask`
- `passwd-check`
- `path-filter`
- `upload`

## 控制用户访问

控制谁可以或不可以进入你的站点是精细调整匿名 FTP 服务器的关键组成部分。以下命令定义了确定每个用户应该被放在哪个组的标准。

### `class`

`class` 命令定义了一类可以访问你 FTP 服务器的用户。你可以定义任意数量的类。每行的格式如下：

```
class <classname> <typelist> <addrglob> [<addrglob> ...]
```

其中 `<classname>` 是你定义的类名称，`<typelist>` 是你允许进入该类的用户类型，而 `<addrglob>` 是允许访问该类的 IP 地址范围。

`<typelist>` 是一个逗号分隔的列表，每个条目具有三个值之一：`anonymous`（匿名）、`guest`（访客）或 `real`（真实）。匿名用户当然是指任何以匿名或 `ftp` 身份连接服务器并只想访问公共可用文件的用户。访客用户是特殊的，因为他们本身在系统上没有账户，但他们对访客组的关键部分具有特殊访问权限（更多细节请参见本章后文对 `guestgroup` 命令的描述）。真实用户必须在 FTP 服务器上拥有账户，并经过相应的身份验证。

`<addrglob>` 采用正则表达式的形式，其中 `*` 表示所有站点。多个 `<addrglob>` 可以关联到特定的类。

以下该行：

```
class anclass anonymous *
```

定义了类 `anclass`，它只包含匿名用户。他们可以从网络任何地方发起连接。

另一方面，该行
`class localclass real 192.168.42.*`
允许在 FTP 服务器上拥有账户的真实用户在来自局域网时通过 FTP 访问其账户。

### `autogroup`

`autogroup` 命令用于在匿名用户登录时自动为他们分配特定的组权限，从而更紧地控制匿名用户的访问。`autogroup` 行的格式为：

```
autogroup <classname> <class> [...]
```

其中 `<classname>` 是你想让匿名用户所在的组名，`<class>` 是使用 `class` 命令定义的类名。一个 `autogroup` 可以有多个 `<class>` 条目。只有 `<class>` 中引用的匿名用户才会受 `autogroup` 的影响。

记住，赋予用户权限的组必须在 `/etc/group` 文件中。

### `deny`

`deny` 命令允许你根据主机名、IP 地址或其主机名是否可以通过 DNS 进行反向解析，显式地拒绝某些主机的服务。`deny` 命令的格式为：

```
deny <addrglob> <message_file>
```

其中 `<addrglob>` 是包含要拒绝地址的正则表达式，`<message_file>` 是包含消息的文件，当主机连接时显示该消息。

以下是一个示例 `deny` 行：

```
deny evilhacker.domain.com /home/ftp/.message.no.evil.hackers
```

该行向任何尝试从 `evilhacker.domain.com` 连接 FTP 的用户显示文件 `/home/ftp/.message.no.evil.hackers` 的内容。要拒绝...

### `guestgroup`

`guestgroup` 命令用于在匿名用户登录时自动为他们分配特定的组权限，从而更紧地控制匿名用户的访问。`autogroup` 行的格式为：

```
autogroup <classname> <class> [...]
```

其中 `<classname>` 是你想让匿名用户所在的组名，`<class>` 是使用 `class` 命令定义的类名。一个 `autogroup` 可以有多个 `<class>` 条目。只有 `<class>` 中引用的匿名用户才会受 `autogroup` 的影响。

记住，赋予用户权限的组必须在 `/etc/group` 文件中。

### `deny`

`deny` 命令允许你根据主机名、IP 地址或其主机名是否可以通过 DNS 进行反向解析，显式地拒绝某些主机的服务。`deny` 命令的格式为：

```
deny <addrglob> <message_file>
```

其中 `<addrglob>` 是包含要拒绝地址的正则表达式，`<message_file>` 是包含消息的文件，当主机连接时显示该消息。

以下是一个示例 `deny` 行：

```
deny evilhacker.domain.com /home/ftp/.message.no.evil.hackers
```

该行向任何尝试从 `evilhacker.domain.com` 连接 FTP 的用户显示文件 `/home/ftp/.message.no.evil.hackers` 的内容。要拒绝...

### `guestgroup`

`guestgroup` 命令用于在匿名用户登录时自动为他们分配特定的组权限，从而更紧地控制匿名用户的访问。`autogroup` 行的格式为：

```
autogroup <classname> <class> [...]
```
