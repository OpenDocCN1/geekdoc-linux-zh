

-   `-i, -u, -idle`
    将用户空闲时间作为小时:分钟，或以 old 形式显示
-   `-l, -lookup`
    尝试通过 DNS 规范化主机名
-   `-m`
    仅显示与标准输入关联的主机名和用户
-   `-g, -count`
    显示所有登录名以及已登录用户的数量
-   （等等）

“Synopsis”（概要）部分中的代码使用以下排版约定。

可选字段显示在方括号中，[ 和 ]。它们表示你无需输入某个选项或参数。如果存在强制字段，它们将显示在花括号中：{ 和 }。如果存在强制字段，则你必须在命令名称后为该对应的选项或参数输入一个值。当看到管道符 ( | ) 分隔两个强制选项或参数时，则你必须输入其中一个来配合命令使用。不过，对于 who 命令而言，尽管参数由管道符分隔，但它们都是可选的。因此，除非你选择提供参数，否则无需提供任何内容。

你可能会注意到 who 的手册页中包含 FILE 选项。当用户登录时，其登录记录会保存在文件 /var/run/utmp 中。默认情况下，who 命令会在此处查找信息。如果系统管理员已配置系统使用其他文件来记录登录信息，则你必须在 who 命令后指定该文件名。

## info 页面

info 页面使用与 man 相同的数据库，但以不同的格式呈现信息。有些人认为 info 功能更强大，因为它允许你将信息分解为更小的块进行检查，并显示你所搜索的信息与其他相关信息之间的关系。

info 的另一个重要特性，尤其对于新用户而言，是它会在第一个屏幕上提供自身的操作说明，并允许你在调用 info 后立即进入入门指导。这种引导式方法大大提高了搜索成功的可能性。

其语法再简单不过了：

```
$ info<Enter>
```

调用该命令后，会出现第一个基于 ASCII 字符的 *info* 屏幕，并声明你位于 *info* 目录树的顶部。随后是基本说明，以及启动 *info* 入门指导的机会。

如果你不需要入门指导，请按下 Tab 键或上、下箭头键，在可用的众多用户命令、系统调用、子例程、设备、文件格式、游戏、系统管理功能等之间移动。示例 3.5 列出了基本类别，但未列出你可以从此屏幕访问的所有功能。当你选择一个类别后，按下 Enter 键。随后会显示一个包含你所选信息内容的屏幕。

然而，当用户退出 *info* 后，并没有类似 *fg*（我们在 *man* 中使用过的）那样的命令可以将用户返回到他们离开 *info* 时的位置。他们必须从头开始重新进入，并再次执行整个流程。

用户还可以从 *xterm* 窗口调用 *info*，并且可以从 X Window 系统桌面调用其他类似 *info* 或 *man* 的程序。这些程序的名称和类型因每个 X 窗口管理器而异。例如，从 KDE 中，你可以调用 KDE Help。KDE Help 允许你使用鼠标通过超链接进行导航，而不是我们用来通过面向 ASCII 的 *info* 页面的键盘导航。有关 X Window 系统和 X 窗口管理器的更多信息，请参阅第 14 章，“Linux X Window 系统”。

> **注意** 请检查本章提到的所有命令的 *man* 页面及其他信息源中的选项和参数。

### 示例 3.5 使用 *info* 获取命令信息

假设 Sancho 想要比较 *man* 和 *info* 提供的 who 信息。为了调用 *info* 命令，他输入：

```
$ info<Enter>
```

Linux 响应以 *info* 目录树，其大约 250 行的结构如下所示：

```
File:dir          Node:top    This is the top of the INFO tree

"Basic Instructions"

*Menu:

Texinfo documentation system
Miscellaneous (i.e., list of common commands)
Programming Languages
GNU Gettext Utilities
GNU Packages
Libraries
Individual Utilities
Net Utilities
World Wide Web
Printing Tools
C library code
Programming
GNU Emacs
GNU Admin
Programming & development tools
GNU libraries
Indent Code Formatter
GNU programming tools
```

