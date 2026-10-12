
## 使用 Red Hat NFS 服务器配置工具

Red Hat Linux 附带了一个图形化的 NFS 服务器配置工具，可轻松配置和启动 NFS 服务器。要使用此工具配置 NFS 服务器，请按照以下步骤操作：

1. **以 root 身份登录并从 GNOME 或 KDE 桌面选择 主菜单：系统设置：服务器设置：NFS 服务器。**
   NFS 服务器配置窗口出现。
2. **在工具栏上单击 添加。**
   添加 NFS 共享 对话框出现。
3. **使用对话框添加您希望通过 NFS 共享的目录。**
   首先指定目录、谁有权访问它（主机或 IP 地址）以及访问类型（只读或读写）。图 6-1 显示了将 /home 目录以读写方式与 192.168.0.0 网络中的所有主机共享的设置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_728_0.png)

图 6-1：
从此对话框指定共享目录和基本权限。

4. **在 添加 NFS 共享 对话框中单击 常规选项 选项卡并设置您想要的选项（如图 6-2 所示）。**
   这些选项对应于表 6-1 的 常规选项 部分中列出的选项。

图 6-2：
从此对话框指定 NFS 共享的常规选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_729_0.png)

5. **在 添加 NFS 共享 对话框中单击 用户访问 选项卡并设置您想要的选项（图 6-3）。**
   这些选项对应于表 6-1 的 用户 ID 映射选项 部分中列出的选项。

6. **在 添加 NFS 共享 对话框中单击 确定。**
   NFS 配置工具将设置保存到 `/etc/exports` 文件中并启动 NFS 服务器。

7. **选择 文件→退出 以退出 NFS 配置工具。**
   完成这些步骤后，您可以在网络中的其他主机上挂载 NFS 共享。

图 6-3：
从此对话框指定 NFS 共享的用户访问选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_729_1.png)

## 使用 Samba 设置 Windows 服务器

如果您依赖 Windows 进行文件共享和打印共享，那么您可能在服务器和客户端中使用 Windows。如果是这样，您仍然可以在不丢失 Windows 文件和打印共享功能的情况下将 Red Hat Linux PC 作为服务器使用；Red Hat Linux 可以设置为 Windows 服务器。当您从本书的附带 CD-ROM 安装 Red Hat Linux 时，您也有机会安装 Samba 软件包，该软件包执行此设置。您只需在安装期间选择 Windows 文件服务器 软件包组即可。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_730_0.png)

在 Linux PC 上安装并配置 Samba 后，您的客户端 PC — 即使它们运行的是旧的 Windows for Workgroups 操作系统或更新的 Windows 95/98/NT/2000/XP 版本 — 也可以访问 Red Hat Linux PC 上的共享磁盘和打印机。为此，它们使用 Server Message Block（SMB）协议，即 Windows 文件和打印共享中的底层协议。

安装 Samba 软件包后，您可以将 Red Hat Linux PC 设为 Windows 客户端，这意味着 Red Hat Linux PC 可以访问 Windows 服务器管理的磁盘和打印机。

Samba 软件包具有以下主要组件：

- `/etc/samba/smb.conf`：这是 SMB 服务器使用的 Samba 配置文件。
- `/etc/samba/smbusers`：此 Samba 配置文件显示 Samba 用户名与本地 Red Hat Linux PC 上用户名的对应关系。
- `nmbd`：这是 NetBIOS 名称服务器，客户端使用它查找服务器。（NetBIOS 的全称是 Network Basic Input/Output System — 应用程序用于与网络传输（如 TCP/IP）通信的接口）
- `nmblookup`：此命令返回由其 NetBIOS 名称标识的 Windows PC 的 IP 地址。
- `smbadduser`：此程序将用户添加到 SMB 密码文件。
- `smbcacls`：此程序操作共享文件上的 Windows NT 访问控制列表（ACL）。
- `smbclient`：这是 Windows 客户端，在 Linux 上运行，允许 Linux 访问任何 Windows 服务器上的文件和打印机。
- `smbcontrol`：此程序向 `smbd`、`nmbd` 或 `winbindd` 进程发送消息。
- `smbd`：SMB 服务器，接受 Windows 客户端的连接并提供文件和打印共享服务。
- `smbmount`：此程序在 Red Hat Linux PC 上挂载 Samba 共享目录。
- `smbpasswd`：此程序更改 SMB 用户的密码。
- `smbprint`：此脚本启用在 SMB 服务器上的打印机上打印。
- `smbstatus`：此命令列出本地主机的当前 SMB 连接。
- `smbtar`：此程序直接将 SMB 共享备份到 Red Hat Linux 系统上的磁带驱动器。
- `smbumount`：此程序卸载当前已挂载的 Samba 共享目录。
- `testparm`：此程序确保 Samba 配置文件正确。
- `winbindd`：此服务器解析来自 Windows NT 服务器的名称。

