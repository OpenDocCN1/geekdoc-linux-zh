
### 3.3.2.2 工具

#### 3.3.2.2.1 创建目录

整理事物的一种方法是通过创建目录和子目录（如果你愿意也可以说是文件夹和子文件夹）来为特定文件指定默认位置。这是通过 `mkdir` 命令完成的：

```
richard:-> mkdir archive

richard:-> ls -ld archive
drwxrwxrwx 2 richard richard         4096 Jan 13 14:09 archive/
```

使用 `-p` 选项可以在一步中创建目录和子目录：

```
richard:-> cd archive

richard:~/archive> mkdir 1999 2000 2001

richard:~/archive> ls
1999/   2000/   2001/

richard:~/archive> mkdir 2001/reports/Restaurants-Michelin/
mkdir: cannot create directory '2001/reports/Restaurants-Michelin/':
No such file or directory

richard:~/archive> mkdir -p 2001/reports/Restaurants-Michelin/

richard:~/archive> ls 2001/reports/
Restaurants-Michelin/
```

如果新文件需要不同于默认文件创建权限的权限，仍可使用 `mkdir` 命令一步设置新的访问权限，更多信息请参见 Info 页面。我们将在下一节关于文件安全的部分中讨论访问模式。

目录名称必须遵循与普通文件名称相同规则。最重要的限制之一是，你不能在一个目录中拥有两个同名文件（但要记住，Linux 和 UNIX 一样，是一个区分大小写的操作系统）。文件名长度实际上没有太大限制，但通常保持在 80 个字符以内，以便能显示在终端的一行内。你可以在文件名中使用任何字符，但建议你排除对 shell 有特殊含义的字符。如有疑问，请查阅附录 C。

#### 3.3.2.2.2 移动文件

现在我们已经适当地结构化主目录，是时候使用 `mv` 命令清理未分类的文件了：

```
richard:~/archive> mv ../report[1-4].doc reports/Restaurants-Michelin/
```

此命令也适用于重命名文件：

```
richard:-> ls To_Do
-rw-rw-rw--   1 richard richard    2534 Jan 15 12:39 To_Do

richard:-> mv To_Do done

richard:-> ls -l done
-rw-rw-rw--   1 richard richard    2534 Jan 15 12:39 done
```

显然，只有文件名发生了改变。所有其他属性保持不变。

有关 `mv` 命令语法和功能的详细信息可在 `man` 或 Info 页面中找到。当你遇到问题时，首先应当查阅这些文档。你问题的答案在于这很可能包含在系统文档中。即使是经验丰富的用户也会每天阅读 `man` 手册页，因此初学者也应该经常阅读。一段时间后，你会熟悉常用命令中最常见的选项，但你仍需要文档作为主要信息源。请注意，HOWTO、FAQ、`man` 手册页等中包含的信息正在缓慢合并到 Info 页面中，这些页面如今是最新的在线（即系统中随时可获取的）文档来源。

#### 3.3.2.2.3 复制文件

使用 `cp` 命令来复制文件和目录。一个有用的选项是递归复制（复制所有底层文件和子目录），使用 `cp` 的 `-R` 选项。一般语法是

```
cp [-R] fromfile tofile
```

例如，假设用户 `newguy` 希望拥有与用户 `oldguy` 相同的 Gnome 桌面设置。解决此问题的一种方法是将 `oldguy` 的设置复制到 `newguy` 的主目录中：

```
victor:~> cp -R ../oldguy/.gnome/ .
```

这会产生一些涉及文件权限的错误，但所有错误都与 `newguy` 本来就不需要的私人文件有关。我们将在下一部分讨论如果这些权限确实有问题，如何更改它们。

#### 3.3.2.2.4 删除文件

使用 `rm` 命令删除单个文件，使用 `rmdir` 删除空目录。（使用 `ls -a` 检查目录是否为空）。`rm` 命令还有选项可以删除包含所有子目录的非空目录，对于这些相对危险的选项，请阅读 Info 页面。

