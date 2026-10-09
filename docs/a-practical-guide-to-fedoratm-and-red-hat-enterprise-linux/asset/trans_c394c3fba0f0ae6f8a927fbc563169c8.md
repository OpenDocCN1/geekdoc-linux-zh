

## 挂载共享

使用 `-t cifs` 选项的 `mount` 实用程序（第 520 页）可以像挂载 Linux 目录层级一样挂载共享。有关 CIFS 协议的更多信息，请参阅第 1242 页。挂载共享时，您可以写入共享上的文件；但是，使用 `smbclient` 时无法写入共享上的文件。

挂载共享的命令语法如下（必须以 root 权限运行此命令）：

```
mount -t cifs //host/share dir
```

其中 *host* 是共享所在系统的名称，*share* 是你要挂载的共享的名称，*dir* 是将共享挂载到其上的 Linux 目录的绝对路径名（即挂载点）。

以下命令在 root 权限下运行时，会将 plum 上的 sam 共享挂载到 `/plum.sam` 目录：

```
# mount -t cifs //plum.sam /plum.sam -o username=sam
Password for sam@/plum.sam: ****** RETURN
# ls /plum.sam
Desktop Documents Downloads Music Pictures Public ...
```

省略用户名参数并提供空密码，即可挂载对匿名用户可见的共享。

使用 `uid`、`file_mode` 和 `dir_mode` 挂载选项配合 cifs 类型的文件系统，以建立已挂载文件的所有权和权限：

```
# mount -t cifs //plum.sam /plum.sam -o username=sam,uid=sam,file_mode=0644,dir_mode=0755
```

权限必须表示为以零开头的八进制数。更多信息请参考 `mount.cifs` 手册页。

您还可以将用户名、密码以及可选的工作组（域）存储在凭据文件中。为了防止其他用户挂载此共享，凭据文件应归 root 所有，且仅允许具有 root 权限的用户读取和写入（权限为 600）。如果在 `fstab`（第 524 页）中指定了凭据文件，则系统启动时会自动挂载该共享。以下是前例中共享的凭据文件：

```
# cat /etc/plum.sam.credentials
username=sam
password=password
domain=MC5
# ls -l /etc/plum.sam.credentials
-rw------- 1 root root 40 06-27 17:38 /etc/plum.sam.credentials
```

以下命令使用凭据文件挂载此共享：

```
# mount -t cifs //plum/sam /plum.sam -o credentials=/etc/plum.sam.credentials
```

`/etc/fstab` 中的以下行会导致系统启动时挂载该共享：

| //plum/sam | /plum.sam | cifs | defaults,credentials=/etc/plum.sam.credentials |
|---|---|---|---|

除非某个共享使用与其他共享相同的登录信息，否则每个共享必须拥有其自己的凭据文件；如果是这种情况，则这些文件可以使用同一个凭据文件。

## 从 Windows 操作共享

本节描述了如何从 Windows 机器访问 Linux（或 Windows）目录。你不需要设置 Linux 客户端就能从 Windows 机器浏览或映射 Linux 共享。

### 浏览共享

要从 Windows 访问 Samba 服务器上的共享，请在 Windows 系统上打开“我的电脑”或资源管理器，并在标记为“地址”的文本框中输入 `\\` 后跟 Samba 服务器的 NetBIOS 名称（如果未分配不同的 NetBIOS 名称，则只需输入主机名）。随后，Windows 将显示远程系统正在共享的目录的共享名称。例如，要查看名为 plum 的 Linux 系统上的共享，请输入 `\\plum`。从此窗口，你可以查看，如果允许，还可以浏览远程系统上可用的共享。如果你设置服务器上的共享使其不可浏览，你需要使用 `\\servername\\sharename` 格式输入共享的路径才能显示该共享。

### 映射共享

从 Windows 机器访问 Samba 服务器上的共享的另一种方法是映射（挂载）共享。在 Windows 系统上打开“我的电脑”或资源管理器，点击窗口顶部的“映射网络驱动器”，或从菜单栏的下拉列表中选择（在许多 Windows 机器上位于“工具”菜单中）。Windows 将显示“映射网络驱动器”窗口。从标记为“驱动器”的列表框中选择一个未使用的 Windows 驱动器字母，并在标记为“文件夹”的文本框中输入你要映射的共享的 Windows 路径。（当你使用 system-config-samba [仅限 Fedora] 创建共享时，共享的名称与你正在共享的目录的名称相同。）Windows 路径的格式为 `\\hostname\\sharename`。例如，要将 plum 上的 `\\tmp` 映射到 Windows 驱动器 J，假设共享名为 tmp，请在标记为“驱动器”的列表框中选择 J，在标记为“文件夹”的文本框中输入 `\\plum\tmp`，然后点击“完成”。在提供用户名和密码后，你应该能够从 Windows 机器上将 plum 的 `/tmp` 目录作为 J (tmp) 进行访问。如果无法映射驱动器，请参阅第 846 页的“故障排除”。

