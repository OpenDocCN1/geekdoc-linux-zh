
对于许多站点来说，Samba 配置中最棘手的方面之一（特别是对于具有许多用户和复杂需求的大型站点）是集成 Samba 的 Unix 风格和微软文件安全模型。正如第 2 章“独特的所有权和权限”所述，Linux 的安全模型与 Windows 不同。与 Windows 9x 相比，Linux 的安全模型相当复杂，因此你通过 Samba 服务器可以实现的操作比通过 Windows 9x 服务器更多。然而，Windows NT 和 2000 支持访问控制列表 `ACL`，它提供了 Linux 风格安全性的替代方案，与 Linux 的安全模型不同，并且在某些方面更加灵活。因此，如果你是一位经验丰富的 Windows NT 管理员，Linux 的安全功能可能需要一些适应。如果你已经熟悉 Linux 或 Unix 文件权限，那么在让你的 Linux 服务器在这方面满足你的需求上，应该没有困难。

Samba 在重要的方面扩展了 Linux 文件权限，其中一些我已经在本章早些部分列出，特别是在“浏览选项”中。具体来说，`allow`、`deny`、`valid users` 和 `invalid users` 参数允许你对共享访问进行精细调整，而这些调整是 Linux 所有权和权限无法控制的。例如，你可以拒绝特定用户或任何来自特定计算机的访问访问该共享。这些问题在第 14 章“Samba 安全考量”中会有更详细的介绍。

## Samba 所有权和权限选项

Samba 提供了几个影响用户使用 Linux 文件名和权限的选项。你可以使用这些选项创建一个适用于你网络环境的安全配置。

### 控制所有权

在 Linux 服务器上，每个文件都有所有者和一个组。每个用户根据其用户 ID 和所属的组拥有读取和写入文件的权限。你可以使用一对配置参数来调整与访问共享相关的所有者和组：

`force user` 通常情况下，当你连接到 Samba 服务器时，你会发送你的用户名和密码，然后可以使用与该用户名关联的权限访问和创建文件。例如，如果你以 `susani` 的身份连接，你创建的任何文件将归 Linux 用户 `susani` 所有。在 Samba 2.0.0 之前，如果用户通过 `samba` 守护进程创建了文件，那么该文件的所有者将设置为 `samba`，而组将设置为 `samba` 组。从 Samba 2.0.0 之后，Samba 将使用创建文件的用户的身份来设置所有者。如果你使用 `force user susani`，那么任何创建的文件都将属于 `susani` 用户，且其组将设置为 `susani` 组。由于在 Samba 2.0.0 之后，Samba 停止使用 `force group` 选项，转而使用 `force user` 配合该参数来实现，这将强制将文件的组设置为 `susani` 组。

`force group` 在 Samba 2.0.0 之后，此选项已不再使用，取而代之的是使用 `force user` 配合该参数来实现。

# 第 5 章 文件共享配置

`security mask` 此参数控制用户通过 Windows NT 安全控制可以操作哪些 Linux 安全位，如第 14 节所述。如果没有显式设置，它的默认值与 `create mask` 参数相同。

`directory security mask` 此参数与 `security mask` 语义效，但它应用于目录而不是文件。

`force security mode` 此参数在用户通过 Windows NT 安全控制操纵安全选项时，会强制开启 Linux 安全位。它的默认值与 `force create mode` 选项相同。

`force directory mode` 此参数与 `force security mode` 语义效，但它应用于目录而不是文件。

`inherit permissions` 通常情况下，文件和目录权限是通过 `create mask` 等选项设置的。`inherit permissions` 会覆盖这些设置，并导致权限从父目录继承。例如，如果目录的权限为 `0750`，则权限将从父目录继承，但执行权限是由 Samba 对 DOS 风格隐藏、系统和归档位的映射设置的。Linux 用户 ID `suid` 无法继承。

## 使用示例

你可以利用所有权和权限选项执行非常不寻的操作。例如，假设你想给一个用户（比如，管理员）所有用户主目录共享的完全读写权限，并给该用户组的其他成员只读权限。你可以创建一个如下的共享定义：

