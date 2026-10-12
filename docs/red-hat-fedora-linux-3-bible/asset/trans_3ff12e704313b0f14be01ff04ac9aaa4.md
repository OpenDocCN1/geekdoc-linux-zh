
## 使用 NIS 映射

为了使 NIS 服务器分发的信息能够被 NIS 客户端使用，你必须配置 `/etc/nsswitch.conf` 文件，将 `nis` 包含在你要使用的每个文件的搜索路径中。

以下是来自 `/etc/nsswitch.conf` 文件的一个列表，展示了访问不同配置文件时搜索路径中有效的值。

```
# Legal entries are:
#
# nisplus or nis+     Use NIS+ (NIS version 3)
#   nis or yp          Use NIS (NIS version 2), also called YP
#   dns                Use DNS (Domain Name Service)
#   files              Use the local files
#   db                 Use the local database (.db) files
#   compat             Use NIS on compat mode
#   hesiod             Use Hesiod for user lookups
#   [NOTFOUND=return]  Stop searching if not found so far
```

就本例而言，我想在文件路径中添加 `nis`，以便从我的 NIS 服务器向此 NIS 客户端分发这些文件。在大多数情况下，只检查本地文件（`files`）。以下是某些条目外观的示例：

```
passwd:		files
shadow:		files
group:		files
hosts:		files dns
```

对于每个这些条目，首先会检查原始文件（`/etc/passwd`、`/etc/shadow` 等）。对于主机名，在检查本地 hosts 文件之后会检查 DNS 服务器。在这个例子中，你可以添加 `nis` 以访问 NIS 服务器共享的映射。（Linux NIS 服务器仅实现 `nis`，而不实现 `nisplus`。）这些行将如下所示：

```
passwd:		files nis
shadow:		files nis
group:		files nis
hosts:		files nis dns
```

一旦 `/etc/nsswitch` 文件被修改，NIS 映射中的数据即可访问。无需重启 NIS 服务。你可以遍历并修改 `/etc/nsswitch` 文件中列出的任何文件，使其配置为允许你的系统访问正在共享的 NIS 映射。

## 将 Fedora 配置为 NIS 主服务器

要将你的 Fedora 系统配置为 NIS 主服务器，首先应将其配置为 NIS 客户端（即，设置 NIS 域名，设置 `/etc/yp.conf`，并如前所述配置客户端守护进程）。然后你可以创建 NIS 映射并配置 NIS 主服务器守护进程（ypserv 和 rpc.ypasswdd）。以下小节描述了这些步骤。

> **注意：** 如果你的 NIS 服务器上有防火墙，你必须使 UDP 端口 111 (sunrpc) 可用，否则 NIS 客户端将无法连接到你的 NIS 服务。如果该计算机也是路由器，如果可能，请阻止来自本地网络外部对端口 111 的访问。

## 创建 NIS 映射

为了创建 NIS 映射以便你的 Fedora 系统可以充当 NIS 主服务器，请以 root 用户身份从终端窗口进入 `/var/yp` 目录。在该目录中，Makefile 允许你配置哪些文件正在通过 NIS 共享。默认共享的文件列表位于本章开头以及 Makefile 本身中。

### 选择要映射的文件

如果你不想共享 Makefile 中设置的文件，你可以阻止该文件的构建。通过找到 Makefile 中的以下行并简单删除你想排除的文件来实现：

```
all: passwd group hosts rpc services netid protocols mail \
    # netgrp shadow pubkeykey networks ethers bootparams printcap \
    # and_home auto_master auto_netid home auto.local passwd.adjunct \
    # timezone locale netmasks
```

你可能会注意到，`all:` 行中的并非所有名称都代表确切的文件名。例如，`netgrp` 对应的是 `/etc/netgroup` 文件。每个名称所代表的文件列在 Makefile 中 `all:` 行下方的几行中。你还会注意到许多文件已经被注释掉了，包括 shadow 文件。

> **提示：** NIS-HOWTO 文档建议，使用 NIS 配合 shadow 密码“始终是一个坏主意”。Makefile 中的选项（在下一节中描述）允许你自动将 shadow 和 gshadow 文件分别合并到 passwd 和 group 文件中。

### 选择映射选项

在 Makefile 中设置了几个选项。你可以选择更改这些选项或保持原样。选项如下：

- **B=** — 你可以使用 B= 选项允许 NIS 使用域名解析器来查找不在当前域中的主机。默认情况下，未设置 B=。要启用此功能，请将其设置为 `-b` (B=-b)。
- **NOPUSH=true** — 当设置为 true（默认值）时，NOPUSH 选项阻止映射被推送到从服务器。这意味着 NIS 主服务器是 NIS 域中唯一的服务器。如果不想让 NIS 主服务器成为域中唯一的服务器，请将其设置为 false，并将从服务器的主机名放入 /var/yp/ypservers 文件。
- **MINUID=500** — 为了防止分发管理用户的密码条目，MINUID 被设置为 500。这假设你想要共享的系统上所有常规用户账户的 UID 都大于或等于 500。
- **MINGID=500** — 为了防止分发管理组的密码条目，MINGID 被设置为 500。这假设你想要共享的所有常规组的 GID 都大于或等于 500。

