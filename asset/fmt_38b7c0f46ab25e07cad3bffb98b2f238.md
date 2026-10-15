
Manual page 1s(1) line 1 (press h for help or q to quit)

$

要搜索 man 页面，请向 `man` 命令的 `-k` 选项提供关键字。如果你正在寻找一个可以重启系统的命令，可以搜索 `"reboot"`。一旦获得了包含该关键词的 man 页面列表，你就可以阅读其中最有希望的文档了。

```
$ man -k reboot
grub-reboot (8) - 仅为下次启动设置 GRUB 的默认启动项
halt (8) - 重启或停止系统
poweroff (8) - 重启或停止系统
reboot (2) - 重启或启用/禁用 Ctrl-Alt-Del
reboot (8) - 重启或停止系统
$ man reboot
```

NAME

`reboot`, `halt`, `poweroff` - 重启或停止系统...

某些命令在提供参数 `-h` 或 `--help` 时会打印帮助信息。即使是 `man` 命令也遵循这一约定。

```
$ man -h
Usage: man [OPTION...] [SECTION] PAGE

-C, --config-file=FILE 使用此用户配置文件
-d, --debug 发出调试消息
-D, --default 将所有选项重置为默认值
  --warnings=[WARNINGS] 启用 groff 的警告
```

```
$ man --help
Usage: man [OPTION...] [SECTION] PAGE

-C, --config-file=FILE 使用此用户配置文件
-d, --debug 发出调试消息
-D, --default 将所有选项重置为默认值
  --warnings=[WARNINGS] 启用 groff 的警告
...
$ ls --help
Usage: ls [OPTION]... [FILE]...
```

列出 `FILE`（默认是当前目录）的信息。

如果未指定 `-cftuvUX` 或 `--sort`，则按字母顺序对条目排序。

长选项的强制性参数对于短选项也是强制性的。

`-a`, `--all` 不忽略以 `.` 开头的条目。

根据你对 Linux 目录结构的了解以及 Linux 操作系统附带的文档，你可以开始自己探索命令了。例如，列出 `/bin` 和 `/usr/bin` 的目录内容。挑选一些引起你注意的命令，并使用 `man` 命令查找其中每个命令的作用。

```
$ cd /bin
$ ls
awk diff cat cp date du echo grep groups less more
$ man date
NAME
    date - 打印或设置系统日期和时间
...
$ cd /usr/bin
$ ls
clear crontab cut dos2unix find kill mv pstree pwd sed strings touch ...
$ man clear
```

前面的 `ls` 命令的输出被截断了。在实际上，你可能会在 `/bin` 中找到几十个命令，在 `/usr/bin` 中找到数百个命令。

在继续之前，我想分享最后一个你可能觉得有基础命令。它是 `clear` 命令。如果你想要一个干净的屏幕来工作，那就是 `clear` 命令。

# 第4 章 目录

根据你对 Linux 目录结构的了解以及 Linux 操作系统附带的文档，你可以开始自己探索命令了。例如，列出 `/bin` 和 `/usr/bin` 的目录内容。挑选一些引起你注意的命令，并使用 `man` 命令查找其中每个命令的作用。

## 创建和删除目录

除了通过完整或相对路径引用目录外，你还可以创建新目录。绝对路径以 `/` 开头。相对路径不是。以下是一个示例：

```
$ mkdir testdir
$ls
testdir
$ mkdir testdir/subdir
$ ls -R testdir
testdir
subdir
```

要删除空目录，使用 `rmdir` 命令。要删除目录及其内容，请使用 `rm -rf` 命令。

```
$ rmdir testdir
$ rm -rf testdir
```

## 绝对路径和相对路径

绝对路径以 `/` 开头。相对路径不是。以下是一个示例：

```
$ mkdir testdir
$ls
testdir
$ mkdir testdir/subdir
$ ls -R testdir
testdir
subdir
```

要删除空目录，使用 `rmdir` 命令。要删除目录及其内容，使用 `rm -rf` 命令。

```
$ rmdir testdir
$ rm -rf testdir
```

# 第5 章 查看文件详情

`ls` 命令在第3章中简单介绍。它不仅列出文件和目录，还能提供这些目录的详细信息。`ls` 最常用的选项之一是 `-l`，它显示列表格式。以下是一个示例：

```
$ ls
Desktop Documents Music to-do.txt
$ ls -l
total 20
drw-xr-x 2 jason users 4096 May 3 08:33 Desktop
drw-xr-x 2 jason users 4096 May 3 08:35 Documents
drw-xr-x 2 jason users 4096 May 3 08:38 Downloads
drw-xr-x 3 jason users 4096 Jun 21 21:16 Music
-rw-r---- 1 jason users 73 Jun 22 19:34 to-do.txt
$
```

`ls -l` 提供的信息以一系列字符开头，表示文件或目录的权限。权限将在第6章中介绍。权限字符串后面的数字代表指向该文件或目录的链接数。接着显示所有者，然后是组名。然后显示文件大小。时间戳代表修改时间。最后一项是文件或目录名称。

