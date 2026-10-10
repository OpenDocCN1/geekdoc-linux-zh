
（可以使用 `smbpasswd -a user` 命令在设置用户密码的同时创建 smbpasswd 文件。）对每个用户重复此步骤。稍后，每个用户可以登录 Linux 并重新运行 `passwd` 和 `smbpasswd` 命令来设置私人密码。）

> 注意：在最新版本的 Samba 中，`smb.conf` 文件中提供的选项可以使 SMB 和 Linux 密码自动同步。请参阅本章 SWAT 部分中关于 `passwd` 程序、`passwd chat` 和 `UNIX password sync` 选项的说明。

# Samba 服务

要启动 Samba SMB 和 NMB 守护进程，你可以通过以 root 用户输入以下内容运行 `/etc/init.d/smb` 启动脚本：

```
# service smb start
```

这会在当前会话中运行 Samba 服务。设置 Samba 在 Linux 系统启动时自动启动，请输入：

```
# chconfig smb on
```

这开启了 Samba 服务在运行级别 3、4 或 5 时自动启动。你现在可以检查网络上的 SMB 客户端，查看它们是否可以访问你的 Samba 服务器。

# 测试你的 Samba 权限

你可以从 shell 多个命令来操作 Samba。其中一种是 `testperm` 命令，你可以用它来检查设置的访问权限。它列出了已设置的全局参数以及任何共享目录或打印机。

# 检查共享目录状态

`smbd status` 命令可以查看当前正在使用你的 Linux 系统提供的 Samba 共享资源的用户。以下是 `smbstatus` 输出示例：

Samba version 3.0.3-4

| PID | Username | Group | Machine |
| :--- | :--- | :--- | :--- |
| | | | |

# 第18章：搭建文件服务器

# 设置 Samba 客户端

一旦你配置了 Samba 服务器，就可以尝试从客户端使用共享目录。后续章节描述了如何从另一个系统使用 Samba 服务器。

# 在 Linux 中使用共享目录

Linux 可以像查看其他介质（硬盘、NFS 共享、光ROM）一样查看你的共享目录。有几种方法从客户端连接共享目录。后续章节将介绍这些方法。

# 从 Nautilus 使用 Samba

要从 Nautilus 连接 Samba 共享，请通过点击文件（File）-> 位置（Location）使用位置框。然后在 Nautilus 文件管理器中输入 `smb:`。

会出现网络上的 SMB 工作组列表。你可以选择一个工作组、服务器，然后选择要使用的资源。这对于不需要密码的共享是有效的。

Nautilus 界面要求你提供明文密码或在位置框输入密码。例如，为了通过 Nautilus 进入我的主目录（`/home/chris`），我可以如下输入用户名、密码、服务器名称和共享名称：

```
smb://chris:aaaa密码@toys/chris
```

与其在位置框中输入这些信息，可以使用 Nautilus 的连接服务器（Connect to Server）功能。在出现的连接服务器窗口中，你可以请求特定的共享、文件夹或用户名。你也可以为连接选择特定的名称。你也可以省略密码部分（例如 `smb://chris@toys/chris`）并提示输入密码。

# 在 Linux 中挂载 Samba 目录

Linux 查看共享目录就像查看任何其他介质（硬盘、NFS 共享、CD-ROM 等）一样。使用 `mount` 命令，你可以挂载 Samba 共享文件系统，使其永久连接到你的 Linux 文件系统。

以下 `mount` 命令的示例展示了如何将我的主目录（`/home/chris`）挂载到指定的本地目录（`/mnt/toys`）上。作为 root 用户，从终端窗口输入：

```
# mkdir /mnt/toys
# mount -t cifs -o username=chris,password=a2mg //toys/chris /mnt/toys
```

Samba 共享的文件系统类型是 `cifs` (`-t cifs`)。我将用户名（`chris`）和密码（`a2mg`）作为选项传递 (`-o`)。`toys` 上的远程共享是 `//toys/chris`。此时，你可以访问

你可以像访问本地文件或目录一样，访问 `toys` 上的 `/home/chris` 内容。你将拥有的访问和更改该目录（及其子目录）内容的权限，与你直接从 `toys` 使用 `chris` 用户这些内容时是相同的。

