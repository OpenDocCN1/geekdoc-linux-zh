
## 故障排除

如果您的系统上未安装 Apache Web 服务器，请使用以下说明进行安装：

- 以 root 用户身份登录。
- 挂载 Red Hat Linux 安装光盘 (CD-ROM，第 1 张)。
- 输入以下命令以安装 Apache 及其支持包（如果 CD-ROM 驱动器的挂载点不同，请将 `/mnt/cdrom` 替换为您的 CD-ROM 驱动器的挂载点）：

```
# rpm -ivh /mnt/cdrom/RedHat/RPMS/apache\*.rpm
```

如果 Apache Web 服务器未运行，请以 root 身份输入以下命令以启动它：

```
/etc/rc.d/init.d/httpd start
```

如果您的系统上未安装 FTP 服务器，请使用以下说明进行安装：

- 以 root 用户身份登录。
- 挂载 Red Hat Linux 安装光盘 (CD-ROM，第 1 张)。
- 输入以下命令以安装 FTP 服务器及其支持包（如果 CD-ROM 驱动器的挂载点不同，请将 `/mnt/cdrom` 替换为您的 CD-ROM 驱动器的挂载点）：

```
# rpm -ivh /mnt/cdrom/RedHat/RPMS/wu-ftpd*.rpm
```

如果您的系统上未安装匿名 FTP 支持，请使用以下说明进行安装：

- 以 root 用户身份登录。
- 挂载 Red Hat Linux 安装光盘 (CD-ROM，第 1 张)。
- 输入以下命令以安装匿名 FTP 及其支持包（如果 CD-ROM 驱动器的挂载点不同，请将 `/mnt/cdrom` 替换为您的 CD-ROM 驱动器的挂载点）：

```
# rpm -ivh /mnt/cdrom/RedHat/RPMS/anonftp*.rpm
```

### 复习

本节课向您介绍了互联网服务。您学习了如何使用邮件服务器 (sendmail) 与互联网上的其他系统交换电子邮件。我们还研究了 Apache Web 服务器的设置，以及放置 HTML 文档的位置和查找日志文件的位置。最后，您探索了在 Red Hat Linux 系统上如何设置匿名 FTP。

### 自我测验

- 哪个配置文件存储了互联网服务与端口号之间的关联？（参见“理解互联网服务”。）
- 什么是邮件传输代理？（参见“使用电子邮件服务器”。）
- Apache Web 服务器从哪个目录提供 Web 页面 (HTML 文件)？（参见“设置 Apache Web 服务器”。）
- Web 服务器的配置文件存储在哪里？（参见“设置 Apache Web 服务器”。）
- 您应该在哪个目录中放置希望其他人通过匿名 FTP 下载的文件？（参见“设置 FTP 服务器”。）

## 第 15 课

# 将 Red Hat Linux 用作工作组服务器

**会话检查清单**

- 使用 NFS 共享文件
- 使用 Samba 将 Red Hat Linux 电脑设置为 Windows 服务器

![](img/5fe8f856723cde0b366f73584b9e64b8_170_0.png)

配置了 Red Hat Linux（来自本书配套 CD-ROM）的低端 Pentium PC（甚至是 486）可以成为一个功能强大的工作组或办公室服务器。工作组是一个小型局域网 (LAN)，可能包含大约十几台 PC。您可以将 Red Hat Linux 电脑配置为文件和打印服务器，并将其他电脑配置为客户端。客户端电脑可以运行 Windows 而不是 Linux。

本节课向您介绍 Samba 软件包，它随 Red Hat Linux 一起提供，并提供了将 Red Hat Linux 电脑设置为 Windows 网络服务器所需的一切。但是，首先您将通过网络文件共享 (NFS) 了解文件共享，这提供了除 Samba 之外的另一种文件共享方式。

### 使用 NFS 共享文件

使用 NFS 共享文件很简单，涉及两个基本步骤：

