

total 12
drwxr-xr-x 2 rich rich 4096 Sep 1 09:42 dir1/
drwxr-xr-x 2 rich rich 4096 Sep 1 09:45 dir2/
-rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
-rw-r--r-- 1 rich rich 6 Sep 1 09:51 test4
lrwxrwxrwx 1 rich rich 5 Sep 1 09:56 test5 -> test1
rich@testbox:~$ cat test4
hello
rich@testbox:~$ cat test5
cat: test5: No such file or directory
rich@testbox:~$

我删除了 test1 文件，该文件与 test4 文件有硬链接，与 test5 文件有软链接。注意发生了什么。两个链接文件仍然存在，即使 test1 文件现在已经消失了（尽管在我的彩色终端窗口中 test5 文件名现在显示为红色）。当我查看 test4 文件的内容时，它是硬链接，仍然显示文件的内容。当我查看 test5 文件的内容时，它是软链接，bash 提示它不再存在。

请记住，硬链接文件使用与原始文件相同的 inode 编号。硬链接文件在你删除最后一个链接文件之前会保持该 inode 编号，从而保留数据。软链接所知道的只是底层文件现在已经消失，所以它无处可指。在处理链接文件时，记住这一重要特性。

如果你要删除大量文件并且不想被确认提示打扰，请使用 -f 参数强制删除。只要小心一点！

> 与复制文件一样，你也可以使用通配符与 rm 命令。再次提醒，在这样做时要谨慎，因为你删除的任何东西，即使是意外删除，也永远消失了！

## 目录处理

在 Ubuntu 中，有一些命令同时适用于文件和目录（例如 cp 命令），也有一些命令仅适用于目录。要创建新目录，你需要使用特定命令，我们将在本节中讨论。删除目录可能会变得有趣，所以我们也会对此进行研究。

## 创建目录

在 Ubuntu 中创建新目录并没有什么复杂之处。只需使用 mkdir 命令：

```
rich@testbox:~$ mkdir dir3
rich@testbox:~$ ls -il
total 16
```

```
1954886 drwxr-xr-x 2 rich rich 4096 Sep 1 09:42 dir1/
1954889 drwxr-xr-x 2 rich rich 4096 Sep 1 10:55 dir2/
1954893 drwxr-xr-x 2 rich rich 4096 Sep 1 11:01 dir3/
1954888 -rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
1954793 -rw-r--r-- 1 rich rich 6 Sep 1 09:51 test4
rich@testbox:$
```

系统创建了一个新目录（在此示例中为 dir3）并为其分配了新的 inode 编号。

## 删除目录

删除目录可能很棘手，但这是有原因的。当你开始删除目录时，很容易出错，但 bash shell 尽可能地保护你免受意外灾难。删除目录的基本命令是 rmdir：

```
rich@testbox:$ rmdir dir3
rich@testbox:$ rmdir dir1
rmdir: failed to remove 'dir1': Directory not empty
rich@testbox:$
```

默认情况下，rmdir 命令仅用于删除空目录。因为 dir1 目录中有一个文件，所以 rmdir 命令拒绝删除它。你可以使用 --ignore-fail-on-non-empty 参数删除非空目录。

我们的朋友 rm 命令也可以帮助处理目录。如果你尝试在不带参数的情况下使用它，就像处理文件一样，你会感到失望：

```
rich@testbox:$ rm dir1
rm: cannot remove 'dir1': Is a directory
rich@testbox:$
```

然而，如果你真的想删除一个目录，可以使用 -r 参数递归删除目录中的文件，然后删除目录本身：

```
rich@testbox:$ rm -r -i dir2
rm: descend into directory 'dir2'? y
rm: remove 'dir2/test1'? y
rm: remove 'dir2/test3'? y
rm: remove 'dir2/test4'? y
rm: remove directory 'dir2'? y
rich@testbox:$
```

尽管此命令有效，但有点笨拙。最终的解决方案是抛开谨慎，删除整个目录及其内容，使用同时带 -r 和 -f 参数的 rm 命令：

```
rich@testbox:$ rm -r -f dir2
rich@testbox:$
```

就这样。没有警告，没有喧哗——只是另一个 shell 提示。当然，这是一个极其危险的工具，特别是如果你以 root 用户账户登录时。要谨慎使用，并且只有在三重检查确保你确实想这样做之后才使用。

