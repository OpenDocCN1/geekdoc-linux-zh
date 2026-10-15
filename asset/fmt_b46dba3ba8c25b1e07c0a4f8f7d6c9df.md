
`smbclient` 命令允许其他 Linux 访问你的 Samba 共享。你无法在主机上挂载共享，但可以用类似于 FTP 客户端的方式使用它。`smbclient` 命令可以使用多个选项。最常用的是 `-I`，后面跟着连接计算机的 IP 地址。运行 `smbclient` 命令不需要 root 权限：

```bash
smbclient -I 10.10.10.20 -Username%password
```

这将为你提供以下提示符：

```
smb: <共享上的当前目录>
```

从这里开始，命令与标准的 UNIX/Linux FTP 命令几乎相同。注意，你可以在 `smbclient` 命令行中省略密码。然后会提示你输入 Samba 共享密码。

# 让 Samba 运转

```bash
mount -t smbfs //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,fmask=777
```

> 注意
>
> 如果您的名称服务正在运行或主机位于您的 `/etc/hosts` 文件中，可以将主机名替换为 IP 地址。

此命令将 `ahudson` 的家目录挂载到您的主机上，并赋予所有用户对该挂载点的完全权限。这些权限等于 `chmod` 命令中的权限。

第二种方法使用 `smbmount` 命令产生相同的结果：

- `# smbount //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,fmask=777`

要卸载共享目录，请使用标准命令：

# `umount /mount/point`

这些挂载命令也可以用于将真正的 Windows 客户端共享挂载到您的 Fedora。通过 Samba，您可以配置服务器提供 Windows 可以提供的任何服务，但又谁会知道呢。

# 使用 SWAT 配置 Samba

Samba 开发者团队通过 Samba Web 管理工具 `SWAT` 让管理 Samba 变得轻而易举。`SWAT` 是一个基于 Web 的配置和维护界面，尽可能地接近点击式的 Samba 环境。本节提供了一个如何使用 `SWAT` 设置用户家目录的 SMB 访问以及如何共享目录的简单示例。

在启动 `SWAT` 之前，您需要执行几个步骤。首先，确保您已安装了 Samba 和 `samba-swat` RPM 包。然后，通过编辑 `/etc/xinetd.d/swat` 文件并更改以下行来启用 `SWAT` 对您系统的访问：

```
disable = yes
```

将单词 `yes` 改为 `no`，如下所示：

```
disable = no
```

保存文件，并使用 `system-config-services` 客户端或 `/etc/rc.d/init.d` 下的 `xinetd` 脚本重启 `xinetd` 守护进程，如下：

```
# /etc/rc.d/init.d/xinetd restart
```

# 第 23 章 文件与打印

接下来，启动 X 会话，启动 Mozilla 浏览器，并浏览到 `http://localhost:9011` 统一资源定位符 `URL`。屏幕将显示登录提示。输入 `root` 用户名和密码，然后点击 `OK` 按钮。屏幕清除，您将看到 `SWAT` 主页，如图 23.2 所示。

> 提示
>
> 您也可以使用 Fedora 的 `system-config-samba` 客户端配置 Samba。从 X 终端窗口的命令行启动客户端，或者选择系统设置中的 Samba 服务器菜单项（如后文图 23.2 所示）。

![](img/c4a0ea5ab3561ff33a8da88887702720_641_0.png)

图 23.2 `SWAT` 可以轻松配置和管理系统上的 Samba。

首先，点击 `SWAT` 主页上的 `GLOBALS` 图标。您将看到一个与图 23.2 类似的页面。窗口中有许多选项，但您只需在 `Security Options` 部分下的 `Hosts` 字段中输入一个或多个 IP 地址或子网地址（例如 `192.168.2.2`——注意末尾的点，它允许所有所有主机访问；在示例中，为 `192.168.2.2` 子网），即可为您的局域网主机设置地址。如果您需要关于如何格式化输入的帮助，请点击字段左侧的 `Help` 链接。将出现一个带有相关信息的网页。