```
$ ls -l to-do.txt
-rw-r---- 1 jason users 73 Jun 22 19:34 to-do.txt
```

默认情况下，`ls` 不显示以点（`.`）开头的文件或目录。在 Linux 中，此类文件被视为隐藏文件。要用 `ls` 显示隐藏文件，请使用 `-a` 选项来包含所有项目。要以长列表格式显示所有项目，请使用 `-1` 和 `-a`。记住选项可以组合使用。这三个命令是等价的：`ls -1 -a`、`ls -la` 和 `ls -al`。

```
$ ls
Desktop  Documents  Downloads  Music  to-do.txt
$ ls -a
..  .bash_history  bash_logout  bashrc  Desktop  Documents  Downloads
Music  .profile  .ssh  to-do.txt
$ ls -a -l
total 48
drwxr-xr-x 7 users 4096 Jun 22 20:36 .
drwxr-xr-x 6 root 4096 May 4 10:26 ..
-rw-r--r 1 users 3738 Jun 22 19:37 .bash_history
-rw-r---- 1 users 220 Mar 30 2013 .bash_logout
-rw-r---- 1 users 3650 Jun 22 19:41 .bashrc
drwxr-xr-x 2 users 4096 May 3 08:33 Desktop
drwxr-xr-x 2 users 4096 May 3 08:35 Documents
drwxr-xr-x 2 users 4096 May 3 08:38 Downloads
drwxr-xr-x 3 users 4096 Jun 21 21:16 Music
-rw-r---- 1 users 675 Mar 30 2013 .profile
drwx------ 2 users 4096 May 3 12:44 .ssh
-rw-r---- 1 users 73 Jun 22 19:34 to-do.txt
$ ls -al
total 48
drwxr-xr-x 7 users 4096 Jun 22 20:36 .
drwxr-xr-x 6 root 4096 May 4 10:26 ..
-rw------ 1 users 3738 Jun 22 19:37 .bash_history
-rw-r---- 1 users 220 Mar 30 2013 .bash_logout
-rw-r---- 1 users 3650 Jun 22 19:41 .bashrc
drwxr-xr-x 2 users 4096 May 3 08:33 Desktop
drwxr-xr-x 2 users 4096 May 3 08:35 Documents
drwxr-xr-x 2 users 4096 May 3 08:38 Downloads
drwxr-xr-x 3 users 4096 Jun 21 21:16 Music
-rw-r---- 1 users 675 Mar 30 2013 .profile
drwx------ 2 users 4096 May 3 12:44 .ssh
-rw-r---- 1 users 73 Jun 22 19:34 to-do.txt
$ ls -la
total 48
drwxr-xr-x 7 users 4096 Jun 22 20:36 .
drwxr-xr-x 6 root 4096 May 4 10:26 ..
-rw------ 1 users 3738 Jun 22 19:37 .bash_history
-rw-r--r-- 1 jason users 220 Mar 30 2013 .bash_logout
-rw-r--r-- 1 jason users 3650 Jun 22 19:41 .bashrc
drwxr-xr-x 2 jason users 4096 May 3 08:33 Desktop
drwxr-xr-x 2 jason users 4096 May 3 08:35 Documents
drwxr-xr-x 2 jason users 4096 May 3 08:38 Downloads
drwxr-xr-x 2 jason users 4096 Jun 21 21:16 Music
-rw-r--r-- 1 jason users 675 Mar 30 2013 .profile
drwx------ 2 jason users 4096 May 3 12:44 .ssh
-rw-r--r-- 1 jason users 73 Jun 22 19:34 to-do.txt
```

若要在 `ls` 中在文件或目录名称后添加文件类型指示，请使用 `-F` 选项。

```
$ ls
Desktop Documents Downloads link-to-to-do Music program to-do.txt
$ ls -F
Desktop/ Documents/ Downloads/ link-to-to-do@ Music/ program* to-do.txt
$ ls -1F
total 24
drwxr-xr-x 2 jason users 4096 May 3 08:33 Desktop/
drwxr-xr-x 2 jason users 4096 May 3 08:35 Documents/
drwxr-xr-x 2 jason users 4096 May 3 08:38 Downloads/
lrwxr-xr-x 1 jason users 9 Jun 22 21:01 link-to-to-do -> to-do.txt
drwxr-xr-x 3 jason users 4096 Jun 21 21:16 Music/
-rwxr-xr-x 1 jason users 13 Jun 22 21:02 program*/
-rw-r--r-- 1 jason users 73 Jun 22 19:34 to-do.txt
$
```

表 2：文件类型指示

| 符号 | 文件类型 |
| --- | --- |
| / | 目录 |
| @ | 符号链接，`->` 符号之后的文件是链接的目标。 |
| * | 可执行脚本或程序 |
| = | 套接字 |
| > | 门 (Door) |
| \| | 命名管道 |

