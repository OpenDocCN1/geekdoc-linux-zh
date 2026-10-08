
# 第三部分：Ubuntu 系统管理员

# 注意

如果你想让你的 Samba 服务器作为 Windows 域的域控制器 (PDC)，你还必须将 Samba 配置文件 `[Domains]` 部分的 `domain master` 设置值更改为 `yes`，并确保该条目没有被注释。在这种情况下，该条目看起来如下：

```
domain master = auto
```

这意味着，如果找不到其他域控制器，Samba 服务器将作为你网域的主域控制器，这在你的 Samba 服务器托管网域时将会发生。

本章解释了如何将 Samba 作为工作组的一部分使用，这是在家庭或小型办公（SOHO）网络中使用 Samba 的典型方式。关于设置 Samba 的信息，请参考本章“安装 Samba 服务器”章节，并查看 `/usr/share/samba-doc/Samba-3` 的在线副本。

# 注意

Windows 7 系统在执行安全方面比任何之前的 Samba 版本都做得更好。如果你想让 Windows 7 加入 Samba 域，必须运行 Samba 3.4 或更高版本，并执行 Windows 7 上的一些注册表项。请访问 www.linuxplanet.com/linuxplanet/tutorials/6911/2/ 获取详细信息。

由于此示例显示了一个小型工作组，你可能还会想要激活以下条目，让 Samba 使用 WINS（Windows NetBIOS 名称服务，本章之前讨论过），而是使用你的系统 DNS 服务器来查找主机：

```
wins support = no
resolve order = lmhosts broadcast
```

最后一条条目告诉 Samba，客户端首先在本地文件中查找主机（在 Windows 系统上），然后检查 Samba 服务器上的 `/etc/hosts` 文件，接着检查 WINS（在本情况下，WINS 被代理到本地 DNS 服务器），最后使用广播来搜索正确的主机。这种组合适用于你曾设置或使用过的每个 Samba 服务器配置。

最后，你必须定义用于识别 Samba 服务器已验证用户的安全模型。要实现这一点，请取消 Samba 配置文件中以下条目的注释：

```
security = user
```

这完成了对 Samba 文件的核心修改，使 Samba 能够与指定的工作组或域共享文件。这样对吗？

# 配置 Samba 认证

在我们章所使用的示例工作组配置中，Samba 已经预配置为执行工作组成员所需的认证类型。然而，为了能够访问共享资源，你必须能够向 Samba 服务器进行认证。Samba 维护自己的认证信息——要添加用户的登录和密码信息，必须使用 `smpasswd` 命令。在添加用户信息时，必须使用 `-a` 选项，后跟要添加的用户名。`smpasswd` 命令会提示输入密码，然后再次提示该密码以确保你输入正确。以下是添加用户 `vwh` 的示例脚本：

```
$ smbpasswd -a vwh
Password:
New SMB password:
Retype new SMB password:
```

第一个密码提示来自 sudo ，要求输入 Ubuntu 密码以便执行此特权操作。后两个是输入用户 `vwh` 的 Samba 密码。

# 注意

Samba 配置文件建议的安全级别 `security = user` 要求 Samba 用户也存在于 Ubuntu 系统的密码文件中，否则你将收到错误消息且 `smpasswd` 命令将失败。关于其他安全模型及其影响，请查看 `samba-doc` 软件包中的 `/user/share/samba-doc/html/ServerType.html` 文件。

# 使用 Samba 共享打印机和主目录

在设置工作组并创建用户后，下一个考虑的是 Ubuntu 系统上的通用资源，你希望这些资源对连接你 Samba 服务器的所有 Windows 系统可用。这些最常见的例子是打印机和用户的主目录。

Samba 配置文件 `[global]` 部分中与 Ubuntu 打印机和打印相关的条目如下，你应该确保它们没有被注释（即不是以分号开头）：

- load printers = yes
- printing = cups
- printcap name = cups

在 Samba 配置文件的后半部分，`[printers]` 部分提供了关于你的 Windows 系统如何与 Samba 服务器交互的信息。你不需要更改其中的任何内容，但供你参考，这些条目如下：

```
[printers]
comment = 所有打印机
```

```
browseable = no
path = /tmp
printable = yes
guest ok = no
read only = yes
create mode = 0700
[print$]
```

```
comment = 打印机驱动
path = /var/lib/samba/printers
browseable = yes
read only = yes
guest ok = no
```

`[printers]` 部分标识 Samba 服务器将如何处理来自 Windows 客户端的打印机识别请求和传入的打印请求，而 `[print$]` 部分将传统的 `print$` 共享名称映射到你 Linux 系统上的一个目录，你可以在那里放置特定打印机的驱动程序，这样当 Windows 客户端系统中没有这些驱动程序时，它们就可以定位并加载它们。

除了打印机之外，Ubuntu 系统上供 Windows 系统访问的最自然资源是其主目录。关于在 Ubuntu 系统上备份文件，请参考第 28 章“备份和恢复文件”。

幸运的是，Samba 配置文件已经设置好在 Ubuntu 系统上共享主目录，只要你的 Linux 和 Windows 用户名匹配。以下是该配置文件的部分：

```
[homes]
comment = 主目录
browseable = no
read only = yes
create mask = 0700
directory mask = 0700
```

从此配置摘录可以看出，主目录默认共享但不可写。这很不方便，因此你希望将配置文件中的 `read only` 条目更改为 `no`，如下：

```
read only = no
```

这允许用户读写他们的主目录。

# 提示

如果你的 Windows 和 Ubuntu 用户具有不同的登录名，可以通过在 `/etc/samba/smusers` 文件中创建相应的条目来关联它们。该文件中的格式为 `UnixLogin = WindowsLogin`。例如，映射 Ubuntu 用户 `vwh`：

```
vwh = bill.vonhagen
```

如果你的 Windows 登录名包含一个或多个空格，必须在该文件中用引号括起来。在实践中，我建议保持 Ubuntu 和 Samba 登录一致，但如果你有不同的命名规范可以使用可以使用文件。

# 验证 Samba 配置文件

在修改 Samba 配置文件后，你应该验证是否违反了文件语法。如果 Samba 配置包含无效条目，Samba 会显示错误消息且不会加载。如果不是 Samba 服务器还提供了一个测试 Samba 配置文件有效性的工具，并能识别发现的错误位置。该工具是 `testparm`，你可以无参数运行它来测试默认 Samba 配置文件 `/etc/samba/sm.conf`。运行 `testparm` 工具的输出如下：

```
testparm
Load smb config files from /etc/samba/sm.conf
Processing section "homes"
Processing section "printers"
Processing section print$
Loaded services OK.
* WARNING: passdb add explicit = yes is deprecated
Server role: ROLE_STANDALONE
Press enter to see a dump of service definitions
```

如前面的示例所示，在显示某些通用信息后，`testparm` 工具提示你按回车键以查看 Samba 服务器配置提供的服务的详细信息。以下是这些详细信息的示例：

```
[global]
workgroup = WVH
server string = %h server (Samba, Ubuntu)
obey pam restrictions = Yes
passdb backend = tdbsam, guest
syslog = 0
log file = /var/log/samba/log.%m
max log size = 1000
```
