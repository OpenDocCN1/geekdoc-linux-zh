

在 */etc/exports* 文件中添加条目后，请在终端窗口中键入以下命令手动导出文件系统：

```
exportfs -a
```

此命令将导出 */etc/exports* 文件中定义的所有文件系统。

现在您可以启动 NFS 服务器进程。

![](img/792720823146d68f19fd50c99ebfce4b_689_0.png)

在 Debian 中，登录为 *root* 用户，并在终端窗口中键入 */etc/init.d/nfs-kernel-server start* 来启动 NFS 服务器。在 Fedora Core 中，键入 */etc/init.d/nfs start*。在 SUSE 中，键入 */etc/init.d/nfsserver start*。如果希望 NFS 服务器在系统启动时自动启动，请在 Debian 中键入 *update-rc.d nfs-kernel-server defaults*。在 Fedora Core 中，键入 *chkconfig --level 35 nfs on*。在 SUSE 中，键入 *chkconfig --level 35 nfsserver on*。在 Xandros 中，键入 *update-rc.d nfs-user-server defaults*。

当 NFS 服务启动后，NFS 的服务器端即准备就绪。现在您可以尝试从客户端系统挂载导出的文件系统，然后根据需要访问该导出的文件系统。

![](img/792720823146d68f19fd50c99ebfce4b_689_1.png)

如果您对 */etc/exports* 文件中列出的导出文件系统进行了任何更改，请记得重启 NFS 服务。要重启服务，请在 */etc/init.d* 目录中调用脚本，并以 *restart* 作为参数（而不是启动服务时使用的 *start* 参数）。

## 挂载 NFS 文件系统

要在客户端系统上访问已导出的 NFS 文件系统，您必须将该文件系统挂载到一个挂载点上。*挂载点* 无非就是一个本地目录。例如，假设您想要访问服务器 *LBNP200* 导出的 */home* 目录，并将其挂载到客户端系统上的本地目录 */mnt/lbnp200*。为此，请按照以下步骤操作：

1. **登录为 _root_ 并使用以下命令创建目录：**

   ```sh
   mkdir /mnt/lbnp200
   ```

2. **键入以下命令，将远程系统（LBNP200）的目录挂载到本地目录 / _mnt/lbnp200_ 上：**

   ```sh
   mount lbnp200:/home /mnt/lbnp200
   ```

完成这些步骤后，您就可以从本地目录 */mnt/lbnp200* 查看和访问导出的文件。

要确认 NFS 文件系统确实已挂载，请以 **root** 身份登录客户端系统，并在终端窗口中键入 **mount**。您会看到关于 NFS 文件系统的一行信息，类似于以下内容：

```
lbnp200:/home/public0 /mnt/lbnp200 type nfs (rw,addr=192.168.0.4)
```

NFS 支持两种类型的挂载操作——硬挂载（hard）和软挂载（soft）。默认情况下是硬挂载，这意味着如果 NFS 服务器没有响应，客户端会持续尝试访问服务器，直到服务器响应为止。您可以通过在 mount 命令中添加 -o soft 选项来实现 NFS 卷的软挂载。对于软挂载，如果 NFS 服务器未能响应，客户端将返回错误。

## 使用 Samba 设置 Windows 服务器

如果您依赖 Windows 进行文件共享和打印共享，那么您可能在服务器和客户端上都使用 Windows。如果是这样，您仍然可以将 Linux PC 作为服务器，而不会失去 Windows 的文件共享和打印共享功能；您可以将 Linux 设置为 Windows 服务器。当您从本书的配套 DVD-ROM 安装 Linux 时，您也有机会安装 Samba 软件包，该软件包会执行此设置。您只需在安装期间选择 Windows File Server 软件包组即可。

在您的 Linux PC 上安装并配置 Samba 后，您的客户端 PC——即使是运行旧版 Windows for Workgroups 操作系统或较新的 Windows 95/98/NT/2000/XP 版本的计算机——都可以访问 Linux PC 上共享的磁盘和打印机。为此，它们使用服务器消息块（SMB）协议，即 Windows 文件和打印共享的底层协议。

安装了 Samba 软件包后，您可以将 Linux PC 设为 Windows 客户端，这意味着 Linux PC 可以访问由 Windows 服务器管理的磁盘和打印机。同时，您的 Linux PC 也可以作为网络中其他 Windows 系统的客户端。

Samba 软件包包含以下主要组件：

