
```
--rw-r--r-- 1 tclark 0 Jan 27 00:22 umask_example.fil

drwxr-xr-x 8 root 4096 Jan 25 22:16

--rw-r--r-- 1 tclark 0 Jan 13 21:13 example2.xxx

--rw-r--r-- 1 tclark 120 Aug 24 06:44 .ggtkrc

--rw-r--r-- 1 tclark 24 Aug 18 11:23 .bash_logout

--rw-r--r-- 1 tclark 191 Aug 18 11:23 .bash_profile

--rw-r--r-- 1 tclark 124 Aug 18 11:23 .bashrc

--rw------- 1 tclark 237 May 27 2003 .emacs

--rw------- 1 tclark 220 Nov 27 2002 .zshrc

drwxr-xr-x 3 tclark 4096 Aug 12 2002 .kde
```

```
$ cd examples

$ ls -alt

total 20

drwxr-xr-x 2 tclark authors 4096 Feb 3 17:45

--rw-r--r-- 1 tclark 0 Feb 3 17:45 other.txt

--rw-r--r-- 1 tclark authors 360 Feb 3 17:44 preamble.txt

drwxr-xr-x 4 tclark 4096 Feb 3 11:17

--rw-r--r-- 1 tclark authors 2229 Jan 13 21:35 declaration.txt

--rw-r--r-- 1 tclark presidents 1310 Jan 13 17:48 gettysburg.txt
```

现在我们看到 `find` 找到了我们正在寻找的内容。现在我们将进一步完善搜索。

### 查找过去 3 天内修改过的 .txt 文件

有时我们只关注目录中的某些特定文件。例如，你在过去几天里的某某时间写了一个文本文件，但不记得它叫什么名字或者放在了哪里。这里提供了一种“按时间查找”的方法，可以让你无需遍历整个系统就能找到该文本文件：

```
$ find -name '*.txt' -mtime -3

./preamble.txt

./other.txt
```

现在你在上一次搜索中得到的文件更少了，可以轻松地识别出你想要的那个。

### 按大小查找文件

如果用户磁盘空间不足，他们可能想要找到一些大文件并进行压缩以恢复空间。以下命令将从当前目录搜索所有大于 10000KB 的文件。为了节省树结构，输出已被缩略。

### 查找大于 10000k 的文件

```
$ find -size +10000k

./proc/kcore

./var/lib/rpm/Packages

./var/lib/rpm/Filemds

/home/stage/REPCA/wireless/USData.xml

/home/stage/REPCA/wireless/complete.xml

/home/stage/REPCA/wireless/bootstrap.xml

/home/bbcl_9e-btf/BBOUT.OLD
```
同样，在示例中使用 `-+` 可以查找所有小于 10000KB 的文件——在 Linux 系统上，会有很多这样的文件。
`find` 命令非常灵活，接受许多选项。我们在这里只介绍了其中几个，但如果你想查看更多，请参考 `find` 的手册页（man page）。大多数 `find` 选项可以组合起来查找符合多个标准的文件。为了这样做，我们可以继续查找在过去三天内修改过的 `.txt` 文件。

### 使用 find 执行操作

`-exec` 选项赋予 `find` 对找到的文件执行命令的能力。语法有点复杂，但通常通过一个例子就能让你正确使用。在使用 `-exec` 选项之前（特别是配合 `rm` 这种强大的命令时），我建议执行不带 `-exec` 的命令。通过这种方式，你可以看到哪些文件会受到影响。以下是一个实用示例，查找旧三天的 `.txt` 扩展文件并将其删除：

```
$ find -name '*.txt' -mtime -3 -exec rm {} \;

$ ls -lt

total 8

--rw-r--r-- 1 tclark authors 2229 Jan 13 21:35 declaration.txt

--rw-r--r-- 1 tclark presidents 1310 Jan 13 17:48 gettysburg.txt
```

`-exec` 选项允许你在其之后放置任何命令。在这里使用了 `rm`，但通常配合 `cp` 或 `chmod` 使用也非常有用。在命令内部，`{}` 会替换文件名（路径）。最后，`-exec` 选项的结尾由分号 (`;`) 标记。`-exec` 选项应该是 `find` 给出的最后一个选项。`find` 命令对于查找文件和目录非常棒，接下来我们将查看查找其他内容的选项。

### 处理“权限拒绝”

如果你经常使用 `find`（你可能会这样做），有时会遇到没有权限搜索某些目录的问题。这会让 `find` 的有用输出变得困难，因为它们与错误混合在一起：

```
$ find -name '*.txt'

find: /var/lib/dav: Permission denied

find: /var/lib/nfs: Permission denied

find: /var/lib/dhcp: Permission denied

find: /var/lib/slocate: Permission denied

find: /var/lib/php: Permission denied

find: /var/log/samba: Permission denied

find: /var/log/ppt: Permission denied

find: /var/log/audit: Permission denied

find: /var/log/squid: Permission denied
```

为了忽略这些（以及其他）错误并只获取结果，我们可以在命令末尾使用特殊的重定向。重定向将在 Shell 脚本章节中详细介绍，但只需说在该命令中 `2>/dev/null` 是将错误输出重定向到空处。

```
$ find -name '*.txt' 2>/dev/null

/var/www/icons/small/README.txt

/usr/X11R6/lib/X11/rgb.txt

/usr/X11R6/lib/X11/doc/FAQ.txt

/usr/lib/tests/xml/count.txt
```

一直重定向错误输出并不是一个好主意（通常你想知道发生了什么错误），但在这种情况下，`find` 命令可以非常有用。

### 在文本文件中查找字符串

`grep` 命令可以检查文件中是否包含特定字符串。如果 `grep` 找到了字符串，它将在屏幕上打印出该行。这里有一个示例：

```
$ cd /etc

$ grep localhost hosts

127.0.0.1        localhost.localdomain    localhost
```

我们在 `/etc` 目录下的 `hosts` 文件中查找 `localhost` 单词。它找到了，`grep` 打印了找到的行。`grep` 对于搜索输出中的错误或任何具有正则模式的内容都非常有用。

### 查找命令的目录路径

我们执行的命令以文件的形式存在系统的某处。`which` 命令用于查找这些命令的完整路径。以下示例将显示你如何查找某些常用执行文件所在的目录。

### 查找 emacs 和 sort 的目录路径

```
$ which emacs

/usr/bin/emacs

$ which sort

/bin/sort
```

`which` 命令接受任何命令的单一参数。我们在上面展示了 `emacs` 和 `sort` 的 `which` 命令。结果指示了这些命令的二进制文件存在于系统中。

### 查找 emacs 和 sort 的二进制文件、源码和手册页

`whereis` 命令也可以用于定位命令的二进制文件。此外，`whereis` 还能定位源文件和手册页文件。

```
$ whereis emacs

emacs:/usr/bin/emacs /usr/libexec/emacs /usr/share/emacs

/usr/share/man/man1/emacs.1.gz

$ whereis sort

sort: /bin/sort /usr/share/man/man1/sort.1.gz

/usr/share/man/man3pm.gz
```
