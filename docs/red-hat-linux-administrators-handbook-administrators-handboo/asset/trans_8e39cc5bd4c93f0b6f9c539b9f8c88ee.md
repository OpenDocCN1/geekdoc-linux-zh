
如果您希望打印机列表出现在浏览器列表中，请在前面的配置中将 browseable 参数设置为 yes。同样，如果您希望允许访客账户使用打印机，请在 [printers] 配置中将 guest ok 设置为 yes。

这就是设置所有打印机所需的一切。然而，如果您希望将一台或多台打印机私下提供给一个或多个用户，您可以为这些用户中的每个用户指定一个单独的节。例如，如果我想为名为 bigboss 的用户创建对私有打印机（fancyjet）的访问权限，我可以创建如下配置：

```
[fancyjet]
comment = Big Boss Only Printer
valid users = bigboss
path = /home/bigboss/fancyjet
guest ok = no
browseable = no
writable = no
printable = yes
```

valid users 参数使您能够指定一个由空格分隔的用户列表，这些用户可以访问打印机。

修改并测试 /etc/smb.conf 文件后，重新启动 Samba 服务，然后您应该能够从 Windows 计算机访问 Linux 打印机。

## 使用交互式 Samba 客户端

Samba 包附带一个名为 smbclient 的程序，可让您交互式地访问 Samba 资源。例如，如果您想从 Linux 系统访问 Windows 系统上的磁盘共享，请按如下方式使用 smbclient 程序进行访问：

```
smbclient //WINDOWS-SERVER/resource -U username -P password
```

在下面的示例中，smbclient 用于以用户 kabir 的身份访问 PLUTO 上的 C 驱动器：

```
smbclient //PLUTO/c -U kabir -P foobar
```

如果身份验证成功（换句话说，PLUTO 允许连接），smbclient 会显示类似 FTP 客户端的提示，并允许您执行许多 FTP 客户端命令。随时键入 help 或 ? 可提供有关命令的更多信息。

您可以使用 smbclient 列出远程计算机上可用的 Samba 资源。在下面的示例中，-L 选项指定使用用户名 kabir 进行查询的 Samba 服务器：

```
smbclient -L reboot -U kabir
```

示例输出如列表 11-2 所示。

### 列表 11-2 smbclient 示例输出

```
Server time is Sat Feb 13 19:48:03 1999
Timezone is UTC-8.0
Password:
Domain=[NITEC] OS=[Windows NT 4.0] Server=[NT LAN Manager 4.0]
security=user

Server=[REBOOT] User=[] Workgroup=[NITEC] Domain=[]
```

| 共享名 | 类型 | 注释 |
|-----------|------|---------|
| ADMIN$ | Disk | 远程管理 |
| C | Disk | PLUTO 上的 C 驱动器 |
| C$ | Disk | 默认共享 |
| F | Disk |  |
| home | Disk |  |
| IPC$ | IPC | 远程 IPC |
| Okidata0 | Printer | Okidata OL-600e |
| print$ | Disk | 打印机驱动程序 |
| sheila | Disk |  |
| TEMP | Disk |  |

### 列表 11-2 继续

此机器有一个浏览列表：

| 服务器 | 注释 |
|-------- | -------- |
| PICASO | Picaso Samba 服务器 |
| PLUTO |  |
| R2D2 | Nitec 笔记本电脑 (r2d2) |
| REBOOT |  |

此机器有一个工作组列表：

| 工作组 | 主服务器 |
|---------- | -------- |
| NITEC | PLUTO |

正如您所见，smbclient 程序可用于确定从其他 Samba 兼容系统共享了哪些资源。

smbclient 程序还允许您向已启用此服务的 Windows 计算机发送 Windows 弹出消息。

例如，当您运行

```
smbclient -M reboot
```

smbclient 使您能够键入文本消息，它将这些消息作为弹出消息显示在目标 Windows 计算机上。

## 保护您的 Samba 服务器

如果使用正确，Samba 可以将混合环境（Linux/Windows）转变为更顺畅的计算环境。然而，与其他任何有用的服务一样，当 Samba 配置错误时，它可能成为安全漏洞的潜在来源。如果您的 Samba 服务器连接到 Internet，此问题尤其重要。我建议您不要将 Samba 服务器连接到 Internet 或通过 Internet 启用 Samba 服务。本节讨论您可以采取的几项安全措施，以降低涉及 Samba 的风险。

