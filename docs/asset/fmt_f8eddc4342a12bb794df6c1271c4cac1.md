
在第一个示例中，来自 `maple` 计算机的 `/tmp` 目录（`maple:/tmp`）挂载在本地目录 `/mnt/maple` 上。文件系统类型为 `nfs`，读写缓冲区设置为 `8192` 以加速关联连接的数据传输。在第二个示例中，来自 `maple` 计算机的 `/tmp` 目录（`maple:/tmp`）挂载在本地目录 `/mnt/maple` 上。文件系统类型为 `nfs`，读写缓冲区设置为 `8192` 以加速关联连接的数据传输。

两种形式均可。如果 `/maple` 是自动挂载的（通过 `/etc/fstab` 中的列表），则该目录将在下次启动 Red Hat Linux 时重新挂载。如果它是临时挂载（或在 `/etc/fstab` 中设置为 `noauto`），则它不会在启动时重新挂载。

当你尝试卸载文件系统时如果收到“device is busy”（设备正忙）的消息，意味着挂载失败了，因为 NFS 文件系统中的某个目录是你当前 `shell` 的工作目录（或者是你或其他用户的 `shell` 工作目录）。另一种可能性是某个命令打开了 NFS 文件系统中的文件（例如文本编辑器）。检查你的终端窗口和其他 `shell`，如果你处于该目录中，请使用 `cd` 退出该目录，或者直接关闭终端窗口。

## 使用 NFS 的其他酷操作

你可以共享目录，以便用户可以在网络上的任意几台不同的 Linux 计算机上进行工作。以下是一些实用的目录示例：

- `var/spool/mail` — 通过从你的邮件服务器共享此目录，并将其挂载到网络上其他计算机的相同目录上，用户可以从所有其他计算机访问他们的邮件。这让用户无需将消息下载到当前计算机，也无需为了获取邮件而登录服务器。无论从何处访问，每个用户只有一个信箱。

- `home` — 这与共享邮件的概念类似，不同之处是所有用户都可以从任何 NFS 客户端访问他们的主目录。同样，你会将 `/home` 挂载到每台客户端计算机的相同挂载点。当用户登录时，他们就可以访问位于 `/home/user` 目录中包含的所有启动文件和数据文件。

如果你的用户依赖共享的 `/home` 目录，你应该确保 NFS 服务器导出的目录是相当可靠的。如果 `/home` 不可用，当 NFS 目录未挂载时，用户可能没有正确登录所需的启动文件，或者没有完成工作所需的数据文件（用户主目录下的 `bashrc`、`.defaults` 等）。这样做可以允许用户正常登录。

- `project` — 虽然你不一定非要使用这个名称，但项目用户之间的一种常见做法是共享一个包含项目人员需要共享的文件的目录结构。这样，每个人都可以在原始文件上工作，并在一处保留最新版本的副本。

## 在 Red Hat Linux 中设置 Samba 文件服务器

`/var/log` — 管理员可以通过在管理员计算机上挂载 `/var/log` 文件来跟踪来自几台不同计算机的日志文件。（为了实现此功能，每个服务器可能需要导出目录，以便 `root` 在计算机之间进行映射。）如果某计算机出现问题，管理员可以轻松地查看共享的日志文件。

如果你主要与 Red Hat Linux 和其他 UNIX 系统工作，NFS 可能是你共享文件系统的最佳选择。如果你的网络主要连接 MS Windows 计算机，你可能想要考虑使用 Samba 进行文件共享。

Samba 是 Red Hat Linux 自带的一个软件包，允许你在网络上与使用会话消息块（SMB）协议的计算机共享文件和打印机。SMB 是随 Windows 9x/2000 操作系统分提供的用于共享文件和打印机的协议。虽然你不能总是认为 Windows 9x/2000 客户端上安装了 NFS（除非你自己手动安装），但 SMB 总是可用的（只需进行少量设置）。

在 Red Hat Linux 侧，Samba 软件包包含各种守护进程、管理工具、用户工具和配置文件。你需要在 Samba 上进行的工作主要集中在 `/etc/samba/smb.conf` 文件上。你可以手动编辑 `/etc/samba/smb.conf`，也可以使用 SWAT 程序（在浏览器窗口中运行）来设置该文件。

守护进程由 `smbd`（SMB 守护进程）和 `nmbd`（NetBIOS 名称服务器）组成。`smbd` 使得你添加到 Red Hat Linux 计算机上的文件共享和打印服务在 Windows 9x/2000 客户端计算机上可用。支持的客户端包包括：

- Windows 9x
- Windows 2000
- Windows NT
- Windows for Workgroups
- MS Client Client 3.0 for DOS
- OS/2
- Dave for Macintosh Computers
- Samba for Linux

## 第 18 章：设置文件服务器

对于 Samba 的管理工具，有几种 `shell` 命令你可以可以使用。你可以使用 `testparm` 和 `teststatus` 命令检查你的配置文件。`smbstatus` 命令将告诉你是哪些计算机当前连接到你的共享资源。使用 `nmlookup` 命令，你可以查询 NetBIOS 名称（用于识别主机的名称）。

尽管 Samba 使用 NetBIOS 服务与客户端共享资源，但底层网络必须配置为 TCP/IP。虽然其他主机可以使用 TCP/IP 和 IPX/SPX 传输数据，但 Linux 版 Samba 只支持 TCP/IP。在带有 TCP/IP 的主机之间传输的消息将由 NetBIOS 处理。

### 获取并安装 Samba

虽然 Red Hat Linux 没有在所有组中安装 Samba，但在 RedHat CD 上提供了 Samba。要从 CD 安装它，请挂载 CD 并运行：

```bash
# mount /mnt/cdrom
# cd /mnt/cdrom/RedHat
# rpm -ivh samba*
```

如果你愿意，可以从 `http://www.samba.org` 获取最新版本的 Samba。比 RedHat CD 上的更新的 `rpm` 可以从 Samba 网站的下载获取。Samba 自带了许多文档。在你开始配置 Samba 之前，请阅读 `README` 文件。在 Red Hat Linux 中，`/etc/fstab` `README` 描述了如何使用 SWAT 进行配置，请遵循以下步骤：

1. 在 `/etc/services` 中确保以下行存在：`swat 139`。
2. 在 `disable.conf` 中，你需要更改 `disable` 行：`disable=no`。
3. 为了让更改生效，重启 `/etc/samba/smb.conf`。

为了让 Samba 能够正常工作，你需要配置 `/etc/samba/smb.conf`。这样做可以允许用户正常登录。

你需要在 Samba 上进行的工作主要集中在 `/etc/samba/smb.conf` 文件上。你可以手动编辑 `/etc/samba/smb.conf`，也可以使用 SWAT 程序（在浏览器窗口中运行）来设置该文件。

`swat 139`。

守护进程由 `smbd`（SMB 守护进程）和 `nmbd`（NetBIOS 名称服务器）组成。`smbd` 使得你添加到 Red Hat Linux 计算机上的文件共享和打印服务在 Windows 9x/2000 客户端计算机上可用。支持的客户端包包括：

- Windows 9x
- Windows 2000
- Windows NT
- Windows for Workgroups
- MS Client Client 3.0 for DOS
- OS/2
- Dave for Macintosh Computers
- Samba for Linux

### 创建 Samba 配置

使用 SWAT 创建你的配置（在 `/etc/samba/smb.conf`）。本部分的后续描述了如何使用 SWAT 创建配置项：

```
http://localhost:139/
```
