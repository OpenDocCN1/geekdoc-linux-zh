
`*Directory host1*`(`*options*`) `*host2*`(`*options*`) ...

第一个字段是通过 NFS 共享的目录，随后是跟在后面的一个或多个指定哪些主机可以远程挂载该目录的字段，以及括号中的几个选项。

你可以用名称或 IP 地址指定主机，包括地址范围。

![](img/3e16ea99a8df672d45599724c19769ac_437_0.png)

## 使用 Samba 和 NFS

括号中的选项表示每个主机被授予的访问类型，以及服务器上的用户 ID 和用户组 ID 是如何映射到客户端的 ID 的。（例如，如果文件在服务器上归 `root` 所有，那么在客户端上的所有者是谁？）在括号内，用逗号分隔选项。如果允许一个主机同时具有读和写权限，且所有 ID 都映射到匿名用户（默认情况下，匿名用户名为 `nobody`），则选项如下：

`(rw,all_squash)`

表 4-1 显示了可以在 `/etc/exports` 文件中使用的选项。你可以发现两类选项：通用选项和用户 ID 映射选项。

表 4-1 **/etc/exports 中的选项**

| 选项 | 描述 |
| :--- | :--- |
| **通用选项** | |
| `secure` | 仅允许来自端口 1024 或以下的连接（默认） |
| `insecure` | 允许来自端口 1024 或更高版本的连接 |
| `ro` | 允许只读访问（默认） |
| `rw` | 允许读取和写入访问 |
| `sync` | 在请求时执行写入操作（向磁盘写入信息）（默认） |
| `async` | 在服务器准备好时执行写入操作 |
| `no_wdelay` | 立即执行写入操作 |
| `wdelay` | 等待一下是否有相关的写入请求到达，然后一起执行它们（默认） |
| `hide` | 隐藏作为另一个导出目录的子目录的导出目录（默认） |
| `no_hide` | 使目录不隐藏（`hide` 的反面） |
| `subtree_check` | 执行子树检查，这涉及到在每次访问文件时检查导出的子目录的 目录的父目录（默认） |
| `no_subtree_check` | 关闭子树检查（`subtree_check` 的反面） |
| `insecure_locks` | 允许不安全的文件锁定 |
| *(续)* | |

在 `/etc/exports` 文件中添加条目后，在终端窗口中输入以下命令手动导出文件系统：

`exportfs -a`

此命令导出 `/etc/exports` 文件中定义的所有文件系统。现在你可以启动 NFS 服务进程。

在 Debian 中，以 `root` 登录并在终端窗口中输入 `/etc/init.d/nfs-kernel-server start`。在 Fedora 中，输入 `/etc/init.d/nfs start`。在 SUSE 中，输入 `/etc/init.d/nfsserver start`。如果你希望系统启动时启动 NFS 服务，在 Debian 中输入 `update-rc.d nfs-kernel-server defaults`。在 Fedora 中，输入 `chkconfig --level 3 nfs on`。在 SUSE 中，输入 `chkconfig --level 3 nfsserver on`。

![](img/3e16ea99a8df672d45599724c19769ac_440_0.png)

在你的 Linux PC 上安装并配置 Samba 之后，你的客户端 PC——即使它们运行的是旧版本的 Windows 操作系统或较新的 Windows 版本——也可以访问 Linux PC 上的磁盘和打印机。为了实现这一点，它们使用通用互联网文件系统（CIFS）协议，这是 Windows 文件和打印机共享的底层协议。

安装 Samba 软件包后，你可以让你的 Linux PC 变成 Windows 客户端，这意味着 Linux PC 可以访问由 Windows 服务器维护的磁盘和打印机。同时，你的 Linux PC 也可以是网络上其他 Windows 系统的客户端。

Samba 软件包包含以下主要组件：

