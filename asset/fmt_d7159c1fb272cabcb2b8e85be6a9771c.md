
# log file

Samba 日志文件名。Samba 将 `%m` 替换为客户端名称，允许为每个客户端生成单独的日志文件。

默认：`none`

Red Hat:`/var/log/samba/%m.log`

# log level

设置日志级别，`0`（零）为关闭，数字越大越详细。

默认：`0 (off)`

# max log size

一个整数，指定日志文件的最大大小（单位为 `KB`）。`0` 表示不限制。当文件达到此大同时，Samba 会在文件名后添加 `.old` 并开始新日志，删除任何旧日志文件。

默认：`5000`

Red Hat:`50`

# Browser Parameters

域主浏览器（`domain master browser`）是负责在浏览 Windows 网络邻域或“我的位置”时列出网络机器的系统。`SMB`（第 1055 页）每 `1115` 分钟进行一次加权选举，以决定哪台机器作为域主浏览器。

Samba 服务器是否赢得选举取决于两个参数：首先，将 `domain master` 设置为 `YES` 指示 Samba 服务器进入选举。其次，`os level` 决定了 Samba 服务器的权重。此选项与大多数最新的 Windows 版本不兼容。（此处由于原文重复，已按要求处理）。

确定共享是否可以浏览，例如在 Windows 的“网络位置”中浏览。

默认值：`YES`

Red Hat：`NO`

# comment

共享的描述，当从 Windows 浏览时显示。

默认值：`none`

Red Hat：`various`

# guest ok

允许以 `guest` 登录的用户访问此共享。

默认值：`NO`

# path

正在共享的目录路径。

默认值：`none`

Red Hat：`various`

# read only

不允许写入访问。

默认值：`YES`

## [homes] 共享：用户家目录

用户经常希望将他们的 Linux 家目录共享给 Windows 机器。为了方便完成此任务，Samba 提供了 `[homes]` 共享。当你定义此共享时，每个用户的家目录都将被共享。在大多数情况下，以下参数是足够的：

```
comment = Home Directories
browseable = no
writable = yes
```

这些设置防止了所有者以外的用户浏览家目录，同时允许登录的所有者完全访问权限![](img/0f75ae90508d4578c00a5b09fe29d_972_0.png)

如果系统运行带有目标策略的 `SELinux`，且你想允许用户共享他们的家目录（如本节所述），你必须开启 `Samba 允许共享家目录` 设置，见 `system-config-security`（第 402 页）。![](img/0f75ae90508d4578c00a5b09fe29d_972_1.png)

![](img/00a5b09fe29d_972_2.png)

## 从 Windows 访问 Linux 共享

### 浏览共享

要从 Windows 访问 Samba 服务器上的共享，在 Windows 系统上打开“我的电脑”或“资源管理器”，并在地址框输入 Samba 服务器的 `NetBIOS` 名称（如果没有分配 `NetBIOS` 名称，则输入主机名）。Windows 将显示 Linux 系统共享的目录。要查看名为 `bravo` 的 Linux 系统共享，例如输入 `\bravo`。从此窗口，你可以查看 Linux 系统上可用的共享。如果你设置共享不可浏览，则需要使用 `\servername:sharename` 格式输入共享。

访问 Samba 服务器共享的另一种方法是映射网络驱动器。在 Windows 系统上打开“我的电脑”或“资源管理器”，点击菜单栏上下拉菜单中的“映射网络驱动器”。Windows 会显示“映射网络驱动器”窗口。从组合框中选择一个未分配的驱动器号，输入你刚刚创建的共享路径。（当使用 `system-config-samba` 创建共享时，共享框与驱动器名称相同）。假设 Linux 系统上的共享名为 `tmp`，在组合框中选择 `J`，在文件夹框中输入 `bravo:tmp`，然后点击“完成”。你应该能够在 Windows 机器上通过 `J` 访问 `bravo` (`tmp`)。如果你无法映射驱动器，请参考第 714 页的“故障排除”。

## 从 Linux 访问 Windows 共享

