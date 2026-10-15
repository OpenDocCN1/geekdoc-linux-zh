
用户 **john** 的主目录中的目录并具有原始文件的文件名。用户 **john** 必须首先在其主目录中创建 **unixbook** 目录，并在其 **unixbook** 目录中创建 **examples** 目录。您必须对 **john** 的 **unixbook** 目录具有执行权限，并且对其 **examples** 目录具有执行和写入权限，才能使命令成功运行并完成任务。

```
$ ln -f ~/unixbook/examples/* /home/john/unixbook/examples
$
```

## 8.6.2 硬链接的缺点

硬链接是传统上用于粘合 UNIX 文件系统结构的方式，UNIX 文件系统结构通常包含多个文件系统。然而，硬链接存在一些问题和限制，使其对普通用户来说吸引力降低。

第一个问题是，硬链接不能在位于不同文件系统的文件之间建立。如果您在自己的目录结构之间建立链接，以主目录作为顶层目录，或者在与您相同的文件系统上的另一用户目录结构中的文件之间建立链接，则此限制不是问题。但是，如果您想在 /bin 目录中的文件（命令）和您自己的文件结构中的文件之间创建硬链接，它很可能不会成功，因为在几乎所有系统上，/bin 目录和您的目录结构都位于不同的文件系统上。下面的命令说明了这一点。在此示例中，我们尝试将名称 del 赋予位于 /bin 目录中的 UNIX 命令 rm。由于 rm 命令位于一个文件系统（我们的系统上的 /）中，而我们的目录结构位于另一个文件系统（我们的系统上的 /usr/home）中，因此 UNIX 不允许我们在当前目录中的文件和 /bin/rm 之间创建硬链接 del。

```
$ ln /bin/rm del
ln: del: Cross-device link
$
```

当具有多个链接的文件被移动到另一个文件系统时，此问题也会出现。下面的会话说明了这一点。`ls -il` 命令显示 Chapter3 和 Chapter3.hard 是指向同一文件的硬链接（请注意相同的 inode 号）。`mv` 命令用于将文件 Chapter3 移动到 /tmp 目录，而 /tmp 目录与当前包含 Chapter3（和 Chapter3.hard）的目录是不同的文件系统。请注意，在执行 `mv` 命令后，Chapter3.hard 和 /tmp/Chapter3 的链接计数各为 1，并且文件具有不同的 inode；/tmp/Chapter3 的 inode 为 472，而 Chapter3.hard 仍为旧的 inode 52473。请注意，尽管 set 命令失败，但 `mv` 命令是成功的。`ln` 命令无法将 /tmp/Chapter3 链接到 temp.hard，因为这两个文件位于不同的文件系统。

```
$ ls -il
total 2
```
```
13059 -rw-r--r-- 1 sarwar faculty 398 Mar 11 14:20 Chapter1
17488 -rw-r--r-- 1 sarwar faculty 5983 Jan 17 11:57 Chapter2
52473 -rw-r--r-- 2 sarwar faculty 9352 May 28 23:09 Chapter3
52473 -rw-r--r-- 2 sarwar faculty 9352 May 28 23:09 Chapter3.hard
$ mv Chapter3 /tmp/Chapter3
mv: /tmp/Chapter3: set owner/group (was: 1004/1008): Operation not permitted
$ ls -il
total 2
13059 -rw-r--r-- 1 sarwar faculty 398 Mar 11 14:20 Chapter1
17488 -rw-r--r-- 1 sarwar faculty 5983 Jan 17 11:57 Chapter2
52473 -rw-r--r-- 2 sarwar faculty 9352 May 28 23:09 Chapter3.hard
$ ls -il /tmp/Chapter3
472 -rw-r--r-- 1 sarwar root 9352 Aug 23 10:03 /tmp/Chapter3
$ ln /tmp/f3 temp.hard
ln: temp.hard: Cross-device link
$
```

第二个问题是，只有超级用户才能创建目录的硬链接。当非超级用户尝试创建目录 **myweb** 的硬链接时，`ln` 命令会给出错误消息，如

```
$ ln ~/myweb myweb.hard
ln: /home/sarwar/myweb: Is a directory
$
```

第三个问题是，一些编辑器会删除您正在编辑的文件的现有版本，并将新版本放在新文件中。这样一来，对已删除文件的任何硬链接都无法访问新文件，从而违背了链接（文件共享）的目的。幸运的是，常用的编辑器都没有这样做。因此，[第 3 章](#) 中讨论的文本编辑器（vim 和 emacs）是安全的。

在下面的章节练习中，您将使用 `ln` 和 `ls -il` 命令来创建和识别硬链接，并验证硬链接的一个严重限制。

### EXERCISE 8.1

在您的主目录中创建一个包含此问题的 **Ch8Ex1** 文件。为此文件建立一个硬链接，也在您的主目录中，并将链接命名为 **Ch8Ex1.hard**。使用 `ls -il` 命令验证链接是否已建立。您在该命令的输出中使用了哪个字段进行验证？

### EXERCISE 8.2

在您的 UNIX 系统上执行 `ln /tmp ~/tmp` 命令。该命令的目的是什么？执行该命令时会发生什么？结果合理吗？为什么或为什么不？