> **注意：** 用于向 Fedora 添加用户和组的工具始终从数字 500 开始。然而，一些 UNIX 和 Linux 系统可能使用较低的 UID 和 GID 作为常规用户。在这种情况下，你可能需要将 MINUID 和 MINGID 降低到 500 以下，但不能低于 100（100 以下始终代表管理登录）。

- **MERGE_PASSWORD=true** — 如果你希望每个用户的密码从 shadow 文件合并回由 NIS 共享的密码文件中，请保持此选项设置为 *true*。
- **MERGE_GROUP=true** — 如果你希望每个组的密码从 gshadow 文件合并回由 NIS 共享的组文件中，请保持此选项设置为 *true*。

要构建 NIS 映射，你的系统必须拥有 awk、make 和 umask 命令。在 Makefile 中，这些命令的位置分别是 /usr/bin/gawk、/usr/bin/gmake 和 umask。（umask 命令是 shell 内置命令，因此你不必查找其位置。）你可以通过更改 Makefile 中 AWK、MAKE 和 UMASK 变量的值，使用位于不同位置的可比较命令。

除了刚才提到的选项外，还有几个变量你可以设置以更改 NIS 文件的位置。例如，密码文件 (YPPWDDIR) 和其他源文件 (YPPSRCDIR) 的位置默认都设置为 /etc。YP 命令 (YPPBINDDIR) 的位置设置为 /usr/lib/yp。如果你想更改这些或其他变量的值，你可以在 Makefile 中这样做。

### 定义 NIS 客户端访问

将允许访问你的 NIS 映射的客户端计算机的 IP 地址添加到 /var/yp/securenets 文件中。默认情况下，任何网络上任何可以到达你的 NIS 主服务器的计算机都可以访问你的映射（这不是一种安全的情况）。因此，配置此文件很重要。IP 号可以以 netmask/network 对的形式给出。例如：

```
255.255.255.0 10.0.0.0
```

此示例允许网络编号 10.0.0 上的所有计算机访问你的 NIS 主服务器映射。

> **交叉引用**：请参阅第 15 章了解 IP 地址和子网掩码的描述。

## 配置映射访问

在 `/etc/ypserv.conf` 文件中，你可以定义关于哪些客户端主机计算机可以访问哪些映射的规则。你还可以设置几个相关选项。`ypserv.conf` 文件中的访问规则具有以下格式：

```
host:map:security:mangle[.field]
```

星号可以替换 `host` 和 `map` 字段，以分别创建匹配任何主机或映射的规则。`host` 字段是规则适用的网络或特定主机的 IP 地址。`map` 字段是你正在定义访问权限的映射的名称。`security` 字段由 `none`（始终允许访问）、`port`（允许来自小于 1024 端口的访问）、`deny`（拒绝访问此映射）或 `des`（要求 DES 认证）替换。

`mangle` 字段由 `yes` 或 `no` 替换（指示如果请求来自非特权主机，映射中的字段是否应被替换为 `x`）。如果 `mangle` 字段设置为 `yes`，`field` 将被替换为应该被 mangle 的字段名称（默认使用第二个字段）。

可以在 `ypserv.conf` 文件中设置以下选项：

- **dns** — 如果是（`dns: yes`），当在映射中找不到主机名时，NIS 将查询 TCP/IP 名称服务器以获取主机名。默认情况下，设置为 `dns:no`。
- **xfr_check_port** — 如果是（`xfr_check_port: yes`），NIS 主服务器必须运行在小于 1024 端口的端口上。如果为否，可以使用任何端口号。默认情况下，设置为 `yes`。

如果你对 `/etc/ypserv.conf` 文件进行了更改，`ypserv` 守护进程将在你的系统下次重新启动（或 `ypserv` 服务重启）时拾取这些更改。或者，你可以通过向 `ypserv` 进程发送 `SIGHUP` 信号让 `ypserv` 立即读取文件内容。从 `/etc/ypserv.conf` 中的下一行中移除注释字符 (#) 允许所有主机访问所有映射：

```
* : * : * : none
```

## 生成 NIS 映射数据库

要安装并构建 NIS 数据库，请运行 `ypinit` 命令。要启动 `ypinit` 程序，请输入以下内容：

```bash
# /usr/lib/yp/ypinit -m
 next host to add:  mapie
 next host to add:
```

`ypinit` 命令应自动选择你的主机名用作 NIS 服务器。之后，它会询问你添加从服务器。逐个添加；然后在你完成添加后按 Ctrl+D

