
# 第二部分：面向桌面用户的 Ubuntu

## 第 26 章：文件传输与共享

```
$ smbtree
Password:
WVH
YM901252
\\\YM901252$ADMIN$
\\\YM901252$IPC$
\\\YM901252$disk1
\\\HD-HTGLB05
\\\HD-HTGLB05$info
\\\HD-HTGLB05$share
\\\HD-HTGLB05$IPC$
\\\HD-HTGLB05$ADMIN$
\\\XEN
\\\XEN$wwh
\\\XEN$brother
\\\XEN$Silentwriter
\\\XEN$Styl_200
\\\XEN$IPC$
\\\UBUNTU
\\\UBUNTU$wwh
\\\UBUNTU$pdf
\\\UBUNTU$IPC$
\\\UBUNTU$prints
\\\WINSERVER
\\\WINSERVER$IPC$
\\\WINSERVER$print$
\\\WINSERVER$wwh
\\\WINSERVER$office Y901252
IPC Service (YM901252)
IPC Service (YM901252)
TeraStation utilities
TeraStation folder
TeraStation folder
IPC Service (HD-HTGLB05)
IPC Service (HD-HTGLB05)\aSamba Ubuntu Server
Home Directories
Brother Hl-2070N h11250 Driver
Office Silentwriter
Epson Stylus Photo R200
IPC Service (Samba Ubuntu Server)
Desktop Ubuntu
Home Directories
PDF
IPC Service (Desktop Ubuntu)
Printer Drivers
Windows 2000 LAN Mgr
Remote IPC
Printer Drivers
Home Directory
Shared Enterprise Data
```

如果你不确定 Windows（或 Samba）服务器导出的共享，也可以使用 `smbclient` 命令列出它们，它会提示你输入 Windows 密码，如下例所示：

```
$ smbclient -L 192.168.6.2
Password:
Domain-[WINSERVER] OS--[Windows 5.1] Server--[Windows 2000 LAN Mgr]
Sharename Type Comment
--------- ---- ----------
IPC$ IPC Remote IPC
print$ Disk Printer Drivers
wwh Disk Home Directory
office Disk Shared Enterprise Data
Domain-[WINSERVER] OS--[Windows 5.1] Server--[Windows 2000 LAN Mgr]
```

| Server | Comment |

| --- | --- |

| Workgroup | Master |

| WVH | HD-HTGL0B5 YM091252 |

你可以使用这两个示例中的任何信息来识别想要挂载的共享名称以及该共享的服务器。你需要这些信息来使用后续节中描述的任何机制将其挂载到你的系统上。

### 在启动时挂载 Windows 共享

如果你知道自己将经常需要访问共享中的文件和目录，那么让它永久可用的简单方法是将其添加到 Ubuntu 系统启动的文件系统列表中。第 4 章“基础 Linux 系统概念”中名为“启动时自动挂载文件系统”的章节解释了包含文件系统列表的文件格式。本节解释了在启动时挂载网络共享所需的条目。

如果你知道要挂载的 Windows 共享名称和相关服务器，你就拥有了将其挂载到 Ubuntu 系统上所需的所有信息。如果不知道，你可以可以使用一节中的任何一个示例来获取共享和名称。要在系统启动时挂载该共享，请向 `/etc/fstab` 文件添加该 Windows 共享添加条目。例如，为了将上例所示的 `office` 共享挂载到目录 `/mnt/office`（该目录必须已存在），我会创建一个如下的 `/etc/fstab`：

```
/192.168.6.2 /mnt/office cifs \
  creds=/etc/cifs.login,uid=0,gid=users 0 0
```

（此条目将在 `/etc/fstab` 文件中单行显示——反斜杠仅用于格式化。）

此条目的独特选项是挂载选项，它们的含义如下：

- `Automatically`：在系统启动时自动挂载文件系统。

