
```
$ sudo /etc/init.d/samba start
```

## 使用 `smbstatus` 命令

`smbstatus` 命令报告 Samba 连接的当前状态。语法如下：

```
/usr/bin/smbstatus [options]
```

表 22.2 显示了一些可用的选项

### 表 22.2 `smbstatus` 选项

| 选项 | 结果 |
|---|---|
| `-b` | 简要输出 |
| `-d` | 详细输出 |
| `-s /path/to/config` | 如果启动时使用的配置文件不是标准文件，则使用该配置 |
| `-u username` | 显示特定用户连接的状态 |
| `-p` | 列出当前 `smb` 进程，这在脚本中可能很有用 |

## 使用 `smbclient` 命令连接

`smbclient` 命令允许其他 Linux 主机上的用户访问你的 `smb` 共享。你无法在主机上挂载该共享，但可以以类似于 FTP 客户端的方式使用它。`smbclient` 命令可以使用多个选项。最常用的是 `-I` 后跟要连接的计算机的 IP 地址。`smbclient` 命令运行不需要 `root` 权限：

```
smbclient -I 10.10.10.20 -Uusername%password
```

这会给出以下提示：

```
smb: <current directory on share>
```

从这里开始，命令几乎与标准的 UNIX/Linux FTP 命令相同。请注意，你可以在 `smbclient` 命令行上省略密码。然后会提示你输入 Samba 共享密码。

## 挂载 Samba 共享

有两种方法可以将 Samba 共享挂载到你的 Linux 主机。挂载共享与挂载可用的媒体分区或远程 NFS 目录相同，只是 Samba 共享使用 SMB 进行访问。第一种方法使用标准的 Linux `mount` 命令：

```
mount -t smbfs //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,\ fmask=777
```

### 注意

如果你的名称服务正在运行或主机在你的 `/etc/hosts` 文件中，你可以用主机名代替 IP 地址。

此命令将 `ahudson` 的主目录挂载到你的主机上，并给予所有用户对挂载点的完全权限。权限等于 `chmod` 命令上的权限。

第二种方法使用 `smbmount` 命令产生相同的结果，如下所示：

```
# smbmount //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,\
fmask=777
```

要卸载共享，请使用以下标准命令：

```
# umount /mount/point
```

你也可以使用这些挂载命令将真正的 Windows 客户端共享挂载到你的 Ubuntu 主机。使用 Samba，你可以配置服务器提供 Windows 可以提供的任何服务，而除了你之外没有人会知道。

## 使用 SWAT 配置 Samba

Samba 开发团队通过 Samba Web Administration Tool（SWAT）使管理 Samba 变得更加容易。SWAT 是一个基于 Web 的配置和维护界面，尽可能接近所见即所得的 Samba 环境。本节提供了一个简单示例，说明如何使用 SWAT 设置对用户主目录的 SMB 访问以及如何共享目录。

> 注意
>
> 使用 SWAT 需要你安装 `inetd` 和 `swat` 包，因此在继续之前请确保已安装。
>
> 此外你需要通过使用命令 `sudo passwd root` 为 `root` 账户设置密码来启用 `root` 账户。不启用 `root` 账户会阻止你有效地使用 SWAT。

在你开始使用 SWAT 之前需要执行几个步骤。首先，确保已安装 Samba 和 `swat` 包。然后通过编辑 `/etc/inetd.conf` 文件并将以下行更改为删除 `#<off>#` 注释来启用对系统的 SWAT 访问：

```
#<off># swat stream tcp nowait.400 root\
/usr/sbin/tcpd /usr/sbin/swat
```

保存文件，然后使用以下命令重新启动 `inetd` 守护进程：

```
# /etc/init.d/inetd restart
```

接下来，启动一个 X 会话，启动 Firefox，并浏览到 `http://localhost:901` 统一资源定位符（URL）。你会看到登录提示。输入 `root` 用户名和密码，然后单击 OK 按钮。屏幕清除后，你会看到主 SWAT 页面，如图 22.2 所示。

### TIP

你也可以使用 Ubuntu 的 `shares-admin` 客户端来配置 Samba。从 X 终端窗口的命令行启动该客户端，或选择 System、Administration、Shared Folders 菜单项（如下文图 22.9 所示）。

![](img/e464b828c497c99e41f61d4c55f1c0db_551_0.png)

**FIGURE 22.2** 你可以使用 SWAT 在系统上轻松配置和管理 Samba。

首先，在 SWAT 主页中单击 Globals 图标。你会看到类似图 22.3 所示的页面。窗口中有许多选项，但你只需在 Security Options 部分下的 Hosts Allow 字段中输入一个或多个 IP 地址或子网地址（例如 `192.168.2.`—注意末尾的句点，这允许所有主机访问；在该示例中，为 `192.168.2` 子网），即可快速为来自本地网络的主机设置访问权限。如果需要了解如何格式化条目，请单击该字段左侧的 Help 链接。会出现一个新网页，其中包含相关信息。

完成后，单击 Commit Changes 按钮保存全局访问设置。下一步是创建 Samba 用户并设置用户的密码。单击 SWAT 主页上的 Password 图标（参见图 22.2）。Server Password Management 页面打开，如图 22.4 所示。在 User Name 字段中输入新用户名；然后在 New Password 和 Re-type New Password 字段中输入密码。

**FIGURE 22.3** 配置 Samba 以允许来自本地网络上的特定主机或子网的访问。

**NOTE** 你必须提供一个现有系统用户的用户名，但用于 Samba 访问的密码不必与现有用户的密码匹配。

完成后，单击 Add New User 按钮。SWAT 然后创建用户名和密码并显示 Added user `username`（其中 `username` 为你输入的名称）。如果 Samba（`smb`）服务器正在运行，新 Samba 用户现在应该能够从任何允许的主机访问其主目录。

例如，如果你在一台名为 `mini` 的主机上设置了 Samba，该主机有一个名为 `andrew` 的用户，则该用户可以从任何远程主机（如果 Globals 设置允许）访问 `mini` 上的主目录，也许可以使用 `smbclient` 命令如下：

```
$ smbclient //mini/andrew -U andrew
added interface ip=192.168.2.68 bcast=192.168.2.255 netmask=255.255.255.0
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.5]
smb: \> pwd
Current directory is \\mini\andrew\
smb: \> quit
```

![](img/e464b828c497c99e41f61d4c55f1c0db_552_0.png)

![](img/e464b828c497c99e41f61d4c55f1c0db_553_0.png)

**FIGURE 22.4** 在 SWAT Password 页面中输入 Samba 用户名和密码。

单击 Status 图标（如图 22.2 或 22.4 所示）以查看 Samba 的状态或启动、停止或重启服务器。你可以使用结果网页上的各种按钮来控制服务器并查看定期或连续的状态更新。

你也可以使用 SWAT 来共享 Linux 目录。首先，单击主 Samba 页面顶部工具栏中的 Shares 图标（参见图 22.2）。在 Create Shares 字段中输入共享名称，然后单击 Create Shares 按钮。SWAT Shares 页面会在对话框中显示详细配置信息，如图 22.5 所示，提供对新 Samba 共享的详细配置的访问。