符号链接（有时称为 symlink 或 link）指向实际文件或目录的位置。符号链接只是一个指针，但你可以像操作实际文件或目录一样对其进行操作。符号链接通常用于创建长路径的快捷方式。符号链接的另一个常见用途如下所示，指向应用程序的当前版本。

```
$ cd /opt/
$ ls -F
1.6.0/ 1.7.1/ 1.7.2/ current@
$ ls -l
total 12
drwxr-xr-x 2 root 4096 Jun 22 21:12 1.6.0/
drwxr-xr-x 2 root 4096 Jun 22 21:11 1.7.1/
drwxr-xr-x 2 root 4096 Jun 22 21:11 1.7.2/
lrwxrwxrwx 1 root 5 Jun 22 21:12 -> 1.7.2/
$
```

要按时间对 `ls` 命令的输出进行排序，请使用 `-t` 选项。它会显示最近修改的项目。如果你想反转顺序，请使用 `-r`。这在你有一个包含许多文件的目录时非常有用。当按时间反向排序时，旧文件将滚出屏幕顶部，而最新的文件将显示在你的提示符上方。

```
$ ls -t
program link-to-to-do to-do.txt Music Desktop
$ ls -lt
total 24
drwxr-xr-x 1 jason users 13 Jun 22 21:02 program
-rw-r---- 1 jason users 73 Jun 22 19:34 to-do.txt
drwxr-xr-x 3 jason users 4096 Jun 21 21:16 Music
drwxr-xr-x 2 jason users 4096 May 3 08:38 Downloads
drwxr-xr-x 2 jason users 4096 May 3 08:35 Documents
drwxr-xr-x 2 jason users 4096 May 3 08:33 Desktop
```

### 空格与特殊字符的转义

尽管文件名和目录名允许包含空格，但最好尽可能避免它们。如果不使用空格，可以考虑使用连字符或下划线。另一个很好的选择是使用驼峰命名法（CamelCase）。例如，不要将文件命名为 `my to do list`，而是命名为 `my-to-do-list`、`my_to_do_list`甚至是 `ToDoList`。

即使你选择在文件名中使用空格，可能会遇到他人创建的文件。处理包含空格的文件有两种方法：使用引号或转义。要操作名为 `my to do list` 的文件，请用引号括起来，如 `"my to do list"`。要转义文件名，请在空格前加反斜杠，如 `my\ to\ do\ list`。转义就像引号，只不过适用于单个字符。

如果你不确定如何转义文件或目录名称，可以让 `ls` 通过 `-b` 选项为你显示。引用和转义不仅针对空格，还针对其他特殊字符，如 `|`、`&`、'` `;`、空格和制表符。

```
$ ls
my to do list
$ ls -l
total 4
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my to do list
$ ls -1 my to do list
ls: cannot access my: No file or directory
ls: cannot access to: No file or directory
ls: cannot access do: No file or directory
ls: cannot access list: No file or directory
$ ls -1 "my to do list"
```

```bash
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my to do list
$ ls -l my\ o\ do\ list
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my to do list
$ ls -lb
total 4
-rw-r--r-- 1 jason users 73 Jun 22 22:16 my\ o\ do\ list
$
```

# 第 6 章 权限

回看 `ls` 命令提供的长列表，我们现在可以解读给定文件或目录列表的权限了。权限显示在长列表的开头。

```bash
$ ls -l sales.data
-rw-r--r-- 1 jason users 10400 Jun 14 09:31 sales.data
```

权限字符串中的第一个字符揭示了类型。例如，`-` 是普通文件，`d` 是目录，`l` 是符号链接。这些是你会遇到的最常见的类型。然而，下表还列出了其他文件类型。

表 4：文件类型

| 文件类型 | 符号 |
| :--- | :--- |
| 普通文件 | - |
| 块设备文件 | b |
| 字符设备文件 | c |
| 目录 | d |
| 符号链接 | l |
| FIFO (命名管道) | p |
| 套接字 | s |
| 其他文件类型 | ? |

权限字符串中的其余字符代表了三种主要的权限类型：读、写和执行。每个权限由单个字母表示，称为符号。读用 `r` 表示，写用 `w` 表示，执行用 `x` 表示。

表 5：权限

| 权限 | 符号 |
| :--- | :--- |
| 读取 | r |
| 写入 | w |
| 执行 | x |

对于文件而非目录，读、写和执行权限具有直观的含义。读取权限允许你查看文件内容。写入权限允许你修改文件。执行权限允许你运行或作为程序执行一个文件。

当涉及到目录时，读、写和执行权限的含义并不直观。读取权限允许你读取目录中的文件名。写入权限允许通过重命名文件、创建文件和删除文件来更改目录中的项。执行权限允许你 `cd` 进入该目录。查看以下文件权限和目录权限之间的区别。

表 6：文件和目录权限

| 权限 | 文件含义 | 目录含义 |
