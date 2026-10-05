

如果你需要重新挂载已经列在 fstab 文件中的大量文件系统，可以使用 `mount` 命令的 `-a` 选项来重新挂载 fstab 中的所有项：

```
mount -a
```

如果发现某个文件系统已经挂载，则不会对该文件系统执行任何操作。相反，如果发现某项未被挂载，它将自动使用相应的参数对其进行挂载。

## 注意

当你在设置挂载来自其他服务器文件系统的服务器时，要小心交叉挂载（cross mounting）。交叉挂载是指两台服务器互相挂载对方的文件系统。如果你没有配置 `/etc/fstab` 文件通过 `bg` 选项在后台挂载这些系统，这可能是危险的，因为这两台机器在启动过程中可能会发生死锁，因为每个主机都在等待对方的响应。

例如，假设让 host1 挂载 host2 的 `/export/usr/local`，让 host2 挂载 host1 的 `/export/home/admin`。如果两台机器在断电后重启，host1 将在启动自己的 NFS 服务之前尝试挂载来自 host2 的目录。同时，host2 将在启动自己的 NFS 服务之前尝试挂载来自 host1 的目录。结果是每台机器都在等待另一台机器启动。

如果你在两个主机的 `/etc/fstab` 项中使用了 `bg` 选项，它们将在初始挂载时失败，将挂载放在后台并继续启动。最终，两台机器都会启动它们的 NFS 守护进程，并允许对方挂载各自的目录。

## 完整示例配置文件

列表 15.1 包含一个完整的 `/etc/exports` 文件。

### 列表 15.1 完整的 /etc/exports 文件

```
# /etc/exports for denon
```

# 列表 15.1 继续

# # 共享主目录：
/export/home technics(rw) pioneer(rw) vestax(rw)
  ->atus(rw) rane(rw)

# # 共享本地软件
# /export/usr/local technics(rw,no_root_squash)
  ->vestax(rw,no_root_squash)
  ->pioneer(rw,no_root_squash)
  ->atus(rw,no_root_squash)
  ->rane(rw,no_root_squash)

列表 15.2 包含一个客户端的完整的 `/etc/fstab` 文件。

### 列表 15.2 完整的 /etc/fstab 文件

# # /etc/fstab for technics
| 设备 | 挂载点 | 类型 | 选项 | Dump | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hdb2 | | ext2 | defaults | 1 | 1 |
| denon:/exports/home | /home | nfs | hard,intr,rw,nosuid | | |
| denon:/exports/projects | /usr/local/projects | nfs | hard,intr,rw,nosuid | | |
| /dev/hda7 | swap | swap | defaults | 0 | 0 |
| /dev/fd0 | /mnt/floppy | ext2 | noaute | 0 | 0 |
| /dev/cdrom | /mnt/cdrom | iso9660 | noaute,rw | 0 | 0 |
| none | /proc | | defaults | 0 | 0 |
| none | /dev/pts | devpts | | 0 | 0 |

你也可以管理文件系统。如果你想将软盘作为 msdos 文件系统挂载，这一点非常重要。以下命令将软盘挂载到 `/mnt/floppy`。

```
mount -t msdos /dev/fd0 /mnt/floppy
```

卸载只是一个简单的命令：
`unmount /mnt/floppy` （注：此处原文命令应为 unmount）

![](img/cbac72550c7126a22162e94d91a0c360_512_0.png)

## 总结

在本章中，你学习了如何：
- 启动和卸载 NFS
- 创建和维护共享
- 安装 Samba
- 配置 Samba
- 共享 Samba
- 优化 Samba
- 测试 Samba
- 使用 Samba
- 访问 Samba

## 理解 Samba

在我们开始讨论安装和配置 Samba 的正确方法之前，良好地掌握 Samba 的功能以及背后发生了什么是十分重要的。

## Samba 的功能

在实际意义上，Samba 可以让你的 Linux 机器看起来像是一个基于 Windows 的系统。不仅意味着你配置的 Samba 系统将出现在“网络邻域”中，你还可以在你的系统上创建所谓的“共享”。这将允许你进行挂载。该功能的一个流行用途是从你的 Linux 机器上导出主目录，以便在 Windows 客户端上可用。此外，Samba 还允许你创建打印机“共享”，以便 Windows 客户端可以使用连接到你 Linux 机器的打印机。

## 访问共享

Samba 共享可以通过 Windows 和 Linux 平台上的 SMB 客户端访问。Windows 通过“网络邻域”和“资源管理器”访问。Linux 通过 `smclient` 和 `mount` 命令访问。

## Samba 组件

Samba 服务器由两个守护进程组成：smbd 和 nmbd。smbd 守护进程提供文件和打印共享服务。nmbd 守护进程提供 NetBIOS 名称支持。

## NetBIOS 名称解析

在本节中，我们想要涵盖几个重要的主题。第一个是 NetBIOS 名称解析。正如我们所说的，Samba 实际上由两个守护进程 nmbd 和 smbd 组成。nmbd 提供 NetBIOS 名称解析并充当 WINS 服务器。Windows 机器可以（并且应该）配置为使用你的 Linux 机器作为 WINS 服务器，nmbd 将帮助你的 Windows 机器找到与特定名称关联的 IP 地址。这将允许你的客户端在通过名称访问 Samba 机器时，正确地“找到”它。

在 Samba 发行版中，可以在以下位置找到文件：

```
smbd and nmbd: /usr/bin
smclient, testparm, mbstatus: /usr/bin
smb.conf: /etc/
```

