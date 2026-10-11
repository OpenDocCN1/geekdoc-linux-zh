

**注意**

以下大多数示例均已在 Windows XP 专业版客户端上进行了验证。当本文档描述对命令的响应时，请记住，Windows 200x/XP 客户端非常相似，但在细微之处可能存在差异。Windows NT4 则又有所不同。

## 20.2 技术介绍

Samba 的打印支持始终依赖于其运行的 UNIX 操作系统上已安装的打印子系统。Samba 充当**中介**。它从 Windows（或其他 SMB）客户端接收打印文件，并将其传递给实际的打印系统进行进一步处理；因此，它需要与双方进行沟通：Windows 打印客户端和 UNIX 打印系统。因此，我们必须区分各种客户端操作系统类型（它们的行为各不相同）以及各种 UNIX 打印子系统（它们自身具有不同的功能，并且访问方式也不同）。

本章讨论 UNIX 打印的传统方式。下一章将详细涵盖更现代的 CUPS。

**重要**

CUPS 用户请注意：不要直接跳到下一章。你可能会遗漏仅在此处找到的重要信息！

从 Samba 邮件列表上的帖子可以看出，打印配置是当今 Samba 管理中最具问题性的方面之一。许多新的 Samba 管理员认为 Samba 执行某种打印处理。请放心，Samba 不执行任何形式的打印处理。它也不执行任何形式的打印过滤。

Samba 从客户端获取数据流（打印作业），并将其重定向到本地暂存区。当整个打印作业接收完毕后，Samba 调用本地 UNIX/Linux 打印命令，并将暂存的文件传递给该命令。正确处理打印作业并将其提交给打印机是本地系统打印子系统的责任。

### 20.2.1 客户端到 Samba 打印作业处理

通过 Samba 打印服务器从 Windows 客户端成功打印到 UNIX 打印机涉及六个（潜在七个）阶段：

- 1. Windows 打开到打印机共享的连接。
- 2. Samba 必须对用户进行身份验证。
- 3. Windows 通过网络将打印文件副本发送到 Samba 的暂存区。
- 4. Windows 关闭连接。
- 5. Samba 调用打印命令，将文件移交给 UNIX 打印子系统的暂存区。
- 6. UNIX 打印子系统处理打印作业。
- 7. 可能需要明确地从 Samba 暂存区删除打印文件。此项取决于你的打印暂存器配置设置。

### 20.2.2 与打印相关的配置参数

有许多配置参数用于控制 Samba 的打印行为。有关这些参数的概述，请参阅 **smb.conf** 的手册页。与其他参数一样，存在全局级别（在列表中带有 *G* 标记）和服务级别（*S*）参数。

**全局参数** 这些参数*不得*放入单个共享定义中。如果因错误而放入，**testparm** 实用工具可以检测到这种情况（如果你运行该工具）并告知你。

**服务级别参数** 这些参数可以在 **smb.conf** 的 *[/global]* 部分中指定。在这种情况下，它们定义了所有单个或服务级别共享的默认行为（除非它们为同一参数定义了不同的设置，从而覆盖全局默认值）。

## 20.3 简单打印配置

示例 20.3.1 显示了一个简单的打印配置。如果你将其与自己的配置进行比较，你可能会发现操作系统厂商预先配置了其他参数。以下是对这些参数的讨论和解释。此示例没有使用很多参数。然而，在许多环境中，这些足以提供一个有效的 **smb.conf** 文件，使所有客户端都能进行打印。

这只是一个配置示例。Samba 会为所有配置参数分配默认值。默认值是保守且合理的。当在 **smb.conf** 文件中指定某个参数时，这将覆盖默认值。以 root 身份运行时，**testparm** 实用工具能够报告所有设置，包括默认设置以及 **smb.conf** 文件设置。**Testparm**

**示例 20.3.1 使用 BSD 打印的简单配置**

```text
[global]
     printing = bsd
     load printers = yes
[printers]
     path = /var/spool/samba
     printable = yes
     public = yes
     writable = no
```

对所有配置错误的设置发出警告。完整输出轻松达到 360 行或更多，因此你可能希望将其通过分页器程序进行管道处理。

配置文件的语法很容易掌握。你应该知道它对语法不太挑剔。正如本书其他地方所述，Samba 容许某些拼写错误（例如使用 *browsable* 而不是 *browsable*），并且拼写不区分大小写。对于布尔设置，使用 *Yes/No* 或 *True/False* 都是允许的。名称列表可以用逗号、空格或制表符分隔。

