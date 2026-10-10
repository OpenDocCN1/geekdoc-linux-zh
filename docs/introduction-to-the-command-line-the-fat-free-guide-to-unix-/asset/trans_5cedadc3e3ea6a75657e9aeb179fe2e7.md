

## man

**用途**：命令行程序的在线手册。

**使用语法**：`man [选项] [命令/文件]`

```
$ man ls
LS(1)               User Commands                LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List information about the FILES (the current directory by
       default).  Sort entries alphabetically if none of -cftuvSX nor
       --sort.

       -a, --all
               do not ignore entries starting with .
       ...

查看 ls 命令的手册页
```

**man** 命令显示指定命令的手册（通常称为*man 页*）。每个手册页都提供了关于命令选项和用法的详细信息。在上一个示例中，执行 **man ls** 会显示 **ls** 命令的手册。

下表描述了可用于导航手册程序的按键。

| 按键 | 功能 | 按键 | 功能 |
| :--- | :--- | :--- | :--- |
| 上箭头 | 向上移动一行 | 下箭头 | 向下移动一行 |
| Page Up | 向上翻一页 | Page Down | 向下翻一页 |
| Q | 退出 man 程序 | /[*字符串*] | 搜索文本字符串 |

**man** 命令是你获取命令行帮助的最宝贵资源。如果你不确定某个命令的正确使用语法，请务必查阅手册页。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| man [命令] | 显示指定命令的手册 |
| man -k [关键词] | 在手​​册页中搜索指定关键词 |

## whatis

**用途**：显示指定命令的描述。

**使用语法**：`whatis [选项] [命令]`

```
$ whatis ls
ls (1) - list directory contents
```

查看 ls 命令的手册描述

`whatis` 显示指定命令的简要描述。上述示例使用 `whatis` 显示了 `ls` 命令的描述。这可以作为命令用途的有用提示，而无需查阅 `man` 命令。

可以在一次 `whatis` 查询中使用多个命令来显示每个单独命令的描述。例如，输入 `whatis ls who rm` 会一次性显示所有三个命令的描述，如下一个示例所示。

```
$ whatis ls who rm
ls (1) - list directory contents
who (1) - show who is logged on
rm (1) - remove files or directories
```

查看多个命令的手册描述

> **注意**
> *某些 Unix 系统可能使用 apropos 命令替代 whatis。*

**常见用法示例：**

- `whatis [命令]` - 显示指定命令的描述
- `whatis -w [通配符]` - 使用通配符搜索命令

## ls

**用途**：列出目录内容。

**使用语法**：`ls [选项] [目录/文件]`

```
$ ls
Notes.txt  ShoppingList.txt  ToDoList.txt
```

*ls 命令的典型输出*

执行 **ls** 命令会显示当前目录中的文件简单列表，如上述示例所示。若要查看目录中文件的更多信息，你可以使用命令行选项来启用其他功能，如下一个示例所示。

```
$ ls -l
-rw-r--r--  1 nick sales 35068 2009-05-19 08:41 Notes.txt
-rw-r--r--  1 nick sales   23 2009-05-19 08:43 ShoppingList.txt
-rw-r--r--  1 nick sales   37 2009-05-19 08:43 ToDoList.txt
```

*使用 -l 选项运行 ls 命令*

在此示例中，使用 `-l` 选项生成详细的文件列表，包括权限、所有者、组和修改日期/时间。下表描述了 `ls -l` 命令的输出。

| 权限 | 链接数 | 所有者与组 | 大小 | 修改日期 | 文件或目录 |
|:---|:---|:---|:---|:---|:---|
| -rw-r--r-- | 1 | nick sales | 35068 | 2009-05-19 08:41 | Notes.txt |

*ls -l 命令显示的字段说明*

大多数命令行程序都有许多可用选项。**ls** 命令也不例外。通过组合这些选项，你可以同时启用多个功能。例如，将 `-a` 选项与 `-l` 组合会产生一个详细的文件列表，其中包含隐藏文件（以点开头的文件）。

```
$ ls -l -a
drwxr-xr-x  2 nick sales  4096 2009-05-19 21:14 .
drwxr-xr-x 92 nick sales  4096 2009-05-19 20:46 ..
-rw-r--r--  1 nick sales   168 2009-05-19 21:14 .MyHiddenFile
-rw-r--r--  1 nick sales 35068 2009-05-19 08:41 Notes.txt
-rw-r--r--  1 nick sales   23 2009-05-19 08:43 ShoppingList.txt
-rw-r--r--  1 nick sales   37 2009-05-19 08:43 ToDoList.txt
```

