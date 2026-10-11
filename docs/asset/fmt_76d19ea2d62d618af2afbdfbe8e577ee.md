
| `no_subtree_check` | 关闭子树检查（subtree_check 的相反） |
| `insecure_locks` | 允许不安全的文件锁定 |
| 用户映射选项 |  |
| `all_squash` | 将客户端所有的用户 ID 和组 ID 映射到匿名用户 |
| `no_all_squash` | 将远程用户和组 ID 映射到客户端上类似的 ID（默认） |
| `root_squash` | 将远程 root 映射到客户端的匿名用户（默认） |
| `no_root_squash` | 将远程 root 映射到本地 root |
| `anuid=UID` | 设置用于 `all_squash` 和 `root_squash` 选项的匿名用户 ID |
| `anongid=GID` | 设置用于 `all_squash` 和 `root_squash` 选项的匿名用户组 ID |

## 使用 NFS 进行工作

### 510 使用 NFS 共享文件

在 `/etc/exports` 文件中添加条目后，在终端窗口中输入以下命令来手动导出文件系统：

```
exportfs -a
```

此命令导出 `/etc/exports` 文件中定义的所有文件系统。

现在你可以启动 NFS 服务器进程了。

在 Debian 中，通过 root 身份登录并输入 `/etc/init.d/nfs-kernel-server start` 来启动 NFS 服务器。在 Fedora 中，你输入 `/etc/init.d/nfs start`。在 SUSE 中，输入 `/etc/init.d/nfserver start`。如果你希望 NFS 服务器在系统启动时启动，在 Debian 中使用 `update-rc nfs-kernel-server defaults`。在 Fedora 中，输入 `chkconfig --level 35 nfs on`。在 Xandros 中，输入 `update-rc --level 35 nfs-server defaults`。

当 NFS 服务启动后，NFS 服务器端就绪绪。你现在从客户端系统挂载导出的文件系统，并根据需要访问。

如果你对 `/etc/exports` 文件列出的导出文件系统进行了任何更改，请重启 NFS 服务。要重启服务，请调用 `/etc/init.d` 目录下的脚本，并将 `restart` 作为参数（而不是你启动服务时使用的 `start` 参数）。

## 挂载 NFS 文件系统

要在客户端系统访问导出的 NFS 文件系统，你必须将该文件系统挂载到挂载点上。挂载点仅仅是一个本地目录。例如，假设你想将名为 LNBP200 的服务器导出的 `/home` 目录挂载到客户端系统的本地目录 `/mnt/lnbp200`。为此，请按照以下步骤操作：

- 1. 以 root 身份登录并使用此命令创建目录：

```
mkdir /mnt/lnbp200
```

- 2. 输入以下命令将目录挂载到远程系统 (LNBP200) 的本地目录 `/mnt/lnbp200`：

```
mount lnbp200:/home /mnt/lnbp200
```

完成这些步骤后，你就可以从本地目录 `/mnt/lnbp200` 查看并访问导出的文件。

## 使用 Samba 设置 Windows 服务器

要确认 NFS 文件系统确实已挂载，在客户端系统上以 root 身份登录并在终端窗口中输入 `mount`。你会看到类似下面关于 NFS 文件系统的行：

```
lnbp200:/home/public on /mnt/lnbp200 nfs (rw,addr=192.168.0.4)
```

NFS 支持两种挂载操作——硬挂载（hard）和软挂载（soft），这意味着如果 NFS 服务器没有响应，客户端将无限尝试访问服务器直到其响应。你可以通过在 `mount` 命令中添加 `-o soft` 选项软挂载 NFS 卷。对于软挂载，如果 NFS 服务器未响应，客户端将返回错误。

![](img/49a40dc66bb14561782e2a1125eaccf3_536_0.png)

## 使用 Samba 设置 Windows 服务器

如果你依赖 Windows 进行文件共享和打印共享，你可能在服务器上使用了 Windows。

安装 Samba 包后，你可以让 Linux 成为任何 Windows 服务器的客户端。

Samba 包包含几个主要组件：