- **/etc/samba/smb.conf：** 这是 SMB 服务器使用的 Samba 配置文件。
- **/etc/samba/smbusers：** 这个 Samba 配置文件显示了与本地 Linux PC 上用户名相对应的 Samba 用户名。
- **nmbd：** 这是 NetBIOS 名称服务器，客户端使用它来查找服务器。（NetBIOS 代表 **Network Basic Input/Output System**——应用程序用于与网络传输（如 TCP/IP）通信的接口。）
- **nmblookup：** 此命令返回由 NetBIOS 名称标识的 Windows PC 的 IP 地址。
- `smbadduser`：此程序将用户添加到 SMB（Server Message Block）密码文件中。
- `smbcacls`：此程序操纵共享文件上的 Windows NT 访问控制列表（ACLs）。
- `smbclient`：这是 Windows 客户端，它在 Linux 上运行，允许 Linux 访问任何 Windows 服务器上的文件和打印机。
- `smbcontrol`：此程序向 `smbd`、`nmbd` 或 `winbind` 进程发送消息。
- `smbd`：这是 SMB 服务器，它接受来自 Windows 客户端的连接，并提供文件共享和打印共享服务。
- `smbmount`：此程序在 Linux PC 上挂载 Samba 共享目录。
- `smbpasswd`：此程序更改 SMB 用户的密码。
- `smbprint`：此脚本启用在 SMB 服务器上的打印机上打印。
- `smbstatus`：此命令列出本地主机当前的 SMB 连接。
- `smtar`：此程序直接将 SMB 共享备份到 Linux 系统上的磁带驱动器。
- `smbumount`：此程序卸载当前已挂载的 Samba 共享目录。
- `testparm`：此程序确保 Samba 配置文件是正确的。
- `winbindd`：此服务器从 Windows NT 服务器解析名称。

在以下章节中，我将描述如何配置和使用 Samba。

### 安装 Samba

在安装 Linux 时，您可能已经安装了 Samba。您可以先检查一下，如果未在系统上找到 Samba，您可以轻松安装它。

![](img/792720823146d68f19fd50c99ebfce4b_691_0.png)

在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `dpkg -l samba*` 以查看是否已安装 Samba。在 Fedora Core 和 SUSE 中，键入 `rpm -q samba` 以查看是否已安装 `samba` 软件包。

![](img/792720823146d68f19fd50c99ebfce4b_691_1.png)

在 Debian、MEPIS 和 Ubuntu 中，键入 `apt-get install samba` 来安装 Samba。在 Fedora Core 中，登录为 `root`，挂载 DVD，然后键入 `cd /media/cdrom/Fedora/RPMS`，接着键入 `rpm -ivh samba*`。在 SUSE 中，点击 YaST 控制中枢软件类别中的软件管理。然后使用 YaST 的搜索功能查找 `samba`，选择相关软件包并安装它们。至于 Xandros，安装 Xandros 时即可获得 Samba。

安装 Samba 软件后，您必须在配置 Samba 之后才能使用它。

## 配置 Samba

要设置 Windows 文件共享和打印共享服务，您可以手动编辑配置文件或使用图形用户界面（GUI）工具。当然，使用 GUI 工具比编辑配置文件容易得多。Fedora Core 和 SUSE 附带用于配置 Samba 服务器的 GUI 工具。

在 Fedora Core 中，选择“桌面 > 系统设置 > 服务器设置 > Samba”以打开 Samba 服务器配置窗口。点击“添加”并填写您希望与 Windows 系统共享的目录信息，如图 6-1 所示。点击“访问”选项卡以指定哪些用户可以访问共享目录。Samba 服务器配置工具通过在配置文件 `/etc/samba/smb.conf` 中添加条目来创建 Samba 共享。

![](img/792720823146d68f19fd50c99ebfce4b_692_0.png)

在 SUSE 中，您可以通过 YaST 控制中枢配置 Samba——选择“主菜单 > 系统 > 控制中枢 (YaST)”，点击窗口左侧的“网络服务”，然后点击窗口右侧的“Samba 服务器”。YaST 显示一个窗口（见图 6-2），您可以通过该窗口配置 Samba。首先，您选择一个工作组名称（YaST 会显示局域网上任何现有 Windows 工作组的名称）并点击“下一步”。然后，您可以选择服务器类型，启用服务器，并选择您希望共享的内容。退出 Samba 服务器配置实用程序后，YaST 会将 Samba 设置存储在 `/etc/samba` 目录中的配置文件中。

