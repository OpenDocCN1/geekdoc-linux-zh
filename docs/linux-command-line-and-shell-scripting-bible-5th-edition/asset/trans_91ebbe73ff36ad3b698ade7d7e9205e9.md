
## 重命名文件

在 Linux 世界中，重命名文件被称为*移动文件*。可以使用 `mv` 命令将文件或目录移动到新位置或新名称：

```bash
$ ls -li f*11
1414976 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 fall
1415004 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 fell1
1415005 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 fill1
1415011 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 full1
$
$ mv fall fz11
$
$ ls -li f*11
1415004 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 fell1
1415005 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 fill1
1415011 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 full1
1414976 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 fz11
$
```

请注意，移动文件后，名称从 *fall* 变为了 *fz11*，但其 inode 号和时间戳值保持不变。这是因为 `mv` 只影响文件的名称。

你也可以使用 `mv` 来更改文件的位置：

```bash
$ ls -li /home/christine/fz11
1414976 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 /home/christine/fz11
$
$ ls -li /home/christine/NewDocuments/fz11
ls: cannot access `/home/christine/NewDocuments/fz11': No such file or directory
$
$ mv /home/christine/fall /home/christine/NewDocuments/
$
$ ls -li /home/christine/NewDocuments/fz11
1414976 -rw-rw-r---. 1 christine christine 0 Feb 29 16:12 /home/christine/NewDocuments/fz11
$
$ ls -li /home/christine/fz11
ls: cannot access `/home/christine/fz11': No such file or directory
$
```

前面的例子使用 `mv` 命令将 `fz11` 文件从 `/home/christine` 移动到了 `/home/christine/NewDocuments`。同样，文件的 inode 号或时间戳值没有发生任何变化。

> **提示**
> 与 `cp` 命令一样，你可以在 `mv` 命令上使用 `-i` 选项。这样，在执行覆盖现有文件的尝试之前，系统会先询问你。

唯一的改变是文件的位置。`fz11` 文件不再存在于 `/home/christine` 中，因为没有在原位置留下副本（如果是使用 `cp` 命令的话，会留下副本）。

你可以使用 `mv` 命令在一步操作中既移动文件位置又重命名文件，非常简单：

```bash
$ ls -li NewDocuments/fz11
1414976 -rw-rw-r--. 1 christine christine 0 Feb 29 16:12 NewDocuments/fz11
$
$ mv /home/christine/NewDocuments/fz11 /home/christine/fall
$
$ ls -li /home/christine/fall
1414976 -rw-rw-r--. 1 christine christine 0 Feb 29 16:12 /home/christine/fall
$
$ ls -li /home/christine/NewDocuments/fz11
ls: cannot access '/home/christine/NewDocuments/fz11': No such file or directory
$
```

这个例子将文件 `fz11` 从子目录 `NewDocuments` 移动到了主目录 `/home/christine`，并将其重命名为 `fall`。时间戳值和 inode 号均未改变。只有位置和名称发生了变化。

你还可以使用 `mv` 命令移动整个目录及其内容：

```bash
$ ls NewDocuments
my_file    my_script    really_ridiculously_long_file_name    test_two
my_scrap    my_scrypt    test_one
$
$ mv NewDocuments OldDocuments
$
$ ls NewDocuments
ls: cannot access 'NewDocuments': No such file or directory
$
$ ls OldDocuments
my_file    my_script    really_ridiculously_long_file_name    test_two
my_scrap    my_scrypt    test_one
$
```

目录内的所有内容均未改变。唯一改变的是目录的名称。

一旦你掌握了如何使用 `mv` 命令重命名……呃……移动文件，你就会发现这其实很简单。另一个简单但潜在危险的操作是删除文件。

## 删除文件

你很可能会在某个时候想要删除现有文件。无论是为了清理文件系统还是移除临时工作数据，你总有机会删除文件。

### 第 3 章：基础 Bash Shell 命令

在 Linux 世界中，删除被称为*移除*。在 Bash shell 中移除文件的命令是 `rm`。`rm` 命令的基本形式很简单：

```bash
$ rm -i fall
rm: remove regular empty file 'fall'? y
$ ls fall
ls: cannot access 'fall': No such file or directory
$
```

请注意，`-i` 命令参数会提示你确认是否真的要移除该文件。shell 没有回收站或垃圾桶。一旦移除文件，它就永久消失了。因此，良好的习惯是在 `rm` 命令后始终加上 `-i` 参数。

你也可以使用通配符元字符来删除文件组。然而，再次强调，请使用 `-i` 选项来保护你自己：

```bash
$ rm -i f?ll
rm: remove regular empty file 'fell'? y
rm: remove regular empty file 'fill'? y
rm: remove regular empty file 'full'? y
$ ls ffll
ls: cannot access 'f?ll': No such file or directory
$
```

