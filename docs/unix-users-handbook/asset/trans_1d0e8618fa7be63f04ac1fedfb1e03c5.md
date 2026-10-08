

POSIX 命令是本章中 UNIX 和 Windows 部分的核心内容。不过，我认为涵盖其他 Windows 命令能让 UNIX 系统管理员对可用的 Windows 系统管理命令类型有所了解。

## Windows 命令行

整个 Windows 操作系统都是基于通过图形用户界面执行系统管理任务的。那么，为什么我要包含一个关于命令行的章节呢？嗯，我们中的许多人使用过这样的操作系统，在这些系统中，绝大多数的系统管理工作都是在命令行上完成的——而旧习惯往往难以改变。

本章的目的是展示一些在命令行上发出的有用命令。然后你可以决定，使用这样的命令是否有助于你的 Windows 服务器的管理，或者你是否希望仅使用 Windows 的图形用户界面。

## NET 命令

本节介绍了一些 Windows 的 **net** 命令。以下是常用 **net** 命令的列表及其简要说明：

- **net accounts**
  用于维护用户账户数据库。
- **net computer**
  用于将计算机添加到域数据库或从中删除。
- **net config server**
  显示或更改执行该命令的服务器服务的设置。
- **net config workstation**
  显示或更改执行该命令的工作站服务的设置。
- **net continue**
  重新激活已通过 **net pause** 命令挂起的 Windows 服务。
- **net file**
  用于网络文件操作，例如列出 ID 号、关闭共享文件、移除文件锁等。
- **net group**
  用于在服务器上添加、显示或修改全局组。
- **net help**
  显示任何 net 命令的帮助选项列表。
- **net helpmsg**
  显示 Windows 网络消息的解释，如错误、警告和警报。
- **net localgroup**
  用于修改计算机上的本地组。

| 命令 | 描述 |
|---|---|
| **net name** | 用于在计算机上添加或删除“消息名称”，这是消息发送的目标名称。 |
| **net print** | 用于列出打印作业和共享队列。 |
| **net send** | 向网络上的其他用户、计算机和“消息名称”发送消息。 |
| **net session** | 用于列出或断开计算机与网络上其他计算机之间的会话。 |
| **net share** | 将服务器的资源与网络上的其他计算机共享。 |
| **net start** | 用于启动 *server* 等服务。 |
| **net statistics** | 显示本地工作站或服务器服务的统计日志。 |
| **net stop** | 用于停止 *server* 等服务。 |
| **net time** | 将计算机时钟与域上的另一台计算机同步。 |
| **net use** | 显示、连接或断开计算机与共享资源的连接。 |
- **net user**
  创建或修改用户账户。
- **net view**
  列出计算机上正在共享的资源。

以下是对部分 NET 命令的简要描述及使用示例。

许多描述都包含了通过输入命令名称后跟 /? 获得的命令摘要。例如，要获取 NET ACCOUNTS 命令的摘要，你需要输入以下内容：

```
C:\ NET ACCOUNTS /?
```

你还可以通过输入 HELP 和命令名称来获取详细的帮助信息，如下例所示：

```
C:\ HELP NET ACCOUNTS
```

### NET ACCOUNTS

**NET ACCOUNTS** - 维护用户账户数据库。

以下是 **NET ACCOUNTS** 命令的摘要。

```
C:\ NET ACCOUNTS /?
NET ACCOUNTS  [/FORCELOGOFF:{minutes | NO}]  [/MINPWLEN:length]
              [/MAXPWAGE:{days | UNLIMITED}]  [/MINPWAGE:days]
              [/UNIQUEPW:number]  [/DOMAIN]
NET ACCOUNTS [/SYNC]
```

以下是一些常用选项：

- `/DOMAIN` 
  在域控制器上而非当前计算机上执行指定操作。
- `/FORCELOGOFF` 
  显示行号以及输出行。（注：原文此处描述可能与常规用法不符，但依原文翻译）
- `/MINPWLEN:length` 
  指定密码的最小字符数，使用 *length* 表示。
