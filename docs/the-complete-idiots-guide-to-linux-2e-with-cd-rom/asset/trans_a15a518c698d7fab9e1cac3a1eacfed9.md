

如果路径的某些部分已经存在，则保留这些部分并将缺失的部分添加到路径中。

## 重点关注：谨防 root 的强大权限！

如果你以 root 身份登录，这条规则适用于你：root 是一个特殊的管理员账户，可授予对整个系统的无限制访问权限。在需要执行系统管理类型任务时，这非常有价值，但这不是你用于其他任何目的的账户。root 账户可以执行某些不可逆的操作，例如擦除磁盘上的所有文件或其他某种灾难性操作。

在你了解更多关于 Linux 和 UNIX 的一般知识之前，我建议你除非绝对必要，否则不要使用 root 账户，例如添加软件或配置某种设备的情况。

如果你没有登录到自己的账户，立即创建一个！有关更多信息，请参阅第 18 章“用户、组和密码”。

## 删除空目录：rmdir

要删除空目录，请使用 rmdir 命令。rmdir 命令是“安全”的，因为它只会在目录为空时才删除目录。其用法如下：

```
[alberto@digital alberto]$ mkdir empty
[alberto@digital alberto]$ rmdir empty
```

## 同时删除文件和目录：rm -R

通常当你想要擦除一个目录时，你也想处理掉它包含的所有文件。在 UNIX 和 Linux 中，此任务使用你之前看到的 rm 命令完成。

要产生这种效果，rm 需要在删除目录之前递归删除找到的文件。虽然这是正确的做法，但要小心：你很容易在意识到发生了什么之前就擦除大量内容。不要忘记，shell 操作非常快。在删除文件时要小心；当你以 root 身份登录时尤其重要，因为一条命令就可能摧毁你的整个文件系统。

要访问内容，请点击章节和节标题。

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## 复制文件：cp

要复制文件，请使用 cp 命令。cp 的语法如下：

```
cp [options] source destination
```

source 是你想要复制的文件名，destination 是你创建的副本的名称。

如果 destination 是一个目录（路径未指定文件名），文件将以其原始名称复制到指定目录中。

options 参数用方括号括起来，表示选项是可选的。我们将在下一节中使用 cp 命令的一个选项。

这里有一个例子：

```
[alberto@digital alberto]$ ls -F
Xrootenv.0  afile  anotherlink  helloworld*
ad ir/  alink@  hello

[alberto@digital alberto]$ cp helloworld /tmp

[alberto@digital alberto]$ ls -F /tmp
fvw mrca00455  helloworld*  install.log  screens/
```

你可以通过在单个命令中列出多个用空格分隔的源文件，将多个文件复制到单个目录中。唯一的要求是最后一个参数（destination）必须是目录。

## 复制目录

复制目录的方式与复制文件非常相似。复制目录时，你需要告诉 cp 你想要递归复制源目录包含的所有文件和目录。这可以通过 -R 选项轻松完成。语法如下：

## 移动文件和目录：mv

要移动文件或目录，你使用 mv 命令。移动文件与复制文件类似。最大的区别是新副本创建后原始文件会被删除。mv 命令遵循以下语法：

```
mv [options] source destination
```

```
[alberto@digital alberto]$ ls
Xrootenv.0  adir/      afile      alink@     anotherlink
    helloworld*
[alberto@digital alberto]$ mv afile file2
[alberto@digital alberto]$ ls
Xrootenv.0  adir/      alink@     anotherlink  file2
    helloworld*
```

mv 命令也可以用于移动整个目录树。

mv 命令提供多个选项。有关更多信息，请参阅其手册页。

> 注意：
> 要阅读 UNIX 工具或命令的文档，请参阅第 15 章“帮助请”。

## 技术谈：符号链接

