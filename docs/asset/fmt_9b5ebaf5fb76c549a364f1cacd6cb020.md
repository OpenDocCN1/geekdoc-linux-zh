
- `/sbin` 必需系统二进制文件。用于系统管理的实用程序存储在 `/bin` 和 `/usr/sbin` 中。`/sbin` 目录持有系统在启动和运行过程中所需的实用程序。在旧版本的 GNU/Linux 中，许多系统管理实用程序散落在几个目录中，通常包括其他文件系统（`/etc`、`/usr/bin`、`/usr/adm`、`/usr/include`）。

- `/tmp` 临时文件。许多程序使用此目录存放临时文件。

- `/usr` 第二主要层次结构。此目录传统上包含系统信息的子目录。`/usr` 子目录并不经常更改，并且被多个系统共享。

- `/usr/bin` 大多数命令。此目录包含标准的 GNU/Linux 实用程序：在单用户模式下不需要的二进制文件（第 949 页）。

- `/usr/bin/X11` 指向 `/usr/X11R/bin` 的符号链接

- `/usr/games` 游戏和教育程序

- `/usr/include` C 程序包含的头文件

- `/usr/include/X11` 指向 `/usr/X11R/include/X11` 的符号链接

- `/usr/lib` 库

- `/usr/lib/X11` 指向 `/usr/X11R/lib/X11` 的符号链接

- `/usr/local` 本地层次结构。此目录持有本地重要的文件和目录，这些通常被添加到 Red Hat 中。`/usr/local` 的子目录包括 `bin`, `games`, `include`, `lib`, `shin`, `share` 和 `src`。

- `/usr/man` 在手册

- `/usr/sbin` 非易失性系统管理独立性数据二进制文件。参见 `/sbin`。

- `/usr/share` 体系无关数据。`/usr/share` 子目录包括 `dict`, `doc`, `games`, `info`, `local`, `man`, `misc`, `terminfo` 和 `zoneinfo`。

- `/usr/doc` 杂类文档

- `/usr/share/info` GNU info 系统的主目录

- `/usr/src` 源代码

- `/usr/X11R6` X 窗口系统，第 11 版本 6。

- `/var` 可变数据。内容随系统运行而变化的文件位于 `/var` 的子目录。最常见的例子是临时文件、系统日志文件、损坏文件和邮件邮箱。`/var` 的子目录包括 `cache`, `lib`, `lock`, `log`, `opt`, `run`, `spool`, `tmp` 和 `var`。

- `/var/log` 文件。此目录包含 `lastlog`（每个用户的最后登录记录）、`messages`（来自 `syslog` 的消息）和 `wtmp`（所有登录/注销记录）。

- `/var/spool` 队列应用程序数据。此目录包含 `anacron` `at`, `cron`, `lpd`, `mail`, `mqueue`, `news`, `samba` 和 `uucp`。`/var/spool/mail` 文件在 `/var` 中有一个符号链接

# 操作目录

本节涵盖了删除目录、在目录之间复制和移动文件以及移动目录。它描述了如何使用路径让 GNU/Linux 工作变得更容易。

## `rmdir`：删除目录

`rmdir`（删除目录）实用程序删除目录。你不能删除工作目录或包含除 `.` 和 `..` 外内容的目录。如果你需要删除包含文件的目录，首先使用 `rm` 删除文件，然后删除目录。你不需要删除 `.` 和 `..` 条目；`rmdir` 会自动删除。以下命令删除了图 4-5 中创建的目录：

```
rmdir /home/alex/literature
```

`rm` 实用程序有一个 `-r` 选项（`rm -r filename`），递归删除目录内的文件、目录，并删除该目录

虽然 `rm -r` 是一个方便的命令，但你必须谨慎使用。不要对模糊的文件引用（如 `*`）使用它。你很容易通过一个简单的命令抹掉整个目录。

| 谨慎使用 rm -r，如果可以不用的 || 警告 |

## 路径 (Pathnames)

在下面的示例中，`/home/alex` 是工作目录。该示例使用相对路径将文件 `letter` 复制到 `/home/alex/literature/promo` 目录。复制的文件同为 `letter.0610`：

```
$ pwd
/home/alex
$ cp letter literature/promo/letter.0610
```

