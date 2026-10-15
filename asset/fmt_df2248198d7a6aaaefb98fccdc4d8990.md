
在这里，`man` 是你想查找的命令名称。它是基于超文本的，因此你可以通过超文本链接浏览文档。要查看命令的完整列表，在命令行提示符处输入 `info`。某些屏幕会显示更多可用选项。按 `m` 然后输入菜单名称将你带到另一个名为 `node` 的页面。节点是文本中的超链接，提供了一个某种交互式的帮助系统。

按 `n` 键将到下一个节点，按 `p` 键返回上一个屏幕。在文档中使用这种导航不仅可以帮助你找到要找的内容，还可以引导你找到最有用的信息。

> 文档在 `man` 页和 `info` 页中是相同的。其他文档会以 `info` 的形式详细详细存在，而 `man` 页将引用 `info` 文档。某些情况下，你可能会从两个源发现略有不同的信息，因为文档的作者不是同一个。

### 在文件之间穿行

对于大多数人来说，最大的困难是在所有文件之间穿梭——记住你去过哪里以及知道你想去哪里。你可以通过几个简单的命令轻松学会这种技能。以下命令并不是一个完整的集合。然而，掌握基础集合可以帮助你处理更高级的命令。

### ls

列表命令 (`ls`) 显示目录的内容。单独执行 `ls` 命令会显示当前目录的内容。加上 `ls` 路径会显示你指定的路径的内容。其语法如下：

```
ls [option] [path]
```

这里是 `ls` 的示例：

```
$ ls
Mail misc smb.conf util.doc
util.txt
Xrootenv.0 mbox public_html tmp util.list
$
```

如你所示，这些文件按列列出。优先级从数字开始，接着是大写字母，然后是小写字母。该命令还有几个实用的选项可以以各种形式显示内容。表 3-3 显示了最有用的选项。

| 表 3-3 常用的 ls 选项 |

| 选项 (Option) | 描述 (Description) |

| --- | --- |

| -a, --all | 列出给定目录中的所有文件，包括隐藏文件 |

| -l | 以长格式列出文件信息，显示文件的所有信息 |

| -F | 通过在文件名末尾添加指示类型的字符进行分类 |

| * | 普通可执行文件 |

| / | 目录 |

| @ |符号链接（类似于 MS Windows 中的快捷方式） |

|    | 普通文件 |

| -R | 递归列出所有目录的内容 |

# 第 3 章 作为 Linux 用户的第一步

这些选项为检索目录中文件的最有用信息提供了至关重要的部分。除了使用选项外，你还可以结合其他选项使用以获取更完整的信息。这里是结合其他选项的一个示例：

```
$ ls -al
drwxr-xr-x  2 root root 4096 Jan  1 00:00 .
drwxr-xr-x 20 root root 4096 Jan  1 00:00 ..
-rw-r--r--  1 user user     0 Jan  1 00:00 Mail
-rw-r--r--  1 user user     0 Jan  1 00:00 misc
-rw-r--r--  1 user user 4096 Jan  1 00:00 smb.conf
-rw-r--r--  1 user user     0 Jan  1 00:00 util.doc
-rw-r--r--  1 user user     0 Jan  1 00:00 util.txt
-drwxr-xr-x  1 root root 4096 Jan  1 00:00 Xrootenv.0
-rw-r--r--  1 user user     0 Jan  1 00:00 mbox
-drwxr-xr-x  2 root root 4096 Jan  1 00:00 public_html
-drwxr-xr-x  2 root root 4096 Jan  1 00:00 tmp
-rw-r--r--  1 user user     0 Jan  1 00:00 util.list
```

这些选项为检索目录中文件的最有用信息提供了至关重要的部分。除了使用选项外，你还可以结合其他选项使用以获取更完整的信息。这里是结合其他选项的一个示例：