```
[homes]
comment = Home Directories
include = /etc/samba/smb.conf,%U
create mask = 0640
writeable = Yes
browseable = No
```

然后，你创建一个名为 `/etc/samba/smb.conf.superv` 的辅助配置文件（其中 `superv` 是管理员的用户名）。该文件将包含一行：

```
force user = %S
```

### 设置所有权和权限

主 `samba.conf` 文件中 `include` 行的 `%U` 变量会使 Samba 搜索以共享用户提供的提供的用户名结尾的文件。如果未找到该文件，Samba 将忽略 `include` 指令。如果文件存在，Samba 将读取它并将其内容包含在文件的相应位置。当 `super` 连接到用户的共享时，Samba 读取 `smb.conf`，`super` 用户行和 `force user` 行会让 Samba 将连接处理为来自 `%S`。在 `[homes]` 共享的情况下，共享名称 `%S` 与共享的所有者相同。因此，Samba 授予用户与共享所有者相同的权限。

`create mask` 参数导致所有创建的文件都以 `0640` 权限创建（客户端程序指定只读除外），文件对组内其他成员是可读但不可写的。结果是 `super` 和共享所有者对共享具有完全的读写访问权限，而组其他成员只有只读访问权限。（主目录必须具有适当的权限，例如 `0750`）。

> **警告** 像我上面概述的这种复杂函数可能会带来不便，例如，如果允许普通用户在 `/etc/samba` 目录下创建新文件，他们可能会创建具有增强权限的文件，甚至获得超级用户访问权限！此外，在本例配置中，`super` 可以添加或删除文件，这些更改看起来就像是共享普通用户执行的一样——从安全角度来看，这并不一定是我们需要的。

## 与其他服务的交互

当你通过 Samba 设置（或未设置）文件所有权权限时，这些选项可能会对其他 Linux 服务产生影响。例如，如果用户使用 Telnet 或安全外壳 `SSH` 访问共享，他们可以修改文件属性。

## Samba 可以将 Linux 权限呈现给 Windows NT 客户端，仿佛它们是“特殊访问”ACL 一。

![](img/3a24c35ebb6bb7434f422c2c74e83fe8_166_0.png)

## 网络安全预览

Samba 包含许多安全功能，将在第 14 章进行更详细的检查，但从一开始开始，你就考虑一些问题和某些 `smb.conf` 参数。其中之一是控制一个用户访问另一个用户文件的机制。如果你的系统用户很少，且需要对其他的文件进行较少限制的访问，必须使用 `create mask`、`force create mode` 及其目录参数来设置一个相当开放的环境，使所有用户都能读写他人的文件。另一方面，在高度安全的环境中，你可能希望使用严格的默认安全选项，例如 `create mask = 0600`，以限制对用户主目录下文件的访问。

### 符号链接

Samba 服务器上出现但 Windows 服务器上没有的一个网络安全问题与链接，即符号链接有关。这些特殊文件允许一个文件充当另一个文件的替身。假设你的目录中有一个名为 `report.wp` 的文件。如果你想从重要目录访问此文件，可以创建一个指向 `important/report.wp` 的链接，从而访问 `report/report.wp`。在 Linux 中，你使用 `ln` 命令来创建链接（`ln -s` 创建符号链接，这是本文讨论感兴趣的类型）。`ln` 命令的工作原理与 `cp` 相似，用于复制文件。例如，此命令创建一个符号链接 -

```bash
$ ln -s papers/report.wp important/report.wp
```

你无法从客户端计算机通过 Samba 创建 Linux 链接。

### 设置所有者和权限

**注意** Windows 包含名为快捷方式的类似链接的功能。由于 Windows 将快捷方式实现为普通文件，你可以从 Windows 客户端在 Samba 服务器上创建快捷方式。这些快捷方式可以指向同一个服务器、客户端文件或其他服务器的文件。同样，Samba 服务器上的快捷方式也是如此。

Samba 对链接的处理受两个参数的影响：

