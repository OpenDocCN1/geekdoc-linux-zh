
### 私有目录

你计算机上的用户有自己的私有目录——他们的家目录。除了 Red Linux 以外的许多发行版将用户组织为 `users` 组的一部分。在这种情况下，其他用户可以看到并读取所有 `/home` 目录下的文件。

在这种情况下，需要特殊命令来给用户 fred 提供一个私有目录。例如，你可以激活以下命令来设置一个仅 Fred 可见且访问的私有目录：

```
comment = Fred's Service
path = /usr/somewhere/private
valid users = fred
public = no
writable = yes
printable = yes
```

为了让这些命令生效，你需要创建由 `path` 变量指定的目录。你需要将 fred 设置为 `/usr/somewhere/private` 目录的用户和组所有者。

# 按客户端划分目录

由于 `[homes]` 共享是按用户划分的，你可以根据网络上客户端计算机的 NetBIOS 名称设置特殊目录。例如，我的其中一台计算机的 NetBIOS 名为 StStephen，因此我为 `/home/stephen` 设置了一个家目录。我修改了从默认 Samba 配置文件中的路径，并在以下段中配置了 NetBIOS 客户端目录：

```
comment = PC Directories
path = /home/%m
public = no
writable = yes
```

记住，`%m` 对应计算机的 NetBIOS 名称。因此，`/home/stephen` 目录对登录到你的 Samba 服务器的用户可见。当你创建特定目录时，你需要让所有用户都可访问。否则，用户可能无法向该目录写入。如第 4 章“设置你的用户”所描述，你可以通过以下命令实现这一点：

```
chmod 777 /home/stephen
```

# 102 Windows 管理员 Linux 传输

### 所有用户作为访客

你可以为所有用户设置一个公共目录。以下段设置了一个所有人都可以覆盖文件的目录。我将 `path` 变量更改为 `/home` 部分。

```
[public]
path = /home/public
public = yes
only guest = yes
writable = yes
```

关键命令是 `only guest = yes`，它将所有登录重定向到访客账户。在 Samba 服务器上，无论你如何登录此共享目录，创建的任何文件都属于访客账户。任何登录该访客账户的人都可以删除创建的文件。

### 小组

最后的段允许你为两个用户设置一个私有目录。它与之前的“组目录”部分描述的目录类似，但这个目录是私有的。你仍然需要设置一个由组拥有的独立目录。

你需要为共享目录设置完整的组权限，在这种情况下仅允许 mary 和 fred。每个用户对其放在共享目录中的任何文件保留个人所有权。例如，如果 Fred 创建了 `chapter4.doc` 文件，Mary 无法删除该文件。

```
[myshare]
comment = Mary's and Fred's stuff
path = /home/maryfred
valid users = mary fred
public = no
writable = yes
printable = no
create mask = 0765
```

### 总结

你可以配置 Samba，将你的 Linux 计算机设置为 Microsoft Windows 网络上的客户端、服务器或域控制器。在这样做之前，你需要了解 Microsoft CIFS 的背景。在该系统中，你可以在 Microsoft 网络中设置客户端和服务器计算机，按工作组和域进行组织。

还有另一种方案；你可以在 Microsoft Windows 计算机上设置 Microsoft Services for Unix。遗憾的是，这是昂贵的，而且不支持局域网上的 Microsoft Windows 9/ME 计算机。相比之下，Samba 是免费可靠的，因此它是本书的核心。

在配置 Samba 之前，你需要了解如何启动和管理 Samba 进程。

### 第3章：设置你的服务器文件系统

计算机。在 Red Hat Linux 中，`/etc/samba` 目录下有几个基本的 Samba 文件。

你可以使用两个 GUI 工具来配置 Samba。Red Hat 创建了 Samba 服务器配置器（Samba Server Configurator），它可以帮助你设置带有基础配置的 Samba 服务器。还有一个更完整的实用程序被称为 Samba 网页管理工具（SWAT）。

但要真正理解 Samba 的工作原理，你需要深入主 Samba 配置文件 `smb.conf` 的细节，它包含了全局参数（`global`）和共享参数（`share`）。我详细分析了该文件的默认版本，这样你就可以更智能地决定如何在你自己的计算机和网络上配置 Samba。

> 本章的更新和更正可以在 Hentzenwerke 的网站 `www.hentzenwerke.com` 上找到。点击“Catalog（目录）”并导航到该书的页面。

## 第4章：设置你文件服务器的用户

计算机网络围绕用户和组展开。用户可以登录到计算机和网络，并访问他们拥有的文件和目录。在基于微软的网络中，管理员通常会与组共享额外的文件和目录。虽然微软和 Linux 的用户和组数据库是不同的，但本章将展示它们如何协同工作。完成本章后，你将能够在基于微软或基于 Linux 的 PDC（主域控制器）上设置用户和组。

如果你要建立 Linux PDC，你需要按照第3章描述的方法了解如何设置 Linux 用户和组；你还需要在 Linux PDC 上有一个相应的 Samba 用户数据库，以便从微软 Windows 计算机访问。

当你配置单一用户名和密码数据库时，可以配置 `winbind` 进程，允许网络上的 Linux 计算机与微软 Windows PDC 配合。或者，你可以配置一个带有 Samba 的 Linux 计算机作为 PDC，并为微软工作站自定义登录配置文件。

登录 Linux PDC 的用户至少可以访问家目录。额外的共享在 Linux PDC 的 `smb.conf` 文件中定义，并受到 Linux 文件和目录所有权及权限模型的限制。连接到 Linux 成员服务器的用户也可以根据每个成员服务器的 `smb.conf` 文件进行连接。

> 你可以在附录 B 中找到 PDC 和成员服务器的 `smb.conf` 配置。

![](img/6ee4859e736a0839007ea9afb576c195_125_0.png)

尽管 Samba 不完全支持微软的访问控制列表（`ACL`），但你仍然可以在选择的目录上为自定义组配置访问控制。本章基于第3章“设置你的文件系统”中描述 `smb.conf` 设置。在较大的网络中，监管每个用户和组使用的资源是非常重要的；我将向你展示如何使用 Linux 配额系统来实现。

由于这是为管理员编写的章节，以下几乎所有的命令和实用程序都需要访问你设置为 PDC 或成员服务器的 Linux 计算机上的管理员账户。换句话说，以普通用户身份登录后，运行以下命令启动 Linux 管理员账户；输入 root 用户密码

```bash
su
password:
```
