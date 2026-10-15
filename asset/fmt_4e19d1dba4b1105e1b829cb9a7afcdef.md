
| `cd` | 更改当前目录。输入 `cd /usr` 以切换到 `/usr` 目录。 |
| `chmod` | 更改文件权限。输入 `chmod +x filename` 以该文件可执行（用现有文件的名称替换 `filename`）。 |
| `cp` | 复制文件。输入 `cp` 以将目录更改为你的主目录。然后输入 `cp /etc/X11/XF86Config .` 以将文件复制到你的主目录。 |
| `ls` | 显示目录的内容。输入 `ls -F` 以查看当前目录的内容。 |
| `mkdir` | 创建一个目录。输入 `cd` 以切换到你的主目录，然后输入 `mkdir temp` 以创建一个名为 `temp` 的目录。 |
| `mv` | 重命名文件或将其从一个目录移动到另一个目录。输入 `mv filename1 filename2` 以更改文件名；对 `filename1` 使用现有文件的名称。 |
| `rm` | 删除文件。语法是 `rm filename`。（请谨慎使用，因为文件会被删除。） |
| `rm dir` | 删除目录。输入 `rm dir -temp` 以从你的主目录中删除名为 `temp` 的目录（参见本表中前面的 `mkdir` 命令）。 |
| `pwd` | 显示当前目录。输入 `pwd` 以查看当前目录名称。 |

## 查找文件

`find`：根据指定的条件（如名称、大小等）查找文件。输入 `find /usr -name "README*" -print` 以尝试此命令。

## 处理文件

`cat`：在标准输出上显示文件（可以将多个文件连接成一个大的文件）。输入 `cd` 以进入你的主目录，然后输入 `cat .bash_profile` 以查看该文件的内容。

`grep`：在文本文件中搜索正则表达式。输入 `cd` 以进入你的主目录，然后输入 `grep BASH .b*` 以查看在指定文件中搜索字符串 BASH 的结果。

`more`：一次显示一页文本文件。输入 `more /etc/inittab` 以分页查看内容。（按空格键前进或输入 `q` 退出。）

## 管理用户

`passwd`：更改密码。输入 `passwd` 并按照提示更改你的密码。

`su`：在没有参数调用的情况下，变为另一个用户或 root。输入 `su`，并在提示时输入 root 密码。请小心你做什么，因为你现在是超级用户。输入 `exit` 以返回普通用户。

以下部分按类别介绍了未在之前小节中涵盖的新命令。

## 管理进程的命令

每次 shell 响应你键入的命令时，它都会启动一个进程，即运行中程序的一个实例。shell 本身就是一个进程，它执行的任何脚本或应用程序也是如此。你可以使用 `ps` 命令查看进程列表。例如，当你输入 `ps -x` 时，Bash 会显示当前的进程集合。以下是该命令的部分输出。我还包含了 `-cols 132` 选项，以确保你能完整地看到每个命令：

```text
ps -x --cols 132
  PID TTY  STAT TIME COMMAND
  1  ?    S     0:05 init [5]
  325 ?  S     0:00 syslogd -m 0
```

```text
335 ? S 0:00 *clockd
480 ? S 0:00 crond
511 ? S 0:00 xinetd reuse pidfile /var/run/xinetd.pid
580 ? S 0:00 sendmail: accepting connections
596 ? S 0:00 gpm -t imp2
849 ? S 0:01 /usr/bin/gnome-session
853 ? S 0:00 gnome-apropos --sm-client-id default0
901 ? S 0:02 sawfish --sm-client-id=default0
967 ? S 8:36 magic --sm-client-id=default12
985 ? S 0:00 gnome-name-service
994 ? S 0:01 panel --sm-client-id default1
1001 ? S 0:00 gmc --nomindows --sm-client-id default8
2143 ? S 0:00 gnome-terminal --use-factory --start-factory-server
21433 ? S 0:00 gnome-pty-helper
21444 pts/5 S 0:00 bash
21455 pts/0 R 0:00 ps x --cols 132
```

