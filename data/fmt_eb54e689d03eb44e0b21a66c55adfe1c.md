
参见第 2-4 节以获取关于 `nano` 编辑器的详细信息。

## 使用 `uniq` 命令

`uniq` 命令识别文件或输入中的重复行。在没有任何选项的情况下，该命令打印唯一的行；使用 `-d` 选项时只打印重复行。你可以指定 `-i` 选项来指示命令忽略大小写。这是一个示例：

```
$ uniq /etc/profile
```

```
## .bashprofile

if [ -f~/.bashrc ]; then

  ~/.bashrc

```

```
# User specific environment and startup programs

export PATH
```

## 使用 `strings` 命令

`strings` 命令发现并显示嵌入非文本文件中的可读信息。例如，当你对 `/bin/cat` 运行 `strings` 命令时，你会看到类似下面的输出。尽管 `/bin/cat` 是非文本文件，但它确实包含一些可读信息。

```
$ strings /bin/cat
/lib/ld-linux.so.2
_gmon_start_
libc.so.6
_IO_std_used
_printf_chk
setlocale
mbrtwc
optind
......
```

## 复制文件和目录

复制操作复制文件或目录。有一个名为 `cp` 的命令用于此处。

### 复制文件

`cp` 命令将一个或多个文件复制到当前目录或其他目录。如果你想在相同目录下复制文件，则必须给目标文件一个不同的名称。如果你想将文件复制到另一个目录，可以使用与原始文件相同的文件名，也可以分配一个不同的名称。考虑以下示例。

在相同目录下将 `file1` 复制为 `newfile`：

```
$ cp file1 newfile
```

将 `file1` 按相同名称复制到目录 `subdir1`：

```
$ cp file1 subdir1
```

## 文件和目录操作总结

表 2-2 列出了你刚刚学习的文件和目录操作命令。

| 命令目标 | 文件 | 目录 |
|---|---|---|
| 创建 | `cat`, `touch`, `vi`, `vim`, `nano` | `mkdir` |
| 列出 | `ll`, `ls` | `ll`, `ls` |
| 显示内容 | `cat`, `more`, `head`, `tail`, `view`, `vi`, `vim`, `nano`, `uniq`, `strings` | `ll`, `ls` |
| 复制 | `cp` | `cp` |
| 移动 | `mv` | `mv` |
| 重命名 | `mv` | `mv` |
| 删除 | `rm` | `rm -r`, `rdir` |
| 显示统计信息 | `stat` | `stat` |

表 2-2 文件/目录操作总结

## 使用 Nautilus 文件管理器进行文件和目录操作

可以使用 Nautilus 文件管理器来执行目前讨论的文件和目录操作。要启动该工具，请在 X 终端窗口提示符处执行 `nautilus` 命令，或者点击应用程序 $\rightarrow$ 系统工具 $\rightarrow$ 文件浏览器，亦或点击桌面上的计算机图标。默认情况下，Nautilus 显示运行它的用户的家目录内容。见图 2-3。在界面中导航并执行操作进行练习。

![](img/3f35ec29a294974bc1a4fdae3ae46652_77_0.png)

图 2-3 Nautilus 文件管理器

## 修改文件和目录控制属性

在文件或目录上可以设置某些控制属性，使其变为仅可追加、不可更改、不可检测等。例如，你可以对关键系统文件或目录启用某些属性，使得包括 `root` 在内的任何用户无法删除或更改它；禁用如 `dump` 命令之类的备份工具以备份特定的文件或目录等。这些属性只能设置在位于 `ext2` 或 `ext3` 文件系统中的文件和目录上。有关 `ext2` 和 `ext3` 文件系统的详细信息，请参阅第 14 章“文件系统和交换”。

表 2-3 列出了常见的控制属性。

