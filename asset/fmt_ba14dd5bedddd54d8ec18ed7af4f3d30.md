
`ls :/plum: No such file or directory`

```
$ sudo /etc/init.d/autofs reload
Reloading automounter: checking for changes ...
Reloading automounter map for: /free1
Reloading automounter map for: /plum
```

```
$ ls /free1 /plum
/free1:
/plum:
```

```
$ ls /plum/pl16
lost+found memo
```

接下来的命令显示有关已配置和激活的 `autofs` 挂载点的信息：

```
/etc/init.d/autofs status
Configured Mount Points:
/usr/sbin/automounter --timeout=60 /free1 /etc/auto.misc
/usr/sbin/automounter --timeout=300 /plum /etc/auto.plum
Active Mount Points:
/free1:
/plum:
```

# 总结

NFS 允许服务器向异构网络上的客户端共享本地目录层次结构，从而减少存储需求和管理开销。NFS 定义了客户端/服务器关系，服务器提供客户端可以挂载的目录层次结构。

在服务器上，`/etc/exports` 文件通常列出系统导出的目录层次结构。每行指定一个目录层次结构以及允许挂载的客户端系统，包括每个客户端的选项（只读、读写等）。`exportfs -r` 命令允许 NFS 重新读取此文件。

从客户端来看，`mount` 命令挂载 NFS 层次。或者你可以在 `/etc/fstab` 中放置条目，让系统在启动时自动挂载。

自动挂载的目录层次结构有助于一致地管理包含大量服务器和文件系统的组，并可以消除服务器-服务器依赖。自动挂载守护进程需要在需要时自动挂载 `autofs` 目录层次结构，并在不再需要时卸载。

# 练习

- 1. 使用 NFS 的三个理由是什么？
- 2. 在本地系统上挂载位于服务器 `plum` 的 `/home` 目录层次结构，你应该执行什么命令？假设挂载点在本地显示为 `/plum.home`。如果该目录位于 `192.168.1.1` 的文件服务器，你应该如何挂载 `/home`？
- 3. 如何列出名为 `plum` 的远程系统上提供的挂载点？
- 4. 哪个命令列出当前挂载的 NFS 目录层次结构？
- 5. `/etc/fstab` 文件的作用是什么？
- 6. 从服务器开始，如何允许 `example.com` 中的任何系统只读访问 `/opt`？

# 高级练习

- 7. 什么时候禁用属性缓存是一个好主意？
- 8. 描述 `/etc/exports` 中 `root_squash` 和 `all_squash` 选项之间的区别。
- 9. 为什么 `/etc/exports` 中的 `secure` 选项实际上没有提供任何安全性？
- 10. 无磁盘工作站使用 NFS 作为交换空间。这种方法有什么好处？缺点是什么？
- 11. NFS 将客户端用户映射到服务器用户。解释为什么这种映射存在安全风险。
- 12. `mount nosuid` 选项的作用是什么？为什么你想使用这个选项？

# 24

# SAMBA：LINUX 与 WINDOWS 文件和打印机共享

## 本章内容

- 关于 Samba ........................... 825
- 快速上手：使用 `shares-admin` 配置 Samba 服务器 ................... 826
- `smb.conf`：手动配置 Samba 服务器 ................... 832
- 从 Windows 访问 Linux 共享 ................................ 838
- 从 Linux 访问 Windows 共享 ................................. 839
- 故障排除 ....................................... 841

Samba 是一个程序包，它允许类 Unix 操作系统（包括 Linux、Solaris、FreeBSD 和 Mac OS X）能够与其他操作系统（如 OS/2 和 Windows）协同工作，既作为服务器也作为客户端。

作为服务器，Samba 与 Windows 系统共享 Linux 文件和打印机。作为客户端，Samba 让 Linux 用户能够访问 Windows 系统上的文件。其跨操作系统共享文件的能力使 Samba 成为异构计算环境中的理想工具。

有关使用 Samba 进行打印的信息，请参阅第 630 页和 632 页。

# 引言

