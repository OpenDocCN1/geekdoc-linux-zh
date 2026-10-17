
![](img/df365d352a104b50fea29e59a052de4d_968_0.png)

因此，单独使用 `find` 将打印以当前目录为根的整个目录层级结构。

`expression` 包含四种返回 `true` 或 `false` 的术语类型：

* **选项**—影响整体操作，而非特定文件的处理。选项始终返回 `true`。
* **测试**—返回 `true` 或 `false`。
* **操作**—具有副作用，并可以返回 `true` 或 `false`。
* **运算符**—改变测试的结果或将两个测试组合在一起。

通常，表达式从左到右针对每个文件进行评估。一旦任何术语返回 `false`，`find` 就会移动到下一个文件。否则，如果到达表达式的末尾且未执行任何操作，`find` 将调用 `-print` 操作。

### 选项

选项始终生效，而不仅仅是作为 `find` 遍历表达式时的处理内容。为了清晰起见，您应将选项放在表达式的开头。表 A.3 列出并描述了一些重要的选项。

**表 A.3 选项**

| 选项 | 描述 |
| :--- | :--- |
| `-depth` | 在处理目录本身之前先处理目录的内容。这使 `find` 以深度优先的方式遍历层级结构。 |
| `-follow` | 跟踪符号链接。通常，它们不会被跟踪。 |
| `-maxdepth levels` | 在命令行提供的路径下方，最多下降 `levels`（一个非负整数）层目录。 |
| `-mindepth levels` | 在应用任何测试或执行任何操作之前，在命令行提供的路径下方至少下降 `levels`（一个非负整数）层目录。 |
| `-mount` 或 `-xdev` | 不进入位于其他文件系统上的目录。 |

例如，要查找并列出当前目录中（而非任何子目录中）大于 100KB 的所有文件，请使用：

```bash
$ find . -maxdepth 1 -size +100k -ls
```

### 测试

许多测试需要一个数值参数。该参数可以用三种方式指定：

* `+n` 大于 `n`。
* `-n` 小于 `n`。
* `n` 恰好为 `n`。

以下是一些有用的测试：

* `-atime n` 如果文件最后一次访问是在 `n` 天前，则返回 `true`。例如，要查找所有在七天前或更早未被访问的文件，请使用：

  ```bash
  $ find path -atime +6 -print
  ```

  要查找在过去一天内被访问过的文件，请使用：

  ```bash
  $ find path -atime -2 -print
  ```

* `-ctime n` 如果文件的 `status` 在 `n` 天前发生过更改，则返回 `true`。
* `-empty` 如果文件是普通文件或目录且为空，则返回 `true`。
* `-fstype type` 如果包含该文件的文件系统类型为 `type`，则返回 `true`。`type` 的常见值包括用于普通 Linux 文件系统的 `ext2`，用于 `/proc` 伪文件系统的 `proc`，以及用于 CD-ROM 文件系统的 `iso9660`。
* `-gid n` 如果文件的数字组 ID 为 `n`，则返回 `true`。
* `-group gname` 如果文件的组为 `gname`，则返回 `true`。
* `-name pattern` 如果文件的基本名称（去除前导目录）匹配 shell 模式 `pattern`，则返回 `true`。
* `-iname pattern` 类似于 `-name`，但匹配时不区分大小写。
* `-mtime n` 如果文件的内容在 `n` 天前最后被修改，则返回 `true`。
* `-newer otherFile` 如果文件的修改时间比 `otherFile` 更近，则返回 `true`。
* `-perm mode` 如果文件的权限位恰好为 `mode`，则返回 `true`。
* `-perm -mode` 如果 `mode` 中的所有位都已在该文件中设置，则返回 `true`。
* `-perm +mode` 如果 `mode` 中设置的任何一位已在该文件中设置，则返回 `true`。
* `-size n[bcwk]` 如果文件使用了 `n` 个单位的空间，则返回 `true`。一个“单位”是 512 字节，除非 `n` 后面跟着一个字母。在这种情况下，`c` 使单位为一字节，`k` 使单位为 1KB，`b` 使单位为 512 字节，`w` 使单位为 2 字节。
    * 例如，要查找主目录下所有大于 1MB 的文件，请使用：

      ```bash
      $ find $HOME -size +1024k -print
      ```