在以下各节中，我将描述如何从附带 CD-ROM 安装 Samba 以及如何从 Red Hat Linux PC 打印到 Windows PC 上的共享打印机。

### 检查 Samba 是否已安装

通过在终端窗口中键入以下命令检查 Samba 是否已安装：

```
rpm -q samba
```

如果您看到类似以下输出，则表示 Samba 已安装在您的系统上：

```
samba-3.0.0-5rc1
```

如果收到软件包未安装的消息，请按照以下步骤从本书的附带 CD-ROM 安装 Samba：

1. **以 root 身份登录并将第一张 DVD 插入驱动器。如果您使用 GNOME 或 KDE，DVD 应该会自动挂载。如果没有，请键入以下命令挂载 DVD：**
   `mount /mnt/cdrom`
2. **使用以下命令更改到 DVD — 具体来说是 Red Hat Package Manager（RPM）软件包所在的目录：**
   `cd /mnt/cdrom/RedHat/RPMS`
3. **使用以下 rpm 命令安装 Samba：**
   `rpm -ivh samba*`
   如果 Samba 已安装，此命令会返回错误消息。否则，rpm 命令通过将各种文件复制到适当位置在您的系统上安装 Samba。

安装 Samba 软件后，您必须在可以使用它之前配置 Samba。

### 配置 Samba

要设置 Windows 文件共享和打印共享服务，请使用图形化 Samba 服务器配置工具按照以下步骤操作：

1. **选择 主菜单→系统设置→服务器设置→Samba。**
   如果您未以 root 身份登录，系统会提示您输入 root 密码。然后 Samba 服务器配置窗口出现。

2. **单击 添加 按钮。**
   创建 Samba 共享 对话框出现。

3. **输入要共享的目录名称或单击 浏览 并选择一个目录（目录必须已存在）。还选择权限 — 只读或读写（见图 6-4）。**
   图 6-4 显示了一个典型的示例，共享 `/home/public` 目录。如果目录不存在，您可以以 root 身份登录并在终端窗口中键入 `mkdir /home/public` 来创建目录。

4. **在 创建 Samba 共享 对话框的 访问 选项卡上，输入应有权访问共享目录的用户或选择 允许所有人访问 单选按钮，然后单击 确定。**

![](img/a7eec43a54473e95dc5ea333fecf1bd7_732_0.png)

图 6-4：输入要共享的目录信息。

Samba 服务器配置工具通过在配置文件 `/etc/samba/smb.conf` 中添加条目来创建 Samba 共享。

5. 要设置 Samba 服务器的工作组名称，请在 Samba 服务器配置工具中选择 首选项→服务器设置。然后在 服务器设置 对话框的 基础 选项卡中输入与您的 Windows 网络相同的 workgroup 名称（见图 6-5）。

图 6-5：
输入工作组名称和描述。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_733_0.png)

6. 在 服务器设置 对话框的 安全 选项卡上，选择来宾用户名称（如果需要）并选择身份验证模式。
   如果您将身份验证模式设置为 用户，用户可以使用用户名和密码登录以访问 Samba 共享。

7. 要添加可以访问 Samba 共享的用户，请在 Samba 服务器配置工具中选择 首选项→Samba 用户；在 Samba 用户 对话框中，单击 添加用户 并在 创建新的 Samba 用户 对话框中填写所需信息 — 用户名和密码。
   首先识别 Unix 用户名，然后为该用户设置 Samba 用户名和 Samba 密码（见图 6-6）。

图 6-6：
添加可以访问 Samba 共享的用户信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_733_1.png)

8. 添加完用户后，单击 确定 关闭 Samba 用户 对话框。