我们知道 Sancho 想了解关于 who 命令的一些事情。通过 Tab 键或上、下箭头键，他将光标移动到 Miscellaneous 下的 who，并按下 Enter 键选择 who。随后，Linux 跳转，或超链接到，who 的信息：

```
'who': Print who is currently logged in
=================================================
'who' prints information about users who are currently logged on.
"Synopsis"
"Explanation"
"Options"
(etc.)
```

Sancho 可以在信息中上下导航。他可以按下以下按键：

-   空格键，每次一屏地向下导航文件
-   h，显示帮助
-   / 后跟一个字符串和 Enter，在文本中搜索该字符串
-   n，移动到下一个相关主题或功能（如果有）
-   p，移动到上一个相关主题或功能
-   d，返回第一屏（即回到 **info** 目录的顶部）
-   q，退出 **info**

## usage 实用工具

**usage** 实用工具可能非常有价值。它基于 **man** 和 **info** 使用的相同数据库。你可以通过两种方式调用此功能。首先，让我们通过请求命令 **usage** 帮助来调用它。语法如下：

```
$ **commandname** -help<Enter>
```

调用 **usage** 的第二种方式基本上是意外发生的。如果你错误地输入了一个命令，Linux 会响应告诉你做错了什么，然后（通过 **usage**）告诉你如何更正命令输入。

示例 3.6 说明了调用 **usage** 的两种方式。

### 示例 3.6 调用 usage 实用工具

Sancho 一直是 *sneakernet*（即软盘传输）的支持者——也就是说，他仍然偶尔使用软盘。自然，他想知道如何使用他所在的 Rueful Figures, Inc. 系统上的软盘驱动器。系统管理员 Preston 告诉他，必须熟悉 **mount** 命令。Sancho 似乎记得一个可以与 **mount** 一起使用的 -d 选项。在这里，他将通过调用 **usage** 来检查。首先，他故意请求 **mount** 命令的信息：

```
$ **mount** -help<Enter>
Usage: **mount** -v
: print version
**mount** -h
: print this help
**mount**
: list mounted **filesystems**
**mount** -l
: idem, including volume labels
So far the informational part. Next the mounting.
The command is ‘**mount** [ -t *fstype*] something somewhere’.
Details found in /etc/fstab may be omitted.
(/etc.)
```

Sancho 没有看到 -d 选项，但他认为可能有所遗漏。因此，他将冒险故意输入带有 -d 选项的 **mount** 命令，看看 Linux 如何响应：

```
$ mount -d /dev/Fd0<Enter>
```

这是 Linux 的响应：

```
mount: invalid option -d
Usage:    mount -V        : print version
          mount -h        : print this help
          mount           : list mounted filesystems
          mount -l        : idem, including volume labels
So far the informational part. Next the mounting.
The command is `mount [ -t fstype] something somewhere`.
Details found in /etc/fstab may be omitted.
(etc.)
```

确信确实没有 -d 选项后，Sancho 决定探索其他 mount 选项。与此同时，我们将在第 4 章“Linux 中的文件和目录”中讨论 mount 命令。

## 查看日期：date 和 cal 命令

现在我们知道 1) 有关命令语法的一些事情，以及 2) 在哪里寻求命令帮助；让我们来看看一些我们在日常管理中使用的常见命令。

Freston 作为系统管理员的职责包括为 Ruel Figure, Inc. 网络全局设置日期。一旦他完成设置，用户就可以通过输入 date 命令在自己的系统上显示日期。

当你使用 date 命令显示日期时，你可以以几种方式自定义它——但默认情况下，它不需要任何选项。（有关设置日期的更多信息，请查阅 date 命令的手册页。）语法很简单：

```
$ date<Enter>
```

Linux 响应基于 24 小时制时钟的时间（例如，下午 1 点显示为 13:00:00），随后是日期和时区（例如，CST 代表中部标准时间）。

cal（日历）命令的语法如下：