- `/etc/samba/smb.conf`: SMB（服务器消息块）服务器程序所使用的 Samba 配置文件。
- `/etc/samba/smbusers`: 一个 Samba 配置文件，显示与本地 Linux PC 用户名对应的 Samba 用户名。
- `nmbd`: NetBIOS 名称服务器，客户端通过它来查找服务器。（*NetBIOS* 代表 *Network Basic Input/Output System*——一种应用程序用于与网络传输层（如 TCP/IP）通信的接口。）
- `nmblookup`: 一个命令，用于返回通过 NetBIOS 名称标识的 Windows PC 的 IP 地址。
- `smbadduser`: 一个将用户添加到 SMB 密码文件的程序。
- `smbcacls`: 一个用于操作共享文件上的 Windows NT 访问控制列表的程序。
- `smbclient`: Windows 客户端，运行在 Linux 上，并允许 Linux 访问任何 Windows 服务器上的文件和打印机。
- `smbcontrol`: 一个向 `smbd`、`nmbd` 或 `winbindd` 进程发送消息的程序。
- `smbd`: SMB 服务器，接受 Windows 客户端的连接并提供文件共享和打印共享服务。
- `smbmount`: 一个在 Linux PC 上挂载 Samba 共享目录的程序。
- `smbpasswd`: 一个更改 SMB 用户密码的程序。
- `smbprint`: 一个启用 SMB 服务器上打印机打印功能的脚本。
- `smbstatus`: 一个列出本地主机当前 SMB 连接的命令。
- `smbtar`: 一个在 Linux 系统上将 SMB 共享直接备份到磁带驱动器的程序。
- `smbumount`: 一个卸载当前挂载 Samba 目录的程序。
- `testparm`: 一个确保 Samba 配置文件正确的程序。
- `winbindd`: 一个解析 Windows NT 服务器名称的服务器。

![](img/3e16ea99a8df672d45599724c19769ac_441_0.png)

## 安装 Samba

你可能在安装 Linux 时已经有了 Samba。以下章节描述了如何配置和使用 Samba。要检查 Samba 是否已安装，在 Debian 和 Ubuntu 上使用 `dpkg -l samba`，在 Fedora 上使用 `rpm -q samba`。在 Debian 和 Ubuntu 上使用 `apt-get install samba`。在 Fedora 上，以 root 身份登录并执行 `yum install samba-swat`。该命令不仅安装了 samba，还安装了 SWAT Samba 配置界面。在 SUSE 中，点击 YaST 中的软件包管理。安装 Samba 后，你必须配置它才能使用。

为了设置 Windows 文件共享和打印共享服务，你可以手动编辑配置文件，也可以使用图形用户界面（GUI）工具。使用 GUI 工具比编辑配置文件简单得多。Fedora 和 SUSE 都提供了配置 Samba 的 GUI 工具。

在 Fedora 中，选择系统设置 -> 高级 -> Samba 打开 Samba 服务器配置窗口。在提示处输入有效的用户名和密码。配置界面允许你创建和编辑 `/etc/samba/smb.conf` 中的项。

在 SUSE 中，可以通过 YaST 配置 Samba。从主菜单选择系统控制中心 (YaST)。点击窗口左侧的网络服务；然后点击右侧的 Samba 服务器。在弹出的窗口中选择工作组名称（YaST 会显示网络上的任何 Windows 工作组），然后点击下一步。然后你可以选择服务器类型并启用服务器。退出 Samba 配置工具后，YaST 将 Samba 设置存储在 `/etc/samba` 目录中。

![](img/3e16ea99a8df672d45599724c19769ac_443_0.png)

## 使用 Samba 和 NFS

## 了解更多 Samba

本章仅是对 Samba 的介绍。要了解更多关于 Samba 的信息，请参考以下资源：

- 查看 Samba 文档，访问 `www.samba.org/samba/docs/`。
- 阅读 *Using Samba,*（第3版，Gerald Carter, Jay Ts 和 Robert Eckstein 著）（O’Reilly & Associates, 2007）。

