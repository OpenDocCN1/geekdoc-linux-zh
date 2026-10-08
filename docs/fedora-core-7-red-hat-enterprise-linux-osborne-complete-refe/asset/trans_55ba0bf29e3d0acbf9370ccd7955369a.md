
## 测试 Samba 配置

在对 **smb.conf** 文件进行修改后，你可以使用 **testparm** 程序来检查条目是否正确输入。**testparm** 用于检查 Samba 条目的语法和有效性。默认情况下，**testparm** 检查的是 **/etc/samba/smb.conf** 文件。如果你使用的是其他配置文件，可以将该文件作为参数传递给 **testparm**。你还可以让 **testparm** 检查特定主机是否有权访问配置文件所设置的服务。

在使用 SWAT 时，状态页面会列出你的连接和共享。在命令行中，你可以使用 **smbstatus** 命令来检查网络上当前的 Samba 连接。

要检查 Samba 服务器的实时运行情况，你可以登录到运行 Samba 服务器的 Linux 系统上的用户账户，并连接到该服务器。

## 域登录

Samba 还支持域登录，允许用户登录到网络。可以为单个用户设置登录脚本。为了配置这种 netlogon 功能，你需要在 **smb.conf** 文件中设置一个 **netlogon** 共享。以下示例取自原始的 **smb.conf** 文件。该共享包含 **netlogon** 脚本——在本例中为 **/var/lib/samba/netlogon** 目录——该目录不应可写，但应允许所有用户（包括来宾）访问：

```
[netlogon]
 comment = Network Logon Service
 path = /var/lib/samba/netlogon
 guest ok = yes
 writable = no
 share modes = no
```

Global 部分应启用以下参数：

```
domain logons = yes
```

借助 netlogon，你可以将 Samba 配置为 Linux 和 Windows 主机的身份验证服务器。需要为每个主机设置 Samba 用户名和密码。在 **smb.conf** 文件的 Global 部分，确保启用了加密密码、用户级安全性以及域登录，并且操作系统级别至少为 33：

```
[global]
 encrypt passwords = yes
 security = user
 domain logons = yes
 os level = 33
```

> **注意** 你还可以将 Samba 配置为 Windows NT 网络的主要域控制器（PDC）。作为 PDC，Samba 可以处理域登录，获取用户和组列表，并提供用户级安全性。

## 使用客户端访问 Samba 服务

连接到 SMB 网络的客户端系统可以访问 Samba 服务器提供的共享服务。Windows 客户端应能够通过 Windows 桌面上的“网上邻居”和“ Entire Network”图标自动访问共享目录和服务。对于连接到同一网络的 Linux 系统，可以使用 GNOME Nautilus 文件管理器和 KDE 文件管理器，以及专门的 Samba 客户端程序来访问 Samba 服务。

使用 Samba 的 **smbclient**（一个命令行客户端），本地 Linux 系统可以连接到 Samba 服务器上的共享目录并传输文件，还可以运行 shell 程序。使用带有 `-t cifs` 选项的 **mount** 命令，可以将 Samba 服务器上的目录挂载到 Linux 客户端上的本地目录。**cifs** 选项会调用 **mount.cifs** 来挂载目录。

### 从 GNOME 访问 Windows Samba 共享

你可以使用 Nautilus（GNOME 文件管理器）来访问你的 Samba 共享。你可以打开“我的计算机”图标，然后打开“网络”图标。这将显示你网络中的图标。“Windows 网络”图标将包含你的 Windows 主机所属的 Windows 工作组。打开“Windows 网络”图标将列出你的 Windows 网络组，例如 **WORKGROUP**。打开 Windows 组图标将列出该组中的主机。这些将显示共享 Windows 主机的图标。点击主机图标将列出其上所有的共享资源。以下步骤用于访问你的 Windows 共享：

1. 点击“我的计算机”以打开带有“网络”图标的窗口。
2. 点击“网络”图标以打开带有“Windows 网络”图标的窗口。
3. 点击“Windows 网络”图标以列出你的 Windows 网络组，例如工作组。
4. 点击工作组图标以列出你所有的 Windows 主机。

