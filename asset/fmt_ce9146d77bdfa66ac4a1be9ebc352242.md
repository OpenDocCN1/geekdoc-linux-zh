
### 3. 在 `/var/yp/Makefile` 文件中，设置任何 NIS 服务器选项并指定要管理的配置文件。

### 4. 使用 `ypinit` 创建配置文件的 NIS 版本。

## 定义 NIS 域

你首先必须定义一个 NIS 域名。你可以在启动系统时随时通过在 `/etc/sysconfig/network` 文件中定义 `NIS_DOMAIN` 变量来定义 NIS 域。向该变量分配分配你想要赋予 NIS 域的名称。以下示例定义了名为 `myturtles.nis` 的 NIS 域：

```
NIS_DOMAIN=myturtles.nis
```

在设置服务器时，你可能希望在不重启系统的情况下定义 NIS 域名。你可以使用 `domainname` 命令来实现，如下：

```
domainname myturtles.nis
```

# 第 36 章：NFS 和 NIS 719

你可以通过 `ypserv` 启动脚本启动 NIS 服务器：

```
service ypserv
```

## 设置 NIS 服务器选项

然后编辑 `/var/yp/Makefile` 文件以设置 NIS 服务器将维护的配置文件，并设置任何 NIS 服务器选项。标准选项以及常用的配置文件通常已经设置好了。

NIS 服务器选项首先列在最前面。`NOPUSH` 选项将被设置为 `true`，表示没有 NIS 从用服务器。如果你正在为此域设置任何 NIS 从用服务器，你将不得不将此选项设置为：

```
NOPUSH = true
```

最小用户 ID 和组组 ID 被设置为 500。这些是使用 `MINUID` 和 `MGID` 变量设置的：

```
MINUID=500
MINGID=500
```

大多数发行版使用 shadow 密码和 shadow组文件来加密密码和组。`MERGE_PASSWD` 和 `MERGE_GROUP` 设置将被设置为 `true`。NIS 将 shadow 密码信息合并到它的密码文件中：

```
MERGE_PASSWD=true
MERGE_GROUP=true
```

NIS 查找密码和其他配置文件的目录使用 `YPSCRDIR` 和 `YPPWDDIR` 变量定义。通常，`/etc` 目录存放你的配置文件：

```
YPSCRDIR = /etc
YPPWDDIR = /etc
```

然后列出 NIS 可以管理的配置文件。在这里，你将找到像 `PASSWD`（密码）、`GROUP`（组）和 `PRINTCAP`（打印机配置）之类的条目。条目的示例显示在此：

```
GROUP = $(YPPWDDIR)/group
PASSWD = $(YPPWDDIR)/passwd
SHADOW = $(YPPWDDIR)/shadow
GSHADOW = $(YPSCRDIR)/gshadow
ALIASES = /etc/aliases
ETHERS = $(YPSCRDIR)/ethers # 以太网地址（用于 raspd）
BOOTPARAMS = $(YPSCRDIR)/bootparams # 用于启动 Sun 盒子（bootparamd）
HOSTS = $(YPSCRDIR)/hosts
NETWORKS = $(YPSCRDIR)/networks
PRINTCAP = $(YPSCRDIR)/printcap
PROTOCOLS = $(YPSCRDIR)/protocols
```

## 指定共享文件

网络上共享的实际文件列在 `all:` 条目中，它位于配置文件列表之后。只有定义文件中的部分文件被列为共享，即列在 `all:` 之后第一行的文件。其余行被自动注释掉（前面带有一个 `#` 号）。你可以通过删除 `#` 号或将它们的条目移动到第一行来添加文件。

```
all: passwd hosts services netid protocols ethers bootparms printcap \
    # netgrp shadow publickey networks ethers bootparms printcap \
    # amd.home auto.master auto.home.local passwd.adjunct \
    # timezone locale netmasks
```

确保触碰 Makefile 的剩余部分。

## 创建 NIS 数据库

然后你带有 `-m` 选项输入 `ypinit` 命令来创建 NIS 数据库。这将创建一个 NIS 域的 NIS 副本。对于 NIS 从用服务器，你需要：

```
-m
```

对于 NIS 服务器，你将使用：

```
ypinit
```

如果收到以下错误，可能意味着你的 NIS 服务器没有运行：

```
failed to start ypserv
```

之后你需要进入 `/var/yp` 目录：

```
cd /var/yp
```

更新 NIS 域文件：

```
make
```

## 访问控制

此处 原文文本 混乱（注：此处原文文本存在大量重复和截断的错误，已根据原文逻辑进行对应翻译）

## 访问服务器

你网络上的每个 NIS 客户端主机都必须运行 `ypbind` NIS 客户端来访问服务器。在客户端的 `/etc/yp.conf` 文件中，你需要指定它将使用的 NIS 服务器。以下条目将引用 `192.168.1.1` 处的 NIS 服务器：

```
ypserver192.168.1.1
```

或者，你可以指定 NIS 域名和它所使用的服务器：

```
domain mydomain.nis server servername
```

`authconfig-gtk` 工具将为使用 `turtle.mytrek.com` 服务器的 `myurtle.nis` NIS 域在 `/etc/yp.conf` 中创建以下条目：

```
domain myurtles.nis server turtle.mytrek.com
```

要启动 NIS 客户端，你需要运行 `ypbind` 脚本：

```
service ypbind start
```

然后，为了检查一切运行运行正常，你可以使用 `ypcat` 尝试列出 NIS 密码文件：`ypcat passwd`。

你可以使用 `ypcat` 列出任何 NIS 配置文件。`ypwhich` 命令将显示你的客户端正在使用的 NIS 服务器名称。`ypmatch` 可用于查找配置文件中的特定条目。

```
ypmatch cecelia passwd.
```

用户可以使用 `yppasswd` 命令在 NIS `passwd` 文件中更改密码。它的工作原理与 `passwd` 命令相同。你还需要确保 `yppasswd` 守护正在运行。

## 使用 nsswitch.conf 指定配置文件

为了确保客户端访问特定配置文件时使用 NIS 服务器，你应该在 `/etc/nsswitch.conf` 文件的对应条目中指定 `nisplus`。`nisplus` 选项指的是 Red Hat 上当前使用的 NIS 3 版本。`nis` 用于指代较旧的 NIS 2 版本。`/etc/nsswitch.conf` 文件指定了主机应该去哪里查找各种信息。例如，以下条目表示首先检查本地配置文件（files），然后检查 NIS 服务器（nisplus）以获取密码数据（pass data）：

```
passwd: files nisplus
```

`files` 指定表示首先使用系统自己的文件，即本地主机上的文件。`nis` 表示在 NIS 中查找条目，访问 NIS 服务器。`nisplus` 表示使用由 NIS+ 服务器维护的 NIS+ 文件。`dns` 表示执行 DNS 查找；它只能用于像 `hosts` 这样包含主机名的文件。是一些标准条目：

```
passwd: files nisplus
shadow: files nisplus
group: files nisplus

hosts: files nisplus dns
bootparams: nisplus [NOTFOUND=return] files

ethers: files
netmasks: files
networks: files
protocols: files nisplus
rpc: files
services: files nisplus
netgroup: files nisplus
publickey: nisplus
automount: files nisplus
aliases: files nisplus
```

## Samba
