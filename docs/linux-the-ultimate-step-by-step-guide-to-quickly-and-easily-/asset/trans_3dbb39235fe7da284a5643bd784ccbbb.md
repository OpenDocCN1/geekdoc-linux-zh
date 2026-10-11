
如果设置了 **$BROWSER**，其值是一个以冒号分隔的命令列表，每个命令都用于尝试为 **man --html** 启动一个网络浏览器。在每个命令中，**%s** 会被替换为包含 **groff** 输出的 HTML 文件名的文件名，**%%** 会被替换为单个百分号（%），**%c** 会被替换为冒号（:）。

| 变量 | 描述 |
| :--- | :--- |
| **BROWSER** | 如果设置了 **$BROWSER**，其值是一个以冒号分隔的命令列表，每个命令都用于尝试为 **man --html** 启动一个网络浏览器。在每个命令中，**%s** 会被替换为包含 **groff** 输出的 HTML 文件名的文件名，**%%** 会被替换为单个百分号（%），**%c** 会被替换为冒号（:）。 |
| **SYSTEM** | 如果设置了 **$SYSTEM**，其效果等同于将其作为 **-m** 选项的参数指定。 |
| **MANOPT** | 如果设置了 **$MANOPT**，它将在 **mans** 命令行之前被解析，并且预期具有类似的格式。由于其他所有特定的 man 环境变量都可以表示为命令行选项，因此它们都是包含在 **$MANOPT** 中的候选项，预计它们将逐渐被淘汰。注意：所有应解释为选项参数的一部分的空格都必须进行转义（前面加一个反斜杠）。 |
| **MANWIDTH** | 如果设置了 **$MANWIDTH**，其值将用作手册页应进行格式化的行长度。如果未设置，手册页将按适合当前终端的行长度进行格式化（如果可用则使用 **ioctl**，使用 **$COLUMNS** 的值，或者如果两者都不可用则回退到 80 个字符）。**cat** 页面仅当可以使用默认格式化时才会保存，即当终端行长度在 66 到 80 个字符之间时。 |
| **MAN_KEEP_FORMATTING** | 通常，当输出不重定向到终端（例如重定向到文件或管道）时，格式化字符会被丢弃，以便在没有特殊工具的情况下更容易阅读结果。但是，如果将 **$MAN_KEEP_FORMATTING** 设置为任何非空值，这些格式化字符将被保留。这对于能够解释格式化字符的 **man** 包装器可能很有用。 |

**MAN_KEEP_STDERR**

通常，当输出重定向到终端（通常是分页器）时，用于生成手册页格式化版本的命令产生的任何错误输出都会被丢弃，以避免干扰分页器的显示。像 **groff** 这样的程序通常会产生相对较轻微的错误消息，涉及排版问题（例如对齐不良），这些消息在手册页旁边显示时既不美观又容易混淆。但是，你可能仍然希望看到它们，因此如果将 **$MAN_KEEP_STDERR** 设置为非空值，错误输出将按往常一样显示。

**LANG, LC_MESSAGES**

根据系统和实现的不同，**$LANG** 和 **$LC_MESSAGES** 中的一个或两者都将被查询以获取当前的消息语言环境，**man** 将使用该语言环境显示其消息（如果可用）。

## 文件

**man** 使用以下文件：

| 文件 | 描述 |
| :--- | :--- |
| **/etc/manpath.config** | man-db 配置文件。 |
| **/usr/share/man** | 全局手册页层级结构。 |
| **/usr/share/man/index.(bt\|db\|dir\|pag)** | 传统的全球索引数据库缓存。 |
| **/var/cache/man/index.(bt\|db\|dir\|pag)** | 符合 FHS 标准的全球索引数据库缓存。 |

## 示例

```bash
man man
```

查看 man 命令的手册页。

```bash
man -nh -nj man
```

## 第七章：LINUX 目录命令

Linux 或类 UNIX 系统使用 ls 命令列出文件和目录。但是，ls 没有仅列出目录的选项。你可以使用 ls 和 grep 的组合来仅列出目录名称。你也可以使用 find 命令。在这个快速教程中，你将学习如何在 Linux 或 UNIX 中仅列出目录。

在 Unix 中列出所有目录

键入以下命令：

```bash
$ ls -l | grep `^d*`
ls -l | egrep `^d*`
```

尝试以下 ls 命令以列出当前目录中的目录：

```bash
$ ls -d */
```

![](img/95e14ba64977353b42ea3103515e63c3_60_0.png)

示例输出

## 在 Unix 中仅列出文件

**键入以下命令：**

```bash
`$ ls -l | egrep -v '^d'`
`$ ls -l | egrep -v '^d'`
```

