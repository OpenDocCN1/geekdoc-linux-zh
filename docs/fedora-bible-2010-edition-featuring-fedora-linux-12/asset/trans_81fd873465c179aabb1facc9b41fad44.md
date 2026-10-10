

## 配置共享的 CUPS 打印机

在将本地打印机添加到您的 Linux 计算机后，使其可供网络上的其他计算机使用非常简单。如果在共享打印机的计算机之间存在 TCP/IP 网络连接，您可以简单地授予远程主机上的特定主机或用户访问您计算机打印服务的权限。本章前面讨论了设置本地打印机的步骤。

要将本地打印机作为打印服务器共享给网络上的其他计算机，请执行以下操作：

- 1. 从桌面面板中选择 **System → Administration → Printing**。将出现 **Printer Configuration** 窗口。
- 2. 右键单击您要共享的打印机图标。（如果尚未配置打印机，请参考本章前面的“设置打印机”部分。）
- 3. 选中菜单中的 **Shared** 复选框，以便在该框中出现勾选标记。
- 4. 如果只希望选定的用户访问您的打印机，请从菜单中选择 **Properties**，然后单击 **Access Control** 项。选择 **Deny printing for everyone except these users**，输入您允许使用打印机的每个用户，并单击 **Add** 以添加每个用户。同样，您可以选择 **Allow printing for everyone except these users**，并添加要从允许打印的用户中排除的选定用户。在 **Printer Properties** 窗口上单击 **Cancel** 或 **OK**，返回到 **Printer configuration** 窗口。
- 5. 在 **Printer configuration** 窗口顶部的 **Server** 菜单中从 **Server** 菜单中选择 **Settings**。（这不是 **Printer Properties** 窗口中的 **Settings** 选项。相反，请查看 **Printer configuration** 窗口中的 **Server** 菜单。）从出现的 **Basic Server Settings** 屏幕中，选中 **Publish shared printers connected to this system** 复选框。
- 6. 单击 **OK** 以使更改永久生效。

此时，您可以配置其他计算机以使用您的打印机。如果您尝试从另一台计算机打印但不起作用，以下是您可以尝试的一些事项：

- **Open your firewall** — 如果您拥有限制性防火墙，它可能不允许远程用户访问您的打印机。您必须允许访问端口 513（UDP 和 TCP）以及可能的端口 631，以允许访问您计算机上的打印功能。有关配置防火墙的信息，请参见第 13 章。
- **Enable LPD-style printing** — 某些应用程序可能需要较旧的 LPD 样式打印服务才能在您的共享打印机上打印。要在您的 CUPS 服务器上启用 LPD 样式打印，必须打开 `cups-lpd` 服务。作为 root 用户，输入 `**chkconfig cups-lpd on**`。然后重启 `xinetd` 守护进程 (`*service xinetd restart*`)。要使用此服务，您可能需要安装 `cups-lpd` 包 (`*yum install cups-lpd*`)。
- **Check names and addresses** — 确保在配置其他计算机上的打印机时正确输入了计算机的名称和打印队列。尝试使用 IP 地址而不是主机名（如果有效，则表明存在 DNS 名称解析问题）。wireshark 等工具可以让我们观察事务在哪里失败。

对共享打印机的访问更改在 `/etc/cups/cupsd.conf` 文件中完成。

### 配置共享的 Samba 打印机

您的 Linux 打印机可以配置为共享 SMB 打印机。要将打印机共享为 Samba (SMB) 打印机，您只需要按照第 17 章中所述配置基本的 Samba 服务器设置即可。您的所有打印机默认都应在本地网络上共享。下一节展示了结果设置的样子以及您可能想要如何更改它们。

### 理解用于打印的 smb.conf

当按照第 17 章中的描述配置 Samba 时，`/etc/samba/smb.conf` 文件被配置为允许共享您配置的所有打印机。以下是您在 `smb.conf` 文件的 `[global]` 和 `[printers]` 部分中可能会找到的与打印机共享相关的几行内容：

```text
[global]
    workgroup = MYGROUP
    serverstring = Samba Server Version %v
    security = share
    printcap name = /etc/printcap
    load printers = yes
    printing = cups
    encrypt passwords = yes
    smb passwd file = /etc/samba/smbpasswd
    unix password sync = Yes

[printers]
    comment = All Printers
    path = /var/spool/samba
    guest ok = yes
    browseable = no
    writable = no
    printable = yes
```

此处显示的设置是通过 Samba 服务器配置窗口 (System → Administration → Samba) 配置 Samba 的结果。您需要安装 `system-config-samba` 包才能使用 Samba 服务器配置窗口。在这种情况下，我选择使用加密密码。这些行表明已从 `/etc/printcap` 加载打印机，并且正在使用 CUPS 服务。`/etc/samba/smbpasswd` 文件存储加密的密码。由于密码同步已开启，每个用户的 Samba 密码都与该用户的本地 UNIX 密码同步。