- 在 Red Hat Linux 服务器上，通过在 `/etc/exports` 文件中列出一个或多个目录来导出这些目录，从而使客户端系统能够访问它们。
- 在每个客户端系统上，使用 mount 命令挂载 Red Hat Linux 服务器导出的目录。

使用 NFS 进行文件共享的唯一问题是每个客户端系统必须支持 NFS。大多数 PC 都不附带 NFS。这意味着如果您想使用 NFS 共享文件，必须单独购买 NFS 软件。如果您的局域网 (LAN) 上的所有系统都运行 Linux 或具有内置 NFS 支持的其他 UNIX 变体，则使用 NFS 是有意义的。本节课通过示例向您展示了如何在局域网中的两台 Red Hat Linux 电脑上设置 NFS。

### 使用 NFS 导出文件系统

在服务器上，您必须运行 NFS 服务，并指定一个或多个文件系统以供*导出*，即供客户端系统使用。您可以使用 Linuxconf 图形化系统管理工具执行这两项任务。

执行以下步骤以启动 Linuxconf：

1. 以 root 身份登录，并从 GNOME 菜单中选择主菜单 **程序 系统 Linuxconf**。或者，再次以 root 身份打开终端窗口，并在命令提示符处输入 `linuxconf`。
2. 点击“配置”选项卡，然后选择**网络 服务器任务 导出文件系统** (NFS)。Linuxconf 随后显示“导出文件系统”选项卡，其中显示 `/etc/exports` 文件的当前内容。如果 `/etc/exports` 为空，显示效果应与图 15-1 相似。

![](img/5fe8f856723cde0b366f73584b9e64b8_171_0.png)

**图 15-1 空的“导出文件系统”对话框**

3. 点击**添加**按钮。这会在显示界面中添加“单个导出文件系统”选项卡，允许您定义导出文件系统的详细信息。您需要使用完整路径名指定文件系统，如图 15-2 所示。
4. 在此对话框中，您还应输入可以挂载此导出文件系统的客户端系统名称。在图 15-2 所示的示例中，正在导出 `/home/public` 目录，名为 *katie* 的主机可以挂载此文件系统以进行读和写操作。
5. 输入信息后，点击**接受**按钮。Linuxconf 返回到图 15-1 中显示的对话框，但现在显示关于导出文件系统的摘要信息。
6. 点击**取消**按钮以完成导出文件系统的定义。

![](img/5fe8f856723cde0b366f73584b9e64b8_172_0.png)

作为此会话的结果，Linuxconf 向 `/etc/exports` 文件添加了以下条目：`/home/public katie(rw)`

若要验证导出的目录是否列在 `/etc/exports` 文件中，请在终端窗口中输入 `cat /etc/exports`。

现在您应该打开 NFS 服务器。为此，点击“控制”选项卡，然后选择“控制面板 控制 服务状态”。Linuxconf 显示服务控制屏幕，其中列出所有服务及其状态，如图 15-3 所示。

![](img/5fe8f856723cde0b366f73584b9e64b8_172_1.png)

**图 15-3 在 Linuxconf 的服务控制屏幕中查看服务及其状态**

每一行有三个字段：一个提供服务名称，另一个指示服务是启用自动运行还是手动运行，最后一个揭示服务是否已在运行。向下滚动列表，找到名为 nfs 的 NFS 服务条目。在这种情况下，NFS 服务尚未运行。点击该条目。这将使 Linuxconf 显示“Service nfs”选项卡，如图 15-4 所示。

![](img/5fe8f856723cde0b366f73584b9e64b8_173_0.png)

**图 15-4 通过 Linuxconf“Service nfs”选项卡启动 NFS 服务**

此选项卡中的按钮允许您启动、停止或重启服务。在这种情况下，点击“启动”按钮以启动 NFS 服务。然后点击“接受”返回到上一个对话框（图 15-3）。现在，服务控制屏幕应显示 nfs 条目的状态为“运行中”。点击“取消”退出此对话框。