- `credentials=/etc/cifs.login`：指定包含挂载文件系统时身份验证所需的用户名和密码的文件。因为 `/etc/fstab` 对所有人可读，出于安全考虑，你不希望将这些信息嵌入该文件中。你应该将这些信息放在单独的文件中并更改该文件使其仅供 root 读取（`sudo chmod g-r-o-r /etc/cifs.login`）。该文件应包含以下两行：

```
username=USERNAME
password=PASSWORD
```

- `USERNAME`：你想要在远程主机上挂载 Windows 共享的用户名，而 `PASSWORD` 是该用户的密码。

- `uid=0`：在挂载文件系统时使用用户 ID 0。

- `gid-users`：Windows 共享上的所有文件将将分配给 `users` 组。这使得你系统中属于该组的用户（使用其 Windows 登录名）可以访问它们在远程系统上拥有访问权限的文件。

#### 注意事项

某些版本的内核对 CIFS 文件系统的支持存在一些问题。如果由于你无法从远程系统挂载 CIFS 共享，或者在挂载后无法看到这些共享中的文件，你必须在针对这些共享的 `/fstab` 条目中，挂载选项列表中添加 `noserver` 关键字。

通过 `/etc/fstab` 文件挂载 Windows 共享将使你系统上的所有用户都能使用该共享，通过 `/etc/group` 文件中的用户条目以及共享中文件和目录的 Windows 权限设置来强制访问安全，这对于多用户服务器系统是没问题的。对于个人桌面 Linux 系统，你可能倾向于让每个系统的用户手动挂载他们自己需要的 Windows 共享，这将允许你更精确地在 Windows 服务器上利用他们的个人安全设置。接两个部分将讨论用户如何在自己的 Ubuntu 桌面系统上自行挂载 Windows 共享。

### 从 GNOME 桌面连接 Windows 共享

Ubuntu 的“位置”（Places）提供了“连接到服务器”命令，这让你轻松地在桌面上创建一个 Windows 共享的图标，并使用 Nautilus 文件管理器连接到该共享。选择“位置”->“连接到服务器”将显示如图 26-2 所示的对话框。要指定你想连接到一个需要身份验证的 FTP 服务器，请点击此对话框顶部的“服务类型”菜单，并在图 26-8 中选择 Windows 共享条目。

**图 26-8**

识别要连接的 Windows 共享

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_979_0.png)

你至少需要托管你想要连接的共享 Windows Windows 服务器名称或 IP 地址。如果你打算经常访问此目录，可以通过勾选“添加书签”并在“位置”菜单中输入书签名称，为它创建一个永久条目。你也可以指定你想要连接的用户身份名称、你想要连接的 Windows 域或工作组名称，以及你想要连接的共享，但这些都是可选的——当你尝试连接时，系统将对此处未指定的任何条目进行提示。点击“连接”以为你定义的 Windows 共享创建一个桌面图标。

仅仅为 Windows 共享创建一个桌面图标并不会真正建立连接。要实现这一点，请双击相应的桌面图标打开它。你将看到一个对话框，提示你输入尚未指定的任何必要信息，如图 29 所示。

**图 26-9**

完成 Windows 共享的身份验证信息

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_980_0.png)

一旦你输入了关于要连接的服务器共享的任何剩余信息，就会出现一个 Nautilus 文件管理器窗口，显示与你登录用户关联的默认目录的内容，如图 26-10 所示。

一旦 Nautilus 文件管理器显示，向任意方向复制文件都使用第 5 章中讨论的标准 Nautilus 和 GNOME 桌面规范。

当你访问 Windows 共享时，请关闭 Nautilus 文件管理器窗口。要丢弃图标，右键点击 Windows 共享图标并从弹出菜单中选择“卸载卷”以断开连接并丢弃图标。SMB 共享的桌面图标会在注销时自动移除。如果你想创建一个永久桌面图标，请参见本章前面的名为“为服务和位置创建永久桌面图标”的侧边栏获取更多信息。

**图 26-10**

在 Nautilus 文件管理器中连接到 Windows 共享