* `-type x` 如果文件的类型为 `x`，则返回 `true`，其中 `x` 为以下值之一：
    * `b` 块设备
    * `c` 字符设备
    * `d` 目录
    * `f` 普通文件
    * `l` 符号链接
    * `p` 命名管道 (FIFO)
    * `s` 套接字

![](img/df365d352a104b50fea29e59a052de4d_970_0.png)

### 注意

我尚未讨论命名管道或套接字。它们是用于进程间通信 (IPC) 的两种特殊文件类型。

* `-uid n` 如果文件的数字用户 ID 为 `n`，则返回 `true`。
* `-user uname` 如果文件由用户 `uname` 所有，则返回 `true`。

### 操作

表达式中的操作术语可以出现在测试可以出现的任何位置。它可以返回 `true` 或 `false`，但具有副作用。以下是一些有用的操作：

* `-exec command` 执行 `command`。如果命令无错误执行，则返回 `true`。`-exec` 后面的所有参数被视为命令的一部分，直到找到一个由分号组成的参数为止。字符串 `{}` 将被替换为正在处理的文件名。

  **警告**

  必须转义分号，以免其被 shell 解释。

  例如，假设您有一个文本编辑器，它创建名为 `filename.bak` 的备份文件，您想要删除主目录中的所有此类文件。请使用：

  ```bash
  $ find $HOME -name "*.bak" -print -exec rm {} \;
  ```

  让我们剖析这个命令：

  1. 命令开始在主目录 (`$HOME`) 中查找文件。
  2. 它查找名为 `*.bak` 的文件。请注意 shell 模式是如何被引号括起来以防止 shell 对其进行展开的。
  3. 当找到每个匹配的文件时，它会打印该名称。
  4. 它还通过执行命令 `rm filename` 来删除该文件。请注意大括号 `{}` 是如何被文件名替换的。还要注意终止分号是如何用反斜杠转义的。

* `-ok command` 类似于 `-exec`，但在执行命令前会提示确认。
* `-print` 在标准输出上打印文件名，后跟换行符。始终返回 `true`。
* `-prune` 如果未使用 `-depth`，则返回 `true` 且不进入当前目录。如果使用了 `-depth`，则返回 `false`。
* `-ls` 以 `ls -dils` 格式将当前文件列表输出到标准输出。返回 `true`。

### 运算符

最后，你可以使用运算符组合术语和操作的结果：

* `(` `expr` `)` 强制求值的优先级。括号需要被转义。
* `-not expr` 如果 `expr` 为 `false`，则为 `true`。
* `expr1` `-a` `expr2` 如果两个表达式都为 `true`，则为 `true`；如果 `expr1` 为 `false`，则不评估 `expr2`。
* `expr1` `-o` `expr2` 如果任一表达式为 `true`，则为 `true`；如果 `expr1` 为 `true`，则不评估 `expr2`。

还有其他选项、测试、动作和运算符；详见 `find(1)`。现在，让我们来看看其中一些的实际应用。

以下命令查找当前目录下所有文件名以 `.cc` 或 `.h` 结尾且修改时间超过七天的文件，并打印出来：

```bash
$ find . \( -name '*.cc' -o -name '*.h' \) -mtime +7
```

下一个命令将查找整个目录层次结构中开启了 `set-uid` 或 `set-gid` 位的所有文件：

```bash
$ find / -perm +6000 -ls
```

> **注意**
>
> 你应该以 `root` 身份运行上一个示例，因为普通用户无权访问某些文件和目录。

下一个示例执行相同的搜索，但仅针对本地文件。它不会查看 CD、`/proc` 文件系统或远程挂载的卷：

```bash
$ find / \( -not -fstype ext2 -prune \) -o -perm +6000 -ls
```

注意表达式的第一部分是如何用括号分组的。如果文件系统类型不是 `ext2`，你就“剪枝”（prune）搜索。这使得 `find` 不进入该目录。否则（使用 `-o` 运算符），你执行权限测试，如果测试通过，则列出文件名。