- `/MAXPWAGE:days` 
  指定密码有效的最大 *days* 天数，或使用 *unlimited* 选项指定密码有效期无限制。
- `/MINPWAGE:days` 
  指定在用户允许更改密码之前必须经过的最小 *days* 天数。
- `/UNIQUEPW:number`
  用户密码必须在由 *number* 指定的更改次数内保持唯一。
- `/SYNC`
  同步账户数据库。

以下示例显示了未指定任何选项的 **NET ACCOUNTS**：

```
C:\ NET ACCOUNTS

Force user logoff how long after time expires?:	Never
Minimum password age (days):	0
Maximum password age (days):	42
Minimum password length:	0
Length of password history maintained:	None
Lockout threshold:	Never
Lockout duration (minutes):	30
Lockout observation window (minutes):	30
Computer role:	BACKUP
Primary Domain controller for workstation domain: \\NISDEV

The command completed successfully.
```

现在，我们将使用 *MINPWLEN* 选项发出 **NET ACCOUNTS**，将最小密码长度更改为五个字符：

```
C:\ NET ACCOUNTS /MINPWLEN:5

The request will be processed at the primary domain controller for domain NSDNS

The command completed successfully.
```

再次发出未指定选项的 **NET ACCOUNTS** 将反映新的最小密码长度：

```
C:\ NET ACCOUNTS

Force user logoff how long after time expires? Never
Minimum password age (days): 0
Maximum password age (days): 42
Minimum password length: 5
Length of password history maintained: None
Lockout threshold: Never
Lockout duration (minutes): 30
Lockout observation window (minutes): 30
Computer role: BACKUP
Primary Domain controller for workstation domain: \\NISDEV
The command completed successfully.
```

### NET COMPUTER

**NET COMPUTER** - 将计算机添加到域数据库或从中删除。

以下是 **NET COMPUTER** 命令的摘要：

```
C:\ NET COMPUTER /?  
NET COMPUTER \\ computername ({/ADD | /DEL})
```

以下是一些常用选项：

- `\\ computername`
  要添加或删除的计算机名称。
- `/ADD`
  添加计算机。
- `/DEL`
  删除计算机。

以下示例显示了使用 /ADD 选项添加计算机：

```
C:\ NET COMPUTER \\SYSTEM2 /ADD

The request will be processed at the primary domain controller for domain NSDNIS.

The command completed successfully.
```

### NET CONFIG SERVER

**NET CONFIG SERVER** - 作为管理员组成员，你可以更改服务的设置。

以下是 **NET CONFIG SERVER** 命令的摘要。

```
C:\ NET CONFIG SERVER /?
NET CONFIG SERVER [ /AUTODISCONNECT:time]
[/SRVCOMMENT:"text"]
[/HIDDEN: {YES | NO}]
```

以下是一些常用选项：

- *AUTODISCONNECT:time*
  使用 *time* 指定在断开非活动账户之前经过的分钟数。
- *SRVCOMMENT:"text"*
- *HIDDEN: {YES|NO}*

### NET CONTINUE

**NET CONTINUE** - 重新激活此前已通过 **NET PAUSE** 挂起的 Windows 服务。

以下是 **NET CONTINUE** 命令的摘要。

```
C:\> NET CONTINUE /?
NET CONTINUE service
```

你可以分别使用 **NET PAUSE** 和 **NET CONTINUE** 命令暂停和继续许多 Windows 服务。以下示例显示了使用 **NET PAUSE** 命令暂停 **NET LOGON** 服务，然后使用 **NET CONTINUE** 命令重新启动它。

图 19-1 是来自某系统的 *Services*（服务）对话框，显示了系统中正在运行的一些服务。

![](img/75f39fc91296b889c0653851accdfd46_1297_0.png)

图 19-1 显示已启动 Net Logon 的服务对话框

现在我们使用 **NET PAUSE** 命令暂停 *Net Logon* 服务：

```
C:\NET PAUSE NtLOGON

The Net Logon service was paused successfully.
```

图 19-2 显示了 *Services* 对话框，表明 *Net Logon* 服务确实已被暂停。

