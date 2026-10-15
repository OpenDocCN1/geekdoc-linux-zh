
# locate

`locate` 实用程序在文件的绝对路径名中任意位置搜索您提供的字符串作为参数。因此，命令 `locate sam` 返回所有绝对路径名中包含字符串 `sam` 的文件名称，包括名为 `sample` 的目录层级中的所有文件。如果您希望进行更精细的搜索，请使用 `find`。命令 `find / -name "sam"` 仅返回名为 `sam` 的文件，而 `find / -name "*sam*"` 仅返回简单文件名中包含字符串 `sam` 的文件。

默认情况下，`locate` 搜索普通字符串；使用 `-r` 选项可使其搜索正则表达式。

## script：记录 Shell 会话

`script` 实用程序记录登录会话的一部分，包括您的输入和系统的响应。该实用程序仅适用于字符设备，例如终端或终端模拟器。它可以捕获与 `vim` 相关的会话；但是，由于 `vim` 使用控制字符来定位光标并显示不同的字体（如粗体），输出将难以阅读且可能没有用处。当您 `cat` 一个捕获了 `vim` 会话的文件时，会话内容会迅速从眼前划过。

默认情况下，`script` 将会话捕获到一个名为 `typescript` 的文件中，覆盖同名文件。以下是一个正在被 `script` 记录的会话：

```
$ script
Script started, file is typescript
$ ls -l /bin | head -5
-rwxr-xr-x. 1 root root     123 02-07 17:32 alsaunmute
-rwxr-xr-x. 1 root root    25948 02-08 03:46 arch
lrwxrwxrwx. 1 root root       4 02-25 16:52 awk -> gawk
-rwxr-xr-x. 1 root root    25088 02-08 03:46 basename
$ exit
exit
Script done, file is typescript
```

使用 `exit` 命令终止 `script` 会话。然后，您可以使用 `cat`、`less`、`more` 或编辑器查看创建的文件。以下是前面 `script` 命令创建的文件内容：

```
$ cat typescript
Script started on Tue 08 Apr 2014 10:16:36 AM PDT
$ ls -l /bin | head -5
-rwxr-xr-x. 1 root root     123 02-07 17:32 alsaunmute
-rwxr-xr-x. 1 root root    25948 02-08 03:46 arch
lrwxrwxrwx. 1 root root       4 02-25 16:52 awk -> gawk
-rwxr-xr-x. 1 root root    25088 02-08 03:46 basename
$ exit
exit

Script done on Tue 08 Apr 2014 10:16:50 AM PDT
```

如果您将编辑该文件，可以使用 `dos2unix`（第 260 页）消除 `typescript` 文件行尾出现的 `^M`（回车）字符。有关更多信息，请参阅 `script man` 页。

### 参数

参数是 `script` 写入的文件的路径名。如果未指定参数，`script` 将写入 `typescript`，如果该文件存在，则会覆盖它。

## 选项

- **追加**：`-a`（`--append`）选项向输出文件追加内容。如果没有此选项，`script` 会覆盖现有文件。

- **命令**：`-c cmd`（`--command cmd`）选项运行 `cmd` 而不是交互式 Shell。当程序在标准输出未连接到屏幕时产生不同输出时很有用。例如，当重定向时，`ls` 实用程序以列形式显示输出，而如果不重定向，则以行形式显示。

```
$ ls
memos.max  memos.sam  memos.zach  old

$ ls | cat
memos.max
memos.sam
memos.zach
old
```

`-c` 选项使您可以捕获 `ls` 的输出而无需重定向其输出。

```
$ script -c ls
Script started, file is typescript
memos.max  memos.sam  memos.zach  old  typescript
Script done, file is typescript
```

# LPI tr：替换指定字符

`tr` 实用程序读取标准输入，并对每个输入字符将其映射到替代字符、删除该字符或保持该字符不变。此实用程序从标准输入读取并写入标准输出。

### 参数

`tr` 实用程序通常与两个参数 `string1` 和 `string2` 一起使用。两个字符串中每个字符的位置很重要：每当 `tr` 在输入中找到 `string1` 中的字符时，它用 `string2` 中对应的字符替换该字符。

当 `string1` 比 `string2` 长时，`string1` 的初始部分（长度等于 `string2`）用于转换。当 `string1` 比 `string2` 短时，`tr` 重复 `string1` 的最后一个字符以将 `string1` 扩展到 `string2` 的长度。在这种情况下，`tr` 偏离了 POSIX 标准，该标准未定义结果。

您可以使用连字符表示 `string1` 或 `string2` 中的字符范围。以下示例中的两条命令行产生相同的结果：

```
$ echo abcdef | tr 'abcdef' 'xyzabc'
xyzabc
$ echo abcdef | tr 'a-f' 'x-za-c'
xyzabc
```

下一个示例演示了一种常用的文本伪装方法，通常称为 ROT13（旋转 13），因为它将字母表中的第一个字母替换为第十三个，第二个替换为第十四个，等等。第一行以管道符号结尾，隐式地继续该行（参见第 161 页的可选部分），并导致 `bash` 在下一行以次要提示符开始：

