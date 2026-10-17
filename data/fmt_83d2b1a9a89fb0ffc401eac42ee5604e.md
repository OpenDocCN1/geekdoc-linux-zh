
`-squeeze-repeats`（或 `-s`）开关将多个出现的字母减少为每个指定字母的单个字符：

```bash
$ printf "%s\n" "aaabbbccc" | tr -squeeze-repeats 'c'
aaabbbc
```

`tr` 最普遍的用途是将 MS-DOS 文本文件转换为 Unix 文本文件。DOS 文本文件具有回车符和换行符，而 Linux 仅使用换行符标记行尾。需要删除多余的回车符。

```bash
$ tr -d '\r' < dos.txt > linux.txt
```

Apple 文本文件使用回车符而不是换行符。`tr` 也可以通过替换回车符来处理这种情况。

```bash
$ tr '\r' '\n' < apple.txt > linux.txt
```

`tr` 识别的其他转义字符如下：

- `\o` — ASCII 八进制值 o（一到三个八进制数字）
- `\\` — 反斜杠
- `\a` — 可听蜂鸣声
- `\b` — 退格符
- `\f` — 换页符
- `\n` — 换行
- `\r` — 回车
- `\t` — 水平制表符
- `\v` — 垂直制表符

你可以使用接下来讨论的 `sed` 命令执行更复杂的文件编辑。

不受 `sed` 影响的行可以通过 `~quiet`（或 `~n` 或 `~silent`）开关隐藏。

与 `transform` 命令类似，还有其他 `sed` 命令模仿了 Linux 命令。`p`（打印）命令通过打印匹配行来模仿 `grep` 命令。只有在使用了 `~quiet` 开关时，这才有用。`~`（行号）命令会打印匹配行的行号。`q`（退出）命令使 `sed` 表现得像 `head` 命令，显示行直到遇到某一行。

```
$ head orders.txt | sed -quiet '/^$B/p'\
Bunk Bed,705.99,1,757\
Queen Bed,925.99,1,757\
\
$ head orders.txt | sed -quiet '/^$B/d'\
5\
6
```

剩余的 `sed` 命令代表专用操作。控制流由 `n`（下一行）命令处理。文件可以用 `r` 读取或用 `w` 写入。`a`（追加下一行）将两行合并为一行用于匹配目的。`d`（多行删除）删除多行。`p` 是多行打印。`h`、`H`、`g`、`G` 和 `x` 允许你将行保存到临时缓冲区，以便你可以进行修改，显示结果，然后恢复原始文本以进行进一步分析。这就像电子计算器的内存一样工作。复杂的 `sed` 表达式可以在表达式中使用 `b` 命令嵌入分支到标签。`t`（测试）命令充当 `shell if` 或 `switch` 语句，尝试一系列操作直到其中一个成功。子命令可以用花括号嵌入在 `sed` 中。可以使用 `info sed` 找到关于这些命令的更多文档。

长的 `sed` 脚本可以存储在文件中。你可以使用 `~files`（或 `~f`）开关从文件读取 `sed` 脚本。你可以使用 `#` 字符包含注释，就像 `shell` 脚本一样。

`sed` 表达式也可以使用 `~expression`（或 `~e`）开关指定，或者当使用 `~filename` 时从标准输入读取。

你不能在 `sed` 模式中使用 `ASCII` 值转义序列。

## 压缩文件

大多数 Linux 程序区分归档和压缩。`归档` 是将多个文件存储到单个文件中。`压缩` 是通过编码文件来减小文件大小。一般来说，归档文件占用的空间比原始文件多，因此大多数归档文件也被压缩。

Linux 的 `bzip2`（BWH zip）命令使用 Burrows–Wheeler–Huffman 压缩来压缩文件。这是最常用的压缩格式。大多数发行版上都提供了较旧的压缩程序。`gzip`（GNU zip）使用 `LZ77` 压缩进行压缩，并广泛用于较旧的发行版。`compress` 是较旧的 Lempel–Ziv 压缩程序，在大多数版本的 `Unix` 上可用。`zip` 是 DOS `pkzip` 程序的 Linux 版本。`hexbin` 解压某些 Macintosh 归档。

