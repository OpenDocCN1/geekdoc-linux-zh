
> 注意：在 Mandrake 和 Red Hat 系统上，你还可以通过 `/etc/rc.d/initetfs` 脚本同时挂载和卸载所有的 NFS 系统，你可以通过 `service` 命令调用它。该脚本读取 `/etc/fstab` 文件中的 NFS 条目，并利用它们来挂载和卸载 NFS 远程目录。使用 `stop` 参数卸载文件系统，使用 `start` 参数重新挂载它们。`restart` 参数则先卸载后重新挂载文件系统。

## 按需挂载 NFS：autofs

你可以使用 `autofs` 服务来挂载 NFS 文件。这需要在客户端进行额外的配置。`autofs` 服务仅在你尝试访问文件系统时才会挂载它。对指定目录执行目录切换操作 (`cd`) 将触发挂载操作，从而在此时挂载远程文件系统。

`autofs` 服务通过一个主文件来列出映射文件，而映射文件反过来列出主文件。`/etc/auto.master` 文件就是 `autofs` 的主文件。它列出了可以挂载文件系统的根路径，以及这些路径中每个名称对应的映射文件。映射文件随后将列出键（子目录）、挂载选项以及可以在根路径目录下挂载的文件系统。在某些发行版中，`/auto` 目录已经实现为自动挂载文件系统的根路径。如果你愿意，可以在 `/etc/auto.master` 文件中添加你自己的配置以及映射文件。你会发现该文件包含了针对 `/auto` 目录的以下条目，并将 `auto.misc` 列为其映射文件：

```
/auto auto.misc --timeout=20
```

在映射文件中，你可以像上一个示例所示添加选项。`timeout` 选项定义了尝试自动卸载之前需要等待的空闲秒数。

在映射文件中，列出键、挂载选项和要挂载的文件系统。键将是本地系统上挂载文件系统的子目录。例如，要将 `rabbit.mytrek.com` 主机上的 `/home/projects` 目录挂载到 `/auto/projects` 目录，你需要使用以下条目：

```
projects soft,intr,time=20 rabbit.mytrek.com:/home/projects
```

## 第 34 章：NFS、NIS 和 AppleTalk

你也可以在主文件中为 NFS 系统创建一个新条目，如下所示：

```
/myprojects auto.myprojects --timeout 60
```

然后你将创建一个 `/etc/auto.myprojects` 文件，并在其中放置 NFS 系统挂载的条目，如下所示：

```
dylan soft,intr,rw rabbit.mytrek.com:/home/projects
newgamew soft,intr,ro lizard.mytrek.com:/home/supergame
```

`autofs` 服务可以用于任何文件系统，包括软磁盘和 CD-ROM。请参见第 29 章。

## 网络信息服务：NIS

在支持 NFS 的网络中，许多资源和设备由相同的系统共享。通常情况下，每个系统为每个设备或资源都需要自己的配置文件。更改将涉及逐个更新每个系统。然而，NFS 提供了一种名为网络信息服务 (NIS) 的特殊机制，它为整个网络维护此类配置文件。对于更改，你只需要更新 NIS 文件。NIS 适用于大多数管理任务所需的信息，例如与用户、网络访问或设备相关的任务。例如，你可以使用 NIS 服务维护用户和密码信息，只需更新那些 NIS 密码文件即可。

> `NIS+` 是 `NIS` 的更高级形式，提供了对加密和认证的支持。然而，它的管理更加困难。

NIS 由太阳微科技（Sun Microsystems）开发，最初被称为 Sun 黄页（Yellow Pages, YP）。NIS 文件保留在 NIS 服务器上（NIS 服务器仍称为 YP 服务器）。网络上的各个系统使用 NIS 客户端向 NIS 服务器发出请求。NIS 在特殊的数据库文件映射上维护其信息。Linux 存在 NIS 客户端和服务器版本。Linux 客户端可以使用 NIS 轻松连接到任何网络。