## 设置 Samba 服务器

本节描述了如何使用 **system-config-samba** 图形界面（仅限 Fedora）和编辑器编辑配置文件来安装和配置 Samba 服务器。

### 前提条件

安装以下软件包：

- samba
- system-config-samba（可选；仅限 Fedora）
- samba-common（随 samba 一起安装）

**启用并启动 smb** 运行 **systemctl** 使 **smb** 服务（**smbd** 守护进程）在系统每次进入多用户模式时启动，然后启动 **smb** 服务。使用 **systemctl status** 命令确保服务正在运行。

```
# systemctl enable smb.service
# systemctl start smb.service
```

虽然通常不需要，但在修改 **smb** 配置文件后，你可以再次运行第二条命令，将 **start** 替换为 **reload** 以使 **smb** 重新读取这些文件。

**启用并启动 nmb** 运行 **systemctl** 使 **nmb** 服务（**nmbd** 守护进程）在系统每次进入多用户模式时启动，然后启动 **nmb** 服务。使用 **systemctl status** 命令确保服务正在运行。

```
# systemctl enable nmb.service
# systemctl start nmb.service
```

虽然通常不需要，但在修改 **nmb** 配置文件后，你可以再次运行第二条命令，将 **start** 替换为 **reload** 以使 **nmb** 重新读取这些文件。

**服务器防火墙** Samba **服务器**使用 UDP 端口 137 和 138，以及 TCP 端口 139 和 445。如果服务器正在运行防火墙或位于防火墙之后，你需要打开这些端口。运行以下命令以在系统每次启动时（永久地）以及在正在运行的系统上打开这些端口；有关 **firewall-cmd** 的信息请参阅第 906 页。

```
# firewall-cmd --add-port=137/udp
# firewall-cmd --permanent --add-port=137/udp
# firewall-cmd --add-port=138/udp
# firewall-cmd --permanent --add-port=138/udp
# firewall-cmd --add-port=139/tcp
# firewall-cmd --permanent --add-port=139/tcp
# firewall-cmd --add-port=445/tcp
# firewall-cmd --permanent --add-port=445/tcp
```

**SELinux** 当 **SELinux** 设置为使用目标策略时，Samba 受 **SELinux** 保护。如有必要，你可以使用 **system-config-selinux**（第 475 页）来禁用此保护。如果你希望允许用户共享其主目录，请参阅第 840 页的“SELinux”。**smb.conf** 文件中包含关于为 Samba 配置 SELinux 的大量注释。

**打印机** 默认的 **smb.conf** 配置文件会共享 Samba 服务器上的打印机；无需额外配置。

![](img/243613168ac865b539f12460d966088e_893_0.png)

图 23-1 Samba 服务器配置窗口

主目录 默认的 smb.conf 配置文件会共享 Samba 服务器上用户的主目录；无需额外配置。

配置 /etc/sysconfig/samba 文件使 smbd 和 nmbd 均以 -D 选项启动，从而使 smbd 和 nmbd 进程作为守护进程运行。

### 快速入门：使用 system-config-samba 配置 Samba 服务器（Fedora）

system-config-samba 实用程序在 RHEL 下不可用，它只能设置 Samba 服务器的基本功能。然而，如果你不熟悉 Samba 并希望快速设置一个简单的 Samba 服务器，这是最佳工具。system-config-samba 实用程序执行三个基本功能：配置服务器、配置用户以及设置导出到 Windows 机器的共享（目录层级）。

要显示 Samba 服务器配置窗口（图 23-1），请从终端仿真器或输入命令窗口（Alt+T2）输入 `system-config-samba`。

配置服务器 选择菜单栏：首选项=>服务器设置，以显示“服务器设置”窗口的“基本”选项卡（图 23-2）。将工作组更改为 Windows 中正在使用的那个

![](img/243613168ac865b539f12460d966088e_893_1.png)

图 23-2 服务器设置窗口，基本选项卡

