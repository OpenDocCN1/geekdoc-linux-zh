
访问 root 账户的一种略好的方法是使用 `su` 命令。如果无参数调用，`su` 会提示输入 root 密码，然后启动一个 root shell。root 权限将一直有效，直到你通过键入 `<Control-D>` 或 `exit` 命令来终止该 shell。`su` 不会记录以 root 身份执行的命令，但确实会创建一条日志条目，说明谁成为了 root 以及何时成为 root。

`su` 命令也可以替换 root 以外的其他身份。有时，重现或调试用户问题的唯一方法是 `su` 到他们的账户，以便重现问题出现的环境。

如果你知道某人的密码，可以通过执行 `su - 用户名` 直接访问该人的账户。与 `su` 到 root 一样，系统会提示你输入 `用户名` 的密码。选项 `-`（破折号）使 `su` 以登录模式启动 shell。登录模式的具体影响因 shell 而异，但通常会改变 shell 读取的启动文件的数量或身份。例如，`bash` 在登录模式下读取 `~/.bash_profile`，在非登录模式下读取 `~/.bashrc`。在诊断其他用户的问题时，尽可能重现其登录环境会很有帮助。

在某些系统上，root 密码允许 `su` 或 `login` 到任何账户。在其他系统上，你必须首先显式 `su` 到 root，然后再 `su` 到另一个账户；root 可以 `su` 到任何账户而无需输入密码。

养成键入 `su` 命令的完整路径名的习惯（例如，`/bin/su` 或 `/usr/bin/su`），而不是依赖 shell 为你找到该命令。这种预防措施可以让你免受任意名为 `su` 的程序的影响，这些程序可能已被偷偷放入你的搜索路径，意图窃取密码。⁶

在某些系统上，你必须是 `wheel` 组的成员才能使用 `su`。

我们认为 `su` 在很大程度上已被下一节所述的 `sudo` 所取代。`su` 最好保留给紧急情况使用。

### sudo：受限的 su

如果没有 RBAC 或 SELinux 等系统，很难在不让某人对系统拥有完全控制权的情况下，赋予其执行某单一任务（例如备份）的能力。而且，如果 root 账户由多个管理员使用，你实际上只能模糊地知道谁在使用它或他们做了什么。

解决这些问题最广泛使用的程序是 sudo，目前由 Todd Miller 维护。它在我们所有的示例系统上运行，也可以从 sudo.ws 获取源代码形式。

Solaris 的 `pfexec` 命令实现了一个类似于 sudo 的功能，该功能基于 Solaris 自己的 RBAC 系统。

`sudo` 将其参数作为要以 root（或其他受限用户）身份执行的命令行。`sudo` 查阅文件 `/etc/sudoers`，该文件列出了有权使用 sudo 的人员以及允许他们在每台主机上运行的命令。如果提议的命令被允许，`sudo` 会提示输入用户自己的密码并执行该命令。

在五分钟（可配置）内没有进一步的 sudo 活动后，额外的 sudo 命令可以在 `sudoer` 无需输入密码的情况下执行。此超时作为对具有 sudo 权限且让终端无人看管的用户的一种适度保护。

`sudo` 保存已执行命令行的日志，包括执行这些命令的主机、请求者、运行目录以及调用时间。此信息可以通过 syslog 记录，或放入你选择的文件中。我们建议使用 syslog 将日志条目转发到安全的主机。

以下是 randy 执行 `sudo /bin/cat /etc/sudoers` 的日志条目示例：

```
Dec 7 10:57:19 tigger sudo: randy: TTY=tty p0 ; PWD=/tigger/users/randy; USER=root ; COMMAND=/bin/cat /etc/sudoers
```

`sudoers` 文件的设计使得一个版本可以同时用于许多不同的主机。以下是一个典型示例：

```
### Define aliases for machines in CS & Physics departments
Host_Alias CS = tigger, anchor, piper, moet, sigi
Host_Alias PHYSICS = eprince, pprince, icarus

### Define collections of commands
Cmdn_Alias DUMP = /sbin/dump, /sbin/restore
Cmdn_Alias PRINTING = /usr/sbin/lpc, /usr/bin/lprm
Cmdn_Alias SHELLS = /bin/sh, /bin/tcsh, /bin/bash, /bin/ksh, /bin/bsh

### Permissions
mark, ed PHYSICS = ALL
h erb CS = /usr/sbin/tcpdump : PHYSICS = (operator) DUMP
lynda ALL = (ALL) ALL, !SHELLS
%wheel ALL, !PHYSICS = NOPASSWD: PRINTING
```

