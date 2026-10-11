
选项可以包含空格——你只需要将其放在引号外面，这样空格就会包含在内。例如，为了在密码文件中搜索我的名字，我输入了以下 `grep` 命令（`grep` 用于在文件中搜索文本）：

```
grep "Emmett Dulaney" /etc/passwd
```

当 `grep` 打印出带有我名字的行时，它看起来像这样：

```
deulaney:x:1000:100:Emmett Dulaney:/home/deulaney/bin/bash
```

如果你用自己的用户名创建了账户，请以该用户名作为参数输入 `grep` 命令，在 `/etc/passwd` 文件中查找该用户名。

在 `grep` 命令的输出中，你可以看到冒号（`:`）后面的 shell 名称（`/bin/bash`）。

当然，命令选项的数量及其格式取决于具体的命令。通常，这些选项（如 `-x`）是单个字符。例如，`ls` 命令列出目录的内容。你可以使用 `-l` 选项来查看更多细节。例如，这里是在用户主目录下输入 `ls -l` 的结果：

```
total 0
drwxr-xr-x users 48 2005-09-08 21:11 bin
drwx------ users 32 2005-09-08 21:16 Desktop
drwx------ users 80 2005-09-08 21:11 Documents
drwxr-xr-x users 80 2005-09-08 21:11 public_html
drwxr-xr-x users 464 2005-09-17 18:21 sdump
```

