

## which 与 whereis 的区别

给定一个实用程序名称，**which** 会依次查找您的*搜索路径*（第 359 页）中的目录并定位该实用程序。如果您的搜索路径中包含多个同名实用程序，**which** 仅显示第一个（即*您*将会运行的那个）的名称。

**whereis** 实用程序会查找一个*标准目录*列表，并且独立于您的搜索路径工作。使用 **whereis** 可以定位您指定的程序的二进制文件（可执行文件）、任何手册页以及源代码；**whereis** 会显示它找到的所有文件。

### which、whereis 和内置命令

**which** 和 **whereis** 实用程序仅报告磁盘上现有实用程序的名称；它们不报告 Shell 内置命令（内置于 Shell 中的实用程序；第 170 页）。当您使用 **whereis** 尝试查找 **echo** 命令（它既作为实用程序程序存在，也作为 Shell 内置命令存在）的存储位置时，它会显示以下信息：

```
$ whereis echo
  echo: /usr/bin/echo /usr/share/man/man1/echo.1.gz
        /usr/share/man/man1p/echo.1p.gz
```

**whereis** 实用程序不显示 **echo** 内置命令。甚至 **which** 实用程序报告的信息也是错误的：

```
$ which echo
  /usr/bin/echo
```

在 **bash** 中，您可以使用 **type** 内置命令（第 1041 页）来确定某个命令是否为内置命令：

```
$ type echo
  echo is a shell builtin
```

### locate：搜索文件

**locate** 实用程序（locate 软件包）在本地系统上搜索文件。

```
$ locate logrotate
  /etc/logrotate.conf
  /etc/logrotate.d
  /etc/cron.daily/logrotate
  /etc/logrotate.d/chrony
  /etc/logrotate.d/cups
  ...
```

在使用 **locate** 之前，必须使用 **updatedb** 实用程序构建或更新 **locate** 数据库。通常，数据库每天由一个 **cron** 脚本（第 607 页）更新一次。

### locate 不像 find 那样返回实时结果

由于 **locate** 依赖于 **locate** 数据库，而该数据库通常每天更新一次，因此结果可能不准确。**locate** 实用程序会显示自数据库上次更新以来已被删除的文件名称。同样，它也不会显示自上次更新以来创建的文件名称。要获取准确的实时结果，请使用 **find**（第 229 页）搜索文件名。

**locate** 实用程序在文件的绝对路径名中任意位置搜索您提供的字符串作为参数。因此，命令 **locate sam** 返回所有绝对路径名中包含字符串 **sam** 的文件名称，包括名为 **sample** 的目录层级中的所有文件。如果您希望进行更精细的搜索，请使用 **find**。命令 **find / -name "sam"** 仅返回名为 **sam** 的文件，而 **find / -name "*sam*"** 仅返回简单文件名中包含字符串 **sam** 的文件。

默认情况下，**locate** 搜索普通字符串；使用 **-r** 选项可使其搜索正则表达式。

## script：记录 Shell 会话

**script** 实用程序记录登录会话的一部分，包括您的输入和系统的响应。该实用程序仅适用于字符设备，例如终端或终端模拟器。它可以捕获与 **vim** 相关的会话；但是，由于 **vim** 使用控制字符来定位光标并显示不同的字体（如粗体），输出将难以阅读且可能没有用处。当您 **cat** 一个捕获了 **vim** 会话的文件时，会话内容会迅速从眼前划过。

默认情况下，**script** 将会话捕获到一个名为 **typescript** 的文件中，覆盖同名文件。以下是一个正在被 **script** 记录的会话：

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

使用 **exit** 命令终止 **script** 会话。然后，您可以使用 **cat**、**less**、**more** 或编辑器查看创建的文件。以下是前面 **script** 命令创建的文件内容：

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

如果您将编辑该文件，可以使用 **dos2unix**（第 260 页）消除 **typescript** 文件行尾出现的 ^M（回车）字符。有关更多信息，请参阅 **script man** 页。

### 参数

参数是 `script` 写入的文件的路径名。如果未指定参数，`script` 将写入 `typescript`，如果该文件存在，则会覆盖它。

### 选项

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

## LPI tr：替换指定字符

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

### 选项

- **补集**：`-c`（`--complement`）选项取 *string1* 的补集，使 `tr` 匹配 *string1* 中除这些字符以外的所有字符。
- **删除**：`-d`（`--delete`）选项删除与 *string1* 中指定字符匹配的字符。如果您将此选项与 `-s`（`--squeeze-repeats`）选项一起使用，必须指定 *string1* 和 *string2* 两者。
- **帮助**：`--help` 选项总结了如何使用 `tr`，包括在 *string1* 和 *string2* 中可使用的特殊符号。

当仅使用一个字符串参数调用 `tr` 时，`-s`（`--squeeze-repeats`）选项将 *string1* 中字符的多次连续出现替换为该字符的单次出现。如果您同时使用 *string1* 和 *string2*，`tr` 实用程序首先将 *string1* 中的字符转换为 *string2* 中的字符；然后它会将 *string2* 中字符的多次连续出现替换为该字符的单次出现。

如果您同时使用 `-d`（`--delete`）和 `-s`（`--squeeze-repeats`）选项，`tr` 首先删除 *string1* 中的字符，然后将 *string2* 中字符的多次连续出现替换为该字符的单次出现。

在以下示例中，`tr` 替换字符并将相同的字符对减少为单个字符：

```
$ echo tennessee | tr -s 'tnse' 'srme'
serene
```

下一个示例将文件 `draft1` 中每个非字母字符序列（由字符范围 `A-Za-z` 指定的所有字母字符的补集）替换为单个 NEWLINE（换行）字符。输出是单词列表，每行一个。

```
$ tr -c -s 'A-Za-z' '\n' < draft1
```

