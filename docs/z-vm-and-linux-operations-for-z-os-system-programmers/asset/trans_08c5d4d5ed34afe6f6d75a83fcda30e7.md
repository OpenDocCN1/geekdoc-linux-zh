

IBMUSER 在 z/OS 中更加强大，因为 root 默认可以访问所有内容。Root 访问权限无法被限制。

## 3.2.2 基本入门步骤

本节讨论基本命令，例如在目录中导航、查看目录或文件的内容以及创建目录。

**重要：** Linux 命令和文件名区分大小写。例如，命令 `chmod` 不能输入为 `Chmod` 或 `CHMOD`。

**提示：** 在开始输入命令或文件名后按 Tab 键可以补全剩余的命令或文件名。此外，按 Ctrl+R 可以搜索所有先前发出的命令。

## 获取 Linux 命令的帮助

Linux 没有像 z/VM 和 z/OS 那样的帮助菜单。相反，Linux 有一个名为 man 的命令，它会显示来自在线参考手册的命令页面。该页面包括：名称、使用的概要、命令功能的描述以及其他详细信息。要使用该命令，输入：

```
man commandname
```

commandname 是你想要获取帮助的命令的名称（参见示例 3-1）。

**注意：** 你必须知道要使用的命令的名称才能访问其手册页。

要滚动浏览文件，请使用上下箭头。要退出文件请按 Q。

*示例 3-1 对 man 命令本身使用 man 命令*

```
lnxken:/ # man man
NAME
    man - an interface to the on-line reference manuals

SYNOPSIS
man [-c|-w|-tZHT device] [-adhu7V] [-i|-I] [-m
system[...]] [-L
locale] [-p string] [-M path] [-P pager] [-r prompt] [-S
list] [-e
extension] [[section] page ...] ...
```

```
man -l [-7] [-tZHT device] [-p string] [-P pager] [-r prompt]
file ...
man -k [apropos options] regexp ...
man -f [whatis options] page ...
```

## DESCRIPTION

man 是系统的手册分页器。传递给 man 的每个 page 参数通常是程序、实用程序或函数的名称。然后找到并显示与每个参数关联的手册页。如果提供了 section，man 将只在手册的该部分中查找。默认操作是在所有可用部分中按预定义顺序搜索，并仅显示找到的第一个页面，即使该页面存在于多个部分中。

下表显示了手册的章节编号及其包含的页面类型。

| Section | Description |
|---|---|
| 0 | 头文件（通常位于 /usr/include） |
| 1 | 可执行程序或 shell 命令 |
| 2 | 系统调用（内核提供的函数） |
| 3 | 库调用（程序库中的函数） |
| 4 | 特殊文件（通常位于 /dev） |
| 5 | 文件格式和约定 例如 /etc/passwd |
| 6 | 游戏 |
| 7 | 杂项（包括宏包和约定），例如 man(7)、groff(7) |
| 8 | 系统管理命令（通常仅 root 可用） |
| 9 | 内核例程 [非标准] |

手册页由几个部分组成。

它们可能标记为 NAME、SYNOPSIS、DESCRIPTION、OPTIONS、FILES、SEE ALSO、BUGS 和 AUTHOR。

## 在文件系统中导航

从一个目录更改到另一个目录的命令是 cd（change directory 的缩写）。命令的正确用法是：

```
cd directoryname
```

directoryname 是要访问的目录的名称（参见第 104 页的示例 3-2）。

## 示例 3-2 cd（change directory）命令

```
lnxken:~^ # cd Desktop/
lnxken:~/Desktop #
```

使用 cd 命令时你有几个选项：

- cd ..    这会将你向上移动一级目录树（参见示例 3-3）。
- cd /    这会将你带到文件系统目录的根，无论你当前在哪个目录中（参见示例 3-4）。
- cd -    这会将你返回到之前所在的目录（参见示例 3-5）。

## 示例 3-3 更改到父目录：cd ..

```
lnxken:/etc/init.d/rc3.d # cd ..
lnxken:/etc/init.d #
```

## 示例 3-4 更改到文件系统目录的根：cd /

```
lnxken:/etc/init.d/rc3.d # cd /
lnxken:/ #
```

## 示例 3-5 更改到上一个目录：cd -

```
lnxken:/ # cd -
/etc/init.d/rc3.d
lnxken:/etc/init.d/rc3.d #
```

## 显示目录的内容

现在你可以在一个目录和另一个目录之间切换，你希望能够查看目录的内容。为此，使用 ls 命令。

- 要列出当前目录的内容，请使用不带选项的 ls 命令。
- 要列出另一个目录的内容，输入带选项的 ls 命令：
- ls directoryname

directoryname 是你想要查看内容的目录的名称。参见示例 3-6。

## 示例 3-6 列出当前目录内容

```
lnxken:/ # ls
bin  dev  home  lib64  media  opt  root  srv  tmp  var
boot  etc  lib  lost+found  mnt  proc  sbin  sys  usr
```
