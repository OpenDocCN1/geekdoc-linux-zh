
| | 资源 | 备注 |
| --- | --- | --- |
| ADMINS | `C:\OPT\ASU\LANMAN` | 管理共享 |
| IPCS | | IPC 共享 |
| CS | `C:\` | 根共享 |
| DS | `C:\VAR\OPT\ASU\LANMAN\SHARES` | 系统根共享 |
| ASTOOL | `C:\VAR\OPT\ASU\LANMAN\SHARES...` | 高级服务器工具 |
| DOSUTIL | `C:\VAR\OPT\ASU\LANMAN\SHARES...` | DOS 实用程序 |
| HOME | `C:\HOME:` | |
| NETLOG | `C:\VAR\OPT\ASU\LANMAN\SHARES...` | 登录脚本目录 |
| PATCHES | `C:\VAR\OPT\ASU\LANMAN\SHARES...` | 客户端补丁 |
| PRINTLOG | `C:\VAR\OPT\ASU\LANMAN\SHARES...` | LP 打印机消息 |
| USERS | `C:\HOME\LANMAN` | 用户目录 |
| LASER | `laser` | 已打印 |

命令成功完成。

# 第 13 章 Windows NT 与 UNIX 的互操作性：适用于 UNIX 的高级服务器

现在你可以在 Windows NT 系统上查看此共享并将其映射到驱动器，如图 13-3 所示。

![](img/3ab707b472189378db808b8f9502ab8c_1069_0.png)

图 13-3 Windows NT 资源管理器显示新共享 HOME

在本章中，我只涵盖了 Advanced Server/9000 功能的一小部分。我涵盖了使用运行 Advanced Server/9000 的 UNIX 系统作为备份域控制器、与 Windows NT 网络共享连接 UNIX 的打印机，以及与 Windows NT 网络共享连接 UNIX 的磁盘。这些都是 Advanced Server/9000 的一些常见用途。你可以在 Windows NT 系统上执行几乎所有操作都可以通过 Advanced Server/9000 来完成，因此不要仅局限于本章涵盖的功能。

# 第 14 章 Windows NT 命令行：NET 命令、POSIX 实用程序及其他

面向 UNIX 系统管理员的介绍

UNIX 系统管理主要通过命令行完成。虽然有非常好的系统管理接口，可以通过这些接口执行许多例行的系统管理任务；然而，对于大多数 UNIX 系统管理员来说，在使用任何图形化工具之前，仍然在使用命令行。Windows NT 情况则相反。在 Windows NT 中，大多数系统管理功能都是通过“点和点击”完成的。然而，在 UNIX 和 Windows NT 互操作性章节中，有很多功能可以从命令行执行；我将泛介绍 Windows NT 命令行，以及一组专门在 Windows NT 中提供 UNIX 功能的 POSIX 实用程序。

我将从 Windows NT "`NET`" 命令开始，这些是 Windows NT 的系统管理命令。然后我将介绍可以在 Windows NT 命令行运行的 POSIX 命令，这些命令在 Windows NT 中为你提供 UNIX 功能，例如 `grep`、`ls` 等。接着，我将涵盖一些你可以执行的额外 Windows NT 命令，用于执行备份和在特定时间运行命令等任务。

POSIX 命令真正构成了本章的 UNIX 和 Windows NT 部分。然而，我认为涵盖其他 Windows NT 命令可以帮助 UNIX 系统管理员对可用的 Windows NT 系统管理命令类型有一个大致的了解。

## Windows NT 命令行

整个 Windows NT 操作系统基于基于图形用户界面执行管理任务的。那么，为什么我还要包含一个关于命令行的章节呢？嗯，我们许多人都使用过大部分功能都是命令行的操作系统。本章的目的是证明使用命令行对 Windows NT 是否有帮助。

## NET 命令

本节描述了一些 `net` 命令。以下是某些常用命令的列表：

- `net accounts`: 维护用户账户数据库。
- `net computer`: 从域中添加或删除计算机。
- `net config`: 显示或更改服务器设置。
- `net config`: 显示或更改工作站设置。
- `net file`: 用于网络文件操作。
- `net group`: 用于修改全局组。
- `net help`: 显示任何命令的帮助。
- `net helpmsg`: 显示 Windows NT 消息解释。
- `net localgroup`: 用于修改本地组。
- `net name`: 接收消息的名称。
- `net print`: 列出打印作业和队列。
- `net send`: 向其他用户、计算机发送消息。
- `net session`: 列出计算机与其他计算机之间的会话。
- `net share`: 与计算机共享服务器资源。
- `net start`: 用于启动服务。
- `net statistics`: 显示本地站或服务器统计信息。
- `net stop`: 用于停止服务。
- `net time`: 将计算机的时钟与另一台计算机同步。
- `net use`: 显示或连接计算机共享资源。
- `net user`: 创建或修改用户账户。
- `net view`: 列出计算机共享资源。

以下是某些 NET 命令的简要描述及其用法示例。许多描述包含了通过在命令名后加 `?` 获取的命令摘要。例如，要获取 `NET ACCOUNTS` 命令的摘要，你需要输入：

```
C:\ NET ACCOUNTS /?
```

你也可以通过输入 `HELP` 和命令名来获取详细帮助信息，如下所示：

```
C:\ HELP NET ACCOUNTS
```

### NET ACCOUNTS

`NET ACCOUNTS` - 维护用户账户数据库。

此处是 `NET ACCOUNTS` 命令的摘要。

```
C:\ NET ACCOUNTS /?

