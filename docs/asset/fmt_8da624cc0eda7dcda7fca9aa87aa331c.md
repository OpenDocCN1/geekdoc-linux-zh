
一旦数据库在服务器上建立，客户端就可以向服务器查询数据库条目。通常，当客户端在本地数据库中找不到条目时，会被配置为查找 NIS 映射，这时就会发生这种情况。主机可能只包含一个简单文件，其中仅包含系统在单用户模式下（没有网络连接时）运行所需的条目——例如 `/etc/passwd` 文件。当程序发出请求查找用户密码信息时，客户端检查其本地 `passwd` 文件，发现该用户不存在；然后客户端向 NIS 服务器发出请求，查找 `passwd` 表中对应的条目。如果 NIS 确实有该条目，它会返回给客户端，然后返回给最初请求信息的程序。该程序本身并不知道使用了 NIS。如果 NIS 映射返回的答案是用户 `passwd` 条目不存在，情况也是如此。程序会接收到信息，而不会知道中间发生了多少活动。

这当然适用于我们告诉 NIS 共享的所有文件。其他流行的共享文件包括 `/etc/group` 和 `/etc/hosts`。

> **注意：** 尽管从技术上讲将 NIS 的表称为数据库是正确的，但它们通常被称为映射 `maps`。（在此上下文中，我们正在将键映射到值。）以 *passwd* 文件为例，我们将用户的登录名（我们知道它是始终唯一的）映射到密码条目的其余部分。

## NIS 服务器

NIS 只能有一个权威服务器，原始数据文件保存在该服务器上（这有点像 DNS）。这个权威服务器被称为 *主* NIS 服务器。如果你的组织规模足够大，你可能需要在多台机器上分发负载。这可以通过设置一个或多个*辅助*（从属）NIS 服务器来实现。除了帮助分发负载之外，辅助服务器还提供了一种更好地处理服务器故障的机制。即使主服务器或其他辅助服务器宕机，辅助 NIS 服务器也可以继续回答查询。

每当*主* NIS 服务器更新时，辅助 NIS 服务器都会接收到更新，从而保持主服务器和从服务器处于*同步*状态。将辅助服务器与主服务器保持同步的过程称为*服务器推送*。作为其更新脚本的一部分，NIS 主服务器还会将映射文件的副本推送到辅助服务器。在接收到这些文件后，辅助服务器也会更新其数据库。直到辅助服务器也完全更新时，NIS 主服务器才认为自己是完全最新的。

> **注意：** 服务器可以同时既是服务器又是客户端。

## 域

主 NIS 服务器建立*域*，类似于 PDC 的域。一个显著的区别是，NIS 域不需要 NIS 服务器管理员明确允许客户端加入。此外，NIS 服务器只发送数据；它不执行身份验证。用户身份验证过程留给每个单独的主机；NIS 仅提供一个集中的用户列表。

> **注意：** 请记住，NIS 模型假设所有客户端都是同一管理域的成员，因此由同一系统管理员进行管理。

> **提示：** 由于 NIS 域必须被命名，使用与 DNS 域名不同的名称是一个良好的实践（虽然并非强制要求）。当每个人都清楚哪个是哪个时，你与同行管理员讨论网络域时会轻松得多。

## NIS 与黄页 (Yellow Pages)

当 NIS 在 1980 年代最初开发时，它被称为黄页（简称 YP）。当 Sun Microsystems（SunOS 操作系统（也称为 Solaris 1）的开发商）开始在英国销售其系统时，发生了冲突：“黄页”一词是英国电信公司的商标。为了避免诉讼，Sun 将该软件包重新命名为网络信息服務，其他 UNIX 厂商也纷纷效仿。

如今你会发现所有 NIS 工具仍以 `yp` 作为前缀，而不是 `nis`。出于某种原因，文件名没有随着软件包的正式名称一起更改。因此，请不要被 YP 和 NIS 的混合引用所困惑。它们都是同一件事。

## 配置主 NIS 服务器

Linux 发行版通常已经编译并安装了 NIS。你所要做的就是启用该服务（如果尚未启用）。为此，你可以使用 `chkconfig` 工具，并确保 `ypserv` 是运行级别 3 和 5 启动过程的一部分。

启用 NIS 后，你需要进行配置。执行此操作有四个步骤：

1. 建立域名。
2. 启动 `ypserv` 守护进程以启动 NIS。
3. 编辑 `Makefile`。
4. 运行 `ypinit` 以创建数据库。

### 建立域名

设置 NIS 域名是通过 `domainname` 命令完成的。假设我们要设置一个名为 `ornet.domain.com` 的域；我们可以像这样告诉系统 NIS 域的名称：

```
[root@ford /root]# domainname ornet.domain.com
```

当然，为了在每次重启时都能建立此设置，我们需要将 `domainname` 命令放入一个 `rc` 脚本中。

- 如果你使用的是 Red Hat，你可以编辑 `/etc/sysconfig/network` 并添加这一行：

  `NIS_DOMAIN=ornet.domain.com`

- 非 Red Hat 用户可以编辑 `/etc/rc.d/init.d/ypserv` 脚本。搜索包含 "`domainname.`" 的行，如果找不到，则在第一行后的任何位置添加一行。该行应如下所示：

  `domainname ornet.domain.com`

  并且你会用你自己的 NIS 域名替换 `ornet.domain.com`。

- 设置域名应在 NIS 服务器启动之前进行。

### 启动 NIS

`ypserv` 守护进程负责处理 NIS 请求。如果你正在向正在运行的服务器安装 NIS，你很可能不希望重启服务器以完成安装。相反，你可以简单地自己运行 init 脚本，如下所示：

```
[root@ford root]# /etc/rc.d/init.d/ypserv start
```

如果你需要随时停止 NIS 服务器，你可以使用以下命令

```
[root@ford root]# /etc/rc.d/init.d/ypserv stop
```

### 编辑 Makefile

你在其他许多章节中看到过 `make` 命令用于编译程序。然而，`make` 工具并不执行编译——它只是跟踪哪些文件需要被编译，然后调用必要的程序来执行编译。实际包含 make 指令的文件称为 `Makefile`。

`make` 工具是高效的，因为它调用的程序是任意的。你可以用你首选的编译器替代特定 Linux 发行版附带的编译器。当 `make` 看到文件的日期和时间已更改时，`make` 认为这意味着文件的内容已更改。如果文件已更改，这就告诉 `make` 该文件需要重新编译。

将这个概念应用于 NIS 非常简单明了。在这种情况下，有一系列需要转换为数据库格式的纯文本文件。我们需要一个工具来恢复任何已更改的文件——你可以看到 `make` 正符合需求！

切换到 `/var/yp` 目录，我们看到一个名为 `Makefile` 的文件（是的，全部是一个单词，且 M 大写）。此文件列出了通过 NIS 共享的文件，以及一些附加的-

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
