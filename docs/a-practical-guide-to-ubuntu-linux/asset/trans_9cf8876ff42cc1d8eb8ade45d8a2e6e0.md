

# 794 第 22 章 NFS：共享文件系统

第二列是文件名称，称为映射文件（map files），用于存储补充信息。第三列包含映射条目的挂载选项。在之前的示例中，第一行将超时时间（即目录在不被使用时保持挂载的时间长度）设置为 60 秒；默认超时时间为 300 秒。你可以在 `/etc/default/autofs` 中更改 autofofs 的默认值。

虽然映射文件可以命名任何名称，但其中引入了 `auto.misc`。以下是 `auto.master` 中指定的两个映射文件：

```
$ /etc/auto.misc
music      -fstype=ext4             :/dev/sdb7
```

```
$ /etc/auto.plum
pl6        -fstype=nfs               plum:/pl16
```

映射文件的第一列保存相对 autofs 自动挂载点（上述文件中的 `music` 和 `pl6`）。将此挂载点附加到 `auto.master` 第一列中对应的 autofs 挂载点，即可创建绝对挂载点。在本示例中，`music`（来自 `auto.misc`）附加到 `/frec1`（来自 `auto.master`），生成 `/frec1/music`；`pl6` 附加到 `/plum/pl6`。第二列包含选项，第三列显示要挂载的目录层级结构（`/dev/sdb7`）。你可以通过此判断它是本地的，因为它的文件系统类型被指定为 `ext4`，且在冒号之前没有出现任何系统名称。第二个示例显示了远程系统上的文件系统。它的文件系统类型为 `nfs`，并指定了远程系统名称、冒号以及挂载在远程系统下的文件系统名称。

在新设置生效之前，你必须使用 `automofs init` 脚本（第 793 页）重新加载自动挂载守护。该脚本会在启动、重启或重新加载 autofs 时创建持有挂载点的目录（示例中的 `/frec1` 和 `/plum`），并在停止时移除这些目录。

在接下来的示例中，第一条命令显示 `/frec1` 和 `/plum` 目录不存在。下一条以 root 权限运行的命令执行 `autofs init` 脚本以重新加载 autofofs。现在目录已存在但不包含任何文件。当用户列出 `/plum/plum` 的内容时，autofofs 会挂载 `pl6` 结果如下：

```
$ ls /frec1 /plum
ls: /frec: No such file or directory
ls: /plum: No such file or directory
```

```
$ sudo service autofs reload
Reloading automounter: checking for changes...
Reloading automounter map for: /frec1
Reloading automounter map for: /plum
```

```
$ ls /frec1 /plum
frec:
plum:
```

```
$ ls /plum/plum/pl16
lost+found memo
```

# 本章总结

NFS 允许服务器与异构网络上的客户端系统共享选定的本地目录层级结构，从而减少存储需求和管理开销。NFS 定义了客户端/服务器关系，其中服务器提供客户端可以挂载的目录层级结构。

在服务器上，`/etc/exports` 文件列出了系统所拥有的目录层级结构。`exports` 中的每一行都指定了一个目录层级结构和允许挂载它的客户端系统，包括每个客户端的选项（只读、读写等）。`exports -r` 命令强制 NFS 读取此文件。

从客户端来看，`mount` 命令用于挂载已导出的 NFS 目录层级结构。或者，你可以在 `/etc/fstab` 中放入一个条目，以便系统在启动时自动挂载该目录层级。

自动挂载的目录层级有助于以一致的方式管理包含许多服务器和文件系统的大型系统，并有助于处理服务器之间的依赖。`autount` 守护会在需要时自动挂载 autofs 目录层级结构，并在不需要时卸载它们。

# 练习

- 1. 使用 NFS 的三个原因是什么？
2. 你会什么命令在本地系统挂载位于名为 `plum` 的文件服务器上的 `/home` 目录层级？假设挂载的目录层级在本地系统上显示为 `/plum.home`。如果该目录层级位于位于 192.168.1.1 的文件服务器上，你会如何挂载同一个目录层级结构？你会如何卸载 `/home`？
3. 你如何列出本地名为 `grape` 的系统可以挂载到名为 `plum` 的远程系统上的挂载点？
4. 哪条命令列出当前挂载的 NFS 目录层级结构？
5. `/etc/fstab` 文件的作用是什么？
6. 从服务器允许 example.com 中的任何系统对 `/opt` 进行只读访问？
- 7. 什么时候禁用属性缓存是一个好主意？

