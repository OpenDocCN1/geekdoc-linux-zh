
## 指定从服务器：NOPUSH

如果您计划设置 NIS 从服务器，则需要告知 NIS 主服务器将生成的映射推送到从服务器。如果您希望使用从服务器，请将 `NOPUSH` 变量更改为 `false`。

> **注意**：如果您现在不需要从服务器但认为以后会需要，您可以在稍后添加服务器时更改此选项。

```makefile
# If we have only one server, we don't have to push the maps to the
# slave servers (NOPUSH=true); if you have slave servers, change this
to "NOPUSH=false" and put all hostnames of your slave servers in
# the file /var/yp/ypservers.
NOPUSH=true
```

请记住在 `/var/yp/ypservers` 文件中列出从服务器的主机名。并且，对于您在其中列出的每个主机名，请确保在 `/etc/hosts` 文件中列出相应的条目。

## 最小 UID 和 GID：MINUID 和 MINGID

当添加账户时，在 `/etc/passwd` 和 `/etc/group` 文件中创建的最小 UID 和 GID 会因您的 Linux 发行版而异。请务必设置您愿意通过 NIS 共享的最小 UID 和 GID 值。显然，您不希望通过 NIS 共享 root 条目，因此最小值永远不应为零。

```makefile
# We do not put passwd entries with lower UIDs (the root and system
# entries) in the NIS passwd database. For security. MINUID is the
# lowest uid that will be included in the passwd maps.
MINUID=500
# MINGID is the lowest gid that will be included in the group maps.
MINGID=500
```

## 将 Shadow 密码与真实密码合并：MERGE_PASSWD

为了使 NIS 能够用于其他系统对用户进行身份验证，您需要允许共享加密的 passwd 条目。如果您使用 shadow 密码，NIS 会自动为您处理此操作，通过从 `/etc/shadow` 文件中获取加密字段并将其合并到 NIS 共享的 `/etc/passwd` 副本中。除非有特定原因不想启用加密密码共享，否则请保持 `MERGE_PASSWD` 设置不变。

```makefile
# Should we merge the passwd file with the shadow file ?
# MERGE_PASSWD=true/false
MERGE_PASSWD=true
```

## 将 Group Shadow 密码与真实组合并：MERGE_GROUP

`/etc/group` 文件允许将密码应用于组设置。由于 `/etc/group` 文件需要公开可读，一些系统已开始支持 shadow 组文件——这些文件在性质上类似于 shadow passwd 文件。除非您有 shadow 组文件，否则需要将 `MERGE_GROUP` 设置设为 `false`。

```makefile
# Should we merge the group file with the gshadow file ?
# MERGE_GROUP=true/false
MERGE_GROUP=false
```

## 指定文件名

以下 Makefile 片段显示了预配置为通过 NIS 共享的文件。然而，仅因为它们列在这里，并不意味着它们会被自动共享。此列表只是为 Makefile 中稍后的使用建立文件名。

大多数条目以 `$(YPSRCDIR)` 开头，这是一个在 Makefile 此部分之前刚设置的变量。该变量的默认值是 /etc，这意味着运行 Makefile 时，`$(YPSRCDIR)` 的任何出现都会被替换为 /etc。因此，`GROUP` 将等于 `/etc/group`，`PASSWD` 将变为 `/etc/passwd`，等等。此外，变量 `$(YPYPWDIR)` 也设置为 /etc。

> **注意**：在原文中，该变量在一个实例中引用为 `$(YYPWDIR)`，在另一个实例中引用为 `$(YPSRCDIR)`，且代码块使用的是 `$(YPYPWDIR)`。标准 NIS Makefile 使用 `YPSRCDIR` 和 `YPYPWDIR`。文本提到“该变量的默认值是 /etc”，这通常适用于 `YPSRCDIR` 或基础目录。代码块明确定义 `GROUP = $(YPYPWDIR)/group`。我将保留文本可能的意图，即 `YPYPWDIR` 和 `YPSRCDIR` 均设置为 /etc。

