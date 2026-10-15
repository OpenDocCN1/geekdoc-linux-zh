
### MINGID 和相关选项

`MINGID=500` — 为了防止分发管理组的密码条目，`MINGID` 被设置为 500。这假设你想要共享的所有常规组的 GID 都大于或等于 500。

> **注意：** 用于向 Fedora 添加用户和组的工具始终从数字 500 开始。然而，一些 UNIX 和 Linux 系统可能使用较低的 UID 和 GID 作为常规用户。在这种情况下，你可能需要将 `MINUID` 和 `MINGID` 降低到 500 以下，但不能低于 100（100 以下始终代表管理登录）。

`MERGE_PASSWORD=true` — 如果你希望每个用户的密码从 `shadow` 文件合并回由 NIS 共享的密码文件中，请保持此选项设置为 `true`。

`MERGE_GROUP=true` — 如果你希望每个组的密码从 `gshadow` 文件合并回由 NIS 共享的组文件中，请保持此选项设置为 `true`。

要构建 NIS 映射，你的系统必须拥有 `awk`、`make` 和 `umask` 命令。在 `Makefile` 中，这些命令的位置分别是 `/usr/bin/gawk`、`/usr/bin/gmake` 和 `umask`。`umask` 命令是 shell 内置命令，因此你不必查找其位置。你可以通过更改 `Makefile` 中 `AWK`、`MAKE` 和 `UMASK` 变量的值，使用位于不同位置的可比较命令。

除了刚才提到的选项外，还有几个变量你可以设置以更改 NIS 文件的位置。例如，密码文件 (`YPPWDDIR`) 和其他源文件 (`YPPSRCDIR`) 的位置默认都设置为 `/etc`。`YP` 命令 (`YPPBINDDIR`) 的位置设置为 `/usr/lib/yp`。如果你想更改这些或其他变量的值，你可以在 `Makefile` 中这样做。

### 定义 NIS 客户端访问

将允许访问你的 NIS 映射的客户端计算机的 IP 地址添加到 `/var/yp/securenets` 文件中。默认情况下，任何网络上任何可以到达你的 NIS 主服务器的计算机都可以访问你的映射（这不是一种安全的情况）。因此，配置此文件很重要。IP 号可以以 `netmask/network` 对的形式给出。例如：

```
255.255.255.0 10.0.0.0
```

此示例允许网络编号 10.0.0 上的所有计算机访问你的 NIS 主服务器映射。

> **交叉引用**：请参阅第 15 章了解 IP 地址和子网掩码的描述。

### 配置映射访问

在 `/etc/ypserv.conf` 文件中，你可以定义关于哪些客户端主机计算机可以访问哪些映射的规则。你还可以设置几个相关选项。`ypserv.conf` 文件中的访问规则具有以下格式：

```
host:map:security:mangle[.field]
```

星号可以替换 `host` 和 `map` 字段，以分别创建匹配任何主机或映射的规则。`host` 字段是规则适用的网络或特定主机的 IP 地址。`map` 字段是你正在定义访问权限的映射的名称。`security` 字段由 `none`（始终允许访问）、`port`（允许来自小于 1024 端口的访问）、`deny`（拒绝访问此映射）或 `des`（要求 DES 认证）替换。

`mangle` 字段由 `yes` 或 `no` 替换（指示如果请求来自非特权主机，映射中的字段是否应被替换为 `x`）。如果 `mangle` 字段设置为 `yes`，`field` 将被替换为应该被 mangle 的字段名称（默认使用第二个字段）。

可以在 `ypserv.conf` 文件中设置以下选项：

- `dns` — 如果是（`dns: yes`），当在映射中找不到主机名时，NIS 将查询 TCP/IP 名称服务器以获取主机名。默认情况下，设置为 `dns:no`。
- `xfr_check_port` — 如果是（`xfr_check_port: yes`），NIS 主服务器必须运行在小于 1024 端口的端口上。如果为否，可以使用任何端口号。默认情况下，设置为 `yes`。

如果你对 `/etc/ypserv.conf` 文件进行了更改，`ypserv` 守护进程将在你的系统下次重新启动（或 `ypserv` 服务重启）时拾取这些更改。或者，你可以通过向 `ypserv` 进程发送 `SIGHUP` 信号让 `ypserv` 立即读取文件内容。从 `/etc/ypserv.conf` 中的下一行中移除注释字符 (`#`) 允许所有主机访问所有映射：

