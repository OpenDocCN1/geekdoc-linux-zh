
```
$ ls -a -
. .mailrc file2
.. .profile mail
.forward .sh_history mail.instr
.desktop-cis-b12 C-Programs mail.staff.ids
.history f-files manVi
.login file.c status
.signature file.bin
```

### 会话 3.5 列出所有

工作目录 `Working Directory`：目录选项 `-d` 只显示目录本身。如果与长列表配合使用，它显示目录属性。

### 3.6 节 目录列出选项

```
$ ls -ld
drwxr-xr-x 2 gilberg staff 40 May 17
```

### 用户和组 ID `User and Group ID`：用户和组选项 `-n` 显示用户和组 ID，而不是用户名和组名。这与长列表相同，只是显示的是 ID。

### 会话 3.7 用户和组 ID

```
$ ls -ln
drwxr-xr-x 2 0 0 40 May
```

### 反序 `Reverse Order`：反序选项 `-r` 以反向顺序对文件名排序。这会导致以 'z' 开头的文件显示在前。会话 3.8 显示反序下的文件列表。

### 会话 3.8 反序列出

```
$ ls -lr
zFile saturn memo509 file1
```

### 时间排序 `Time Sort`：三种时间排序。它们都应该与长列表配合使用。基础排序 `-lt` 按最新时间排序文件。第二种时间排序是按访问时间 `-lu`。第三种时间排序按创建时间 `-lc`；这基本上是文件的创建日期，尽管其他更改（如权限）也会影响它。会话 3.9 显示基础时间序列。

### 会话 3.9 时间排序

```
$ ls -lt
total 12
-rw-r--r-- 1 gilberg staff 14 May 19 13:33 file1
drwxr-xr-x 2 gilberg staff 512 May 19 13:29 memos
-rw-r--r-- 1 gilberg staff 15 May 18 18:17 zFile
-rw-r--r-- 1 gilberg staff 15 May 18 18:16 aFile.tmp
```

识别目录 `Identify Directories`：我们可以通过文件类型来识别目录，它是每行的第一个字符。在短列表中，无法区分目录和文件。然而，如果我们使用 `p` 选项，它会在末尾添加一个斜杠，如会话 3.10 所示。

### 会话 3.10 列出目录

```
$ ls -lp
./unix.1/
BST.c
BST.h
./unix.1/memos/
src.c
gnuFile
./unix.1/personal/
profile.doc
```

递归列表 `Recursive List`：递归选项 `-R` 不仅显示目录的内容还显示其子目录。列表从当前目录开始。然后列出工作目录下第一个子目录及其子目录。最后列出子目录的内容。每个目录都以路径开头。目录之间有一个空行。在每个目录内部，内容按字母顺序排列。当需要多列时，序列首先按列向下。

### 会话 3.11 递归列表

```
$ ls -Rp
./unix.1/:
BST.c
BST.h
./unix.1/memos/:
src.c
gnuFile
./unix.1/personal/:
profile.doc
```

## 创建目录 `mkdir` 命令

要创建目录，你可以使用创建目录 `mkdir` 命令。它有两个选项：权限模式和父目录。其格式见图 3.17。

> 如果你学习过数据结构，你会识别出这是对目录结构的深度优先遍历。

## 第 3.6 节目录特有的操作 • 87

![](img/6e4cdc423ec40606ea72b32fdafff220_108_0.png)

图 3.17 `mkdir` 命令

你可以使用模式 `-m` 选项控制新目录的权限。如果没有指定模式，目录通常将拥有一个包含对三组用户（所有者、组、其他）的读取和执行权限，而仅对所有者开放权限。在第 3.14 节中，我们为 `saturn` 组文件创建了一个目录，然后使用列目录命令列出其属性。在第 4 节中，你将学习如何使用并更改它们以确保你的文件安全。

## 第 3.14 节 创建目录

```
$ mkdir saturnGp
$ ls -ld saturnGp
drwxr-xr-x 2 gilberg staff 512 May 19 14:03 saturnGp
```