NIS 客户端作为 Linux 发行版初始安装的一部分进行。NIS 客户端程序包括 `ybind`（NIS 客户端守护进程）、`ypwich`、`ypcat`、`yppoll`、`ymatch`、`passwd` 和 `ypset`。每个程序都有详细说明使用的 Man 手页。NIS 服务器程序有 `ypserv`、`ybind`、`passwd`、`ypxup`、`ypxfer` 和 `netgroup`——每个也有自己的 Man 手页。`/usr/share/doc/HOWTO` 目录下有一个详细的 NIS HOW-TO 文档。

# Linux：完全参考

> 注意
> 你可以使用 `Linuxconf`、`Webmin`、SuSE 的 `Yast` 和 Red Hat 的 `authconfig` 等工具来指定网络上的远程 NIS 服务器。

## NIS 服务器

在设置 NIS 服务器时，你有很大的灵活性。如果你有一个小型网络，只需要一个 NIS 域，并配备一个 NIS 服务器。对于较大的网络，你可以将网络划分为几个 NIS 域，每个域都有自己的服务器。即使你只有一个域，也可以拥有主 NIS 服务器和若干个 NIS 从服务器。从服务器可以作为备份，以防主服务器宕机。从服务器仅包含 NIS 主服务器上设置的文件副本。配置 NIS 服务器涉及几个步骤：

- 定义 NIS 服务器将维护的 NIS 域。
- 启动 `ypserv` 守护进程。
- 在 `/var/yp/Makefile` 文件中设置任何 NIS 选项。
- 使用 NIS 域创建配置文件。
- 定义 NIS 域。

# 760 Linux：完全参考指南

```make
NETWORKS      = $(YPSRDIR)/networks
PRINTCAP     = $(YPSRDIR)/printcap
PROTOCOLS    = $(YPSRDIR)/protocols
PUBLICKEYS   = $(YPSRDIR)/publickey
RPC           = $(YPSRDIR)/rpc
SERVICES      = $(YPSRDIR)/services
NETGROUP     = $(YPSRDIR)/netgroup
NETID        = $(YPSRDIR)/netid
AMD_HOME      = $(YPSRDIR)/amd.home
AUTO_MASTER  = $(YPSRDIR)/auto.master
AUTO_HOME    = $(YPSRDIR)/auto.home
AUTO_LOCAL   = $(YPSRDIR)/auto.local
TIMEZONE     = $(YPSRDIR)/timezone
LOCALE       = $(YPSRDIR)/locale
NETMASKS     = $(YPSRDIR)/netmasks
```

在网络上共享的实际文件列在 `all:` ，位于配置文件列表之后。只有 `all:` 之后第一行定义的文件中会被共享。其余行被自动注释（前面带有 `#` 符号）。你可以通过移除 `#` 符号或将其项移动到第一行来添加文件。

```make
all: passwd group hosts services netid mail \
    # netgrp shadow publickey ethers bootparams printcap \
    # amd.home auto.master auto.home local passwdd.adjunct \
    # timezone locale netmasks
```

确保不要碰 Makefile 的其余部分。

然后带有 `-m` 选项输入 `ypinit` 命令，创建一个由 NIS 配置文件组成的 NIS 数据库。系统将检测你的 NIS 服务器，然后要求你输入在该域内使用的任何从 NIS 服务器名称。如果有，请输入它们。完成后，按 `CTRL-D`。NIS 数据库文件即被创建。

```bash
/usr/lib/yp/ypinit -m
```

此时，我们必须构建一个运行 NIS 服务器的主机列表。

`turtle.mytrek.com` 在 NIS 服务器主机列表中。

请继续添加其他主机的名称，每行一个。

完成列表后，输入 `<control D>`。

下一个添加的主机: `turtle.mytrek.com`

下一个的主机:

当前 NIS 服务器列表所示：

`turtle.mytrek.com`

# 第 34 节：NFS、NIS 和 AppleTalk 761
