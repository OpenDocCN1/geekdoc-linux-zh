
# 让 Linux 良好运行：核心技巧与技术

- 不要在你的 PC 上创建不需要的用户账户。你 PC 上的每个用户账户都是一个潜在的弱点，可能被用来破坏你的系统安全。

- 不要与不需要知道或不应经常访问你系统的用户共享密码（包括用户密码和 root 密码）。控制 root 密码的访问尤为重要。

- 不要运行不必要的网络服务。如果系统中某个服务（如 Telnet）完全没有被使用，请确保没有安装该服务的可执行文件，并从 `/etc/inetd.conf` 中删除任何条目。`/etc/inetd.conf` 文件将在提示 884 “*inetd.conf 在提供网络服务中的作用*”和提示 885 “*inetd.conf 文件的结构*”中进行讨论。

- 如果可能，请以具有限制系统访问的受限用户运行提供网络服务的守护进程（daemons）。这样，如果你的配置中存在安全漏洞或守护进程存在 Bug 导致你面临攻击，所造成的损害将受到运行守护进程的账户权限的限制。例如，Apache Web 服务器通常以 `nobody` 用户运行，这是一个高度受限的用户账户。

- 如果你必须运行网络服务，请使用 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件将服务的访问限制为那些应该访问该服务的主机，正如提示 165 “*控制你系统上可网络服务*”中所讨论的。

### 8.4.1: 使用影子密码（Shadow Passwords）保护网络密码

直到最近，影子密码（shadow passwords）还不是大多数 Linux 发行版的标准部分。然而，这种情况开始发生变化。例如，RedHat 已选择为 RedHat Linux 6.1 及以上版本启用影子密码。

影子密码是一种用于增加潜在攻击者破解系统难度的机制。传统上，Linux 和 Unix 密码存储和管理方式如下：

- 密码使用标准的 Unix `crypt` 加密算法进行加密。

- 加密后的密码存储在 `/etc/passwd` 的用户记录中。

- 为了让所有软件都能访问账户信息（如用户 ID 和组 ID），`/etc/passwd` 文件必须对所有用户都是可读的（但不可写的）。

这种方法存在两个主要问题：

- 因为 `passwd` 文件对系统上的任何用户都可见，潜在攻击者获取 `passwd` 文件的副本是非常简单的。
- 因为 Unix `crypt` 加密方案并不复杂，仅需极少的资源和合适的软件，攻击者就可以从文件中解密一个或多个密码。对于攻击者来说，破解你的 root 账户密码并不会困难。

影子密码是试图解决这一困境部分的尝试：`passwd` 文件包含了所有用户都必须访问的信息（如 ID 和用户名），那么如何防止对加密密码的访问呢？解决方案非常简单：将加密后的密码移动到另一个文件中：

- `/etc/passwd` 包含每个密码的占位符（placeholder），并对所有用户可读。
- `/etc/shadow` 包含加密后的密码，但仅对 root 用户可读。

在标准系统中，`/etc/passwd` 中的用户条目可能如下所示：

```
someuser:03hj45XJ123d:1000:1000:Some User:/home/someuser:/bin/bash
```

在启用影子密码的系统中，`/etc/passwd` 将包含以下条目：

```
someuser:x:1000:1000:Some User:/home/someuser:/bin/bash
```

而 `/etc/shadow` 文件将包含以下条目：

```
someuser:03hj45XJ123d:10935:0:99999:7:-1:-134550664
```

`/etc/shadow` 文件中的字段含义如下：

```
<user name>:<encrypted password>:<last change>:<possible password change date>:<required password change>:<password change warning>:<disabled>:<reserved>
```

这些字段的含义如下：

- 用户名（user name）字段是用户的用户名。
- 加密密码（encrypted password）包含用户的加密密码。
- 最后更改日期（last change）字段表示密码上次更改的时间，即自 1970 年 1 月 1 日以来的天数。
- 可更改密码日期（possible password change date）表示距离可以更改密码的天数。
- 强制更改密码日期（required password change）表示用户必须更改密码所需的天数。
- 密码更改警告（password change warning）在必须更改密码之前，警告用户需要更改密码的天数。
- 禁用日期（disabled date）表示在密码更改日期后如果不更改，账户应被禁用的天数。
- 禁用字段（disabled）表示账户被禁用的时间，即自 1970 年 1 月 1 日以来的天数。
- 预留字段（reserved）供系统使用，管理员绝不应进行编辑。

