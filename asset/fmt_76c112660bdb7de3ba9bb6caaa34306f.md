
这将将位于 CLF 日志文件中的唯一 IP 地址，这是 Apache Web 服务器使用的格式。

## vi

`vi` 程序是一个强大的全屏文本编辑器，由于其规模和功能，它几乎可以存在于所有的 UNIX 系统上。`vi` 利用其功能不需要大量的资源。除了基本的编辑功能外，`vi` 还可以进行搜索、替换和合并文件，并且有它自己的宏语言以及许多其他附加功能。

`vi` 有两种模式。学习并理解这些模式非常重要；这会让你的生活变得简单得多。

第一个模式是输入模式。在输入模式下，可以在文档中输入文本。你可以插入或追加文本。

第二模式是命令模式。当 `vi` 处于命令模式时，你可以在文档中移动、合并行、搜索等。除了输入文本，你可以从命令模式执行 `vi` 的所有功能。只有在输入模式下才能输入文本。

典型的新手会假设自己处于输入模式并开始在文档中打字。他期望看到新输入的文本，但他看到的却是当前文档被弄乱了，因为他处于命令模式。

当 `vi` 启动时，它处于命令模式。你可以使用以下命令之一从命令模式切换到输入模式：`[aIIOccSR]`。要返回命令模式，按 `Esc` 键正常退出，或按中断（`Ctrl+C` 键序列）异常结束。

表 5-7 显示了常用 `vi` 命令及其在命令模式下的效用摘要。

### 表 5-7 常用 vi 命令总结

| 命令 | 效用 |
|---|---|
| `Ctrl+D` | 窗口向下移动一半 |
| `Ctrl+U` | 窗口向上移动一半 |
| `Ctrl+F` | 窗口向前移动一半 |
| `Ctrl+B` | 窗口向后移动一半 |
| `h` | 光标向左移动 |
| `j` | 光标向下移动一行 |
| `l` | 光标向右移动 |
| `k` | 光标向上移动一行 |
| `w` | 光标移动到下一个单词 |
| `b` | 光标移动到上一个单词 |
| `^` | 光标移动到行首 |
| `$` | 光标移动到行尾 |
| `A` | 在行尾插入文本 |
| `o` | 在行后插入文本 |
| `s` | 删除源代码行 |
| `x` | 删除字符 |
| `dw` | 删除单词 |
| `D` | 删除到行尾 |
| `w` | 保存更改 |
| `q` | 不保存退出 vi |
| `ZZ` | 保存并退出 vi |

## 第 5 章：常用命令 117

| 命令 | 效用 |
|---|---|
| `:w` | 保存更改 |
| `:q` | 不保存退出 vi |
| `:ZZ` | 保存并退出 vi |

## WC

语法：

```
wc [-lw] filename
```

`wc`（单词计数）命令统计行、字符和单词。如果使用 `wc` 命令时不带任何选项，输出将显示所有统计数据。文件 `test.txt` 包含：

```
the brown fox jumps over the lazy dog
wc test.txt
1 9 44
```

结果告诉我们一行、九个单词、44 个字符。只想显示行数，使用 `-l` 选项。`w` 选项显示单词数。最后，`c` 选项将显示总字符数。

## whatis

语法：

```
whatis keyword
```

此命令显示关键字单行描述。`whatis` 命令等同于执行 `man -f`。例如，你想显示时间，但不确定使用 `time` 还是 `date` 命令，输入：

```
whatis time date
time (1) - time a simple command
date (1)   - print the date and time
```

查看结果，你可以你需要命令是 `date`。`time` 命令实际上测量程序或命令执行的时间。

## whereis

`whereis` 命令查找指定文件的源/二进制和手册部分。提供的名称首先去除领先路径组件和任何单字符文件扩展名（如 `.c,.hand` 等）。使用源码控制产生的 `s` 前缀也会被处理。

```
whereis ls
s:/bin/ls /usr/man/man1/ls.1.gz
```

前面的示例指示了该命令的位置。`ls` 位于 `/bin` 目录，相应的手册位于 `/usr/man/man1/ls.1.gz`。