要永久挂载 Samba 共享目录，你可以向 `/etc/fstab` 文件添加一个条目。对于上述描述的示例，你可以以 root 用户身份添加以下行：

```bash
//toys/chris /mnt/toys cifs username=chris,password=a72mg
```

你可以添加一个凭据文件并使用它来包含你的用户名和密码，而不是将这些信息暴露在命令行中。这样，在你系统上运行 `ps` 命令的人将无法看到这些信息。例如，你可以创建一个名为 `/etc/samba/creds.smbpub` 的文件，内容包含如下：

```bash
username=chris
password=a72mg
```

你可以将之前显示的挂载命令修改为：

```bash
# mount -t cifs -o credentials=/etc/samba/creds.smbpub //toys/chris
```

## 从 Windows 使用 Samba 共享目录

在使用 Windows 系统时，要查看来自 Linux Samba 服务器的可用文件和打印服务（以及网络上其他计算机的服务），请打开“我的网络位置”（Windows XP）或“网络邻居”（Windows 98 及更早的 Windows 系统）。要打开此窗口，在 Windows XP 桌面上选择“开始 -> 我的网络位置”。图 18-6 显示了网络位置窗口的示例，其中来自本地 Windows XP 系统（名为 Bluestream）和 Linux Samba 服务器（名为 Waldo）的可用共享。

# 第 18 章：设置文件服务器 781

![](img/c7605e408543e0a1829c1fd0cf2f687d_816_0.png)

图 18-6：从“我的位置”窗口查看你的 Linux Samba 服务器。

“我的网络位置”窗口显示 Windows 在你的网络上找到计算机。如果你的服务器出现在屏幕上（在我的情况下，服务器名称是 Waldo），双击它。否则，你可能需要双击“整个网络”，然后打开你的服务器所在的工作来找到你的服务器。服务器应该显示两种资源：

- 打印机和传真机 —— 一个名称和一个图标代表从服务器共享的每台打印机和传真机。要访问打印机或传真机，双击它。Windows 将让你为电脑设置打印机或传真机。之后，你可以像使用任何本地打印机或传真机一样使用它。

- 目录 —— 一个名称和一个文件夹代表来自服务器的共享目录。打开目录以查看该目录中的文件和文件夹。

双击文件夹以查看该文件夹的内容。此时，你可能会收到输入密码的请求。输入密码并点击确定。此时，你应该能够查看该文件夹及其子文件夹的内容。

> 提示：如果你经常使用该目录，你可能想为它分配一个驱动器号。右键点击文件夹图标，然后选择“映射网络驱动器”。从列表中选择一个驱动器，如果你喜欢，勾选“登录时重新连接”以便在登录时可以使用它。然后点击“确定”。

如果你正在寻找的文件服务器没有出现在你的“网络邻居”中，你可以尝试搜索它。选择“开始 -> 搜索 -> 计算机或用户 -> 计算机”。输入要搜索的计算机名称，然后选择“立即查找”。如果出现了计算机名称，双击它。应该会打开一个窗口，显示服务器的共享目录和打印机。

# 第四部分：Fedora 和 RHEL 网络与服务器设置

或者，你也可以创建一个 `lmhosts` 文件帮助你的 Windows 计算机找到 Linux Samba 服务器。将示例 `C:\windows\lmhosts.sam` 文件复制到 `C:\windows\lmhosts`。然后编辑该文件，添加网络上 SMB 服务器的主机和 IP 地址。

## 故障你的 Samba 服务器

Samba 服务器可能会很多问题。如果你的 Samba 服务器无法正常工作，本节中的描述应该帮助你确定问题。

## 基础已就绪？

在计算机能够 Samba 共享目录和打印机之前，它们必须能够在你的局域网（LAN）上通信。设置 LAN 请参考第 15 章。

在 Samba 中，你的 Samba 服务器可以使用 TCP/IP 名称作为 NetBIOS 名称（Windows 网络用于文件和打印机共享），或在 `smb.conf` 文件中设置独立的 NetBIOS 名称。然而，广播地址对于所有与你的 Samba 服务器通信的客户端是相同的至关重要的。要验证你的广播地址，输入

```bash
$ config -a
eth0 Link encap:Ethernet HWidth 00:D1:B3:75:A5:1B
inet addr:10.0.0.1 Bcast:10.0.0.255 Mask:255.255.255.0
```