# 高级练习

- 8. 描述 `/etc/exports` 中 `root_squash` 和 `all_squash` 选项之间的区别。
- 9. 为什么 `/etc/exports` 中的 `secure` 选项并没有真正提供安全性？
- 10. 一无盘工作站使用 NFS 作为交换空间。为什么这种方法很有用？缺点是什么？
- 11. NFS 将客户端的用户映射到服务器的用户。解释为什么这种映射存在安全风险。
- 12. `mount nosuid` 选项的作用是什么？你为什么想使用这个选项？

# 23

# SAMBA：LINUX 与 WINDOWS 文件和打印机共享

# 本章内容

- Samba 简介 ........................... 798
- 快速上手：使用 system-config-samba 配置 Samba 服务器 ...... 800
- ssmb.conf：手动配置 Samba 服务器 ................ 807
- 从 Windows 使用 Linux 共享 ....................... 814
- 从 Linux 使用 Windows 共享 .......................... 815
- 故障排除 ................................................ 817

Samba 是一套程序，使类 Unix 操作系统（包括 Linux、Solaris、FreeBSD 和 Mac OS X）能够作为服务器和客户端与其他操作系统（如 OS/2 和 Windows）协同工作。

作为服务器，Samba 共享 Linux 文件和 Windows 系统资源。作为客户端，Samba 让 Linux 用户访问 Windows 系统上的文件。它跨操作系统共享文件的能力使得 Samba 成为异构计算环境中的理想工具。

有关使用 Samba 进行打印的信息，请参考第 566 页和 568 页。

# Samba 简介

本章首先提供了 Samba 工具列表，然后是一些基本信息。“快速上手”部分讨论了如何使用“共享文件夹”（Shared Folders）窗口设置简单的 Samba 服务器。接下来的部分涵盖了如何使用 Web 配置工具 `swat` 来设置 Samba 服务器。最后一部分讨论了如何通过文本编辑器编辑控制文件来设置 Samba 服务器。本章的后两个部分“从 Windows 使用 Linux 共享”（第 814 页）和“从 Linux 使用 Windows 共享”（第 815 页）解释了如何处理 Linux 和 Windows 文件及打印机。最后的“故障排除”（第 817 页）提供了 Samba 无法工作时的建议。

表 23-1 列出了组成 Samba 套件的一些工具和守护。完整列表请参阅 samba 手册页。

| 工具或守护 | 功能 |
|---|---|
| net | 该工具的语法与 DOS 的 net 命令相同，并将最终取代 smbpasswd 等工具。 |
| nmbd | NetBIOS（第 1161 页）名称服务器，默认作为守护运行。为 Samba 客户端提供基于 IP 的 NetBIOS 命名服务。还提供浏览支持（如 Windows 网络或“我的网络位置”）。 |
| nmblookup | 查询 NetBIOS（第 1161 页）名称；见第 818 页。 |
| pddebit | 维护 Samba 用户数据库。 |
| smbclient | 显示 Samba 服务器（如 Windows ）上的共享；使用类似 FTP 的命令（第 815 页）。 |
| smbd | Samba 程序，默认作为守护运行。为 Samba 客户端提供文件和打印服务。 |
| smbpasswd | 修改 Samba 和 Windows NT 服务器上的  哈希（第 803 页）。 |
| smbtatus | 显示当前 Samba 连接的信息。 |
| smbtar | 从 Samba 服务器备份和恢复数据；类似于 tar。 |
| smbtree | 显示可用共享的层级图（第 815 页）。 |
| swat | Samba 网页管理工具。smb.conf 文件的浏览器端编辑器（第 804 页）。 |
| testparm | 检查 smb.conf 文件的语法（第 817 页）。 |