## which

语法：

```
which command
```

`which` 命令将显示任何有效执行命令的路径和别名。

```
which df
/usr/bin/df
```

前面的示例告诉我们 `df` 命令位于 `/usr/bin` 目录，它也会显示 shell 命令的信息。

```
which setenv
setenv: shell 内置命令。
```

## 文件压缩和存档特定命令

本节命令用于压缩、归档和打包文件。

# compress

语法：

```
compress [-v] file(s)
```

# 第 5 章：日常命令 119

`compress` 命令将尝试使用自适应 Lempel-Ziv 编码算法缩小文件大小。被压缩的文件将被带有 `Z` 扩展的文件替换。对文件使用任何类型的压缩都是意义的，因为较小的文件大小可以增加可用磁盘空间。此外，跨网络传输较小的文件可以减少网络拥堵。

`-v`（详细）选项将显示每个被压缩文件的压缩百分比，并告诉你新文件的名称。以下是使用 `compress` 命令的典型会话：

```
ls -alF inbox
-rw-- 1 username cscstd 194261 Feb 23 20:12 inbox
compress -v inbox
inbox: Compression: 37.20% - replaced with inbox.Z
```

```
ls -alF inbox.Z
-rw-- 1 username cscstd 121983 Feb 23 20:12 inbox.Z
```

# gunzip

语法：

```
gunzip [-v] file(s)
```

要将文件解压为原始格式，请使用 `gunzip` 命令。`gunzip` 将尝试解压扩展名为：`.gz`、`-gz`、`.z`、`-z`、`.Z` -Z 或 `tgz` 的文件。
`-v` 选项在解压文件时显示详细输出。

```
gunzip -v README.txt.gz
README.txt.gz: 65.0% - replaced with README.txt
```

# gzip

语法：

```
gzip [-rv9] file(s)
```

`gzip` 命令是另一个压缩程序。它以具有最佳压缩率之一而闻名，但这是有代价的。它可能会很慢。用 `gzip` 压缩的文件将被带有 `.gz` 扩展的文件替换。

`-9` 选项将牺牲速度以获得最佳压缩。`-v` 选项是详细选项。将列出每个文件的大小、总量和压缩率。此外，`-r` 选项将递归遍历每个目录，压缩路径上的所有文件。

## 第二部分：作为超级用户工作

```
ls -alF README.txt
-rw-r-r- 1 root root                16213 Oct 14 13:55 README.txt
```

```
gzip -9v README.txt
README.txt:                               65.0% - replaced with README.txt.gz
```

```
ls -alF README.txt.gz
-rw-r-r- 1 root root                5691 Oct 14 13:55 README.txt.gz
```

# rpm

语法：

```
rpm -[ivhqladefUV] [-force] [-nodeps] [-oldpackage] package list
```

这是 RedHat 包管理器（Red Hat Package Manager）。它允许你管理 RPM 包，使安装和卸载软件变得非常简单。

要安装新的 RPM 包 `precious-software-1.0.i386.rpm`，请运行：

```
rpm -i precious-software-1.0.i386.rpm
```

你可以使用 `-iv` 代替单独的 `-i` 选项来让 `rpm` 输出更详细。如果你已经安装了该包，且由于某些原因你想在旧安装之上重新安装，你将需要使用 `--force` 选项来强制 `rpm` 执行。

如果你正在升级软件包，应该使用 `-U` 选项。例如：

```
rpm -Uvh precious-software-2.0.i386.rpm
```

此命令将以前版本的 `precious-software` 包升级到版本 2.0 版本。然而，如果你已经安装了更新的版本，`rpm` 会检测到并显示错误信息，提示返回之前的版本，或者安装的版本比你尝试安装的版本新。在这种情况下，如果你决定仍然继续，可以使用 `-U` 选项配合 `-oldpackage` 选项来强制 `rpm` 降级你的软件。

要查找系统中安装的所有可用包列表，请运行：

```
rpm -qa
```

要查找诸如 `sendmail` 的程序属于哪个包，请运行：

```
rpm -q sendmail
```