- `follow symlinks` 此参数控制 Samba 是否遵循符号链接。如果设置为 `No`，任何访问符号链接的尝试都将失败。这是一个非常有用的安全预防措施，防止访问其他用户目录或系统目录中的敏感数据。Linux 内核的严格安全也可以防止滥用，但你可能希望将其作为额外的预防措施——特别是在你设置了 `force user` 参数的共享中。`follow symlinks` 不影响 Samba 对硬链接的处理（在创建 `ln` 时没有 `-s` 参数）。

- `wide links` 此参数允许指向用户正常范围之外目录的链接。具体来说，如果 `links = No`，Samba 不遵循指向共享正常树之外的目录链接，但该树内的链接仍然有效。例如，如果你共享了 Linux 目录 `/usr/samba/share`，那么从该共享到 `/usr/local` 或 `/somedir/anotherdir` 的链接将成功。此参数不影响 Samba 对指向共享目录树之外文件的符号链接的处理，也不适用于硬链接。

`follow = No` 和 `wide links = No` 参数都会影响文件访问，因此你必须在潜在的安全收益与性能开销之间取得平衡。这些参数是共享级别的，可以为单独共享设置不同的值。

## 用户与用户访问控制

你已经解释了参数如何决定谁允许访问共享。除了 `valid users` 和 `invalid users` 参数以及 `hosts`、`allow` 和 `deny` 控制外，还有几个值得注意的参数。

- `admin users` 你可以在此参数中指定一个或多个用户名。这些用户在访问共享时将获得等同 root 的权限。在大多数情况下，不需要此选项；你可以通过其他手段（例如 `write list 1` 列表参数）授予特定用户高于正常水平的访问。我建议你少用 `admin users`，甚至尽量不用，因为它的权限很大，如果配置不当可能会导致问题。

![](img/3a24c35ebb6bb7434f422c2c74e83fe8_167_0.png)

- `write list` 当 `writeable` 参数设置为 `No` 时，用户无法写入共享。尽管如此，你可能仍需要向一个或多个用户授予写入权限，可以通过 `write list` 参数来实现这一点。例如，`write list = susani` 为一个原本被标记为只读的共享授予写入权限。然而，在这种情况下，susani 无法克服她自己基于 Linux 的权限。如果没有权限在共享中创建文件（例如，因为目录属于他人且具有 `075` 权限），即使 susani 出现在 `write list` 中，她无法写入该目录。

- `read list` `read list` 是 `write list` 的相反；它指定了在创建和修改文件方面需要降低共享权限的用户。如果你使用 `read list`，该共享实际上与使用 `writeable = ..` 创建的共享相同。与 `write list` 一样，此参数不会覆盖 Linux 的文件权限正常规则。

- `username` 此共享级别参数指定了一个用户名列表，提供的密码将对比这些用户名。当客户端计算机没有发送用户名或发送了错误的用户名时，你可以使用此选项。设置 `username` 会减慢验证速度并增加安全风险。你可以通过三种方式之一指定用户组而不是单个用户：

    - 如果 `username` 前有 `@` 符号 (`@username`)
    - 如果 `username` 前有 `+` 符号 (`+username`)
    - 如果 `username` 前有 `&` 符号 (`&username`)

考虑一个包含数据文件的共享，你希望网络中的所有用户都能访问它，即使这些人在 Samba 服务器上没有账户。你可以将 `map to guest` 设置为 `Bad User`，然后创建一个如下所示共享：

```
[guest]

comment = All Users Welcome
path = /home/samba/guest
guest account = nemo
writeable = No
write list = marcusc, susani
guest ok = Yes
guest only = Yes
```

