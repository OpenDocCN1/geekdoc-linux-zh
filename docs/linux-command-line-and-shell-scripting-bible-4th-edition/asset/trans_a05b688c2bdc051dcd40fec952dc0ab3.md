

此功能允许你查看哪些内容需要键入，才能使制表符补全正常工作。

## 链接文件

在 Linux 文件系统中，链接文件是一个非常有用的选项。如果你需要在系统中维护同一文件的两个（或更多）副本，除了拥有独立的物理副本外，你还可以使用一个物理副本和多个虚拟副本，这些虚拟副本称为链接。链接是目录中的一个占位符，指向文件的真实位置。Linux 中可用的文件链接类型有两种：

- 符号链接
- 硬链接

符号链接，也称为软链接，只是一个物理文件，它指向虚拟目录结构中某处的另一个文件。两个通过符号链接关联的文件并不共享相同的内容。

要创建符号链接，原始文件必须已经存在。然后，我们使用带有 `-s` 选项的 `ln` 命令来创建符号链接：

```bash
$ ls -l test_file
-rw-rw-r--. 1 christine christine 74 Feb 29 15:50 test_file
$
$ ln -s test_file slink_test_file
$
$ ls -l *test_file
lrwxrwxrwx. 1 christine christine 9 Mar 4 09:46 slink_test_file -> test_file
-rw-rw-r--. 1 christine christine 74 Feb 29 15:50 test_file
$
```

在上面的示例中，请注意符号链接的名称 `slink_test_file` 在 `ln` 命令中列为第二个。在符号链接文件的长列表（`ls -l`）中，文件名后显示的 `->` 符号表明它符号链接到了文件 `test_file`。

另外，请注意符号链接的文件大小与数据文件的文件大小。符号链接 `slink_test_file` 仅占 9 字节，而 `test_file` 占 74 字节。这是因为 `slink_test_file` 只是指向 `test_file`。它们不共享内容，并且是两个物理上独立的文件。

判断这些链接文件是独立物理文件的另一种方法是查看它们的 inode 号。文件或目录的 inode 号是内核分配给文件系统中每个对象的唯一标识号。要查看文件或目录的 inode 号，请在 `ls` 命令中添加 `-i` 参数：

```bash
$ ls -i *test_file
1415020 slink_test_file 1415523 test_file
$
```

示例显示 `test_file` 的 inode 号是 1415523，而 `slink_test_file` 的 inode 号不同（它是 1415020）。因此，它们是不同的文件。

硬链接创建了一个独立的虚拟文件，其中包含有关原始文件及其位置的信息。然而，这两个文件实际上是同一个物理文件。要创建硬链接，同样，原始文件必须预先存在，只是这次 `ln` 命令不需要参数：

```bash
$ ls -l *test_one
-rw-rw-r---. 1 christine christine 0 Feb 29 17:26 test_one
$
$ ln test_one hlink_test_one
$
$ ls -li *test_one
1415016 -rw-rw-r---. 2 christine christine 0 Feb 29 17:26 hlink_test_one
1415016 -rw-rw-r---. 2 christine christine 0 Feb 29 17:26 test_one
$
```

在上面的示例中，创建硬链接文件后，我们使用了 `ls -li` 命令来显示 `*test_one` 的 inode 号和长列表。请注意，这两个通过硬链接关联的文件共享相同的 inode 号。这是因为它们在物理上是同一个文件。它们的文件大小也完全相同。

**注意**

> 你只能在同一物理介质上的文件之间创建硬链接。要在不同物理介质上的文件之间创建链接，必须使用符号链接。

你可能会发现符号链接和硬链接的概念比较难理解。幸运的是，重命名文件（下一节的主题）要容易理解得多。

## 重命名文件

在 Linux 世界中，重命名文件被称为*移动文件*。可以使用 `mv` 命令将文件和目录移动到另一个位置或新名称：

```bash
$ ls -li f?ll
   1414976 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fall
   1415004 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fell
   1415005 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fill
   1415011 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 full
   $
   $ mv fall fzll
   $
   $ ls -li f?ll
   1415004 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fell
   1415005 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fill
   1415011 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 full
   1414976 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fzll
   $
```

请注意，移动文件时将名称从 `fall` 更改为 `fzll`，但保留了相同的 inode 号和时间戳值。这是因为 `mv` 仅影响文件的名称。

你还可以使用 `mv` 来更改文件的位置：

