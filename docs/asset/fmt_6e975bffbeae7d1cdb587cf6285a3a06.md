
无论安装哪种类型的服务器，本地 UNIX 组都必须映射到 Windows 网络域全局组账户。你会问为什么吗？因为 Samba 始终通过传统的 UNIX UID 和 GID 控制来限制对主服务器资源的访问。这意味着必须将本地组映射到域全局组，以便域全局组的成员（即域用户）可以根据托管 Samba 的服务器本地的 UID 和 GID 获得访问权限。这种映射是使用 `net` 命令实现的。

托管运行作为成员（PDC、BDC 或 DMS）的 Samba-3 服务器的 UNIX 系统必须在域身份验证数据库（或目录）中拥有一个机器安全账户。此类安全（或信任）账户的创建也是使用 `net` 命令处理的。

使用 `net` 命令还可以实现域间信任的建立，以及许多典型的行政职责，如用户管理、组管理、共享和打印机管理、文件和打印机迁移、安全标识符管理等。

现在整体情况应该很清楚了：`net` 命令在 Samba-3 舞台上发挥着核心作用。这一角色将继续发展。本章的纳入证明了其重要性，其复杂性已经增长到不再认为在在线 UNIX 手册页中完全涵盖其用法是明智的地步。

## 12.2 管理任务和方法

此处记录了 `net` 命令的基本操作。该文档并非详尽无遗，因此是不完整的。由于主要焦点是从 Windows 服务器迁移到 Samba 服务器，因此重点在于使用分布式计算环境远程过程调用（DCE RPC）操作模式。当针对属于活动目录域的服务器使用时，最好（且通常是必需的）使用 ADS 模式操作。`net` 命令支持这两种模式，但并非支持所有操作。对于大多数操作，如果未指定模式，`net` 将通过 ads、rpc 和 rap 模式自动回退。有关此实用程序功能的更全面概述，请参阅手册页。

## 12.3 UNIX 和 Windows 组管理

如前所述，本章的大部分重点在于使用 Samba 支持的 `net rpc` 系列操作。大多数操作在使用活动目录时由 `net ads` 模式支持。对于这些操作中的某些操作，也支持 `net rap` 操作模式。RAP 协议由 IBM OS/2 和早期的一些 SMB 服务器使用。

Samba 的 `net` 工具实现了足够的功能，允许从命令行完成所有常见的管理任务。本节将探讨每个必要的用户和组管理功能。

Samba-3 识别两种类型的组：域组和局部组。域组只能包含（作为成员）域用户账户。局部组可以包含局部用户、域用户和域组作为成员。

局部组的目的是允许为组账户设置文件权限，该组账户像典型的 UNIX/Linux 组一样，在重新部署 Windows 文件服务器时是持久的。

### 12.3.1 添加、重命名或删除组账户

Samba 为 Windows 客户端提供文件和打印服务。它向 Windows 环境提供的文件系统资源必须，不可避免地，以与 Windows 网络环境兼容的方式提供。UNIX 组根据需要创建和删除，以满足 UNIX 操作系统及其文件系统的操作需求。

为了使 Windows 环境能够访问，Samba 提供了一种机制，可以将 UNIX 组映射到逻辑实体，称为 Windows（或域）组。Samba 支持两种类型的 Windows 组：局部组和全局组。全局组可以包含全局用户作为成员。这种成员身份以正常的 UNIX 方式实现，即将 UNIX 用户添加到 UNIX 组。Windows 用户账户由用户 SAM 账户（逻辑实体）和 UNIX 用户账户之间的映射组成。因此，UNIX 用户映射到 Windows 用户（即，被赋予 Windows 用户账户和密码），而该用户所属的 UNIX 组映射到 Windows 组账户。结果是，在 Windows 账户环境中，该用户由于 UNIX 组成员身份也是 Windows 组账户的成员。

处理 Windows 组管理的以下小节演示了 UNIX 组账户及其成员与相应的 Windows 组账户之间的关系。接着展示了如何在创建逻辑映射后，UNIX 组成员自动传递为 Windows 组成员身份。

#### 12.3.1.1 添加或创建新组

在尝试添加 Windows 组账户之前，可以列出当前可用的组，如下所示：

```
root#  net rpc group list -Uroot\%not24get
Password:
Domain Admins
Domain Users
Domain Guests
Print Operators
Backup Operators
Replicator
Domain Computers
Engineers
```

通过执行以下命令，可以添加一个名为“SupportEngrs”的 Windows 组账户：

```
root#  net rpc group add "SupportEngrs" -Uroot%not24get
```

添加完成后，新的组账户将立即可用，可通过执行此命令进行验证：

```
root#  net rpc group list -Uroot%not24get
Password:
Domain Admins
Domain Users
Domain Guests
Print Operators
Backup Operators
Replicator
Domain Computers
Engineers
SupportEngrs
```

以下内容演示了通过调用 `add group script = /opt/IDEALX/sbin/smbldap-groupadd -p "%g" interface script` 已创建了 POSIX（UNIX/Linux 系统账户）组：

```
root#  getent group
..
Domain Admins:x:512:root
Domain Users:x:513:ght,ict,ajt,met
Domain Guests:x:514:
Print Operators:x:550:
Backup Operators:x:551:
Replicator:x:552:
Domain Computers:x:553:
Engineers:x:1002:ght
SupportEngrs:x:1003:
```

以下内容演示了使用 `net` 命令添加组账户会导致已创建的 POSIX 组立即映射到 Windows 组账户，如下所示：

```
root#  net groupmap list
Domain Admins (S-1-5-21-72630-4128915-11681869-512) -> Domain Admins
Domain Users (S-1-5-21-72630-4128915-11681869-513) -> Domain Users
Domain Guests (S-1-5-21-72630-4128915-11681869-514) -> Domain Guests
Print Operators (S-1-5-21-72630-4128915-11681869-550) -> Print Operators
Backup Operators (S-1-5-21-72630-4128915-11681869-551) -> Backup Operators
Replicator (S-1-5-21-72630-4128915-11681869-552) -> Replicator
Domain Computers (S-1-5-21-72630-4128915-11681869-553) -> Domain Computers
Engineers (S-1-5-21-72630-4128915-11681869-3005) -> Engineers
SupportEngrs (S-1-5-21-72630-4128915-11681869-3007) -> SupportEngrs
```

### 12.3.1.2 将 Windows 组映射到 UNIX 组

Windows 组必须映射到 UNIX 系统（POSIX）组，以便能够以一种与托管 Samba 服务器的主机操作系统所采用的适当方法一致的方式实施文件系统访问控制。

在托管 Samba 服务器的 UNIX/Linux 服务器文件系统内，所有文件系统（文件和目录）访问控制都是通过 UID/GID 身份元组实现的。Samba 在某种程度上都不会覆盖或替换 UNIX 文件系统语义。因此，所有访问文件系统的 Windows 网络操作都需要提供一种机制，将 Windows 用户映射到特定的 UNIX/Linux 组账户。用户账户还必须映射到本地已知的 UID。请注意，`net` 命令在此处不会调用任何 RPC 函数，而是直接访问 passwd。

Samba 依赖于 Domain Admins、Domain Users 和 Domain Guests 全局组的默认映射。可以像刚才给出的示例那样添加额外的组。有时需要将现有的 UNIX 组账户映射到 Windows 组。此操作实际上会创建映射，从而作为结果创建一个 Windows 组账户。

允许的操作包括：`添加`、`修改`和`删除`。每个操作的示例如下所示。

在此示例中，可以将现有的 UNIX 组映射到现有的 Windows 组：