```
$ echo The punchline of the joke is ... |
> tr 'A-M N-Z a-m n-z' 'N-Z A-M n-z a-m'
Gur chapuvyr bs gur wxbr vf ...
```

要使文本再次可读，请反转 `tr` 参数的顺序：

```
$ echo Gur chapuvyr bs gur wxbr vf ... |
> tr 'N-Z A-M n-z a-m' 'A-M N-Z a-m n-z'
The punchline of the joke is ...
```

## 选项

- **补集**：`-c`（`--complement`）选项取 `string1` 的补集，使 `tr` 匹配 `string1` 中除这些字符以外的所有字符。

- **删除**：`-d`（`--delete`）选项删除与 `string1` 中指定字符匹配的字符。如果您将此选项与 `-s`（`--squeeze-repeats`）选项一起使用，必须指定 `string1` 和 `string2` 两者。

- **帮助**：`--help` 选项总结了如何使用 `tr`，包括在 `string1` 和 `string2` 中可使用的特殊符号。

当仅使用一个字符串参数调用 `tr` 时，`-s`（`--squeeze-repeats`）选项将 `string1` 中字符的多次连续出现替换为该字符的单次出现。如果您同时使用 `string1` 和 `string2`，`tr` 实用程序首先将 `string1` 中的字符转换为 `string2` 中的字符；然后它会将 `string2` 中字符的多次连续出现替换为该字符的单次出现。

如果您同时使用 `-d`（`--delete`）和 `-s`（`--squeeze-repeats`）选项，`tr` 首先删除 `string1` 中的字符，然后将 `string2` 中字符的多次连续出现替换为该字符的单次出现。

在以下示例中，`tr` 替换字符并将相同的字符对减少为单个字符：

```
$ echo tennessee | tr -s 'tnse' 'srme'
serene
```

下一个示例将文件 `draft1` 中每个非字母字符序列（由字符范围 `A-Za-z` 指定的所有字母字符的补集）替换为单个 `NEWLINE`（换行）字符。输出是单词列表，每行一个。

```
$ tr -c -s 'A-Za-z' '\n' < draft1
```

# unix2dos：将 Linux 文件转换为 Windows 和 Macintosh 格式

如果你想将你在 Linux 系统上创建的文本文件分享给使用 Windows 或 Macintosh OS X 系统的人，你需要转换该文件，以便对方能轻松阅读。`unix2dos` 实用程序可以将 Linux 文本文件转换为由 Windows 机器读取的格式；使用 `unix2mac` 可以将 Linux 文件转换为 Macintosh 系统可读取的格式。这些实用程序是 `dos2unix` 软件包的一部分。输入以下命令可将名为 `memo.txt` 的 Linux 格式文件转换为 Windows 格式文件（使用 `unix2mac` 将其转换为 Macintosh 格式文件）：

```
$ unix2dos memo.txt
```

现在，你可以将文件作为附件通过电子邮件发送给使用 Windows 或 OS X 系统的人。此实用程序会覆盖原始文件。

`dos2unix` 实用程序将 Windows 格式的文件转换为可在 Linux 系统上读取的格式（使用 `mac2unix` 从 Macintosh 格式进行转换）：

```
$ dos2unix memo.txt
```

你还可以使用 `tr`（转换；第 258 页）将 Windows 或 OS X 文本文件更改为 Linux 文本文件。在以下示例中，`-d`（删除）选项使 `tr` 在复制文件时移除回车符（由 `\r` 表示）：

```
$ cat memo | tr -d '\r' > memo.txt
```

大于号（`>`）符号（第 154 页）将 `tr` 的标准输出重定向到名为 `memo.txt` 的文件。如果不使用 `unix2dos` 而反向转换文件则没有这么容易。

# xargs：将标准输入转换为命令行

`xargs` 实用程序是一种方便且高效的方法，可将一个命令的标准输出转换为另一个命令的参数。`xargs` 命令行的格式为

```
xargs [选项] [命令]
```

`xargs` 实用程序从标准输入读取 `command` 的参数，将每个以空白符分隔的字符串解释为独立的参数。然后，它从 `command` 和一系列参数构建命令行。如果添加另一个参数会导致超过最大命令行长度，`xargs` 将执行已构建的命令行。如果还有更多输入，`xargs` 将重复构建命令行并执行它的过程。此过程将持续进行，直到所有输入都被读取。

### 参数

`command` 参数是你希望 `xargs` 用作其构建命令基础的命令行。如果没有参数，`command` 默认为 `echo`。`xargs` 实用程序将从标准输入接收的参数附加到 `command` 之后。如果某些参数需要位于来自标准输入的参数之前，你必须在 `command` 中包含它们。

`xargs` 实用程序常被用作 `find`（第 231 页）的 `-exec` 选项的高效替代方案。如果你使用 `-exec` 选项调用 `find` 来运行命令，它会为处理的每个文件运行一次该命令。每次执行命令都会创建一个新进程，当处理大量文件时，这会消耗系统资源。通过尽可能多地累积参数，`xargs` 可以大大减少所需的进程数量。