```bash
$ ls -li /home/christine/fzll
   1414976 -rw-rw-r--. 1 christine christine   0 Feb 29 16:12
   /home/christine/fzll
   $
   $ ls -li /home/christine/NewDocuments/fzll
   ls: cannot access '/home/christine/NewDocuments/fzll': No such file or directory
   $
   $ mv /home/christine/fzll /home/christine/NewDocuments/
$
$ ls -li /home/christine/NewDocuments/fzll
1414976 -rw-rw-r--. 1 christine christine 0 Feb 29 16:12
/home/christine/NewDocuments/fzll
$
$ ls -li /home/christine/fzll
ls: cannot access '/home/christine/fzll': No such file or directory
$
```

在上面的示例中，我们使用 `mv` 命令将文件 `fzll` 从 `/home/christine` 移动到了 `/home/christine/NewDocuments`。同样，文件的 inode 号或时间戳值没有变化。

**提示**

> 与 `cp` 命令类似，你可以在 `mv` 命令上使用 `-i` 选项。因此，在命令尝试覆盖任何现有文件之前，系统会询问你。

唯一的改变是文件的位置。`fzll` 文件不再存在于 `/home/christine` 中，因为没有在原始位置留下它的副本，这与 `cp` 命令的行为不同。

你可以使用 `mv` 命令在一个简单的步骤中同时移动文件位置并重命名它：

```bash
$ ls -li NewDocuments/fzll
1414976 -rw-rw-r--. 1 christine christine 0 Feb 29 16:12
NewDocuments/fzll
$
$ mv /home/christine/NewDocuments/fzll /home/christine/fall
$
$ ls -li /home/christine/fall
1414976 -rw-rw-r--. 1 christine christine 0 Feb 29 16:12
/home/christine/fall
$
$ ls -li /home/christine/NewDocuments/fzll
ls: cannot access '/home/christine/NewDocuments/fzll': No such file or directory
$
```

对于这个示例，我们将文件 `fall`（原为 `fzll`）从子目录 `NewDocuments` 移动到了主目录 `/home/christine`，并将其重命名为 `fall`。时间戳值和 inode 号均未改变。只有位置和名称发生了变化。

你还可以使用 `mv` 命令移动整个目录及其内容：

```bash
$ ls NewDocuments
my_file     my_script   really_ridiculously_long_file_name
test_two
my_scrap    my_scrapt   test_one
$
$ mv NewDocuments OldDocuments
$ ls NewDocuments
ls: cannot access 'NewDocuments': No such file or directory
$
$ ls OldDocuments
my_file     my_script   really_ridiculously_long_file_name
test_two
my_scrap    my_scrapt   test_one
$
```

目录的完整内容保持不变。唯一改变的是目录的名称。

一旦你知道如何使用 `mv` 命令重命名……呃……*移动* 文件，你就会意识到完成这一点是多么简单。另一个简单但潜在危险的任务是删除文件。

## 删除文件

很可能在某个时候你需要删除现有文件。无论是为了清理文件系统还是移除临时工作数据，你总是有机会删除文件。

在 Linux 世界中，删除被称为*移除*。在 Bash shell 中移除文件的命令是 `rm`。`rm` 命令的基本形式很简单：

```bash
$ rm -i fall
rm: remove regular empty file 'fall'? y
$ ls fall
ls: cannot access 'fall': No such file or directory
$
```

请注意，`-i` 命令参数会提示你确认是否真的要移除该文件。Shell 没有回收站或垃圾桶。移除文件后，它将永久消失。因此，一个好习惯是始终在 `rm` 命令后加上 `-i` 参数。你还可以使用通配符元字符来删除一组文件。不过，同样，请使用 `-i` 选项来保护自己：

```bash
$ rm -i f?ll
rm: remove regular empty file 'fell'? y
rm: remove regular empty file 'fill'? y
rm: remove regular empty file 'full'? y
$ ls f?ll
ls: cannot access 'f?ll': No such file or directory
$
```

`rm` 命令的另一个特性是，如果你要删除大量文件且不想被提示打扰，可以使用 `-f` 参数强制移除。请务必小心！

# 管理目录

Linux 有一些命令适用于文件和目录（如 `cp` 命令），也有一些仅适用于目录的命令。要创建新目录，你需要使用一个特定的命令，这将在本节中介绍。移除目录可能会变得有趣，因此本节也将涵盖这一点。

## 创建目录

在 Linux 中创建新目录很容易——只需使用 `mkdir` 命令：

```bash
$ mkdir New_Dir
$ ls -ld New_Dir
drwxrwxr-x. 2 christine christine 6 Mar 6 14:40 New_Dir
$
```

系统创建了一个名为 `New_Dir` 的新目录。在新目录的长列表中，请注意目录的记录以 `d` 开头。这表明 `New_Dir` 是一个目录。