### 20.3.1 使用 testparm 验证配置

若要查看 Samba 中所有（或至少大多数）与打印相关的设置，包括隐式使用的设置，请尝试下面概述的命令。该命令在 **testparm** 的输出中搜索 **lp**、**print**、**spool**、**driver**、**ports** 和 **l** 的所有出现。这提供了对正在运行的 **smbd** 打印配置的便捷概览。该命令不会显示单独创建的打印机共享或其可能使用的暂存路径。以下是我的 Samba 设置输出，其中显示了示例 20.3.1 中的设置：

```bash
root# testparm -s -v | egrep "(lp|print|spool|driver|ports|\\D)"
Load smb config files from /etc/samba/smb.conf
Processing section "[homes]"
Processing section "[printers]"

[global]
     smb ports = 139 445
     lpq cache time = 10
     load printers = Yes
     printcap name = /etc/printcap
     disable spoolss = No
     enumports command =
     addprinter command =
     deleteprinter command =
     show add printer wizard = Yes
     os2 driver map =
     printer admin =
min print space = 0
max print jobs = 1000
printable = No
printing = bsd
print command = lpr -r -P'%p' '%s'
lpq command = lpq -P'%p'
lprm command = lprm -P'%p' '%j'
lppause command =
lpresume command =
printer name =
use client driver = No

[homes]

[printers]
    path = /var/spool/samba
    printable = Yes
```

你可以轻松验证哪些设置是由 Samba 的默认行为隐式添加的。请记住：这在你未来处理 Samba 时可能很重要。

![](img/86d74c6cc862465e3a42e6dc3c90935a_360_0.png)

> **注意**
>
> Samba-3 中的 **testparm** 行为与 2.2.x 中的不同：如果不使用 “-v” 开关，它只显示实际写入的设置！要查看使用的完整配置，请给 testparm 添加 “-v” 参数。

### 20.3.2 快速配置验证

如果你在任何阶段需要故障排除，请首先回到这一点，验证 **testparm** 是否显示你期望的参数。为了给你一个来自个人经验的警告，尝试只是注释掉 *load printers* 参数。如果你的 2.2.x 系统表现得像我的一样，你会看到：

```bash
root# grep "load printers" /etc/samba/smb.conf
    #  load printers = Yes
    # This setting is commented out!!

root# testparm -v /etc/samba/smb.conf | egrep "(load printers)"
    load printers = Yes
```

我假设注释掉此设置应该能阻止 Samba 发布我的打印机，但它仍然发布了。花了一些时间才找出原因。但我再也不被迷惑了……至少不是被这个。

```bash
root# grep -Ai "load printers" /etc/samba/smb.conf
    load printers = No
    # The above setting is what I want!
    # load printers = Yes
    # This setting is commented out!
root# testparm -s -v smb.conf.simpleprinting | egrep "(load printers)"
    load printers = No
```

只有当参数明确设置为 `load printers = No` 时，Samba 才会符合我的意图。因此，我的强烈建议是：

- 永远不要依赖被注释掉的参数。
- 始终按你期望的行为显式设置参数。
- 使用 `testparm` 来发现可能不符合你意图的隐藏设置。

以下是最小化的配置文件：

```bash
root# cat /etc/samba/smb.conf-minimal
    [printers]
```

这个例子表明，你可以使用 `testparm` 测试任何 Samba 配置文件。实际上，我们鼓励你*不*更改你的工作系统（除非你确切知道自己在做什么）。不要依赖“更改仅在重启 smbd 后生效”的假设！事实并非如此。Samba 每 60 秒以及每次新的客户端连接时都会重新读取配置。你可能会面对那些你并未打算应用于生产客户端的更改。你现在会注意到一些更有趣的事情：`testparm` 有助于识别如果你使用这种最小化配置，Samba 打印配置将会是什么样。以下是你可以预期找到的内容：

```bash
root# testparm -v smb.conf-minimal | egrep "(print|lpq|spool|driver|ports|[D])"
    Processing section  "[printers]"
    WARNING: [printers] service MUST be printable!
    No path in service printers - using /tmp

    lpq cache time = 10
    load printers = Yes
    printcap name = /etc/printcap
    disable spoolss = No
    enumerports command =
```

