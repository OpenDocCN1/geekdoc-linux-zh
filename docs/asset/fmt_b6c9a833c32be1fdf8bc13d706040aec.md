
$ ls

file1 file2 file3

```

注意看 `file3` 的内容现在变成了 `file4`。使用 `-i` 选项可以让你在你准备覆盖现有文件时，`mv` 会向你提示。试一下：

```bash
$ touch file4 file5

$ mv -i file4 file3

mv: overwrite 'file3?' y
```

### 移动文件

使用 `mv` 命令可以将文件从一个目录移动到另一个目录。

创建几个目录用于移动：

```bash
$ cd ~/linux_essentials-2.4/

$ mkdir dir1 dir2

$ ls

dir1 dir2 file1 file2 file3 file5
```

将 `file1` 移动到 `dir1`：

```bash
$ mv file1 dir1

$ ls

dir1 dir2 file2 file3 file5

$ ls dir1

file1
```

注意 `mv` 的最后一个参数是目标目录。每当 `mv` 的最后一个参数是一个目录，文件就会移动到其中。在一个 `mv` 命令中可以指定多个文件：

```bash
$ mv file2 file3 dir2

$ ls

dir1 dir2 file5

$ ls dir2

file2 file3
```

也可以使用 `mv` 来移动和重命名目录。将 `dir1` 重命名为 `dir3`：

```bash
$ ls

dir1 dir2 file5

$ ls dir1

file1

$ mv dir1 dir3

$ ls

dir2 dir3 file5

$ ls dir3

file1
```

# 删除文件和目录

`rm` 命令可以删除文件和目录，而 `rmdir` 命令只能删除目录。让我们通过删除 `file5` 来清理移动过的目录：

```bash
$ cd ~/linux_essentials-2.4/

$ ls

dir2 dir3 file5

$ rmdir file5

rmdir: failed to remove 'file5': Not a directory

$ rm file5

$ ls

dir2 dir3
```

默认情况下，`rmdir` 只能删除空目录，因此我们必须使用 `rm` 来删除普通文件。尝试删除正在删除目录：

```bash
$ cd ~/linux_essentials-2.4/

$ ls

copying creating deleting globs moving

$ rmdir deleting

rmdir: failed to remove 'deleting': Directory not empty

$ ls -d deleting

total 0

drwxr-xr-x. 2 emma Mar 26 14:58 directories

drwxr-xr-x. 2 emma Mar 26 14:58 files
```

默认情况下，`rmdir` 拒绝删除非空目录。使用 `rmdir` 删除 `deleting` 目录下的一个空子目录：

```bash
$ ls -a deleting/files

..

$ rdir deleting/files

$ ls -l deleting

directories
```

删除大量文件或包含许多子目录的深层目录结构似乎很麻烦，但实际上非常简单。默认情况下，`rm` 只作用普通文件。`-r` 选项用于覆盖此行为。小心，`rm -r` 是一个极佳的“自残武器”！当你使用 `-r` 选项时，`rm` 不仅删除任何目录，还会删除该目录内的所有内容，包括子目录及其内容。亲自看看 `rm -r` 是如何工作的：

```bash
$ ls

copying deleting globs moving

$ rm deleting

rm: cannot remove 'deleting': Is a directory

$ ls -l deleting

total 0

drwxwxr-x. 2 emma 6 Mar 26 14:58 directories

$ rm -r deleting

$ ls

copying creating globs moving
```

注意 `deleting` 消失了，尽管它不是空的？像 `mv` 一样，`rm` 有一个 `-i` 选项可以在执行任何操作前进行提示。使用 `rm -ri` 删除移动部分中不再需要的目录：

```bash
$ find

.

./creating

./moving

./moving/dir2

./moving/dir2/file2

./moving/dir2/file3

./moving/dir3

./moving/dir3/file1

./globs

./globs/question1

./globs/question2012

./globs/question23

./globs/question13

./globs/question14

./globs/star10

./globs/star1100

./globs/star2002

./globs/star2013

./globs/question15

./copying

./copying/files

./copying/directories

$ rm -ri moving

rm: descend into directory 'moving?' y

rm: descend into directory 'moving/dir2?' y

rm: remove empty file 'moving/dir2/file2?' y

rm: remove empty file 'moving/dir2/file3?' y

rm: descend into directory 'moving/dir3?' y

rm: remove empty file 'moving/dir3/file1?' y

rm: remove directory 'moving/dir3?' y

rm: remove directory 'moving?' y
```

# 复制文件和目录

`cp` 命令用于复制文件和目录。将几个文件复制到 `copying` 目录：

```bash
$ cd ~/linux_essentials-2.4/copying

$ ls

directories files

$ cp /etc/nswitch.conf files/nswitch.conf

$ cp /etc/issue /etc/hostname files
```

如果最后一个参数是目录，`cp` 会在其中创建一个副本。像 `mv` 一样，可以同时指定多个文件。如果两个操作数存在，`cp` 会覆盖第一个。

```bash
$ cd ~/linux_essentials-2.4/copying

$ ls

directories files

$ cp /etc/nswitch.conf files/nswitch.conf

$ cp /etc/issue /etc/hostname files
```

### Globbing

什么是通配符（Globbing），它是一种简单的匹配语言。命令行 Shell 使用它来引用符合特定模式的文件组。在英语中，这意味着你指定了：

- `*` 匹配任意数量的字符
- `?` 匹配单个字符
- `[]` 匹配字符类

星号 (`*`) 匹配任意数量的任何，因此 Shell 解释 `star*` 为相关上下文中以 `star` 开头的内容。当你运行命令 `ls*` 时，Shell 并不是运行 `ls` 程序并带有参数 `*`，而是查找当前目录中匹配模式 `*` 的文件，并将每个匹配的文件转换为 `ls` 的参数：

```bash
$ ls*
```

对于 `ls` 而言，这等同于

```bash
$ ls star10 star1100 star2002 star2013
```

`*` 字符对 `ls` 没有意义。为了证明这一点，请运行以下命令：

```bash
$ ls \*
ls: cannot access *: No such file
```

当你在字符前面加上反斜杠 `\` 时，你是在指示 Shell 不要解释它。在这种情况下，你希望 `ls` 拥有 `star*` 作为参数，而不是通配符 `star*` 展开的结果。

`?` 展开为任何单个字符。尝试以下命令以亲自验证：

```bash
$ ls

question1 question14 question2012 star10 star2002

question13 question15 question23 star1100 star2013

$ ls question?

question1

$ ls question1?

question13 question14 question15

$ ls question3?

question13 question23

$ ls question3?
```
