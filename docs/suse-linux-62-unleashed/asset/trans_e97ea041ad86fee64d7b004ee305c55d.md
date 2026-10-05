

# 安全

我们要讨论的第二点是文件权限如何在 Windows 和 Samba 之间进行转换。在 Windows NT 下，你必须拥有用户名和密码才能登录机器。在基于 NTFS 的系统上创建文件时，文件由你所有，且其他用户无法访问。在 Windows 95 和 98 下，虽然你可能在启动时输入用户名和密码（会出现 Microsoft Windows 网络对话框），但本地硬盘上的文件可以被任何人修改。Windows 产品在安全性方面显然存在巨大差异；但 Samba 是如何处理安全性的？

在 Samba 中，有不同的安全级别，但我们在本章中关注的是被称为“用户级”（user-level）的安全，这也是 Samba 默认使用的级别。当 Samba 机器使用用户级安全时，它要求访问特定共享需要有效的用户名和密码。Samba 共享可以被“锁定”仅允许某些用户访问；这在用 Samba 导出主目录并防止“被锁定”的用户访问特定共享时非常有用——即使他们提供了有效的用户名和密码也不行。

你在 Windows 网络对话框（或 NT 下的 Windows 登录对话框）中输入的用户名和密码将将 Windows Windows来尝试访问 Samba 共享。这将自动发生，不需要你再次输入这些用户名和密码。然而，如果 Samba 服务器拒绝访问，Windows 将提示你输入该共享的用户名和密码。在测试初始 Samba 配置时，请记住这一点。

# 文件权限和用户账户

假设你以 drobbins 身份登录 Windows NT，启动一个 Samba 共享并创建几个文件。你可能想知道 Samba 为这些文件分配了什么 UNIX 权限——毕竟，由于 Samba 运行在 UNIX 文件系统上，每个文件都必须有一个默认的用户 ID 和组 ID。答案是，Samba 要求你拥有与 Windows 机器上的用户名完全对应的 Linux 用户。这意味着实际上，Samba 期望在 `/etc/passwd` 文件中找到用户名 `drobbins` 的 Linux 用户。在配置 Samba 时请记住这一点，并记住，如果你从 NT 访问共享，你可能需要在 `/etc/passwd` 中输入一个 Linux 管理员账户，权限才能正常工作。所有的 Samba 系统都需要在 `/etc/passwd` 中有一个名为 `guest` 的账户。如果这些账户还不存在，现在何花些时间向系统添加所需的用户账户呢？这些账户不需要设置任何密码，甚至不需要默认 shell；Samba 仅使用它们来正确设置文件权限，并使用 `/etc/smbpasswd` 文件实际检查密码。

# 密码

理解 Samba 如何处理密码和用户验证过程非常重要。简单来说，Samba 有一个独立的密码文件（`/etc/smbpasswd`）用于验证用户。这意味着你可以为同一个用户设置两个密码——一个用于访问 Samba 共享，另一个用于通过 telnet 本地登录你的 Linux 机器。通常，这两个密码文件保持同步是最好的。

此外，这意味着在用户密码添加到 `/etc/smbpasswd` 文件之前，认证将无法工作。请记住这一点，特别是当你以后遇到认证问题时。

这里有一个例外：如果你使用“非加密”密码（这不推荐，且未来用得会越来越少），Samba 将使用标准的 Linux 密码进行验证，而不需要 `/etc/smbpasswd` 文件。但是，如果可能，建议使用加密密码，因为最近版本的 Windows 能够正确处理它们，并且它们将为你的网络提供增强的安全保护。

# 安装 Samba 软件包

你可以在从光盘 安装 SuSE 期间，或者之后使用 YaST 或 rpm 安装 Samba。如果你需要安装该包，请先从 SuSE 网站 (http://www.suse.com) 下载当前版本，或在光盘 1 上找到该包。然后可以使用 YaST（“n”系列下的 samba）或通过以下命令使用 RPM 安装：

```
rpm -ivh samba-2.0.5a-1.1386.rpm
```

该包应该包含所有需要的文件，包括运行 Samba 的两个主要程序（smbd 和 nmbd）。

# 配置 Samba

Samba 可能非常复杂，因此在进行重大配置更改之前，运行一个尽可能简单的 Samba 实现是非常重要的。在这个示例中，我们将创建自己的最小化配置文件。在让这个最小版本正常运行后，是尝试新功能的良好时机。

# 网络和互联网服务
第二部分

主配置文件 `smb.conf` 位于你 SuSE Samba 服务器的 `/etc` 目录。它被 Samba 服务器软件 (smbd) 用于确定哪些目录和打印机是共享的，并确定用于这些目录和打印机的安全选项。

> 注意
smb.conf 行开头的 `;` 字符表示该行是注释，Samba 服务器在处理时会忽略该行。`#` 字符的作用相同。通常情况下，`;` 字符用于注释选项行，而 `#` 用于真正注释的行开头。

`smb.conf` 文件布局由一系列命名的节组成。每个节以方括号开头，如 `[global]`。每个节内的参数通过键值对指定，例如 SuSE Samba。

smb.conf 包含三个特殊节和多个自定义节。特殊节是 `[global]`、`[homes]` 和 `[printers]`。在详细描述它们之前，先让 Samba 。

# 我们的初始 smb.conf

为了让 Samba 运行起来，我们要做的第一件事是创建一个新的 /etc/smb.conf 文件，并在其中包含信息。此配置专门设计用于消除可能的问题并快速测试你的配置。在我们确认此配置有效后，鼓励探索你感兴趣的 Samba 功能：

```ini
[global]
guest account=guest
encrypt passwords=yes
workgroup=mygroup
security=user
socket_options=TCP_NODELAY
wins support=yes
os level=65
local master=yes
domain master=yes
preferred master=yes
public=yes

[tmp]
comment=test share
path=/tmp
writeable=yes
```

```ini
[username]
comment=username's home directory
path=/home/username
writeable=yes
force user=username
```

![](img/cbac72550c7126a22162e4491a0c60_520_0)

> 注意
将 username 替换为你 SuSE 系统上的有效用户账户。force user 告诉 Samba 将所有文件归 username 所有，即使是由 Administrator 创建的。这可以防止在多个用户账户修改此共享时出现问题。更多信息请查看 man smb.conf。

此文件做了许多有助于 Samba 运行更顺畅的工作。首先，它配置 nmbd 作为网络的主浏览器。让你的 Samba  作为主浏览器，它将管理 Windows 机器通过邻域可见的主机数据库。为了获得最佳性能，建议将你的 Windows 机器配置为使用你的 Samba 作为主 WINS 服务器；可以在网络控制面板中配置，并允许你的 Windows 机器快速找到 Samba 服务器。

关于此配置文件还有几点重要的说明。首先，你应该让所有的 Windows 机器加入你在 workgroup 选项中选择的工作组名称。或者，简单地更改 workgroup 选项以匹配你的 Windows 机器目前所属的工作组。其次，确保你的 /etc/passwd 文件中有一个 guest 用户。我们添加了一个名为 tmp 的测试共享，你可以用它来测试 Samba 是否正常工作。对于网络共享的通用浏览，Samba 和 Samba 广泛使用了 guest 账户。

重启 Samba 服务器：

```
$ /etc/rc.d/init.d/samba restart
```

