
## 数字编号行

`cat` 的 `-n` 选项将为每一行输出编号。可按如下方式使用：

```
$ cat -n fruits
```

这会产生以下输出

```
1  Fruit  Price/lbs  Quantity
2  Banana $0.89 100
3  Peach $0.79 65
4  Kiwi $1.50 22
5  Pineapple $1.29 35
6  Apple $0.99 78
7
```

从此输出可以看出，此文件中的最后一行是空白的。我们可以使用 `-b` 选项要求 `cat` 跳过对空白行的编号，如下所示：

```
$ cat -b fruits
```

现在输出类似于以下内容：

```
1  Fruit  Price/lbs  Quantity
2  Banana $0.89 100
3  Peach $0.79 65
4  Kiwi $1.50 22
5  Pineapple $1.29 35
6  Apple $0.99 78
```

空白行仍存在于输出中，但未编号。如果空白行出现在文件中间，它会被打印但不编号：

```
$ cat -b hosts
1  127.0.0.1  localhost  loopback

2  128.32.43.52  soda.berkeley.edu  soda
```

如果指定多个文件，文件的内容将在输出中连接，但每个文件的行编号都会从 1 重新开始。作为说明，以下命令。

```
$ cat -b fruits users
```

产生以下输出

```
1 Fruit Price/lbs Quantity
2 Banana $0.89 100
3 Peach $0.79 65
4 Kiwi $1.50 22
5 Pineapple $1.29 35
6 Apple $0.99 78

1 ranga
2 vathsa
3 amma
```

## WC

现在让我们看看如何获取有关文件内容的一些信息。使用 `wc` 命令（缩写为 word count），我们可以获取文件中包含的总行数、单词数和字符数的计数。此命令的基本语法是：

```
wc [opts] files
```

这里 `opts` 是表 3.1 中给出的一或多个选项，而 `files` 是你想要检查的文件。选项 `opts` 是可选的，可以省略。

### 表 3.1 wc 选项

| 选项 | 描述 |
|---|---|
| `-l` | 行数计数。 |
| `-w` | 单词数计数。 |
| `-m` | 字符数计数。此选项在 Mac OS X、OpenBSD、Solaris 和 HP-UX 上可用。此选项在 FreeBSD 和 Linux 系统上不可用。 |
| `-c` | 字符数计数。此选项是 Linux 和 FreeBSD 上 `-m` 选项的等效项。 |

当未指定选项时，`wc` 的默认行为是打印出文件中包含的行数、单词数和字符数的摘要。例如，命令

```
$ wc fruits
```

生成以下输出：

```
8      18      219 fruits
```

第一个数字，在本例中为 8，是文件中的行数。第二个数字，在本例中为 18，是文件中的单词数。第三个数字，在本例中为 219，是文件中的字符数。行末列出了文件名。当指定多个文件时，文件名有助于识别与特定文件关联的信息。

如果指定多个文件，我们会给出每个文件的计数以及总计。例如，命令

```
$ wc fruits users
```

生成输出类似于以下内容：

```
8      18      219 fruits
3      3       19 users
11     21      237 total
```

您系统上的输出可能略有不同。

### 计数行数

要计数行数，可以使用 `-l`（即 lines）选项。例如，命令

```
$ wc -l fruits
```

生成输出

```
8 fruits
```

第一个数字，在本例中为 8，是文件中的行数。文件名列在行末。

当指定多个文件时，每个文件的行数会列出，同时列出所有指定文件的总行数。例如，命令

```
$ wc -l fruits users
```

生成输出

```
8 fruits
3 users
11 total
```

### 计数单词

要计数文件中单词数，可以使用 `-w`（即 words）选项。例如，命令

```
$ wc -w fruits
```

生成输出

```
18 fruits
```

第一个数字，在本例中为 18，是文件中的单词数。文件名列在行末。

当指定多个文件时，每个文件的单词数会列出，同时列出所有指定文件的总单词数。例如，命令

```
$ wc -w fruits users
```

生成输出

```
18 fruits
3 users
21 total
```

### 计数字符

要计数字符数，需要使用 `-m` 或 `-c` 选项。`-m` 选项在 Mac OS X、OpenBSD、Solaris 和 HP-UX 上可用。在 FreeBSD 和 Linux 系统上，应改用 `-c` 选项。

例如，在 Solaris 上命令

```
$ wc -m fruits
```

生成输出

```
219 fruits
```

生成输出

```
219 fruits
18 users
237 total
```

### 组合选项

`wc` 的选项可以组合在一起并按任意顺序指定。例如，要获取文件 `fruits` 的行数和单词数计数，可以使用以下任意命令：

```
$ wc -w -l fruits
$ wc -l -w fruits
$ wc -lw fruits
$ wc -lw fruits
```

这些命令的输出完全相同：

```
8 18 fruits
```

输出列出了文件中的行数，其后是文件中的单词数。文件名指定在行末。当指定多个文件时，每个文件的信息会列出，同时列出相应的总值。

## 操作文件

在前面的章节中，您查看了列出文件和查看其内容。在本节中，您将使用 `cp`、`mv` 和 `rm` 命令查看复制、重命名和删除文件。

### 复制文件 (cp)

`cp` 命令（copy 的缩写）用于复制文件。命令的基本语法是

```
cp src dest
```

也可以为 `cp` 指定多个源文件，前提是目标 `dest` 是一个目录。复制多个文件的语法是

```
$ cp src1 ... srcn dest
```

这里 `src1 ... srcn` 是源文件，`dest` 是目标目录。例如，以下命令

```
$ cp fruits users Documents/
```

在 `Documents` 目录中创建文件 `fruits` 和 `users` 的副本。

### 交互模式

`cp` 的默认行为是如果目标文件存在则自动覆盖。这种行为可能导致问题。可以使用 `-i` 选项（interactive 的缩写）来防止此类问题。在交互模式下，`cp` 会在覆盖任何文件之前提示确认。

假设文件 `fruits.sav` 存在，以下命令

```
$ cp -i fruits fruits.sav
```

会产生类似以下的提示：

```
overwrite fruits.sav? (y/n)
```

如果选择 y（yes），文件 `fruits.sav` 将被覆盖；否则文件保持不变。实际提示在不同版本的 UNIX 中有所不同。

### 常见错误

当遇到错误时，`cp` 会生成一条消息。以下是一些常见的错误条件：

- 源文件 `src` 是一个目录。
- 源文件 `src` 不存在。
- 当指定多个源文件 `src1 ... srcn` 时，目标 `dest` 不是一个目录。
- 与多个源文件 `src1 ... srcn` 一起指定了不存在的目标 `dest`。
- `src1 ... srcn` 中的某个源不是文件。

第一种错误类型由以下命令说明：

```
$ cp Downloads/ fruits
```

因为 `src`（本例中为 `Downloads`）是一个目录，所以会生成类似以下的错误消息：

```
cp: Downloads: is a directory
```

在本例中，`dest` 是文件 `fruits`；如果 `dest` 是一个目录，也会生成相同的错误。

第二种错误类型由以下命令说明：

```
$ cp fruits.sav
```

```
cp: cannot access fruits: No such file or directory
```

这里文件名 `fruits` 被拼错为 `fruits`，导致错误。在本例中 `dest` 是文件 `fruits.sav`；如果 `dest` 是一个目录，也会生成相同的错误。

第三种错误类型由以下命令说明：

```
$ cp fruits users fruits.sav
```

```
usage: cp [R -H | -L | -P] [-f | -i | -n] [-p] src target
cp [R -H | -L | -P] [-f | -i | -n] [-p] src ... srcN directory
```
