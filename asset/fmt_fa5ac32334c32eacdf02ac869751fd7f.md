
Bash 有时能猜出你在想什么。你可以输入命令或路径名的一部分，Bash 可以为你补全剩余部分。你可以输入命令或路径名的一部分，并使用 `tab` 键补全命令。例如，如果你希望发出 `run-level` 命令以查看当前系统运行级别，但记不住完整命令，你可以键入 `run` 和 `tab` 键，命令就会为你补全，如下例所示：

```
# run<tab key>level 
N 3 
```

Bash 确定以 `run` 开头的唯一命令是 `runlevel`，并补全了该命令。

只要你发出的命令或路径名足够独特，Bash 就会为你补全它。如果命令或路径名不唯一，Bash 会显示补全该命令的选项。以下示例显示键入 `ru` 和两个 `tab` 键以获取以 `ru` 开头的命令列表：

```
# ru<tab key><tab key>
runlevel  rusers
```

从这个例子中可以看出，键入 `ru` 产生了两个可能的命令 - `runlevel` 和 `rusers`。

这种出色的补全功能也适用于路径名。如果你将目录更改为 `/b`，你会得到以下结果：

```
# cd /b<tab key><tab key>
bin  boot
```

![](img/75f39fc91296b889c0653851accdfd46_304_0.png)

因为根级别有两个以 `b` 开头的目录，Bash 无法确定你想要哪一个，所以列出了两者。

### 文件名扩展

在我们能够覆盖即将到来的主题以及 shell 编程章节的内容之前，你需要查看文件名扩展。作为操纵文件用户，你肯定正在编写处理文件名的 shell 脚本。文件名扩展的概述是有帮助的，以确保在你开始编写 shell 脚本之前，你能舒适地处理这个主题。

表 5-3 列出了一些常见的文件名扩展和模式匹配。

## 表 5-3 文件名扩展和模式匹配

| 字符 | 示例 | 描述 |
|---|---|---|
| * | `ls *.c` | 匹配零个或多个字符 |
| ? | `ls conf.?` | 匹配任意单个字符 |
| [list] | `ls conf.[co]` | 匹配列表中的任意字符 |
| [lower-upper] | `ls libdd.9873[5-6].sl` | 匹配范围内的任意字符 |
| str{str1,str2,str3,...} | `ls ux*.{700,300}` | 使用 {} 中的内容扩展 str |
| ~ | `ls -a ~` | 主目录 |
| ~username | `ls -a ~gene` | username 的主目录 |

表 5-3 中所示示例的更详细说明如下：

- 1. 要列出目录中以 `.c` 结尾的所有文件，可以执行以下操作：

```bash
$ ls *.c
conf.SAM.c conf.c
```

- 2. 要查找目录中名为 `conf` 且扩展名为单个字符的所有文件，可以执行以下操作：

```bash
$ ls conf.?
conf.c conf.o conf.l
```

- 3. 要列出目录中名为 `conf` 且扩展名仅为 `c` 或 `o` 的所有文件，可以执行以下操作：

```bash
$ ls conf.{co}
conf.c conf.o
```

- 4. 要列出名称相似但包含一个范围字段的文件，可以执行以下操作：

```bash
$ ls libddd9873[5-6].sl
libddd98735.sl libddd98736.sl
```

- 5. 要列出以 `ux` 开头且扩展名为 `300` 或 `700` 的文件，可以执行以下操作：

```bash
$ ls ux*.{700,300}
uxboot1f.700 uxinstd.300
```

- 6. 要列出主目录中的文件，可以使用 `~`：

```bash
$ ls -a ~
.       .cshrc.org .login .shrc.org
..      .exrc      .login.org .cshrc
.history
```

- 7. 要列出某用户主目录中的文件，可以执行以下操作：

```bash
$ ls -a ~gene
.       .history .splinedat under.des
..      .login traxl.txt xtra.part
.cshrc  .login.org ESP-File
.cshrc.org .profile Mail
.exrc   .shrc.org opt
```

