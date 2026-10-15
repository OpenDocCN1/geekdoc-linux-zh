
其中 `groupname` 是分配给组的任何名称 `member` 是：

- 另一个 `netgroup`
- 由三元组定义的项：`(hostname, username, domainname)`

`domainname` 字段省略表示在当前 NIS 域有效；`hostname` 和 `username` 字段中的 `(-)` 表示未包含。

一旦设置了 NIS，它运行得很好，对用户隐藏，有时对管理员也是如此。然而，与其他一样，NIS 也需要维护——检查 NIS 状态以及修改和更新 NIS 数据库是管理职责。NIS是一个非常有用的网络服务，但 NIS 会带来很多麻烦。常用的 UNIX 命令无法高效使用；这就是为什么 NIS 引入了许多新命令来处理 NIS过程和映射，以便于管理。这些命令在每个 UNIX 平台上大多是标准的。以下是对有用的 NIS 特定命令的简要介绍。

## 17.3 yp 命令

NIS 特定命令（我们称之为 yp 相关命令）位于多个目录中，通常为 `/bin`、`/usr/sbin` 和 `/usr/lib/netsvc/yp`。识别这些命令非常容易；它们以 `yp` 前缀开头。下表描述这些命令（命令布局来自 Solaris 2.x；其他 UNIX 变体可能存在差异）：

| yp 命令 | 描述 |
|---|---|
| `/bin/ypcat` | 打印 NIS 映射中的所有值；`ypservers` 映射需要 `-k` 选项：`ypcat -k ypservers` |
| `/bin/ypmatch` | 打印 NIS 映射中选定键的值，例如显示用户 `"bjl"` 的密码数据： |

| `/bin/yppasswd` | 在 NIS 数据库中更改登录密码，而不影响本地数据。其行为类似于普通的 `passwd` 命令。 |
| `/bin/ypwhich` | 列出哪些主机是当前的 NIS 服务器并为该主机提供 NIS 服务；这是一个检查 NIS 客户端与可用 NIS 服务器之间当前绑定情况非常有用的命令。 |
| `/usr/sbin/ypalias` | 更改 NIS 数据库中的别名。 |
| `/usr/sbin/ypinit` | 在主服务器或从用 NIS 服务器上构建并安装 NIS 数据库（已讨论过）。 |
| `/usr/sbin/ypypoll` | 查询指定的 NIS 服务器（默认为绑定的服务器）关于特定 NIS 映射的信息。该信息包括映射构建的时间（秒）以及该映射的主服务器。例如，要获取关于 **group**（组组）映射的信息：`/usr/sbin/ypypoll -h NISslave group` 或 `/usr/sbin/ypypoll group` |
| `/usr/sbin/ypset` | 将客户端绑定到特定的 NIS 服务器。这对于绑定不在广播网络上的 NIS 客户端非常有用，因为广播是 `ypbind` 进程（客户端）定位 NIS 服务器的方法。如果 `ypbind` 已经绑定到 `ypserv` 进程，则只有在启动 `ypbind` 时使用了允许更改当前绑定的 `-ypset` 选项，此命令才能生效（这特定于 Solaris 系统）。 |
| `/usr/lib/netsvc/ypbind` | NIS 客户端进程（已讨论）。 |
| `/usr/lib/netsvc/yppush` | 强制将指定的 NIS 映射（数据库）从主服务器向从用服务器传播。 |
| `/usr/lib/netsvc/ypserv` | NIS 服务器进程（已讨论）。 |
| `/usr/lib/netsvc/ypstart` | 启动和停止 NIS 服务器，`ypstart` 会自动确定系统的 NIS 配置状态并启动相应的守护进程，而 `ypstop` 则停止 NIS 守护进程。 |
| `/usr/lib/netsvc/ypstop` | |
| `/usr/lib/netsyc/yp/ypxfr` | 开始从 NIS 服务器传输 NIS 映射（数据库）。应该使用 `cron` 设施定期执行数据库命令以保持 NIS 数据库的同步。 |
| `/usr/lib/netsyc/yp/ypxfr_1p deaday` | 定期启动 NIS 映射（数据库）的模板：每天一次、每小时一次和每天两次。 |
| `/usr/lib/netsyc/yp/ypxfr_2p deaday` | |
| `/usr/lib/netsyc/yp/ypxfd` | NIS 数据库传输守护进程（已讨论）。 |

## 17.3. 更新 NIS 映射

NIS 映射更新是 NIS 管理中最频繁的活动。配置更改都需要更新并传播映射；例如，当添加新用户或创建新组时，必须更新相应的 NIS 映射并将其推送到所有从用服务器。这是一个常规程序，通常为了让这项工作变得更容易，我们经常忘记某些工具（有时甚至是自制的），这些工具假设一切工作都可以通过命令行完成。首先，任何更改和更新始终在 NIS 主服务器上进行；一旦源 `/etc` 文件被修改，就需要重新构建相应的 NIS 映射（映射实际上需要重新构建）。在映射准备好推送到从用服务器后，主、从用服务器上的数据库就能保持同步。