本章首先列出 Samba 工具列表，随后介绍一些基础信息。“快速上手”部分讨论了如何使用 Shared Folders 设置 Samba 服务器。随后的章节介绍了如何使用基于 Web 的高级配置工具 `swat` 来设置 Samba 服务器。最后一节讨论了如何通过文本编辑器手动编辑控制 Samba 的文件来设置服务器。本章接下来的两个章节“从 Windows 访问 Linux 共享”（第 838 页）和“从 Linux 访问 Windows 共享”（第 839 页）解释了如何处理 Linux 和 Windows 的文件及打印机。最后一节“故障排除”（第 841 页）提供了 Samba 运行不正常时的处理建议。

表 24-1 列出了组成 Samba 程序包的一些工具和守护进程。

# 表 24-1 Samba 工具和守护进程

| 工具或守护进程 | 功能 |
| :--- | :--- |
| `net` | 它的语法与 DOS 的 `net` 命令相同，随着时间的推移，最终将取代 `smbpasswd` 等 Samba 工具。 |
| `nmbd` | NetBIOS（第 1049 页）名称服务器程序，默认作为守护进程运行。为 Samba 客户端提供基于 IP 的 NetBIOS 命名服务。还提供浏览支持（类似于 Windows 网络邻居或“我的网络”视图）。 |
| `nmblookup` | 查询 NetBIOS（第 1049 页）名称；见第 842 页。 |
| `pdbedit` | 维护 Samba 用户数据库。 |
| `smbclient` | 以 Windows 机器显示 Samba 服务器上的共享；使用类似 `ftp` 的命令（第 840 页）。 |
| `smbd` | Samba 程序，默认作为守护进程运行。为 Samba 客户端提供文件和打印服务。 |
| `smbpasswd` | 作为 Samba 和 Windows NT 服务器更改 Windows NT 密码哈希（第 828 页）。 |
| `smbstatus` | 显示当前 `smbd` 连接的信息。 |
| `smbtar` | 从 Samba 服务器备份和恢复数据；类似于 `tar`。 |
| `smtree` | 显示可用共享的层级结构图（第 839 页）。 |
| `swat` | Samba Web 管理工具。一个基于浏览器的 `smb.conf` 文件编辑器（第 828 页）。 |
| `testparm` | 检查 `smb.conf` 文件的语法（第 842 页）。 |

# 关于 SAMBA

本节涵盖了运行 Samba 所需安装的软件包、Samba 的信息源以及 Samba 下的用户和密码。

# 前提条件

安装以下软件包：

- `samba`
- `smbclient`
- `smbfs`（挂载 Windows 共享所需的唯一包）
- `swat`（可选，但很有用）
- `openbsd-inetd`（运行 `swat` 需要；作为 `swat` 的依赖项安装）
- `samba-doc`（可选文档；随 `swat` 安装）
- `samba-doc-pdf`（可选；PDF 格式的文档）

`samba` 初始化脚本：当你安装 `samba` 软件包时，`dpkg` 的后处理脚本会配置 Samba 作为普通守护进程运行（不通过 init 启动），将所有 Linux 用户复制到 Samba 用户列表中，设置 Samba 使用加密密码，并启动 `smbd` 和 `nmbd` 守护进程。在配置 `samba` 后，调用 `samba` 初始化脚本来重启 `smbd` 和 `nmbd`：

```
$ sudo /etc/init.d/samba restart
```

在活动运行的服务器上更改 `samba` 配置后，使用 `reload` 代替 `restart` 来重新加载 `samba` 配置文件，而不会干扰连接到服务器的客户端。

# 更多信息

- 本地 Samba/swat 主页有本地 Samba 文档（第 828 页）
- `/usr/share/doc/samba-*`
- Web Samba: `www.samba.org`（邮件列表、文档等）
- CIFS: `www.samba.org/cifs`
- HOWTO: 官方 Samba HOWTO `hr.uregon.edu/davidrl/samba.html`
- Samba 文档集：将浏览器指向 `/usr/share/doc/samba-doc/html/index.html`；如果你安装了 `samba-doc-pdf` 包，请查看 `/usr/share/doc/samba-doc-pdf`。