| 属性 | 对文件或目录的影响 |
| --- | --- |
| a `append` | 文件只能被追加。 |
| A | 防止更新访问时间。 |
| c `compressed` | 文件自动压缩。 |
| d `dump` | 文件无法使用 `dump` 命令备份。 |
| D | 目录上的更改将同步写入磁盘。 |
| i `immutable` | 文件无法被更改、重命名或删除。 |
| j `journaling` | 文件在写入文件本身之前，其数据会被写入日志。有关日志记录的详细信息，请参阅第 14 章“文件系统和交换”。 |
| s `secure delete` | 文件块将被擦除。 |
| S `synchronous` | 文件上的更改将同步写入磁盘。 |
| u `undeletable` | 文件无法被删除。 |

### 表 2-3 文件和目录控制属性

可以使用 `lsattr` 和 `chattr` 两个命令来列出和修改这些属性。以下演示了几个用法示例，假设你处于 `/root` 目录且 `install.log` 存在。

列出 `install.log` 上的当前属性：

```
### lsattr install.log
---------- install.log
```

输出表明该文件目前没有设置任何属性。

防止 `install.log` 被删除和进行任何修改：

```
### chattr +i install.log
### lsattr install.log
------i install.log
```

现在，以 `root` 身份删除此文件：

```
### rm install.log
rm: remove write-protected regular file `install.log`? y
rm: cannot remove `install.log`: Operation not permitted
```

仅允许对文件进行追加操作：

```
# chattr +a install.log
# cat /etc/fstab >> install.log
```

取消两个属性：

```
# chattr -ia install.log
```

一次性设置两个属性：

```
# chattr =ia install.log
```

# 模式匹配

RHEL 提供了一个强大的工具，用于搜索一个或多个文本文件的内容，或者输入匹配模式的输入内容。这被称为模式匹配（也称为正则表达式或通配符匹配）。一个模式可以是单个字符、一系列字符、一个单词或一个句子。如果模式包含任何空格，必须用双引号将其括起来。该工具称为 `grep`（全局正则表达式打印），它会在一个或多个指定文件的内容中搜索正则表达式。如果找到，它将在屏幕上打印每一行，而不更改原始文件。请考虑以下示例。

在 `/etc/passwd` 文件中搜索模式 `"user1"`：

```
$ grep user1 /etc/passwd
user1:x:503:/home/user1/bash
```

在 `/etc/passwd` 和 `/etc/group` 文件中同时搜索模式 `"user1"` 的所有出现：

```
$ grep user1 /etc/passwd /etc/group
/etc/passwd:user1:x:503:/home/user1/bash
/etc/group:user1:x:503:
```

从指定的列表中仅显示包含模式 `"user1"` 的名称，使用 `-l` 选项：

```
$ grep -l user1 /etc/group /etc/passwd
```

在 `/etc/group` 文件中查找模式 `"root"` 并带上行号，使用 `-n` 选项：

```
$ grep -n root /etc/group
1:root:x:root,bin,daemon
2:root:x:root,bin,daemon
```

# 使用 `find` 命令查找文件

`find` 命令递归地搜索目录树，找到符合指定标准的文件并执行相应的操作。这个强大的工具可以进行自定义，以多种方式查找文件。搜索标准可能包括按名称、大小、所有者、组员身份、最后访问或修改时间、权限、文件类型和 inode 号进行查找。以下是命令语法：

| find | 路径 | 动作 |
| --- | --- | --- |
| 命令本身 | 搜索位置。可以是 `/etc`, `/var/adm`, `/usr/lib` 等。 | 按名称查找：`-name` `-exec cmd {} \;` `-ok cmd {} \;` |
| | 按 UID 查找：`-user` |
| | 按 GID 查找：`-group` |
| | 按权限查找：`-perm` |
| | 按 inode 查找：`-inum` |
| | 按访问时间查找：`-atime` |
| | 按修改时间查找：`-mtime` |

使用 `find` 命令，系统会找到符合指定标准的文件，并在屏幕上显示每个文件的完整路径。让我们来看几个例子。

在 `user1` 的家目录 `/home/user1` 中查找 `file2`（假设 `file2` 存在）：