在后台，更新和推送更新后的 NIS 映射的例程非常复杂，需要按顺序执行许多步骤。这些每一个步骤本质上都可以从命令行完成，但要彻底遵循所需的算法将是一场真正的噩梦。然而，UNIX 为此类场景提供了优秀的工程工具：这就是 `make` 命令（确切说是 `make` 实用程序），它可以将非常复杂的算法执行简化为只需发布单个命令，即 `make` 命令本身。

本文不再详细阐述 `make` 实用程序/命令。只需提到 `make` 会读取描述文件（默认情况下 `make` 查找当前目录下的描述文件 `Makefile`）并遵循其指令。描述文件 `Makefile` 的格式和语法是特定的，但对于 `make` 命令本身是为人知的。文件中的每个条目都描述（指定）了完成某操作的几个独立步骤；所有条目共同完成任务。

UNIX NIS 软件提供了构建 NIS 数据库/映射所需的 `Makefile`；描述文件 `/var/yp/Makefile` 适用于大多数 NIS 实现。如果需要某些特定领域的自定义，修改它并并不是什么困难；其内容对于新手来说是足够易读且全面的。自定义意味着在几个选项之间进行选择，或者重命名或添加新的 NIS 映射。

### 17.3.2.1 make 实用程序与 NIS

在不带参数的情况下，`make` 将尝试为所有过期的 NIS 映射创建 dbm 数据库，然后执行 `ypush` 通知从用服务器已发生更改。请记住，实现的算法（由 `/var/yp/Makefile` 描述）是比较源文件和当前映射的时间戳，以确定映射是否过期；否则，它将跳过映射创建。触发映射更新的技巧只需修改相应的源 `/etc` 文件的时间戳，而不修改其内容；UNIX 的 `touch` 命令就能做到这一点。

如果从命令行上作为参数提供映射，`make` 将仅更新该一个映射。通过输入 `passwd`，将创建并推送密码映射。同样，`make hosts` 将创建并推送网络映射。

`make` 使用三个特殊变量：`DIR`，用于生成源文件目录；`NOPUSH`，为空时则抑制新映射的 `ypush`；以及 `DOM`，用于构建主服务器以外的域。`DIR` 的默认值为 `/etc`，`NOPUSH` 的默认值为空字符串。

`makedbm` 要求输入文件采用特殊的“键值格式”，这与现有的 `/etc/passwd` 文件不同。编写脚本将标准源文件（如 `/etc/passwd`）转换为所需的键值格式是非常简单的；一个简单的 `awk` 脚本即可：

```awk
#! /bin/awk -f

BEGIN { FS = ":"; OFS = "\t"; }

print $1, $0
```

在 `/etc/passwd` 文件上实现时，该脚本将获取 `/etc/passwd` 文件转换为 `makedbm` 可制作 NIS 映射 `passwd.byname` 的格式。在存在用户名（passwd 条目的第一个字段）的情况下，名称是 `/etc/passwd` 中的剩余行。

同样，在 `/etc/passwd` 文件上实现的 `awk` 脚本将获取 `/etc/passwd` 文件转换为 `makedbm` 可制作 NIS 映射 `passwd.byuid` 的格式。

```awk
#! /bin/awk -f

BEGIN { FS = ":"; OFS = "\t"; }
```

`makedbm` 命令的常用选项有：

- `-L`：将给定映射的键转换为小写，这样主机名匹配（例如）可以独立于大小写。
- `-S`：安全映射；仅接受来自安全网络的连接。
- `-yp 输入文件`：创建一个键为 yp 输入文件文件的特殊条目。
- `-o 输出名称`：创建一个键为 yp 输出名称的特殊条目。
- `-d 域名`：创建一个键为 yp 域名的特殊条目。
- `-m 主服务器名`：创建一个键为 yp 主服务器名的特殊条目。如果没有指定主主机名，则使用。`name -u dbfilename`：使用 dbm 文件；即每行打印一个 dbm 条目，并用单个空格分隔键和值。

```printf("%10d", $3); print $0 )
```

也就是说，键是 `userID`（`passwd` 条目中的第三个字段），而值是 `/etc/passwd` 文件中行的剩余部分。

这正是在 `makedbm` 命令实现之前 `make` 正在执行的操作。一旦生成了递归 NIS 映射，它就会被推送到 NIS 服务器。`Makefile` 定义了执行 `make` 命令/工具的每一步。一个来自 Solaris/SunOS 平台的示例（仅展示了部分文件）：