第二个创建目录选项 `-p` 会在目录指定的路径路径创建一个父目录。如果我们为 `saturn` 项目创建一个 `memos` 目录，并在 `memos` 内部创建一个 `schedule` 目录，我们可以使用第 3.15 节中的选项同时创建它们。

## 第 3.15 节 在路径中创建目录

```
$ mkdir -p saturnGp/memos/schedule
$ ls -1R saturnGp
total 1
drwxr-xr-x 3 gilberg staff 512 May 19 14:17 memos

saturnGp/memos:
total 1
drwxr-xr-x 2 gilberg staff 512 May 19 14:17 schedule

saturnGp/memos/schedule:
total 0
```

第 3.15 节分析：让我们更仔细地看看创建目录命令。在执行之前，`saturnGp` 是空的；命令执行后，它包含了一个文件，即 `memos` 目录。在创建 `memos` 目录的同时，我们也创建了它的子目录 `schedule`。验证目录创建的 `list` 命令指定了带有递归的详细列表选项 `-1R`。这允许我们验证目录是否已按预期创建。

## 切换目录 `cd` 命令

现在我们有了多个目录，我们需要某种方法在它们之间移动——也就是说，更改我们的工作目录。切换目录 `cd` 命令正是是此的。其格式如图 3.18 所示。

![](img/6e4cdc423ec40606ea72b32fdafff220_109_0.png)

切换目录命令没有选项。路径可以是相对的，也可以是绝对的；通常是相对的。如果没有路径参数，目标是主目录。也可以通过主目录缩写 `cd ~` 来指定主目录。要从图 3.18 中的主目录移动到 `saturnGp` 目录，我们使用第 3.16 节中的命令。

## 第 3.16 节 切换目录

```
$pwd
~/gilberg
$ cd saturnGp
$ pwd
~/gilberg/saturnGp/memos
```

假设在 `saturnGp` 下方我们创建了 `memos` 目录，并在 `memos` 内部创建了 `schedule` 目录。使用主缩写，我们可以使用第 3.17 节中的命令从账户中的任何地方移动到 `schedule` 目录。

## 第 3.17 节 使用主目录切换目录

```
$ cd ~/saturnGp/memos/schedule
$ pwd
~/gilberg/saturnGp/memos/schedule
```

> 要直接移动到主目录，请使用不带参数的切换目录命令。

## 删除目录 `rmdir` 命令

当目录不再需要时，应该将其删除。删除目录 `rmdir` 命令用于删除目录。其格式如图 3.9 所示。

![](img/6e4cdc423ec40606ea72b32fdafff220_110_0.png)

图 3.19 `rmdir` 命令

除非目录为空，否则 `rmdir` 命令无法删除目录。如果它包含任何文件，UNIX 将返回错误信息“Directory not empty”。3.18 节显示了成功和失败的删除目录。请注意，当命令成功执行时，唯一的响应是 shell 提示符。

## 第 3.18 节 删除目录

```
$ rmdir memos
rmdir: Directory not empty
$ rmdir memo
```

在第 108 页，我们展示了即使目录不为空如何删除目录；然而，优于使用 `rmdir` 命令，因为它不会删除任何内容因此更安全。

## 3.7 普通文件的特有操作

在本节中，我们讨论了普通文件的特有操作：创建文件、编辑文件和打印文件。这些实用工具在图 3.20 中突出显示。

## 创建文件

创建文本文件常用的工具是编辑器，如 `vi`（见第 2 章）。后续章节将讨论如 `cat` 等创建小文件的有用工具。二进制文件是由为特定应用程序（如 C 编译器）编写的程序创建的。

## 编辑文件

UNIX 提供了几个编辑文本文件的实用工具。最常用如 `vi` 这样的编辑器。此外，我们在后续章节中讨论的其他工具，例如 `sed`，它提供了强大的搜索和编辑工具。所有基本工具都可以创建文件，但只有部分可以编辑文件。

## 显示文件 `more` 命令

虽然许多实用工具将其输出写入到标准输出（显示器），但显示文件最有用的工具是 `more`。它允许我们设置输出大小，并在每页结束处暂停以便我们阅读文件。在每一页之后，我们可以请求更多行、新的一页或退出。图 3.21 显示了 `more` 命令。