作为客户端，Samba 允许你从 Linux 系统查看并操作 Windows 系统的文件。本节讨论了从 Linux 访问 Windows 文件的几种方法。

### smbtree：显示 Windows 共享

`smbtree` 工具显示可用共享的层级结构。当你运行 `smbtree` 时，它会提示输入密码；如果你想浏览 `guest` 用户可见的共享（例如 `[homes]` 共享中的用户目录），以下是 `smbtree` 的示例输出：

```
$ smbtree
Password:
MGS
\PB
  \|mark pb Samba
  \|MainPrinter MainPrinter
  \|ADMIN$ IPC Service (pb Samba)
  \|IPC$ IPC Service (pb Samba)
  \|tmp temp
```

在前面的输出中，`MGS` 是工作组名称，`PB` 是 Windows 机器名称，`mark` 和 `tmp` 是目录共享，`MainPrinter` 是共享打印机。工作组和机器名称始终大写。更多信息请参考 `smbtree` 手。

### smbtclient：连接 Windows 共享

`smbtclient` 工具类似于 `ftp` (`601`)，连接 Windows 共享；然而，`smbtclient` 使用 Linux 正斜杠 (`/`) 而不是 Windows 式的反斜杠 (`\`)。下一个示例连接到上一个示例显示的共享之一：

```
$ smbtclient //PB/mark
Password:
[Domain OS]=[Unix] Server~[Samba 3.0.10-1.tc2]
smb: > ls
nD D Wed Feb 22 15:10:03 2006
D D Mon Feb 6 12:40:17 2006
D D Tue Feb 7 22:24:17 2006
.kde DH
.emacs DH Mon Feb 6 10:12:45 2006
.bash_logout H 24 Tue Oct 25 06:15:04 2005
.bash_profile H 191 Tue Oct 25 06:15:04 2005
.bashrc H 124 Tue Oct 25 06:15:04 2005
```

## 浏览 Windows 网络

使用 `smbt` 浏览 Windows 共享相比于从 Windows 浏览网络显得相当笨拙；`Gnome` 和 `KDE` 提供了更友好的界面。在 Windows 上的“我的电脑”或“资源管理器”（或 `KDE` 的文件管理器），在位置栏输入 `smb/` 来浏览 Samba 上的共享。

`Konquer` 和 `Nautilus` 使用虚拟文件系统，它们并不是原生系统的一部分。结果，只有原生 `Gnome` 应用程序可以打开远程共享。

## 挂载 Windows 共享

`mount` (`466`) 使用 `cifs` 选项将 Windows 共享挂载为 Linux 共享。关于 `CIFS` 协议的更多信息请见第 24 页。该语法如下：

```
# mount -t cifs host/share dir
```

其中 `host` 是系统名称，`share` 是共享名称，`dir` 是要挂载目录的绝对路径。

你可以使用 `cifs` 文件系统的 `uid`、`file_mode` 和 `dir_mode` 选项来建立挂载文件的所有权和权限。

```
username,file_mode=0644,dir_mode=0755
```

权限必须以零开头的八进制数字表示。更多信息请参考 `mount.cifs` 页。

## 故障排除

Samba 提供了三个工具可以帮助排查连接：`mbstatus` 工具显示打开连接的报告；`testpcm` 检查 `/etc/samba/smb.conf` 的语法并显示其内容；`testpr` 检查打印机的有效性。

当 Samba 无法工作时，以下步骤可以帮助缩小范围：

1. 重启 `smbd` 和 `nmbd` 守护进程。确保输出的最后几行显示 `OK`。

```
# /sbin/service smb restart
   Shutting down SMB services: [ OK ]
   Shutting down SMB services: [ OK ]
   Starting SMB services: [ OK ]
   Starting SMB services: [ OK ]
```

2. 运行 `testpcm` 检查 `smb.conf` 文件语法是否正确：

```
$ testpcm
Load smb config files from /etc/samba/smb.conf
Processing section "homes"
Processing section "printers"
Processing section "imp"
Loaded services OK.
Server role: ROLE_STANDALONE
...
```

> 如果你在 `smb.conf` 中漏掉关键字，你会得到类似这样的错误：

```
$ testpcm
Load smb config files from /etc/samba/smb.conf
Unknown parameter encountered: "workgroup"
Ignoring unknown parameter "workgroup"
...
```

3. 从连接的两端使用 `ping` (`365`) 确保网络畅通。

`net view`

4. 从 Windows 命令行提示符，使用 `net view` 显示此示例中服务器 `pb` 提供的可用共享列表：

```
C:>net view \pb
Shared resources at \pb
```

| 共享名称 | 用作 | 注释 |
| :--- | :--- | :--- |
| MainPrinter | 打印 | MainPrinter |
| mark | 磁盘 (UNC) | 用户目录 |
| tmp | 磁盘 | messages temp |

命令执行成功。

`net use`

5. 尝试从 Windows 命令行提示符映射驱动器。以下命令尝试将共享名称 `tmp` 挂载为 `X` 盘：

```
C:>net use x: \pb\tmp
The command completed successfully.
```

6. 从服务器查询 `nmbd` 服务器，使用特殊名称 `__SAMBA__` 作为服务器的 `NetBIOS` 名称。`-d 2` 选项开启级别 `2` 的调试器，它会产生相当数量的输出：

```
$ nmblookup -d 2 -B pb __SAMBA__
added interface ip=192.168.0.10 bcast=192.168.0.255
nmask=255.255.255.0
querying__SAMBA__ on 192.168.0.10
Got a positive name query response from 192.168.0.10 ( 192.168.0.10 )
192.168.0.10__SAMBA__<00>
```

7. 从服务器查询 `nmbd` 服务器获取客户端的 `NetBIOS` 名称。（机器 `jam` 是 Windows 客户端）。

```
$ nmblookup -B jam
querying * on 192.168.0.9
192.168.0.9 <->
```

省略 `-B jam` 选项可以查询所有 `NetBIOS` 名称。

`smbclient`

8. 从服务器使用带有 `-L` 选项的 `smbclient` 生成由服务器提供的共享列表：

```
$ smbclient -L pb
Password:
Domain=[PB] OS=[Unix] Server=[Samba 3.0.10-1.fc2]
```

| 共享名称 | 类型 | 注释 |
| :--- | :--- | :--- |
| tmp | 磁盘 | mgs temp |
| IPC$ | IPC | IPC 服务 (pb Samba) |
| ADMIN$ | IPC | IPC 服务 (pb Samba) |
| MainPrinter | 打印 | MainPrinter |
| mark | 磁盘 | 用户目录 |

Domain=[PB] OS=[Unix] Server=[Samba 3.0.10-1.fc2]

| 服务器 | 注释 |
| :--- | :--- |
| Workgroup | 主节点 |
| MGS | TUNAER |

9. 要从服务器查询主机，运行带有 `-M` 选项的 `nmblookup` 后跟工作组名称：

```
$ nmblookup -M MGS
querying MGS on 192.168.0.255
192.168.0.8 MGS<->
```

# 总结

Samba 是一套程序，使 Linux 和 Windows 能够共享目录和打印机。在 Linux 和 Windows 系统之间共享的目录或打印机被称为共享。要访问 Linux 系统上的共享，Windows 用户必须提供用户名和密码。用户名必须直接与 Linux 用户名相对应，或者通过 `/etc/samba/smbusers` 文件进行映射。Samba 密码由 `smbspasswd` 生成并存储在 `/etc/samba/smbpasswd` 中。

主要的 Samba 配置文件是 `/etc/samba/smb.conf`，你可以使用文本编辑器、`swat`（一种基于 Web 的管理实用）或 `system-config-samba`（一个极简配置 GUI）对其进行编辑。`swat` 是一个强大的配置工具，提供了集成的在线文档和可点击的默认值，帮助你设置 Samba。

从 Windows 机器，你可以通过打开“我的电脑”或“资源管理器”，并在地址文本框中输入 `\\` 后跟服务器名称来访问 Linux Samba 服务器上的共享。Windows 会显示服务器上的共享，你可以像处理 Windows 文件一样操作它们。

从 Linux 系统，你可以使用多种 Samba 工具中的任意一种来访问 Windows 共享。这些工具包括 `smbtree`（显示共享）、`smclient`（类似于 `ftp`）以及带有 `t cifs` 选项的 `mount`（挂载共享）。此外，你可以在 `Conqueror` 或 `Nautilus` 的位置栏中输入 `smbc/` 并浏览共享。

## 练习

- 1. Samba 套件中包含哪两个守护进程？它们各自的作用是什么？

2. 将一个 Windows 用户映射到 Linux 用户需要哪些步骤？

3. 你如何只允许来自 `192.168.1.0/8` 子网的机器访问 `swat`？

4. `[homes]` 共享的目的是什么？

## 高级练习

- 5. 描述 Samba 处理用户的方式与 NFS 有何不同。

6. 如果你想在不配置主浏览器的情况下跨多个子网浏览 `SMB/CIFS`，你需要对路由器进行哪些配置更改？

7. 如何从远程位置安全地使用 `swat`？

8. `WINS` 解析允许主机定义自己的名称。请建议一种使用 Samba 从集中列表中分配名称的方法。

# 24. DNS/BIND: 跟踪域名和地址

| 本章内容 | |
| :--- | :--- |
| 快速入门 I: 设置 DNS | 733 |
| 快速入门 II: 设置 BIND | 734 |
| 设置 BIND | 739 |
| 故障排除 | 751 |
| 全功能服务器 | 752 |
| 从用服务器 | 756 |
| 分 Split 区域服务器 | 757 |

`DNS`（域名系统）将域名映射到 `IP` 地址，反之亦然。分级 `DNS` 数据库中的每个节点被称为领域，并以（领域）名称标记。与 Linux 文件系统结构相同，`DNS` 层次结构的顶端节点被称为根节点或根领域。虽然 Linux 文件系统结构使用斜杠（`/`）分隔节点和文件，并用斜杠标记根节点（目录），但 `DNS` 结构使用点图 24-1。

`BIND` 是目前最流行的 `DNS` 实现。然而，最近对其安全性产生了一些担忧。你可能希望在 `chroot` 环境中运行 `BIND` 或使用签名来提高安全性。

`DNS` 所做的映射最初是静态地在网络上每个系统的 `/etc/hosts` 文件完成的。小型局域网使用此文件。随着互联网的出现，需要一种动态映射系统。`DNS` 于 1983 年规范，`BIND` 于 1985 年成为 `BSD` 的。

# DNS 简介

你通常使用 `DNS` 显示页面。例如，你在浏览器中输入 `www.redhat.com`。然而，在 `IPv6` 中，`DNS` 在后台工作。

- **分级的**，使其能够提供响应。

- **分布式的**，跨越数个系统。

- **复制的**，以便当某些系统故障时，`DNS` 不会停止工作。

- **安全的**，以便你的浏览器被引导。

- **灵活的**，使其能够适应新名称。

- **快速的**，以便互联网连接。

# 节点、领域和子领域

分级 `DNS` 数据库中的每个节点被称为领域，并以（领域）名称标记。与 Linux 文件系统结构相同，`DNS` 层次结构的顶端节点被称为根节点或根领域。虽然 Linux 文件系统结构使用斜杠（`/`）分隔节点和文件，并用斜杠标记根节点（目录），但 `DNS` 结构使用点图 24-1。

我们从左到右读取 Linux 文件系统中的绝对路径：它从左侧的根目录 `/` 开始，向右我们读取所标识的文件路径。与 Linux 路径不同，你从右到左读取 `DNS` 域名名称：它从右侧的根（用点 `.` 表示）开始，向左穿过顶级域名和二级域名，到达子领域或主机。通常，域名名称会省略根的名称（右侧的点）。

`FQDN`（完全域名）