如果你正在删除大量文件并且不想被提示打扰，`rm` 命令的另一个特性是使用 `-f` 参数强制移除。请务必小心！

### 管理目录

Linux 有一些命令既可以用于文件也可以用于目录（如 `cp` 命令），也有一些仅用于目录的命令。要创建新目录，你需要使用特定命令，本节将对此进行介绍。删除目录可能会变得复杂，因此本节也将涵盖相关内容。

### 创建目录

在 Linux 中创建新目录很简单——只需使用 `mkdir` 命令：

```bash
$ mkdir New_Dir
$ ls -ld New_Dir
drwxrwx-x. 2 christine christine 6 Mar 6 14:40 New_Dir
$
```

系统创建了一个名为 `New_Dir` 的新目录。在新目录的长列表视图中请注意，目录记录以 `d` 开头。这表明 `New_Dir` 是一个目录。

偶尔，你可能需要“批量”创建目录和子目录。要做到这一点，请给 `mkdir` 命令添加 `-p` 选项，如下所示：

```bash
$ mkdir -p New_Dir/SubDir/UnderDir
$ ls -R New_Dir
New_Dir:
SubDir

New_Dir/SubDir:
UnderDir

New_Dir/SubDir/UnderDir:
```

`mkdir` 命令的 `-p` 选项会按需创建任何缺失的*父目录*。父目录是指包含下一级目录树中其他目录的目录。

当然，创建了一些东西之后，你需要知道如何删除它们。如果你把目录创建在了错误的位置，这一点尤其有用。

### 删除目录

删除目录可能会很棘手，原因是有充分的理由。当你开始删除目录时，有很多事情可能会出错。shell 会尽可能保护你免受意外灾难。

删除目录的基本命令是 `rmdir`：

```bash
$ mkdir Wrong_Dir
$ touch Wrong_Dir/newfile
$
$ rmdir Wrong_Dir/
rmdir: failed to remove 'Wrong_Dir/': Directory not empty
$
```

默认情况下，`rmdir` 命令仅适用于删除*空*目录。因为我们在 `Wrong_Dir` 目录中创建了一个文件 `newfile`，所以 `rmdir` 命令拒绝删除它。若要用 `rmdir` 删除此目录，你必须先删除该文件。然后你可以对现在为空的目录使用 `rmdir` 命令：

```bash
$ rm -i Wrong_Dir/newfile
rm: remove regular empty file 'Wrong_Dir/newfile'? y
$ rmdir Wrong_Dir
$ ls Wrong_Dir
ls: cannot access 'Wrong_Dir': No such file or directory
$
```

`rmdir` 没有 `-i` 选项来询问你是否要删除目录。这也是 `rmdir` 仅删除空目录有所帮助的原因之一。

你也可以使用 `rm` 命令删除整个非空目录。使用 `-r` 选项允许命令进入目录，删除文件，然后删除目录本身：

```bash
$ mkdir TestDir
$ touch TestDir/fileone TestDir/filetwo
$ ls TestDir
fileone  filetwo
$ rm -ir TestDir
rm: descend into directory 'TestDir'? y
rm: remove regular empty file 'TestDir/fileone'? y
rm: remove regular empty file 'TestDir/filetwo'? y
rm: remove directory 'TestDir'? y
$ ls TestDir
ls: cannot access 'TestDir': No such file or directory
$
```

这对于进入多个子目录也适用，特别是在你有很多目录和文件要删除时非常有用：

```bash
$ touch New_Dir/testfile
$ ls -FR New_Dir
New_Dir:
SubDir/  testfile

New_Dir/SubDir:
UnderDir/

New_Dir/SubDir/UnderDir:
$
$ rm -iR New_Dir
rm: descend into directory 'New_Dir'? y
rm: descend into directory 'New_Dir/SubDir'? y
rm: remove directory 'New_Dir/SubDir/UnderDir'? y
rm: remove directory 'New_Dir/SubDir'? y
rm: remove regular empty file 'New_Dir/testfile'? y
rm: remove directory 'New_Dir'? y
$
```

虽然这可行，但操作起来有点麻烦。请注意，你仍然必须验证每个被删除的文件。对于一个包含大量文件和子目录的目录，这可能会变得很繁琐。

> **注意**
> 对于 `rm` 命令，`-r` 参数和 `-R` 参数的工作方式完全相同——它们递归遍历目录以删除文件。对于 shell 命令来说，拥有相同功能但大小写不同的参数是不寻常的。

快速删除目录树的终极解决方案是 `rm -rF` 命令。它不会给出任何警告或消息，而是直接删除指定的目录及其所有内容。当然，这是一个极其危险的工具。请谨慎使用，并且务必三思后行，确保你做的正是你本想做的！

在之前的几个小节中，你学习了如何管理文件和目录。到目前为止，本章涵盖了你需要了解的关于文件的一切，除了如何查看其内部内容。
