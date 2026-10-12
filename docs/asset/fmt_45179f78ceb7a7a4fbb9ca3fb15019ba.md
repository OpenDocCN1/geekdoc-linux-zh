
示例 20.3.1 显示了一个简单的打印配置。如果你将其与自己的配置进行比较，你可能会发现操作系统厂商预先配置了其他参数。以下是对这些参数的讨论和解释。此示例没有使用很多参数。然而，在许多环境中，这些足以提供一个有效的 `smb.conf` 文件，使所有客户端都能进行打印。

这只是一个配置示例。Samba 会为所有配置参数分配默认值。默认值是保守且合理的。当在 `smb.conf` 文件中指定某个参数时，这将覆盖默认值。以 root 身份运行时，`testparm` 实用工具能够报告所有设置，包括默认设置以及 `smb.conf` 文件设置。`Testparm`

### 示例 20.3.1 使用 BSD 打印的简单配置

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

若要查看 Samba 中所有（或至少大多数）与打印相关的设置，包括隐式使用的设置，请尝试下面概述的命令。该命令在 `testparm` 的输出中搜索 `lp`、`print`、`spool`、`driver`、`ports` 和 `l` 的所有出现。这提供了对正在运行的 `smbd` 打印配置的便捷概览。该命令不会显示单独创建的打印机共享或其可能使用的暂存路径。以下是我的 Samba 设置输出，其中显示了示例 20.3.1 中的设置：

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
> Samba-3 中的 `testparm` 行为与 2.2.x 中的不同：如果不使用 “-v” 开关，它只显示实际写入的设置！要查看使用的完整配置，请给 testparm 添加 “-v” 参数。

### 20.3.2 快速配置验证

如果你在任何阶段需要故障排除，请首先回到这一点，验证 `testparm` 是否显示你期望的参数。为了给你一个来自个人经验的警告，尝试只是注释掉 `load printers` 参数。如果你的 2.2.x 系统表现得像我的一样，你会看到：

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

`testparm` 发出了两个警告：

- 我们未将 `[printers]` 部分指定为可打印。
- 我们未告知 Samba 使用哪个暂存目录。

然而，这不是致命的错误，Samba 会使用默认值，这些值也能正常工作。请务必不要依赖此行为，也不要使用此示例。包含此内容的目的是为了提醒你在设计和指定配置时要格外小心，以确保其精确满足你的需求。由于 Samba 可能基于不同的编译时选项进行构建，对于某些给定的参数，你的系统上的结果可能会有所不同。警告：不要在有效行的末尾添加注释符号。这将导致该参数被忽略（就像你把注释符号放在行首一样）。起初，我将其视为我使用的 Samba 版本中的一个 bug。但手册页明确指出：参数值内部的空白字符将原样保留。这意味着，对于例如由以下各行组成的行：

```
# This defines LPXng as the printing system
printing = iprng
```

系统将等号后面的整个字符串视为你想要定义的值。这是一个无效值，将被忽略，并会使用默认值代替。