# 让 Samba 运转

![](img/c4a0ea5ab3561ff33a8da88887702720_642_0.png)

**图 23.3** 配置 Samba 以允许来自局域网内特定主机或子网的访问。

完成后，点击 `Commit Changes` 按钮以保存全局访问设置。下一步是创建一个 Samba 用户并设置用户密码。点击 `SWAT` 账户主页上的 `PASSWORD` 图标（参考图 23.2）。服务器密码管理页面将打开，如图 23.4 所示。在 `User Name` 字段中输入新用户名；然后在 `New Password` 和 `Re-type New Password` 字段中输入密码。

> 注意
>
> 您必须提供一个现有系统用户的用户名，但用于 Samba 访问的密码不需要与现有用户的密码匹配。

完成后，点击 `Add New User` 按钮。`SWAT` 随后创建用户名和密码，并显示已添加的用户名 `username`（*username 为您输入的名称*）。如果 Samba (`smb`) 服务器正在运行，则新的 Samba 用户现在应该能够从任何允许的主机访问家目录。

# 第 23 章 文件与打印

![](img/c4a0ea5ab3561ff33a8da88887702720_643_0.png)

图 23.4 在 `SWAT Password` 页面输入 Samba 用户名和密码。

例如，如果您在名为 `mini` 的主机上设置了 Samba，该主机有一个名为 `andrew` 的用户，该用户就可以从任何远程主机访问 `mini` 上的家目录（如果 `GLOBALS` 设置允许），可能通过使用如下 `smbclient` 命令：

```
$ smbclient //mini/andrew -U andrew
added interface ip=192.168.2.68 bcast=192.168.2.255 nmask=255.255.255
```

```
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.5]
smb: > pwd
Current directory is \mini\andrew
smb: > quit
```

点击 `STATUS` 图标（如图 23.2 和 23.4 所示）以查看 Samba 状态，或停止、重启服务器。您可以使用网页上的各种按钮控制服务器并查看定期或持续的状态更新。

您还可以使用 `SWAT` 共享 Linux 目录。首先，点击 Samba 顶部工具栏上的 `SHARE` 图标（参考图 23.2）。在 `Create Share` 字段中输入共享名称，然后点击 `Create Share` 按钮。`SWAT` 在对话框中显示详细配置信息，如图 23.5 所示。

# 让 Samba 运转

![](img/c4a0ea5ab3561ff33a8da88887702720_644_0.png)

**图 23.5** 使用 `shares` 页面轻松配置和管理系统上的 Samba。

完成后，点击 `Commit Changes` 按钮以保存全局访问设置。下一步是创建一个 Samba 用户并设置用户密码。点击 `SWAT` 账户页上的 `PASSWORD` 图标（参考图 23.2）。服务器密码管理页面打开，如图 23.4 所示。在 `User Name` 字段中输入新用户名；然后在 `New Password` 和 `Re-type New Password` 字段中输入密码。

> 注意
>
> 您必须提供一个现有系统用户的用户名，但用于 Samba 访问的密码不需要与现有用户的密码匹配。

完成后，点击 `Add New User` 按钮。`SWAT` 随后创建用户名和密码，并显示已添加的用户名 `username`（*username 为您输入的名称*）。如果 Samba (`smb`) 服务器正在运行，新的 Samba 用户现在应该从任何允许的主机访问家目录。

# 第 23 章 文件与打印

![](img/c4a0ea5ab3561ff33a8da88887702720_644_0.png)

图 23.4 在 `SWAT Password` 页面输入 Samba 用户名和密码。

例如，如果您在名为 `mini` 的主机上设置了 Samba，该主机有一个名为 `andrew` 的用户，该用户就可以从任何远程主机访问 `mini` 上的家目录（如果 `GLOBALS` 设置允许），可能通过如下 `smbclient` 命令：

```
$ smbclient //mini/andrew -U andrew
added interface ip=192.168.2.68 bcast=192.168.2.255 nmask=255.255.255
```
