
你可以使用键盘键（上、下、右、左方向键）回溯之前在 shell 中输入过的命令。因此，如果你需要再次输入相同的命令，可以使用键盘上和下方向键在可用命令列表中循环，并按 Enter 键执行。

作为一名 Linux 管理员，你将经常运行只有 root 用户才能执行的系统配置命令。如果你以普通用户账户登录系统，可以使用 `su`（切换用户）命令轻松切换到 root 用户以执行任何管理任务。要切换到 root 用户并加载 root 的环境变量，你可以运行带有 `-` 选项的并在提示时提供 root 密码：

```
[user1@server1]$ su root
Password:\ Last login Mon Aug 16 09:45:42 EDT 2023 for tty3
[root@server1]#
```

或者，要运行单个命令，可以运行 `su -c "command" root` 并在提示时指定 root 用户的密码。

如果你在使用 `su` 命令时不指定用户名，则假设为 root 用户。此外，root 用户可以使用 `su` 命令切换到任何其他用户账户而无需指定密码：

```
[root@server1]$ su user1
Last login Mon Aug 16 10:22:21 EDT 2023 for tty5
[user1@server1]$_
```

## Shell 元字符

shell 的另一个重要部分是元字符，它们是具有特殊含义的键盘字符。shell 中最常用的元字符之一是字符 `$`，它告诉后续的文本指的是一个变量。变量是内存中的一段信息；变量名通常是大写单词，大多数变量由 Linux 系统在你登录时设置。一个如何使用 `echo` 命令（将文本打印到屏幕的命令）的示例是使用如下：

```
[root@server1]# echo Hi There!
Hi There!
[root@server1]# echo My shell is $SHELL
My shell is /bin/bash
[root@server1]#
```

注意前面的输出，`$SHELL` 被翻译为内存中相应的值（`/bin/bash`，BASH shell）。由于变量前带有元字符 `$`，shell 将 `$` 识别为（变量标识符）。表 2-7 列出了贯穿书中讨论的常用 shell 元字符列表。

### 表 2-7 常用 shell 元字符

| 元字符(s) | 描述 |
| --- | --- |
| `$` | Shell 变量 |
| `~` | 特殊主目录变量 |
| `#` | Shell 脚本注释 |
| `&` | 后台命令执行 |
| `;` | 命令终止 |
| `< << >>` | 输入/输出重定向 |
| `|` | 命令管道 |
| `* ? [ ]` | Shell 通配符 |
| `' \` | 元字符引号 |
| `` ` `` | 命令替换 |
| `( )` | 命令分组 |

在输入命令时，避免使用元字符是一个良好的习惯，除非你需要利用它们的特殊功能，因为 shell 会很容易解释它们，这可能会导致意之外的结果。

> 注意 21
> 如果你不小心使用了这些字符之一，且你的 shell 没有返回到正常提示符，请按 `Ctrl+c` 取消并清除你当前的命令。

在某些情况下，你可能需要在命令中使用元字符并防止 shell 解释其特殊含义。要做到这一点，将元字符封装在单引号（' '）中。单引号可以保护这些元字符不被 shell 特殊解释（也就是说，`$` 被解释为 `$` 而不是变量标识符）。你也可以使用双引号（`"`）执行相同任务；但是，如果需要保护一个字符免受 shell 解释，双引号会保护除 `\` 和 `"` 之外的字符。

你可以在该字符前加上反斜线（`\`）而不是将其封装在引号内。示例如下：

```
[root@server1]# echo My Shell is $SHELL
My Shell is /bin/bash
[root@server1]# echo 'My Shell is $SHELL'
My Shell is $SHELL
[root@server1]# echo "My Shell is $SHELL"
My Shell is /bin/bash
[root@server1]# echo My Shell is \SHELL
My Shell is $SHELL
[root@server1]#_
```

如表 2-7 所示，并不是所有的引号字符都能保护字符免受 shell 的影响。反引号（`` ` ``）可用于执行命令替换；反引号之间的任何内容都将替换命令本身。以 `date` 为例：

```
[root@server1]# echo `date`
Today is Tue Mar 29 09:28:11 EST 2023
[root@server1]#
```

## 获取帮助

大多数 Linux 发行版包含 5000 多个命令，记忆每个命令的语法和用法是不现实的。最常见的文档形式是手册页（称为 man pages）。输入 `man` 后跟命令名即可显示关于该命令的信息：

```
[root@server1]# man whoami
```

手册页在终端屏幕上逐页显示。可以使用方向键滚动或按 `q` 退出。`whoami` 的手册页类似于：

```
WHOAMI (1)

WHOAMI (1)

NAME
whoami      print effective user name

SYNOPSIS
whoami [OPTION]...

DESCRIPTION
Print the user name associated with effective user ID. Same as -un.

--help display this help and exit

--version output version

GNU coreutils 9.0                March 2022                WHOAMI (1)
[root@server1 root]#
```

注意输出顶部显示为 `WHOAMI(1)`。`(1)` 表示手册页的章节；章节 (1) 表示 `whoami` 是任何用户都可以执行的命令。

作者：Richard Markik。

报告 BUGS

GNU coreutils 主页：https://www.gnu.org/software/coreutils/

向 <https://translationproject.org/team/> 报告翻译错误。

版权

Copyright©2021 Free Software Foundation, Inc. 许可证 GPLv3; GNU

GPL 版本 3 或更高版本 https://www.gnu.org/licenses/gpl.html。

这是免费软件：你可以更改和分发它

在法律允许的范围内不提供保证。

参见

完整文档：https://www.gnu.org/software/coreutils/whoami

或通过本地获取：info '(coreutils) whoami invocation'

