
```bash
$ paste llsum.out ll.out
FILENAME             SIZE      total 792
README               810      -rwxrwxrwx
backup_files         3408     -rwxrwxrwx
biography            427      -rwxrwxrwx
cshtest              1024     drwxr-xr-x
gkill                1855     -rwxrwxrwx
gkill.out            191      -rw-r--r--
hostck               924      -rwxrwxrwx
ifstat               1422     -rwxrwxrwx
ifstat.int            2147    -rwxr-xr-x
ifstat.out             723     -rw-r--r--
intros               54018    -rw-r--r--
introux              52476    -rwxrwxrwx
letter               23552    -rw-r--r--
letter.auto          69632    -rw-r--r--
letter.auto.recover  71680    -rw-r--r--
letter.backup        23552    -rw-r--r--
letter.lck            57      -rw-rw-rw-
letter.recover      69632     -rw-r--r--
ll.out               1057     -rw-r--r--
llsum                1267     -rwxrwxrwx
llsum.orig           1267     -rwxr-xr-x
llsum.out            1657     -rw-r--r--
llsum.tomd.out       1356     -rw-r--r--
psg                  670      -rwxrwxrwx
psg.int              802      -rwxr-xr-x
psg.out              122      -rw-r--r--
sam_adduser          1010     -rwxrwxrwx
tdolan               1024     drwxr-xr-x
trash                4554     -rwxrwxrwx
trash.out            329      -rw-r--r--
typescript           679      -rw-r--r--
$
```

![](img/75f39fc91296b889c0653851accdfd46_662_0.png)

这生成了一个列表，其中包含来自 `llsum.out` 的 `FILENAME` 和 `SIZE` 以及来自 `ll.out` 的权限。

![](img/75f39fc91296b889c0653851accdfd46_662_1.png)

如果两个文件具有相同的第一字段，你可以使用 `join` 命令合并这两个文件：

![](img/75f39fc91296b889c0653851accdfd46_662_2.png)

以下是 `paste` 和 `join` 命令的总结，包含一些常用的选项：

# `paste` - 合并文件中的行。

## 选项

- `-d list` 使用 `list` 作为列之间的分隔符。你可以使用特殊的转义序列作为分隔符，例如 `\n` 表示换行符，`\t` 表示制表符。

![](img/75f39fc91296b889c0653851accdfd46_663_0.png)

![](img/75f39fc91296b889c0653851accdfd46_663_1.png)

# `join` - 合并两个具有公共键字段的已排序文件。

## 选项

- `-a n` 生成正常输出，并为文件 1 或 2 中无法连接的每一行生成一行输出。
- `-e string` 使用 `string` 替换输出中的空字段。
- `-t char` 使用 `char` 作为字段分隔符。

### `tr`

![](img/75f39fc91296b889c0653851accdfd46_663_2.png)

`tr` 命令用于转换字符。`tr` 非常适合此类任务，例如更改大小写。例如，如果你想将所有小写字符转换为大写，该怎么办？以下示例展示了列出后缀为 "zip" 的文件，然后将这些文件名转换为大写的过程：

![](img/75f39fc91296b889c0653851accdfd46_663_3.png)

```
$ ls -al *.zip
file1.zip
file2.zip
file3.zip
file4.zip
file5.zip
file6.zip
file7.zip
$ ls -al *.zip | tr "[:lower:]" "[:upper:]"
FILE1.ZIP
FILE2.ZIP
FILE3.ZIP
FILE4.ZIP
FILE5.ZIP
FILE6.ZIP
FILE7.ZIP
$
```

在此情况下我们使用方括号，因为我们要转换的是一类字符。

以下是 `tr` 命令的摘要，包含一些更常用的选项。

![](img/75f39fc91296b889c0653851accdfd46_664_0.png)

# `tr` - 转换字符。

## 选项

- `-A` 基于字节逐个进行转换。
- `-d` 删除所有指定的字符。
- `[:class:]` 从一类字符转换到另一类，例如从小写字母类转换为大写字母类，如示例所示。

### 第 10 章中使用的某些命令的手册页

以下是该章节中使用的许多命令的 HP-UX 手册页。不同的 UNIX 变体之间命令往往存在差异，因此你可能会发现某些命令在选项或其他方面有所不同；然而，以下手册页可作为极佳的参考。

![](img/75f39fc91296b889c0653851accdfd46_666_0.png)

# `awk` - 模式处理语言。

## `awk(1)`

### 名称

`awk` - 模式驱动的扫描和处理语言

### 概要

```
awk [-Ff s] [-v var=value] [program | -f progfile ...] [file ...]
```

### 描述

`awk` 扫描每个输入文件，查找匹配 `program` 中或作为 `-f progfile` 指定的一个或多个文件中定义的一组模式中任意一个的行。每个模式可以关联一个动作，当文件中的行匹配该模式时执行该动作。每一行都会与每个模式-动作语句的模式部分进行匹配，并对每个匹配的模式执行关联的动作。文件名 `-` 表示标准输入。形式为 `var=value` 的任何文件都被视为赋值，而不是文件名。除非使用 `-v` 选项，否则赋值在其本应作为文件名打开的时间点进行评估。

输入行由字段组成，字段之间以空白或正则表达式 `FS` 分隔。字段用 `$1, $2, ...` 表示，`$0` 指代整行。

### 选项

`awk` 识别以下选项和参数：

- `-F fs` 指定用于分隔字段的正则表达式。默认情况下识别空格和制表符字符，并丢弃前导空格和制表符。如果使用了 `-F` 选项，则不再丢弃前导输入字段分隔符。
- `-f progfile` 指定一个 `awk` 程序文件。最多可以指定 100 个程序文件。这些文件中的模式-动作语句按照文件指定的顺序执行。
- `-v var=value` 使 `var=value` 赋值在 `BEGIN` 动作（如果存在）执行之前发生。

### 语句

模式-动作语句的形式为：

```
pattern { action }
```

缺少 `{ action }` 意味着打印该行；缺少模式意味着始终匹配。模式-动作语句之间用换行符或分号分隔。

动作是一系列语句。语句可以是以下内容之一：
