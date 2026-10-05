

# 第 21 章 NIS 与 LDAP

关于这些用户和组的信息。将 `MINUID` 设置为您想要在 NIS 映射表中包含的最低 UID 号，并将 `MINGID` 设置为您想要包含的最低 GID 号。

Ubuntu: 1000/1000

NFSNOBODYUID,
FSNOBODYGID

分别指定名为 `nfsnobody` 的用户的 UID 和 GID。NIS 不导出此用户的值。设置为 0 以导出 `nfsnobody` 的映射表。

Ubuntu: 4294967295/4294967295

MERGE_PASSWD,
MERGE_GROUP

当设置为 `TRUE` 时，分别在 `passwd` 和 group 映射表中创建 `/etc/shadow`、`/etc/passwd` 文件以及 `/etc/gshadow` 和 `/etc/group` 文件，从而启用影子用户密码和组密码。

Ubuntu: FALSE/FALSE

## 文件位置

`/var/yp/Makefile` 的后续部分指定了标准文件位置；通常不需要更改这些条目。makefile 的这部分分为以下几组：

- 命令 (Commands)：调用 `awk` 和 `make` 并设置 `umask` 值（第 459 页）
- 源目录 (Source directories)：定位包含 NIS 源文件的目录
- NIS 源文件：定位构建 NIS 数据库的 NIS 源文件
- 服务器 (Servers)：定位列出 NIS 服务器的文件

## ALL 目标

`/var/yp/Makefile` 中的 `ALL` 目标指定了构建 NIS 的映射表：

```
ALL =\ passwd group rpc services protocols netgrp
ALL #= pubkey mail ethers bootstraps printcap
ALL #= auto.home.master auto.home.local
ALL #= timezone locals netmasks
```

`ALL` 目标的第一行列出了默认构建的映射表。该行以单词 `ALL` 开始，后跟等号和一个制表符。最后三行被注释掉了。取消注释并删除或移动映射表，直到列表符合您的需求。

根据需要，您可以更改 `Makefile` 中的 `ALL` 目标并在 `/var/yp` 目录下运行 `make` 来修改 NIS 分发的映射表列表。

## 启动服务器

在完成上述步骤后，重启主服务器（第 745 页），然后重启从服务器。在主服务器上，`nis init` 脚本启动 `ypserv`、`ypppasswd`、`ypfrd` 守护进程。如果您在本地系统上运行 NIS 客户端，它还会启动 `ypbind`。在从服务器上，`nis init` 脚本启动 `ypserv` 守护进程以及可选的 `ypbind` 守护进程。

在运行 `ypinit`（下一节讨论）之前启动主服务器，必须避免出现错误；如第 745 页“No server”部分所述，启动需要很长时间。运行 `ypinit` 后，您必须重启服务器（第 745 页）。

`ypfrd` 守护进程加速了从主服务器到从服务器复制 NIS 数据库的过程。它允许从服务器复制映射表，避免每个从服务器都复制原始数据并编译映射表。当 NIS 从服务器收到收到有新映射表的消息时，它会启动 `ypfrd` 并从服务器读取映射表。

`ypfrd` 守护进程仅在主服务器上运行；没有在从服务器上运行。更多信息请参见第 750 页的“前提条件”。

## ypinit：构建或导入映射表

`ypinit` 工具用于构建或导入并安装 NIS 数据库。在主服务器上，`ypinit` 从 `/etc` 中的 `password`、`group`、`hosts`、`networks`、`services`、`protocols`、`nitro` 和 `rpc` 文件收集信息并构建数据库。在从服务器上，`ypinit` 从主服务器复制数据库。

您必须通过提供绝对路径（`/usr/lib/ypinit`）来运行 `ypinit`。`-m` 选项在服务器上创建子目录 `/var/yp` 并构建其中的映射表；在从服务器上使用 `-s master` 选项从名为 `master` 的主服务器导入映射表。在以下示例中，`ypinit` 会询问每个从服务器的名称；因为它已经有了主服务器的名称，因为此命令是在运行主服务器的系统上执行的（请在示例中添加 `plum`）。在列表末尾单独按 `CONTROL-D` 结束。当您回答服务器列表是否正确的查询时，`ypinit` 构建 `ypsvers` 映射表并调用 `/var/yp/Makefile` 执行 `make`，从而构建指定的映射表。

```
$ sudo /usr/lib/ypinit -m
```

此时，我们必须构造运行 NIS 服务器的主机列表。`dog` 在 NIS 服务器主机列表中。继续添加其他主机的名称，每行一个。完成列表后，输入添加：`plum`

下一个要添加的主机：CONTROL-D

当前的 NIS 服务器列表如下：

plum
这正确吗？[y:n] y
我们需要几分钟来构建数据库...
正在构建 /var/yp/mgs/ypsvers...
运行 /var/yp/Makefile...

```
make[1]: 进入目录 '/var/yp/mgs'
Updating passwd.byname...
Updating passwd.byuid...
Updating group.byname...
Updating group.byid...
Updating hosts.byname...
Updating hosts.byaddr...
Updating rpc.byname...
Updating rpc.number...
Updating services.byname...
Updating services.byservic...
Updating netid.byname...
Updating protocols.number...
Updating protocols.byname...
Updating netgroup...
Updating netgroup.by...
Updating netgroup.user...
Updating shadow.byname...
make[1]: 离开目录 '/var/yp/mgs'
```

## 756 第 21 章 NIS 与 LDAP