- `/etc/samba/smb.conf`：这是用户的 Samba 配置。
- `/etc/samba/users`：这是用户名的 Samba 配置。
- `nmbd`：这是 NetBIOS 名称服务器，客户端用它查找服务器。

## 使用 Samba 进行工作

### 512 使用 Samba 设置 Windows 服务器

- `smadduser`：此程序将用户添加到 SMB 密码文件中。
- `smbc`：此程序处理共享文件的 Windows 访问控制列表 (ACL)。
- `smclient`：这是运行在 Linux上的 Windows 客户端，允许 Linux 访问任何 Windows 服务器的文件和打印机。
- `smcontrol`：此程序向 `smbd`、`nmbd` 或 `winbindd` 进程发送消息。
- `smbd`：这是 SMB 服务器，接受 Windows 客户端的连接并提供文件共享和打印共享服务。
- `smbmount`：此程序在 Linux PC 上挂载 Samba 目录。
- `smpasswd`：此程序更改 SMB 用户的密码。
- `smprint`：此脚本启用 SMB 服务器上打印机的打印。
- `smstatus`：此命令列出本地 SMB 连接。
- `smbtar`：此程序将 SMB 共享直接备份到 Linux 上的磁带驱动器。
- `smbmount`：此程序卸载已挂载的 Samba 共享。
- `testparm winbind`：此服务器解析来自 Windows 服务器的名称。

## 安装 Samba

你可能在安装 Linux 时已经安装了 Samba。你可以先检查，如果系统中没有找到 Samba，可以轻松安装它。

在 Debian、MEPS、Ubuntu 和 Xandros 中，使用 `dpkg -l samba*` 查看是否安装 Samba。在 Fedora 和 SUSE 中，使用 `rpm -q samba` 查看 `samba` 包是否安装。

在 Debian、MEPS 和 Ubuntu 中，使用 `apt-get install samba` 安装 Samba。在 Fedora 中，以 root 身份登录并运行 `yum install samba-swat`。这会安装 Samba，以及 Web 配置界面 SWAT（Samba Web 管理工具）。在 SUSE 中，点击 YaST 中的“软件管理”。

### 使用 Samba 设置 Windows 服务器

进入控制中心的“软件”（Software）类别。然后使用 YaST 的搜索功能查找 `samba`，选择相关软件包并安装它们。对于 Xandros，在安装 Xandros 时就会获取 Samba。

安装 Samba 软件后，你必须先配置 Samba 才能使用。

## 配置 Samba

要设置 Windows 文件共享和打印机共享服务，你可以手动编辑配置文件，也可以使用 GUI 工具。当然，使用 GUI 比编辑配置文件要容易得多。Fedora 和 SUSE 都使用 GUI 工具来配置 Samba 服务器。

在 Fedora 中，选择 Firefox 并访问 `http://localhost:901/` 以打开 Samba 配置窗口。系统会提示你输入有效的用户名和密码。如果发生错误，请使用命令 `/sbin/chkconfig swat on` 确保 SWAT 正在运行。这将打开图 4-1 所示的配置界面。该工具创建并编辑 `/etc/samba/smb.conf` 文件中的条目。

图 4-1：在 Fedora 中使用 SWAT 配置 Samba。

![](img/49a40dc66bb14561782e2a1125eaccf3_538_0.png)

### 514 使用 Samba 设置 Windows 服务器

在 SUSE 中，你可以通过 YaST 控制中心配置 Samba —— 选择主菜单：系统；控制中心 (YaST) —— 点击窗口左侧的“网络服务”（Network Services），然后点击窗口右侧的“Samba 服务器”。YaST 会显示一个可以在其中配置 Samba 的窗口。首先选择一个工作组名称——YaST 会显示你局域网上任何 Windows 工作组的名称，点击下一步。然后你可以选择服务器类型、启用服务器并选择你想要共享的内容。退出 Samba 配置工具后，YaST 将 Samba 设置存储在 `/etc/samba` 目录下的配置文件中。

配置 Samba 后，在终端窗口中输入以下命令验证 Samba 配置文件是否正确：

```
testprogram
```

如果命令显示文件加载正常，那么你已经准备就绪了。`testprogram` 还会显示 Samba 配置文件的内容。