如果您 ever 对 `/etc/exports` 文件中列出的导出文件系统进行了任何更改，请记住重启 NFS 服务。点击图 15-3 所示对话框中的“重启”按钮。（注意：原文引用了图 15-6，可能是 OCR 或上下文错误，此处保留原文引用逻辑，但根据上下文，该按钮通常位于服务选项卡中。）

*更正说明：步骤 4 合并*：原文有“4. 输入信息...”和一个子项目符号“在此对话框中...”。为了流程更顺畅，我将其合并为步骤 4，因为它描述的是在同一对话框内的同一操作。

如果您更喜欢使用命令启动 NFS 服务，请以 root 身份登录，并在终端窗口中输入以下命令：

```
/etc/rc.d/init.d/nfs start
```

这样就设置好了 NFS 的服务器端。现在您可以尝试从客户端系统挂载导出的文件系统。

### 挂载 NFS 文件系统

您可以使用客户端系统上的 Linuxconf 来挂载导出的 NFS 文件系统。然而，执行挂载操作最简单的方法是以 root 身份登录并使用 mount 命令。例如，要在名为 katie 的客户端系统的 `/mnt/luther` 目录上挂载 luther 系统的 `/home/public` 文件系统，请输入：

```
mount luther:/home/public /mnt/luther
```

若要确认 NFS 文件系统确实已挂载，请在客户端系统上以 root 身份登录，并在终端窗口中输入 `mount`。您应该会看到一行关于 NFS 文件系统的类似内容：

```
luther:/home/public on /mnt/luther type nfs (rw,addr=192.168.1.200)
```

### 使用 Samba 将您的 Linux PC 设置为 Windows 服务器

如果您的业务依赖 Windows 进行文件和打印共享，您可能在服务器和客户端中都使用 Windows。您可以将 Red Hat Linux 电脑用作服务器，而不会失去 Windows 文件和打印共享功能，因为您可以将 Linux 电脑设置为 Windows 服务器。当您从本书的配套 CD-ROM 安装 Red Hat Linux 时，您也有机会安装 Samba 软件包，该包执行此任务。您只需在安装期间选择 DOS/Windows 连接包组即可。

![](img/5fe8f856723cde0b366f73584b9e64b8_174_0.png)

在安装和配置 Red Hat Linux PC 上的 Samba 之后，运行 Windows 95/98/NT/2000 的客户端 PC 可以通过使用服务器消息块 (SMB) 协议访问 Red Hat Linux PC 上的磁盘和打印机，该协议是 Windows 文件和打印共享的基础协议。

安装了 Samba 软件包后，您还可以将 Red Hat Linux PC 设置为 Windows 客户端。这意味着 Red Hat Linux PC 可以访问由 Windows 服务器管理的磁盘和打印机。Samba 软件包由以下主要组件组成：

- `smb` 是 SMB 服务器，接受来自 Windows 客户端的连接并提供文件和打印共享服务。
- `nmbd` 是客户端用于查找服务器的 NetBIOS 名称服务器。NetBIOS 代表网络基本输入/输出系统。NetBIOS 是应用程序用于与网络传输（如 TCP/IP）通信的接口。
- `/etc/samba/smb.conf` 是 SMB 服务器使用的 Samba 配置文件。
- `testparm` 是一个确保 Samba 配置文件正确的程序。
- `smbclient` 是运行在 Red Hat Linux 上的 Windows 客户端，允许 Red Hat Linux 访问任何 Windows 服务器上的文件和打印机。
- `smbprint` 是一个脚本，用于启用在 SMB 服务器上的打印机上打印。
- `smbadduser` 是一个将用户添加到 SMB 密码文件的程序。
- `smbpasswd` 是一个更改 SMB 用户密码的程序。
- `smbstatus` 是一个列出当前本地主机 SMB 连接的命令。