```
* : * : * : none
```

### 生成 NIS 映射数据库

要安装并构建 NIS 数据库，请运行 `ypinit` 命令。要启动 `ypinit` 程序，请输入以下内容：

```bash
# /usr/lib/yp/ypinit -m
 next host to add:  mapie
 next host to add:
```

`ypinit` 命令应自动选择你的主机名用作 NIS 服务器。之后，它会询问你添加从服务器。逐个添加；然后在你完成添加后按 Ctrl+D

进入了您的最后一台从属服务器。请验证 NIS 服务器列表是否正确（输入 y）。（请记住，从属服务器不是必需的。）

此时数据库已建立完成。在 `/var/yp` 目录下会创建一个以您的 NIS 域名为名的新目录。例如，如果您的 NIS 域名是 `trident`，则该目录为 `/var/yp/trident`。所有构建好的映射（maps）都会放置在该目录中。

### 添加 NIS 从属服务器

在 Fedora 中，NIS 默认配置为拥有一台主 NIS 服务器，且没有从属 NIS 服务器。通过设置 `/var/yp/Makefile` 文件中的 `NOPUSH=False`，您可以允许将 NIS 映射推送到一台或多台从属服务器。之后，您需要将从属服务器的名称添加到您的 `/var/yp/ypservers` 文件中。您可以手动添加主机名，或者在稍后运行 `ypinit` 命令时让系统自动添加。

### 配置 NIS 服务器守护进程

为了作为 NIS 服务器，NIS 服务器必须运行多个守护进程。Fedora 提供了运行级别脚本，您可以配置这些脚本来启动 NIS 服务器守护进程。这些脚本位于 `/etc/init.d` 目录中，包括以下内容：

- `ypserv` — 此脚本启动 `ypserv`（`/usr/sbin/ypserv`）守护进程。它从 `/etc/ypserv.conf` 文件中读取信息以确定操作。然后它监听网络上 NIS 客户端计算机的请求。
- `yppasswdd` — 此脚本启动 `rpc.yppasswd`（`/usr/sbin/rpc.yppasswdd`）守护进程。此守护进程处理来自 NIS 客户端计算机上希望更改用户密码的用户的请求。

除非您在安装 Fedora 时要求这些脚本配置为在启动时启动，否则它们不会自动启动。您可以使用以下 `chkconfig` 命令设置 `ypserv` 和 `yppasswdd` 脚本在启动时自动运行。

```
# chkconfig ypserv on
# chkconfig yppasswdd on
```

如果您想立即启动这些服务，可以输入以下内容：

```
# /etc/init.d/ypserv start
# /etc/init.d/yppasswdd start
```

此时，NIS 主服务器应该已启动并运行。如果有任何 NIS 从属服务器，您现在应该配置它们。

### 设置 Fedora 为 NIS 从属服务器

要设置 NIS 从属服务器，必须像配置 NIS 主服务器一样进行配置，但有一个例外：您不是创建 NIS 映射，而是运行 `ypinit` 命令以便将 NIS 映射从主服务器复制过来。您给 `ypinit` 提供的选项是 `-s` 主服务器选项，其中“master”被替换为您的 NIS 主服务器名称。以下是一个运行 `ypinit` 的示例，其中 NIS 主服务器的名称为 `maple`：

```
# /usr/lib/yp/ypinit -s maple
```

只要允许 NIS 从属服务器访问，映射就应该能从 NIS 主服务器复制到您的计算机。如果 NIS 主服务器宕机，这台从属计算机应该能够处理来自网络的 NIS 请求。

此时，您可以返回设置 NIS 客户端的部分，以确保您的 NIS 服务器正常运行并将映射分配给其客户端。

### NIS 和 Active Directory

如果您需要同时处理 Microsoft Windows 用户和 Linux 用户，您可能需要某种集成方式。如果您的 Windows 网络使用带有 Active Directory (`AD`) 身份验证的域，那么让 Linux 客户端也能访问相同的用户信息会非常方便。如果您在 Windows 2000/2003 域控制器 (`DC`) 上安装 NIS 服务器服务，就可以开始这种集成。