链接是指向文件系统其他位置的文件或文件夹的指针。链接看起来并像它指向的文件或文件夹一样工作。如果你通过 KFM 查看它，它将具有相同的图标（区别是它旁边会有一个小箭头）。如果你对 ls 命令指定 -F 标志，你会看到一个 at 符号（@）附加在链接文件名的末尾。当你打开一个链接时，你会看到链接指向的文件的相同文件内容。

链接作为组织工具非常有用。它们允许你方便地访问可能存储在文件系统深处（因此具有长而难以输入的文件路径）或甚至在网络不同部分的<|message|>。无需遍历长路径来访问文件，你只需访问一个方便位置的链接即可。

链接也可以用于节省磁盘空间。不要复制大文件以便随时使用，你可以在方便的地方创建指向它们的链接。链接占用非常少的磁盘空间，只有几个字节。

符号链接存储它指向的文件的文件路径。你可以移动和重命名链接而不影响它。然而，如果原始文件——链接指向的文件——被移动、删除或重命名，链接就会断开。断开的链接可以通过将原始文件恢复到其正确位置和名称来修复。否则它们可能应该被删除。符号链接将文件路径与文件关联起来。

## 技术谈：硬链接

还有另一种类型的链接称为硬链接。硬链接与符号（或软）链接类似，因为它为访问文件提供了不同的名称。然而，相似之处到此为止。硬链接有一个优势：与软链接不同，如果你移动、删除或重命名原始文件，软链接会断开，而硬链接不会。

硬链接实际上并不指向文件路径，如软链接那样；相反，它们指向磁盘上存储的实际数据。因此，所有文件至少有一个链接：文件创建时分配给它的名称。当你为文件添加另一个硬链接时，文件系统将其视为文件具有不同的名称，但链接指向的数据与原始文件相同。如果你删除原始文件，剩余的链接仍然指向磁盘上的相同数据。

正如你所见，硬链接与文件写入的实际磁盘存储绑定。因此，硬链接不能跨越磁盘边界。

另一个小的区别是硬链接只引用文件——永远不引用目录。唯一能区分硬链接和文件的方法是使用 ls 的 -i 和 -l 选项，并且 ls 报告硬链接计数大于一并且打印的 inode 地址相同：

```
[alberto@digital alberto]$ ls -il
169688 -rwxrwxr-x  2 alberto  alberto      74 Aug 26 12:19 bye.pl
169972 -rwxrwxrwx  1 alberto  alberto      65 Aug 30 14:49 capture.pl
169688 -rwxrwxr-x  2 alberto  alberto      74 Aug 26 12:19 hello.pl
```

在前面的例子中，hello.pl 和 bye.pl 具有相同的 inode：169688。注意，两者都说它们有两个硬链接。两个文件实际上是同一个文件，只是名称不同！

## Linux 完全傻瓜指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

要访问内容，请点击章节和节标题。

## 创建链接：ln

链接是使用 ln 命令创建的。ln 用于创建软链接和硬链接。命令的语法是

```
ln [options] source destination
```

要创建符号（软）链接，你指定 -s 选项，表示 symbolic。以下是列出目录的示例：

```
[alberto@digital alberto]$ ls -l
total 2
drwxrwxr-x  3 alberto alberto      1024 Aug  1 20:41 adir/
-rw-rw-r--  1 alberto alberto        57 Aug  2 13:12 file
```

以下是创建硬链接的示例：

```
[alberto@digital alberto]$ ln file file2
```

以下是创建软链接的示例：

```
[alberto@digital alberto]$ ln -s file file3
```

以下是再次列出目录的语法。注意 file3 指向 file：

```
[alberto@digital alberto]$ ls -l
total 3
drwxrwxr-x  3 alberto alberto      1024 Aug  1 20:41 adir/
-rw-rw-r--  2 alberto alberto        57 Aug  2 13:12 file
-rw-rw-r--  2 alberto alberto        57 Aug  2 13:12 file2
lrwxrwxrwx  1 alberto alberto         4 Aug  2 13:15 file3 -> file
```

以下是删除原始文件的语法：

```
[alberto@digital alberto]$ rm file
```