`Linux tar`（`tape archive`）命令是最常用的归档命令，当使用正确的命令行选项时，它在归档时会自动进行压缩。虽然该命令最初用于收集文件以便存储在磁带驱动器上，但它也可以创建磁盘文件。

最初，`tar` 命令不使用命令行开关：使用的是一系列单个字符。Linux 版本支持命令行开关以及旧的单字符语法以向后兼容。

要在文件上使用 `tar`，`--file`（`F`（或 `-f`））开关指示要操作的文件名。必须指定至少一个操作开关以指示 `tar` 将如何处理文件。远程文件可以通过前面的主机名和冒号来指定。

`--create`（`-c`）开关创建一个新的 tar 文件。

```
$ ls -1 orders.txt
-rw-rw-r--  1 kburcht  kburcht     592 May 11 14:45 orders.txt
$ tar --create --file orders.tar orders.txt
$ ls -1 orders.tar
-rw-rw-r--  1 kburcht  kburcht   10240 Oct  3 12:06 orders.tar
```

归档文件明显大于原始文件。要应用压缩，使用 `--bzip`（或 `-I`）、`--gzip`（或 `-z`）、`--compress`（或 `-Z`）或 `--use-compress-program` 来选择压缩类型以指定特定的压缩程序。

```
$ tar --create --file orders.tbz --bzip orders.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     421 Oct  3 12:12 orders.tbz
$ tar --create --file orders.tgz --gzip orders.txt
$ ls -1 orders.tgz
-rw-rw-r--  1 kburcht  kburcht     430 Oct  3 12:11 orders.tgz
```

可以同时归档多个文件。

```
$ tar --create --file orders.tbz --bzip orders.txt orders2.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     502 Oct  3 12:14 orders.tbz
```

新的归档会覆盖现有的归档。

要恢复原始文件，使用 `--extract` 开关。使用 `--verbose` 查看文件名。`tar` 无法自动检测压缩格式；你必须指定正确的压缩开关以避免错误。

```
$ tar --extract --file orders.tbz
tar: 502 garbage bytes ignored at end of archive
tar: Error exit delayed from previous errors
$ tar --extract --bzip --file orders.tbz
$ tar --extract --verbose --bzip --file orders.tbz
orders.txt
orders2.txt
```

`--extract` 开关还会恢复文件路径名中的任何子目录。将文件解压到最初压缩所在的目录很重要，以确保它们被恢复到正确的位置。

`tar` 命令还可以使用 `--concatenate`（或 `-A`）将文件追加到归档中，使用 `--compare`（或 `--diff` 或 `-d`）与归档进行比较，使用 `--delete` 从归档中删除文件，使用 `--list` 列出内容，并使用 `--update` 替换现有文件。除非使用 `--verbose`，否则 `tar` 会静默地执行这些功能。

`tar` 开关的完整列表出现在参考部分。

另一个归档程序 `cpio`（`copy in/out`）提供用于与其他版本的 `Unix` 兼容。`rpm` 包管理器命令基于 `cpio`。

## 参考部分

### `grep` 命令开关

- `--after-context=n`（或 `-A n`）— 打印匹配行后的 `n` 行
- `--before-context=n`（或 `-B n`）— 打印匹配行前的 `n` 行
- `--context[=n]`（或 `-C [n]`）— 显示匹配行周围的 `n` 行（默认为 2）
- `--basic-regexp`（或 `-G`）— 模式不是扩展正则表达式
- `--binary-files=binary`— 正常的二进制文件行为；如果模式在二进制文件的某处存在，则发出消息
- `--binary-files=without-match`（或 `-I`）— `grep` 假设所有二进制文件都不匹配