如果你想尝试接下来的示例，请使用文本编辑器创建一个名为 `letter` 的文件。

假设 Alex 没有切换到其他目录，以下命令允许他编辑他刚刚创建的文件副本：

```
$ vi literature/promo/letter.0610
.
```

如果 Alex 不想使用长路径来指定文件，可以使用 `cd` 将 `promo` 目录设置为工作目录，然后再使用 `vi`。

```
$ cd literature/promo
$ pwd
/home/alex/literature/promo
$ vi letter.0610
.
```

如果 Alex 想将工作目录的父目录（命名为 `/home/alex/literature`）设置为新的工作目录，可以输入以下命令，该命令利用了 `..` 目录项：

```
$ cd ..
$pwd
/home/alex/literature
```

## 可选项 (Optional)

## 特殊路径 (Special Pathnames)

为了减少输入，shell 和某些工具（如 `vi`）识别路径中的一些快捷方式。shell 会将路径开头的字符 `~/`（波浪号加斜杠）扩展为你的家目录路径。使用此快捷方式，无论你当前在哪个目录中，都可以通过以下命令检查你的 `.login` 文件：

```
$ less ~/.login
```

## 目录操作 (Working with Directories)

波浪号 `~` 可以快速引用以你或某人的家目录开头的路径。shell 会将路径开头波浪号加登录名的扩展为该用户家目录的路径。假设 Alex 有权限这样做，他可以使用以下命令检查 Scott 的登录文件：

```
$ less ~scott/.login
```

关于此主题的讨论，请参阅第 609 页的“波浪号扩展 (Tilde Expansion)”。

## `mv`, `cp`：移动或复制文件

第 3 章描述了如何使用 `mv` 重命名文件。然而，`mv` 的功能比此更广：你可以使用 `mv` 将文件从一个目录移动到另一个目录（更改文件的路径），并更改简单的文件名。

当用于将一个或多个文件移动到新目录时，`mv` 命令的语法为：

```
mv existing-file-list directory
```

如果工作目录是 `/home/alex`，Alex 可以以下命令将 `names` 和 `temp` 文件从工作目录移动到 `literature` 目录：

```
$ mv names temp
```

此命令将 `names` 和 `temp` 的绝对路径从 `/home/alex/names` 和 `/home/alex/temp` 更改为 `/home/alex/literature/temp`。与大多数 GNU/Linux 命令一样，`mv` 接受绝对或相对路径。![](aa8214d91cf502c43284529fb3b166_0.png) 图 4-11 目录与普通文件

## 第 4 章 GNU/Linux 文件系统 (Chapter 4 The GNU/Linux Filesystem)

当你使用 GNU/Linux 并创建更多文件时，你需要使用 `mkdir` 创建目录以保持文件整齐。`mv` 工具是将文件从一个目录移动到另一个目录的有用工具。`cp` 工具的工作原理与 `mv` 相同，但是在指定的目录下创建 `existing-file-list` 的副本。

## `mv`：移动目录 (mv: Moves a Directory)

`mv` 在将普通文件从一个目录移动到另一个目录的同时，也可以移动目录。其语法相似，但你指定的是一个或多个目录，而不是普通文件：

```
mv existing-directory new-directory
```

如果 `new-directory` 不存在，则 `existing-directory` 必须仅包含一个目录，此时 `mv` 将重命名该目录。虽然可以使用 `mv` 重命名目录，除非使用 `-r` 选项（第 12 页），否则无法复制其内容。其他复制方法参考第三部分的 `tar`。

## 访问权限 (Access Permissions)

三类型的用户可以访问文件：文件的所有者（`owner`）、所有者所属组的成员（`group`）以及其他所有人（`other`）。用户可以通过三种方式尝试访问普通文件：尝试读取、写入或执行它。三类用户，每种用户都可以以三种方式访问文件，总共有九种访问普通文件的可能方式。

## `ls -l`：显示权限 (ls -l: Displays Permissions)

当你带有 `-l` 选项和普通文件名调用 `ls` 时，`ls` 会显示关于该文件的信息。文件 `letter.0610` 包含信的内容，而 `check_spell` 包含一个用高级编程语言编写的 shell 脚本：