```
$ ls -al
total 24
drwxr-xr-x  2 root root 4096 Jan  1 00:00 .
drwxr-xr-x 20 root root 4096 Jan  1 00:00 ..
-rw-r--r--  1 user user     0 Jan  1 00:00 Mail
-rw-r--r--  1 user user     0 Jan  1 00:00 misc
-rw-r--r--  1 user user 4096 Jan  1 00:00 smb.conf
-rw-r--r--  1 user user     0 Jan  1 00:00 util.doc
-rw-r--r--  1 user user     0 Jan  1 00:00 util.txt
-drwxr-xr-x  1 root root 4096 Jan  1 00:00 Xrootenv.0
-rw-r--r--  1 user user     0 Jan  1 00:00 mbox
-drwxr-xr-x  2 root root 4096 Jan  1 00:00 public_html
-drwxr-xr-x  2 root root 4096 Jan  1 00:00 tmp
-rw-r--r--  1 user user     0 Jan  1 00:00 util.list
```

### 第一部分 入门

当你开始更多地使用 `ls` 时，可能会遇到各种查看列表的理由。在表 3-4 中，你看到了通配符及其用途。

| 表 3-4 ls 命令的通配符 |

| --- | --- |

| 字符 | 替换 |

| * | 零或多个字符 |

| [] | 括号内的任何字符（包括） |

| ? | 任意单个字符 |

## 第 3 章：Linux 用户的第一步

这条 `ls Fig13-[2-5].tif` 向列表中又添加了两个文件。现在，假设你正在寻找一系列文件。

```
$ ls Fig13-[2-5].tif Fig13-0.tif Fig13-0.tif Fig13-4.tif Fig13-5.tif
```

同样，这个版本生成了目录内容的子集，其中包含特定类别的一范围文件。当你开始使用这些命令选项时，我确定你会发现它们像我一样好用。

## cd

这个切换目录命令（`cd`）允许在文件系统中进行导航，并让你能够切换到某个目录进行近距离查看。为了更好地了解文件结构，请直接跳到文件系统章节。以下是该命令的语法：

```
cd [directorypath]
```

在不带任何选项的情况下执行 `cd` 命令，可以让你从任何地方回到用户主目录。

`directorypath` 是你想要切换的路径。例如，如果你当前的路径是 `/home/jo`，执行

```
$ cd /tmp
```

将将当前的可视图更改到 `tmp` 目录。

要前往完全不同的地方，只需指定完整路径。例如，

```
$ cd /usr/bin
```

这将你从当前目录传输到 `usr` 目录下一个名为 `bin` 的另一个目录。同样，如果你迷路了或想快速返回主目录，使用

```
$ cd
```

将带你从任何地方带回默认账户目录。下一个命令 `pwd` 将帮助你在在目录结构导航时保持方向。

通过一些练习，切换目录将变成你的本能。

## pwd

一旦你开始习惯在目录间移动，你就可能会迷路。“我在哪儿？”这个问题可能会掠过你的脑海。一个简单的命令就能显示当前路径——`pwd`。使用这个命令帮助找到你所在的目录路径。使用 `pwd` 的结果如下：

```
## pwd
home/jo/tmp
```

## mkdir

这个创建目录命令（`mkdir`）在文件系统上创建一个目录。当你开始组织一组文件时，这变得非常重要。使用 `mkdir dirname` 在当前目录位置创建一个名为 `dirname` 的目录。以下是语法：

```
mkdir [option] dirname
```

你可以使用 `-p` 选项一次创建目录链。该选项会创建目录以及所有不存在的父目录。例如，假设你想在 `files` 目录内部创建一个名为 `new` 的目录。在这种情况下，`files` 是 `new` 的父目录。这两个目录目前都不存在。你可以这样输入：

```
$ mkdir -p ./files/new
```

该命令的结果是：

```
$ ls -R files
total 3
drwxr-xr-x 3 root      1024 Jun 8 15:16
drwxr-xr-x 10 users    1024 Jun 8 15:16
drwxr-xr-x 2 steve    1024 Jun 8 15:16

files/new:
total 2
drwxr-xr-x 2 users    1024 Jun 8 15:16
drwxr-xr-x 3 steve    1024 Jun 8 15:16
$
```