![](img/75f39fc91296b889c0653851accdfd46_306_0.png)

许多这些技术在编写 shell 脚本时非常有用，因此请熟悉文件名扩展。

### 重定向（I/O 重定向）

UNIX 的设置通常是命令从键盘（通常称为标准输入）接收输入，并将输出发送到屏幕（通常称为标准输出）。命令还将错误信息发送到屏幕。你并不总是希望输入来自标准输入，输出和错误去往标准输出。你被赋予了大量的控制权来覆盖这些默认设置。这被称为重定向。表 5-4 展示了许多常见的重定向形式。

如表所示，要将命令的输出从标准输出重定向到文件，应使用 `>` 或 `>`。这几乎在所有情况下都有效。如果你设置了一个名为 `noclobber` 的环境变量，则重定向到现有文件将不起作用（我们稍后将介绍环境变量）。`noclobber` 不允许重定向覆盖现有文件。如果你试图覆盖现有文件，例如下面的 `/tmp/processes`，你会收到一条文件已存在的消息：

```bash
# ps -ef > /tmp/processes
/tmp/processes: File exists
```

![](img/75f39fc91296b889c0653851accdfd46_307_0.png)

然而，你可以使用重定向中的 `!` 来强制覆盖文件。使用 `>!` 强制覆盖文件，而 `>>!` 强制将输出附加到现有文件的末尾。这些示例在表 5-4 中有所展示。

## 表 5-4 常见的重定向形式

| 命令或赋值 | 示例 | 描述 |
|---|---|---|
| < | `wc -l < .login` | 标准输入重定向：执行 `wc`（单词计数）并列出 `.login` 中的行数（-l） |
| > | `ps -ef > /tmp/processes` | 标准输出重定向：执行 `ps` 并将输出发送到文件 `/tmp/processes` |
| >> | `ps -ef >> /tmp/processes` | 追加标准输出：执行 `ps` 并将输出追加到文件 `/tmp/processes` 的末尾 |
| >! | `ps -ef >! /tmp/processes` | 输出重定向并覆盖 `noclobber`：即使 `/tmp/processes` 存在也将其覆盖 |
| >>! | `ps -ef >>! /tmp/processes` | 追加标准输出并覆盖 `noclobber`：追加到 `/tmp/processes` 的末尾 |
| (pipe) | `ps \| wc -l` | 运行 `ps` 并将其结果作为 `wc` 的输入 |
| 2> | `cat program 2> errors` | `cat` 文件 `program` 到标准输出，并将错误重定向到文件 `errors` |
| 2>> | `cat program 2>> errors` | `cat` 文件 `program` 到标准输出，并将错误追加到文件 `errors` |
| 2> | `find / -name '*.c' -print > cprograms 2> errors` | `find` 系统中所有以 `.c` 结尾的文件，将文件列表放在当前工作目录的 `cprograms` 中，并将所有错误（文件描述符 2）发送到当前工作目录的文件 `errors` |
| 2>&1 | `find / -name '*.c' -print > cprograms 2>&1` | `find` 系统中所有以 `.c` 结尾的文件，将文件列表放在当前工作目录的 `cprograms` 中，并将所有错误（文件描述符 2）发送到与文件描述符 1（`cprograms`）相同的地方 |

### 环境变量

环境变量是一个与字符串相关联的名称。名称是变量，字符串是其值。当你在系统中发出命令时，你通常输入的是相对路径名，而不是绝对路径名。你发出的命令之所以能被找到，是因为 `PATH` 变量指向命令所在目录的位置。如果没有这个 `PATH` 变量，你将不得不键入你发出的每个命令的绝对路径名。当你发出命令时，shell 按照 `PATH` 变量中列出的顺序搜索目录中列出的目录。使用 `env` 命令查看你设置的许多环境变量是一个好方法，如下所示，在我的 Linux 系统上：
