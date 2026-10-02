
- `Ctrl+J` 在历史记录中后滚动
- `Ctrl+L` 在历史记录中向前滚动

最后但同样重要的是，按住 `CTRL` 并按 `r` 将调用反向搜索类型（reverse-i search）。输入一个字母，例如 `c`，你将获得历史记录中包含字母 "c" 的最近命令的匹配。继续输入以缩小匹配范围，当找到所需的命令时，按回车执行它。

```
kali@kali:~ $ history
1 cat /etc/lsb-release 2 clear
3 history
```

```
kali@kali:~ $ !!
cat /etc/lsb-release DISTRIB_RELEASE=kali-rolling DISTRIB_CODENAME=kali-rolling DISTRIB_DESCRIPTION="Kali GNU/Linux Rolling"
```

```
kali@kali:~$ [CTRL-R]c (reverse-i-search)'ca: cat /etc/lsb-release
```

列表 37 - 探索反向搜索功能

- 1. 检查你的 bash 历史并使用历史扩展重新运行其中的命令。
- 2. 执行你选择的各种命令，并通过快捷键以及反向搜索功能浏览历史记录。

## 3.2 管道与重定向

从命令行运行的每个程序都有连接到它的三个数据流，作为与外部环境通信通道。这些流定义如下：

表 3 - 连接到命令行程序的流

| 流名称 | 描述 |
| :--- | :--- |
| 标准输入 (STDIN) | 输入到程序的数据 |
| 标准输出 (STDOUT) | 程序的输出（默认到终端） |
| 标准错误 (STDERR) | 错误信息（默认到终端） |

管道（使用 `|` 运算符）和重定向（使用 `>` 和 `<` 运算符）连接程序和文件之间的流，以适应无限可能的情况。

### 3.2.1 重定向到新文件

在之前的命令中，输出打印在屏幕上。这在大多数情况下是方便的，但我们可以使用 `>` 运算符将输出保存到文件中以便以后参考或操作：

### 3.1.3.2 使用 Kali Linux 进行渗透测试

如列表 38 所示，如果我们将输出重定向到一个不存在的文件，该文件将被创建。然而，如果我们将输出保存到已存在的文件，文件内容将被替换。重定向时要小心！

列表 38 - 将输出重定向到文件

### 3.2.2 重定向到现有文件

要向现有文件追加数据（而不是覆盖文件），使用 `>>` 运算符：

### 3.2.3 从文件重定向

正如你可能猜到的那样，我们可以使用 `<` 运算符反向发送数据。在下面的示例中，我们将 `wc` 命令直接重定向到我们在上一节生成的文件。让我们尝试使用 `wc -m`，它可以计算文件中的字符数：

列表 39 - 使用 `<` 为 wc 命令提供输入

注意，这“连接”了我们的文件内容到 wc 命令的标准输入。

### 3.2.4 重定向 STDERR

根据 POSIX 规范，STDIN、STDOUT 和 STDERR 的文件描述符分别定义为 0、1 和 2。这些描述符非常重要，因为它们可以在执行或组合命令时从命令行操作对应的数据流。

为了更好地理解文件描述符的工作原理，请考虑这个重定向标准错误 (STDERR) 的示例：

```
kali@kali:~$ echo "that is maintained and funded by Offensive Security" >> redirection_test.txt
kali@kali:~ $ cat redirection_test.txt
Kali Linux is an open source project
that is maintained and funded by Offensive Security
```

```
kali@kali:~ $ wc -m < redirection_test.txt
89
```

# 列表 41 - 将 STDERR 重定向到文件

在列表 41 中，error.txt 只包含错误信息（生成在 STDERR 上）。我们通过在 `>` 运算符前加上流标识符（2=STDERR）来实现这一点。

## 3.2.5 管道

继续使用 `cat` 命令的示例，让我们来看看如何将一个命令的输出重定向到另一个命令的输入。考虑这个示例：

```
kali@kali:~ $ cat error.txt
is: cannot access '/test/: No such file or directory

kali@kali:~ $ cat error.txt | wc -m 53

kali@kali:~ $ cat error.txt | wc -m > count.txt

kali@kali:~ $ cat count.txt 53
```

# 列表 42 - 将 cat 命令的输出管道到 wc

在列表 42 中，我们使用管道 (|) 将 `cat` 命令的输出重定向到 `wc` 命令的输入。这个概念看起来可能微不足道，但将不同的命令组合起来是处理各种数据的强大工具。

### 3.2.5.1 练习

- 1. 使用 `cat` 命令结合 `sort` 来重新排序你的 Kali Linux 系统上 `/etc/passwd` 文件的内容。
- 2. 将上一个练习的输出重定向到你家目录下的任意文件中。

## 3.3 文本搜索与处理

在本节中，我们将通过引入几个命令：`grep`、`sed` 和 `awk`，来提高文件和文本处理的效率。对使用这些工具的高级用法需要对正则表达式（regex）的工作原理有良好的理解。正则表达式是一种描述搜索模式的特殊字符串。如果你不熟悉正则表达式，请在继续之前访问以下 URL：