NET ACCOUNTS [/FORCELOGOFF:{minutes | NO}] [/MINPWLEN:length]

[/MAXPWAGE:days | LIMITED)] [/MINPWAGE:days]

[/UNIQUEFPW:number] [/DOMAIN]

NET ACCOUNTS [/SYNC]
```

常用选项如下：

| `/DOMAIN` | 在域控制器而非当前计算机上执行指定的操作。 |
| `/FORCELOGOFF` | 输出行将显示行号。 |
| `/MINPWLEN:length` | 指定密码的最小字符长度。 |
| `/MAXPWAGE:days` | 指定密码有效的最大天数，或使用无限选项指定对密码有效期无限制。 |
| `/MINPWAGE:days` | 指定用户允许更改密码之前必须经过的最少天数。 |

#### NET ACCOUNTS（网络账户）

`/UNIQUEEPW:number` 在指定的更改次数内，用户密码必须是唯一的。

`/SYNCH` 同步账户数据库。

以下示例显示了未指定选项的 `NET ACCOUNTS`：

```
C:\ NET ACCOUNTS

时间过期后多久强制用户注销?: 从不

最小密码年龄（天）:0

最大密码年龄（天）:42

最小密码长度: 0

维护的密码历史长度: 无

锁定阈值: 从不

锁定时间（分钟）:30

锁定观察窗口（分钟）:30

计算机角色: 备份

工作站所在域的主域控制器: \NISDEV

命令执行成功。
```

现在我们现在执行带有 `/MINPWLEN` 选项的 `NET ACCOUNTS`，将最小密码长度更改为五个字符：

```
C:\ NET ACCOUNTS /MINPWLEN: 5

请求将在域 NSDNIS 的主域控制器上处理

命令执行成功。
```

重新执行不带选项的 `NET ACCOUNTS` 将反映出新的最小密码长度：

```
C:\ NET ACCOUNTS

时间过期后多久强制用户注销?: 从不

最小密码年龄（天）:0

最大密码年龄（天）:42

最小密码长度: 5

维护的密码历史长度: 无

锁定阈值: 从不

锁定时间（分钟）:30

锁定观察窗口（分钟）:30

计算机角色: 备份

工作站所在域的主域控制器: \NISDEV

命令执行成功。
```

### NET COMPUTER（网络计算机）

`NET COMPUTER` - 从域数据库中添加或删除计算机。

以下是 `NET COMPUTER` 命令的摘要：

```
C:\ NET COMPUTER /?

NET COMPUTER \\computername (/ADD | /DEL)
```

以下是一些常用的选项：

| `\\computename` | 要添加或删除的计算机名称。 |
|---|---|
| `/ADD` | 添加计算机。 |
| `/DEL` | 删除该计算机。 |

以下示例显示了使用 `/ADD` 选项添加计算机。

```
C:\ NET COMPUTER \\SYSTEM2 /ADD
```

请求将在域 NSDNIS 的主域控制器上处理。
命令执行成功。
