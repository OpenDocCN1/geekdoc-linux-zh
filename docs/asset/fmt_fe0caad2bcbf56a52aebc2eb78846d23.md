
`C:\` `net use` `\ststephen`

```
### 文本模式网络命令

你可以从命令行界面连接到共享目录。在功能上，该过程与映射网络驱动器的方式相似。关键命令是：

```

`C:\` `net view`

`C:\` `net use`

```
### 查看计算机

正如你使用`smclient`命令来查看域上的计算机一样，你可以在 MS-DOS 提示符中使用`net view`命令。

> 有时当你从提示符运行`net`命令时，可能会得到类似“拒绝访问”的错误信息。如果你的连接是通的，不要让这让你气馁。如果你刚刚登录计算机，计算机之间可能需要一两分钟才能找到彼此。

![](img/6ee4859e736a0839007ea9afb576c195_213_0.png)

如图 40 所示，`net view`命令返回你的工作组或域中当前计算机的列表。`net view /domain:darkstar`命令有些反直觉；它允许我查看我的`darkstar`点对点工作组中的计算机。如果`darkstar`是一个域的名称，该命令同样有效。

> 如果你是另一个工作组或域的成员，可以使用以下命令查看我 Grateful 域中的计算机：`net view /domain:grateful`。

![](img/6ee4859e736a0839007ea9afb576c195_213_1.png)

> 你可能会注意到 STSTEHEN 计算机同时出现在我的域和工作组的浏览列表中。这只是告诉我最近将 STEPHEN 从工作组移动到了域（或反之）。

你还可以使用`net view`命令浏览域或工作组中任何可访问计算机的共享目录。例如，我可以使用以下命令查看我的名为`nopopaws:`的 Linux 域成员服务器上的共享目录：

```
C:\ net view \nopopaws
```

## 194 面 Windows 管理员的 Linux 迁移

```
C:\WINDOWS\System32> command
C:\DOCUMENT\I\DONNA\DESKTOP\>net view

Server Name Renark

\\ACCESS             Windows XP Pro Workstation
\\COSMOS               PDC from a Samba Server
\\DRIS                 experimental samba server
\\MOUSS                
\\RIPPLE             Windows 95 Workstation
\\STEPHEN             W2008R2
\\VERNON             

The command completed successfully.

C:\DOCUMENT\I\DONNA\DESKTOP\>net view /domain:darkstar

Server Name Renark

\\REDUBEN             win98se
\\STEPHEN             W2008R2

The command completed successfully.
```

**图 40.** 来自 DOS 提示符的域视图和组成员。

### 挂载共享目录

我已经向你展示了通过 GUI 将远程计算机的共享目录挂载到 Windows 驱动器的方法。在第 5 章中，你学习了如何将远程计算机的共享目录挂载到 Linux 目录。你可以将在本节中看到的命令整合到登录批处理文件中，以便在用户登录域时自动运行这些命令。

> 如本章早些介绍，批处理文件位于 PDC 上，由`[netlogon]`共享定义。

如果你想从域成员服务器挂载目录，你需要以目标用户的身份登录到工作站。你将能够使用以下命令轻松地挂载所需的共享目录：

```
C:\> net use L: \\nopaws\tmp

The command completed successfully.
```

在这种情况下，我将来自`nopaws`成员服务器的`[imp]`共享目录挂载到了 Microsoft Windows 驱动器 D: 上。

> 有时在域中，用户名和密码无法及时到达服务器；你可能需要重新输入一次你的域用户名和密码。如果在登录批处理文件中发生此类情况，你可能需要直接从 Linux PDC 的`[netlogon]`共享运行该批处理文件，或者手动重新连接共享驱动器。

如果你想从对等网络工作组（Workgroup）中的计算机挂载共享目录，命令是相似的。例如，我共享了我名为`reuben`的 Windows 98 计算机上的“我的文档”目录。我可以使用以下命令将其挂载到 M: 盘（不用担心“密码无效”错误消息）：

```
C:\ net use M: \reuben\my documents
```

针对`\reuben\my documents`的密码无效。要连接`reuben`到驱动器，请按回车键或输入新用户名：输入`'reuben'`的密码以连接到`'reuben'`。命令成功完成。`net use`命令首先尝试你登录工作站时使用的用户名和密码。除非完全匹配，否则你将看到“密码无效”的错误消息。因为`reuben`是对等网络工作组中的 Windows 98 计算机，因此不需要用户名。在提示用户名时，不要输入任何内容。在提示密码时，输入共享目录的只读或完整密码。观察我是如何使用双引号来确保 Windows 读取`"My Documents"`的完整名称的。否则，由于`"My Documents"`包含空格，`net use`命令将寻找名为`"My"`的共享目录。

### 故障排除

每当 Samba 启动时都会记录在日志中。每当出现问题时，都会记录在日志中。每当另一台计算机连接到 Samba 服务器时，都会记录在日志中。在 Red Hat Linux 中，日志文件存储在`/var/log/samba`。但在查看日志之前，还有语法问题。

### Samba 语法

检查 Samba 配置文件`smb.conf`的语法非常简单。你只需要使用`testpar`。如果你其中一个变量出现问题，它将显示在输出中。例如，如果我在`smb.conf`中拼写错误，我可能会看到以下内容：

```
### testpar -x | more

Load config files from /etc/samba/smb.conf

Unknown parameter: "workgrou"

Ignoring unknown parameter "workgrou"

Processing section [homes]

Processing section [printers]

Processing section [tmpl]

Processing section [shared]

Processing section [project]

Loaded services OK
```

我使用`testpar -x`命令显示所有与默认值不同的 Samba 变量，并使用`| more`使我可以一次滚动查看变量列表。`testpar`识别出了我`smb.conf`文件中的语法错误；我拼写错误了`workgroup`。当你按下回车键时，`testpar`会逐页滚动显示 Samba 变量。如果你漏掉了`-x`开关，`testpar`将列出与你的 Samba 配置相关的所有变量。尝试一下；你会发现这是一个很长的列表。

### Samba 日志

如果 Samba 出现问题，且`smb.conf`文件的语法检查通过，下一步是检查日志。典型的 Samba 问题包括密码无效、Winbind 等服务未运行以及浏览器无法工作。Linux 日志文件存储在`/var/log`；Samba 日志文件存储在`/var/log/samba`。对这些文件的访问限于 Linux PDC 上的`root`用户。查看图 41 中的这些文件。如你所见，它包含了我连接到此 Samba 服务器的每台计算机命名的日志。

```
root@cosmic]# cd /var/log/samba/

root@cosmic]# ls

allaccess.log delilah.log reuben.1 smb.log.2
allaccess.1 localhost.log reuben.2 smb.log.3
allaccess.2 localhost.log reuben.3 smb.log.4
allaccess.3 log_smbd reuben.4 ststpen.1
allaccess.4 log_smbd r8.5 ststpen.2
cosmic.1 log_winbind r9.2 ststpen.3
cosmic.2 log_winbind r9.3 ststpen.4
cosmic.3 log_winbind r9.4 ststpen.5
cosmic.4 log_winbind ripple.1
```