*使用多个选项运行 ls 命令*

> **提示** 大多数命令行选项都可以使用简写符号组合。例如，`ls -l -a` 可以简写为 `ls -la`。

> **注意** 命令行选项并非通用。每个命令都有其特定的选项集，仅适用于该程序。此外，同一命令在不同平台上的不同实现可能使用不同的选项。请查阅手册页以获取你的系统支持的完整命令行选项列表。

**常见用法示例：**

- `ls` 显示当前目录中文件的基本列表
- `ls [目录]` 显示指定目录中文件的基本列表
- `ls -l` 带详细信息列出文件
- `ls -la` 列出隐藏文件
- `ls -lh` 以“人类可读格式”（KB、MB 等）列出文件大小
- `ls -R` 递归列出所有子目录
- `ls -d [目录]` 仅列出指定目录（不列出其内容）

## pwd

**用途**：显示当前/工作目录。

**使用语法**：`pwd`

```
$ pwd
/home/nick
```

*使用 pwd 命令显示当前目录*

`pwd` 命令（**Print Working Directory**，即打印工作目录的缩写）显示你在文件系统当前所在的位置。在上述示例中，执行 `pwd` 会显示 `/home/nick` 作为当前工作目录。

> **注意**
> *Unix、Linux 和 BSD 系统使用正斜杠（即 /home/nick）来分隔目录名称，而 MS-DOS 和 Windows 系统使用反斜杠（即 C:\Windows\system32）。*

**常见用法示例：**

- `pwd` | 显示当前工作目录。

## cd

**用途**：更改（导航）目录。

**使用语法**：`cd [目录]`

```
$ cd /etc
$ pwd
/etc
```

*使用 cd 命令导航到 /etc 目录*

**cd** 命令（**Change Directories**，即更改目录的缩写）将你在文件系统中的位置更改为指定路径。在上述示例中，执行 **cd /etc** 会将 `/etc` 设为新的工作目录。

除非你手动指定完整路径（例如第一个示例中使用的 **cd /etc**），否则 **cd** 命令会根据你当前的位置解释目录路径。下一个示例演示了如何使用 **cd** 根据当前位置更改目录。

```
$ pwd
/home/nick
$ cd documents
$ pwd
/home/nick/documents
```

*使用 cd 命令导航到相对于当前位置的目录*

在此示例中，起始目录是 `/home/nick`。输入 **cd documents** 会将 `/home/nick/documents` 设为新的工作目录。如果你从其他位置开始，则需要输入完整路径（即 **cd /home/nick/documents**）才能达到相同结果。由于之前的位置是 `/home/nick`，因此不需要输入完整路径。

> **提示** 不带任何选项执行 **cd** 命令会无论你当前位于何处，都带你回到主目录。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `cd [目录]` | 导航到指定目录 |
| `cd` | 导航到用户的主目录 |
| `cd -` | 返回到前一个工作目录 |
| `cd .` | 在目录树中向上导航一级 |

## tree

**用途**：以树状层次结构格式显示目录内容。

**使用语法**：`tree [选项] [目录]`

```
$ cd /
$ tree -d -L 2
.
|-- bin
|-- boot
|   `-- grub
|-- cdrom -> media/cdrom
|-- dev
|   |-- block
|   |-- bus
|   |-- char
|   |-- disk
|   |-- fd -> /proc/self/fd
|   `-- input
|..
|-- etc
|   |-- ConsoleKit
|   |-- NetworkManager
|   |-- PolicyKit
|   |-- X11
|   |-- acpi
|   |-- alsa
|   `-- alternatives
|..
```

*目录结构的树状列表*

**tree** 命令以树状形式显示目录列表。这对于可视化目录结构的布局非常有用。在上述示例中，执行 **tree -d -L 2** 会以树状形式显示 2 个目录级别（相对于当前位置）。

**常见用法示例：**

- `tree` ：以树状形式显示当前目录的内容
- `tree [目录]` ：以树状形式显示指定目录的内容
- `tree -a` ：在树状列表中包含隐藏文件
- `tree -d` ：仅列出目录
- `tree -L [数字]` ：列出指定层级的深度

