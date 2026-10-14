

# 管理 Samba

对 Samba 配置进行更改后，你需要重启 Samba 程序。最简单的方式是使用 /etc/init.d 文件夹中的 Ubuntu 启动脚本：

- `/etc/init.d/samba start`：启动 Samba 服务器。
- `/etc/init.d/samba stop`：停止 Samba 服务器。
- `/etc/init.d/samba restart`：停止并重新启动 Samba 服务器。

当你重启 Samba 服务器时，它会读取当前的 smb.conf 配置文件并处理配置设置。

提示
如果你不喜欢仔细阅读文本配置文件，可以试试 Samba Web 管理工具（称为 SWAT）。它提供了一种基于 Web 的方式来创建共享和更改 Samba 配置文件中的设置。要运行 SWAT，你必须使用 apt-get 安装 swat 包：
`sudo apt-get install swat`
安装该软件包后，你需要启动 inetd 程序，该程序在后台运行并监听 SWAT 端口上的连接：
`sudo /usr/sbin/inetd`

## Samba 客户端

为你所在环境制定好 Samba 服务器配置后，你需要对其进行测试。你可以使用 Ubuntu 服务器上的 smbclient 程序来执行此操作。

smbclient 程序提供了一个命令行界面，用于与网络上的 Windows 共享进行交互，无论它是 Samba 共享还是来自 Windows 服务器或工作站的共享文件夹。该命令行界面有些笨重，但它能够让你在远程 Windows 共享和 Ubuntu 服务器之间存储和检索文件。

### smbclient 程序

你可以使用多个命令行参数来控制 smbclient 程序的行为。smbclient 程序的格式为：

```
smbclient servicename [password] [options]
```

servicename 参数定义要连接的 Windows 共享。Windows 共享使用以下格式指定：

```
//server/share
```

其中 server 是服务器的 Windows 主机名，share 是共享文件夹的共享名。

默认情况下，smbclient 会尝试使用运行命令的用户帐户连接到共享。你可以在命令行中指定帐户密码，或者，如果你愿意，也可以不指定，smbclient 会提示你输入密码。

以下是一个连接到当前用户帐户主文件夹的示例：

```
test@testbox:~$ smbclient //localhost/test
Enter test's password:
Domain=[TESTBOX] OS=[Unix] Server=[Samba 3.2.3]
smb: \>
```

输入密码后，smbclient 程序会连接到共享并显示 smb> 提示符。

如果你想以其他用户帐户连接，请使用 -U 参数：

```
test@testbox:~$ smbclient //localhost/rich -U rich
Enter rich's password:
Domain=[TESTBOX] OS=[Unix] Server=[Samba 3.2.3]
smb: \>
```

smbclient 程序可以像连接其他 Samba 共享一样轻松地连接 Windows 共享：

```
rich@testbox:~$ smbclient //elijah/testshare
Enter rich's password:
Domain=[ELIJAH] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
smb: \>
```

在此示例中，服务器 Elijah 是一台 Windows XP Home Edition 工作站。smbclient 连接信息显示为 Windows 5.1 操作系统。

一旦连接到共享，你会看到 smb> 提示符。下一节将讨论如何在该提示符下与远程服务器进行交互。

> **提示**
> 
> 另一个有用的参数是 -I 参数。它允许你指定远程服务器的 IP 地址，这样 Samba 就不必尝试解析服务器名称。如果服务器位于远程网络上，并且没有为该网络提供服务的 WINS 服务器，此参数尤其有用。

## 与 Windows 共享交互

使用 smbclient 程序连接到远程共享后，你会希望能够与远程共享进行交互。smbclient 程序提供了许多命令，用于在远程共享上执行各种功能。

smb> 提示符的工作方式与 Ubuntu 中的命令行提示符类似。键入命令并按 Enter 键发送处理。表 22-2 列出了一些较常用的命令。

