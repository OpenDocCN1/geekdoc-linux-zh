
# chkconfig autofofs on

信不信由，这就是你需要完成的全部工作了。只要你与想要共享目录的 NFS 服务器有网络连接，你就可以尝试访问共享的 NFS 目录。例如，如果你知道名为 `shuttle` 的计算机正在共享 `/usr/local/share` 目录，请执行以下操作：

- 1. 输入以下内容：

```bash
$ cd /net/shuttle
```

如果 `shuttle` 计算机有任何你可用的共享目录，你将能够成功切换到该目录。另一个需要注意的是，你可以使用 IP 地址代替代主机名（例如 `cd /net/10.0.0.1`）。

- 2. 输入以下内容：

```bash
$ ls
```

你应该能看到 `usr` 目录是共享目录路径的一部分。如果来自其他顶层目录的共享目录，你也应该能看到它们（例如 `/var` 或 `/home`）。当然，这些目录的任何一个都取决于服务器上安全性的设置。

- 3. 接下来，你可以尝试直接进入共享目录。例如：

```bash
$ cd /net/shuttle:usr/local/share
$ ls
info man music television
```

此时，`ls` 命令将显示名为 `shuttle` 的计算机上 `/usr/local/share` 目录的内容。你对这些内容可以做什么，取决于服务器是如何配置这些内容进行共享的。

## 卸载 NFS 文件系统

在 NFS 文件系统挂载后，卸载它非常简单。你使用 `unmount` 命令，并配合本地挂载点或远程文件系统名称。例如，这里有两种方法可以从本地目录 `/media/maple` 卸载 `maple:/home/chris/files`：

```bash
# unmount maple:/home/chris/files
# unmount /media/maple
```

这两种形式均可。如果 `maple:/home/chris/files` 是自动挂载的（来自 `/etc/fstab` 中的列表），则在下次启动 Fedora 或 RHEL 时将重新挂载。如果是临时挂载（或在 `/etc/fstab` 中为 `noauto`），则在启动时不会重新挂载。

> 提示：该命令不是 `unmount`，而是 `umount`。这很容易出错。

当你尝试卸载文件系统时收到“device busy”的消息，意味着卸载失败，因为该文件系统正在被访问。最可能可能是 NFS 文件系统中的某个目录是你当前 shell 的工作目录（或系统中其他人的 shell ）。另一种可能性是某个命令打开了 NFS 文件系统中的一个文件（例如文本编辑器）。检查你的终端窗口和其他窗口，如果你在目录中，请 `cd` 出来，或者直接关闭终端窗口。

如果 NFS 文件系统无法工作，你可以强制卸载它（`umount -f /media/maple`）或稍后清理（`umount -l /media/maple`）。`-l` 通常是更好的选择，因为强制卸载可能会破坏正在进行的文件修改。

## 使用 NFS 的其他酷玩操作

你可以共享目录，以便使用户可以在网络上的几台 Linux 计算机上保持工作一致性。共享目录的一些示例包括：

- `/var/spool/mail`：通过从你的邮件服务器共享此目录，并将其挂载到网络上其他计算机的相同目录上，用户可以从任何其他计算机访问他们的邮件。这节省了用户无需将消息下载到当前计算机或无需登录服务器获取邮件的精力。每个用户只有一个邮箱箱，无论从何处访问。
- `/home`：这与共享邮件的概念类似，不同之处在于所有用户都可以从任何 NFS 客户端访问他们的家目录。同样，你会在每台客户端计算机上将 `/home` 挂载到相同的挂载点。当用户登录时，该用户就可以访问位于 `/home/user` 目录包含的所有启动文件和数据文件。

提示：如果你的用户依赖 `/home` 目录，你应该确保导出该目录的 NFS 服务器足够可靠。如果 `/home` 不可用，用户可能没有无法正确登录的启动文件，或者没有完成工作所需的任何数据文件。一种解决方法是，当 NFS 目录未挂载时，在用户的家目录中提供一组最小的启动文件（`.bashrc`、`.xdefs` 等）。这样做允许用户在这些时间能够正常登录。

- 你不必非使用这个名称，项目用户之间的一种常见做法是共享一个包含项目人员需要共享的文件的目录。每个人都可以在原始文件上工作，并在一处保留最新版本的副本。（当然，管理项目的更好方法是使用 CVS 或其他版本控制软件，但这是一项简单的工作。）
- `/var/log`：你可以共享日志目录，以便多个管理员可以从中心位置监控日志。这对于跨服务器集群的故障排除非常有用。
- `/tmp`：共享 `/tmp` 目录允许用户共享临时文件，尽管需要注意安全和权限问题。

## 设置 Samba 文件服务器

Samba 是一个适用于 Fedora、RHEL 和其他 Linux 系统的软件包。它允许与使用服务器消息块 (SMB) 或通用互联网文件系统 (CIFS) 协议的计算机共享文件和打印机。SMB 是一种基于 SMB 的跨平台协议。Samba 包含了 SMB 和 CIFS 的实现。

虽然你不能指望 Windows 上安装了 NFS（除非你自己安装），但 SMB 总是可用的（只需设置）。如果尚未安装 Samba，请参考本章的“获取与安装”部分。

在 Fedora 或 RHEL 上，Samba 软件包包含各种守护进程、管理工具、用户工具和配置文件。要进行 Samba 配置，可以从 Samba 配置开始。该窗口提供了配置服务器和设置共享目录的图形界面。

### Samba 的管理工具

由于 SMB 被认为是 Windows 系统技术，描述 Samba 的某些术语听起来比 Linux 更 Windows。例如，共享目录或文件系统通常被称为“share”。

尽管 Samba 使用 NetBIOS 服务与 SMB 客户端共享资源，但底层网络必须配置为 TCP/IP。其他 SMB 主可以使用 TCP/IP、NetBEUI 和 IP/SPX 传输数据，但 Linux Samba 仅支持 TCP/IP。消息在 TCP/IP 之间传输并由 NetBIOS 处理。

### 守护进程

守护进程由 `smbd`（SMB 守护进程）和 `nmbd`（NetBIOS 服务器）组成。`smbd` 守护使得你添加到 Linux 系统的文件共享和打印服务对 Windows 客户端可用。此软件包支持的客户端：

- Windows 9x
- Windows 2000
- Windows Server 2003
- Windows NT
- Windows ME
- Windows XP
- Windows Vista
- Windows for Workgroups
- MS Client 3.0 for DOS
- OS/2
- Dave for Macintosh
- Mac OS X
- Samba for Linux

### 获取并安装 Samba

要查看 Fedora 或 RHEL 系统是否安装了 Samba，输入以下命令：

```bash
# rpm -qa | grep samba
samba-*
system-config-samba
samba-swat-*
samba-common-*
samba-client-*
```

# 774 第四部分：Fedora RHEL 网络与服务器设置

你应该看到五个软件包中的每一个名称，后面跟着版本号（我用星号表示版本号）。虽然在 Fedora 和 RHEL 中没有通过安装组安装这些包，但组成 Samba 的软件包都包含在随书提供的 DVD 中。要安装 Samba，请插入 DVD。然后运行以下命令（注意，设备名称可能不是 `cdrecorder`，且如果自动挂载，则你可以跳过第一步）：

```bash
# mount /media/cdrecorder
# cd /media/cdrecorder/Fedora/RPMS
# rpm -Uvh samba*
# cd; unmount /media/cdrecorder
```