此处显示的最后几行构成了 `\[printers\]` 部分，它决定了 Samba 中打印机共享的默认值。最后一行 (`printable = yes`) 定义了用户可以打印到所有打印机。

## 摘要

共享打印机是一种经济且高效的方式来使用组织的打印资源。集中放置的打印机可以更轻松地维护，同时仍允许每个人完成其打印任务。

您使用 Printer configuration 窗口配置打印机。各种过滤器使得能够打印到不同类型的打印机，以及连接到网络上计算机的打印机。

Fedora 中的默认打印服务是 Common UNIX Printing Service (CUPS)。除了能够设置您的计算机作为 Linux 打印服务器外，您还可以让计算机模拟 SMB (Windows) 打印服务器。在正确配置网络并安装本地打印机后，将该打印机作为 UNIX 或 SMB 打印服务器通过网络共享并不复杂。

# 第 17 章
## 设置文件服务器

### 本章内容

- 在 Linux 中设置 NFS 文件服务器
- 在 Linux 中设置 Samba 文件服务器

当一群人需要协同工作项目时，他们通常需要共享文档。同样，对于计算机网络上的一群人来说，共享常用的应用程序和完成工作所需的信息目录也可以提高效率。在网络上集中存储文件并共享它们的常见方法是设置文件服务器。

Fedora 系统包含对当前使用的所有最常见文件服务器协议的支持。网络文件系统 (NFS) 一直是 Linux 和其他 UNIX 系统的首选文件共享协议。拥有许多 Windows 计算机的网络倾向于使用 Samba 或 SMB/CIFS (Server Message Block/Common Internet File System) 协议。本章描述如何设置与在 Linux 中设置的 NFS 和 Samba 文件服务器相关的文件服务器和客户端。

> **交叉参考：** 本书中还描述了另一种类型的文件服务器：FTP (使用 vsFTPd)。要设置公共 FTP 文件服务器，请参见第 19 章。

### 设置文件服务器的目标

通过在文件服务器上集中数据和应用程序，您可以实现几个目标：

- **集中分发** — 您可以将文档或应用程序添加到单个位置，并使任何授权的计算机或用户都可以访问。这样，您就不必负责将必要的文件放置在每台计算机上。
- **透明性** — 使用 NFS 等协议，您的文件服务器的客户端（Windows、Linux 或 UNIX 系统）可以将您的文件系统连接到其本地文件系统，就好像您的文件系统位于本地一样。（换句话说，在 Linux 或 UNIX 系统上没有驱动器号。只需更改到远程系统的挂载点，您就在那里。）

### 设置 NFS 文件服务器

与 Microsoft 操作系统中传统上代表存储设备的驱动器号（A、B、C 等）不同，Linux 系统将多个硬盘、USB 驱动器、CD-ROM 和其他本地设备上的文件系统不可见地连接起来，以形成单个 Linux 文件系统。网络文件系统 (NFS) 设施允许您以相同方式扩展 Linux 文件系统，以将其他计算机上的文件系统连接到您的本地目录结构。

> **交叉参考：** 有关如何在 Linux 文件系统中挂载本地设备的描述，请参见第 9 章。使用相同的命令 (mount) 来挂载本地设备和 NFS 文件系统。

创建 NFS 文件服务器是共享组织内用户和计算机之间大量数据的一种简单方法。配置为使用 NFS 共享其文件系统的 Linux 系统的管理员必须执行以下任务来设置 NFS：

- 1. **设置网络** — 如果已经有 LAN 或其他网络连接连接了您想要使用 NFS 的计算机（使用 TCP/IP 作为网络传输），那么您已经拥有所需的网络。

- 2. **在服务器上，选择要共享的内容** — 决定要在 Linux NFS 服务器上对哪些文件系统可供其他计算机访问。您可以选择文件系统中的任何点，并使该点下方的所有文件和目录可供其他计算机访问。但是，从文件系统分区的根目录共享目录是最安全的。

- 3. **在服务器上，设置安全性** — 您可以使用几种不同的安全功能来满足您的安全级别需求。挂载级安全允许您限制可以挂载资源的计算机，并且对于允许挂载的计算机，允许您指定它是读/写挂载还是只读挂载。在用户级安全中，您将客户端系统的用户映射到 NFS 服务器上的用户。这样，用户可以依赖标准的 Linux 读/写/执行权限、文件所有权和组权限来访问和保护文件。

- 4. **在客户端上，挂载文件系统** — 每个被允许访问服务器 NFS 共享文件系统的客户端计算机都可以在客户端选择的任何位置挂载它。例如，您可能将在名为 `oak` 的计算机上的文件系统挂载在本地文件系统的 `/mnt/oak` 目录中。挂载后，您可以通过输入 `ls /mnt/oak` 来查看该目录的内容。然后，您可以使用 `/mnt/oak` 挂载点下的 `cd` 命令来查看它包含的文件和目录。

图 17-1 展示了使用 NFS 共享（导出）文件系统的 Linux 文件服务器，以及将文件系统挂载以供其本地用户使用的客户端计算机。

