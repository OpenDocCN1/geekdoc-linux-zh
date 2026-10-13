
## 其他示例段落

要了解更多关于 Samba 的信息，检查共享目录的其他段落可能会有所帮助。以下示例包含在 Samba 的早期 Red Hat 版本中。虽然它们未包含在 Samba 的注释中，但仍可包含在 smb.conf 配置文件中，因此至少在学习目的上仍然有用。

> 考试提示
> 
> RHCE 目标规定需要“提供适合团队协作的网络共享”。

例如，以下 /tmp 目录的共享可以提供一个公共位置供用户共享下载的文件。如果启用，所有用户（public = yes）都可获得对此共享的写访问权限（read only = no）。

```
# This one is useful for people to share files
;[tmp]
; comment = Temporary file space
; path = /tmp
; read only = no
; public = yes
```

此段落为 Fred 的专属使用配置一个目录。它允许该用户通过 Samba 独占访问他的主目录。路径的更好位置应在 /home 目录内。

```
# A private directory, usable only by fred. Note that fred
# requires write access to the directory.
;[fredsdir]
; comment = Fred's Service
; path = /usr/somewhere/private
; valid users = fred
; public = no
; writable = yes
; printable = no
```

以下段落与 [tmp] 共享略有不同。连接后，唯一连接的用户是访客。除非您已配置访客用户，否则默认为名为 nobody 的用户。

```
# A publicly accessible directory, read/write to all users. Note
that all files created in the directory by users will be owned
by the default user, so any user with access can delete any
other user's files. Obviously this directory must be writable
# by the default user. Another user could of course be specified,
# in which case all files would be owned by that user instead.
;[public]
; path = /usr/somewhere/else/public
; public = yes
; only guest = yes
; writable = yes
; printable = no
```

最后，这是在用户私有组方案上的另一个变体，可创建组目录。与 [public] 段落不同，此共享为私有。

```
# The following two entries demonstrate how to share a directory so
# that two users can place files there that will be owned by the
# specific users. In this setup, the directory should be writable
# by both users and should have the sticky bit set on it to prevent
# abuse. Obviously this could be extended to as many users as required.
;[myshare]
; comment = Mary's and Fred's stuff
; path = /usr/somewhere/shared
; valid users = mary fred
; public = no
; writable = yes
; printable = no
; create mask = 0765
```

## 让 Samba 加入域

如果您已配置 Samba 服务器，且它不是网络的 DC，则可能需要将其配置为域的成员。为此，您可以在网络的 DC 上配置一个账户。只要该网络上有一个域，就可以使用以下命令轻松完成：

```
# net rpc join -U root
```

如果有多个域可用，请在 net rpc join -S DC -U root 命令中将 DC 替换为控制器的名称。这假设名为 root 的用户是 DC 上的管理员用户。然而，由 Microsoft Windows 计算机管理的域上的管理员用户是 administrator。如果命令成功，它会提示输入该用户在远程 DC 上的密码。结果是在 DC 的用户数据库中为本地计算机添加一个账户。

## Samba 用户数据库

您可以在网络上的 Microsoft Windows 和启用 Samba 的 Linux 计算机上设置相同的用户名和密码。然而，这并不总是可行，尤其是在存在预先存在的数据库时。在这种情况下，您可以设置一个 Samba 用户和密码数据库，使其对应于网络上当前的 Microsoft 用户名和密码。模板可在 /etc/samba/smbusers 中获得，如果在 smb.conf 文件中添加以下条目，则会生效：

```
username map = /etc/samba/smbusers
```

如果您熟悉命令行界面，使用 smbpasswd 命令设置 Samba 用户是最快的方法。请记住，您只能从 Linux 计算机上的有效账户创建新的 Samba 用户。

然而，您可以在 Linux 系统上不具有登录权限的情况下配置此类账户。例如，以下命令在没有有效登录 shell 的情况下添加了指定的用户：

```
# useradd winuser1 -s /sbin/nologin
```

