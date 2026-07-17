# Linux 命令行：涵盖所有核心 Linux 命令的参考指南（第3版）：Linux 书籍与 Linux 内核



![](img/image_rsrc4RW.jpg)






## 关于作者：Ray Yao 团队
- 美国 Zend 认证 PHP 工程师
- 美国 Sun 认证 JAVA 程序员
- 美国 Oracle 认证 SCWCD 开发者
- 美国 CompTIA 认证 A+ 专业人士
- 美国 Microsoft 认证 ASP. NET 专家
- 美国 Microsoft 认证 MCP 专业人士
- 美国 Microsoft 认证 TECHNOLOGY 专家
- 美国 CompTIA 认证 NETWORK+ 专业人士

- [www.amazon.com/author/ray-yao](http://mybook.to/yaowining)
- [Ray Yao 编写的平装书籍](https://geni.us/ray-yao)
- [C# 速查表](https://author.to/C_Sharp_Cheat_Sheet)
- [C++ 速查表](https://mybook.to/C_Plus_cheat_sheet)
- [JAVA 速查表](https://author.to/Java_Cheat_Sheet)
- [JavaScript 速查表](https://mybook.to/JavaScript_cheat_sheet)
- [PHP MySQL 速查表](https://mybook.to/PHP_cheat_sheet)
- [Python 速查表](https://author.to/Python_Cheat_Sheet)
- [Html Css 速查表](https://mybook.to/Html_Css_cheat_sheet)
- [MySQL 速查表](https://geni.us/MySQL_chsh_paperback)
- [SQL 速查表](https://geni.us/SQL_chsh_paperback)
- [Linux 命令行](http://mybook.to/Linux_Command_Line)
- [Ray Yao 编写的 Kindle 电子书](https://geni.us/ray-yao)

*(注：每份速查表包含包含 300 个示例、300 多个输出和 300 多个解释。)*

## 关于本书
本书是一本快速学习 Linux 命令的参考指南，这些命令被 Linux 管理员或初学者常用。书中涵盖了所有核心 Linux 命令及其操作、示例和解释。它还包含了 Linux 帮助命令、符号、快捷键、运行级别和 Vi 命令。通过本书，你可以轻松学习到：

- 如何运行所有核心 Linux 指令。
- 如何复制、移动和删除文件及目录。
- 如何创建、删除和管理用户及组。
- 如何访问 Linux 服务器并使用 `SSH` 命令。
- 如何操作和更改运行级别。
- 如何通过帮助命令在命令行中导航。
- 如何比较文件、查找文件、处理文件内容。
- 如何启动、停止和调度任务。
- 如何管理文件、目录的权限和所有权。
- 如何跨网络连接与网络通信。
- 如何通过网络传输文件、发送网络消息。
- 以及更多技能……

书中有一个包含所有常用 Linux 指令的长表，这可以为你的工作或学习提供极大帮助。你可以快速学习所有核心 Linux 指令。

**注意：** 本书是一份参考指南，可能并不适合完全全新的 Linux 初学者。


# 第 01 章
## Linux 简介

### 关于 Linux 操作系统
Linux 是一种类 Unix 操作系统，在自由和开源软件开发与分发模式下构建，并大多符合 POSIX 标准。

Linux 通常作为服务器，因为其稳定性和安全性。

Linux 操作系统在 IT 行业极具优势：
- Linux 程序大多免费下载。
- 它们频繁更新且免费！
- 许多功能比 Windows 更好。某些功能在 Windows 中甚至不存在！

为了更好地了解 Linux，我们需要回到 1984 年。

#### 1984 年
当我们回到 1984 年时，计算机科学的发展还并不完美。微软刚刚发布了第一个操作系统：`MS-DOS`，它通过命令行运行。

#### 但是，当时 MS-DOS 是唯一的吗？
#### 不！当时存在另一个操作系统，但公众较少知道。

那个系统被称为 `Unix`。它比 `MS-DOS` 强大得多，但也复杂，这解释了为什么只有 IT 专业人士才能使用 `Unix`。

从图形上看，`Unix` 类似于 `MS-DOS`，它们都显示为带有白色文本的黑色屏幕，并通过命令行运行。

#### Linux 的诞生
1991 年，赫尔辛基大学的学生 Linus Torvalds 开始创建他自己的自由操作系统。这个系统被称为 Linux，指的是其创造者的名字（Linux 是 Linus 和 UNIX 的缩写）。

#### 如今三大操作系统
`Mac OS` 和 Linux 均基于 `UNIX`，这是这两个操作系统的祖先。而来自 `MS-DOS` 的 `Windows OS` 是一个独立分支。

#### Linux 发行版
Linux 发行版（简称 distro）是一个基于 Linux 内核的软件包集合和软件包管理系统的操作系统。最为人知的发行版有 RedHat、SUSE、Debian、Mandriva、Slackware 和 Ubuntu。你可以在不同的 Linux 发行版中找到大量软件。





无论你安装哪种发行版，你都会获得一个 Linux 操作系统以及与其他系统的兼容性。大多数发行版在处理上都或多简单。

## 各种现有发行版

有许多不同的 Linux 发行版。很难选择吗？你一定会说：确实。起初并不清楚该选哪一个……尤其是它们都是免费的！别担心；我会帮助你做出选择。

我不会列出所有的现有发行版，但这里至少有主要的几个：

- **Slackware**：最老的 Linux 发行版之一。它今天仍然存在！
- **Mandriva**：由一家法国公司出版，简单易；
- **RedHat**（红帽）：由一家美国公司出版，该发行版在世界上广为人知，特别是在服务器领域；
- **SUSE**：由 Novell 公司出版；顺便问一下，你知道著名的 Novell Networking（新潮流）吗？
- **Debian**：由独立开发者而非公司管理。这是最受欢迎的发行版之一。

正如我所说，无论你选择哪种发行版（distribution 的缩写），你拥有的都是 Linux 操作系统。

## Linux 操作系统--文件系统

### 什么是文件系统？

“文件系统”一词有两个含义：首先，指的是存储在某些特定目录中的组织文件集合。其次，它指的是用于在硬盘分区或外部磁盘上组织文件的低级数据结构。

Linux 文件系统组织成由目录组成的逻辑树结构。下面的插图描述了一个文件系统树：

| | | `/dev` | | |
|---|---|---|---|---|
| | `/bin` | `/lib` | `/sbin` | |
| `/boot` | `/initrd` | `/etc` | `/proc` | |
| `/mnt` | `/tmp` | `/var` | `/opt` | `/usr` |
| | `/root` | `/home` | | |
| | | `/` | | |

**解释：**

- `/bin`：包含基本的命令行工具，持有的用于操作系统的系统二进制文件或程序，包含所有用户可用的命令。
- `/boot`：包含 Linux 在计算机上启动所需的命令和文件，包括内核、启动加载程序以及定义系统启动时在屏幕上打印文本的文件。
- `/Dev`：包含所有访问系统上各种硬件组件的设备文件。该目录用于表示系统上设备的特殊文件。
- `/etc`：包含一组系统配置文件，用于管理系统初始化以及网络、服务、密码和子系统的配置参数……
- `/home`：包含用户的数据文件。它是存放用户个人配置和数据文件的默认位置。
- `/lib`：包含许多不同应用程序以及 Linux 内核所需的程序库。
- `/mnt`：包含各种移动设备的挂载点。
- `/opt`：包含加载到系统上的可选文件和包。
- `/proc`：包含当前运行的所有内核相关进程。
- `/root`：超级用户的家目录。
- `/sbin`：包含系统管理命令，这些是系统二进制文件。
- `/tmp`：包含普通用户创建的临时文件。
- `/usr`：包含所有用户可用的程序和数据，这是一个带有许多子目录和文件的巨大目录。
- `/var`：包含变量数据，如系统日志、打印队列文件和锁文件。
- `/initrd`：仅包含一个文件，警告该文件夹不能删除。否则，Linux 系统将无法启动。

Linux 操作系统的运行方式与 Windows 不同。Linux 文件系统的结构看起来像一棵树。

文件系统是从像硬盘之类的存储设备上组织和管理文件的技术。文件系统通常由各种文件组成，分成称为目录。目录可以包含文件或额外的子目录。

## 总结

- Windows、Mac OS 和 Linux 是最流行的操作系统。
- Linux 通常作为服务器运行，因为它的稳定性和安全性特性。
- Linux 是一个免费操作系统，它的源代码（制造配方）是开放的，任何人都可以查看。
- 如今，有许多不同的 Linux 版本，被称为发行版。
- 文件系统，Linux 操作系统由各种 Linux 系统文件组成。

# 第 02 章

## 输入第一条命令

亲爱的朋友们，大日子终于到了！你准备好在控制台中编写第一条命令了！

好了，压力不大吧？

## 我向你保证，我们将从简单的事情开始，熟悉控制台。我们将真正看到 ABC，新手的基础生存指南。

## Linux 命令与参数

Linux shell 是一个命令行解释器，或者为 Linux 操作系统和类 Linux 系统提供传统的用户界面。

shell 识别许多 Linux 命令及其改变其行为的选项。Linux 命令的典型语法如下：

```
command --option argument
```
或
```
command parameter
```
（通常 `--option argument` 参数）

例如：

- 命令看起来像：`ls`, `cat`, `pwd`, `cp`, `mv`, `date`……
- 参数看起来像：`-a`, `-l`, `-s`, `--all`, `--help`……

**示例：**

```
ls -a
```

**解释：**

- `ls` 是一个命令，意思是“列出当前目录的内容”。
- `-a` 是一个参数，意思是“所有”。
- 结果：列出当前目录下的所有内容。

Linux 命令可以在文本界面模式运行，也可以在 shell 终端窗口运行。

### 命令提示符

命令提示符是提示你输入命令的消息。命令提示符显示在每个命令之前。

**示例：**

```
username@hostname ~ $
```

```
root@hostname ~ #
```

```
user >
```

**解释：**

- `username@hostname ~ $`：第一个元素是你的用户名。这是你登录账户的用户。
- `@`：这个符号表示“位于”。它是一个分隔符。
- `hostname`：你正在工作的计算机名称。在我的例子中它被称为 hostname，但你可以在安装期间给它起任何名字。
- `:` 这个符号没有特殊含义，它是一个分隔符。
- `~`：意味着你处于家目录，Linux 中所谓的“home”等于 Windows 上的“我的文档”文件夹。我们将在下一章详细学习文件的操作。
- `$`：这个符号非常重要；它显示你在机器上的权限级别。
- `ls`：ls 是一个命令。（显示当前目录的内容）。

关于 `$` 的更多细节：

- 意味着你目前以具有有限权限的“普通”账户身份工作（“普通”账户的用户无法更改最重要的系统文件）。我的账户 `user014` 是一个权限有限的普通账户；

如你所见，一旦你和命令提示符使用相同的语言，你就能理解它的意思了！

此时，Linux 机器似乎在对你说：

“欢迎，你是 user-linux 机器上的 user014。你现在位于普通账户的家目录，拥有有限权限。你正在使用命令 `ls` 列出当前目录的内容。”

关于 `root@hostname:~#whoami`

**示例：**

```
root@user-linux:~# whoami
```

**解释：**

- `root`：意味着你以超级用户“root”账户身份工作。
- `@`：这个符号表示“位于”。它是一个分隔符。
- `user-linux`：你正在工作的计算机名称。在我的例子中它被称为 user-linux，但你可以在安装期间给它起任何名字。
- `:` 这个符号没有特殊含义，它是一个分隔符。
- `~`：那是你当前所在的文件夹。你可以在控制台中在文件夹之间导航，在输入每个命令之前始终提醒你身处哪里，这是非常有用的。





符号 `~` 表示你正处于主目录，Linux 中所谓的“home”等同于 Windows 上的“我的文档”文件夹。我们将在下一章详细学习 Linux 中文件的操作。

`#` 表示你正在以“root”账户的超级用户（super user）身份工作。

`whoami`：`whoami` 是一个命令。（显示当前用户名）。

## 关于 `#` 的更多细节

`#`:意味着你正在以“root”账户的超级用户身份工作。`root` 是管理员，拥有极大的权力，可以对计算机上的其他用户账户进行任何操作（甚至是摧毁它！）。我们稍后将详细查看 `root` 的工作原理；

此时，Linux 机器似乎在向你打招呼：

“欢迎，你是 user-linux 机器上的一个超级用户。你目前处于 root 账户的主目录，并拥有超级用户权限。你正在使用命令 `whoami` 来显示当前用户名。”

## 关于 `user>pwd`

示例：

```bash
user>pwd
```

解释：

`user>`：是一个自定义的命令提示符。

`pwd`：`pwd` 是一个命令。（打印工作目录）。

你可以自定义像 `user>` 这样的命令提示符。当然，在你熟悉了大多数 Linux 命令编程后，将能够自定义 shell 提示符。

此时，Linux 机器似乎在向你打招呼：

“欢迎，你是 user-linux 机器上的一个用户。你正在使用自定义的命令提示符。你目前处于主目录并拥有有限的用户权限。你正在使用 `pwd` 命令打印工作目录。”

命令提示符可以完全配置。如果你发现它太长，可以缩短它；如果显示的信息不够，可以延长它。从理论上讲，你可以在提示符中放入任何想要的信息，例如当前时间。

## 关于 Linux 命令

Shell 命令的典型语法如下：

```
command   option   argument
```
或

```
command   parameter
```

让我们来看一些 Linux 命令示例。

示例：

输入 `date` 并按回车键。

```bash
user2014 @ user-linux: ~ $ date
Monday, September 20, 2010, 3:39:51 p.m. (UTC-0200)
```

解释：

第一行包含命令提示符和我输入的命令。在这里，`date` 是一个命令。

第二行是计算机对该命令的响应：我刚刚请求了日期和时间！

## 关于参数（Parameters）

参数是输入命令后面的选项。命令和参数之间用空格分隔，如下：

```bash
user2014 @ user-linux: ~ $ command parameters
```

参数本身可以包含空格、字母、数字……以及一些其他内容。参数的格式并没有真正的规则，但幸运的是，程序员们采用了一种“约定”，以便我们能够识别不同类型的参数。

### 短参数（单字母）

短参数由一个连字符开头的单个字母组成。

例如：

- `-d`
- `-l`
- `-a`

如果我们必须给出几个参数，可以这样写：

`-d -a -U -h`

或者更短的：

`-daUh`

注意：不同命令中的短参数含义不同。

示例：

- `ls -t` (`-t` 表示“按时间戳列出”）
- `eject -t` (`-t` 表示“关闭托盘”）
- `chfn -f` (`-f` 表示“通过指纹名称更改信息”）
- `cut -f` (`-f` 表示“按字段编号切割文本”）
- `ps -f` (`-f` 表示“显示完整信息的进程状态”）

注意！参数是对大小敏感的（大写/小写）。如果你输入 `-u`，它的含义通常与 `-U` 不同。

让我们用 `ls` 命令进行测试，并跟上参数 `-a`。（`-a` 表示“所有”）：

示例：

```bash
user2014@user-linux: ~ $ ls -a.
.gconfd .mozilla-thunderbird .. gimp-2.2 .nautilus .bash_history .gksu.lock .profile .bash_logout .gnome .recently-used .bashrc .gnome2 .recently-used.xbel .config .gnome2_private .ssh Desktop .gstreamer- .sudo_as_admin_successful .dmrc .gtkrc 0.10-1.2-gnome2 .themes .esd_auth .ICEauthority .thumbnails .evolution .icons .Trash Examples .lesshst tutorials .face .local .update-manager-core .fontconfig .macromedia .update-notifier .gaim. metacity .Xauthority .gconf .mozilla .xsession-errors
```

屏幕显示当前目录下的所有文件，甚至是隐藏文件。通常，主目录包含许多隐藏文件，它们通常是程序的配置文件。

### 长参数（多个字母）

长参数由两个连字符开头的几个字母组成，如下：

```
--long parameter
```

例如：

- `--all`
`--all` 是长参数，意味着所有内容或所有事物。

- `--version`
`--version` 是长参数，意味着命令的版本。

- `--help`
`--help` 是长参数，意味着获取当前命令的帮助。

如果你想将多个功能参数放在一起，它们之间会添加空格：

```
Command --long parametre1 --long parametre2
```

你也可以以这种方式结合长短参数：

```
Command -daUh --All
```

注意，某些参数不提供短版本和长版本之间的选择。

让我们用 `--all` 参数测试 `ls` 命令，它的意思是“所有事物”：

示例：

```bash
user2014@user-linux: ~ $ ls --all.
.gconfd .mozilla-thunderbird .. gimp-2.2 .nautilus .bash_history .gksu.lock .profile .bash_logout .gnome .recently-used .bashrc .gnome2 .recently-used.xbel .config .gnome2_private .ssh Desktop .gstreamer- .sudo_as_admin_successful .dmrc .gtkrc 0.10-1.2-gnome2 .themes .esd_auth .ICEauthority .thumbnails .evolution .icons .Trash Examples .lesshst tutorials .face .local .update-manager-core .fontconfig .macromedia .update-notifier .gaim. metacity .Xauthority .gconf .mozilla .xsession-errors
```

如所示，`--all` 和 `-a` 是同义词，这说明命令提供了两种使用参数的方法：短版本和长版本。

## 命令和参数示例

好的！让我们进一步查看这些命令。

`su -l`：切换用户

示例：

```bash
user>su -l
```
(su 将以 root 用户身份登录，l 是一个表示“登录”的参数)

`ls -l`：列出详细内容

示例：

```bash
user>ls -l
```
(ls 显示当前目录的内容。l 是表示“详细”的参数)

`ls -a`：列出所有内容

示例：

```bash
user>ls -a
```
(ls 显示当前目录的内容。a 是表示“所有”的隐藏文件的参数。)

`rm -ri`：删除目录及其内容

示例：

```bash
user>rm -ri NonEmptyDir
```
(rm 删除目录。ri 是表示非空目录的参数。NonEmptyDir 是一个目录名。)

`w -s`：显示每个用户的当前进程

示例：

```bash
user>w -s
```
(w 显示当前进程。s 是表示“摘要”的参数)

`usermod -l`：修改现有用户账户

示例：

```bash
user>usermod -l oldname newname
```
(usermod 修改现有用户账户。l 是表示“登录名”的参数)

## 虚拟控制台 (Virtual Console)

### 什么是虚拟控制台？

虚拟控制台是指输入设备和输出设备的接口，旨在让你与系统进行交互。

Linux 有 7 个虚拟控制台，你可以使用 `Ctrl+Alt+F1` 到 `F7` 在之间切换。

`Ctrl+Alt+F1~F6`：切换虚拟控制台 1~6

`Ctrl+Alt+F7`：进入图形桌面，这是默认虚拟控制台。

1. 当用户是普通用户时，使用：
`username@hostname:~$ command parameter`

2. 当用户是超级用户时，使用：
`root@hostname:~# command parameter`

3. 当 shell 提示符被自定义后，使用：
`User> command parameter`

4. Linux 命令：`ls, pwd, su, whoami, loginname, rm, exit…`

5. 命令参数：`-a, -ri, -l,--all, --help…`

6. 虚拟控制台：让你同时激活多个接口 shell 会话。





## `su`: 将普通用户切换为 root 超用户

示例：
```
user2014@user-linux:~$ su –l
```
(`su`: 将普通用户切换为 root 超用户。`–l`: 输入 root 密码并登录。注意：登录为超级用户后，`$` 将变为 `#`。）

## `loginname`: 显示登录名

示例：
```
root@user-linux: ~ # loginname
```
(`loginname`: 显示登录名，输出为“root”。注意：登录为超级用户后，`$` 变为 `#`。）

## `exit`: 退出 shell 

示例：
```
root@user-linux:~# exit
```
(`exit`: 退出 shell。在此处：退出超级用户模式，并回到普通用户模式。注意：退出超级用户后，`#` 将变为 `$`。）

## `whoami`: 显示当前用户名

示例：
```
user2014@user-linux: ~ $ whoami
```
(`whoami`: 显示当前用户名，输出为“user2014”。）

## `hostname`: 显示当前主机名

示例：
```
user2014@user-linux: ~ $ hostname
```
(`hostname`: 显示当前主机名，输出为“user-linux”。）

## `sudo`: 允许具有适当权限的用户以用户的身份执行命令，例如超级用户

示例：
```
root> sudo -u andy ls /home/mydir
```
(以用户 andy 的身份列出 `/home/mydir` 目录的内容。`-u`: 指定用户)

示例：
```
root> sudo –v
```
(`-v`: 刷新认证超时，下次 `sudo` 命令将不需要密码。）

示例：
```
root> sudo -k
```
(`-k`: 过期认证超时，下次 `sudo` 命令将需要密码。）

## 总结
- `su`: 将普通用户切换为 root 超用户
- `loginname`: 显示登录名
- `exit`: 退出 shell。
- `whoami`: 显示当前用户名
- `hostname`: 显示当前主机名
- `sudo`: 允许具有适当权限的用户以用户的身份执行命令，例如超级用户。

# 第 04 章：导航 At 命令

- `pwd`: 打印工作目录。
- `cd dir`: 切换目录。
- `cd~`: 切换到家目录。
- `cd..`: 切换到父目录。
- `type`: 确定命令类型。

### `pwd` 示例
```
user> pwd
```
(`pwd`: 打印工作目录，输出为你的当前工作目录。）

### `cd dir` 示例
```
user> cd mydir
```
(`cd`: 切换目录到 mydir，输出为 mydir。）

### `cd~` 示例
```
user> cd ~
```
(`cd~`: 切换到家目录，输出为家目录。）

### `cd..` 示例
```
user> cd ..
```
(`cd..`: 切换到父目录，输出为父目录。）

### `type` 示例
```
user> type pwd
```
(输出: `pwd` 是 shell 内置命令。)

## 总结
- `pwd`: 打印工作目录。
- `cd`: 切换目录。
- `cd~`: 切换到家目录。
- `cd..`: 切换到父目录。
- `type`: 确定命令类型。

# 第 05 章：文件操作命令

- `cp`: 复制文件
- `mv`: 移动文件
- `mv`: 重命名文件
- `rm`: 删除文件
- `rm –ri`: 删除非空目录
- `vi`: 打开 vi 编辑器并编辑文件
- `find`: 查找文件
- `wc`: 显示文件字数
- `file`: 描述文件类型
- `ln`: 在两个文件之间创建链接
- `ln -s`: 创建文件的符号链接
- `readlink`: 显示符号链接的目标
- `lpr`: 将文件发送到打印机
- `lpq`: 显示打印队列。

### `cp` 示例
```
user> cp myfile /dir1
```
(`cp`: 将 `myfile` 复制到 `/dir1` 目录。）

### `mv` 示例（移动）
```
user> mv myfile /dir2
```
(`mv`: 将 `myfile` 移动到 `/dir2` 目录。）

### `mv` 示例（重命名）
```
user> mv myfile1 myfile2
```
(`mv`: 将 `myfiel1` 重命名为 `myfile2`。）

### `rm` 示例
```
user> rm myfile
```
(`rm`: 删除 `myfile`。）

### `rm –ri` 示例
```
user> rm –ri NonEmptyDir
```
(`rm`: 删除名为 `NonEmptyDir` 的目录。`-ri`: 删除包含内容的目录。）

### `vi` 示例
```
user> vi myfile.txt
```
(`vi`: 打开 vi 编辑器并编辑 `myfile.txt`。）

### `find` 示例
```
user> find directory –type f –name myfile.txt -print
```
(`find`: 查找文件。`-type f`: 指定文件，`-name`: 指定文件名，`-print`: 打印）

### `wc` 示例
```
user> wc myfile.txt
```
(`wc`: 显示 `myfile.txt` 的字数。）

### `file` 示例
```
user> file myfile.txt
```
(`file`: 描述 `myfile.txt` 的类型。）

### `ln` 示例
```
user> ln dir1/file1.txt dir2/file2.txt
```
(`ln`: 在 `file1` 和 `file2` 之间创建链接。）

### `ln -s` 示例
```
user> ln –s dir1/file1.txt dir2/file2.txt
```
(`ln-s`: 在 `file1` 和 `file2` 之间创建符号链接。`-s`: 符号链接允许给定文件同时出现在多个地方或多个名称下。例如，符号链接可以链接到目录。）

### `readlink` 示例
```
user> readlink dir2/file2.txt
```
(输出：`dir1/file1.txt`)

### `lpr` 示例
```
user> lpr myfile.txt
```
(`lpr`: 将 `myfile.txt` 发送到打印机。）

### `lpq` 示例
```
user> lpq
```
(`lpq`: 显示打印队列。）

## 总结
- `cp`: 复制文件
- `mv`: 移动文件
- `mv`: 重命名文件
- `rm`: 删除文件
- `rm –ri`: 删除非空目录
- `vi`: 打开 vi 编辑器并编辑文件
- `find`: 查找文件
- `wc`: 显示文件字数
- `file`: 描述文件类型
- `ln`: 在两个文件之间创建链接
- `ln -s`: 创建文件的符号链接
- `readlink`: 显示符号链接的目标
- `lpr`: 将文件发送到打印机
- `lpq`: 显示打印队列。

# 第 06 章：查看文件命令

- `cat`: 查看文件内容
- `cat | less`: 分页查看文件内容
- `cat | more`: 分屏查看文件内容
- `head`: 查看文件开头部分
- `tail`: 查看文件末尾部分
- `aspell`: 检查拼写
- `cut`: 提取特定列
- `paste`: 合并文件
- `sort`: 排序文件
- `stat`: 查看文件状态
- `nl`: 为每行添加编号
- `tr`: 转换字符
- `tee`: 读取标准输出并写入文件

`cat` 示例
```
user> cat myfile.txt
```
(`cat`: 查看文件内容。）

`cat | less` 示例
```
user> cat myfile.txt | less
```
(`cat`: 查看文件内容，`| less`: 分页查看文件内容。）

`cat | more` 示例
```
user> cat myfile.txt | more
```
(`cat`: 查看文件内容，`| more`: 分屏查看文件内容。）

`head` 示例
```
user> head myfile.txt
```
(`head`: 查看文件开头部分。）

`tail` 示例
```
user> tail myfile.txt
```
(`tail`: 查看文件末尾部分。）

`aspell` 示例
```
user> aspell myfile.txt
```
(`aspell`: 检查拼写。）

`cut` 示例
```
user> cut –f2 myfile.txt
```
(`cut`: 提取特定列，`-f2`: 指定第二列。）

`paste` 示例
```
user> paste myfile1.txt myfile2.txt
```
(`paste`: 合并文件。）

`sort` 示例
```
user> sort myfile.txt
```
(`sort`: 排序文件。）

`stat` 示例
```
user> stat myfile.txt
```
(`stat`: 查看文件状态。）

`nl` 示例
```
user> nl myfile.txt
```
(`nl`: 为每行添加编号。）

`tr` 示例
```
user> tr 'a-z' 'A-Z' < myfile.txt
```
(`tr`: 转换字符。）

`tee` 示例
```
user> cat myfile.txt | tee output.txt
```
(`tee`: 读取标准输出并写入文件。）





`nl`: 显示文件的每行数字

Example:

```bash
root> nl myfile.txt
```
(output:
……
023  sld slwflflf gjo4ijg gj4jf9ej
024  wz wg tjletj geg4t4y
025  sjflew gjlgnu4g jgu675h dk9fh fmj6ju
026  jf5hjd fjtjfj  d8gj1nfj,nuigrr ? rit
……)

`vi`: 使用 `vi` 编辑器或创建文本文件

Example:

```bash
root> vi myfile.txt
```
(`vi`: 用 `vi` 编辑器打开 `myfile.txt`)

`tr`: 转换文件中的文本

Example:

```bash
root> echo apple | tr “apple” “banana”
```
(output: banana)

`tee`: 打印标准输出并写入文件

Example:

```bash
Root> sort file1.txt | tee file2.txt
```
(`sort file1.txt` 结果并写入 `file2.txt`)

### Summary

- `cat`: 显示文件内容
- `cat | less`: 分页显示文件内容
- `cat | more`: 分屏显示文件内容
- `head`: 显示文件的开头部分
- `tail`: 显示文件的末尾部分
- `aspell`: 对文件进行拼写检查
- `cut`: 显示文本文件中指定的列
- `paste`: 合并并显示两个文件的内容
- `sort`: 按字母顺序显示文本行
- `stat`: 显示文件或目录的属性
- `wc`: 显示文件的单词数
- `file`: 测试文件类型
- `touch`: 创建文件或修改文件时间戳
- `nl`: 显示文件的每行数字
- `vi`: 使用 `vi` 编辑器或创建文本文件
- `tr`: 转换文件中的文本
- `tee`: 打印标准输出并写入文件

# 第 07 章

## 文件比较命令

`diff`: 显示两个文件之间的差异

`cmp`: 逐字节比较两个文件

`comm`: 按行比较两个文件

`md5sum`: 创建 md5 校验和数字

`cksum`: 创建 crc 校验码

`diff`: 显示两个文件之间的差异

Example:

```bash
user> diff myfile1.txt  myfile2.txt
```
(`diff`: 显示两个文件之间的差异。)

`cmp`: 逐字节比较两个文件

Example:

```bash
user> cmp myfile1.txt  myfile2.txt
```
(`cmp`: 逐字节比较两个文件。)

`comm`: 按行比较两个文件

Example:

```bash
user> comm myfile1.txt  myfile2.txt
```
(`comm`: 按行比较两个文件。)

`md5sum`: 创建 md5 校验和数字

Example:

```bash
user> md5sum  myfile1.txt
```
(output:  f7tkgu5orj1fjt8kelc2os95nd57jf8r  myfile1.txt.)

`cksum`: 创建 crc 校验码

Example:

```bash
user> chsum  myfile2.txt
```
(output: 4658791048  19  myfile2.txt.)

### Summary

- `diff`: 显示两个文件之间的差异
- `cmp`: 逐字节比较两个文件
- `comm`: 按行比较两个文件
- `md5sum`: 创建 md5 校验和数字
- `cksum`: 创建 crc 校验码

# 第 08 章

## 文本匹配命令

`grep`: 显示所有包含指定字符串的行

`egrep`: 显示所有包含指定字符串的行

`uniq`: 显示文件中唯一的行

`find`: 在指定目录中查找文件

`look`: 显示与给定前缀匹配的单词

`grep`: 显示所有包含指定字符串的行

Example:

```bash
user> grep  good  myfile.txt
```
(`grep`: 显示所有包含“good”字符串的行。)

`egrep`: 显示所有包含指定字符串的行

Example:

```bash
user> egrep  excellent  myfile.txt
```
(`egrep`: 显示所有包含“excellent”字符串的行。)

`uniq`: 显示文件中唯一的行

Example:

```bash
user> uniq myfile.txt
```
(`uniq`: 显示 `myfile.txt` 中的唯一行。)

`find`: 在指定目录中查找文件

Example:

```bash
user> find /mydir –type f myfile.txt -print
```
(`find`: 在目录中查找文件。
`-type f`: 指定为文件
`-print`: 打印)

`look`: 显示与给定前缀匹配的单词

Example:

```bash
User> look ab
```
(output: aba, abb, abc, abd…)

### Summary

- `grep`: 显示所有包含指定字符串的行
- `egrep`: 显示所有包含指定字符串的行
- `uniq`: 显示文件中唯一的行
- `find`: 在指定目录中查找文件
- `look`: 显示与给定前缀匹配的单词

# 第 09 章

## 目录命令

`mkdir`: 创建新目录

`rmdir`: 删除空目录

`basename`: 显示文件路径的最后部分

`dirname`: 只显示目录路径

`mkdir`: 创建新目录

Example:

```bash
user> mkdir mydir
```
(`mkdir`: 创建新目录)

`rmdir`: 删除空目录

Example:

```bash
user> rmdir mydir
```
(`rmdir`: 删除空目录)

`basename`: 显示文件路径的最后部分

Example:

```bash
user> basename /home/foo/usr/file.txt
```
(output:  file.txt)

`dirname`: 只显示目录路径

Example:

```bash
User>dirname  /foo/bar/baz/myfile.txt
```
(output:  /foo/bar/baz)

### Summary

- `mkdir`: 创建新目录
- `rmdir`: 删除空目录
- `basename`: 显示文件路径的最后部分
- `dirname`: 只显示目录路径

# 第 10 章

## 压缩命令

`zip`: 压缩文件
`unzip`: 解压缩文件

`gzip`: 压缩文件
`gunzip`: 解压缩文件

`bzip2`: 压缩文件
`bunzip2`: 解压缩文件

`tar`: 归档文件

`gzip`: 压缩文件
`gunzip`: 解压缩文件

`zip`: 压缩文件
解压缩文件

Example:

```bash
user> zip myfile.txt
```
(`zip`: 压缩 `myfile.txt`)

```bash
user> unzip myfile.zip
```
(`unzip`: 解压缩 `myfile.zip`)

```bash
user> gzip myfile.txt
```
(`gzip`: 压缩 `myfile.txt`)

```bash
user> gunzip myfile.gz
```
(`gunzip`: 解压缩 `myfile.gz`)

```bash
user> bzip2 myfile.txt
```
(`bzip2`: 压缩 `myfile.txt`)

```bash
user> bunzip2 myfile.txt.bz2
```
(`bunzip2`: 解压缩 `myfile.txt.bz2`)

```bash
user> tar -cvf archive.tar file1 file2
```
(`tar`: 归档文件)

### Summary

- `zip`: 压缩文件
- `unzip`: 解压缩文件
- `gzip`: 压缩文件
- `gunzip`: 解压缩文件
- `bzip2`: 压缩文件
- `bunzip2`: 解压缩文件
- `tar`: 归档文件

# 第 11 章

## 进程命令

`ps`: 显示当前进程

`kill`: 按 ID 杀死进程

`w`: 显示所有工作进程

`df`: 显示文件系统使用情况

`uptime`: 显示系统运行时间

`top`: 查看实时进程列表

`ps`: 显示当前进程

Example:

```bash
root> ps -u root
```
(`ps`: 显示用户 `root` 运行的进程。)

`kill`: 按 ID 杀死进程

Example:

```bash
root> kill 6270
```
(`kill`: 杀死 PID 为 6270 的进程。)

`w`: 显示所有工作进程

Example:

```bash
root> w -n 10
```
(`w`: 显示当前正在运行的进程。
`-n 10`: 显示 10 个)

`df`: 显示文件系统使用情况

Example:

```bash
root> df -h
```
(`df`: 显示文件系统使用情况。
`-h`: 以易读格式显示)

`uptime`: 显示系统运行时间

Example:

```bash
root> uptime
```
(`uptime`: 显示系统运行时间。)

`top`: 查看实时进程列表

Example:

```bash
root> top -p 1234
```
(`top`: 查看 PID 为 1234 的进程。
`-p`: 指定 PID
1234: 进程)

### Summary

- `ps`: 显示当前进程
- `kill`: 按 ID 杀死进程
- `w`: 显示所有工作进程
- `df`: 显示文件系统使用情况
- `uptime`: 显示系统运行时间
- `top`: 查看实时进程列表

# 第 12 章

## 账户命令

`useradd`: 创建新用户

`usermod`: 修改现有账户

`userdel`: 删除现有账户

`passwd`: 设置用户密码

`chfn`: 修改用户详细信息

`finger`: 显示用户个人详细信息

`useradd`: 创建新用户

Example:

```bash
root> useradd username
```
(`useradd`: 创建新用户。)

`usermod`: 修改现有账户

Example:

```bash
root> usermod –l oldname  newname
```
(`usermod`: 修改现有账户。
`-l`: 修改登录名)

`userdel`: 删除现有账户

Example:

```bash
root> userdel username
```
(`userdel`: 删除现有账户。)

`passwd`: 设置用户密码

Example:

```bash
root> passwd username
```
(`passwd`: 为用户设置密码。)

`chfn`: 修改用户详细信息

Example:

```bash
root> chfn username
```
(`chfn`: 修改用户的详细信息。)

`finger`: 显示用户个人详细信息

Example:

```bash
root> finger username
```
(`finger`: 列出用户的登录名、邮箱、域名、时间等信息。)

### Summary

- `useradd`: 创建新用户
- `usermod`: 修改现有账户
- `userdel`: 删除现有账户
- `passwd`: 设置用户密码
- `chfn`: 修改用户详细信息
- `finger`: 显示用户个人详细信息





`userdel`: 删除现有的用户账户

`passwd`: 设置用户账户密码

`chfn`: 更改个人 finger 信息

`finger`: 显示个人用户的 finger 信息

# 第 13 章

## 组命令

`groups`: 显示组成员关系
`groupadd`: 创建新组
`groupmod`: 修改现有的组
`groupdel`: 删除现有的组
`groups`: 显示组成员关系

### 示例：
```
root> groups username
```
(`groups`: 显示用户的所属组信息。）

`groupadd`: 创建新组
### 示例：
```
root> groupadd newgroup
```
(`groupadd`: 创建一个名为 `newgroup` 的新组。）

`groupmod`: 修改现有的组
### 示例：
```
root> groupmod newgroup
```
(`groupmod`: 修改名为 `newgroup` 的现有组。）

`groupdel`: 删除现有的组
### 示例：
```
root> groupdel newgroup
```
(`groupdel`: 删除名为 `newgroup` 的现有组。）

## 总结
`groups`: 显示组成员关系
`groupadd`: 创建新组
`groupmod`: 修改现有的组
`groupdel`: 删除现有的组

# 第 14 章

## 权限命令

`chmod`: 更改访问权限模式
`chgrp`: 更改组所有
`chown`: 更改文件或目录的所有者
`chmod`: 更改访问权限模式
### 示例：
```
root> chmod 752 myfile1.txt
```
(`chmod`: 更改 `myfile1.txt` 的访问权限。
7: 设置用户读、写、执行权限
5: 设置组用户读、执行权限
2: 设置其他用户仅写权限。）

`chmod`: 更改访问权限模式
### 示例：
```
root> chmod g+w myfile.txt
```
(`g+w`: 为文件所在组的成员赋予写权限）

`chgrp`: 更改组所有
### 示例：
```
root> chgrp groupname myfile2.txt
```
(`chgrp`: 更改 `myfile2.txt` 的组所有`)

`chown`: 更改文件或目录的所有者
### 示例：
```
root> chown username myfile3.txt
```
(`chown`: 更改 `myfile3` 的所有者`)
### 示例：
```
root> chown groupname /user/dir
```
(`chown`: 更改 `dir` 的所有者。）

### 总结：
`chmod`: 更改访问权限模式
`chgrp`: 更改组所有
`chown`: 更改文件或目录的所有者

# 第 15 章

## 作业命令

`job`: 显示所有作业的状态
`fg`: 在前台运行挂起的任务
`bg`: 在后台运行挂起的任务
`kill`: 通过编号杀死作业或通过 pid 杀死进程
`at`: 在指定时间调度运行作业
`atq`: 显示计划的作业
`atrm`: 删除计划作业
`ps`: 显示当前进程状态
`w`: 显示谁登录了以及正在做什么
`uptime`: 显示系统运行时间
`top`: 查看最活跃的进程
`crontab`: 创建一个在指定时间运行的作业
`job`: 显示所有作业的状态
### 示例：
```
root> jobs
```
(`job`: 显示所有作业的状态。）

`fg`: 在前台运行挂起的任务
### 示例：
```
root> fg %2
```
(`fg %2`: 在前台运行挂起的作业 `%2`。）

`bg`: 在后台运行挂起的任务
### 示例：
```
root> bg %3
```
(`bg %3`: 在后台运行挂起的作业 `%3`。）

`kill`: 通过编号杀死作业或通过 pid 杀死进程
### 示例：
```
root> kill %4
```
(`kill %4`: 杀死正在运行的作业 `%4`。）

`at`: 在指定时间调度运行作业
### 示例：
```
root> at 9:30 pm
```
(`at 9:30`: 在 `9:30` 设置一个计划作业。）

`atq`: 显示计划的作业
### 示例：
```
root> atq
```
(`atq`: 显示所有计划作业）

`atrm`: 删除计划作业
### 示例：
```
root> atrm 25
```
(`atrm 25`: 删除计划作业 `25`。）

`ps`: 显示当前进程状态
### 示例：
```
root> ps -f
```
(`ps-f`: 显示当前进程的完整信息。）

`ps`: 显示当前进程状态
### 示例：
```
root> ps -u username
```
(`ps -u`: 显示用户的当前进程。）

`w`: 显示谁登录了以及正在做什么
### 示例：
```
root> w -s username
```
(`-s`: 显示用户的摘要信息。）

`uptime`: 显示系统运行时间
### 示例：
```
root> uptime
```
(`uptime`: 显示系统运行时间。）

`top`: 查看最活跃或指定的进程
### 示例：
```
root> top
```
(`top`: 显示系统上运行的所有进程）

`crontab`: 创建一个在指定时间运行的作业
### 示例：
```
root> crontab -e
```
(`-e`: 编辑 `crontab` 文件，向表中添加一个 `crontab` 作业）

## 总结
`job`: 显示所有作业的状态
`fg`: 在前台运行挂起的任务
`bg`: 在后台运行挂起的任务
`kill`: 通过编号杀死作业或通过 pid 杀死进程
`at`: 在指定时间调度运行作业
`atq`: 显示计划的作业
`atrm`: 删除计划作业
`ps`: 显示当前进程状态
`w`: 显示谁登录了以及正在做什么
`uptime`: 显示系统运行时间
`top`: 查看最活跃的进程
`crontab`: 创建一个在指定时间运行的作业

# 第 16 章

## 备份/恢复命令

`cpio`: 输出或输入 cpio 档文件
`tar`: 创建、查看、提取 tar 档文件
`cpio -o`: 输出 cpio 档文件
### 示例：
```
root> cpio -o > directory.cpio
```
(`-o`: 备份到 cpio 档文件）

`cpio -i`: 输入 cpio 档文件
### 示例：
```
root> cpio -i < directory.cpio
```
(`-i`: 从 cpio 档文件恢复）

`tar -xf`: 提取 tar 档文件
### 示例：
```
root> tar -xf archived.tar
```
(`-xf`: 提取 tar 档文件）

`tar -cf`: 创建 tar 档文件
### 示例：
```
root> tar -cf archive.tar directory
```
(`-cf`: 创建 tar 档文件）

## 总结
`cpio`: 输出或输入 cpio 档文件
`tar`: 创建、查看、提取 tar 档文件

# 第 17 章

## 日期命令

`date`: 显示日期和时间
`cal`: 显示日历
`date`: 显示日期和时间
### 示例：
```
root> date
```
(`date`: 显示当前日期和时间。）

`cal`: 显示日历
### 示例：
```
root> cal
```
(`cal`: 显示日历。）

## 总结
`date`: 显示日期和时间
`cal`: 显示日历

# 第 18 章

## 网络命令

`host`: 查询主机名对应的 IP 地址
`ifconfig`: 显示网络接口配置
`ping`: 测试网络连通性
`ssh`: 安全登录到远程主机
`ftp`: 文件传输协议
`mesg`: 向登录用户发送消息
`write`: 向用户写入消息
`netstat`: 显示网络统计信息
`traceroute`: 跟踪数据传输路径
`nslookup`: 查询 DNS 信息
`ip`: 显示或配置 IP 地址
`route`: 显示或配置路由表
`host`: 查询主机名对应的 IP 地址
`ifconfig`: 显示网络接口配置
`ping`: 测试网络连通性
`ssh`: 安全登录到远程主机
`ftp`: 文件传输协议
`mesg`: 向登录用户发送消息
`write`: 向用户写入消息
`netstat`: 显示网络统计信息
`traceroute`: 跟踪数据传输路径
`nslookup`: 查询 DNS 信息
`ip`: 显示或配置 IP 地址
`route`: 显示或配置路由表

`host`: 查询主机名对应的 IP 地址
### 示例：
```
root> host google.com
```
(`host`: 查询主机名对应的 IP。）

`ifconfig`: 显示网络接口配置
### 示例：
```
root> ifconfig
```
(`ifconfig`: 显示网络接口配置。）

`ping`: 测试网络连通性
### 示例：
```
root> ping -c 4 google.com
```
(`ping -c 4`: 向 google.com 发送 4 次 ping。）

`ssh`: 安全登录到远程主机
### 示例：
```
root> ssh user@remotehost
```
(`ssh`: 安全登录到远程主机 `remotehost`。）

`ftp`: 文件传输协议
### 示例：
```
root> ftp myserver.com
```
(`ftp`: 连接到 ftp 服务器。）

`mesg`: 向登录用户发送消息
### 示例：
```
root> mesg all
```
(`mesg`: 向所有登录用户发送消息。）

`write`: 向用户写入消息
### 示例：
```
root> write username
```
(`write`: 向用户 `username` 写入消息。）

`netstat`: 显示网络统计信息
### 示例：
```
root> netstat -a
```
(`netstat -a`: 显示所有套接字。）

`traceroute`: 跟踪数据传输路径
### 示例：
```
root> traceroute google.com
```
(`traceroute`: 跟踪到 google.com 的路径。）

`nslookup`: 查询 DNS 信息
### 示例：
```
root> nslookup google.com
```
(`nslookup`: 查询 google.com 的 DNS 信息。）

`ip`: 显示或配置 IP 地址
### 示例：
```
root> ip addr
```
(`ip addr`: 显示所有 IP 地址。）

`route`: 显示或配置路由表
### 示例：
```
root> route -n
```
(`route -n`: 显示路由表。）

## 总结
`host`: 查询主机名对应的 IP 地址
`ifconfig`: 显示网络接口配置
`ping`: 测试网络连通性
`ssh`: 安全登录到远程主机
`ftp`: 文件传输协议
`mesg`: 向登录用户发送消息
`write`: 向用户写入消息
`netstat`: 显示网络统计信息
`traceroute`: 跟踪数据传输路径
`nslookup`: 查询 DNS 信息
`ip`: 显示或配置 IP 地址
`route`: 显示或配置路由表





(`nslookup`: 手动查询 DNS 服务器。

DNS（域名命名系统）协议允许你从名称服务器获取给定的主机名的 IP 地址。这个过程被称为解析。）

## 总结
- `host`: 显示远程主机名和 IP
- `ifconfig`: 显示本地网络配置
- `ping`: 发送数据包以测试远程主机是否可达
- `ssh`: 安全地连接到远程计算机
- `ftp`: 通过“文件传输协议”传输文件
- `mesg`: 启用或禁用消息传递功能
- `write`: 向其他用户写入消息
- `open`: 连接到 ftp 服务器
- `mail`: 在本地和范围内发送和接收邮件
- `dhclient`: 提供配置一个或多个网络接口的手段
- `nslookup`: 交互式查询互联网名称服务器以获取 IP 信息。

# 第 19 章：脚本命令

- `echo`: 显示文本。
- `expr`: 执行数学计算
- `#!/bin/bash`: 放在 bash 脚本文件的第一行。
- `echo`: 显示文本。

### 示例
```bash
root> STR=”Hello World!”
root> echo $STR
```
(`echo`: 显示文本。输出是 “Hello World!”)

- `echo -e`: 使用转义序列显示文本。

### 示例
```bash
root> STR=”Hello World!”
root> echo –e “\n$STR\n”
```
(`echo -e`: 使用 `\n` 显示文本。`\n` 意味着换行。）
输出是
““
Hello World!
””

- `expr`: 执行数学计算

### 示例
```bash
user> expr 20 + 80
```
(输出是 “100”)

### 示例
```bash
user> expr 21/7
```
(输出是 “3”)

### 示例
```bash
user> expr 9 “>” 6
```
(输出是 “1”，这个 1 表示真)

### 示例
```bash
user> expr 9 “<” 6
```
(输出是 “0”，这个 0 表示假)

- `#!/bin/bash`: 放在 bash shell 脚本的第一行。

### 示例
```bash
#!/bin/bash
If…then…else…fi
```
(`#!/bin/bash`: 始终放在 bash 脚本的第一行)

## 总结
- `echo`: 显示文本。
- `expr`: 执行数学计算
- `#!/bin/bash`: 始终放在 bash 脚本的第一行

# 第 20 章：系统命令

- `df`: 显示文件系统的磁盘占用情况
- `mount`: 使设备对文件系统可用
- `umount`: 使设备对文件系统不可用
- `fsck`: 检查并修复文件系统
- `init n`: 将系统切换到运行级别 n
- `who -r`: 显示当前的运行级别
- `free`: 显示空闲磁盘空间
- `du`: 显示文件或目录的磁盘占用情况
- `export`: 设置环境变量
- `printenv`: 列出环境变量名称和值
- `unset`: 移除环境变量
- `clear`: 清除屏幕
- `exit`: 退出 shell 或注销。
- `shutdown –h +n`: 系统将在 n 分钟后关机！

### 示例：df
```bash
root> df -h
```
(`df`: 显示文件系统的磁盘占用情况。`-h`: 使输出易于读）

### 示例：mount
```bash
root> mount /cdrom
```
(`mount`: 使 cd-rom 对文件系统可用。）

### 示例：umount
```bash
root> umount /dev/hda1
```
(`umount`: 使 `hda1` 对文件系统不可用。`hda1`: 一个硬盘分区）

### 示例：fsck
```bash
root> fsck
```
(`fsck`: 检查并修复文件系统。）

### 示例：init
```bash
root@user-linux: ~ # init 5
```
(`init 5`: 将系统切换到运行级别 5)

### 示例：who -r
```bash
root@user-linux: ~ # who -r
```
(`who -r`: 显示当前的运行级别。）

### 示例：free
```bash
root@user-linux: ~ # free -m
```
(`free`: 显示空闲磁盘空间 `-m`: 以 MB 为单位显示空闲磁盘空间）

### 示例：du
```bash
root@user-linux: ~ # du –b myfile.txt
```
(`du`: 显示文件或目录的磁盘占用情况。`-b`: 统计它占用的字节数。）

### 示例：export
```bash
root@user-linux: ~ # export newvar=8
```
(`echo $newvar`. 输出是 8)

### 示例：printenv
```bash
root@user-linux: ~ # printenv
```
(`printenv`: 列出环境变量名称和值）

### 示例：unset
```bash
root@user-linux: ~ # unset var
```
(`unset var`: 移除环境变量 `var`。）

### 示例：clear
```bash
user>clear
```
(`clear`: 清除屏幕。）

### 示例：exit
```bash
user>exit
```
(`exit`: 退出 shell 或注销。）

### 示例：shutdown
```bash
root@user-linux: ~ # shutdown –h +5
```
(`shutdown –h +5`: 系统将在 5 分钟后关机！(`-h`: 停止系统 `+n`: n 秒后））

## 总结
- `df`: 显示文件系统的磁盘占用情况
- `mount`: 使设备对文件系统可用
- `umount`: 使设备对文件系统不可用
- `fsck`: 检查并修复文件系统
- `init n`: 将系统切换到运行级别 n
- `who -r`: 显示当前的运行级别
- `free`: 显示空闲磁盘空间
- `du`: 显示文件或目录的磁盘占用情况
- `export`: 设置环境变量
- `printenv`: 列出环境变量名称和值
- `unset`: 移除环境变量
- `clear`: 清除屏幕
- `exit`: 退出 shell 或注销。
- `shutdown –h +n`: 系统将在 n 分钟后关机！

# 第 21 章：帮助命令

| 命令 | 操作与示例 |
| :--- | :--- |
| `man` | 显示命令的帮助手册。例如 `man nice` (显示 `nice` 命令的手册) |
| `info` | 显示命令的信息。例如 `info chmod` (显示关于 `chmod` 命令的信息) |
| `whatis` | 显示命令的描述。例如 `whatis ifconfig` (显示 `ifconfig` 是什么的描述) |
| `help` | 显示命令的帮助解释。例如 `help cd` (显示 `cd` 命令的帮助解释) |
| `apropos` | 搜索手册页中的关键词。例如 `apropos download` (显示包含“download”的手册条目) |
| `--help` | 使用 `-help` 选项获取命令的帮助。例如 `wget --help` (获取 `wget` 命令的帮助) |

**注意：** 如果你熟悉这些帮助命令，你将了解完整的 Linux 命令及其用法。

# 第 22 章：命令技巧

### 利用 Tab 键进行自动补全
Linux 提供了许多不同的命令，我们很容易迷失并忘记其中一个。对我个人来说，这种情况经常发生，但幸运的是这并不是什么麻烦。事实上，Linux 提供了多种方法来找到你遗漏的命令。

知道第一个“技巧”是了解自动补全控制。

### 示例：date 命令
对于 `date` 命令：你现在有点头疼，不知道它是怎么拼写的。根据直觉，你确定命令的第一个或第二个字母是“da”。

只需在控制台中输入 "da"，然后双击键盘左侧的 Tab 键。

通过双击 Tab，你向电脑请求了一列表以 "da" 开头的命令。它们显示了 "dash" 和 "date"。所以有两个以 "da" 开头的命令，你只需要找到你寻找的那个，即 "date"。

非常棒，电脑已经重写了下方的提示符和你输入命令的开头。你只需要补全缺失的字母 "you" 并按回车键，就搞了。:-)

更有趣的是，如果你的搜索只有一个结果，电脑会自动补全缺失的字母，你只需要按回车键了！

### 示例：chsh
如果你想输入 `chsh` 命令但不确定拼写，你只需要在控制台中输入“ch”并按两次 Tab。命令就会魔术般地完成。它会显示 ”chfn, chsh”，然后你可以选择“chfn”。

命令也是如此！

### 命令历史记录
我们经常需要找到几分钟前（甚至是几秒钟前）输入的命令。有时是因为我们忘记了命令，但通常是因为你像我一样，真的懒得重写整个命令。

这个快捷键是金子：按下方向上键；你将看到你输入的上一个命令。

再次按下方向上键，你将看到倒数第二个命令，然后是倒数三个，以此此类推。

如果你按下方向下键，你将返回最近的命令。

因此，我可以倒序找到我刚刚输入的命令：
```bash
ls --all;
ls -a,
ls;
Date;
```
等等等。如果你想在命令历史中回溯非常久以前，不需要像疯子一样狂按上百次方向上键。

有一个 `history` 命令可以提醒你命令历史：

### 示例
```bash
history
```





按下向上方向键；你将看到你输入的上一条命令。然后屏幕将显示：

Date 152 ls ls ls 153 154 155--all -a 156 157 history

你会发现这些控制是有编号的：因此，我们可以知道 `date` 是我在终端中输入的第 152 条命令，而三个 `ls` 分别是第 153、154 和 156 条命令。当然，你输入的上述最后一条命令始终会是 `history`。

### Ctrl + R：查找历史命令

如果使用方向方向键和 `history` 命令不足以找到你输入过的旧命令，有一个超级实用的快捷键：`Ctrl+R`。它可以帮助你找到刚刚使用过的历史命令。因此，同时按下 `Ctrl+R` 键，计算机将切换到“查找已输入的命令”模式（"R" 代表 research，搜索）。

在那里，你可以输入任何与旧命令对应的字母序列。

### 示例：

如果你想查找之前使用过的带有“all”的命令，请按 `Ctrl+R` 并输入 "all"。然后，Linux 将找到包含单词“all”的 `ls --all`。你只需按回车键即可运行该命令！:-)

如果这不是你正在寻找的命令，再次按 `Ctrl + R` 向上移动包含 "all" 的命令列表。

这在这样的驱动器上看起来可能很愚蠢，但有些命令非常长，不需要重新编写它们真是一件乐！

## 使用通配符

你可以在许多 Linux 命令中使用通配符。通配符表示其他字符的符号或符号组合。Linux 命令中有三种通配符：

- `?` 问号（`?`）表示单个字符。
  例如：`b??k` 匹配 bank, beak, back, bilk 或任何以 b 开头并 k 结尾的四字母文件名。
- `*` 星号（`*`）表示任意字符或一组字符，包括零字符或多个字符。
  例如：`b*k` 匹配 bk, bkk, bark, break, backtrack。
- `[ ]` 方括号内的字符（`[ ]`）通常表示集合中的任意字符。但请注意它们是区分大小写的。
  例如：`b[a-z]k` 匹配 bak, bbk, bck, bzk，但不匹配 `bAk`, `bBk`, `bCk`, `bZk`，因为区分大小写敏感。

通配符实际上是在 Linux 命令中实现的。

### 示例：

```bash
user2014@user-linux: ls b??k
```
（通配符 `b??k` 匹配当前目录下的五个文件。输出为“bank beak back bilk bark”）

### 示例：

```bash
user2014@user-linux: ls a*d
```
（通配符 `a*d` 匹配当前目录下的某些文件。输出为“ad add acid abroad abounded abed aid”）

### 示例：

```bash
user2014@user-linux: ls se[a-e]
```
（通配符 `se[a-e]` 匹配当前目录下的五个文件。输出为“sea seb sec sed see”）

## 关于运行级别 (Run Levels)

什么是运行级别？运行级别一术指的是实现 Linux System V 风格初始的操作系统之一的运行模式。通常存在七个运行级别，编号从零到六；启动时只执行一个“运行级别”——运行级别不是顺序执行的，即执行运行级别 2 或 3 或 4，而不是先执行 2 再执行 3 然后 4。

“运行级别”定义了机器启动后的状态。不同的运行级别通常分配给：

0. halt-关机-系统正在关闭过程中。
1. 单用户模式
2. 未启动网络服务的多用户模式
3. 已启动网络服务的多用户模式
4. 系统关机
6. 系统重启

### 示例：

```bash
root@user-linux: ~ # init 3
```
(`init 3`：将系统切换到运行级别 3）

### 总结：

- `Tab` 键可以自动补全缺失的命令。
- `向上方向键` 可以查看历史命令。
- `向下方向键` 可以返回最近的命令。
- `Ctrl+R` 可以通过关键词查找历史命令。
- `?` 问号（`?`）表示单个字符。
- `*` 星号（`*`）表示任意字符或一组字符，包括零字符或多个字符。
- `[ ]` 方括号内的字符（`[ ]`）通常表示集合中的任意字符。但请注意它们是区分大小写的。
- 运行级别数字描述了已初始化并正在运行的服务级别。

# 第 23 章

## 权限

### 什么是 rwx？

在使用 `ls –l` 查看文件的访问权限后，你可以看到类似这样的内容：

`rwx ….. ……`

解释：

`rwx` 表示访问权限，可以用 1 到 7 的数字来描述。真的吗？是的，1 到 7 的数字表示访问权限。

- `r` 代表读取权限，值为 4。
- `w` 代表写权限，值为 2。
- `x` 代表执行权限，值为 1。

反之亦然：

- `4` 表示读取权限 (`r`)
- `2` 表示写权限 (`w`)
- `1` 表示执行权限 (`x`)

### 示例：

如果 `rwx` 值为 4，那么你可以判断出它的权限是只读。
如果 `rwx` 值为 2，那么你可以判断出它的权限是只写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

1 到 7 的数字表示各种访问权限：

- `7` 表示读、写、执行权限 (`7=4+2+1`)
- `6` 表示读、写权限 (`6=4+2`)
- `5` 表示读、执行权限 (`5=4+1`)
- `4` 表示只读权限 (`4=4+0`)
- `3` 表示写、执行权限 (`3=2+1`)
- `2` 表示只写权限 (`2=2+0`)
- `1` 表示只执行权限 (`1=1+0`)

### 示例：

如果 `rwx` 值为 7，那么你可以判断出它的权限是读、写和执行。
如果 `rwx` 值为 6，那么你可以判断出它的权限是读和写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

什么是 `rwx`？
`rwx` 表示访问权限，可以用 1 到 7 的数字来描述。真的吗？是的，1 到 7 的数字表示访问权限。

`r` 代表读取权限，值为 4。
`w` 代表写权限，值为 2。
`x` 代表执行权限，值为 1。

反之亦然：

`4` 表示读取权限 (`r`)
`2` 表示写权限 (`w`)
`1` 表示执行权限 (`x`)

示例：

如果 `rwx` 值为 4，那么你可以判断出它的权限是只读。
如果 `rwx` 值为 2，那么你可以判断出它的权限是只写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

1 到 7 的数字表示各种访问权限：

- `7` 表示读、写、执行权限 (`7=4+2+1`)
- `6` 表示读、写权限 (`6=4+2`)
- `5` 表示读、执行权限 (`5=4+1`)
- `4` 表示只读权限 (`4=4+0`)
- `3` 表示写、执行权限 (`3=2+1`)
- `2` 表示只写权限 (`2=2+0`)
- `1` 表示只执行权限 (`1=1+0`)

### 示例：

如果 `rwx` 值为 7，那么你可以判断出它的权限是读、写和执行。
如果 `rwx` 值为 6，那么你可以判断出它的权限是读和写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

什么是 `rwx`？
`rwx` 表示访问权限，可以用 1 到 7 的数字来描述。真的吗？是的，1 到 7 的数字表示访问权限。

`r` 代表读取权限，值为 4。
`w` 代表写权限，值为 2。
`x` 代表执行权限，值为 1。

反之亦然：

`4` 表示读取权限 (`r`)
`2` 表示写权限 (`w`)
`1` 表示执行权限 (`x`)

示例：

如果 `rwx` 值为 4，那么你可以判断出它的权限是只读。
如果 `rwx` 值为 2，那么你可以判断出它的权限是只写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

1 到 7 的数字表示各种访问权限：

- `7` 表示读、写、执行权限 (`7=4+2+1`)
- `6` 表示读、写权限 (`6=4+2`)
- `5` 表示读、执行权限 (`5=4+1`)
- `4` 表示只读权限 (`4=4+0`)
- `3` 表示写、执行权限 (`3=2+1`)
- `2` 表示只写权限 (`2=2+0`)
- `1` 表示只执行权限 (`1=1+0`)

运行级别数字描述了已初始化并正在运行的服务级别。

# 第 23 章

## 访问

##什么是 rwx？

在使用 `ls –l` 查看文件的访问权限后，你可以看到类似这样的内容：

`rwx ….. ……`

解释：

`rwx` 表示访问权限，可以用 1 到 7 的数字来描述。真的吗？是的，1 到 7 的数字表示访问权限。

- `r` 代表读取权限，值为 4。
- `w` 代表写权限，值为 2。
- `x` 代表执行权限，值为 1。

反之亦然：

- `4` 表示读取权限 (`r`)
- `2` 表示写权限 (`w`)
- `1` 表示执行权限 (`x`)

### 示例：

如果 `rwx` 值为 4，那么你可以判断出它的权限是只读。
如果 `rwx` 值为 2，那么你可以判断出它的权限是只写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

1 到 7 的数字表示各种访问权限：

- `7` 表示读、写、执行权限 (`7=4+2+1`)
- `6` 表示读、写权限 (`6=4+2`)
- `5` 表示读、执行权限 (`5=4+1`)
- `4` 表示只读权限 (`4=4+0`)
- `3` 表示写、执行权限 (`3=2+1`)
- `2` 表示只写权限 (`2=2+0`)
- `1` 表示只执行权限 (`1=1+0`)

### 示例：

如果 `rwx` 值为 7，那么你可以判断出它的权限是读、写和执行。
如果 `rwx` 值为 6，那么你可以判断出它的权限是读和写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

什么是 `rwx`？
`rwx` 表示访问权限，可以用 1 到 7 的数字来描述。真的吗？是的，1 到 7 的数字表示访问权限。

`r` 代表读取权限，值为 4。
`w` 代表写权限，值为 2。
`x` 代表执行权限，值为 1。

反之亦然：

`4` 表示读取权限 (`r`)
`2` 表示写权限 (`w`)
`1` 表示执行权限 (`x`)

示例：

如果 `rwx` 值为 4，那么你可以判断出它的权限是只读。
如果 `rwx` 值为 2，那么你可以判断出它的权限是只写。
如果 `rwx` 值为 1，那么你可以判断出它的权限是只执行。

1 到 7 的数字表示各种访问权限：

- `7` 表示读、写、执行权限 (`7=4+2+1`)
- `6` 表示读、写权限 (`6=4+2`)
- `5` 表示读、执行权限 (`5=4+1`)
- `4` 表示只读权限 (`4=4+0`)
- `3` 表示写、执行权限 (`3=2+1`)
- `2` 表示只写权限 (`2=2+0`)
- `1` 表示只执行权限 (`1=1+0`)

运行级别数字描述了已初始化并正在运行的服务级别。





| 符号 | 说明 |
| :--- | :--- |
| `\|` | 将 `cmd1` 的输出发送到 `cmd2` 的输入，例如 `ls -al /etc` \| `less` |
| `;` | 组合两个或多个命令，例如 `cd~; ls` |
| `\` | 转义特殊字符，例如 `echo -e "\n Hello \t World! \n"` |
| `./` | 在当前目录下运行脚本，例如 `./script.sh` |
| `..` | 上级目录，例如 `cd..` |
| `~` | 目录，例如 `cd~` |
| `$` | 变量名和变量值的变量前缀，例如 `echo $var` |
| `$$` | 显示当前运行的进程数，例如 `echo $$` |
| `!!` | 重复上一次命令，例如 `!!` |
| `!string` | 运行最近以字符串开头的 `cmd`，例如 `!cat` |

# 第 25 章

## 快捷键

| 键位 | 说明 |
| :--- | :--- |
| `CTRL+B` | 光标向后移动一个字符长度。 |
| `CTRL+C` | 取消正在运行的命令或杀死运行中的进程。 |
| `CTRL+D` | 退出当前会话。类似于 `exit` 命令。 |
| `CTRL+F` | 光标向前移动一个字符长度。 |
| `CTRL+H` | 删除向后的一个字符。类似于按下退格键（backspace）。 |
| `CTRL+P` | 将上一行或几行粘贴到指定的 Location。 |
| `CTRL+R` | 输入以显示最近的命令，返回历史命令列表 |
| `CTRL+S` | 停止屏幕上所有的输出。通过锁定终端输出来冻结 shell。 |
| `CTRL+Q` | 恢复屏幕上所有已停止的输出，继续终端输出。 |
| `CTRL+U` | 删除光标所在的整行。 |
| `CTRL+W` | 删除最近输入的最后一个单词。 |
| `CTRL+Z` | 挂起正在运行的进程。如果想恢复，请使用 `fg` 或 `bg` 命令。 |

# 第 26 章

## 运行级别表

| 运行级别 | same |
| :--- | :--- |
| `0` | 停止系统。当当前级别为此级别时，系统正处于关闭过程中。 |
| `1` | 单用户模式。仅运行一小部分内核进程。几乎所有其他服务均已禁用。 |
| `2` | 基础多用户模式。此级别启动大多数服务，但未启用网络连接服务。 |
| `3` | 完整多用户模式。此级别启动包括网络连接在内的所有服务，但不会启动 X 窗口。 |
| `4` | 用户定义模式。运行级别 4 没有常规定义。它完全开放给用户配置。 |
| `5` | 带有 X 窗口的完整多用户模式。启动所有启用的服务以及 Linux 图形桌面环境。 |
| `6` | 重启。当当前级别为此级别时，系统正在重启过程中。 |

# 第 27 章

## Vi 编辑器命令

| 命令 | 操作 |
| :--- | :--- |
| `h,l,k,j` | 光标左、右、上、下移动 |
| `w,b` | 光标向前、向后移动 |
| `0` | 跳到行首 |
| `$` | 跳到行尾 |
| `G` | 跳到文件最后一行 |
| `J` | 将当前行与下一行合并 |
| `z` | 撤销上一次命令 |
| `.` | 重复上次命令 |
| `ZZ` | 保存文件并退出 |
| `i` | 在光标字符前插入 |
| `I` | 在行首插入字符 |
| `a` | 在光标字符后追加 |
| `A` | 在行尾追加字符 |
| `c` | 修改直到…… |
| `C` | 修改到行尾 |
| `d` | 删除直到…… |
| `D` | 删除到行尾 |
| `r` | 替换一个字符 |
| `R` | 替换多个字符 |
| `o` | 在下方开启新行 |
| `O` | 在上方开启新行 |
| `esc` | 退出插入模式，进入命令模式 |
| `x` | 删除光标处的字符 |
| `X` | 删除左侧的字符 |
| `u` | 撤销上次修改 |
| `.` | 重做上次修改 |
| `U` | 恢复行 |
| `m` | 标记位置 |
| `M` | 屏幕中间位置 |
| `dw` | 删除当前单词 |
| `dd` | 删除当前行 |
| `cc` | 修改当前行 |
| `f x` | 在当前行查找 `x` |
| `F x` | 在上一行查找 `x` |
| `/string` | 搜索字符串，向前查找 |
| `?string` | 搜索字符串，向后查找 |
| `[n]G` | 跳到行号 “n” |
| `n` | 向前搜索下一个匹配 |
| `N` | 向后搜索下一个匹配 |
| `p` | 将行粘贴到当前行下方 |
| `P` | 将行粘贴到当前行上方 |
| `t` | 直到…… |
| `T` | 向后直到…… |
| `s` | 替换 |
| `S` | 替换整行 |
| `ZZ` | 保存并退出 |
| `:e` | 编辑文件 |
| `:e!` | 放弃文件修改 |
| `:$` | 跳到文件最后一行 |
| `:number` | 跳到行号 |
| `:w` | 写入并保存 |
| `:w!` | 保存只读文件 |
| `:w filename` | 使用新文件名保存 |
| `:wq` | 写入、保存并退出 |
| `:n` | 转到下一个文件 |
| `:rew` | 回到第一个文件 |
| `:q` | 使用 `:w` 保存后退出 |
| `:q!` | 不保存直接退出 |
| `:r filename` | 读取文件，在光标位置插入文件 |
| `:! command` | 运行 shell 命令 |
| `:sh` | 运行临时 shell |

# 第 28 章

## 所有常用 Linux 命令

注意：
- `cmd` 意味着命令
- `regex` 意味着正则表达式
- `(*)` 意味着 root 用户运行的命令

| 命令 | 操作与示例 |
| :--- | :--- |
| `a2p` | 将 `awk` 转换为 perl 文件，例如 `a2p myfile.awk > myfile.pl`（将 `myfile.awk` 转换为 `myfile.pl`） |
| `alias` | 为命令创建另一个名称，例如 `alias p="pwd"`（将 `p` 设置为 `pwd` 的别名） |
| `apropos` | 在帮助页中查看搜索词，例如 `apropos find`（列出帮助页中包含 "find" 的条目） |
| `apropos -e` | 在帮助页中查看精确搜索词，例如 `apropos –e nice` (-e: 在帮助页中显示精确词汇) |
| `apt-get` | 安装、删除或更新包，例如 `apt-get install libc6`（安装 `libc6` 包） |
| `aspell` | 检查并纠正拼写错误，例如 `aspell -c test.txt` (-c:检查 `test.txt` 文件中的拼写） |
| `at` | 在指定时间运行任务 |
| `awk` | 通过正则表达式匹配文本，例如 `awk '$0'`（行的长度） |
| `basename` | 显示路径的最后部分，例如 `basename /home/foo/file.txt` |
| `bc` | 执行计算，例如 `bc+9` |
| `bg` | 在后台恢复挂起的作业，例如 `bg %3` |
| `bunzip2` | 从 zip 格式解压，例如 `bunzip2 myfile.tar` |
| `bzip2` | 将文件压缩为 zip 格式，例如 `bzip2 myfile.dat` |
| `cal` | 显示日历，例如 `cal 2014` |
| `cal -3` | 显示 3 个月，例如 `cal -3`（月份） |
| `cat` | 显示一个或多个文件的内容，例如 `cat file1.txt file2.txt` |
| `cat -n` | 带行号显示内容，例如 `cat -n myfile.txt` |
| `cd` | 切换目录，例如 `cd /home/user/mydir` |
| `chattr` | 为文件设置属性，例如 `chattr +i myfile.txt` (+i 使文件变为只读） |
| `chfn` | 更改用户信息，例如 `chfn`（更改用户） |
| `chfn -f` | 更改全名，例如 `chfn -f Full-Name` (-f: 全名) |
| `chgrp` | 更改组所有，例如 `chgrp groupname /usr/myfile.txt` |
| `chkconfig` | 查看和修改运行级别文件，例如 `chkconfig --list` (-list: 列出运行级别的服务） |
| `chmod` | 修改访问权限，例如 `chmod 755 filename`（设置文件权限为 755） |
| `chown` | 更改文件或目录的所有者，例如 `chown username myfile.txt`（更改 `myfile.txt` 所有者） |
| `chpasswd` | 更改用户密码，例如 `chpasswd`（然后输入用户名：密码） |
| `chsh` | 更改用户的登录 shell，例如 `chsh -s /bin/bash` (-s 指定登录 shell) |
| `cksum` | 生成 CRC 校验和数字，例如 `cksum file.txt`（输出 `file.txt` 的校验和） |
| `clear` | 清除屏幕，例如 `clear`（清除 shell 窗口） |
| `cmp` | 按字节比较两个文件，例如 `cmp first.txt second.txt`（比较 `first.txt` 和 `second.txt`） |
| `collectl` | 监控当前系统状态，例如 `collectl`（列出 cpu、sys、inter 信息） |
| `comm` | 按行比较两个文件的文本，例如 `comm first.txt second.txt`（比较 `first.txt` `second.txt`） |
| `cp` | 将文件复制到另一个目录，例如 `cp myfile.txt /mydir`（将 `myfile.txt` 复制到 `mydir`） |
| `cp -p` | 将文件复制到另一个目录，例如 `cp -p myfile.txt /mydir` (-p: 保留原始权限） |





| 命令 | 说明 |
| :--- | :--- |
| `cp -a` | 将文件（或）复制到另一个目录，例如 `cp –a myfile.txt /mydir` (`-a`: 保留原始属性） |
| `cpio -o` | 输出归档的 cpio 文件，例如 `cpio -o > directory.cpio` (`-o`: 备份到归档 cpio 文件） |
| `cpio -i` | 归归档的 cpio 文件，例如 `cpio -i < directory.cpio` (`-i`: 从归档 cpio 文件中恢复） |
| `crontab` | 创建在指定时间运行的作业，例如 `crontab`（设置按固定间隔运行作业） |
| `crontab -e` | 在指定时间运行周期性作业，例如 `crontab -e` (`-e` 允许编辑 crontab 文件） |
| `crontab -l` | 在指定时间运行周期性作业，例如 `crontab -l` (`-l`: 列出 crontab 文件） |
| `crontab -r` | 在指定时间运行周期性作业，例如 `crontab -r` (`-r`: 删除 crontab 文件） |
| `csplit` | 将文件拆分为一些分离的文件，例如 `csplit myfile.txt ”/part1/” “/part2/`（分离命名为 `xx00`, `xx01` 的文件） |
| `cut -d` | 显示文件中指定的字段，例如 `cut –d “:” myfile.txt` (`-d`: 指定字段分隔符 `:`） |
| `cut -c` | 从文件中提取内容，例如 `cut –c 6 myfile.txt` (`-c6`: 每行的第 6 个字符） |
| `cut -f` | 从文件中提取内容，例如 `cut –f 3 myfile.txt` (`-f3`: 指定字段编号为 3） |
| `date` | 显示日期和时间，例如 `date`（显示当前日期和时间） |
| `date -s` | 设置日期和时间，例如 `date -s "11/20/2014"` (`-s` 设置日期） |
| `dc` | 打开命令行桌面计算器，例如 `dc` (`dc` 意味着桌面计算器） |
| `dd` | 数据转储，用于转换和复制文件，例如 `dd if=/dev/sda of=/dev/sdb`（从 `sda` 复制数据到 `sdb`） |
| `dmesg` | 打印所有内核日志消息，例如 `dmesg > kmsg.txt`（将内核消息输出到 `kmsg.txt`） |
| `df` | 显示空磁盘空间，例如 `df`（显示文件系统空空间） |
| `df -m` | 显示空磁盘空间，例如 `df -m` (`-m`: 以 Mb 显示大小） |
| `dhclient` | 配置网络接口，例如 `dhclient eth0`（刷新 `eth0` 的 IP 地址） |
| `diff` | 显示两个文件之间的差异，例如 `diff firstfile.txt secondfile.txt`（显示两个文件之间的差异） |
| `diff3` | 显示三个文件之间的差异，例如 `diff3 file1.txt file2.txt file3.txt`（显示三个文件之间的差异） |
| `dig` | 显示 DNS 器的详情，例如 `dig xvxaxx.com`（列出关于 `xvxaxx.com` 的信息） |
| `dir` | 显示目录内容，例如 `dir`（显示当前目录内容） |
| `dircolors` | 显示 `ls` 命令的颜色设置，例如 `dircolors`（显示 `ls` 的目录颜色） |
| `dirname` | 去文件路径的最后部分，例如 `dirname /foo/bar/baz/myfile.txt`（输出：`/foo/bar/baz`） |
| `du -s` | 显示磁盘占用，例如 `du -s *.*` (`-s` 列出当前目录下的文件大小） |
| `du -h` | 显示磁盘占用，例如 `du -h myfile.txt` (`-h`: 显示人类可读的单位） |
| `dump -f` | 创建文件系统的备份，例如 `dump -f0 filebk /mydir` (`-f`:备份-0:转储级别 `filebk`: 转储文件） |
| `echo` | 在标准输出上显示输入，例如 `echo “Hello World!”`（显示 `Hello World!`） |
| `echo -e` | 使用转义序列显示文本，例如 `echo –e "\n Hello World!”` (`-e`: 允许使用 `\n` 显示文本） |
| `ed` | 打开命令行文本编辑器，例如 `ed myfile.txt`（用文本编辑器打开 `myfile.txt`） |
| `egrep` | 搜索文件中指定的正则表达式，例如 `egrep "new | string" myfile.txt`（在 `myfile.txt` 中搜索 `new | string`） |
| `eject` | 弹出 cd 或 dvd 托盘，例如 `eject cdrom`（弹出 `cdrom` 盘） |
| `eject -t` | 弹出或关闭 cd 或 dvd 托盘，例如 `eject –t cdrom` (`-t`: 关闭打开的 cdrom 盘） |
| `emacs` | 强大的可扩展文件编辑器，例如 `emacs file.txt`（启动 `emacs` 并打开 `file.txt`） |
| `env` | 显示、设置环境变量，例如 `env`（列出当前环境变量） |
| `eval` | 根据其参数创建命令，例如 `UPLS=”eval cd.. ; ls ”`（创建一个名为 `UPLS` 的命令） |
| `exit` | 退出 shell，例如 `exit`（终止程序并退出） |
| `expand` | 将制表符转换为空格，例如 `expand myfile.txt`（将 `myfile.txt` 中的制表符转换为空格） |
| `expand -t` | 将制表符转换为空格，例如 `expand -t 3 myfile.txt` (`-t`: 设置制表间隔 3 个字符） |
| `export` | 设置环境变量和值，例如 `export newvar=8 echo $newvar`（输出：8） |
| `expr` | 评估表达式，例如 `expr 10+8`（输出：18） |
| `factor` | 显示数字的质因数，例如 `factor 1001`（输出：7 11 13） |
| `fc` | 列出、编辑、重新执行上一个命令，例如 `fc -l` (`-l`:列出命令历史） |
| `fdisk` | 纵硬盘分区，例如 `fdisk /dev/hdb`（列出硬盘分区信息） |
| `fg` | 在前台恢复已停止的作业，例如 `fg %3`（在前台恢复作业 3） |
| `fgrep` | 在文件中搜索指定的字符串，例如 `fgrep "good" myfile.txt`（在 `myfile.txt` 中搜索 `good`） |
| `file` | 检测文件类型，例如 `file myfile.tar`（确定 `myfile.tar` 的文件类型） |
| `find –print–name` | 在名为 dir 的目录中查找文件，例如 `find –print–name`（在 dir 中查找文件名） |
| `file` | 显示文件的类型信息，例如 `file myfile.tar`（确定 `myfile.tar` 的类型） |
| `fmt` | 格式化文本，例如 `fmt myfile.txt`（格式化 `myfile.txt`） |
| `fmt -u` | 统一格式化文本，例如 `fmt -u myfile.txt`（`-u`: 统一格式化） |
| `fold` | 限制文本宽度，例如 `fold -w 80 myfile.txt`（将 `myfile.txt` 宽度限制为 80） |
| `fold -s` | 在空白处折行，例如 `fold -s myfile.txt`（`-s`: 在空白处折行） |
| `head` | 查看文件的开头部分，例如 `head myfile.txt`（显示 `myfile.txt` 的前 10 行） |
| `head -n` | 显示文件开头几行，例如 `head -n 20 myfile.txt`（`-n`: 显示前 20 行） |
| `tail` | 查看文件的结尾部分，例如 `tail myfile.txt`（显示 `myfile.txt` 的最后 10 行） |
| `tail -n` | 显示文件结尾几行，例如 `tail -n 5 myfile.txt`（`-n`: 显示最后 5 行） |
| `tail -f` | 持续跟踪文件变化，例如 `tail -f myfile.txt`（实时查看 `myfile.txt` 的变化） |
| `wc` | 统计文件计数，例如 `wc myfile.txt`（统计 `myfile.txt` 的行、字、字节） |
| `wc -l` | 统计行数，例如 `wc -l myfile.txt`（统计 `myfile.txt` 的行数） |
| `wc -w` | 统计单词数，例如 `wc -w myfile.txt`（统计 `myfile.txt` 的单词数） |
| `wc -c` | 统计字节数，例如 `wc -c myfile.txt`（统计 `myfile.txt` 的字节数） |
| `sort` | 对文件排序，例如 `sort myfile.txt`（对 `myfile.txt` 进行行排序） |
| `sort -r` | 反向排序，例如 `sort -r myfile.txt`（`-r`: 逆序排序） |
| `sort -n` | 按数字排序，例如 `sort -n myfile.txt`（`-n`: 按数值排序） |
| `sort -u` | 排序并合并重复项，例如 `sort -u myfile.txt`（`-u`: 排序并去重） |
| `uniq` | 过滤相邻重复行，例如 `uniq myfile.txt`（合并 `myfile.txt` 中相邻的重复行） |
| `uniq -c` | 统计出现次数，例如 `uniq -c myfile.txt`（`-c`: 显示每行出现的次数） |
| `uniq -d` | 只显示重复的行，例如 `uniq -d myfile.txt`（`-d`: 只输出重复行） |
| `sed` | 流编辑器，例如 `sed 's/old/new/g' myfile.txt`（将 `myfile.txt` 中的 `old` 替换为 `new`） |
| `sed -i` | 直接修改文件，例如 `sed -i 's/old/new/g' myfile.txt`（`-i`: 原地直接修改文件） |
| `grep` | 在文件中搜索模式，例如 `grep "pattern" myfile.txt`（在 `myfile.txt` 中搜索 `pattern`） |
| `grep -i` | 忽略大小写搜索，例如 `grep -i "pattern" myfile.txt`（`-i`: 忽略大小写） |
| `grep -v` | 反向搜索模式，例如 `grep -v "pattern" myfile.txt`（`-v`: 显示不匹配模式的行） |
| `grep -r` | 递归搜索，例如 `grep -r "pattern" .`（在当前目录及其子目录搜索 `pattern`） |
| `grep -n` | 显示行号，例如 `grep -n "pattern" myfile.txt`（`-n`: 显示匹配行的行号） |
| `grep -l` | 只列出匹配的文件名，例如 `grep -l "pattern" *.txt`（`-l`: 列出包含模式的文件名） |
| `grep -E` | 使用扩展正则表达式，例如 `grep -E "p1|p2" myfile.txt`（`-E`: 使用扩展正则） |
| `awk` | 文本处理语言，例如 `awk '{print $1}' myfile.txt`（打印 `myfile.txt` 的第一列） |
| `awk -F` | 指定分隔符，例如 `awk -F ':' '{print $1}' myfile.txt`（`-F`: 指定冒号为分隔符） |
| `tr` | 翻译或删除字符，例如 `tr 'a-z' 'A-Z' < file.txt`（将小写转为大写） |
| `tar` | 归档工具，例如 `tar -cvf archive.tar dir/`（将 `dir/` 创建为 `archive.tar`） |
| `tar -xvf` | 解归档，例如 `tar -xvf archive.tar`（解压 `archive.tar`） |
| `tar -zcf` | 使用 gzip 压缩，例如 `tar -zcf archive.tar.gz dir/`（`-z`: 使用 gzip 压缩） |
| `tar -zxvf` | 解压 gzip 压缩包，例如 `tar -zxvf archive.tar.gz`（`-z`: 解压 gzip 压缩包） |
| `zip` | 压缩文件，例如 `zip archive.zip file1`（将 `file` 压缩为 `archive.zip`） |
| `unzip` | 解压缩 zip 文件，例如 `unzip archive.zip`（解压 `archive.zip`） |
| `gzip` | 压缩文件，例如 `gzip file.txt`（将 `file.txt` 压缩为 `file.txt.gz`） |
| `gunzip` | 解压缩文件，例如 `gunzip file.txt.gz`（解压 `file.txt.gz` 还原为 `file.txt`） |
| `ls` | 列出目录内容，例如 `ls`（显示目录内容） |
| `ls -l` | 以详细格式列出，例如 `ls -l`（显示权限、所有者、大小、时间等信息） |
| `ls -a` | 显示隐藏文件，例如 `ls -a`（`-a`: 显示以 `.` 开头的文件） |
| `ls -h` | 以可读格式显示，例如 `ls -lh`（`-h`: 以 KB, MB 等单位显示大小） |
| `ls -t` | 按时间排序，例如 `ls -lt`（`-t`: 按修改时间排序） |
| `mkdir` | 创建目录，例如 `mkdir new_dir`（创建一个名为 `new_dir` 的目录） |
| `mkdir -p` | 递归创建目录，例如 `mkdir -p a/b/c`（`-p`: 如果父目录不存在则自动创建） |
| `rm` | 删除文件，例如 `rm file.txt`（删除 `file.txt`） |
| `rm -r` | 递归删除目录，例如 `rm -r dir_name`（`-r`: 递归删除目录及其所有内容） |
| `rm -f` | 强制删除，例如 `rm -f file.txt`（`-f`: 不提示强制删除） |
| `mv` | 移动或重命名文件，例如 `mv old.txt new.txt`（将 `old.txt` 重命名为 `new.txt`） |
| `mv` | 移动文件，例如 `mv file.txt /tmp/`（将 `file.txt` 移动到 `/tmp/`） |
| `touch` | 创建空文件或更新时间，例如 `touch file.txt`（创建一个空的 `file.txt`） |
| `pwd` | 显示当前工作路径，例如 `pwd`（显示你当前在哪个目录） |
| `cd` | 目录，例如 `cd /home/user`（切换到指定目录） |
| `cd ..` | 返回上级目录，例如 `cd ..`（进入上一层目录） |
| `cd ~` | 返回主目录，例如 `cd ~`（返回当前用户主目录） |
| `clear` | 清空终端屏幕，例如 `clear`（清空显示内容） |
| `history` | 查看命令历史，例如 `history`（显示最近执行过的命令列表） |
| `alias` | 设置别名，例如 `alias ll='ls -l'`（为 `ls -l` 设置别名 `ll`） |
| `unalias` | 取消别名，例如 `unalias ll`（取消别名） |
| `whoami` | 显示当前用户名，例如 `whoami`（显示当前登录的用户） |
| `who` | 显示登录的用户，例如 `who`（显示当前登录系统用户） |
| `uptime` | 显示系统运行时间，例如 `uptime`（显示系统运行了多久、负载等） |
| `free` | 显示内存使用情况，例如 `free`（显示物理内存和交换内存） |
| `top` | 实时显示系统进程，例如 `top`（动态监控系统资源和进程） |
| `htop` | 交互式进程查看器，例如 `htop`（比 top 更直观的监控工具） |
| `ps` | 显示当前进程状态，例如 `ps aux`（显示所有运行中的进程） |
| `kill` | 杀死进程，例如 `kill 1234`（杀死 PID 为 1234 的进程） |
| `kill -9` | 强制杀死进程，例如 `kill -9 1234`（`-9`: 使用 SIGKILL 强制终止） |
| `pgrep` | 查找进程 PID，例如 `pgrep "python"`（查找包含 "python" 的进程 ID） |
| `killall` | 按名称杀死进程，例如 `killall firefox`（杀死所有名为 firefox 的进程） |
| `sleep` | 暂停指定时间，例如 `sleep 10`（暂停 10 秒） |
| `wait` | 等进程退出状态，例如 `wait`（等待后台作业完成） |
| `|` | 管道，例如 `ls | grep ".txt"`（将 `ls` 的输出传给 `grep`） |
| `>` | 重定向输出，例如 `echo "hello" > file.txt`（将输出写入 `file.txt`，覆盖原有） |
| `>>` | 追加输出，例如 `echo "hello" >> file.txt`（将输出追加到 `file.txt` 末尾） |
| `2>` | 重定向错误，例如 `command 2> error.log`（将标准错误重定向到文件） |
| `> file 2>&1` | 同时重定向输出和错误，例如 `command > out.log 2>&1`（将输出和错误都重定向到文件） |




## 常用 Linux 命令列表

- `join`: 合并具有共同字段的文件行。例如：`join myfile1.txt myfile2.txt`（通过相同字段合并两个文件的行）
- `join`: 合并两个文件。例如：`join -i myfile1.txt myfile2.txt` (`-i`: 忽略差异）
- `kill`: 通过编号停止作业。例如：`kill %3`（终止作业 %3）
- `kill`: 通过进程 ID（pid）停止进程。例如：`kill 3956`（终止进程 3956）
- `killall`: 通过名称停止进程。例如：`killall norespond`（终止进程 norespond）
- `last`: 显示最近登录的用户。例如：`last`（列出最近用户的日期、时间……）
- `lastb`: 显示失败的登录尝试。例如：`lastb`（显示失败的登录尝试）
- `lastlog`: 显示最后登录信息。例如：`lastlog -u username` (`-u`: 指定用户）
- `less`: 分页显示内容。例如：`less myfile.txt`（分页显示 myfile.txt）
- `let`: 对 shell 变量进行算运算。例如：`let a=12; let a=a+8; echo $a`（输出：20）
- `link`: 创建文件的链接。例如：`link file1.txt file2.txt`（创建从 file1 到 file2 的链接）
- `ln`: 创建文件的硬链接。例如：`~/myfile.txt`（为 myfile.txt 创建硬链接）
- `ln -s`: 在两个文件之间创建链接。例如：`ln -s file1.txt file2.txt`（为 file1/file2 创建符号链接）
- `locate`: 查找文件或目录的位置。例如：`locate myfile.txt`（在本地机器上查找 myfile.txt）
- `logname`: 显示当前用户的登录名。例如：`logname`（显示用户的登录名）
- `look`: 显示匹配给定前缀的单词。例如：`look ab`（输出：aba, abb, abc, abd……）
- `lpc`: 运行行打印控制程序。例如：`lpc status`（显示当前打印队列的状态）
- `lpq`: 显示打印机队列状态。例如：`lpq`（列出打印队列）
- `lpr`: 向打印机发送打印请求。例如：`lpr myfile.txt`（将 myfile.txt 发送到打印机）
- `lprm`: 取消打印队列中的打印作业。例如：`lprm 2`（移除打印作业 2）
- `ls`: 列出当前目录的内容。例如：`ls`（列出文件和子目录）
- `ls -l`: 详细列出当前目录的内容。例如：`ls -l` (`-l`: 包含权限的长列表）
- `ls -a`: 列出所有条目包括隐藏文件。例如：`ls -a` (`-a`: 显示所有文件）
- `ls -t`: 按时间戳列出条目。例如：`ls -t` (`-t`: 按时间显示）
- `ls -lh`: 列出当前目录的内容。例如：`ls -lh` (`-lh`: 以 mb 和 gb 单位列出文件）
- `lsattr`: 列出文件或目录的属性。例如：`lsattr myfile.txt`（显示 myfile.txt 属性）
- `lsof`: 列出打开的文件。例如：`lsof`（列出所有打开的文件）

（ 待续 ）

- `man`: 从手册中获取命令帮助。例如：`man cat`（显示 cat 的手册页）
- `man -k`: 在手册页中搜索关键词。例如：`man -k printf` (`-k`: 指定关键词）
- `md5sum`: 创建 md5 校验和。例如：`md5sum -c file.txt` (`-c`: 根据校验和验证文件）
- `mesg`: 启用或禁用消息功能。例如：`mesg`（显示当前的写入状态）
- `mesg y/n`: 启用或禁用消息功能。例如：`mesg y/n` (`y or n`: 允许或拒绝消息）
- `mail`: 发送接收邮件。例如：`mail ray@websprogram.com`（向 ray@websprogram.com 发送邮件）
- `mkdir`: 创建新目录。例如：`mkdir mydir`（创建一个名为 mydir 的目录）
- `mknod`: 创建设备文件。例如：`mknod /dev/dk b 45 0` (`dk`:设备;`b`:块设备; `45`:主设备号; `0`:从设备号）
- `more`: 一次显示屏幕内容。例如：`more +2 myfile.txt` (`+2`: 从第 2 行开始）
- `mount`: 挂载存储设备。例如：`mount /dev/cd`（挂载设备 cd）
- `mount -l`: 挂载或显示设备。例如：`mount -l` (`-l`: 列出所有挂载的设备）
- `mt`: 磁带驱动控制。例如：`mt -f /dev/tape eod` (`-f`: 选择文件；eod：数据末尾）
- `mv`: 将文件移动到另一个目录。例如：`mv myfile.txt /home/user/mydir`（将 myfile.txt 移动到 mydir）
- `mv`: 重命名文件。例如：`mv myfile1.txt myfile2.txt`（将 myfile1.txt 重命名为 myfile2.txt）
- `netstat`: 显示网络状态。例如：`netstat`（打印网络连接、路由表等）
- `nice`: 设置作业优先级。例如：`nice -19`（将优先级设置为 19）
- `nl`: 为文本添加编号。例如：`nl mylist.txt`（为 mylist.txt 编号）
- `nohup`: 忽略挂断信号。例如：`nohup command`（忽略挂断）
- `nslookup`: 查询服务器。例如：`nslookup example.com`（返回 example.com 的 IP）
- `passwd`: 修改用户密码。例如：`passwd username`（修改 username 的密码）
- `paste`: 合并多个文件的行。例如：`paste file1.txt file2.txt`（合并 file1 和 file2）
- `pidof`: 显示运行程序的进程 ID。例如：`pidof console`（显示 console 的进程 ID）
- `ping`: 向主机发送数据并等待响应。例如：`ping example.com`（测试远程主机是否可访问）
- `ping -c`: 测试远程主机是否可访问。例如：`ping -c 5` (`-c`: 指定 ping 次数）
- `pkill`: 杀死运行的进程。例如：`pkill firefox`（停止浏览器）
- `pr`: 为打印准备文件。例如：`pr myfile.txt`（准备打印 myfile.txt）
- `pr -n`: 为打印准备文件。例如：`pr -n myfile.txt` (`-n`: 指定行数）
- `pr -h`: 为打印准备文件。例如：`pr -h myfile.txt` (`-h`: 指定页眉）
- `printenv`: 显示环境变量。例如：`printenv`（列出环境变量的值）
- `printf`: 格式化并打印数据。例如：`printf "start"`（退格符）
- `printf`: 格式化并打印数据。例如：`printf "hello\n"`（换行符）
- `ps -f`: 显示进程状态。例如：`ps -f` (`-f`: 当前进程完整信息）
- `ps -u`: 显示进程状态。例如：`ps -u ray` (`-u`: 指定用户的当前进程）
- `pstree`: 以树形结构显示进程。例如：`pstree`（以树的形式显示所有进程）
- `pwd`: 打印工作目录。例如：`pwd`（显示当前目录）
- `rcp`: 在两个主机之间远程拷贝文件。例如：`rcp file.txt host2:/dir2/file.txt`（将 file.txt 远程拷贝到 host2）
- `read`: 从标准输入读取行。例如：`read name; echo "$name"`（输入 ray，输出 ray）
- `reboot`: 重启系统。例如：`reboot`（导致重启）
- `renice`: 修改作业优先级。例如：`renice 3 23001`（将作业 23001 的优先级设置为 3）
- `restore`: 从备份文件恢复数据。例如：`restore -f databackup` (`-f`: 指定备份文件）
- `rlogin`: 远程登录系统。例如：`rlogin -l username domain.com` (`-l`: 指定用户名）
- `rm`: 删除一个或多个文件。例如：`rm myfile.txt`（删除 myfile.txt）
- `rm -r`: 删除非空目录。例如：`rm -r /NonEmptyDir` (`-r`: 删除目录及其内容）
- `rm -i`: 删除非空目录或文件。例如：`rm -i myfile.txt` (`-i`: 删除前询问）
- `rmdir`: 删除空目录。例如：`rmdir /emptydir`（删除不含内容的目录）
- `route`: 显示或修改 IP 路由表。例如：`route -n` (`-n`: 以数字格式显示）
- `rsync`: 远程同步文件。例如：`rsync myfile host2:/dir2/myfile`（与远程 host2 同步 myfile）
- `scp`: 在两个主机之间安全拷贝文件。例如：`scp file.txt host2:/dir2/file.txt`（将文件安全拷贝到远程主机 host2）
- `screen`: 打开终端窗口管理器。例如：`screen`（开启一个新会话）
- `sdiff`: 并排显示两个文件的差异。例如：`sdiff myfile1.txt myfile2.txt`（并排比较两个文件）
- `sed`: 过滤和转换输入文本。例如：`sed "{print $3}" myfile.txt`（显示每行的第三个单词）
- `seq`: 在给定范围内列出序列。例如：`seq 1 8`（输出：1 2 3 4 5 6 7 8）
- `seq -w`: 在给定范围内列出序列。例如：`seq -w 1 3` (`-w`: 补零，输出：01 02 03）
- `seq`: 在给定范围内列出序列。例如：`seq -s| 1 3` (`-s`: 使用分隔符，输出：1|2|3）
- `set`: 设置 shell 变量或函数。例如：`set n=`who am i`; echo $n`（输出：who am i）
- `sftp`: 通过 ftp 安全传输文件。例如：`sftp ServerURL`（向 Server 安全传输文件）
- `shopt`: 显示 shell 选项设置。例如：`shopt`（显示 shell 行为设置）





| 命令 | 说明 | 示例 |
| :--- | :--- | :--- |
| `shutdown -h` | 关闭系统 | 例如 `shutdown -h +5` (-h+5: 在 5 分钟后停机) |
| `shutdown -r` | 关机并重启 | 例如 `shutdown -r now` (-r: 关机并立即重启) |
| `sleep` | 暂停指定的时间 | 例如 `sleep 10` (暂停 10 秒) |
| `sort` | 按字母顺序显示排序后的内容 | 例如 `sort -r myfile.txt` (-r: 逆序对文件排序) |
| `split -b` | 按指定大小将文件分成多个文件 | 例如 `split -b 11 file.txt` (将文件拆分成多个大小为 11 字节的文件，命名为 `xaa`、`xab`、`xac` 等) |
| `split -l` | 按指定行数将文件分成多个文件 | 例如 `split -l 8 file.txt` (将文件拆分成多个大小为 8 行的文件，命名为 `xaa`、`xab`、`xac` 等) |
| `ssh` | 登录到远程安全 shell | 例如 `ssh ray@myexample.com` (安全地连接到远程主机) |
| `ssh -l` | 登录到远程安全 shell | 例如 `ssh -l username hostname` (-l: 指定你的远程用户名) |
| `stat` | 列出关于文件大小、访问等的状态 | 例如 `stat myfile.txt` (显示 `myfile.txt` 的统计信息) |
| `su` | 切换用户 | 例如 `su user2` (切换到名为 `user2` 的用户) |
| `su -l` | 以 root 超用户身份登录 | 例如 `su -l` (-l: 输入密码，登录 root 账户) |
| `sudo -u` | 以其他用户的身份执行命令 | 例如 `sudo -u user2 ls /home/mydir` (-u: 指定由 `user2` 执行 `ls` 命令) |
| `sudo -v` | 刷新身份验证超时 | 例如 `sudo -v` (下次 `sudo` 将不再需要密码) |
| `sudo -k` | 使身份验证超时过期 | 例如 `sudo -k` (下次 `sudo` 将需要密码) |
| `sum` | 使用校验和汇总文件 | 例如 `sum myfile.txt` (为 `myfile.txt` 创建校验和) |
| `suspend` | 挂起运行中的 shell | 例如 `suspend` (在执行期间暂停系统) |
| `sync` | 将磁盘数据与内存同步 | 例如 `sync` (将所有文件系统缓冲区刷新到磁盘) |
| `tac` | 逆序显示文件的行 | 例如 `tac myfile.txt` (从最后一行到第一行打印文件) |
| `tail` | 显示文件的最后部分 | 例如 `tail -n 20 file.txt` (-n20: 输出 `myfile.txt` 的最后 20 行) |
| `talk` | 与另一个用户通信 | 例如 `talk ray` (与用户 `ray` 通信) |
| `tar -xf` | 提取归档的 tar 文件 | 例如 `tar -xf archive.tar` (-xf: 提取 tar 归档文件) |
| `tar -cf` | 创建归档的 tar 文件 | 例如 `tar -cf archive.tar` (-cf: 创建 tar 归档文件) |
| `tee` | 输出标准输出并写入文件 | 例如 `sort file1.txt | tee file2.txt` (排序 `file1.txt` 并写入 `file2.txt`) |
| `tee -a` | 输出标准输出并写入文件 | 例如 `sort file1.txt | tee -a file2.txt` (-a: 追加内容而非覆盖) |
| `test` | 计算布尔表达式 | 例如 `[ 8 -gt 6 ]; echo $?` (输出: 0 0:真; 1:假) |
| `test` | 计算布尔表达式 | 例如 `[ 5 -eq 6 ]; echo $?` (输出: 1 0:真; 1:假) |
| `time` | 显示运行程序所需的时间 | 例如 `time ftp` (显示执行 `ftp` 所花费的时间) |
| `times` | 显示 shell 的运行时间 | 例如 `times` (显示系统运行时间) |
| `tload` | 显示系统负载的图形报告 | 例如 `tload` (向指定进程显示当前系统平均负载) |
| `top` | 列出最活跃活跃或指定的进程 | 例如 `top -p pid` (-p: 通过 `pid` 显示特定进程) |
| `touch` | 更新现有文件的时间戳 | 例如 `touch myfile.txt` (将 `myfile.txt` 修改为当前时间) |
| `touch -t` | 更新现有文件的时间戳 | 例如 `touch -t myfile.txt` (-t: 指定时间) |
| `tr` | 翻译字符集 | 例如 `echo apple | tr “apple” “banana"` (输出: banana) |
| `traceroute` | 追踪到主机的路由 | 例如 `traceroute xvauhdhxv.com` (追踪数据包到另一个主机的路由) |
| `trap` | 接收信号时运行命令 | 例如 `trap` (显示当前的信号捕获) |
| `tree -p` | 以树形格式列出目录内容 | 例如 `tree –p` (-p: 也显示文件权限) |
| `tty` | 显示终端设备的名称 | 例如 `tty` (显示终端文件名) |
| `type` | 检测命令的类型 | 例如 `type wait` (输出: `wait` 是 shell 内置命令) |
| `ulimit -a` | 限制用户资源 | 例如 `ulimit -a` (-a: 显示系统所有的限制) |
| `umask` | 显示或设置文件权限值 | 例如 `umask 0022` (允许用户读写权限，其他用户读取) |
| `umask` | 显示或设置文件权限值 | 例如 `umask 0002` (允许用户组读写权限，其他用户读取) |
| `umask` | 显示或设置文件权限值 | 例如 `umask 0077` (允许用户读写权限，其他人无权限) |
| `umount` | 卸载设备或文件系统 | 例如 `umount /dev/dvd` (卸载 DVD 设备) |
| `unalias` | 别名 | 例如 `unalias aliasname` (删除指定的别名) |
| `uname -a` | 显示当前系统信息 | 例如 `uname -a` (-a: 显示所有信息) |
| `uname -n` | 显示当前系统信息 | 例如 `uname -n` (-n: 显示主机名) |
| `unexpand` | 将空格转换为制表符 | 例如 `unexpand myfile.txt` (将 `myfile.txt` 中的空格转换为制表符) |
| `uniq` | 过滤文件中重复的行 | 例如 `uniq myfile.txt` (显示 `myfile.txt` 中的唯一行) |
| `unset` |  shell 变量或函数 | 例如 `unset var` (删除变量) |
| `unzip` | 从 zip 格式解压缩文件 | 例如 `unzip archive.zip` (从 `archive.zip` 解压缩文件) |
| `uptime` | 显示系统运行时间 | 例如 `uptime` (显示系统运行时间) |
| `useradd` | 添加新用户账户 | 例如 `useradd username` (创建用户账户) |
| `useradd -d` | 显示新用户的默认值 | 例如 `useradd -d` (显示新用户的默认数据) |
| `userdel` | 删除现有用户账户 | 例如 `userdel username` (移除用户账户) |
| `usermod -d` | 修改主目录 | 例如 `usermod -d /home/mydir andy` (-d: 为 `andy` 指定主目录) |
| `usermod -l` | 修改现有用户账户 | 例如 `usermod -l oldname newname` (-l: 修改登录名) |
| `usermod -p` | 修改现有用户账户 | 例如 `usermod -p password` (-p: 修改密码) |
| `users` | 列出当前登录的用户 | 例如 `users` (显示当前登录的用户) |
| `vdir` | 详细显示目录内容 | 例如 `vdir` (像 `ls` 一样更详细) |
| `vi` | 文本编辑器 | 例如 `vi filename` (打开文件) |
| `vmstat` | 报告虚拟内存统计 | 例如 `vmstat` (报告交换、磁盘 i/o 等) |
| `w` | 列出当前登录的用户 | 例如 `w username` (显示用户的进程) |
| `w -s` | 只显示 shell 摘要 | 例如 `w -s` (-s: 显示 shell 摘要) |
| `wc` | 统计行数、单词数和字节数 | 例如 `wc filename` (统计文件计数) |
| `man` | 查看帮助手册 | 例如 `man command` (查看命令的手册) |





| 命令 |  |
| :--- | :--- |
| `yum` | 基于 rpm 的包管理器。例如 `yum install update`（安装一个名为 "update" 的包） |
| `zcat` | 输出压缩的文本。例如 `zcat myfiles.txt.gz \| less`（解压文件并显示内容） |
| `zless` | 显示未压缩/压缩文件的内容。例如 `zless myfile.txt.gz`（`zless`: 分页显示内容） |
| `zmore` | 显示未压缩/压缩文件的内容。例如 `zmore myfile.txt.gz`（`zmore`: 按屏显示内容） |
| `zip` | 将文件压缩为 zip 格式。例如 `zip documents *`（为所有文件创建 `documents.zip`） |
| `unzip` | 从 zip 格式解压文件。例如 `unzip myfile.zip`（解压 `myfile.zip`） |

## [Ray Yao 推荐书籍](https://geni.us/ray-yao)

![C+ eCover202102021806.jpg](https://author.to/C_Sharp_Cheat_Sheet) ![RA eCover-202011182256.jpg](https://mybook.to/C_Plus_cheat_sheet)

![JS eCover-202101301841.jpg](https://author.to/Java_Cheat_Sheet) ![HC eCover-202008071843.jpg](https://mybook.to/JavaScript_cheat_sheet)

![PY eCover-202102042255.jpg](https://author.to/Python_Cheat_Sheet) ![VB eCover202101292345.jpg](https://mybook.to/PHP_cheat_sheet)

![MS Cheat Sheet.jpg](https://geni.us/MySQL_chsh_paperback) ![SQ Cheat Sheet (300).jpg](https://geni.us/SQL_chsh_paperback)

![C# eCover-202102052256.jpg](https://mybook.to/Linux_Command_Line) ![F:\书山有路学海无边\A1 Computer Books\JAVA Books\JV eCover(7.44x9.68)\JV eCover-202102012325.jpg](https://mybook.to/Html_Css_cheat_sheet)

（注：每份速查表包含 300 多个示例、300 多个输出和 300 多个解释。）

## [Ray Yao 纸质书籍](https://geni.us/ray-yao)

- [C# 速查表](https://author.to/C_Sharp_Cheat_Sheet)
- [C++ 速查表](https://mybook.to/C_Plus_cheat_sheet)
- [Java 速查表](https://author.to/Java_Cheat_Sheet)
- [JavaScript 速查表](https://mybook.to/JavaScript_cheat_sheet)
- [Php MySql 速查表](https://mybook.to/PHP_cheat_sheet)
- [Python 速查表](https://author.to/Python_Cheat_Sheet)
- [Html Css 速查表](https://mybook.to/Html_Css_cheat_sheet)
- [MySQL 速查表](https://geni.us/MySQL_chsh_paperback)
- [SQL 速查表](https://geni.us/SQL_chsh_paperback)
- [Linux 命令行](http://mybook.to/Linux_Command_Line)

## [100  题问答系列]

- [C# 100 题问答](https://mybook.to/C_Sharp_Examination)
- [C++ 100 题问答](https://mybook.to/C_Plus_Examination)
- [Java 100 题问答](https://mybook.to/Java_Examination)
- [JavaScript 100 题问答](https://mybook.to/JavaScript_Examination)
- [Php MySql 100 题问答](https://mybook.to/PHP_MySQL_Examination)
- [Python 100 题问答](https://mybook.to/Python_Examination)
- [Html Css 100 题问答](https://mybook.to/Html_Css_Examination)
- [Linux 100 题问答](http://mybook.to/Linux_Examination)

## [示例与详解]

- [C# 示例与详解](https://mybook.to/C_Sharp_Examples)
- [C++ 示例与详解](https://mybook.to/C_Plus_Examples)
- [Java 示例与详解](https://mybook.to/Java_Examples)