- http://www.regexgg.com/
- http://www.regular-expressions.info/

### 3.3.1 grep

简而言之，`grep` 在文件中搜索给定的正则表达式，并将任何包含匹配项的行输出到标准输出（通常是终端屏幕）。一些最常用的开关包括 `-r`（递归搜索）和 `-i`（忽略文本大小写）。考虑以下示例：

列表 43 - 在 /usr/bin 中搜索包含 "zip" 的文件

在列表 43 中，我们使用 `ls` 列出 /usr/bin 目录下的所有文件，并将输出管道到 `grep` 命令，该命令会搜索任何包含字符串 "zip" 的行。理解并使用 `grep` 工具将被证明极其有用。

### 3.3.2 sed

`sed` 是一个强大的流编辑器。它也非常复杂，所以我们在这里仅略述皮毛。在很高的层面，`sed` 对文本流执行文本编辑，可以是一组特定的文件或标准输出。让我们来看一个示例：

列表 44 - 在输出流中替换单词

在列表 44 中，我们使用 `echo` 命令创建一个文本流，然后将其管道到 `sed` 以将单词 "hard" 替换为 "harder"。注意，默认情况下，输出已自动重定向到标准输出。

### 3.3.3 cut

`cut` 命令非常简单，但通常非常实用。它用于从行中提取文本段并将其输出到标准输出。一些最常用的开关包括 `-f`（指定我们要切割的字段编号）和 `-d`（字段分隔符）。

列表 45 - 从 echo 命令中提取字段

在列表 45 中，我们 `echo` 了一行文本并将其管道到 `cut` 命令，使用 ":" 作为分隔符提取第二个字段。相同的命令也可以用于文本中的行，如下所示，通过使用 `:` 并检索第一个字段，从 `/etc/passwd` 中提取了用户列表：

```
kali@kali:~ $ ls -la /usr/bin | grep zip
rwx-xr-x 1 root -rwx-xr-x 1 root -rwx-xr-x 1 root -rwx-xr-x 1 root
3440 29 Jan 2017 bzip
3480 29 Jan 2017 bzip
13864 29 Jan 2017 bzip
2301 Mar 14 2016 gzip
10572 Mar 14 2016 gzip
```

```
kali@kali:~ $ echo "I need to try hard" | sed 's/hard/harder/'
```

```
kali@kali:~ $ echo "I need to try binaries, mobile apps, and just anything else" | cut -d ":" -f 2
```

```
kali@kali:~ $ cut -d ":" -f 1 /etc/passwd
```

### 3.3.4 awk

AWK 是一种为文本处理设计的编程语言，通常被用作数据提取和报告工具。它可以非常复杂，所以我们只浅尝此。与 `awk` 一起使用的常用开关是 `-F`（它是字段分隔符）以及输出结果的 `print` 命令。

列表 47 - 在 awk 中使用多字符分隔符从流中提取字段

在列表 47 中，我们 `echo` 了一行并将其管道到 `awk`，使用 `::` 作为字段分隔符提取第一个字段 ($1) 和第三个字段 ($3)。我们使用的 `cut` 和 `awk` 示例之间最大的区别在于，`cut` 只能接受单个字符作为字段分隔符，而 `awk`（如列表 47 所示）要灵活得多。作为一个法则，当你开始编写涉及多个 `cut` 操作的命令时，可能可能考虑切换到 `awk`。

### 3.3.5 实例示例

让我们来看结合了我们为止探索的许多命令的实例示例。我们得到了一个 Apache 服务器日志（http://www.offensive-security.com/pwk-files/access_log.gz），其中包含了攻击证据。我们的任务是使用 Bash 命令来查找并发现信息，例如攻击者是谁以及服务器上到底发生了什么。首先，我们将使用 `head` 和 `wc` 命令快速查看日志文件以理解其结构。`head` 命令显示文件的 10 行，而 `wc` 命令配合 `-l` 显示文件的总行数。

```
kali@kali:~ $ echo "hello:there::friend" | awk -F ":" '{print $1, $3}'
hello friend
```

```
kali@kali:~ $ gunzip access_log.gz
kali@kali:~ $ mv access_log.txt access.log
kali@kali:~ $ head access.log
201.21.152.44 -- [25/Apr/2013:14:05:35-0700] GET /favicon.ico HTTP/1.1 404 89 - - "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/26.0.1410.64 Safari/537.31" "random-site.com"
70.194.129.44 -- [25/Apr/2013:14:10:48-0700] GET /include/jquery.showoff.min.js HTTP/1.1" 200 2553 "http://www.random-site.com/" "Mozilla/5.0 (Linux; Android 4.2; en-us; SC-S135 Build/IZ054K) AppleWebKit/537.36"
```

```
kali@kali:~ $ cat access.log | grep '208.68.234.99' | cut -d '"' -f 2 | uniq -c 1038 GET //admin HTTP/1.1
```

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_68_0.png)