`find` 是系统管理员的好朋友；请研究 `find(1)` 并查找 Shell 脚本和其他书籍中关于 `find` 的其他示例。你可以使用 `find` 命令完成许多例行的系统管理任务。

### 创建链接：ln

你在第 2 章中已经见过 `ln` 命令的实际应用。在那一章中，你总是使用 `-s` 选项来创建符号链接。以下是对如何使用 `ln -s` 的回顾：

* `ln -s path linkName` 创建一个名为 `linkName` 的符号链接，指向文件或目录 `path`。如果 `path` 是相对路径名，则相对于包含 `linkName` 的目录进行解释。如果 `linkName` 已经存在，命令将失败。如果你提供了 `-f` 选项，则如果 `linkName` 存在，会被覆盖。`-i` 选项使 `ln` 询问是否应该覆盖现有文件。
* `ln -s path1 path2... dirName` 在（已存在的）目录 `dirName` 内部创建名为 `path1`、`path2...` 等的符号链接。

还有其他几个选项控制 `ln -s` 的行为。详见 `ln(1)`。请注意，如果你使用 `rm` 删除符号链接，被删除的是链接本身，而不是它所指向的文件。

#### 硬链接

Linux 支持另一种称为硬链接的链接类型。要了解硬链接的工作原理，你需要了解一点关于 Linux 文件系统内部结构的背景知识。

在 Linux（以及 UNIX）中，磁盘上称为 `inode` 的特殊块包含关于文件内容的所有信息。也就是说，`inode` 记录文件的修改日期和时间、文件大小，以及文件系统查找文件内容所需的所有簿记信息。每个文件系统上的 `inode` 都有编号。通过指定其所在的文件系统和其 `inode` 编号，可以唯一标识一个 `inode`。

目录项仅存储两项信息：文件名和 `inode` 编号。两个不同的目录项包含相同的 `inode` 编号是完全可能的。每个条目被称为该文件的一个硬链接。`inode` 记录指向它的硬链接数量，并且只有在最后一个链接被移除时，文件内容才会实际被移除。

> **注意**
>
> 即使如此，如果某个进程打开了该文件，UNIX 也可能推迟删除文件内容。

让我们看一个硬链接的例子。输入以下命令：

```bash
$ echo This is a test > file
$ ln file hlink
$ ls -l file hlink
-rw-rw-r-- 2 dfs dfs 15 Jun 28 09:34 file
-rw-rw-r-- 2 dfs dfs 15 Jun 28 09:34 hlink
```

现在，向 `file` 追加一些信息：

```bash
$ echo More stuff >> file
$ ls -l file hlink
-rw-rw-r-- 2 dfs dfs 26 Jun 28 09:36 file
-rw-rw-r-- 2 dfs dfs 26 Jun 28 09:36 hlink
```

注意 `file` 和 `hlink` 都变大了，且它们的修改时间也发生了变化。这是因为它们指向同一个文件的链接。如果你使用 `rm` 删除 `file`，内容不会受到影响。如果你随后删除 `hlink`，内容将被移除。

你可以使用 `ls -i` 查看文件的 `inode` 编号：

```bash
$ ls -li file hlink
45145 file 45145 hlink
```

注意两个文件具有相同的 `inode` 编号。

你很少需要创建硬链接，但了解它们的工作原理是有用的。例如，`mv` 等程序通过创建一个新的硬链接并删除现有的硬链接（在可能的情况下）来重命名文件。一些 UNIX 手册页提到链接和 `inode`，理解它们会让生活更轻松。

### 检查文件

在大多数情况下，`cat`、`more` 和 `less` 足以让你查看文件。然而，有时其他几个命令也很有用。

#### 识别文件：file

`file` 命令会对文件的内容进行有根据的猜测。它查看文件名、文件的前几百个字节以及文件权限，并试图推断文件中包含什么。

```bash
$ file /usr/bin/locate
/usr/bin/locate: ELF 32-bit LSB executable, Intel 80386, version 1,[Ssr]
→ dynamically linked (uses shared libs), stripped
```