```make
# cat /var/yp/Makefile

# @($)make.script 1.36 SMI

#

# 此文件应该存在于 /var/yp/Makefile 和 /usr/lib/NIS.Makefile 中。

# 它应该只从 /var/py 执行。

#

#################################################################

# 将以下变量设为 "b"，以便让 NIS 服务器对不在当前域内的主机

# 使用域名解析器。

B=-b

# == 这一点将在稍后将讨论！

#################################################################

DIR = /etc

DOM = 'domainname'

NOPUSH = ""

ALIASES = /etc/aliases

YPDIR=/usr/etc/yp

YPBDIR=/var/yp

YPPUSH=$(YPDIR)/yppush

MAKEDBM=$(YPDIR)/makedbm

...
```

```make
MKALIAS=$(YPDIR)/mkalias

CHKPIPE=|| (echo "NIS make terminated:" $@ 1>&2; kill -TERM 0)

@if [ ! $NOPUSH ]; then $(MAKE) ($MFLAGS) -k all; \

else $(MAKE) ($MFLAGS) -k all NOPUSH=$NOPUSH); fi

all: passwd group hosts networks rpc services protocols | \

netgroup bootstraps aliases abbey netid netmas c2secure | \

time auto.master.auto.home_auto_share

passwd.time: $(DIR)/passwd

@awk 'BEGIN {FS=":"; OFS=" "} { $1 ~ /[a-z-0-9_]+/ { print $1, $$, $0 }' $(DIR)/passwd

$(CHKPIPE) $(MAKEDBM) $(YPDIR) $(DOM) passwd.byname;

@awk 'BEGIN {FS=":"; OFS=" "} { $1 ~ /[a-z-0-9_]+/ { printf("%10d", $33); print $0 }' $(DIR)/passwd

$(CHKPIPE) $(MAKEDBM) $(YPDIR) $(DOM) passwd.buid;

@touch passwd.time;

@echo "updated passwd";

@if [ ! $NOPUSH ]; then $(YPPUSH) -d $(DOM) passwd.byname; fi

@if [ ! $NOPUSH ]; then $(YPPUSH) -d $(DOM) passwd.buid; fi

@if [ ! $NOPUSH ]; then echo "pushed passwd"; fi

group.time: $(DIR)/group
```

```make
hosts.time: $(DIR)/hosts

@$(sed -e "^#/d" -e s.*/$/) $(DIR)/hosts $(CHKPIPE) | \

$(STDOUT) $(CHKPIPE) \
```

```awk
awk '{ for (i = 2); i <= NF; print $i, $0 }' '$(DOM)' | \

$(MAKDB) $(B) - $(YPDB) $(DOM) hosts.byname

awk '{ for (i = 2); i <= NF; print $i, $0 }' '$(DOM)' | \

$(MAKDB) $(B) - $(YPDB) $(DOM) hosts.byaddr

@touch hosts.time;

@echo "updated hosts";

if [ ! $NOPUSH ]; then $(YPPUSH) -d $(DOM) hosts.byname; fi

if [ ! $NOPUSH ]; then $(YPPUSH) -d $(DOM) hosts.byaddr; fi

if [ ! $NOPUSH ]; then echo "pushed hosts"; fi

ethers.time: $(DIR)

networks.time: $(DIR)

services.time: $(DIR)

rpc.time: $(DIR)

protocols.time: $(DIR)

netgroup.time: $(DIR)

bootparams.time: $(DIR)

alias.time: $(ALIASES)

netmasks.time: $(DIR)

password.time: $(DIR)

group: $(DIR)

auto.share: $(DIR)

netid: $(DIR)

timezone: $(DIR);
```

从这个示例可以看出，有许多地方引用了相应映射更新的时间点。这些文件仅在处理后才被修改；否则，不需要更新——映射的最新版本已经存在。唯一有趣的部分是关联的时间戳，文件本身的大小为零，这可以通过下面的文件列表看到：

```
ls -l /var/yp*

-rw-xr-r-- 1 root 0 Jul 21 11:36 ../aliases.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../auto.time

-rw-xr-r-- 1 root 0 Jul 21 11:37 ../passwd.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../protocols.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../publickey.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../rpc.time

-rw-xr-r-- 1 root 0 Jul 21 11:36 ../aliases.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../auto.time

-rw-xr-r-- 1 root 0 Jul 21 11:37 ../passwd.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../protocols.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../publickey.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../rpc.time

-rw-xr-r-- 1 root 0 Jul 21 11:36 ../aliases.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../auto.time

-rw-xr-r-- 1 root 0 Jul 21 11:37 ../passwd.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../protocols.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../publickey.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../rpc.time

-rw-xr-r-- 1 root 0 Jul 21 11:36 ../aliases.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../auto.time

-rw-xr-r-- 1 root 0 Jul 21 11:37 ../passwd.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../protocols.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../publickey.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../rpc.time

-rw-xr-r-- 1 root 0 Jul 21 11:36 ../aliases.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../auto.time

-rw-xr-r-- 1 root 0 Jul 21 11:37 ../passwd.time

-rw-xr-r-- 1 root 0 Jun 24 09:51 ../protocols.time
```
