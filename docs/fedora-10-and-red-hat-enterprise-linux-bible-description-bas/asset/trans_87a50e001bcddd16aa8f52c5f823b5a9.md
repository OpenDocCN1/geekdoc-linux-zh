

# 第四部分：Fedora 和 RHEL 网络与服务器设置

| PID | 用户 | 组 | 机器 |
| --- | --- | --- | --- |
| 25770 | chris | chris | booker (10.0.0.50) |
| 25833 | chris | chris | (10.0.0.50) |

| 服务 | pid | 机器 | 连接时间 |
| --- | --- | --- | --- |
| IPCS | 25722 | booker | 2009年1月20日 12:06:20 |
| mytmp | 25770 | booker | 2009年1月20日 12:16:20 |
| mytmp | 25833 | 10.0.0.50 | 2009年1月20日 12:25:52 |
| IPCS | 25730 | booker | 2009年1月20日 12:06:20 |

| Pid | Uid 拒绝模式  | R/W 锁 共享部分 名称 时间 |
| --- | --- | --- | --- | --- | --- |
| 25833 | 501 | DENY_NONE | 0x12019f | RDWR | /home/chris/files/.b.txt_swap | 2009年1月20日 12:26:18 |

此输出显示，你的 Linux Samba 服务器——myhome 服务（/home/chris/files 目录的共享部分）当前正被名为 boxer 的计算机打开。PID 25833 是 Linux 服务器上处理该服务的 `smbd` 守护进程的进程数。当前打开的文件是 `/home/chris/files/.b_swap`，它恰好是由一个 bi 命令打开的。它具有读/写权限。

# 设置 Samba 客户端

一旦你配置好了 Samba 服务器，就可以尝试从网络上的客户端计算机使用共享目录了。接下来的章节将描述如何从另一个 Linux 系统或各种 Windows 系统使用你的 Samba 服务器。

# 从 Linux 使用 Samba 共享目录

从 Samba 客户端连接到共享目录有多种方法。以下章节将介绍这些方法。

# 从 Nautilus 使用 Samba

要从 Nautilus 连接 Samba 共享，请点击“文件 -> 打开位置”来使用位置框。然后，在 Nautilus 文件管理器的位置框中输入 **smb:**。

窗口中会出现你网络上的 SMB 工作组列表。你可以选择一个工作组，选择一个服务器，并选择要使用的资源。这对于不需要密码的共享应该是有效的。

Nautilus 界面要求你发送明文密码或在位置框中输入用户和密码。例如，为了通过 Nautilus 获取你的主目录（/home/chris），我可以按照如下格式输入用户名、密码、服务器名称和共享名称：

```
smb://chris:my72rgb@toys/chris
```

# 第 18 章：设置文件服务器 789

与其直接将这些信息输入位置框，你可以使用 Nautilus 的“连接到服务器”功能。选择出现的“文件 -> 连接到服务器”窗口，将服务器类型选择为“Windows 共享”，输入服务器名称以查看其内部的所有可用共享。可选，你可以请求特定的服务器、文件夹或用户名。你还可以选择一个特定的名称用于连接。你可以直接输入密码（例如 smb://chris@toys/chris），系统会提示输入密码。

# 在 Linux 中挂载 Samba 目录

Linux 查看共享目录的方式与其他任何方法（硬盘、NFS 共享、CD-ROM 等）相同。使用 `mount` 命令，你可以挂载 Samba 共享文件系统，将其永久连接到你的 Linux 文件系统中。

以下 `mount` 命令的示例显示了如何将来自 toys 计算机的我的主目录（/home/chris）挂载到本地目录（mnt/toys）。作为 root 用户，在终端窗口输入：

```
# mount /mnt/toys
# mount -t cifs -o username=chris,password=a72mg //toys/chris /mnt/toys
```

Samba 共享的文件系统类型是 cifs (-t)。我将用户名 (chris) 和密码 (a72mg) 作为选项 (-o)。我主目录的远程共享是 //toys/chris。本地挂载点是 /mnt/。此时，你可以像访问本地任何文件或目录一样访问 toys 上的 /home/chris 的内容。你将拥有访问和更改该内容（及其子目录）的相同权限，就像你是用户 chris 直接从 toys 使用这些内容一样。

要为了个人挂载 Samba 共享目录，你可以在 `/etc/fstab` 文件中添加条目。对于上述描述的示例，你可以（作为 root 用户）添加以下行：