这告诉你 `/usr/bin/locate` 是一个 ELF 32 位 LSB 可执行文件。这是一种冗长的说法，意思是它是一个可执行程序。它运行在 Intel 80386 系列处理器上，并遵循 ELF 标准的第 1 版。

#### 背景资料

ELF（可执行与可链接格式，Executable and Link Format）是一种用于可执行文件的文件格式。它在 UNIX 世界中被广泛使用。

你还发现 `/usr/bin/locate` 是动态链接的，并且不包含符号表或调试信息——它是经过剥离（stripped）的。

以下是另一个示例：

```bash
$ file /opt/kde/share/wallpapers/parrots.jpg
/opt/kde/share/wallpapers/parrots.jpg: JPEG image data, JFIF standard
```

`file` 对大多数文件类型的猜测相当准确。如果它无法识别文件类型，它只会打印 ASCII 文本或数据。

`file` 为某些类型的文件内置了算法，但它也使用两个文件作为用户提供的提示。`/usr/share/misc/magic` 和 `/etc/magic` 包含 `file` 可用于识别文件的特殊格式的提示。你可以通过阅读手册页 `file(1)` 和 `magic(5)` 来了解它们是如何工作的。

#### 查看文件的一部分：head 和 tail

`head` 和 `tail` 是非常简单的命令。它们将文件的前几行或后几行发送到标准输出。以下解释了如何使用它们：

* `head -n file` 将 `file` 的前 `n` 行发送到标准输出。如果省略 `-n`，则输出 10 行。如果省略 `file`，`head` 将标准输入的前 `n` 行发送到标准输出。
* `tail -n file` 将 `file` 的最后 `n` 行发送到标准输出。如果省略 `-n`，则输出 10 行。如果省略 `file`，则使用标准输入。
* `tail +n file` 从第 `n` 行开始将 `file` 的最后一行发送到标准输出。例如，要查看除第一行外的所有内容，请使用：

  ```bash
  $ tail +2 file
  ```

* `tail -f file` 使 `tail` 永远循环，等待文件变大。如果文件变大，新增的行会被发送到标准输出。如果你有一个进程正在写入文件并希望监控文件的进度，这非常有用。

`head` 和 `tail` 都可以接受多个 `file` 参数；在这种情况下，它们会在文件内容之前打印一行标题，以标识正在查看的是哪个文件。

GNU `head` 和 `tail` 拥有更多的选项。这些选项在 `head(1)` 和 `tail(1)` 的手册页中记录得很简略，但在 `head` 和 `tail` 的信息页中记录得很详细。

#### 比较文件：cmp 和 diff

`cmp` 命令用于查看两个（可能是二进制的）文件是否不同。最简单的调用方式如下：

```bash
$ cmp file1 file2
```

如果文件不同，`cmp` 会打印 `file1 file2 differ: char n, line m` 并以状态 1 退出；否则，它不打印任何内容，并以状态 0 退出。

如果使用 `-l` 选项，`cmp` 将打印所有不同字节的偏移量和字节值。`-i n` 选项使 `cmp` 在报告差异时忽略每个文件的前 `n` 个字节。

不幸的是，在 Caldera OpenLinux 上，`cmp` 既没有手册页也没有信息页。输入 `cmp --help` 可获取使用 `cmp` 的简要说明。

`diff` 命令主要用于比较文本文件。`diff` 有很多选项和运行模式。考虑以下两个文件：

| file1 | file2 |
| :--- | :--- |
| Here is some text. | Here is some text. Ouch. |
| Here is a line. | Here is a line. |
| Here is another line. | Yet another line. |
| Yet another line. | foo bar. |

以下是 `diff` 的输出：

```bash
$ diff file1 file2
1c1
< Here is some text.
---
> Here is some text. Ouch.
3c2
< Here is another line.
4d4
> foo bar.
```

前四行表明有一行被更改了（`1c1`）。被更改的原始行前面带有 `<`。接下来是一行三个破折号，然后是前面带有 `>` 的新行。

`3d2` 表示应删除原始文件的第 3 行。被删除的行前面带有 `<`。

`4a4` 表示应在第 4 行之后添加一行，新行前面带有 `>`。