### 表 2-8 手册页章节编号

| 手册页章节 | 描述 |
| --- | --- |
| 1 | 任何用户都可以执行的命令 |
| 2 | Linux 系统调用 |
| 3 | 库例 |
| 4 | 特殊设备文件 |
| 5 | 文件格式 |
| 6 | 游戏 |
| 7 | 杂项 |
| 8 | 只有 root 用户才能执行的命令 |
| 9 | Linux 内核例 |
| n | 尚未分类的新命令 |

## CompTIA Linux+ 与 LPIC-1：Linux 认证指南

有时，会有多个命令在运行。如果你带有参数运行该命令，Linux 会返回章节号最小的目录帮助页。例如，如果有一个名为 `whoami` 的文件和一个名为 `whoami` 的命令，而你输入 `whoami`，则显示 `whoami` 命令的帮助页（帮助页的第 1 节）。要显示 `whoami` 文件格式的帮助页，你输入 `man 5 whoami` 来显示 `whoami` 文件格式（帮助页的第 5 节）。

请记住，Linux 用户可以使用许多命令；因此，如果不使用 Linux 字典，查找执行某任务所需的命令可能会很繁琐。此外，你可以通过关键词搜索帮助页。要找到所有名称或描述中包含 "usb" 单词的命令，请输入：

```bash
[root@server1] # man -k usb
```

此命令产生以下输出：

- - cyrusdb2current (8)
- flatpak-create-usb (1)
- lusb (8)
- ostree-create-usb (1)
- sane-canon630 (5)
- sane-canonide70 (5)
- sane-cardscan (5)
- sane-epitju (5)
- sane-find-camera (1)
- sane-gecko (5)
- sane-gt68 (5)
- sane-kvs1025 (5)
- sane-kvs20xx (5)
- sane-kvs40xx (5)
- sane-mal109 (5)
- sane-mustek_usb (5)
- sane-mustek_usb (2)
- sane-plebus (5)
- sane-plustek (5)
- sane-micro (5)
- sane-sm3840 (5)
- sane-ulai (2)
- sane-usb (5)
- usb-devices (1)
- usb_modeswitch (1)
- usb_modeswitch_dispatcher (1)
- ushid-dump (8)
- usbmuxd (8)
- 转换 SASLDB... 的命令行工具
- 复制应用和/或到可移动设备...
- 列出 USB 设备
- 将给定的引用放在外部驱动器上...
- Canon 630 USB 扫描器的 SANE 后端
- Canon IDE 70 和 600... 的 SANE 后端
- Corex Card USB 扫描器的 SANE 后端
- 富士通（Epson）USB 的 SANE 后端
- 查找 SANE USB 摄像头及其驱动程序...
- GL646, GL643, GL84... 的 SANE 后端
- GT-68XX USB 平板扫描器的 SANE 后端
- 松下 K-S102XC USB/... 的 SANE 后端
- 松下 K-SVS20XX USB/... 的 SANE 后端
- Mustek Pearaf 1200 USB 的 SANE 后端
- Mustek USB 平板扫描器的 SANE 后端
- SQL13 USB 平板扫描器的 SANE 后端
- USB 连接的 PowerWire... 的 SANE 后端
- HP283 [1/2/3] USB 扫描器的 SANE 后端
- 带有 MG01 的微扫描器的 SANE 后端
- Plustek USB 平板扫描器的 SANE 后端...
- SANE 的 USB 配置提示
- 打印 USB 设备详情
- 控制“多态”USB 设备
- usb_modeswitch 的 Linux 封装器...
- 转储 USB 设备报告描述符...
- 暴露一个用于多路复用的 socket...
- usb 的键值

在找到所需的命令后，你可以不带 `-k` 选项运行该命令的 `man` 以获取有关命令的信息。

```bash
[root@server1] # man usb_
```

# 第 2 章 Linux 安装与使用

> 注意 23
> 你可以使用 `apropos usb` 命令来执行与 `man -k usb` 命令相同的功能。这两个命令在终端屏幕上会产生完全相同的输出。

> 注意 24
> 如果在安装 Linux 之后，你没有看到来自 `man -k` 或 `apropos` 命令的任何输出，你可能需要运行 `mand` 命令来对帮助页数据库建立索引。

如果你只想查看命令的简短描述（例如，查看该命令的作用），可以使用 `whatis` 命令，因为 `whatis` 命令只会显示 `whoami` 帮助页的名称和描述。

另一个最初用于替代 Linux 中 `man` 命令的工具是 GNU info 页面。你可以通过输入 `info` 命令后跟感兴趣的命令名称来访问它。`info` 命令返回每个命令的易读描述以及其连接到其他信息页的链接。今天，`info` 页面和帮助页都用于查找文档。帮助页自 Linux 诞生以来一直被使用，在 UNIX 操作系统中也使用了几十年。使用 `info` 工具查找有关 `whoami` 命令信息的示例：

```bash
[root@server]# info whoami
```

`info` 内容以交互方式显示：

Next: groups invocation, Prev: log invocation, Up: User information

```
20.3 'whoami': 打印有效用户 ID
============================

'whoami' 打印与当前有效用户 ID 关联的名称。它等同于命令 'id -un'。

唯一的选项是 `--help` 和 `-version`。*常用选项：*

状态为零表示成功，非零值表示失败
```

------Info: (coreutils) whoami invocation, 14 lines -All---

欢迎来到 info 6.8。按 H 寻求帮助。

> 注意 26
> 状态为零表示成功，非零值表示失败

------Info: (coreutils) whoami invocation, 14 lines -All---

欢迎来到 info 6.8。按 H 寻求帮助。

退出状态：
返回成功

```
[server1] #
```
