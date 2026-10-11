
命令执行成功。

你现在可以在 Windows 系统上查看此共享并将其映射到驱动器，如图 27-3 所示。

![](img/6969df54e516231f8e64fd1177ac1127_1703_0.png)

图 27-3 Windows 资源管理器显示新共享 HOME

在本章中，我只介绍了 Advanced Server/9000 功能的一个部分。我介绍了将运行 Advanced Server/9000 的 UNIX 系统作为备用域控制器、将连接 UNIX 的打印机与 Windows 网络共享以及将连接 UNIX 的磁盘与 Windows 网络共享。这些是 Advanced Server/9000 的一些常见用途。几乎在 Windows 系统上可以做的一切事情都可以用 Advanced Server/9000 完成，因此不要局限于本章涵盖的功能。

# 第 28 章 Windows 命令行：NET 命令、POSIX 工具及其他

UNIX 系统管理员入门

UNIX 系统管理主要通过命令行完成。虽然有非常出色的系统管理接口，可以通过这些接口执行许多例行的系统管理任务；然而，对于大多数 UNIX 系统管理员来说，在使用任何图形化工具之前，他们仍然习惯使用命令行。Windows 的情况则相反。在 Windows 中，大多数系统管理功能是通过“点并点击”完成的。尽管如此，在 Windows 中，你也可以通过命令行执行许多功能。在本章关于 UNIX 和 Windows 互操作的章节中，我将泛介绍 Windows 命令行，以及一组可以让你在 Windows 中获得 UNIX 功能的 POSIX 工具。

我将从 Windows 的 `NET` 命令开始，这些是用于 Windows 的系统管理命令。然后，我将介绍可以在 Windows 命令行运行的 POSIX 命令，它们可以在 Windows 中为你提供 UNIX 功能，例如 `grep` 等。最后，我将介绍一些额外的 Windows 命令，用于执行如备份和在特定时间运行命令等任务。

![](img/6969df54e516231f8e64fd1177ac1127_1706_0.png)

## POSIX 命令真正构成了本章中 UNIX 和 Windows 部分

然而，我认为，介绍其他 Windows 命令可以让 UNIX 系统管理员对可用的 Windows 系统管理命令类型有一个直观的了解。

## Windows 命令行

整个 Windows 操作系统基于通过图形用户界面执行系统管理任务。既然如此，我为什么还要包含一个关于命令行的章节呢？嗯，我们中的许多人使用过大部分系统管理工作都在命令行完成的操作系统——而且旧习性难以改掉。

本章的目的是演示一些在命令行发出的有用命令。然后你可以决定使用此类命令是否对你的 Windows 服务器管理有帮助，或者你是否希望只使用 Windows 的图形用户界面。

## NET 命令

本节描述了 Windows 的某些 `net` 命令。以下是一些常用 `net` 命令的列表以及每个命令的简要解释：

- `net accounts`：用于维护用户账户数据库。
- `net computer`：用于从域数据库中添加或删除计算机。

### `net config server`

显示或更改执行命令的服务器服务的设置。

### `net config workstation`

显示或更改执行命令的工作站服务的设置。

### `net continue`

重新激活通过 `net pause` 命令挂起的的 Windows 服务。

### `net file`

用于网络文件操作，例如列出 ID、关闭共享文件、移除文件锁等。

### `net group`

用于在服务器上添加、显示或修改全局组。

### `net help`

显示任何 `net` 命令的帮助选项列表。

### `net helpmsg`

显示 Windows 网络消息的解释，例如错误、警告和警报。

### `net localgroup`

用于修改计算机上的本地组。

### `net name`

用于在计算机上添加或删除“消息名称”，即发送消息的名称。

### `net print`

用于列出打印作业和共享队列。

### `net send`

向网络上的其他用户、计算机和“消息名称”发送消息。

### `net session`

用于列出或断开计算机与其他网络计算机之间的会话。

### `net share`

与网络上的其他计算机共享服务器资源。

### `net start`

用于启动如 `server` 等的服务。

### `net statistics`

显示本地 Workstation 或 Server 统计日志。

### `net stop`

用于停止如 `server` 等的服务。

### `net time`

将计算机的时钟与域内的另一计算机同步。

### `net use`

显示、连接或断开带有共享资源的计算机。

### `net user`

创建或修改用户账户。

### `net view`

列出计算机上共享的资源。

以下是某些 NET 命令的简要描述及其用法示例。

许多描述都包含了通过输入命令名后跟 `/?` 获取的命令摘要。例如，要获取 `NET ACCOUNTS` 命令的命令摘要，你可以输入以下内容：

```
C:\ NET ACCOUNTS /?
```

你也可以通过输入 `HELP` 加命令名来获取详细的帮助信息，如下例所示：

```
C:\ HELP NET ACCOUNTS
```

## NET ACCOUNTS

`NET ACCOUNTS` 维护用户账户数据库。

以下是 `NET ACCOUNTS` 命令的摘要：

```
C:\ NET ACCOUNTS /

NET ACCOUNTS [/FORCELOGOFF:{minutes | NO}] [/MINPWLEN:length]

[/MAXPWAGE:days | UNLIMITED}] [/MINPWAGE:days]

[/UNIQUEEPW:number] [/DOMAIN]

NET ACCOUNTS [/SYNC]
```

以下是一些常用选项：

- `/DOMAIN`
在域控制器而不是当前计算机上执行指定的操作。

- `/FORCELOGOFF`
显示行号以及输出行。

- `/MINPWLEN:length`
指定密码长度的最小字符数。

- `/MAXPWAGE:days`
指定密码有效的最大天数，或使用 `unlimited` 选项指定对密码有效性无限制。

- `/MINPWAGE:days`
指定用户更改密码之前必须经过的最小天数。

```
/UNIQUEPW:number
```
用户密码对于指定的 `number` 次更改必须是。

```
/SYNC
```
同步账户数据库。

以下是在未指定选项的情况下执行 `NET ACCOUNTS` 的示例：

```
C:\ NET ACCOUNTS

Force user logoff how long after expires?: Never

Minimum password age (days): 0

Maximum password age (days): 42

Minimum password length: 0

Length of password history maintained: None

Lockout threshold: Never

Lockout Duration (minutes): 30

Lockout observation window (minutes): 30

Computer role: BACKUP

Primary Domain controller for workstation domain: \\NISDEV

The command completed.
```

现在我们将带有 `MINPWLEN` 选项的 `NET ACCOUNTS` 将最小密码长度改为五个字符：

```
C:\ NET ACCOUNTS /MINPWLEN:5
```

请求将在 `NSDNIS` 域控制器上处理。
命令执行完成。

在未指定选项的情况下执行 `NET ACCOUNTS` 反映了新的密码长度：

```
C:\ NET ACCOUNTS

Force user logoff how long after expires?: Never

Minimum password age (days): 0

Maximum password age (days): 42

Minimum password length: 5

Length of password history maintained: None

Lockout threshold: Never

Lockout Duration (minutes): 30

Lockout observation window (minutes): 30

Computer role: BACKUP

Primary Domain controller for workstation domain: \\NISDEV
```