##### 目录可以有多空？

目录 `.`（点）和 `..`（双点）无法删除是正常的，因为即使在空目录中，它们对于确定文件系统层次结构中的目录排名也是必需的。

在 Linux 上，就像在 UNIX 上一样，没有垃圾箱——至少对于 shell 来说是这样，尽管针对图形化使用有很多解决方案。因此，一旦文件被删除，它真的就消失了，除非你有备份，或者你速度非常快并且拥有真正优秀的系统管理员，否则通常没有方法找回它。为了保护初学者免受此危害，可以使用 `-i` 选项激活 `rm`、`cp` 和 `mv` 命令的交互式行为。在这种情况下，系统不会立即执行请求。相反，它会要求确认，因此需要额外点击一次 Enter 键才能造成损害：

```
marv:~> rm -ri archive/
rm: descend into directory `archive'? y
rm: descend into directory `archive/reports'? y
rm: remove directory `archive/reports'? y
rm: descend into directory `archive/backup'? y
rm: remove `archive/backup/sysbackup200112.tar'? y
rm: remove directory `archive/backup'? y
rm: remove directory `archive'? y
```

我们将在第 7 章中讨论如何将此选项设置为默认值，该章节讨论了自定义你的 shell 环境。

### 3.3.3 查找文件

#### 3.3.3.1 使用 shell 功能

在移动文件的示例中，我们已经看到 shell 如何同时操作多个文件。在那个示例中，shell 会自动确定方括号之间的需求意味着什么。Shell 可以替换数字范围以及大写或小写字符。它还可以使用星号替换任意数量的字符，使用问号替换单个字符。

各种替换可以同时使用；shell 在这方面非常合乎逻辑。例如，Bash shell 在处理像 `ls dirnameo/*/ * [2-3]` 这样的表达式时没有问题。

在其他 shell 中，星号通常用于减少打字工作：人们会输入 `cd dir*` 而不是 `cd directory`。然而，在 Bash 中，这是不必要的，因为 `GNU` shell 有一个称为`文件名补全`的功能。这意味着你可以输入命令的前几个字符（在任何地方）或文件（在当前目录中），如果不产生歧义，shell 会自动确定你的意图。例如，在一个包含许多文件的目录中，你只需输入 `ls a` 并按两次 `Tab` 键（而不是 `Enter` 键），即可检查是否有以字母 A 开头的文件。如果只有一个以"A"开头的文件，该文件会立即显示为 `ls`（或任何 shell 命令）的参数。

#### 3.3.3.2 which

查找文件的一种非常简单的方法是使用 `which` 命令，在用户搜索路径中列出的目录中查找所需文件。当然，由于搜索路径仅包含含有可执行程序的目录路径，`which` 不适用于普通文件。`which` 命令在排查"命令未找到"问题时很有用。在下面的示例中，用户 `tina` 无法使用 `acroread` 程序，而她的同事在同一系统上没有任何问题。这个问题与前面部分的 `PATH` 问题类似：Tina 的同事告诉她，他可以在 `/opt/acroread/bin` 中看到所需程序，但该目录不在她的路径中：

```bash
tina:~> which acroread
/usr/bin/which: no acroread in (/bin:/usr/bin:/usr/bin/X11)
```

可以通过提供命令的完整路径，或通过重新导出 `PATH` 变量的内容来解决此问题：

```bash
tina:~> export PATH=$PATH:/opt/acroread/bin

tina:~> echo $PATH
/bin:/usr/bin:/usr/bin/X11:/opt/acroread/bin
```

使用 `which` 命令还可以检查某个命令是否是另一个命令的别名：

```bash
gerrit:~> which -a ls
ls is aliased to `ls -F --color=auto`
ls is /bin/ls
```

#### 3.3.3.3 find 和 locate