前五个非注释行定义了主机和命令组，这些组在文件后面的权限规范中被引用。这些列表可以是

有关 syslog 的更多信息，请参阅第 11 章。

- 5. Ubuntu Linux 甚至更进一步。默认情况下，系统没有有效的 root 密码，并且要求使用 sudo，本节后面将详细介绍。

- 6. 出于同样的原因，不要在 shell 的搜索路径中包含 `.`（当前目录）。虽然这样很方便，但此配置很容易无意中运行用户或入侵者作为陷阱留下的系统命令的 `特殊` 版本。当然，这条建议对 root 加倍适用。

虽然在规范中没有明确包含别名，但使用别名可以使 `sudoers` 文件更易于阅读和理解；它也使文件在未来更容易更新。也可以为用户集合以及可以运行命令的用户集合定义别名。

每一行权限规范都包含有关以下内容的信息：

- 该行适用的用户

- 该行应被遵守的主机

- 指定用户可以运行的命令

- 命令可以作为哪些用户执行

第一条权限行适用于 `PHYSICS` 组（`eprince`、`pprince` 和 `icarus`）中的机器上的用户 `mark` 和 `ed`。内置命令别名 `ALL` 允许他们运行任何命令。由于未在括号中指定用户列表，`sudo` 只会以 root 身份运行命令。

第二条权限行允许 `herb` 在 `CS` 机器上运行 `tcpdump`，在 `PHYSICS` 机器上运行与 `dump` 相关的命令。然而，`dump` 命令只能以 `operator` 身份运行，而不能以 root 身份运行。`herb` 实际输入的命令行将类似于

```
ubuntu$ sudo -u operator /usr/sbin/dump 0u /dev/sda1
```

用户 `lynda` 可以在任何机器上以任何用户身份运行命令，只是她不能运行几个常见的 shell。这是否意味着 `lynda` 真的不能获得 root shell？当然不是：

```
aix$ cp -p /bin/sh /tmp/sh
aix$ sudo /tmp/sh
```

一般来说，任何试图允许 `除……之外的所有命令` 的尝试都注定会失败，至少在技术意义上是如此。然而，以这种方式设置 `sudoers` 文件作为提醒，root shell 是不受欢迎的，仍然可能是值得的。

最后一行允许 `wheel` 组中的用户在除 `eprince`、`pprince` 和 `icarus` 之外的所有机器上以 root 身份运行 `lpc` 和 `lprm`。此外，运行这些命令不需要密码。

请注意，`/etc/sudoers` 中的命令使用完整路径名指定，以防止人们以 root 身份执行自己的程序和脚本。虽然上面没有示例，但也可以指定每个命令允许的参数。事实上，这种简单的配置只是 `sudoers` 文件中可用配置选项的冰山一角。

在 AIX 系统上，您可能希望在 `sudoers` 文件的 `defaults` 部分包含以下行。它可以防止 `sudo` 删除 `ODMDDIR` 环境变量，许多管理命令依赖该变量来指向 Object Data Manager 配置数据库。

```
Defaults env_keep = "ODMDDIR"
```

要修改 `/etc/sudoers`，您使用 `visudo` 命令，该命令会检查是否有人正在编辑该文件，在其上调用编辑器，然后在安装之前验证编辑后文件的语法。最后一步尤其重要，因为无效的 `sudoers` 文件可能会阻止您再次 `sudoing` 来修复它。

使用 `sudo` 有以下优点：

- 由于命令日志记录，问责制大大提高。

- 操作员可以在没有无限 root 权限的情况下完成任务。

- 真正的 root 密码可以只为一两个人所知。⁷

- 使用 `sudo` 比使用 `su` 或以 root 身份登录要快。

- 可以在无需更改 root 密码的情况下撤销权限。

- 维护着所有具有 root 权限用户的规范列表。

- root shell 被无人看管的风险更小。

- 可以使用单个文件控制整个网络的访问。