本章前面的一节回顾了如何在 Windows 9x 和 NT 系统的较新版本上启用明文密码。这对这些系统来说效果很好，但在存在非法 TCP/IP 数据包嗅探器风险的局域网或广域网环境中可能不合适。换句话说，如果您认为您的网络可能容易受到数据包嗅探器的攻击，请实施加密密码。SMB 协议允许的基于加密密码的身份验证永远不会在 Samba 客户端和服务器之间传输任何密码。这确保了更高程度的安全性，因此在安全和保密性至关重要的高风险场景中非常理想。存在两种使用加密密码的方法，接下来都会进行描述。

### 使用 Windows NT Server 作为密码服务器

Windows NT Server 默认情况下可以提供加密密码服务。因此，如果您的网络上有 Windows NT Server，请考虑将其作为您的密码服务器。您可以将所有用户账户集中在 Windows NT Server 上，以便使用加密密码启用 Samba 服务。要将 Windows NT Server 用作加密密码服务器，请执行以下操作：

- 1. 为每个需要 Samba 访问的用户创建一个 Windows NT Server 账户。
- 2. 修改 /etc/smb.conf 文件，使 password server 参数设置为 Windows NT Server 的名称。另请将 security 参数设置为 server。
- 3. 运行 testparm 命令，以确保 /etc/smb.conf 文件中的所有配置行在语法上正确。
- 4. 重新启动 Samba 服务。

要测试您的新配置，请使用其中一个 Windows NT Server 用户账户访问 Samba 服务器。

### 在您的 Samba 服务器上使用加密密码

Red Hat 随附的 Samba 包已预编译了加密密码支持，因此您无需下载 Samba 源代码并使用加密密码支持进行编译。要启用加密密码，请执行以下步骤：

- 1. 使用 Samba 包提供的 mksmbpasswd.sh 脚本来为 /etc/passwd 创建一个替换密码文件。运行以下命令：
这将创建一个特殊密码文件，其中包含如下行：
root:x:XXXXXXXXXXXXXXX:XXXXXXXXXXXXXXX:XXXXXXXXXXXXXXX
XXXXXXXXXXXXXXX:root:/root:/bin/tcsh

- 2. 使用 smbpasswd 程序为每个用户创建加密的 Samba 密码。例如，要为名为 sheila 的用户创建加密的 Samba 密码，请运行以下命令：

- 3. 修改 /etc/smb.conf 文件，使以下行出现在 [global] 配置文件中：

- 4. 通过运行 testparm 程序测试您的新配置；如果测试成功，重新启动 Samba 服务。另一方面，如果 testparm 显示错误，请根据需要检查并修改您的配置。

```
cat /etc/passwd | mksmbpasswd.sh > /etc/smbpasswd
```

```
smbpasswd sheila
```

```
encrypt passwords = yes
```

从 Windows 系统测试 Samba 服务。如果您已修改 Windows 注册表以使用明文密码，请删除您创建的注册表项，以便可以使用加密密码。

## 使用 Apache 的 Web 服务

### 从 Internet 获取 Apache

尽管 Red Hat Linux 的官方副本附带了预构建 Apache Web 服务器的 RPM 打包版本，您仍可能希望从官方 Apache 网站 http://www.apache.org/ 下载最新版本。

如果您不在美国，从附近的 Apache 镜像站点获取 Apache 源代码和二进制文件可能会更快。使用 URL http://www.apache.org/dyn/closer.cgi 找到您附近的良好镜像站点。本讨论假设您从官方 Apache 网站获取软件。软件（源代码和二进制文件）可以在 http://www.apache.org/dist/ 找到。

您将看到许多使用各种压缩程序归档的最新 Apache 发行版版本，例如以下内容：

- Apache_1.3.9.tar.gz
- Apache_1.3.9.tar.Z

这些是 Apache 版本 1.3.9 源分发的示例。唯一的区别在于其大小，这是由于使用的压缩技术不同而导致的。下载其中一个文件。无论您下载哪种格式，您都需要 tar 实用程序以及 gunzip 或 gzip 实用程序来解压缩文件。例如，要在我的 Red Hat 5.2 系统上解压缩 Apache 1.3.9.tar.gz 文件，我使用以下命令：

```
tar xzvf apache_1.3.9.tar.gz
```
