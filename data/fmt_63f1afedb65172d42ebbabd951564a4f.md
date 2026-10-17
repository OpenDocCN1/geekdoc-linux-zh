
[global]

`workgroup` = `WVH`

```
该条目解释了我的机器属于名为 `WVH` 的 Windows 工作组或域。在这个 SOHO 示例中，`workgroup` 基本上是透明的——这里的关键在于你的 Samba 服务器要么是你所在地正在使用的工作组/域的成员，或者是定义你希望它所属的域的主控制器。
```

如果你想让 Samba 服务器作为 Windows 域的主域控制器 `PDC`，你还必须更改 Samba 配置文件 `[Domains]` 部分中 `domain master` 设置的值，并确保该条目没有被注释掉。在这种情况下，该条目看起来像这样：

```
domain master = auto
```

这意味着如果找不到域控制器，Samba 服务器将作为你域的主域控制器，当你的 Samba 服务器托管了该域时，情况就会是这样。

本章解释了如何将 Samba 作为工作组的一部分使用，这是 Samba 在家庭或 SOHO 网络上的典型用例。有关设置完整 Windows 域的信息，请确保你已按照本章“安装 Samba 服务器及伙伴”节的建议安装了 `samba-doc`，并参考 `/usr/share/doc/samba-doc/html/Samba3-By-Example` 目录下的 *Samba 3 By Example* 在线副本。

由于此示例显示的是小型工作组，你可能还想激活以下条目，让 Samba 不要作为 `WINDS`（Windows NetBIOS 名称服务，在本章稍早讨论过）运行，而是使用你的域名服务器来查找 Windows 主机名，它看起来如下：

```
wins support = no

dns proxy order = lmhosts hosts bcast
```

最后一个条目告诉客户端首先在本地 `lmhosts` 文件中检查名称信息（在 Windows 系统上），然后检查 Samba 服务器上 `/etc/hosts` 文件中的信息，接着检查 `WINS`（提供给本地 DNS 服务器的），最后使用广播搜索正确的主机。这种主机名查找组合基础在我设置或使用的每个 Samba 服务器配置中都是通用的。

最后，你必须定义用于识别 Samba 服务器经过身份验证的用户的安全模型。要实现这一点，请取消 Samba 配置文件以下条目的注释：

```
security = user
```

这完成了 Samba 能够与指定的工作组或域共享文件所必需的 Samba 配置文件的核心修改。这看起来不难，对吧？

# 配置 Samba 身份验证

在我们在本章示例的工作组配置中，Samba 预配置了执行工作组成员所需的身份验证类型。然而，为了访问共享资源，你必须对 Samba 服务器进行身份验证。Samba 维护身份验证信息——要设置用户密码，必须使用 `smpassword` 命令。在添加用户信息信息时，必须使用 `-a` 选项，后跟要添加的用户名。`smpassword` 命令会提示你输入密码并再次提示以确保你输入正确。以下是设置密码的示例输出：

```
$ smpassword -a whd

Password:

New SMB password:

Retype SMB password:
```

第一个提示来自 `sudo` 程序，要求 Ubuntu 密码以便执行此特权操作。第二个是验证用户 `whd` 的 Samba 密码。

> Samba 配置文件中建议的安全级别 `security = user` 要求 Samba 用户存在于 Ubuntu 系统的密码文件中，否则你将收到错误消息且 `smpassword` 命令将失败。有关其他安全模型及其影响，请查看 `samba-doc` 软件包中的 `/usr/share/samba-doc/htdocs/ServerType.html` 文件。

# 使用 Samba 共享打印机和主目录

在设置工作组并创建用户之后，下一步考虑让连接到 Samba 服务器的所有 Windows 系统可以使用 Ubuntu 系统上的通用资源。常见的例子是打印机和用户主目录。

Samba 配置文件 `[global]` 部分与打印机和打印相关的条目是以下，你应该确保它们没有被注释（即没有以分号开头）：

- `load printers`
- `printing = cups`
- `printcap name = cups`

在 Samba 配置文件的后面，`[printers]` 和 `[print$]` 部分提供了有关你的 Windows 系统如何与 Samba 服务器交互的信息。不需要更改其中的任何内容，但供你参考，这些条目如下：

```
[printers]

comment = All Printers

browseable = no

path = /tmp

printable = yes

guest ok = no

read only = yes

create mode = 0700

[print$]
```

# 设置 Samba 服务器

```
comment = Printer Drivers

path = /var/lib/samba/printers

browseable = yes

read only = yes

guest = no
```

`[printers]` 部分定义了 Samba 服务器将如何处理来自 Windows 客户端的打印机识别请求和传入的打印请求，而 `[print$]` 部分则将传统的 Windows$ 共享名称映射到你 Linux 系统上的目录，你可以在该目录中放置特定打印机的驱动程序，这样当你的 Windows 客户端本地没有这些驱动程序时，就可以下载并加载它们。

作为打印机，用户从其 Windows 系统访问的最自然的资源就是他们的 Ubuntu 或 Ubuntu 主目录。这为你提供了一种简单的方法，将你在 Samba 服务器上的主目录作为存储文件的集中位置，但同时也让你能够将文件从你的 Windows 系统自动备份到 Samba 服务器，并让你能够利用你在 Samba 服务器上执行的任何标准备份。（有关在你的 Ubuntu 上备份文件的更多信息，请参阅附录第 6 章）。

幸运的是，Samba 的配置文件默认已经配置好支持主目录，只要你的 Linux 和 Windows 用户名是匹配的。以下是支持该功能的 Samba 配置部分：

```
[homes]

comment = Home Directories

browseable = no

read only = yes

create mask = 0700

directory mask = 0700
```

如你从此配置文件片段中看到的，主目录默认是共享的，但从 Windows 客户端是不可写的。这非常不方便，因此你可能希望将此配置文件中的 `read` 条目改为 `no`，如下例所示：

```
read only = no
```

这使用户能够对其主目录中的文件进行读取和写入。

> 如果你的 Windows 和 Ubuntu 用户恰好具有不同的登录，你可以通过在 `/etc/samba/smusers` 文件中创建条目来将两者关联。此文件中的条目格式为 `UnixLogin=WindowsLogin`。为了将 Ubuntu 用户 `whv` 映射到 Windows 用户 `bill.vonhagen`，我会在 `/etc/samba/smusers` 文件中创建以下条目：

```
whv = bill.vonhagen
```

如果你的 Windows 登录名包含一个或多个空格，你必须在该文件中用引号将它们括起来。

在实践中，我建议在 Ubuntu 和 Samba 系统之间保持登录名一致，但如果你对不同类型系统的用户有不同的命名规范，可以使用此文件。

# 验证 Samba 配置文件

在对 Samba 配置文件进行任何更改后，你应该验证是否无意中违反了文件的语法。如果 Samba 配置文件包含任何无效条目，Samba 将显示错误信息且不会加载。这可能非常令人沮丧；由于 Samba 软件包还提供了一个测试 Samba 配置文件有效性并识别其发现的任何错误位置的工具。该工具是 `testparm`，你可以带无参数运行它来测试默认 Samba 配置文件 `/etc/samba/smb.conf`。运行 `testparm` 的输出如下：

```
$ testparm

Load config files from /etc/samba/smb.conf

Processing section "[homes]"

Processing section "[printers]"

Processing section "[print3]"

Loaded services OK.

WARNING: passwd expand explicit = yes is deprecated

Server role: ROLE_STANDALONE

Press enter to see a dump of your service definitions
```