如果你的发行版不包含影子密码支持（由于许多应用程序需要它），你需要从以下站点之一下载并安装 Shadow 密码套：

- `ftp://ftp.icm.net/pub/`
- `ftp://ftp.net.com`
- `http://www.linuxdoc.org`

# 8: 网络与安全

### 8.4.2: 使用 hosts.allow 和 hosts.deny 实现简单的安全

Linux 与 Unix 系统一样，具有多个安全层，可以选择性地使用来帮助你在网络环境中的系统。最基础的网络安全机制是通过两个文件实现的：`/etc/hosts.allow` 和 `/etc/hosts.deny`。通过这两个文件，你可以为系统提供粗粒度或细粒度的访问控制。

这两个文件是远程客户端尝试访问资源时触发决策链的一部分。这种三阶段决策链的工作原理如下：

- 如果客户端在 `hosts.allow` 文件中允许访问服务，则允许访问。
- 如果客户端在第一阶段未被允许，则检查其是否在 `hosts.deny` 文件中被拒绝访问，若是则拒绝。
- 如果客户端在第二阶段未被拒绝，则授予访问。

大多数 Linux 版本安装时 `hosts.allow` 或 `hosts.deny` 没有任何条目，这意味着所有人都可以连接到所有资源。重要的是，对资源的授权或拒绝是在客户端和协议级别控制的。也就是说，你可以使用 `hosts.allow` 和 `hosts.deny` 来决定哪些物理客户端（通过主机名或 IP 地址识别）可以访问特定协议。一旦授予权限，由该协议的守护进程决定是否需要进一步的验证（如用户名和密码）。

例如，`hosts.allow` 和 `hosts.deny` 任何人访问你系统的 FTP，但 `ftpd` 可以配置为要求所有用户提供有效的用户名和密码才能连接，并允许匿名访问。

你可以根据 `hosts.allow` 和 `hosts.deny` 文件中创建条目来限制访问。这些文件中的每行都是一个条目。注释以井号 (`#`) 开始并持续到行。每个条目的格式如下：

```
<daemon list>: <client list>
```

守护进程列表（daemon list）是适用于该条目的网络守护进程（如 `ftpd`、`in.telnetd` 或 `in.rshd`）的逗号分隔列表，客户端列表（client list）是适用于该条目的的主名或 IP 地址的逗号分隔列表。

例如，如果在 `/etc/hosts.allow` 中有以下条目：

```
in.telnetd: 10.20.30.40, 10.20.30.50
```

# 让 LINUX 易用：核心技巧与技术

主机 `10.20.30.40` 和 `10.20.30.50` 被允许访问 Telnet 守护进程。同样，`/etc/hosts.deny` 中的以下条目：

```
ftpd, http: somehost
```

表示 `somehost` 不被允许访问 FTP 或 HTTP 服务。

在条目目可以使用几个特殊关键字来增加灵活性：

- `ALL`：匹配任何客户端或守护进程
- `EXCEPT`：指示客户端或守护进程列表的例外
- `LOCAL`：指示本地网络上的所有客户端

例如，你可以通过 `hosts.allow` 中的以下条目，允许主机 `somehost` 访问所有服务：

```
ALL: somehost
```

同样，你可以通过 `hosts.deny` 中的以下条目，拒绝所有主机访问 FTP 服务：

```
ftpd: ALL
```

如果你想允许除 FTP 以外的所有服务，请在 `hosts.allow` 中使用以下条目：

```
ALL EXCEPT ftpd: somehost
```

同样，你可以使用以下条目允许除 `foo.some.domain` 以外的所有主机访问 FTP 服务：

```
ftpd: ALL EXCEPT foo.some.domain
```
