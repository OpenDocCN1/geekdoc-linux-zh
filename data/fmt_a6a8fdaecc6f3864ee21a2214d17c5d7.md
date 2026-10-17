
`/usr` 目录包含 LINUX/UN 文件系统中最大的部分之一。它包含可以在不同主机之间共享的只读数据。在大多数 LINUX 系统上，`/usr` 子目录：`X11R6`、`bin`、`doc`、`games`、`include`、`lib`、`local`、`man`、`sbin`、`src` 和 `tmp`。表 2.1 简要描述了这些目录的内容。

## `/var`

`/var` 目录用于包含变量数据（系统运行期间不断变化的数据）。这些数据维护在几个子目录中，但对大多数子目录的讨论超出了本书的范围。其中一个目录是 `/var/spool/mail`，它包含你的收件箱。当你读取新邮件时，它来自该目录下的一个设置为包含你收件邮件的文件。一旦读取了邮件，它会被放入你家目录下一个名为 `mbox` 的文件中。

# LINUX 中的一些标准目录和文件

| 表 2.1 /usr 中的主要子目录 |
| 子目录 | 内容 |
| :--- | :--- |
| X11R6 | X 窗口系统第11版本第6发布及相关文件 |
| bin | 大多数用户使用。它还包含如 `perl`、`python` 和 `tcl` 等解释器 |
| doc | 各种工具、实用程序、库、应用程序、解释器的文档，如 `cc`、`gcc`、`XFree86`、`GNOME`、`Mesa` 和 `zsh` |
| games | 游戏和教育软件的可执行文件 |
| include | C/C++ 头文件，包含某些特定的头文件，如网络应用程序所需的头文件（`/usr/include/netdb`、`/usr/include/netinet` 等）、GNU C++ 头文件（`/usr/include/g+`）以及系统特定头文件（`/include/sys`） |
| lib | 对象文件和内部二进制文件（不供用户或 脚本执行）。某些子目录包含特定工具或应用程序的库，如 `gcc-lib`、`gnome-lib`、`netscape`、`perl`、`tcl_ib` 和 `emacs` |
| local | 系统管理员本地安装供主机间共享的软件（二进制文件和数据）。大多数系统包含以下目录：`bin`、`doc`、`etc`、`games`、`man`、`sbin` 和 `src` |
| man | LINUX 和 UNIX 命令、实用程序、工具和应用程序的手页 |
| sbin | 系统管理员和守护进程使用的非必需命令和工具 |
| share | 只读体系无关数据文件，即特定操作系统不同平台（Pentium、Alpha、Sparc 等）共享的数据 |
| src | LINUX/UN 软件包管理软件源代码（例如 RPM：红帽软件包管理） |
| tmp | 指向 `/tmp` 的符号链接 |

### `/etc/passwd`

`/etc/passwd` 文件为系统中的每个用户包含一行，描述该用户是。每行有七个字段，用逗号分隔。以下是行的格式：

`login_name:dummy_or_encrypted_password:user_ID:group_ID:home_directory:login_shell`

`login_name` 是系统识别用户的登录名，也是用户登录时输入的名称。`dummy_or_encrypted_password` 字段包含密码 x (*) 或密码的加密版本。如果密码存储在 `/etc/passwd` 中，则加密密码存储在 `/etc/shadow` 中。`user_ID` 是分配给用户的 0 到 65535 之间的整数，0 分配给超级用户，1–99 预留。`group_ID` 标识用户所属的组，也是 0 到 65535-99 之间的整数。`user_info` 字段包含关于用户的信息，通常是用户的全名。`home_directory` 字段包含该的绝对路径。

# 40 第2章 文件与文件处理

在接下来的会话中，我们将展示这些命令的使用。第一个命令将 `temp` 目录移动到主目录。第二个命令生成一个错误消息：目标 (`file1`) 不是一个目录。最后一个命令将你主目录下（并包括）`courses` 目录的完整目录结构复制为 `courses.bak` 目录。

```
$ mv temp ~
$ mv dir file1
mv: cannot create directory `file1`: File exists
$ cp -r courses ~/courses.bak
$
```

## 2.5.3 浏览文件系统结构和列出目录

