

# SAMBA 简介

# 更多信息

本地 Samba/swat 主页提供了指向本地 Samba 文档的链接（第 804 页）
文档路径:/usr/share/samba-doc-*

Web Samba: www.samba.org（邮件列表、文档、下载等）
CIFS: www.samba.org/cifs

HOWTO 非官方 Samba HOWTO: hr.uregon.edu/davidrl/samba.html
Samba 文档集：将浏览器指向 /usr/share/doc/samba-doc/htmldocs/index.html；如果你安装了 samba-doc-pdf 软件包，请查看 /usr/share/doc/samba-doc-pdf。

# 注意事项

防火墙：服务器通常使用 UDP 端口 137 和 138 以及 TCP 端口 139 和 445。如果 Samba 系统正在运行防火墙，您需要开放这些端口。使用 gufw（第 876 页），通过设置允许 samba 服务的策略来开放这些端口。

共享（Share）：在 Samba 中，导出的目录层次结构被称为共享。

映射共享（Mapping a share）：映射共享的术语等同于 Linux 术语挂载（mounting）目录层次结构。

Samba：名称源自 SMB（第 1172 页），SMB 是 Windows 文件和打印机共享的原生协议。

swat：你必须使用 root 密码通过 swat 来更改 Samba 配置；请参阅第 431 页说明。

# SAMBA 用户、用户映射和密码

为了让 Windows 用户访问 Linux 系统上的 Samba 服务，该用户必须提供 Windows 用户名和 Samba 密码。在某些情况下，Windows 会为你提供用户名和密码。也可以使用其他方法进行身份验证。例如，Samba 可以使用 LDAP（第 1156 页）或 PAM（第 478 页）代替默认密码文件。请参考 Samba 文档获取有关身份验证方法的信息。

用户名：Windows 提供的用户名必须与 Linux 用户名相同，或者映射到一个 Linux 用户名。

用户映射（User maps）：你可以创建一个文件（通常命名为 /etc/samba/susers），将用户名映射到 Linux 用户名。更多信息请参阅第 811 页的用户名映射。

密码：默认情况下，Samba 使用 Linux 密码来验证用户。然而，Ubuntu 将 passdb 后端（第 809 页）设置为了 tdsams，导致 Samba 使用 Samba 数据库密码。在 smb.conf（第 807 页）中将此参数更改为 smbpasswd，使 samba 使用 Linux 密码。

# 设置 SAMBA 服务器

本节描述了如何使用 shares-admin 工具和 swat 基于浏览器的配置工具安装并配置 Samba 服务器。

# 前提条件

安装：安装以下软件包：

- samba
- samba-client
- smbfs（挂载 Windows 共享所需的唯一包）
- system-config-samba（可选）
- swat（可选，但有用）
- openbsd-inet（运行 swat 需要；作为 swat 的依赖项安装）
- samba-doc（可选文档；随 swat 安装）
- samba-doc-pdf（可选；PDF 格式的文档）

smbd 启动脚本：当你安装 samba 软件包时，dpkg postinst 脚本会将 Samba 复制并作为普通守护进程运行（而不是通过 inet），它将所有 Linux 用户复制到 Samba 用户列表中，使用加密密码设置 Samba，并启动 smbd 和 nmbd 守护进程。配置 samba 后，执行以下命令（第 434 页）重启 smbd 和 nmbd 守护进程：

```
sudo service smbd restart
smb start/running, process 4662
```

# 快速上手：使用 system-config-samba 配置 Samba 服务器

system-config-samba 工具只能设置 Samba 服务器的基本功能。然而，如果你不熟悉 Samba 并且想要快速建立一个简单的 Samba 服务器，它是最好的工具。system-config-samba 工具执行三个基本功能：配置服务器、配置用户以及设置导出到 Windows 机器的共享（目录层次结构）。

# 备份 smb.conf

在安装状态下，/etc/samba/smb.conf 文件有详尽的注释（第 807 页）。system-config-samba 工具会覆盖此文件。在首次运行此工具之前，请为 smb.conf 创建一个备份以妥善保存。

要显示 Samba 服务器配置窗口（图 23-1），请选择主菜单：系统 ⇨   ⇨ Samba，或从终端模拟器或运行应用程序窗口（ALT-F2）输入 sudo system-config-samba。打印机默认共享的。

# 设置 SAMBA 服务器 801

![](img/45ff4cd21497435daa35084a84b95d07_851_0.png)

**图 23-1** Samba 服务器配置窗口

选择菜单栏：Preferences ⇨ Server Settings 显示服务器设置选项卡（图 23-2）。将工作组（workgroup）更改为 Windows 机器正在使用的那个。根据需要更改服务器描述。点击安全（Security）选项卡并确保身份验证模式（Authentication Mode）设置为 User；你不需要指定身份验证服务器或 Kerberos 域（Kerberos Realm）。如果你使用的是 Windows 98 或更高版本，将加密密码（Encrypt Passwords）设置为 Yes。当你在访客账户（Guest Account）中指定用户名时，任何登录访客账户的用户都可以。

（注：原文此处存在多处重复文本，此处已按要求进行翻译）

选择菜单栏：Preferences ⇨ Server Settings 显示服务器设置选项卡（图 23-2）。将工作组（workgroup）更改为 Windows 机器正在使用的那个。根据需要更改服务器描述。点击安全（Security）选项卡并确保身份验证模式（Authentication Mode）设置为 User；你不需要指定身份验证服务器或 Kerberos 域（Kerberos Realm）。如果你使用的是 Windows 98 或更高版本，将加密密码（Encrypt Passwords）设置为 Yes。当你在访客账户（Guest Account）中指定用户名时，任何登录访客账户的用户都可以。

（注：原文此处存在多处重复文本，此处已按要求进行翻译）

选择菜单栏：Preferences ⇨ Server Settings 显示服务器设置选项卡（图 23-2）。将工作组（workgroup）更改为 Windows 机器正在使用的那个。根据需要更改服务器描述。点击安全（Security）选项卡并确保身份验证模式（Authentication Mode）设置为 User；你不需要指定身份验证服务器或 Kerberos 域（Kerberos Realm）。如果你使用的是 Windows 98 或更高版本，将加密密码（Encrypt Passwords）设置为 Yes。当你在访客账户（Guest Account）中指定用户名时，任何登录访客账户的用户都可以。

选择菜单栏：Preferences ⇨ Server Settings 显示服务器设置选项卡（图 23-2）。将工作组（workgroup）更改为 Windows 机器正在使用的那个。根据需要更改服务器描述。点击安全（Security）选项卡并确保身份验证模式（Authentication Mode）设置为 User；你不需要指定身份验证服务器或 Kerberos 域（Kerberos Realm）。如果你使用的是 Windows 98 或更高版本，将加密密码（Encrypt Passwords）设置为 Yes。当你在访客账户（Guest Account）中指定用户名时，任何登录访客账户的用户都可以。

