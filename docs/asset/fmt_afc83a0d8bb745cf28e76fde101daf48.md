
**图 2-13** 在此示例中，用户输入 `beginningunix` 作为用户名并按下回车（或 Return）。屏幕上出现密码请求（第 4 行）。用户为账户输入了错误的密码，系统用 `Login incorrect` 语句响应，然后提供了另一次登录机会。这次用户输入了正确的用户名和密码。系统随后显示用户上次登录的时间，并提供命令行 shell 的访问权限。

（注：由于源文本中存在严重的逻辑重复，译文已在保留关键信息的基础上进行了去重处理。）

# 第 2 章

```
Terminal - ttypl
[DARWIN-~] beginningunix hostname
DARWIN
[DARWIN-~] beginningunix ssh 192.168.1.65
The authenticity of host '192.168.1.65' (RSA-2048) can't be established.
RSA key fingerprint is MD5:63:55c2ebf:76:dbbe:98:d4:8f.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.1.65' (RSA) to the list of known hosts.
[beginningunix@linux beginningunix]$
[beginningunix@linux beginningunix]$
linux
[beginningunix@linux beginningunix]$ _
```

图 2-15

当你第一次使用 `ssh` 连接到远程系统时，系统会提示你接受远程系统的密钥（或标识），如第 11 行所示（这仅在第一次连接到该系统时发生）。你可以与远程系统管理员确认密钥。如果有人更改了系统或你伪装成服务器使用 `ssh`（试图窃取你的凭据），你将收到警告。

在输入用户账户的密码后，你将进入远程系统的 shell。之所以没有询问你的用户名，是因为除非你指定了不同的用户名，否则 `ssh` 命令会发送你在本地系统上登录的用户名。现在执行 `hostname`，你会发现你确实远程登录到了 `linux` 机器。

当你运行 `ssh` 时，`ssh` 假设你想使用本地系统上使用的用户名登录到远程系统。由于命名规范不同，你在不同系统上的用户名并不总是相同的，因此你在一个系统上可能是 `jdoe`，在另一个系统上可能是 `johnd`，而在第三个系统上可能是 `jd1234`。如果你需要不同的用户名登录远程系统，请使用以下语法：

```
ssh username@hostname
```

如果你以 `jdoe` 身份登录系统 `darwin`，并想以用户 `jdoe` 的身份远程登录系统 `192.168.1.65` (linux)，输入：

```
ssh jdoe@192.168.1.65
```

记住，`hostname` 可以是实际名称（如 `boardroom`），也可以 IP 地址（如 `192.168.1.58`）。

# 初步

`ssh` 提供从本地到远程服务器以及反向的加密，在会话期间提供了更高的安全性，但由于系统限制或策略，`ssh` 可能并不总是可用。在这种情况下，你通常需要使用 `telnet`，它提供了相同的功能，但对本地和远程系统之间传输的数据没有加密。`telnet` 是一个旧的协议，我们在当今注重安全的环境中使用它，是因为它在许多主流平台（包括 Microsoft Windows 和 DOS）上默认可用。你使用 `telnet` 的方式非常像 `ssh`，只是它会提示你输入用户名和密码（`telnet` 并不总是假设你想登录当前用户）。要从 `darwin` 机器输入到 `solaris` 机器 (`192.168.1.60`)，你需要输入：

```
telnet solaris
```

或者

```
telnet 192.168.1.60
```

如图 2-16 所示。

图 2-16

在图 2-16 中，运行 `hostname` 来确定当前系统的主机名 (`DARWIN`)，然后执行 `telnet 192.168.1.60` 命令。系统请求用户密码，提供密码后，会显示最后登录和横幅信息。再次运行 `hostname` 会产生预期的结果：`solaris`。用户现在可以运行命令，就像他们的屏幕和键盘直接连接到 `solaris` 系统一样。

23

# 第 2 章

### Shell

登录后，你将进入由系统管理员为你预定义的 shell。（Shell 在第 1 章中介绍过。）将显示一个命令行界面或图形用户界面 (GUI)，让你能够访问 shell。图 2-17 显示了一个典型的命令行界面。

如果你使用 GUI，请找到提供 shell 访问的 `xterm` 或 `console` 应用程序。现在你已经准备好输入本书书中讨论的所有命令了。

# 销销

当你使用交互式登录完成系统上需要的工作后，你需要以受控制且有序的方式退出系统，以防止进程或作业意外终止。`exit` 命令会结束你的 shell 会话（在 bash 或 c shell 中可以使用 `logout` 命令，如第 5 章所述）。这会关闭你登录的窗口或完全结束会话。如果你使用 GUI，这通常是一个注销会话的按钮或键序列。

