
4. 在命令提示符处，输入 `man 5 cron` 并按回车，查看 crontab 文件格式的帮助页。观察 crontab 文件格式的语法，完成后按 `q` 退出帮助页并返回命令提示符。

5. 在命令提示符处，输入 `info` 并按回车，查看可用的 GNU info 页列表。完成后，按 `q` 退出 info 工具。

6. 在命令提示符处，输入 `info date` 并按回车，查看关于 `date` 命令的语法信息，完成后按 `q` 退出 info 工具。

7. 在命令提示符处，输入 `help` 查看所有带有文档的 BASH shell 函数列表。由于列表过长终端无法完全显示，请同时按下 Shift 和 Page Up 键向上滚动一页以查看列表顶部。然后同时按下 Shift 和 Page Down 键向下滚动一页直到回到命令提示符。

8. 在命令提示符处，输入 `help exit` 查看 `exit` 命令的信息，它是你 BASH shell 的一个函数。

9. 在命令提示符处，输入 `shutdown -h now` 立即停止系统。表 3–6 中的哪一个命令与 `shutdown` 具有相同的功能？

## 探索练习

1. 你是 Slimjim 一家外设公司的网络管理员。你们使用的网络运行 Linux，你需要一些命令信息来完成工作。打开帮助页，找到所有名称或描述中包含 "copy" 字字的命令。你使用了什么命令来完成此任务？列表中是否存在只有 root 用户才能执行的命令？它们是如何指示的？选择其中任意两个，并比较它们的 info 和手动页。通过命令名或使用相关关键词搜索（尝试使用 `apropos`），访问并阅读另外三个你感兴趣的命令帮助页。

2. 识别以下命令中的错误并指出可能的解决方案。（提示：尝试在 shell 提示符下输入它们以查看错误消息。）

```
echo "This command does not work properly"
date -z
apropos man -k
help date
finger route
shutdown -c now
echo "I would like lots of $$$"
man 8 date
```

# 第 4 章

# 探索 Linux 文件系统

完成本章后，你将能够：

- 使用相对路径和绝对路径理解并导航 Linux 目录结构
- 描述各种类型的 Linux 文件
- 查看文件名和文件类型
- 使用 shell 通配符指定多个文件名
- 显示文本文件和二进制文件的内容
- 使用 `grep` 使用正则表达式对文本文件进行搜索
- 识别今日常用的文本编辑器
- 使用 `vi` 编辑器处理文本文件

理解 Linux 文件系统的结构及其相关命令对于有效使用 Linux 处理数据至关重要。在本章的第一部分，你将通过改变文件系统树中的位置并列出各种类型的文件名来探索 Linux 文件系统层次结构。接下来，你将检查用于通过标准 Linux 命令指定多个文件名的 shell 通配符元字符以及文件内容。然后，你将学习在文件中搜索文本时使用的正则表达式元字符，并结识 `vi` 文本编辑器及其等效工具。

## Linux 目录结构

使用 Linux 操作系统的基础是理解 Linux 如何在硬盘上存储文件。典型的 Linux 系统硬盘上可能有数千个数据文件和程序文件；因此，需要一个组织这些文件的结构以便于查找、处理数据以及运行程序。回顾上一章，Linux 使用逻辑目录将文件组织到不同的目录（也称为文件夹）。当用户在特定目录中存储文件时，它们在物理上存储在计算机硬盘内特定分区的文件系统中。大多数人熟悉图 4-1 所示的 Windows 操作系统目录树结构；硬盘分区上的每个文件系统都由驱动器字母（如 `C:` 或 `D:\`）引用，并有一个根目录（由 `\` 字符表示），其中包含子目录，这些子目录共同构成了一个层次树。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_145_0.png)

**图 4-1** Windows 文件系统结构

正确描述目录树中的目录是非常重要的；文件或目录的绝对路径是从根目录开始的特定文件或目录的完整路径。从图 4-1 可以看出，`color` 目录的绝对路径是 `C:\windows\color`，`sue` 目录的绝对路径是 `D:\home\sue`。Linux 使用简单的目录结构；但没有驱动器字母。它有一个根（由 `/` 字符表示），硬盘分区上的不同文件系统被挂载到不同的目录。图 4-2 展示了相当于图 4-1 中 Windows 树的 Linux 目录树示例。

## Linux 目录结构

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_146_0.png)

**图 4-2** Linux 文件系统结构

## 切换目录

当用户登录系统时，他会被放置在**家目录**（home directory），这是每个用户用于存储个人文件的唯一位置。普通用户通常在 `/home` 目录下有一个与其用户账户同名的家目录，例如 `/home/sue`。然而，`root` 用户在系统根目录（root）下有一个名为 `root` 的家目录，如图 42 所示。你可以通过观察 shell 提示符末尾的名称或在命令行提示符处输入 `pwd`（打印工作目录）命令并按回车来确认你当前所在的系统目录。如果你以 `root` 用户身份登录，终端屏幕将显示以下输出：

```
[root@server1 root]#pwd
/root
[root@server1 root]# _
```

然而，如果你以用户 `sue` 的身份登录，你会看到如下输出：

```
[sue@server1 sue]$pwd
/home/sue
[sue@server1 sue]$ _
```

要切换目录，你可以发出 `cd`（切换目录）命令并指定目标目录作为参数。如果你没有指定目标目录，`cd` 命令将直接返回你的家目录：

```
[root@server1 root]# cd /home/mary
[root@server1 mary]# pwd
/home/mary
[root@server1 mary]# cd /etc
[root@server1 etc]#pwd
/etc
[root@server1 etc]# cd
[root@server1 root]#pwd
/root
[root@server1 root]# _
```

## 126 第 4 章 探索 Linux 文件系统

`~` 元字符也可以用于指向当前用户的家目录。或者，你也可以通过在 `~` 元字符的末尾添加用户名来指定另一个用户的家目录：

```
[root@server1 root]# cd ~mary
[root@server1 mary]# pwd
/home/mary
[root@server1 mary]# cd ~
[root@server1 root]# pwd
/root
[root@server1 root]# _
```

在之前讨论的许多示例中，`cd` 命令之后指定的参数是目录的绝对路径，这意味着系统拥有找到目标目录所需的所有信息，因为路径是从系统的根目录（`/`）开始的。然而，在大多数 Linux 命令中，你也可以使用相对路径代替绝对路径。相对路径是相对于你当前位置的目标文件或目录的路径。要指定当前目录下的子目录，只需通过名称引用该目录（不要以字符开头路径）。要引用更接近树树根目录的目录（也称为父目录），只需使用两个点（`..`）。使用路径在目录树中移动的示例是：

```
[root@server1 root]# cd /home/mary
[root@server1 mary]# pwd
/home/mary
[root@server1 mary]# cd ..
[root@server1 root]# pwd
/home
```

在前面的示例中，我们使用“`..`”移动到上父目录，然后使用单词“mary”指定相对于我们当前位置的子目录；然而，你也可以在目录树中向上或向下移动：

```
[root@server1 root]# cd /home/mary
[root@server1 mary]# pwd
/home/mary
[root@server1 mary]# cd ../
[root@server1 root]# pwd
/home
```

```
[root@server1 root]# cd mary
[root@server1 mary]# pwd
/home/mary
[root@server1 mary]# ..
[root@server1 root]# pwd
/home
```

你也可以使用一个点（`.`）来引用当前目录。虽然这在使用 `cd` 命令时并不好用，但在本书中你会用到一个点。