你还应该访问 `www.samba.org` 以获取 Samba 开发的最新动态。该网站还包含学习 Samba 的资源链接。

![](img/3e16ea99a8df672d45599724c19769ac_445_0.png)

## 脚本

### 目录摘要

- **第 1 章：Shell 脚本入门**。 . . . . . . . . . . . . . . . . . . . . . . 431
- 尝试简单的 Shell 脚本。. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 432
- 探索 Shell 脚本的基础知识。. . . . . . . . . . . . . . . . . . . . . . . . . 433
- **第 2 章：使用高级 Shell 脚本**。. . . . . . . . . . . . . . . . . . . . . . 443
- 尝试使用 sed。. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 443
- 使用 awk 和 sed。. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 446
- 关于 Shell 脚本的最后笔记 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 450
- **第 3 章：在 Linux 中编程**。. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 451
- 编程概述。. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 452
- 探索 Linux 中的软件开发工具。. . . . . . . . . . . . . . . . . . . . 453
- 理解 GNU 许可证的影响。. . . . . . . . . . . . . . . . . . . . . . . . . . 473

![](img/3e16ea99a8df672d45599724c19769ac_447_0.png)

## 入门 Shell 脚本 A

正如你在之前的许多章节中所看到的，Linux 为你提供了许多小型而专门的命令，并让你能够连接这些命令，使得一个命令的输出可以作为另一个命令的输入。`bash`（Bourne-Again Shell 的缩写）——大多数 Linux 系统的默认 shell——通过 I/O 重定向和管道的形式提供了这种能力。`bash` 还包含了条件判断，例如 `if` 语句（你可以用它仅在特定条件为真时运行命令）以及 `for` 语句（可以按指定的次数重复一组命令）。

在编写称为 shell 脚本的程序时，可以使用这些 `bash` 功能：存储在文件中的 Shell 命令集合。本章将向你展示如何编写 shell 脚本，它们用于自动化各种任务。例如，当你的 Linux 系统启动时，存储在 `/etc` 目录下各种子目录（如 `/etc/init.d`）中的许多脚本会执行许多初始化任务。

本章内容：
- 尝试一些 Shell 脚本
- 发现脚本的基础知识
- 探索 bash 的内置命令

### 尝试简单的 Shell 脚本

如果你不是编程人员，对脚本感到顾虑是很常见的。但你可以把这种想法抛在脑后：脚本（或编程）可以简单到只需将几个命令存储在文件中并执行该文件。事实上，你可以拥有一个只包含单个命令的实用 Shell 程序。Shell 脚本在系统管理员之间非常流行，因为它们可以帮助自动化你经常执行的任务。例如，如果硬盘似乎快满了，你可能想找到所有超过某些大小（例如， 5MB）且在过去 30 天内未被访问的文件。一旦找到了这些文件，你可能想向所有拥有这些文件的用户发送电子邮件，要求他们存档并清理这些文件。你可以通过 shell 脚本完成所有这些任务。你可以从以下 `find` 命令开始来识别大文件：

`find / -type f -atime +30 -size +5000k -exec ls -l {} > /tmp/largefiles`

此命令创建一个名为 `/tmp/largefiles` 的文件，其中包含占用空间过大的旧文件的详细信息。获取文件列表后，你可以使用其他 Linux 命令——如 `sort`、`cut` 和 `sed`——为需要清理大文件的用户准备并发送邮件。与其手动输入所有这些命令，不如将它们放在一个文件中创建一个 shell 脚本。简而言之，这就是 shell 脚本的本质——将命令收集在文件中，以便你轻松地执行系统管理任务。虽然你可以在命令行中不使用脚本来完成这一切，但这需要你每次都输入命令——包括参数和正确的语法。`bash` 脚本像大多数 Linux 命令一样接受命令行选项。在脚本内部，你可以将选项引用为 `$1`、`$2` 等。特殊名称 `$0` 指向脚本本身。这是一个接受参数的典型 `bash` 脚本：
