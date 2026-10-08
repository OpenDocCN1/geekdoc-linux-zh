

## 表 6-1 命令和路径补全

表 6-1 总结了前面示例中使用的命令和路径补全方式。

| 单词或命令<br>（在每个单词前输入转义字符） | 结果 |
| :-------------------------------------- | :------------------------- |
| wordescape=          | 显示以 word 开头的文件名编号列表。 |
| wordescape*          | 用所有匹配的文件替换 word。 |
| wordescape\          | 用第一个以 word 开头的文件名替换 word。 |
| command wordescape=  | 显示以 word 开头的文件名编号列表。 |
| command wordescape*  | 用所有匹配的文件替换 word。 |
| command wordescape_  | 在光标位置插入上一条命令的最后一个单词。 |
| command wordescape_3 | 在光标位置插入上一条命令的第三个单词。 |

## 文件名扩展

在 ksh 的一般操作活动中，你必须执行大量与文件名相关的工作，包括处理文件名的 shell 脚本的编写。文件名扩展的概述对于确保你在开始编写 shell 脚本之前熟悉该主题非常有用。

表 6-2 列出了一些常见的文件名扩展和模式匹配。

![](img/75f39fc91296b889c0653851accdfd46_350_0.png)

### 表 6-2 文件名扩展和模式匹配

| 字符 | 示例 | 描述 |
|---|---|---|
| * | 1) ls *.c | 匹配零个或多个字符 |
| ? | 2) ls conf.? | 匹配任意单个字符 |
| [list] | 3) ls conf.[co] | 匹配列表中的任意字符 |
| [lower-upper] | 4) ls libdd.9873[5-6],sl | 匹配范围内的任意字符 |
| str{str1,str2,str3,...} | 5) ls ux*.{700,300} | 用 {} 中的内容展开 str |
| ~ | 6) ls -a ~ | 主目录 |
| ~username | 7) ls -a ~gene | username 的主目录 |

以下是表 6-2 中所示示例的更详细描述：

- 1. 要列出目录中所有以“.c”结尾的文件，您可以执行以下操作：
```
$ ls *.c
conf.SAM.c conf.c
```

- 2. 要查找目录中所有名为“conf”且扩展名为一个字符的文件，您可以执行以下操作：
```
$ ls conf.?
conf.c conf.o conf.1
```

- 3. 要列出目录中所有名为“conf”且扩展名仅为“c”或“o”的文件，您可以执行以下操作：
```
$ ls conf.{co}
conf.c conf.o
```

- 4. 要列出名称相似但特定字段覆盖某个范围的文件，您可以执行以下操作：
```
$ ls libdd9873[5-6].sl
libdd98735.sl libdd98736.sl
```

- 5. 要列出以“ux”开头且扩展名为“300”或“700”的文件，您可以执行以下操作：
```
$ ls ux*.{700,300}
uxbootlf.700 uxinstdf.300
```

- 6. 要列出主目录中的文件，您可以使用 ~：
```
$ ls -a ~
.    .cshrc.org    .login    .shrc.org
..    .exrc    .login.org    .cshrc
.history
```

- 7. 要列出某用户主目录中的文件，您可以执行以下操作：
```
$ ls -a ~gene
.
.history
splusddat
under.des
...
.login
trail.txt
xtra.part
.cshrc
.login.org
ESP-File
.cshrc.org
.profile
Mail
.exrc
.shrc.org
opt
```

这些技术中的许多在 ksh 操作和编写 shell 脚本时都非常有用，因此您需要熟悉文件名扩展。

## 重定向（I/O 重定向）

UNIX 的配置方式使得命令通常从键盘（通常称为标准输入）获取输入，并将输出发送到屏幕（通常称为标准输出）。命令还将错误信息发送到屏幕。您并不总是希望输入来自标准输入，输出和错误发送到标准输出。您被赋予了大量控制权来覆盖这些默认设置。这被称为重定向。表 6-3 显示了许多常见的重定向形式。

如表 6-3 所示，要将命令的输出从标准重定向到文件，您使用 `>`。这在几乎所有情况下都有效。如果设置了名为 **noclobber** 的环境变量，则重定向到现有文件将不起作用（我们将很快介绍环境变量）。**noclobber** 不允许重定向覆盖现有文件。如果您尝试覆盖现有文件（例如下面的 `/tmp/processes`），您将收到文件已存在的消息：

![](img/75f39fc91296b889c0653851accdfd46_353_0.png)

```
$ ps -ef > /tmp/processes
/tmp/processes: File exists
```