# 注意事项

防火墙：Samba 通常使用 UDP 端口 137 和 138 以及 TCP 端口 139 和 445。如果 Samba 服务器上运行着防火墙，你需要开放这些端口。使用 `firestarter`（第 886 页），通过设置允许 Samba 服务的策略来开放这些端口。

在 Samba 中，一个导出的目录层级结构被称为“共享”（share）。

# SAMBA 用户、映射和密码

（注：由于原文存在大量 OCR 生成的重复内容，此处已根据核心逻辑进行去重与翻译）

## 828 第 24 章 SAMBA：LINUX 与 WINDOWS 文件和打印机共享

Windows 机器上的名称。大多数情况下，你不需要将系统设置为 WINS 服务器。如果你愿意，可以添加更多共享。完成添加共享后，点击“关闭”退出共享文件夹窗口。

使用 root 权限运行 `smbpasswd`，可以使用 `smbpasswd` 来更改 Linux 用户的 Samba 密码。

```
$ sudo smbpasswd sam
New SMB password:
Retype new SMB password:
```

此示例假设在安装 Samba 之前 Linux 系统上已经有了用户 `sam`。当你安装 Samba 时，它会将所有 Linux 用户复制到 Samba 用户列表中。如果你在安装 Samba 后添加了用户，需要使用 `-a` 选项指示 `smbpasswd` 将该用户添加到 Samba 用户列表中。该命令将新用户 `max` 添加到 Samba 用户列表中，并为 `max` 分配一个 Samba 密码：

```
$ sudo smbpasswd -a max
New SMB password:
Retype new SMB password:
Added user max.
```

一旦用户有了 Samba 密码，他就可以在不带任何参数的情况下使用 `smbpasswd` 来更改密码。

如果你在 Linux 和 Windows 系统上有不同的用户名，你必须将 Windows 用户名映射到 Linux 用户名（参见第 835 页的用户名映射）。确保所有使用 Samba 登录的 Linux 用户都有 Samba 密码。

你现在应该能够从 Windows 机器访问新共享（第 838 页）。不需要重启 Samba 服务器。

# swat: 配置 SAMBA 服务器

## 为 `smb.conf` 创建备份

> 默认安装时，`/etc/samba/smb.conf` 文件包含大量的注释（第 832 页）。`swat` 实用程序会覆盖此文件并移除注释。在第一次运行此实用程序之前，请为 `smb.conf` 创建备份以备安全。

`swat` 实用程序（Samba Web 管理工具，软件包）是一个用于 `smb.conf` 文件的基于浏览器的图形化编辑器。对于每个配置参数，它都提供了帮助列表、默认值和一个用于更改值的文本框。`swat` 实用程序是一个设计良好的工具，它保留了你编辑的 `smb.conf` 文件中的行：你可以使用并从 `swat` 中学习，这样如果你想使用文本编辑器修改 `smb.conf`，过渡将是非常直接的。

该实用程序通过 `inetd`（`openbsd-inetd` 软件包）运行。当你安装 `swat` 软件包时，它会将 `openbsd-inetd` 作为依赖安装并在 `/etc/inetd.conf` 中放置以下行：

```
swat stream tcp nowait.400 root /usr/sbin/tcpd /usr/bin/swat
```

此行在 `inetd` 运行时启用 `swat`。如有必要，请执行以下命令重启 `inetd` 以使其读取其配置：

```
$ sudo /etc/init.d/openbsd-inetd restart
```

![](img/556454b01d95450a92edff64b47580d6_875_0.png)

**图 24-3 本地 swat 主页**

欢迎使用 SWAT！

请选择上方按钮中的一个配置操作

# Samba 文档

- 守护进程
  - `smbd`: SMBD 守护进程
  - `nmbd`: NetBIOS 名字服务器
  - `winbind`: winbind 守护进程
- 配置文件
  - `smb.conf`: Samba 主配置文件
  - `lmhosts`: NetBIOS hosts 文件
  - `smbpasswd`: Samba 密码文件
- 管理工具
