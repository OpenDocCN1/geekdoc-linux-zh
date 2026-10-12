
# 第 35 章：Samba

| 应用 | 描述 |
| --- | --- |
| `smbd` | Samba 服务器守护进程，为 Samba 客户端提供文件和打印机服务 |
| `nmbd` | Samba 守护进程，提供 NetBIOS 名称解析和服务浏览器支持 |
| `smbclient` | 为 Linux 客户端提供类似 FTP 的方式访问 Samba 服务 |
| `smbmount` | Linux 客户端上的 Samba 共享目录 |
| `smbumount` | 卸载 Linux 客户端上挂载的 Samba 目录 |
| `smbpasswd` | 修改 Samba 服务器上的 SMB 加密密码 |
| `smbstatus` | 显示 Samba 网络连接当前状态 |
| `smbrun` | `smbd` 与外部程序之间的接口程序 |
| `testparm` | 测试 Samba 配置文件 `smb.conf` |
| `smbtar` | 直接将 SMB/CIFS 共享资源备份到 Unix 磁带驱动器 |
| `nmblookup` | 将 Windows PC 的 NetBIOS 名称映射到其 IP 地址 |
| `SWAT` | Samba Web 管理工具，用于通过 Web 浏览器配置 `smb.conf`；允许您使用 Web 界面创建和维护 Samba 配置文件 `smb.conf` |
| `winbind` | 使用 Windows 域提供的身份验证服务 |

表 35-1. Samba 应用

您可以使用`testparm`来测试您的 Samba 配置。`smbtar` 是一个直接将 SMB/CIFS 共享资源备份到 Unix 磁带驱动器的 shell 脚本。您使用`nmblookup`将 Windows PC 的 NetBIOS 名称映射到其 IP 地址。该软件包中还包含 Samba Web 管理工具 (`SWAT`)。它允许您使用 Web 界面创建和维护 Samba 配置文件`/etc/samba/smb.conf`。Samba 配置文件存储在`/etc/samba`目录下。

Samba 提供四种主要服务：文件和打印机服务、身份验证与授权、名称解析和服务公告。`smbd` 提供文件和打印机服务，以及这些服务的身份验证和授权。这意味着网络上的用户可以共享文件和打印机。您可以通过要求用户提供密码来控制对这些服务的访问。当用户尝试访问共享目录时，系统会提示输入密码。控制可以通过共享模式或用户模式实现。`share mode`（共享模式）为共享资源设置一个密码，然后允许任何拥有该密码的用户访问。`user mode`（用户模式）则为每个用户提供不同的密码。为此，Samba 维护了自己的独立的密码文件：`/etc/samba/smbpasswd`。

![](img/95726952b50a5b7113b49b7e63a39779_798_0.png)

# Linux：完全参考

名称解析和服务公告由`nmbd`服务器处理。名称解析将 NetBIOS 名称解析为 IP 地址。服务公告（也称为浏览）是让网络上可用服务列表对已连接的 Windows PC（以及通过 Samba 连接的 Linux PC）所感知的方式。

Samba 还包含`winbind`守护进程，它允许 Samba 服务器使用 Windows 域提供的身份验证服务。Samba 服务器不再需要维护自己的用户列表来允许访问，而是利用 Windows 域身份验证服务来验证用户。

如果您想从`www.samba.org`下载压缩包(`.tar.gz`)源码或二进制文件，归包将提取到其自己的`samba`子目录。要使用它，请在类似`/usr/local/`的软件目录中解压归包。确保将`/usr/local/samba/bin`添加到您的`PATH`中。或者，您可以将`samba/bin`文件复制到`/usr/bin`，但`nmbd`和`smbd`除外，它们应该复制到`/usr/sbin`。

# 设置 Samba

对于简单的 Samba 设置，您应该可以使用随 Linux 发行版 Samba 安装的默认`smb.conf`。然而，如果您需要进行更改，必须重启 Samba 服务器才能使更改生效。启动、停止和重启 Samba 服务器由`/etc/rc.d/init.d/smbd`管理，使用`start`、`stop`和`restart`选项。在 Mandrake 和 Red Hat 上，您可以像此处所示直接运行`smbd`脚本：

```
service smbd restart
```

在 Red Hat 上，您可以使用服务配置工具(`service`)来启动和停止 Samba，在 Mandrake 上您可以使用系统中心(`YaST`)。为了确保名称解析，您可以在`/etc/hosts`文件中输入您的主机名及其 IP 地址。在 Windows 系统上，`lmhosts`由一个 IP 地址和系统的 NetBIOS 名称组成，由微软网络已知。对于您的 Linux 系统，您可以输入 IP 地址和 Linux 系统的主机名。要测试从 Linux 系统的连接，您可以使用`smbclient`命令查询 Samba 服务器。要访问 Samba 服务器上的用户主目录，请使用 Samba 服务器的 IP 或主机名，并用`-U`选项指定要连接的用户，如下所示：

```
smbclient //mytarget/homes -U dylan
```

然后会提示您输入密码。如果客户端密码与服务器密码不同，请使用服务器密码。一旦连接，您将看到如所示的`smb`提示符。随后您可以访问用户主目录下的文件：

```
smb:
```

要为 Windows 客户端设置连接，需要指定工作组名称和密码。工作组名称是 Windows (2000, NT 和 XP) 中“网络邻域”中显示的名称。在`smb.conf`文件中，您在全局部分指定工作组条目。工作组名称应该是大写的，且长度不超过八个字符。

## 第 35 章：Samba

```
ypcat passwd | mksmbpasswd.sh > /etc/samba/smbpasswd
```

你需要更改此文件的权限，以防止未经授权的访问。`600`选项仅允许`root`用户进行读取和写入访问：

```
chmod 600 /etc/samba/smbpasswd
```

此时，`/etc/samba/smbpasswd`将包含所有当前用户的条目，密码字段为占位符。你使用`smbpasswd`命令来添加（或稍后添加）加密后的密码。要为特定用户添加密码，请带上用户名使用`smbpasswd`命令：

```
# smbpasswd dylan
New SMB Password: new-password
Repeat New SMB Password: new-password
```

用户可以使用`smbpasswd`更改自己的密码。下面的示例显示了你如何使用`smbpasswd`更改 Samba 密码。如果用户没有 Samba 密码，只需按回车键即可。

```
$ smbpasswd
Old SMB password: old-password
New SMB Password: new-password
Repeat New SMB Password: new-password
```

你还必须确保 Samba 配置为使用加密密码。将`encrypt passwords`选项设置为`yes`并指定`smb`密码文件。这些选项在`/etc/samba/smb.conf`文件中已经设置过（在后续节中描述），但它们是以注释符号`;`开头创建的。找到这些行并删除行开头的`;`：

```
encrypt passwords = yes
smb password file = /etc/samba/smbpasswd
```

你也可以使用`SWAT`来更改。在`GLOBALS`页面中，从`Encrypt Password`条目的弹出菜单中选择`Yes`。点击`Commit Changes`按钮保存更改。

务必使用以下命令重启 Samba 服务：

```
service smb restart
```

## Windows 客户端上的明文密码