但是，您可以使用 `!` 配合重定向强制覆盖文件。使用 `>!` 强制覆盖文件，而 `>>!` 强制将输出附加到现有文件的末尾。表 6-3 中给出了这些用法的示例。

### 表 6-3 常用的重定向形式

| 命令或赋值 | 示例 | 描述 |
| :--- | :--- | :--- |
| `<` | `wc -l < .login` | 标准输入重定向：执行 wc（字数统计）并列出 .login 中的行数（-l） |
| `>` | `ps -ef > /tmp/processes` | 标准输出重定向：执行 ps 并将输出发送到文件 /tmp/processes |
| `>>` | `ps -ef >> /tmp/processes` | 追加标准输出：执行 `ps` 并将输出追加到文件 `/tmp/processes` 的末尾 |
| `>!` | `ps -ef >! /tmp/processes` | 标准输出重定向并覆盖 **noclobber**：即使 /tmp/processes 存在也写入 |
| `>>!` | `ps -ef >>! /tmp/processes` | 追加标准输出并覆盖 **noclobber**：追加到 /tmp/processes 的末尾 |
| `\|`（管道） | `ps \| wc -l` | 运行 `ps` 并使用其结果作为 `wc` 的输入 |
| `0 - 标准输入` | | |
| `1 - 标准输出` | | |
| `2 - 标准错误` | | |
| | `cat program 2> errors` | 将文件 **program** `cat` 到标准输出，并将错误重定向到文件 **errors** |
| | `cat program 2>> errors` | 将文件 **program** `cat` 到标准输出，并将错误追加到文件 **errors** |
| | `find / -name '*.*.c' -print > cprograms 2>errors` | `find` 系统中所有以 .c 结尾的文件，将文件列表放在当前工作目录的 **cprograms** 中，并将所有错误（文件描述符 2）发送到当前工作目录的文件 **errors** |
| | `find / -name '*.*.c' -print > cprograms 2>&1` | `find` 系统中所有以 .c 结尾的文件，将文件列表放在当前工作目录的 **cprograms** 中，并将所有错误（文件描述符 2）发送到与文件描述符 1（**cprograms**）相同的位置 |

## 环境变量

环境变量是与字符串相关联的名称。名称是变量，字符串是其值。环境变量也可用于由 shell 生成的子 shell 或进程。在大多数情况下，您会看到环境变量大写，这是大多数系统上的惯例。

当您在系统上发出命令时，通常输入的是相对路径名而不是绝对路径名。您发出的命令之所以能被找到，是因为 *PATH* 变量指向了命令所在的目录位置。如果没有 *PATH* 变量，您将不得不输入发出的每个命令的绝对路径名。当您发出命令时，shell 会按照 *PATH* 变量中列出的顺序搜索目录。查看您已设置的环境变量的一种好方法是使用 **env** 命令，如下所示：

```
martyp $ env
=/usr/bin/env
MANPATH=/opt/local/ptc/sysadmin/scripts:/opt/local/ptc/man:/opt/local/altrasoftware
_INIT_ UTS_RELEASE=5.7
H2=100
_INIT_ UTS_MACHINE=sun4m
EPC=true
PATH=/usr/bin:/usr/ucb:/etc:..
WEB_SERVER=siox.rose.hp.com
_INIT_ UTS_VERSION=Generic
MODEL=SPARCstation-10
OS_REV=5.7
EDITOR=vi
_INIT_ RUN_NPREV=0
CLASSPATH=..:/usr/java/lib:
LOGNAME=martyp
_INIT_ UTS_NODENAME=sunsys
_INIT_ UTS_ISA=sparc
MAIL=/var/mail/martyp
ERASE=^H
OS=solaris
PS1=$PWD $LOGNAME $TOKEN
_INIT_ PREV_LEVEL=S
HOST=sunsys
TESTEXPERT_HOME=/opt/local/svn/te33
TA_HOME=/opt/local/platinum/solaris2/testadvise
MA_HOME=/opt/local/platinum/solaris2/memadvise
CL_LICENSE_FILE=/opt/local/Centerline/configs/license.dat
SHELL=/bin/ksh
PROFILE_DIR=/opt/local/ptc/sysadmin/profile.d
OSTYPE=solaris2
HOME=/home/martyp
_INIT_ UTS_SYSNAME=SunOS
TERM=vt100
LD_LIBRARY_PATH=:/opt/local/parasoft/lib.solaris
MWHOME=/opt/local/maisoft/mainwin/mw
FMHOME=/opt/local/adobe/frame
PWD=/home/martyp
TZ=US/Pacific
_INIT_ RUN_LEVEL=3
```