### 系统关机

Unix 是多用户、多任务系统，因此通常一直有很多进程或程序在运行。文件系统需要同步，直接断电会导致文件系统问题并影响系统稳定性。系统上始终有进程或任务在运行，即使没有用户登录，不当关机也会导致许多问题。

你通常需要是超级用户或 root（Unix 系统上权限最高的账户）才能关闭系统，在某些独立式或个人拥有的 Unix 机器上，管理员用户有时普通用户也可以操作。某些 GUI 允许你关闭系统。

# 初步

通常需要超级用户来关闭系统。通过命令行正确关闭 Unix 系统最可靠的方法是使用以下命令之一：

| 命令 | 功能 |
|---|---|
| `halt` | 立即关机。 |
| `init 0` | 使用预定义脚本关机。 |
| `init 6` | 重启系统。 |
| `poweroff` | 通过关机按钮关机系统。 |
| `reboot` | 重启系统。 |
| `shutdown` | 关机。 |

推荐的方法是使用 `shutdown`，它在所有 Unix 系统上可用。它使用系统提供的脚本来同步数据。如果你想关机并重启，可以使用以下命令：

```
shutdown -r
```

为了安全地物理关闭计算机，可以使用以下命令：

```
shutdown -h
```

使用 `shutdown` 命令不会损坏数据或产生系统不一致。

### 使用 Man Pages 获取帮助

Unix 命令一直有大量的参数或选项，允许实现不同类型的功能。由于人们无法记住所有命令及其所有选项，从 Unix 早期开始就有在线帮助。Unix 的帮助文件被称为 man pages（手册页）。Man 页面以标准格式呈现在线文档，任何用户都可以阅读，且逻辑清晰。通过输入以下语法使用该命令：

```
man command
```

25

# 第 2 章

将 `command` 替换为你想要了解的命令名称。例如，要查看 `man` 命令的手册页，你会输入：

```
man man
```

此时你会看到类似下面的输出（来自 Linux 系统）：

```
man(1)

man(1)

NAME

man - 格式化显示在线手册

manpath - 确定手册的搜索路径

SYNOPSIS

man -acdffHww [-path] [-m system] [-p string] [-C config_file]
[-M pathlist] [-P pager] [-S section_list] [section] name

DESCRIPTION

man 格式化并显示在线手册。如果你指定 section，man 只在该章节查找。man 通常是手册页名称，通常是命令、函数或文件的名称。然而，如果 man 包含斜杠 (/)，man 将其解释为文件规范，因此你可以 man ./foo.5 甚至 man /cd/foo/bar.gs。

下文提供了 man 查找手册文件的描述。

OPTIONS

-C config_file

指定使用的配置文件；默认是 /etc/man.config。（参见 man.config(5)）。

为了简洁已省略。要查看完整的手册页，请在命令行输入 man man。

SEE ALSO

apropos(1), whatis(1), less(1), groff(1), man.conf(5).

BUGS

-t 仅在安装了类似 rooft 的程序时有效。

如果你看到闪烁的 \255 或 <AD> 代替连字符，请在你的环境中设置 `CHARSET-latin1`。

TIPS

如果你在这一行添加行
```

# 第一步

```
(global-set-key [[f1]] (lambda () (interactive) (manual-entry (current-word))))
```

添加到你的 `.emacs` 文件中，然后按下 F1 即可获得当前光标位置库调用的帮助页（man page）。

要获取不包含退格键和下划线的纯文本版帮助页，请尝试：

```bash
# man foo col -b > foo.mantext
```

1995年9月2日

```
man(1)
```

帮助页通常分为几个章节，这些章节通常取决于帮助页作者的偏好。以下是一些常见的章节：

- NAME—命令名称。
- SYNOPSIS—命令的通用用法参数。
- DESCRIPTION—通常描述命令本身及其功能。
- OPTIONS—描述命令的所有参数或选项。
- ALSO—列出帮助页中与该命令直接相关或功能相似的其他命令。
- BUGS—解释命令或其输出中存在的任何已知问题或错误。
- EXAMPLES (or TIPS)—常见用法示例，让读者了解如何使用该命令。
- AUTHORS—帮助页/命令的作者。

你并不总是知道你需要的命令，但如果你知道某个命令的主要点，可以使用 `-k` 选项来搜索帮助页，该选项会在帮助页中查找关键词。例如，如果你需要更改文件的权限，但不记得要用哪个命令，可以输入：

```bash
man -k permission
```

我们将得到一个关键词中包含 `permission` 单词的命令列表。

### 尝试：使用帮助页

- 1. 使用帮助页。
- 2. 使用帮助页。