或者，你可以以浏览器模式启动 Nautilus 并输入 **smb:** 协议，以显示所有 Samba 和 Windows 网络，从而可以访问 Samba 和 Windows 共享。

### smbclient

**smbclient** 工具像 FTP 一样工作，用于使用 SMB 协议访问系统。与可以访问其他 FTP 服务器或 Unix 系统的 FTP 客户端不同，使用 **smbclient** 可以访问 SMB 共享服务，无论是位于 Samba 服务器上还是 Windows 系统上。许多 **smbclient** 命令与 FTP 类似，例如使用 **mget** 传输文件或使用 **del** 删除文件。**smbclient** 程序提供了多个用于查询远程系统以及连接它的选项。有关选项和命令的完整列表，请参阅 **smbclient** 的 Man 手册页。**smbclient** 程序接受服务器名称以及你想要在该服务器上访问的服务作为参数。服务器名称前有两个斜杠，并且使用一个斜杠将其与服务分开。服务可以是任何共享资源，如目录或打印机。服务器名称是其 NetBIOS 名称，可能与 IP 名称相同也可能不同。例如，要指定名为 **turtle.mytrek.com** 的服务器上的 **myreports** 共享目录，请使用 //turtle.mytrek.com/myreports。如果需要指定路径名，Windows 文件使用反斜杠，Unix/Linux 文件使用正斜杠：
`//server-name/service`

你还可以提供访问该服务的密码。将其作为参数输入在服务名称之后。如果你不提供密码，系统会提示你输入。

### 使用 smbclient 访问共享

然后你可以添加几个选项来访问共享，例如远程用户名或可用服务列表。使用 `-I` 选项，你可以使用 IP 地址来指定系统。使用 `-U` 选项和登录名来指定你想在远程系统上使用的远程登录名。如果需要密码，请在密码前加上 `%`。使用 `-L` 选项，你可以获取服务器提供的服务列表，例如共享目录或打印机。以下命令将列出主机 **turtle.mytrek.com** 上可用的共享：

```
smbclient -L turtle.mytrek.com
```

要访问远程系统上的特定目录，将该目录作为 **smbclient** 命令的参数输入，后跟任意选项。对于 Windows 文件，路径名使用反斜杠；对于 Unix/Linux 文件，使用正斜杠。连接后，会显示一个 SMB 提示符，你可以使用 **get** 和 **put** 等 smbclient 命令来传输文件。**quit** 或 **exit** 命令将退出 smbclient 程序。在以下示例中，smbclient 使用 **dylan** 登录名访问 **turtle.mytrek.com** 系统上的 **myreports** 目录：

```
smbclient //turtle.mytrek.com/myreports -I 192.168.0.1 -U dylan
```

在大多数情况下，你可以简单地使用服务器名称来引用服务器，如下所示：

```
smbclient //turtle.mytrek.com/myreports -U dylan
```

如果你正在访问 Samba 服务器上特定账户的主目录，你可以简单地指定 **homes** 服务。在下一个示例中，用户在被提示输入该账户的密码后，访问 Samba 服务器上 **aleina** 账户的主目录：

```
smbclient //turtle.mytrek.com/homes -U aleina
```

你还可以使用 smbclient 访问位于 Windows 客户端上的共享资源。指定 Windows 客户端的计算机名称及其共享文件夹。在下一个示例中，用户访问名为 **lizard** 的 Windows 客户端上的 **windata** 文件夹。该文件夹被配置为允许任何人访问，因此用户在密码提示符处只需按 ENTER 键即可。

```
$ smbclient //lizard/windata
```

登录成功后，你可以执行 smbclient 命令来管理文件和更改目录。可以使用 `!` 运算符执行 shell 命令。要传输文件，你可以使用 **mget** 和 **mput** 命令，就像在 FTP 程序中那样使用。

