
## 秘密

> 你只能在相同的物理介质上的文件之间创建硬链接。你不能在不同挂载点下的文件之间创建硬链接。在这种情况下，你必须使用软链接。

另一方面，-s 参数可以创建符号链接，也就是软链接：

```
rich@testbox:~$ cp -s test1 test5
rich@testbox:~$ ls -il test*
total 16
1954793 -rw-r--r-- 2 rich rich 6 Sep 1 09:51 test1
1954794 -rw-r--r-- 1 rich rich 0 Sep 1 09:39 test2
1954888 -rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
1954793 -rw-r--r-- 2 rich rich 6 Sep 1 09:51 test4
1954891 lrwxrwxrwx 1 rich rich 5 Sep 1 09:56 test5 -> test1
rich@testbox:~$
```

你会注意到文件列表中几个方面。首先，新的 test5 文件与 test1 文件具有不同的 inode 编号，表明 Ubuntu 将其视为单独的文件。其次，文件大小不同。链接文件只需要存储关于源文件的信息，而不需要存储文件中的实际数据。列表中的文件名区域显示了两者之间的关系。

## 秘密

> 你可以使用 ln 命令而不是 cp 命令来链接文件。默认情况下，ln 命令创建硬链接。如果要创建软链接，仍然需要使用 -s 参数。

> 复制链接文件时要小心。如果你使用 cp 命令复制一个链接到其他源文件的文件，你所做的只是制作源文件的另一个副本。这很快就会变得混乱。与其复制链接文件，不如创建到原始文件的另一个链接。你可以对同一文件创建许多链接，没有任何问题。但是，你不想创建指向其他软链接的软链接。这样做会创建一条链接链，不仅容易混淆，而且很容易断裂，引发各种问题。

## 重命名文件

在 Ubuntu 世界中，重命名文件被称为移动（moving）。你只需将文件从一个名称移动到另一个名称。mv 命令可以将文件和目录移动到另一个位置：

```
rich@testbox:~$ mv test2 test6
rich@testbox:~$ ls -il test*
1954793 -rw-r--r-- 2 rich rich 6 Sep 1 09:51 test1
1954888 -rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
1954793 -rw-r--r-- 2 rich rich 6 Sep 1 09:51 test4
1954891 lrwxrwxrwx 1 rich rich 5 Sep 1 09:56 test5 -> test1
1954794 -rw-r--r-- 1 rich rich 0 Sep 1 09:39 test6
rich@testbox:~$
```

注意，移动文件改变了文件名，但保留了相同的 inode 编号和时间戳值。移动带有软链接的文件会带来问题：

```
rich@testbox:~$ mv test1 test8
rich@testbox:~$ ls -il test*
total 16
1954888 -rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
1954793 -rw-r--r-- 2 rich rich 6 Sep 1 09:51 test4
1954891 lrwxrwxrwx 1 rich rich 5 Sep 1 09:56 test5 -> test1
1954794 -rw-r--r-- 1 rich rich 0 Sep 1 09:39 test6
1954793 -rw-r--r-- 2 rich rich 6 Sep 1 09:51 test8
rich@testbox:~$ 
```

使用硬链接的 test4 文件仍然使用相同的 inode 编号，这完全没问题。然而，test5 文件现在指向一个无效文件，不再是一个有效的链接。

你还可以使用 mv 命令移动目录：

```
mv dir2 dir4
```

目录的全部内容保持不变。唯一改变的是目录的名称。

## 删除文件

在某个时候，你会希望能够删除现有文件。无论是清理文件系统还是移除软件包，总有删除文件的机会。

在 Ubuntu 世界中，删除被称为移除。bash shell 中用于删除文件的命令是 rm。rm 命令的基本形式非常简单：

```
rich@testbox:~$ rm test2
rich@testbox:~$ ls -l
total 16
drwxr-xr-x 2 rich rich 4096 Sep 1 09:42 dir1/
drwxr-xr-x 2 rich rich 4096 Sep 1 09:45 dir2/
-rw-r--r-- 2 rich rich 6 Sep 1 09:51 test1
-rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
-rw-r--r-- 2 rich rich 6 Sep 1 09:51 test4
lrwxrwxrwx 1 rich rich 5 Sep 1 09:56 test5 -> test1
rich@testbox:~$
```

注意，默认情况下，该命令不会提示你确认是否真的要删除文件。你可以使用 -i 参数强制 rm 命令提示你确认删除文件。bash shell 中没有回收站。一旦你删除一个文件，它就永远消失了，所以你最好确定自己在做什么！

现在，这里有一个关于删除带有链接的文件的有趣小知识：

```
rich@testbox:~$ rm -i test1
rm: remove 'test1'? y
rich@testbox:~$ ls -l
```

