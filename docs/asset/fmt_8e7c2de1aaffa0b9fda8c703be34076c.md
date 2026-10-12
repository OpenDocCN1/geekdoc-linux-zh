
| 命令 | 描述 |
| :--- | :--- |
| `uname` | 显示当前系统名称 |
| `uptime` | 获取系统正常运行时间 |
| `useradd` | 创建一个用户账户 |
| `users` | 打印已登录用户的名称 |
| `vmstat` | 报告虚拟内存统计信息 |
| `w` | 显示已登录用户在做什么 |
| `who` | 列出已登录用户 |

# 第十七章：正则表达式

正则表达式是一种字符串，可用于描述多个字符序列。多个不同的 Unix 命令使用正则表达式，包括 `ed`、`sed`、`awk`、`grep`，以及在较小程度上使用的 `vi`。这里 `sed` 代表 *流编辑器*，这是一种面向流的编辑器，专门用于执行脚本。因此，您输入的所有数据都会通过并传递到 `STDOUT`，并且它不会改变输入文件。

## 调用 sed

在开始之前，请确保您有一份 `/etc/passwd` 文本文件的本地副本，以便使用 `sed` 进行工作。如前所述，可以通过管道将数据发送到 `sed` 来调用它，如下所示：

```bash
$ cat /etc/passwd | sed
Usage: sed [OPTION]... {script-other-script} [input-file]...

-n, --quiet, --silent
                 suppress automatic printing of pattern space
-e script, --expression=script
                 "..." 
```

`cat` 命令将 `/etc/passwd` 的内容通过管道转储到 `sed` 的模式空间。模式空间是 `sed` 用来执行工作的内部工作缓冲区。

## sed 的一般语法

`sed` 的一般语法：

```
/pattern/action
```

这里，*pattern*（模式）是一个正则表达式，而 *action*（动作）是下表中的命令之一。如果省略 *pattern*，则如前所述，*action* 将对每一行执行。

包围模式的斜杠字符 (`/`) 是必需的，因为它们用作分隔符。

| 命令 | 描述 |
| :--- | :--- |
| `P` | 打印该行 |
| `D` | 删除该行 |
| `s/pattern1/pattern2/` | 替换第一个出现的内容 |

## 使用 sed 删除所有行

再次调用 `sed`，但这次告诉 `sed` 使用编辑命令删除行，用单个字母 `d` 表示：

```bash
$ cat /etc/passwd | sed 'd'
$ 
```

除了通过管道将文件发送到 `sed` 来调用它之外，您还可以指示 `sed` 从文件中读取数据，如下例所示。以下命令执行与上一个示例完全相同的工作，但没有 `cat` 命令：

```bash
$ sed -e 'd' /etc/passwd
$ 
```

## sed 地址

`sed` 还理解称为地址的概念。地址是文件中的特定位置或应应用特定编辑命令的范围。当 `sed` 没有遇到地址时，它会对文件中的每一行执行操作。

以下命令为您一直在使用的 `sed` 命令添加了一个基本地址：

```bash
$ cat /etc/passwd | sed '1d' | more
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
$ 
```

注意，数字 `1` 添加在删除编辑命令之前。这告诉 `sed` 在文件的第一行上执行编辑命令。在这个例子中，`sed` 将删除 `/etc/passwd` 的第一行并打印文件的其余部分。

## sed 地址范围

那么，如果你想从文件中删除多于一行怎么办？你可以如下使用 `sed` 指定地址范围：

```bash
$ cat /etc/passwd | sed '1, 5d' | more
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
$
```

上述命令将应用于从第 1 行到第 5 行的所有行。因此，它删除了前五行。请尝试以下地址范围：

| 命令 | 描述 |
| :--- | :--- |
| `'4,10d'` | 从第 4 行到第 10 行的行被删除 |
| `'10,4d'` | 只删除第 10 行，因为 `sed` 不能反向工作。 |
| `'4,+5d'` | 这将匹配文件中的第 4 行，删除该行，继续删除接下来的五行，然后停止删除并打印剩余部分 |
| `'2,5!d'` | 这将删除除了第 2 行到第 5 行之外的所有内容。 |
| `'1~3d'` | 这删除第一行，跳过接下来的三行，然后删除第四行。`sed` 继续应用此模式直到文件末尾。 |
| `'2~2d'` | 这告诉 `sed` 删除第二行，跳过下一行，删除下一行，并重复直到到达文件末尾。 |
| `'4,10p'` | 打印从第 4 行到第 10 行的行 |
| `'4,d'` | 这将产生语法错误。 |
| `',10d'` | 这也将产生语法错误。 |

*注意：* 使用 `p` 动作时，你应该使用 `-n` 选项以避免行打印重复。检查这两个命令之间的区别：

```bash
$ cat /etc/passwd | sed -n '1,3p'
```

检查上述不带 `-n` 的命令如下：

## 替换命令

替换命令由 `s` 表示，它会将您指定的任意字符串替换为另一个您指定的字符串。要将一个字符串替换为另一个字符串，您需要一种方法来告诉 `sed` 第一个字符串在哪里结束以及替换字符串从哪里开始。传统上，这是通过用正斜杠 (`/`) 字符作为两个字符串的分隔符来实现的。以下命令将一行中首次出现的字符串 `root` 替换为字符串 `amrood`。

```bash
$ cat /etc/passwd | sed 's/root/amrood/'
amrood:x:0:0:root user:/root:/bin/sh
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
```

需要注意的是，`sed` 仅替换每行中首次出现的字符串。如果字符串 `root` 在一行中出现多次，只有第一个匹配项会被替换。若要指示 `sed` 执行全局替换，请在命令末尾添加字母 `g`，如下所示：

```bash
$ cat /etc/passwd | sed 's/root/amrood/g'
amrood:x:0:0:amrood user:/amrood:/bin/sh
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
```

### 替换标志

| 标志 | 描述 |
| :--- | :--- |
| `g` | 替换所有匹配项，而不仅仅是第一个匹配项。 |
| `NUMBER` | 仅替换第 `NUMBER` 个匹配项。 |
| `p` | 如果进行了替换，则打印模式空间。 |
| `w FILENAME` | 如果进行了替换，则将结果写入 `FILENAME`。 |

除了 `g` 标志外，还可以传递许多其他有用的标志，并且您可以一次指定多个标志。

### 使用备用字符串分隔符

您可能会发现需要对包含正斜杠字符的字符串执行替换。在这种情况下，您可以在 `s` 之后提供指定字符来指定不同的分隔符。

例如：

| 标志 | 描述 | 命令示例 |
| :--- | :--- | :--- |
| `I` 或 `i` | 以不区分大小写的方式匹配。 | `cat /etc/passwd \| sed 's:/root:/amrood:/g'`<br>`amrood:x:0:0:amrood user:/amrood:/bin/sh` |
| `M` 或 `m` | 除了特殊正则表达式字符 `^` 和 `$` 的正常行为外，此标志使 `^` 匹配换行符后的空字符串，使 `$` 匹配换行符前的空字符串。 | `daemon:x:1:1:daemon:/usr/sbin:/bin/sh` |

在上面的示例中，我们使用 `:` 作为分隔符而不是斜杠 `/`，因为我们试图搜索 `/root` 而不是简单的 `root`。

### 用空替换
