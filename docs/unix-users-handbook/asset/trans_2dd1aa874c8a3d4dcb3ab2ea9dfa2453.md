

## 表 7-3 Shell 引号处理

| 字符 | 描述 |
| :--- | :--- |
| `'cmd'` | 单引号表示将字符串中的字符按字面意思处理 |
| `"str"` | 双引号表示允许命令替换和变量替换 |
| `\c` | 转义字符，阻止其后所有内容（包括换行符）的输出 |
| `` `str` `` | 反引号表示执行命令并替换为其输出结果

将表 7-3 应用于前文提到的 **procs** 别名，我们可以看到构成该别名的内容。该别名以单引号开始，这意味着要执行单引号内的命令。第一个命令是 **echo** 命令，它使用双引号来指定要 **echo** 的字符。在双引号中嵌入了转义字符 \c，它阻止换行符的输出。分号用于分隔命令。然后运行 **ps** 以生成进程列表，并将输出通过管道 (|) 传递给单词计数 (**wc**)，从而生成行数计数。实际上共有 43 个进程在运行，因为 **wc** 报告了一个包含 ps 表头的额外行。

![](img/75f39fc91296b889c0653851accdfd46_408_0.png)

![](img/75f39fc91296b889c0653851accdfd46_408_1.png)

![](img/75f39fc91296b889c0653851accdfd46_409_0.png)

如你在图 7-3 中看到的，某些引号的使用会变得棘手。如果你希望修改和重用现有的 shell 脚本或编写自己的脚本，理解引号的使用是非常重要的。

## 文件名扩展

使用 C shell 的另一个重要部分是文件名扩展。当我们讲解 shell 编程时，你肯定会准备处理文件名的 shell 脚本。在开始编写 shell 脚本之前，对文件名扩展进行概述有助于确保你对这一主题感到熟悉。

表 7-4 列出了一些常见的文件名扩展和模式匹配。

### 表 7-4 文件名扩展和模式匹配

| 字符 | 示例 | 描述 |
|---|---|---|
| * | 1) ls *.c | 匹配零个或多个字符 |
| ? | 2) ls conf.? | 匹配任意单个字符 |
| [list] | 3) ls conf.[co] | 匹配列表中的任意字符 |
| [lower-upper] | 4) ls libddd.9873[5-6].sl | 匹配范围内任意字符 |
| str{str1,str2,str3,...} | 5) ls ux*.{700,300} | 用 {} 内的内容扩展 str |
| ~ | 6) ls -a ~ | 主目录 |
| ~username | 7) ls -a ~gene | 用户名的主目录 |

以下是表 7-4 中所示示例的详细扩展说明：

- 1. 若要列出目录中所有以 ".c" 结尾的文件，可以执行以下操作：

```bash
sys1 30: ls *.c
conf.SAM.c conf.c
```

- 2. 若要找到目录中所有名为 "conf" 且扩展名为单个字符的文件，可以执行以下操作：

```bash
sys1 31: ls conf.?
conf.c conf.o conf.l
```

- 3. 若要列出目录中所有名为 "conf" 且扩展名仅为 "c" 或 "o" 的文件，可以执行以下操作：

```bash
sys1 32: ls conf.[co]
```

![](img/75f39fc91296b889c0653851accdfd46_411_0.png)

```bash
conf.c conf.o
```

- 4. 若要列出名称相似但特定字段涵盖一定范围的文件，可以执行以下操作：

```bash
sys1 46: ls libddd9873[5-6].sl
libddd98735.sl libddd98736.sl
```

- 5. 若要列出以 "ux" 开头且扩展名为 "300" 或 "700" 的文件，可以执行以下操作：

```bash
sys1 59: ls ux*.{700,300}
uxbootif.700 uxinstrfs.300 unixstern.300
unistkern.700 unistlf.700
```

- 6. 若要列出你主目录中的文件，可以使用 ~：

```bash
sys1 62: ls -a ~
. .cshrc.org .login .shrc.org
.. .excrc .login.org .vue
.cshrc .history .profile .vueprofile
```

- 7. 若要列出某用户主目录中的文件，可以执行以下操作：

```bash
sys1 65: ls -a ~gene
. .history .vue splexdat
.. .login .vueprofile trail.txt
.cshrc .login.org ESP-File under.des
.cshrc .org .profile Mail xtra.part
.excrc .shrc.org opt
```

许多这些技术在编写 shell 脚本时非常有用，因此你需要熟悉文件名扩展。

