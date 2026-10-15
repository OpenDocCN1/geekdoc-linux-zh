
一旦文件被删除，恢复它的唯一方法是从你或系统管理员对文件系统进行的归档备份中恢复。

```
$ cd
$ rm myfile2
rm: myfile2: No such file or directory
$
```

你收到错误消息是因为在主目录中，名为 myfile2 的文件不存在。它已被移动到了名为 first 的子目录中。

目录组织还包括删除空目录或非空目录的能力。用于删除空目录的命令是 rmdir。rmdir 命令的一般语法如下：

### 语法

```
rmdir [options] dirnames
```

+   **用途：** 删除 dirnames 中指定的空目录
+   **输出：** 删除目录
+   **常用选项/功能：**
+   - **-p** 同时删除空的父目录
+   - **-r** 递归删除当前目录下的文件和子目录

要删除当前工作目录下方的整个目录，请键入以下命令：

```
$ rmdir first
rmdir: first: Directory not empty
$
```

由于文件 myfile2 仍在名为 first 的子目录中，first 不是空目录，因此你会收到 rmdir 命令不会删除该目录的错误消息。如果该目录是空的，rmdir 就会完成删除。删除非空目录的一种方法是使用带 -r 选项的 rm 命令。-r 选项会递归地下沉到子目录中，并在实际删除目录本身之前删除其中的任何文件。使用此命令时要小心，因为可能会无意中删除目录和文件。要了解此命令如何删除非空目录，请键入以下命令：

```
$ rm -r first
$
```

目录 first 和文件 myfile2 现在已从文件结构中删除。

## 2.4.5 使用 man 命令获取帮助

UNIX 系统上一个非常方便的工具是在线帮助功能，可通过 man 命令实现。man 命令的一般语法如下：

### 语法

```
man [options] [-s section] command-list
man -k keyword-list
```

用途：第一种语法：一次显示一屏 command-list 中命令的 UNIX 参考手册页
第二种语法：显示与 keyword-list 中的关键字相关的命令摘要

输出：一次显示一屏手册页

# 常用选项/功能：

+   - **-k keyword-list** 在数据库中搜索 keyword-list 中的关键字摘要并显示它们
+   - **-s sec-num** 搜索节号 sec-num 的手册页并显示它们

要使用 man 命令获取有关 ls 命令用法和选项的帮助，例如，请键入以下命令（针对 PC-BSD 显示）：

```
$ man ls
```

```
LS(1)
FreeBSD General Commands Manual LS(1)
NAME
ls - list directory contents
SYNOPSIS
ls [-ABCFGHLPRTWZabcd fghiklmnopqrstuxwxl] [file ...]
DESCRIPTION
```

对于每个命名非目录类型文件的操作数，ls 会显示其名称以及任何请求的关联信息。对于每个命名目录类型文件的操作数，ls 会显示该目录中包含的文件名，以及任何请求的关联信息。
如果未给出操作数，则显示当前目录的内容。如果给出了多个操作数，则先显示非目录操作数；目录和非目录操作数分别按字典顺序排序。
以下选项可用：
按 <SPACE> 继续，或按 q 退出 q
$

这个来自 UNIX 的输出是一个 UNIX 手册页，即 man 页，它给出了命令用法的概要，展示了选项，并提供了简要说明，帮助你理解该命令应如何使用。如示例所示，在显示一页后键入 q，会返回命令行提示符。按键盘上的空格键，则会一次一屏地显示与 ls 命令相关的手册页的更多内容。

要获取使用所有 UNIX 命令及其选项的帮助，请使用 man man 命令转到 UNIX 参考手册页。