```
kali@kali:~ $ cat access.log | grep '208.68.234.99' | grep '/admin ' | sort -u 208.68.234.99 - - [22/Apr/2013:07:51:20 -0500] "GET //admin HTTP/1.1" 401 742 "-" "Teh Forest Lobster"

208.68.234.99 - admin [22/Apr/2013:07:51:25 -0500] "GET //admin HTTP/1.1" 200 575 "-"
```

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 58

# 使用 Kali Linux 进行渗透测试 2.0

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_68_1.png)

"Teh Forest Lobster" ...

```
kali@kali:~ $ cat access.log|grep '208.68.234.99'|grep -v '/admin '
kali@kali:~$
```

+ 列出 52 - 仔细查看日志文件

显然，208.68.234.99 参与了针对此服务器的 HTTP 暴力破解攻击。此外，在 1000 次尝试后，暴力破解似乎成功了，正如“HTTP 200” 消息所示。

### 3.3.5.1 练习题

- 1. 使用 `/etc/passwd`，提取你的 Kali 机器上所有 shell 为 `/bin/false` 的用户的用户名和主目录字段。请确保你使用 Bash 单行命令将输出打印到屏幕上。输出结果可能类似于下方的列表 53：
- 2. 将 `/etc/passwd` 复制到你的主目录 (`/home/kali`)。
- 3. 使用单行命令 `cat` 打印 `/etc/passwd` 的输出，并将所有的

列表 53 - 具有 /bin/false shell 的用户的主目录

"Gnome Display Manager" 字符串替换为 "GDM"。

## 3.4 从命令行编辑文件

接下来，让我们来看看如何在命令行环境下编辑文件。这是一项极其重要的 Linux 技能，特别是在渗透测试中如果你获得了了类 Unix 系统的权限。

尽管有像 `gedit` 和 `leafpad` 这样的文本编辑器由于其图形用户界面可能更具视觉吸引，但我们将关注基于终端的编辑器，这些编辑器强调速度和多功能性。每个人在选择文本编辑器时都有偏好，但我们将介绍最常用选项的**基本用法**：`nano` 和 `vi`。

### 3.4.1 nano

Nano 是最易用的编辑器之一。要打开文件并开始编辑，只需运行 `nano`，并将文件名作为参数传递：

> ¹(GNOME 项目, 2019), https://wiki.gnome.org/Apps/Gedit
> ²(Wikipedia, 2019), https://en.wikipedia.org/wiki/Leafpad
> ³(Wikipedia, 2019), https://en.wikipedia.org/wiki/Graphical_user_interface
> ⁴(GNU Nano, 2019) https://www.nano-editor.org/docs.php

```
kali@kali: ~ 在此处输入命令...
The user mysql home directory is /nonexistent
The user Debian-snmp home directory is /var/lib/snmp
The user Debian-dispatcher home directory is /var/run/speech-dispatcher
The Debian-gdm home directory is /var/lib/gdm3
```

图 5: 使用 nano 编辑文件

vi 是一个极其强大的文本编辑器，处理速度极快，特别是在自动化重复任务时。然而，它的学习曲线相对陡峭，使用起来远没有 Nano 简单。由于其复杂性，我们将只介绍最基础的操作。和 nano 一样，编辑文件只需将其文件名作为参数传递给 vi：

```
kali@kali: ~ vi_intro_to.vi.txt
列表 55 - 使用 vi 打开文件
```

一旦打开了文件，启用*插入模式*开始打字。要这样做，按下 **i** 键并开始打字。

要禁用*插入模式*并返回*命令模式*，按下 **Esc** 键。在*命令模式*下，使用 **dd** 删除当前行，使用 **yy** 复制当前行，使用 **p** 粘贴剪贴板内容，使用 **x** 删除当前字符，使用 **w** 将当前文件写入磁盘，使用 **:q** 在不写入退出，最后使用 **:wq** 保存并退出。

¹(GNU Nano, 2018) https://www.nano-editor.org/dist/v2/nano.html

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved.

关于 nano 的更多信息，请参阅其在线文档。

### 3.4.2 vi

Nano 是我们最喜欢的编辑器之一。它可能不华丽，但非常好用。

```
终端 - kali@kali ~
nano_intro_to.txt
文件 编辑 标签
^G 帮助      ^O 输出
^X 退出      ^R 读取 ^S 搜索   ^C 跳转行
```

列表 54 - 使用 nano 编辑打开文件

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_70.png)

一旦打开文件，我们就可以像在图形编辑器中立即开始更改。如图 5 所示，菜单位于屏幕底部。一些常用的命令包括：**Ctrl+O** 更改，**Ctrl+K** 删除当前行，**Ctrl+U** 在光标处粘贴，**Ctrl+W** 搜索以及 **Ctrl+X** 退出。

由于 vi 使用起来很奇怪，许多用户避免使用。然而，从渗透测试者的角度来看，vi 可以节省大量时间；它安装在每个符合 POSIX 标准的系统中。

- https://en.wikibooks.org/wiki/Learning_the_vi
- https://www.debian.org/doc/manuals/debian

## 3.5 比较文件
