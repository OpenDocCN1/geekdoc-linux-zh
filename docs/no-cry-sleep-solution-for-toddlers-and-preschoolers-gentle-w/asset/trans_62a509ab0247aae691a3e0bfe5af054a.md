

使用 netlogon，你可以将 Samba 配置为 Linux 和 Windows 主机的身份验证服务器。每个主机都需要设置一个 Samba 用户名和密码。在 smb.conf 文件的 Global 部分中，请确保启用加密密码、用户级安全以及域登录，并且操作系统的级别为 33 或更高：

```
[global]
encrypt passwords = yes
security = user
domain logons = yes
os level = 33
```

> 注意 你也可以将 Samba 配置为 Windows NT 网络的主域控制器（PDC）。作为 PDC，Samba 可以处理域登录、检索用户和组列表，并提供用户级安全。

## 使用客户端访问 Samba 服务

连接到 SMB 网络的客户端系统可以访问 Samba 服务器提供的共享服务。Windows 客户端应该能够通过 Windows 桌面上的“网络邻居”和“整个网络”图标自动访问共享目录和服务。对于连接到同一网络的其他 Linux 系统，可以使用特殊的 Samba 客户端程序访问 Samba 服务。使用 smbclient，本地 Linux 系统可以连接到 Samba 服务器上的共享目录并传输文件，以及运行 shell 程序。使用 smbmount，可以将 Samba 服务器上的目录挂载到 Linux 客户端的本地目录。

> 注意 有多个 Samba 浏览器客户端可用于 GNOME 和 KDE。对于 KDE，你可以使用 Komba2（可从 apps.kde.com 下载）。对于 GNOME，你可以使用 Gnomba。

## smbclient

smbclient 实用程序像 FTP 一样操作，用于通过 SMB 协议访问系统。与使用 FTP 客户端可以访问 FTP 服务器或 Unix 系统不同，使用 smbclient 你可以访问 SMB 共享服务，无论是在 Samba 服务器上还是在 Windows 系统上。许多 smbclient 命令与 FTP 相似，例如 mget 用于传输文件或 del 用于删除文件。smbclient 程序有多个选项用于查询远程系统以及连接到它。有关完整选项和命令列表，请参阅 smbclient 手册页。smbclient 程序以服务器名称和你想在该服务器上访问的服务作为参数。双斜杠在服务器名称前，单斜杠将其与服务分隔开。服务可以是任何共享资源，例如目录或打印机。服务器名称是其 NetBIOS 名称，可能与 IP 名称相同也可能不同。例如，要指定名为 turtle.mytrek.com 的服务器上的 myreports 共享目录，请使用 //turtle.mytrek.com/myreports。如果必须指定路径名，请对 Windows 文件使用反斜杠，对 Unix/Linux 文件使用正斜杠：

```
//server-name/service
```

你也可以提供访问服务的密码。将其作为服务名称之后的參數输入。如果不提供密码，将提示你输入。

> 注意 你也可以使用 Nautilus（GNOME 文件管理器）来访问 Samba 共享。使用 smb: 协议，如 smb://lizard/windata。仅输入 smb:// 将显示所有 Samba 共享。

## 使用 smbclient 访问共享

然后你可以添加多个选项来访问共享，例如远程用户名或可用服务的列表。使用 -I 选项，你可以使用 IP 地址指定系统。你使用 -U 选项和登录名来指定在远程系统上想要使用的远程登录名。如果需要密码，请附加 % 与密码一起使用。使用 -L 选项，你可以获取服务器上提供的服务列表，例如共享目录或打印机。以下命令将列出主机 turtle.mytrek.com 上可用的共享：

```
smbclient -L turtle.mytrek.com
```

要访问远程系统上的特定目录，请将目录作为 smbclient 命令的参数输入，后跟任何选项。对于 Windows 文件，你对路径名使用反斜杠，对于 Unix/Linux 文件你使用正斜杠。连接后，将显示 smb 提示符，你可以使用 smbclient 命令如 get 和 put 来传输文件。quit 或 exit 命令退出 smbclient 程序。在以下示例中，smbclient 访问 turtle.mytrek.com 系统上的 myreports 目录，使用 dylan 登录名：

```
smbclient //turtle.mytrek.com/myreports -I 192.168.0.1 -U dylan
```

在大多数情况下，你只需使用服务器名称来引用服务器，如下所示：

```
smbclient //turtle.mytrek.com/myreports -U dylan
```

如果你正在访问 Samba 服务器上某个特定账户的主目录，你可以简单地指定 homes 服务。在下一个示例中，用户在被提示输入该账户密码后访问 Samba 服务器上 aleina 账户的主目录：

```
smbclient //turtle.mytrek.com/homes -U aleina
```

你也可以使用 smbclient 来访问位于 Windows 客户端上的共享资源。指定 Windows 客户端的计算机名称以及其共享文件夹。在下一个示例中，用户访问名为 lizard 的 Windows 客户端上的 windata 文件夹。该文件夹配置为允许任何人访问，因此用户只需在密码提示时按 ENTER 键。

```
$ smbclient //lizard/windata
added interface ip=192.168.0.2 bcast=192.168.0.255 netmask=255.255.255.0
Got a positive name query response from 192.168.0.3 ( 192.168.0.3 )
Password:
```