```
//toys /mnt/toys cifs username=chris,password=a72mg
```

你可以创建一个凭据文件来包含用户名和密码，而不是将这些信息暴露在命令行中。这样，在你系统上运行 `ps` 命令的人无法看到这些信息。例如，你可以创建一个名为 /etc/samba/creds.smbpub 的文件，包含以下行：

```
username=chris
password=a72mg
```

然后你可以将之前的 `mount` 命令改为如下所示：

```
# mount -t cifs -o credentials=/etc/samba/creds.smbpub //toys/chris
```

# 从 Windows 使用 Samba 目录

在使用 Windows 系统时，要查看来自 Linux Samba 服务器的可用文件和打印服务（以及网络上其他计算机），请打开 Windows Vista 中的“网络和共享”窗口。底部的选项可以让你看到你和其他人共享的所有文件和文件夹。

对于其他 Windows 系统，打开“我的网络”窗口（Windows XP）或“网络邻域”（Windows 98 及其他 Windows 系统）。要打开窗口，从 Windows XP 桌面选择“开始 -> 我的网络”。图 18-6 显示了“我的网络”窗口的示例，其中包含本地 Windows XP 系统（名为 Bluestream）和 Linux 中的 Samba 服务器（名为 Waldo）的可用共享。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_837_0.png)

**图 18-6：** 从“我的网络”窗口查看你的 Samba 服务器。

“我的网络”窗口显示 Windows 在你的网络上找到的计算机。如果你的服务器出现在屏幕上（我的情况下是 Waldo），底部的选项可以看到你和其他人共享的所有文件和文件夹。

对于其他 Windows 系统，打开“我的网络”窗口（Windows XP）或“网络邻域”（Windows 98 及其他 Windows 系统）。要打开窗口，从 Windows XP 桌面选择“开始 -> 我的网络”。图 18-6 显示了“我的网络”窗口的示例，其中包含本地 Windows XP 系统（名为 Bluestream）和 Linux 中的 Samba 服务器（名为 Waldo）的可用共享。

“我的网络”窗口显示 Windows 在你的网络上找到的计算机。如果你的服务器出现在屏幕上（我的情况下是 Waldo），底部的选项可以看到你和其他人共享的所有文件和文件夹。

- **打印机和传真机：** 名称和图标应代表打印机或传真机。双击它即可访问打印机或传真机。
- **目录：** 名称和图标应代表来自服务器的共享目录。

# 第 18 章：设置文件服务器 791

双击目录查看内容。此时，你可能会收到输入密码的请求。提示：如果你计划使用该目录，可以为其分配一个驱动器号。从列表中选择一个驱动器，如果你喜欢，选择“重新连接”以便在登录时可用。然后点击确定。

或者，你可以创建一个 lmhosts 文件来帮助你的 Windows 计算机找到服务器。将备用文件 C:\windows\lmhosts.sam 复制到 C:\windows\lmhosts。编辑该文件以添加 SMB 服务器的主机名和 IP 地址。

# 排除你的 Samba 服务器的故障

Samba 服务器可能会出现很多问题。如果你的 Samba 服务器运行不正常，本节中的描述应该帮助你定位问题。

# 基础网络已就绪？

在计算机可以通过 Samba 共享目录和打印机之前，它们必须能够在你的局域网（LAN）上通信。有关设置 LAN 信息请参考第 15 章。

在 Samba 中，你的 Samba 服务器可以使用 TCP/IP 名称作为 NetBIOS 名称（Windows 网络用于文件和打印机共享），也可以在 smb.conf 文件中设置独立的 NetBIOS 名称。然而，广播地址与与你 Samba 服务器通信的所有客户端相同是非常关重要的。要查看你的广播地址，请输入以下：

```
$ ifconfig -a
eth0 Link:Ethernet HWaddr:00:D1:B3:75:A5:1B
inet addr:10.0.0.1 Bcast:10.0.0.255 Mask:255.255.255.0
```

重要的信息是广播地址（Bcast:10.0.0.255）。它由子网掩码（Mask:255.255.255.0）决定。如果 Samba 服务器和局域网客户端的广播地址不同，客户端就看不到 Samba 服务器有目录或打印机可以共享。

# Samba 服务正在运行吗？

首先，从你的 Linux 系统尝试 smclient 命令，检查一切是否运行正常且共享符合你的预期。smclient 命令是一个非常有用的工具，用于

