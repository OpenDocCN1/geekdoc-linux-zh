
## 变量替换

对于分配给参数的字符串值，您可以加入替换运算符。这提供了在指定可能依赖于上下文的值（例如用户名）时更大的灵活性。例如，假设某项服务需要为每个登录的用户使用单独的目录。此类目录的路径可以使用 %u 变量指定，该变量会替换为当前用户的名称。字符串 path = /tmp/%u 对于 justin 用户将变为 path = /tmp/justin，对于 dylan 用户将变为 /tmp/dylan。表 37-3 列出了一些更常见的替换变量。

表 37-3：Samba 替换变量

| Variable | Description |
|---|---|
| %S | 当前服务的名称 |
| %P | 当前服务的根目录 |
| %u | 当前用户的用户名 |
| %H | 用户的主目录 |
| %h | Samba 运行的 Internet 主机名 |
| %m | 客户端计算机的 NetBIOS 名称 |
| %L | 服务器的 NetBIOS 名称 |
| %M | 客户端计算机的 Internet 名称 |
| %I | 客户端计算机的 IP 地址 |

## 测试 Samba 配置

在您对 `smb.conf` 文件进行更改后，您可以使用 testparm 程序查看条目是否正确输入。testparm 检查 Samba 条目的语法和有效性。默认情况下，testparm 检查 `/etc/samba/smb.conf` 文件。如果您使用不同的文件作为配置文件，可以将其作为参数指定给 testparm。您还可以让 testparm 检查特定主机是否可以访问配置文件设置的服务。

使用 SWAT，状态页面将列出您的连接和共享。从命令行，您可以使用 `smbstatus` 命令检查网络上当前 Samba 连接的情况。

要检查 Samba 服务器的实时运行情况，您可以登录运行 Samba 服务器的 Linux 系统上的用户帐户并连接到服务器。

## 域登录

Samba 还支持域登录，从而用户可以登录到网络。可以为单个用户设置登录脚本。要配置此类 netlogon 功能，您需要在 smb.conf 文件中设置一个 netlogon 共享。以下示例取自原始 smb.conf 文件。此共享保存 netlogon 脚本，在此情况下为 /home/netlogon 目录——该目录不应可写但应可被所有用户访问（Guest OK）：

```
[netlogon]
comment = Network Logon Service
path = /home/netlogon
guest ok = yes
writeable = no
share modes = no
```

Global 部分将启用以下参数：

```
domain logons = yes
```

使用 netlogon，您可以将 Samba 配置为 Linux 和 Windows 主机的身份验证服务器。每个主机都需要设置 Samba 用户名和密码。在 smb.conf 文件的 Global 部分中，请务必启用加密密码、用户级安全性以及域登录，以及 33 或更高的操作系统级别：

```
[global]
encrypt passwords = yes
security = user
domain logons = yes
os level = 33
```

**Note** 您还可以将 Samba 配置为 Windows NT 网络的主域控制器（PDC）。作为 PDC，Samba 可以处理域登录、检索用户和组列表，并提供用户级安全性。

## 使用客户端访问 Samba 服务

连接到 SMB 网络的客户端系统可以访问 Samba 服务器提供的共享服务。Windows 客户端应能够通过 Windows 桌面上的“网络邻居”和“整个网络”图标自动访问共享目录和服务。对于连接到同一网络的其他 Linux 系统，可以使用特殊 Samba 客户端程序访问 Samba 服务。使用 smbclient，本地 Linux 系统可以连接到 Samba 服务器上的共享目录并传输文件，以及运行 shell 程序。使用 smbmount，可以将 Samba 服务器上的目录挂载到 Linux 客户端的本地目录。

Note 有多个 Samba 浏览器客户端可用于 GNOME 和 KDE。对于 KDE，您可以使用 Konba2（可从 apps.kde.com 下载）。对于 GNOME，您可以使用 Gnomba。

### smbclient

smbclient 实用程序像 FTP 一样操作以使用 SMB 协议访问系统。而使用 FTP 客户端您可以访问其他 FTP 服务器或 Unix 系统，使用 smbclient 您可以访问 Samba 服务器或 Windows 系统上的 SMB 共享服务。许多 smbclient 命令与 FTP 相似，例如 mget，用于传输文件或 del，用于删除文件。smbclient 程序有多个选项用于查询远程系统以及连接到它。有关选项和命令的完整列表，请参阅 smbclient 手册页。smbclient 程序以服务器名称和您要在该服务器上访问的服务作为参数。双斜杠位于服务器名称之前，单斜杠将其与服务分隔开。服务可以是任何共享资源，例如目录或打印机。服务器名称是其 NetBIOS 名称，可能与 IP 名称相同也可能不同。例如，要指定名为 turtle.mytrek.com 的服务器上的 myreports 共享目录，请使用 //turtle.mytrek.com/myreports。如果必须指定路径名，请对 Windows 文件使用反斜杠，对 Unix/Linux 文件使用正斜杠：