grep 命令用于搜索输入。它通过匹配第一个字符 `d' 来过滤掉目录名称。要反转效果，即仅显示文件，你需要传递 -v 选项。这会反转匹配的含义，以选择不匹配的行。

**任务：创建别名以节省时间**

你可以创建两个别名，分别用于仅列出目录和文件。

```bash
`alias lf="ls -l | egrep -v '^d'"`
`alias ldir="ls -l | egrep '^d'"`
```

**将上述两个别名放入你的 bash shell 启动文件中：**

```bash
`$ cd`
`$ vi .bash_profile`
```

**附加两行代码：**

```bash
`alias lf="ls -l | egrep -v '^d'"`
`alias ldir="ls -l | egrep '^d'"`
```

**保存并关闭文件。**

**现在只需键入 lf - 以列出文件，键入 ldir - 以仅列出目录：**

```bash
`$ cd /etc`
`$ lf`
```

**示例输出：**

```text
-rw-r-r--   1 root root      2149 2006-09-04 23:25 adduser.conf
-rw-r-r--   1 root root        44 2006-09-29 05:11 adjtime
-rw-r-r--   1 root root      197 2006-09-04 23:48 aliases
-rw----     1 root root       144 2002-01-18 13:43 at.deny
-rw-r-r--   1 root root       162 2006-09-22 23:24 auxixrc
-rw-r-r--   1 root root        28 2006-09-22 23:24 auxixrc1
```

**仅列出目录名称：**

```bash
`$ cd /etc`
`$ ldir`
```

**示例输出：**

```text
drwxr-xr-x   4 root root      4096 2006-09-22 16:41 alsa
drwxr-xr-x   2 root root      4096 2006-09-20 20:59 alternatives
drwxr-xr-x   6 root root      4096 2006-09-22 16:41 apm
drwxr-xr-x   3 root root      4096 2006-09-07 02:51 apt
drwxr-xr-x   2 root root      4096 2006-09-08 01:46 bash_completion.d
```

## 使用 find 命令列出文件或目录

find 命令可以按以下方式使用：要列出 /nas 中的所有目录，请输入：

```bash
`find /nas -type d`
```

```bash
find /nas -type d -ls
find . -type d -ls
```

示例输出：

```text
1070785    8 drwxrwxrwt    8 root    root    4096 Jul  5 07:12 .
1070797    8 drwx--        2 root    root    4096 Jul  4 07:22 ./orbit-root
1070843    8 drwxr-xr-x    2 root    root    4096 Jun 16 18:55 ./w
1070789    8 drwxr-xr-x   10 root    root    4096 Jun 17 14:54 ./b
1071340    8 drwxr-xr-x    2 root    root    4096 Jun 16 18:55 ./b/init.d
1071581    8 drwxr-xr-x    3 root    root    4096 Jun 16 18:55 ./b/bind
1071584    8 drwxr-xr-x    2 root    root    4096 Jun 16 18:55 ./b/bind/bak
1071617    8 drwxr-xr-x    2 root    root    4096 Jun 16 18:55 ./b/fw
1071628    8 drwxr-xr-x    8 root    root    4096 Jun 16 18:55 ./b/scripts
```

## 第八章：处理文件

本章首先描述 Unix 命令的一般特征。然后讨论常用于创建和操作文件的命令。一些最常用的 UNIX 命令的摘要呈现在命令比较中。

### UNIX 文件名

理解创建 UNIX 文件的规则很重要：UNIX 区分大小写！例如，“fileName” 与 “filename” 不同。建议将名称限制为字母字符、数字、下划线（_）和点（.）。UNIX 文件名中使用的点（.）只是字符，而不是文件名组件之间的分隔符；你可以在文件名中包含多个点。将点作为文件名的第一个字符会使文件对普通的 ls 命令不可见（隐藏）；使用 ls 命令的 -a 标志来显示隐藏文件。虽然许多系统允许更长，但建议每个文件名的长度为 14 个字符。Unix shell 通常包含几个重要的通配符。星号 (*) 用于匹配 o 或更多字符（例如，abc* 将匹配以字母 abc 开头的任何文件），问号 (?) 用于匹配任何单个字符，左方括号 ([) 和右方括号 (]) 用于括住一串字符，其中任何一个字符匹配。执行以下命令并观察结果：

```bash
ls m*
ls *,f
ls *.?
ls [a-d]*
```

PC 用户注意事项：Unix 使用正斜杠 (/) 而不是反斜杠 (\) 作为目录分隔符

### 查看文件内容

你可以使用各种命令查看文件内容。此处介绍了 cat、more、pg、head 和 tail。当然，你始终可以使用编辑器；要在“只读”模式下使用 vi 查看文件 “argtest” 的内容，请输入：

```bash
vi -R argtest
```