## 重定向 (I/O 重定向)

UNIX 系统配置为命令通常从键盘获取输入（通常称为标准输入），并将输出发送到屏幕（通常称为标准输出）。命令还将错误信息发送到屏幕。你并不总是希望输入来自标准输入，且输出和错误信息去往标准输出。如果你编写大量脚本，需要控制以覆盖这些默认设置。这被称为重定向。表 7-5 展示了许多常见的重定向形式。

如表中所示，要将命令的输出从标准重定向到文件，你会使用 ">"。这在几乎所有情况下都有效。如果你设置了一个名为 **noclobber** 的环境变量，那么重定向到现有文件将不起作用。**noclobber** 不允许重定向覆盖现有文件。如果你尝试覆盖现有文件，例如下面的 /tmp/processes，你会收到一个文件已存在的消息：

```bash
# ps -ef > /tmp/processes
/tmp/processes: File exists
```

![](img/75f39fc91296b889c0653851accdfd46_412_0.png)

然而，你可以使用 "!" 与重定向一起强制文件被覆盖。使用 ">!" 强制文件被覆盖，而 ">>!" 将强制输出追加到现有文件的末尾。表 7-5 中展示了这些用法示例。

### 表 7-5 常用的重定向形式

| 命令或赋值 | 示例 | 描述 |
|---|---|---|
| < | wc -l < .login | 标准输入重定向：执行 wc (单词计数) 并列出 .login 中的行数 (-l) |
| > | ps -ef > /tmp/processes | 标准输出重定向：执行 ps 并将输出发送到文件 /tmp/processes |
| >> | ps -ef >> /tmp/processes | 追加标准输出：执行 **ps** 并将输出追加到文件 /tmp/processes 的末尾 |
| >! | ps -ef >! /tmp/processes | 标准输出重定向并覆盖 **noclobber**：即使 /tmp/processes 存在也进行写入 |
| >>! | ps -ef >>! /tmp/processes | 追加标准输出并覆盖 **noclobber**：追加到 /tmp/processes 的末尾 |
| \| | ps \| wc -l | 运行 **ps** 并将其结果作为 **wc** 的输入 |
| 0 | - | 标准输入 |
| 1 | - | 标准输出 |
| 2 | - | 标准错误 |
| 2> | cat program 2> errors | 将文件 **program** cat 到标准输出，并将错误重定向到文件 **errors** |
| 2>> | cat program 2>> errors | 将文件 **program** cat 到标准输出，并将错误追加到文件 **errors** |
| >& | cat program >& outfile | 将文件 **program** 和 **errors** 都 cat 到文件 **outfile** |
| ( ) >& | (cat program > outfile) >& errors | 将文件 **program** cat 到 **outfile**，并将错误重定向到文件 **errors** |

## Shell 和环境变量

对于你的 UNIX 系统来说，你确实是特殊的。C shell 中关于你的用户环境的信息存储在 shell 变量和环境变量中。

Shell 变量有时被称为"局部"变量。Shell 变量仅在其创建的 shell 中已知。

环境变量有时被称为"全局"变量。环境变量在创建它们的 shell 中定义，并被从原始 shell 派生的所有 shell 继承。因为这些变量传递给从原始 shell 派生的 shell，所以它们被认为是全局的。

你可以使用 set 命令查看 shell 变量，使用 env 命令查看环境变量，如下所示：

```bash
sys1 22: set
argv ()
autologout 600
cwd /home/martyp2
history 20
home /home/martyp2
noclobber
path (/usr/bin /usr/ccs/bin /usr/contrib/bin /opt/net-tl adm/bin /opt/pd/bin /)
prompt sys1 !:
savhist 20
shell /usr/bin/csh
status 0
system sys1
term vt100

sys1 23: set
argv ()
autologout 600
cwd /home/martyp2
history 20
home /home/martyp2
noclobber
path (/usr/bin /usr/ccs/bin /usr/contrib/bin /opt/net-tl adm/bin /opt/pd/bin /)
prompt sys1 !:
savhist 20
shell /usr/bin/csh
status 0
system sys1
term vt100

sys1 24:

sys1 24: env
HOME=/home/martyp2
PATH=/usr/bin:/usr/ccs/bin:/usr/contrib/bin:/opt/net-tl adm/bin:/opt/pd/bin:/opt/n
LOGNAME=martyp2
TERM=vt100
SHELL=/usr/bin/csh
MAIL=/var/mail/martyp2
COLUMNS=80
LINES=24
```