`cd` 命令允许你在目录结构中来回跳转。如果不带参数执行，它会将你带到主目录。你可以通过 `pwd` 命令显示当前目录的绝对路径，并通过 `ls` 命令显示目录的内容（目录中的文件和目录）。`ls` 可能是最常用的 LINUX 和 UNIX 命令，可以配合许多选项使用。以下是该命令的简要描述。

![](img/62803a90ad1a923bf070a7b5e2ffbb05_57_0.png)

如果不带参数使用，该命令会显示当前目录下的文件和目录名称。该命令的一些常用选项及其含义列于表2.2。`ls` 命令主要配合 `-l` 选项使用。我们将在2.6.2节中描述 `ls -l` 命令的输出。

## 目录操作与浏览文件系统结构 41

| 表 2.2 ls 命令的常用选项及其含义 |
| 选项 | 含义 |
| :--- | :--- |
| -l | 显示目录中文件（所有类型，隐藏文件除外）的详细列表 |
| -a | 显示目录中的所有文件，包括隐藏文件 |
| -d | 显示目录本身的详细列表（而不包含其内容）；通常与 -l 选项配合使用，即 -ld |
| -t | 根据时间戳（修改时间）显示文件，最近修改的文件在最前面；可以使用 -r 选项按反序列出文件 |
| -q | 按访问时间（而非修改时间）显示文件 |
| -s | 按大小显示文件（以 sk 块为单位） |

可以使用 `-ltr` 选项按当前修改时间的反序显示目录的详细列表。如果不带目录参数，该命令将列出当前工作目录下的文件。

在接下来的会话中，我们将展示这些命令的使用。不带参数的 `cd` 命令将你置于主目录。`ls -ld ~/temp` 命令显示 `~/temp` 目录的详细列表。`cd courses/cs475` 将你置于主目录下的 `courses/cs475` 目录。`pwd` 命令显示当前目录的绝对路径。接下来的 `cd` 命令显示你当前目录中的文件名（此时该目录也是你的主目录）。此列表不包含隐藏文件（即以点 `.` 开头的文件），例如 `.bashrc`。`ls -a -` 命令显示你主目录下所有文件的名称，包括隐藏文件（即以点 `.` 开头的文件）。

```
$ cd
$ ls -ld ~/temp
drwx------ 2 sarwar faculty 512 Oct 6 12:45
/home/faculty/sarwar/temp
$ cd ~/courses/cs475
$ pwd
$ cd ..
$ pwd
/home/faculty/sarwar/
$ cd
$ ls
bin books courses linuxtools mail personal temp
```

## 42 第2章 文件与文件处理

```
$ ls -a
  .bash_profile .emacs .gtkrc .nautilus
  .. .bashrc .gconf .ICEAuthority .pinerc
  .addressbook bin .gconfd input.c .sawfish
  .addressbook.lu books .gnome .kde .screenrc
  .bash_history vsroot .gnome-desktop linuxtools .Xauthority
  .bash_logout ddd .gnome_private mail .xsession-
  errors $
```

在随后的课内练习中，你将浏览 LINUX/UNIX 机器的文件系统，在其中定位某些信息，并显示和更改 shell 的搜索路径。

# 课内练习

- 2.1 浏览你的 LINUX/UNIX 文件系统并找到包含 LINUX 或 UNIX 内核的文件。该文件的绝对路径是什么？
- 2.2 搜索 `/etc/passwd` 文件以找到你用户名的那行。写下这一行。你的用户 ID、组 ID、主目录和登录 shell 分什么？
- 2.3 使用 `echo $PATH`（或 `$path`）命令显示你的 shell 搜索路径。扩展搜索路径包含你的主目录和当前目录。

## 2.6 文件处理

我们描述了如何在 LINUX 和 UNIX 中创建和操作文本文件，如何获取有关文件（任何类型）属性的信息，以及你如何保护你的文件。

### 2.6.1 创建文件

你可以使用文本编辑器在 LINUX 和 UNIX 中创建文本文件。LINUX/UNIX 有多种原生和非原生文本编辑器，如 `emacs`, `pico`, `vi`, `vim`, `Wemacs`。附录 A 提供了 `vi` 和 `pico` 编辑器的简要描述。

### 2.6.2 显示文件类型和数据