在上面的输出中，`COMMAND` 列显示了创建进程的命今。此列表显示 Bash shell 和 `ps` 命令作为进程。其他进程包括 shell 在你在图形登录界面登录并启动 GNOME 会话时启动的所有程序。特别是，该列表包括 `sawfish`（窗口管理器）进程和 `gnome-terminal`（终端窗口）进程。请注意，`ps` 甚至将其自身的进程显示在列表的最后一个。

默认的 `ps x` 命令并不提供 Linux 系统上运行的所有进程。`ps x` 显示的是你直接通过 shell 脚本或当登录时自动运行的脚本间接启动的命令。要查看完整的进程集合，请配合使用 `ps` 命令的 `a` 选项和 `x` 选项，如下所示：

```text
ps -ax
```

如果你研究 `ps` 命令的输出，你会发现第一列标题为 PID，并且它为每个进程显示一个数字。PID 代表进程 ID（识别），它是 Linux 内核分配的顺序号。如果你查看 `ps ax` 命令的输出，你应该看到 `init` 命令是第一个进程；它的 PID 或进程号为 1。这就是为什么 `init` 被称为所有进程的“母亲”。

## 日期和时间命令

你可以使用 `date` 命令来显示当前的日期和时间或设置新的日期和时间。在 shell 提示符处输入 `date`，你会得到类似以下结果：

```text
date
Wed Jun 13 19:46:31 MDT 2001
```

你还可以格式化你希望日期或时间显示的方式。例如，要仅查看日期（不带当前时间），请尝试以下命令：

```text
date "+%A %B %d %Y"
Wednesday June 13 2001
```

格式规范是以包含带百分号（%）前缀的单个字母的文本字符串形式给出的。这与 C 和 C++ 编程语言中指定格式的方式类似。在此示例中，格式字符的含义如下：

- `%A` 显示星期的完整名称。
- `%B` 显示月份的完整名称。
- `%d` 显示日期（每月的第几天）。
- `%Y` 使用全部四位数字显示年份。

要设置日期，请以 root 身份登录，然后使用 `date -s` 后跟任意常见日期/时间格式中的日期和时间。例如，要将日期和时间设置为 2002 年 12 月 31 日 晚上 10:30，请输入：

```
date -s "December 31, 2002 10:30 p.m."
```

以下是该命令在我的系统上的运行情况：

```
## date -s "December 31, 2002 10:30 p.m."
Tue Dec 31 22:30:00 MST 2002
## date
Tue Dec 31 22:30:00 MST 2002
```

在使用 `date -s` 设置时间后，一个简单的 `date` 命令会显示新的时间。

![](img/5fe8f856723cde0b366f73584b9e64b8_96_0.png)

**要将系统时间恢复为正确值，请以 root 用户身份执行命令 `hwclock --hctosys`。**

另一个有趣的与日期相关的命令是 `cal`。如果键入 `cal` 而不带任何选项，它会打印当前月份的日历。如果键入 `cal` 后跟一个数字，`cal` 会将该数字视为年份并打印该年的日历。要查看特定年份特定月份的日历，请提供月份编号（1 = 一月，2 = 二月，依此类推）后跟年份。因此，要查看 2001 年 1 月的日历，请键入以下内容：

```
cal 1 2001
      January 2001
Su Mo Tu We Th Fr Sa
        1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
```

## 文件处理命令

您已经了解了如何使用 `grep` 命令搜索文本文件以及如何使用 `more` 命令逐屏查看文本文件。Red Hat Linux 包含许多更多用于处理文件的实用工具——主要是文本文件——但有些命令也可以用于任何文件。

### 统计文本文件中的字符、单词和行数

您可以使用 `wc` 命令来显示文本文件的行数、单词数和字符数。请尝试以下操作：

```
wc /etc/inittab
57   244  1756 /etc/inittab
```
