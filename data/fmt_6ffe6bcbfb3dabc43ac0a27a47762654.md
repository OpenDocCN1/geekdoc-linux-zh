
© Copyright Macmillan Computer Publishing. 版权所有。

你可以指定多个目录作为参数。例如

```
$ ls /home/usr/local
```

在我的系统上会产生以下输出：

```
/home:
amma ftp httpd ranga vatsa
/usr/local:
X11 bin gimp jikes sbin
ace doc include lib share
atalk etc info man turboboj-1.1.0
```

一个空行分隔每个目录的内容。

### 列出文件

如果你指定的是文件名而不是目录，`ls` 只会列出那一个文件。例如

```
$ ls .profile
.profile
```

你可以将文件和目录混合作为 `ls` 的参数：

```
$ ls .profile docs/ /usr/local /bin/sh
```

这将产生指定文件列表和目录内容的列出列表。

如果你不想列出目录的内容，请为 `ls` 指定 `-d` 选项。这强制 `ls` 只显示目录的名字，而不是它的内容：

```
$ ls -d /home/ranga
/home/ranga
```

你可以将 `-d` 选项与你学过的任何其他 `ls` 选项结合使用。其中的例子是

```
$ ls -aFd /usr/local /home/ranga /bin/sh
/bin/sh*/ /home/ranga/ /usr/local/
```

### 常见错误

如果你指定的文件或目录不存在，`ls` 会报告错误。例如

```
$ ls tomrows_stock_prices.txt
tomrows_stock_prices.txt: No such file or directory
```

如果你指定了多个参数而不是一个，`ls` 只会对那些不存在的文件或目录报告错误。它会正确地列出其他项。

```
$ ls tomorrows_stock_prices.txt /usr/local .profile
```

产生一个错误信息

```
tomrows_stock_prices.txt: No such file or directory
/usr/local:
X11 bin gimp jikes sbin
ace doc include lib share
atalk etc info man turboj-1.1.0
.profile
```

### 《萨姆24 小时自学 Shell 编程》目录索引

第 4 小时：目录操作 上一节 下一节

+   本章章节：

目录树

操作目录

切换目录 总结

列出文件和目录 问题

上一节 下一节

© 版 Macmillan 计算机出版社。保留所有权利。

### 《萨姆24 小时自学 Shell 编程》

第 4 小时：目录操作

本章章节：

+   - 目录树

- 切换目录

- 列出文件和目录

+   - 操作目录

- 总结

- 问题

上一章 下一章

上一节 下一节

### 操作目录

+   - 创建目录

- 复制文件和目录

- 移动文件和目录

- 删除目录

现在你已经学习了目录，让我们来看它们吧。最常见的操作是

+   - 创建目录

- 复制目录

- 移动目录

- 删除目录

### 创建目录

你可以使用 `mkdir` 命令创建目录。它的语法如下：

```
mkdir directory
```

在这里，`directory` 是你想要创建的目录的绝对路径或相对路径。例如该命令

```
$ mkdir local
```

会在当前目录下创建一个名为 `local` 的目录。这里是另一个例子：

```
$ mkdir /tmp/test-dir
```

此命令会在 `/tmp` 目录下创建 `test-dir`。如果 `mkdir` 命令成功创建了请求的目录，它不会产生任何输出。

如果你在命令行中给出多个目录，`mkdir` 会创建每一个目录。例如

```
$ mkdir docs pub
```

会在当前目录下创建 `docs` 和 `pub` 两个目录。

### 创建父目录

有时当你想要创建一个目录时，它的父目录或多个目录可能不存在。在这种情况下，`mkdir` 会发出错误信息。以下是这种情况的说明：

```
$ mkdir /tmp/dir/test1
mkdir: Failed to make directory "tmp/dir": No such file or directory
```

在这种情况下，你可以为 `mkdir` 命令指定 `-p`（父目录）选项。它会创建所有必要的目录。例如

```
$ mkdir -p /tmp/dir/test1
```

会创建所有的父目录。`mkdir` 命令使用以下步骤创建请求的目录：

1. `mkdir` 命令检查是否存在目录 `/tmp`。如果不存在，则创建它。

2. `mkdir` 命令检查是否存在目录 `/tmp/dir`。如果不存在，则创建它。

3. `mkdir` 命令检查是否存在目录 `/tmp/dir/test1`。如果不存在，则创建它。

### 常见错误

使用 `mkdir` 最常见的错误是尝试创建一个已经存在的目录。如果目录 `/tmp/dir` 已经存在，该命令

```
$ mkdir /tmp/dir
```

会生成类似下方的错误信息：

```
mkdir: cannot make directory '/tmp/dir': File exists
```

如果你尝试创建一个与文件同名的目录，也会发生错误。例如，以下命令

```
$ ls -F docs/names.txt
names
$ mkdir docs/names
```

会导致错误信息

```
mkdir: cannot make directory 'docs/names': File exists
```

如果你为 `mkdir` 指定了多个参数，它会尽可能地创建其中这些目录。任何无法创建的目录都会生成一个错误。

### 复制文件和目录

在第 3 章中，你学习了使用 `cp` 命令来复制文件。现在来看如何使用它来复制目录。

要复制目录，请使用 `cp` 的 `-r` 选项。语法如下：

```
cp -r source destination
```

在这里，`source` 是你想复制的目录的路径，`destination` 是你想要放置副本的地方。例如

```
$ cp -r docs/book /mnt/zip
```

会将位于 `docs` 目录下的 `book` 目录复制到 `/mnt/zip` 目录。它会在 `/mnt/zip` 下创建一个 `book` 的新目录。

### 复制多个目录

同样，你可以用 `cp` 复制多个文件，你也可以复制多个目录。当 `cp` 遇到多个源时，所有的目录都会复制到目标地。目标假设是最后一个参数。例如命令

```
$ cp -r docs/book src /mnt/zip
```

会将位于 `docs` 目录下的 `school` 和 `book` 目录复制到 `/mnt/zip`。它会将 `src` 复制到目标目录。在复制完成后，`/mnt/zip` 看起来如下：

```
$ ls -aF /mnt/zip
../book/ src/
```

你也可以在参数列表中混合文件和目录。例如

```
$ cp -r .profile docs/book kshrc dir/names /mnt/jaz
```

会将请求的文件和目录复制到 `/mnt/jaz`。如果你的参数列表仅由文件，`-r` 选项没有影响。

### 常见错误

复制文件和目录最常见的错误是目标位置不对。复制目录最常见的问题涉及到一个不是目录的目标。

这种情况的例子是

```
$ cp -r docs /zip/backup
cp: cannot create directory '/zip/backup': File exists
$ ls -F /zip/backup
backup
```

如你所见，`cp` 操作失败是因为名为 `/zip/backup` 的文件已经存在。

### 移动文件和目录

你已经学习过使用 `mv` 命令重命名文件，但它的真正用途是在目录树中移动文件和目录。基本语法如下：

```
mv source destination
```

在这里，`source` 是你想移动的文件或目录的名字，`destination` 是你希望该文件或目录到达的地方。例如

```
$ mv /home/ranga/names /tmp
```

会将位于 `/home/ranga` 目录下的 `names` 文件移动到 `/tmp`。

移动目录完全相同：

```
$ mv docs/ work/
```

会将 `docs` 目录移动到 `work` 目录。要将 `docs` 目录移回当前目录，可以使用命令：

```
$ mv work/docs .
```

`mv` 的一个很好的功能是你可以在一个命令中移动并重命名文件或目录。例如