如果一个命令太长无法排在一行内，你可以按下反斜键（`\`）然后按回车。接着在下一行继续输入命令。例如，输入以下命令（每行后按回车）。

```
cat \
/etc/passwd
```

## 96 使用 bash Shell

`cat` 命令随后会显示 `/etc/passwd` 文件的内容。

你可以在一行中拼接（即串联）多个较短的命令。只需用分号（`;`）将命令隔开即可。例如，以下命令

```
cd; ls -l; pwd
```

会将当前目录切换到家目录，列出该目录的内容，然后显示目录名称。

## 组合 shell 命令

你可以组合简单的 shell 命令来创建一个更复杂的命令。例如，假设你想找出名为 `spbcd` 的设备是否存在于你系统的 `/dev` 目录中，因为某些文档说你为 Sound Blaster Pro CD-ROM 驱动器需要该设备。你可以使用 `ls /dev` 命令获取 `/dev` 目录的目录列表，然后浏览它以查看是否存在 `spbcd`。

遗憾的是，`/dev` 目录有很多非常棒的条目，你可能会发现很难找到任何名称中包含 `spbcd` 的项。不过，你可以将 `ls` 与 `grep` 组合，构造出一个完全符合你要求的命令行。这里是该命令行：

```
ls /dev | grep spbcd
```

shell 将 `ls` 命令的输出（目录列表）发送给 `grep` 命令，`grep` 会搜索字符串 `spbcd`。竖线（`|`）被称为管道（pipe），因为它在两个程序之间充当导管（想象成水管）——第一个命令的输出被喂送到第二个命令的输入中。

## 控制命令的输入和输出

大多数 Linux 命令都有共同特征——它们始终从标准输入（通常是键盘）读取，并写入标准输出（通常是屏幕）。错误信息被发送到标准错误（通常也到屏幕）。这三个设备通常被称为 `stdin`、`stdout` 和 `stderr`。

你可以让命令从文件获取输入，然后将其输出发送到另一个文件。让你知道一下，这种功能的专业术语是输入/输出重定向或 I/O 重定向。

表 3-1 显示了常用 I/O 重定向命令的语法，接下来的几节将解释如何使用这些命令。

| 表 3-1 | 常用标准 I/O 重定向 |

| :--- | :--- |

| 任务 | 命令语法 |

| 将 stdout 发送到文件 | command > file |

| 将 stderr 发送到文件 | command 2> file |

| 将 stdout 和 stderr 发送到文件 | command > file 2>&1 |

| 从文件读取 stdin | command < file |

| 从 file.in 读取 stdin并将 stdout 发送到 file.out | command < file.in > file.out |

| 将 stdout 追加到文件末尾 | command >> file |

| 将 stderr 追加到文件末尾 | command 2>> file |

| 将 stdout 和 stderr 追加到文件末尾 | command >> file 2>&1 |

| 从文件读取 stdin | command < file |

| 将 stdout 管道到文件 | command | file |

| 将 stderr 管道到文件 | command 2> file |

### 从文件获取 stdin

如果你想从文件读取输入，使用 `<` 符号。例如，输入：

```
cat < /etc/passwd
```

`cat` 命令显示 `/etc/passwd` 的内容。

### 保存输出到文件

如果你想将输出发送到文件，使用 `>` 符号。例如，输入：

```
cat /etc/passwd > output.txt
```

`cat` 命令显示 `/etc/passwd` 的内容。

### 追加到文件末尾

如果你想将输出追加到文件末尾，使用 `>>` 符号。例如，输入：

```
cat /etc/passwd >> output.txt
```

`cat` 命令显示 `/etc/passwd` 的内容。

### 重定向错误到文件

如果你想将错误信息重定向到文件，使用 `2>` 符号。例如，输入：

```
ls /nonexistent_directory 2> error.txt
```

`ls` 命令在 `error.txt` 中显示错误信息。

### 重定向 stdout 和 stderr

如果你想将 `stdout` 和 `stderr` 都重定向到文件，使用 `>2>&1` 符号。例如，输入：

```
ls /nonexistent_directory > output.txt 2>&1
```

`ls` 命令在 `output.txt` 中显示错误信息。

### 从文件读取 stdin

如果你想从文件读取输入，使用 `<` 符号。例如，输入：

```
cat < file.txt
```

`cat` 命令显示 `file.txt` 的内容。

### 重定向输入并发送输出

如果你想从一个文件重定向输入并将输出发送到另一个文件，使用 `<` 和 `>` 符号。例如，输入：

```
cat < input.txt > output.txt
```

`cat` 命令显示 `input.txt` 的内容。

# 100 使用 bash Shell

你可以在 `bash` 中使用三种类型的通配符：

- `*` **星号 (*)** 匹配文件名中的零个或多个字符。这意味着 `*` 表示目录中的所有文件。
- `?` **问号 (?)** 匹配任意单个字符。如果你输入 `test?`，它将匹配以 `test` 开头的五个字符的文本。
- **括号中的字符集** 匹配集合中的任意单个字符。例如，字符串 `[AB]*` 匹配任何以 a 或 B 开头的文件名。

当你想要对大量文件进行操作时，通配符非常有用。例如，要将 `/media/cdrom` 目录下的所有文件复制到当前目录，请输入以下命令：

```
cp /media/cdrom/*
```

`bash` 将通配符 `*` 替换为 `/media/cdrom` 目录中所有的文件名。命令末尾的点表示当前目录。

你可以将星号与文件名的其他部分配合使用选择特定的文件组。假设你想使用 `grep` 命令在 `/usr/include` 目录下的搜索符合以下条件的 `typedef struct` ：

- 文件名以 s 开头。
- 文件名以 .h 结尾。

通配符规范 `*.h` 表示所有符合这些标准的文件名。因此你可以使用以下命令执行搜索：

```
grep `typedef struct` /usr/include/s*.h
```

字符串中包含一个你想让 `grep` 命令查找的空格，因此你必须将字符串包含在引号中。这样，`bash` 就不会尝试将其中的单词视为独立的命令参数。

问号 `?` 匹配单个字符。假设你在当前目录下有四个文件——`image1.pcx`、`image2.pcx`、`image3.pcx` 和 `image4.pcx`。要将这些文件复制到 `/media/floppy` 目录，请使用以下命令：

```
cp image?.pcx /media/floppy
```

# bash Shell 101

`bash` 将单个问号替换为任意单个字符，并将四个文件复制到 `/media`。

第三种通配符格式 `[...]` 匹配方括号内特定字符集中的单个字符。你可能想将其与其他通配符结合，将文件名缩小到更小的集合。如果你想查看 `/etc/X11/xdm` 目录下所有以 x 或 X 开头的文件列表，输入以下命令：

```
ls /X11/xdm/]*
```

## 重复之前输入的命令
