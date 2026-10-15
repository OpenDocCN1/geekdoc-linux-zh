
也有其独特的布局，例如处理设备驱动程序的 9E、9F 和 9S 节，以及完全没有第 6 节（游戏）。在任何 Unix 系统上，命令 man man（明白吗？手册的手册）都会给你完整的概要。

| 章节 | 类别 |
|---|---|
| 1 | 用户命令 |
| 1M | 系统维护命令 |
| 2 | 系统调用 |
| 3 | 库例程 |
| 4 | 管理文件 |
| 5 | 杂项 |
| 6 | 游戏 |
| 7 | I/O 和特殊文件 |
| 8 | 管理命令 |

## 表 1.1 System V Unix 手册页组织

不同章节中的手册页可能具有相同的名称，因此您可能需要指定在哪个章节中查找页面。此外，有时您要查找用户级命令，却会在第 2 节或第 3 节中找到匹配项。这些并不是您要找的；它们是专门面向 Unix 程序员的，从表中可以看到。

- 1. mkdir 手册页简洁而典型。当您输入 man mkdir 命令时，您将看到以下内容：

点击此处查看代码图像

```
% man mkdir

MKDIR(1)                 FreeBSD General Commands Manual
Manual                   MKDIR(1)

NAME
    mkdir - make directories

SYNOPSIS
    mkdir [-p] [-m mode] directory_name ...

DESCRIPTION
    Mkdir creates the directories named as operands, in the order specified, using mode rwxrwxrwx (0777) as modified by the current umask(2).

    The options are as follows:

    -m   Set the file permission bits of the final created directory to the specified mode. The mode argument can be in any of the formats specified to the chmod(1) command. If a symbolic mode is specified, the operation characters "+" and "-" are interpreted relative to an initial mode of "a=rwx".
```

-p 按需创建中间目录。如果未指定此选项，则每个操作数的完整路径前缀必须已存在。中间目录以 rwxrwxrwx (0777) 的权限位创建，该权限位由当前 umask 修改，并额外授予所有者写权限和搜索权限。

用户必须对父目录具有写权限。

## 诊断信息

mkdir 实用程序成功时退出 0，出错时退出大于 0。

## 另请参阅

rmdir(1)

## 标准

mkdir 实用程序预期与 IEEE Std1003.2（“POSIX.2”）兼容。

## 历史

mkdir 命令出现在 AT&T UNIX 第 1 版中。

## 注意

注意在示例中，第一行中命令本身是粗体，但其他内容不是粗体。在本书中，只要示例包含用户输入和 Unix 输出，用户输入就用粗体显示，以便您轻松识别需要输入的内容。

输出的第一行告诉我，它在手册页的第 1 节（用户命令）中找到了 mkdir 命令，中间的短语 FreeBSD General Commands Manual 表明我正在运行名为 FreeBSD 的 Unix 版本。NAME 部分总是详细说明命令名称及其作用的一行摘要。SYNOPSIS 解释了如何使用该命令，包括所有可能的命令标志和选项。

DESCRIPTION 才是所有有意义信息的所在，它可能长达数十页，解释 csh 或 vi 等复杂命令的工作方式。SEE ALSO 提供了一些以某种方式相关的其他命令。底部的 Revision 行在每个版本的手册页中都有所不同，它大概表示该文档最近一次修订的时间。

2. 来自 Oracle Solaris 工作站的同一手册页则完全不同，如图 1.1 所示。

## 用户命令

mkdir(1)

## 名称

mkdir - 创建目录

## 语法

```
/usr/bin/mkdir [-m mode] [-p] dir...
```

## 描述

mkdir 命令以模式 777 创建指定目录（可能受文件模式创建掩码 umask(1) 的影响）。

目录中的标准条目（例如，表示目录本身的文件“.”和表示其父目录的“..”）是自动创建的。mkdir 不能按名称创建这些条目。创建目录需要对父目录具有写权限。

新目录的所有者 ID 和组 ID 分别设置为进程的有效用户 ID 和组 ID。mkdir 调用 mkdir(2) 系统调用。

## setgid 与 mkdir

要更改新创建目录上的 setgid 位，您必须在执行 mkdir 后使用 chmod g+s 或 chmod g-s。

setgid 位设置继承自父目录。

## 选项

支持以下选项：

- -m mode  此选项允许用户指定用于新目录的模式。模式的选择可参见 chmod(1)。

- -p  使用此选项时，mkdir 会先创建所有不存在的父目录，从而创建 dir 目录。赋予中间目录的模式是 777 与文件模式创建掩码中的位之间的差值。该差值必须至少为 300（用户的写权限和执行权限）。

## 操作数

支持以下操作数：

# 图 1.1 Oracle Solaris 系统上的 mkdir 手册页

3. 不确定具体命令？这时 man -k 或其别名 apropos 就派上用场了：

点击此处查看代码图像

```
% man -k date | head -18
1. date(1) /usr/share/man/man1/date.1
date - write the date and time
```