此定义允许所有人访问该共享，但权限受限（只读）。为了使此定义生效，目录中的所有文件必须允许用户 `nemo` 读取。请注意，`marcusc` 和 `susani` 在写入列表中，因此它们对该共享具有读/写权限（前提是用户 `nemo` 有权访问 `/home/samba/guest` 目录）。这两个用户可以维护此共享目录中的文件。由于由于 `guest only = Yes`，所有其他用户都根据在计算机上授予 `nemo` 的权限拥有只读访问。由于 `[global]` 部分包含了 `map to guest = Bad User`，在系统中拥有账户的人在使用其普通用户名时必须提供有效的密码。（如果这是计算机上唯一的访客共享，`map to guest = Bad Password` 可能是更好的选择，因为它可以防止访客用户在尝试访问被有效用户使用的共享时被拒绝。）

## 一些常见的文件共享场景

为了说明本章描述的许多参数，让我们来看看它们的实际运行情况。本节将专门介绍你在现实生活中可能会遇到的一些文件共享场景。每个场景都是一个较小但完整的 `smb.conf` 文件，可用于所述情况，并附带有对其影响和后果的描述。

## 共享程序和文件服务器

许多网络将文字处理器、归档工具和图形实用程序等常用程序放在中央服务器上供所有人使用，同时允许用户在服务器上存储个人文件。虽然这种配置很方便，但与程序文件存储在各个工作站的安排相比，它的速度较慢。你还必须小心不要违反程序的许可协议，这些协议可能会限制使用该软件的计算机数量。

这种设置的一个特别棘手的问题是，许多 Windows 程序会将程序文件存储在程序专用的目录中以及 `WINDOWS` 目录中。结果是，你可能需要在每个客户端上重新安装此类程序，尽管配置是存储在 Samba 上的。这些问题可能会使配置变得很麻烦，但对于很少使用且不强制要求在 `WINDOWS` 目录中安装自身部分的程序来说仍然是有用的。

此类配置的示例 `smb.conf` 所示于列表 5.1。

## 列表 5.1 用于共享文件和程序的 smb.conf 文件

```
[global]
workgroup = EF
netbios name = WARLOCK
server string = Samba server on %L
encrypt passwords = Yes
log file = /var/log/samba/log.sm

[homes]
comment = Home Directories
writeable = Yes
browable = No
create mask = 0664
directory mask = 0775

[winprogs]
comment = Windows Programs
path = /home/samba/winprogs
force user = winuser
write list = susani
read only = Yes
create mask = 0600
directory mask = 0700
```

### 第 5 章配置文件共享

列表 5.1 中的定义非常直观。请注意以下几：

- `[global]` 部分设置了第 4 章中描述的各种配置选项。计算机的 NetBIOS 名称为 `WARLOCK`，即使该机器的 TCP/IP 名称是其他内容。Samba 为每个连接到计算机的客户端创建一个不同的日志文件。

- 用户的家目录被显式地设置为可写但不可浏览（not browseable）。这种组合允许用户向其家目录写入内容，并防止在 Windows 浏览器运行时显示名为 `HOME` 的共享。然而，即使设置了 `browseable = No`，Samba 也会自动生成以用户命名的家目录共享。

- `[homes]` 共享中的 `create mask` 和 `directory mask` 参数设置了所有访问权限。这种安排适用于用户可以通过读写他人的文件轻松进行协作的环境。你可以为每个协作组创建 Linux 组。成员可以读写写属于该组的文件，但他们只能读取来自他人目录的文件。

- `winprogs` 共享依赖于一个名为 `winuser` 的用户。Linux 服务器上的 `/etc/password` 文件必须配置一个同名的用户，但该用户不需要（且不应该）任何登录权限。将用户的 shell 设置为 `/dev/nolog` 等内容，这样没有人能使用该用户名登录，并禁用该用户的密码。

- `susani` 在 `winprops` 共享中具有写权限，但对其他人来说，它是一个只读共享。`create mask` 和 `directory mask` 参数确保了 `susani` 创建的文件只有 `winuser` 可读，这是没问题的，因为它是使用 `winuser` 的权限创建的。如果你希望用户能够从 Linux shell 账户访问这些文件，你必须修改配置的这部分。

总的来说，上述安排是许多 Samba 配置的良好起点。当然，你可以以各种方式对其自定义，以实现你所需的安全和其他选项。

## 高安全性中央服务器上的用户文件