然后您可以使用 smbpasswd -a winuser1 命令为该用户配置 Samba 密码。smbpasswd 命令功能强大；它包含许多有用的开关，描述于表 15.4 中。

表 15.4
| smbpasswd 开关 | 描述 |
|---|---|
| -a username | 将指定的用户名添加到数据库中。 |
| -d username | 禁用指定的用户名；从而禁用该密码在 Microsoft 网络中的使用。 |
| -e username | 启用指定的用户名；与 -d 相反。 |
| -r computername | 允许在远程计算机上更改 Windows 或 Samba 密码。通常与 -U 一起使用。 |
| -U username | 通常在指定 -r 开关时更改远程计算机上的用户名。 |
| -x username | 从数据库中删除指定的用户名。 |

身份验证数据库的位置取决于 passdb backend 指令的值。如果设置为 smbpasswd，您将在 /etc/samba/smbpasswd 文件中找到它。如果设置为 tdbsam，您将在 /var/lib/samba/private 目录中的 passdb.tdb 文件中找到它。要读取当前用户列表，请运行以下命令：

```
# pdbedit -L
```

要为 Linux 和 Microsoft 计算机配置不同的用户名和密码，您需要直接将它们编辑到 /etc/samba/smbusers 文件中；或者，可以使用 SWAT 配置此类用户。

## 创建公共共享

有了这些信息，您现在应该知道如何为整个网络创建公共访问共享。为本章目的，创建 /home/PublicShare 目录。以下 /etc/samba/smb.conf 配置文件中的示例段落反映了一个对所有用户可用的目录。

```
[PublicShare]
    comment = Shared Public Directory
    path = /home/PublicShare
    writable = yes
    browseable = yes
    guest ok = yes
```

但这种安全级别可能不合适。例如，假设以下限制是期望的：

- 对 [PublicShare] 的访问应仅限于具有常规本地 Linux 账户的用户（或基于远程身份验证数据库（如 LDAP）可在本地登录的用户）。
- 拒绝访客用户和其他人的访问。
- 允许本地 example.com 域中的所有用户访问。
- 拒绝来自可疑计算机（如 outsider1.example.org）的所有用户访问。

要实现这一点，请更改此段落中的最后一个命令。由于 guest ok = no 是默认值，您只需删除 guest ok = yes 指令即可。要为给定域中的所有用户提供访问权限，请添加以下命令：

```
hosts allow = .example.com
```

要拒绝该网络上特定计算机的访问，您可以添加 EXCEPT；例如，以下行专门将指定的 evil.example.com 系统从列表中排除：

```
hosts allow = .example.com EXCEPT evil.example.com
```

另外，如果该域位于 192.168.122.0 网络上，以下任一指令都支持该网络上所有系统的访问：

```
hosts allow = 192.168.122.
hosts allow = 192.168.122.0/255.255.255.0
```

您可以使用如下命令专门拒绝计算机的访问：

```
hosts deny = evil.example.com
```

另外，您可以用与 hosts allow 指令相同的格式替换 IP 地址。您已在 Samba smb.conf 配置文件中定义了共享属性。但您需要使用以下命令修改与共享关联的目录：

```
# chmod 1777 /home/PublicShare
```

777 目录权限字符串前面的数字 1 被称为“粘滞位”。该粘滞位允许任何用户在目录中执行任何操作，这是 777 权限值的功劳。但此类权限仅限于特定用户创建的文件。否则，任何用户都可以删除或重命名 /home/PublicShare 目录中的任何文件，而不管文件的所有者是谁。

另外，权限仅限于组成员的目录可能具有 2770 权限，其中设置了 SGID 位，并向拥有该目录的组成员授予完全权限。

## 练习 15-1

## 配置 Samba 主目录共享

在本练习中，您将了解基本的主目录共享。您至少需要两台计算机，其中一台应为 Samba 服务器。另一台可以是 Linux 或 Microsoft Windows 工作站。您将从工作站连接到 Samba 服务器并访问 Samba 服务器上主目录中的文件。