若要查找并移除工作目录及其子目录中所有以 `.o` 结尾的文件名，你可以使用 `find -exec` 选项：

```
$ find . -name \*.o -exec rm --force {} \;
```

这种方法会为 `find` 找到的每个 `.o` 文件调用一次 `rm` 实用程序。每次调用 `rm` 都需要一个新进程。如果存在大量 `.o` 文件，系统将花费大量时间来创建、启动并清理这些进程。你可以通过允许 `xargs` 在调用 `rm` 之前尽可能多地累积文件名来减少进程数量：

```
$ find . -name \*.o -print | xargs rm --force
```

在下一个示例中，由 `find` 找到的所有 `.txt` 文件的内容都会被搜索，以查找包含单词 `login` 的行。包含 `login` 的所有文件名称都由 `grep` 显示。

```
$ find . -name \*.txt -print | xargs grep -w -l login
```

## 选项

-   **替换** `-I [marker]` 选项允许你将来自标准输入的参数放置在 `command` 中的任何位置。`command` 中所有出现的 `marker` 都会被 `xargs` 标准输入生成的参数替换。当你使用此选项时，`-I` 选项会被忽略。

下一个示例展示了如何使用 `-I` 选项使 `xargs` 将标准输入嵌入 `command` 中，而不是附加到 `command` 之后。此选项使 `xargs` 在标准输入中每遇到一个 `NEWLINE`（换行）字符时执行一次 `command`。

```
$ cat names
  Tom,
  Dick,
  and Harry

$xargs echo "Hello," < names
Hello, Tom, Dick, and Harry
```

```
$ xargs -I xx echo "Hello xx. Join me for lunch?" < names
Hello Tom,. Join me for lunch?
Hello Dick,. Join me for lunch?
Hello and Harry. Join me for lunch?
```

-   **最大行数** `-l [num]`（小写“el”；`--max-lines=num`）选项每 `num` 行输入执行一次 `command`。当你包含此选项但未指定 `num` 时，`xargs` 将 `num` 设置为 1。

-   **最大参数数** `-n num`（`--max-args=num`）选项每 `num` 个输入行参数执行一次 `command`。下一个示例使用与前面示例相同的输入文件，并包含 `-n` 和 `-l` 选项：

```
$ xargs -n 1 echo "Hi there" < names
Hi there Tom,
Hi there Dick,
Hi there and
Hi there Harry
```

```
$ xargs -l 2 echo "Hi there" < names
Hi there Tom, Dick,
Hi there and
Hi there Harry
```

-   **最大进程数** `-P num`（`--max-procs=num`）选项允许 `xargs` 同时运行最多 `num` 个 `command` 实例。（默认为 1，即顺序执行命令。）如果 `xargs` 在多处理器系统上运行，此选项可能会提高吞吐量。

-   **交互式** `-p`（`--interactive`）选项在每次执行 `command` 之前提示用户确认。

-   **空输入** `-r`（`--no-run-if-empty`）选项导致当标准输入为空时，`xargs` 不执行 `command`。通常，即使标准输入仅包含空格（`SPACES` 和 `TABs`），`xargs` 也至少执行一次 `command`。

# 编辑文件

本节提供了关于两个编辑器的教程：`vim` 和 `nano`。`nano` 编辑器不如 `vim` 功能强大，但学习时间更短，且足够强大，可用于编写简单的程序和笔记。

## 教程：使用 vim 创建和编辑文件

本节解释了如何启动 `vim`，输入文本，移动光标，更正文本，将文件保存到磁盘，以及如何退出 `vim`。教程讨论了 `vim` 的三种操作模式，并解释了如何从一个模式切换到另一个模式。

### vimtutor

除了使用本教程之外，你可能还想尝试 `vim` 的教学程序 `vimtutor`。输入其名称作为命令即可运行它。

### 指定终端

由于 `vim` 利用了特定类型终端的各种特性，你必须告知它你正在使用什么类型的终端或终端模拟器。在许多系统上，通常在你使用终端模拟器时，终端类型会自动设置。如果你需要明确指定终端类型，请参考第 1024 页的“指定终端”。

![](img/243613168ac865b539f12460d966088e_319_0.png)

> **提示** 要运行 `vimtutor` 并获取第 266 页所述的帮助，你必须安装 `vim-enhanced` 软件包。有关安装软件的说明，请参见第 534 页。`vimtutor` 和 `vim` 帮助文件默认不安装。

### 启动 vim

使用以下命令启动 `vim`，以创建和编辑名为 `practice` 的文件（如果你没有安装 `vim-enhanced` 软件包，请使用 `vi` 代替 `vim`）：

```
$ vim practice
```

当你按下 `RETURN`（回车）键时，命令行消失，屏幕看起来与图 7-1 中显示的类似。

> **注意** `vim` 默认不安装：请使用 `vi`