```makefile
# These are the files from which the NIS databases are built. You
# may edit these to taste in the event that you wish to keep your NIS
# source files separate from your NIS server's actual configuration
# files.
#
GROUP		= $(YPYPWDIR)/group
PASSWD		= $(YPYPWDIR)/passwd
SHADOW		= $(YPYPWDIR)/shadow
GSHADOW		= $(YPYPWDIR)/gshadow
ADJUNCT		= $(YPYPWDIR)/passwd.adjunct
ALIASES		= $(YPSRCDIR)/aliases # could be in /etc or etc/mail
MAILALIAS	= /etc/aliases
ETHERS		= $(YPSRCDIR)/ethers # ethernet addresses (for rarpd)
BOOTPARAMS	= $(YPSRCDIR)/bootparams # for booting Sun boxes
				# (bootparamd)
HOSTS         = $(YPSRCDIR)/hosts
NETWORKS      = $(YPSRCDIR)/networks
PROTOCOLS     = $(YPSRCDIR)/protocols
PUBLICKEYS    = $(YPSRCDIR)/publickey
RPC           = $(YPSRCDIR)/rpc
SERVICES      = $(YPSRCDIR)/services
NETGROUP      = $(YPSRCDIR)/netgroup
NETID         = $(YPSRCDIR)/netid
AMD_HOME      = $(YPSRCDIR)/amd.home
AUTO_MASTER   = $(YPSRCDIR)/auto.master
AUTO_HOME     = $(YPSRCDIR)/auto.home
```

## 共享的内容：all 条目

在以下 Makefile 条目中，`all:` 后面列出的所有映射即为将被共享的映射。

```makefile
all: passwd group hosts rpc services netid protocols netgrp mail \
       #shadow publickey # networks ethers bootparams amd.home \
       auto.master auto.home passwd.adjunct
```

请注意，续行符反斜杠（`\`）用于确保 make 程序将整个行视为一行，即使它实际上是三行。此外，请注意第二行以 `#` 开头，这意味着该行的其余部分被注释掉了。

根据此格式，您可以看出配置为共享的映射是 passwd、group、hosts、rpc、services、netid、protocols、netgrp 和 mail。这些条目对应于 Makefile 前一部分中列出的文件名。当然，并非所有站点都希望共享这些条目，或者它们希望共享额外的映射（如 autoconf、auto_master、auto_home）。要更改您希望共享的映射，请更改该行，使您不希望共享的映射列在 `#` 符号之后。

例如，假设您只希望共享 passwd、group、auto_master、auto_home 和 netid 映射。您将 `all` 行更改为以下内容：

```makefile
all: passwd group auto.master auto.home netid \
       # hosts rpc services protocols netgrp mail \
       # shadow publickey networks ethers bootparams amd.home \
       # passwd.adjunct
```

请注意，`all` 行中的顺序并不重要。上述条目的放置只是为了使它们易于阅读。

## 使用 ypinit

一旦 Makefile 准备就绪，您需要使用 ypinit 命令初始化 YP (NIS) 服务器。

> **注意**：请记住，在运行 ypinit 命令之前，必须已经设置域名。这是使用本章前面所示的 domainname 实用程序完成的。

```bash
[root@ford /root]# /usr/lib/yp/ypsetup -m
```

其中，`-m` 选项告诉 ypinit 将系统设置为主 NIS 服务器。假设我们在名为 ford.domain.com 的系统上运行此命令，我们将看到系统响应如下：

此时，我们需要构建一个将要运行 NIS 服务器的主机列表。ford.domain.com 在 NIS 服务器主机列表中。请继续添加其他主机的名称，每行一个。当您完成列表时，输入 `<control D>`。

```text
next host to add:  ford.domain.com
next host to add:
```

继续输入所有辅助 NIS 服务器的名称。当您添加完所有必要的服务器后，按 CTRL-D。这些条目将为您放置在 `/var/yp/ypservers` 文件中；如有必要，您可以稍后通过编辑该文件来更改它们。

完成后，ypinit 将自动为您运行 make 程序，以构建映射并将其推送到您指定的任何辅助服务器。

## Makefile 错误

如果在 Makefile 中犯了错误，当 ypinit 运行 make 程序时您可能会遇到错误。如果您看到此错误：

```text
gmake[1]: *** No rule to make target '/etc/shadow', needed by `passwd.byname'.  Stop.
```

请不必担心。这意味着您指定了在此错误消息中不存在的文件进行共享。您可以创建该文件，或者返回编辑 /etc/Makefile 以不共享该文件。（参见前一部分“共享的内容：The all Entry”。）

另一个常见的错误消息是：

```text
failed to send `clear' to local ypserv: RPC: Program not registered
Updating passwd.byid...
failed to send `clear' to local ypserv: RPC: Program not registered
gmake[1]: *** No rule to make target `/etc/ypgroup', needed by `group.byname'.  Stop.
gmake[1]: Leaving directory `/var/yp/orthew.planetsoird.org'
```
