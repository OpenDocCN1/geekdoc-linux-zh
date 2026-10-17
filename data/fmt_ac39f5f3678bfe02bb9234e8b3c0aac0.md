
```ini
#----------------------------------------------------- Global Settings --------------------------------------------------
[global]

# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = NASH

# server string is the equivalent of the NT Description field
server string = Linux Samba Server

# This option is important for security. It allows you to restrict
# connections to machines which are on your local network.
hosts allow = 192.168.1. 127.

# if you want to automatically load your printer list rather
# than setting them up individually then you'll need this
printcap name = /etc/printcap
load printers = yes

# this tells Samba to use a separate log file for each machine
# that connects
log file = /var/log/samba/log.%m

# Put a capping on the size of the log files (in Kb).
max log size = 50

# Security mode. Most people will want user level security. See
# security_level.txt for details.
security = user

# Most people will find that this option gives better performance.
# See speed.txt and the manual pages for details
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192

# Browser Control Options:
# set local master to no if you don't want Samba to become a master
# browser on your network. Otherwise the normal election rules apply
local master = no

# WINS Server - Tells the NMBD components of Samba to be a WINS Client
#	Note: Samba can be either a WINS Server, or a WINS Client, but NOT both
wins server = 192.168.1.12

# DNS Proxy - tells Samba whether or not to try to resolve NetBIOS names
# via DNS nslookups. The built-in default for versions 1.9.17 is yes,
# this has been changed in version 1.9.18 to no.
dns proxy = no
```

下一节设置目录的共享。这些以方括号中的共享名称开始，例如`[homes]`。可选的注释行设置浏览网络时显示的注释。`browseable`配置选项指定该共享是否会在Microsoft网络的“网上邻居”中显示。`path`命令设置要共享的目录。

```ini
#Share Definitions

[documents]
	comment = Our Documents
	browseable = yes
	writable = yes
	path = /var/docs
```

接下来，示例展示了如何共享打印机。`path`变量指向打印队列目录。`guest ok`命令用于启用或禁用来宾访问。由于`writable`命令的限制，该目录不可写，但由于`printable`命令的存在，它被用于打印。

```ini
# NOTE: If you have a BSD-style print system there is no need to
# specifically define each individual printer
[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = no
# Set public = yes to allow user 'guest account' to print
    guest ok = no
    writable = no
    printable = yes
```

表16-23列出了`smb.conf`文件中的许多配置选项。

**表 16-23 常见的 `smb.conf` 条目**

| 条目 | 功能 |
| :--- | :--- |
| `workgroup = <name>` | 系统所属的工作组或 `Windows NT` 域名。 |
| `server string = <description>` | 当 `Windows` 客户端浏览时显示的描述字段。 |
| `hosts allow = <hosts>` | 允许连接到 `Samba` 共享的主机列表。您可以指定主机或使用通配符（如 `4.18`），后者指定 `4.18.0.0` 网络中的任何主机。也可以使用 `EXCEPT` 关键字来限制特定主机。 |
| `guest account = <account>` | 应用权限的本地来宾账户。 |
| `security = <type>` | 系统使用的安全类型。可以设置为 `share`、`user`、`server` 和 `domain`。 |
| `password server = <server_name>` | 如果选择了服务器安全类型，则会检查此服务器进行身份验证。 |
| `encrypt passwords = yes/no` | 某些配置要求密码必须加密。设置错误会导致连接失败。 |
| `username map = <file>` | 远程用户名可以映射到本地 `Linux` 用户。 |
| `interfaces = <ip addresses>` | 要使用的网络接口。 |
| `local master = yes/no` | 启用或禁用 `Linux` 系统成为网络上的主浏览器（`Master Browser`）。 |
| `domain master = yes/no` | 允许 `Linux` 系统成为网络的域主浏览器（`Domain Master Browser`）。如果您有 `Windows NT` 域控制器，请勿使用此项。 |
| `preferred master = yes/no` | 在选举中启用首选主浏览器状态。 |
| `domain controller = <DC name>` | 本地 `Windows NT` 域控制器的名称。 |
| `wins support = yes/no` | 启用或禁用 `WINS` 服务器功能。 |
| `wins server = <ip address>` | 启用 `WINS` 客户端功能。 |

![](img/96d9ccd181675a8ae8b6a1146c919d2b_678_0.png)

**考试提示**

`smb.conf`中的`wins server`命令启用了`nmbd`中的名称解析客户端。

`/etc/smb.conf`文件底部列出了共享目录，以及`browsable`和`comment`等选项。

#### 管理 Samba

`Samba`通过脚本启动，通常不通过`inetd`运行，尽管这是`Debian`的默认设置。`Red Hat`使用以下脚本：

```
/etc/rc.d/init.d/smb start/stop/restart/status
```

`Debian`使用以下内容：

```
/etc/init.d/samba start/stop/reload/restart/force-reload
```

`Samba`套件包含一个名为`testparm`的工具，用于检查配置文件中的语法错误。以下是`testparm`的一个输出示例。