```
//server-name/service
```

您还可以提供访问服务的密码。将其作为服务名称后的参数输入。如果您未提供密码，将提示您输入。

Note 您还可以使用 Nautilus（GNOME 文件管理器）访问 Samba 共享。使用 smb: 协议，如 smb://lizard/windata。仅输入 smb: 将显示所有 Samba 共享。

### 使用 smbclient 访问共享

然后您可以添加多个选项来访问共享，例如远程用户名或可用的服务列表。使用 -I 选项，您可以使用其 IP 地址指定系统。您使用 -U 选项和登录名来指定要在远程系统上使用的远程登录名。如果需要密码，请附加 % 与密码。使用 -L 选项，您可以获取服务器提供的服务列表，例如共享目录或打印机。以下命令将列出主机 turtle.mytrek.com 上可用的共享：

```
smbclient -L turtle.mytrek.com
```

要访问远程系统上的特定目录，请将目录作为 smbclient 命令的参数输入，后跟任何选项。对于 Windows 文件，您对路径名使用反斜杠，对于 Unix/Linux 文件您使用正斜杠。连接后，将显示 smb 提示符，您可以使用 smbclient 命令例如 get 和 put 传输文件。quit 或 exit 命令退出 smbclient 程序。在以下示例中，smbclient 使用 dylan 登录名访问 turtle.mytrek.com 系统上的 myreports 目录：

```
smbclient //turtle.mytrek.com/myreports -I 192.168.0.1 -U dylan
```

在大多数情况下，您可以简单地使用服务器名称来引用服务器，如下所示：

```
smbclient //turtle.mytrek.com/myreports -U dylan
```

如果您正在访问 Samba 服务器上特定帐户的主目录，您可以简单地指定 homes 服务。在下一个示例中，用户在被提示输入该帐户密码后访问 Samba 服务器上 aleina 帐户的主目录：

```
smbclient //turtle.mytrek.com/homes -U aleina
```

您还可以使用 smbclient 访问位于 Windows 客户端上的共享资源。指定 Windows 客户端的计算机名称以及其共享文件夹。在下一个示例中，用户访问名为 lizard 的 Windows 客户端上的 windata 文件夹。该文件夹配置为允许任何人访问，因此用户只需在密码提示时按 ENTER 键。

```
$ smbclient //lizard/windata
added interface ip=192.168.0.2 bcast=192.168.0.255 nmask=255.255.255.0
Got a positive name query response from 192.168.0.3 ( 192.168.0.3 )
Password:
Domain=[WORKGROUP] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
smb: \> ls
. D 0 Sat Sep 7 17:29:19 2002
.. D 0 Sat Sep 7 17:29:19 2002
hi A 10 Sat Sep 7 17:29:27 2002
mynewdoc.doc A 0 Sat Sep 7 16:59:13 2002
39997 blocks of size 1048576. 39930 blocks available
smb: \> mget hi
Get file hi? y
getting file hi of size 10 as hi (1.22069 kb/s) (average 1.2207 kb/s)
smb: \> quit
```

### smbclient 命令

登录后，您可以执行 smbclient 命令来管理文件和更改目录。可以使用 ! 运算符执行 Shell 命令。要传输文件，您可以使用 mget 和 mput 命令，就像在 FTP 程序中使用一样。recurse 命令使您能够打开递归以一次复制整个子目录。您可以使用此处称为掩码的文件匹配运算符来选择特定集合的文件。文件匹配（掩码）运算符为 *、[] 和 ?（参见第 8 章）。默认掩码为 *，匹配所有内容。以下示例使用 mget 复制所有以 .c 为后缀的文件，如 myprog.c：

```
smb> mget *.c
```

在传输期间，您可以让 smbclient 对每个单独文件提示您或简单地传输所有选定的文件。prompt 命令切换此文件提示的打开和关闭。

要访问远程系统上的特定打印机，请将打印机名称作为 smbclient 命令的参数输入，后跟任何选项。在以下示例中，smbclient 使用 dylan 登录名访问 turtle.mytrek.com 系统上的 myepson 打印机：

```
smbclient //turtle.mytrek.com/myepson -U dylan
```

连接后，将显示 SMB 提示符，您可以使用 smbclient 命令例如 print 打印文件和 printmode 指定图形或文本。在下一个示例中，用户在访问了 turtle.mytrek.com 上的 myepson 打印机后打印名为 myfile 的文件：

```
smb> print myfile
```

### smbmount

使用 smbmount 命令，Linux 或 Unix 客户端可以将共享目录挂载到其本地系统。smbmount 命令的语法与 smbclient 命令类似，其中包含许多
