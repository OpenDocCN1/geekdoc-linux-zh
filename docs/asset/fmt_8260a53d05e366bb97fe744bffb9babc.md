
| 按 `[Q]` | 退出 `info` 工具。 |

| 4 输入 `info date` | 为了查看关于 `date` 命令的语法信息。 |

| 按 `[PAGE DOWN]` | 查看页面的其余部分。 |

| 按 `[Q]` | 退出 `date` 命令的 `info` 页面。 |

| 5 输入 `help` + | 为了查看已文档的 `BASH` shell 函数列表。 |

| 按 `[SHIFT]` + `[PAGE UP]` | 向上翻页以查看列表顶部。 |

| 按 `[SHIFT]` + `[PAGE DOWN]` | 向下翻页以查看命令提示符。 |

| 6 输入 `help exit` | 为了查看 `exit` `BASH` shell 函数的信息。 |

## 系统关机

操作系统处理从内存到磁盘驱动器的数据写入。如果你在执行数据写入磁盘时关闭计算机，你的文件和系统文件可能会丢失或损坏。在关闭电源之前，通过关机来准备操作系统是非常重要的。

## 关系统

`shutdown` 命令用于停止或重启计算机。该命令将向其他命令终端发送消息，告知何时开始关机。它还会向各种用户和系统进程警告，以便它们保存数据、完成任务并准备好结束。

通过使用 `shutdown`，你可以指定命令执行之前的等待时间。例如，若要在 15 分钟后停止系统，你应该输入：

```bash
[root@localhost root] # shutdown -h +15
```

这将产生以下输出：

```
Broadcast message from root (tty2) at Tue 26 04:08:

The system is going DOWN in 15 minutes
```

要停止关机，按 `Ctrl+c` 取消命令。另一种方法是登录另一个终端并执行 `-c` 命令来取消关机。使用此选项，你还可以输入发送到所有终端的消息。

只有管理员账户（如 `root`）可以执行或取消关机命令。

要立即关机，你需要输入：

```bash
[root@localhost root]# shutdown -h now
```

这将产生输出：

```
Broadcast message from root (tty2) at Tue 26 04:08:

The system is going DOWN NOW
```

要重启计算机，使用 `-r` 选项：

```bash
[root@localhost root]# shutdown -r now
```

一个相当奇怪的选项 `-k` 向终端发送警告，但不会关闭系统。

## B-3：关系统系统

| 这样做 | 为什么这样做 |
| --- | --- |
| 1 以 `root` 身份登录 | |
| 2 输入以下命令：`shutdown -h +5` | 在 5 分钟后关机。 |
| 3. 等待一分钟 | 你将看到系统将在 4 分钟后停止。 |
| 4. 按 `CTRL` + `C` | 取消关机。 |
| 5. 切换到 `tty5` | |
| 6. 以 `user1` 身份登录 | |
| 7. 输出 | 因为系统计划停止，非管理员用户无法登录。 |
| 8. 切换到 `tty2` | |
| 9. 按 `CTRL` + `C` | 取消关机命令。 |
| 10. 输入以下命令：`shutdown -h +7` | 在 7 分钟后关机。 |
| 11. 切换到 `tty5` 终端 | |
| 12. 以 `user1` 身份登录 | 如果关机剩余时间大于五分钟，Linux 允许非管理员用户登录。 |
| 13. 输入 `exit` | 退出 shell。 |

## 3-16 CompTIA Linux+ 认证, 2004 目标

12 切换到 `tty5` 终端

13 以 `root` 身份登录

即使距离关机剩余时间不足五分钟，`root` 用户也可以登录。

观察输出

等待片刻直到系统发出警告并关机。

14 等待关机完成

![](img/90ff486f13f13845c7a30a29d84ce954_123_0.png)

## 主题 C：文件和目录

本主题涵盖了以下 CompTIA Linux+ 考试目标。

| 目标 |
|---|---|
| 2.2 | 使用 CLI 命令挂载和卸载各种文件系统 |

解释说明

### Linux 目录结构

与任何文件系统一样，Linux 将相关类型或用途的数据文件组织在不同的文件夹中，这些文件夹也被称为目录。目录的组织类似于一个倒置的树。它从根目录开始，根目录由 `/` 字符表示。

根目录下有几个子目录。每个子目录下还可以有更多的子目录。图 3-5 显示了目录树示例。

![](img/90ff486f13f13845c7a30a29d84ce954_124_0.png)

图 3-5：Linux 文件系统结构

当你将文件存储在某个目录时，该文件物理上存储在计算机内部的硬盘上。目录以相同的方式存储。事实上，目录实际上是一种特殊类型的文件，用于组织并为目录和文件提供指针。文件在目录中的放置并不是物理结构，而是操作系统识别并处理的逻辑结构。

### 路径

你通过目录结构查找特定文件或目录时所经过的路线被称为路径。指明目录的路径被称为该目录的绝对路径名。在图 3-5 中，`share` 目录的绝对路径是 `/usr/share`，`sue` 目录的绝对路径是 `/home/sue`。

在 `/sue` 目录下有一个名为 `dates` 的文件。当列出 `dates` 的完整路径时，我们称 `/home/sue/dates` 为绝对文件名。当我们开始使用命令时，这一概念的重要性将变得更加清晰。

![](img/90ff486f13f13845c7a30a29d84ce954_124_1.png)

## 3-18 CompTIA Linux+ 认证, 2004 目标

## 监控文件系统

上述所有目录都可以存在硬盘的同一个物理分区上，或者某些位于不同的分区，甚至在不同的驱动器上。它们的存储方式对系统用户并不重要，因为所有文件都出现在目录树的某处。

你可以使用 `mount` 命令将磁盘成为目录的一部分。例如，如果 `h2`（硬盘上的第二个分区）存储了 `/home` 的文件，则该分区被认为挂载到了 `/home`。使用软磁盘（`/dev/td0`）时，它通常被挂载到 `/mnt`，因此该目录代表软磁盘。

可移动设备（如软磁盘和 CD-ROM）或其他计算机上的文件系统通常经常使用 `mount` 命令手动挂载。硬盘分区通常固定不变，并在系统启动时自动挂载。

### 主目录

当你使用命令行终端登录 Linux 时，系统会自动将你置于你的主目录中。主目录是每个用户存储个人文件的地方。它在用户账户创建时创建，且除非权限允许，否则只有该用户和 `root` 可以访问。

普通用户通常在 `/home` 目录下有一个与其用户账户同名的主目录，例如 `/home/sue`。你可以通过观察 shell 提示符末尾的提示符或使用 `pwd` 命令（打印工作目录）来确认你当前所在的系统中。

如果 `sue` 已经登录，她将看到以下输出：

```
[sue@localhost]# pwd - absolute path name
/home/sue
```

`root` 的主目录是所不同的。它位于系统的根目录（`/root`）下，如图 3-5 所示。如果你以 `root` 用户身份登录，终端屏幕上将显示以下输出：

```
[root@localhost]# pwd
/root
```

命令行显示了用户名和计算机的主机名（`sue@localhost` 或 `root@localhost`），还显示了当前目录的名称（`sue` 或 `root`）。

### 导航文件系统

登录后，你使用命令查看其他目录或将自己移动到文件系统的其他部分。

要更改目录，使用 `cd`（切换目录）命令并带上指定目标目录的参数。如果不指定目标目录，`cd` 将直接返回你的主目录：

Root 切换到 Mary 的主目录：

```
[root@localhost]# cd /home/mary
```

打印工作目录：

```
[root@localhost mary]## pwd
/home/mary
```

切换目录到 `/etc`：

```
[root@localhost mary]## cd /etc
[root@localhost etc]## pwd
/etc
```

返回主目录：

```
[root@localhost etc]## cd
[root@localhost root]## pwd
/root
```

命令行显示了用户名和计算机的主机名（`sue@localhost` 或 `root@localhost`），还显示了当前目录的名称（`sue` 或 `root`）。

如果 `sue` 已经登录，她将看到以下输出：

```
[sue@localhost]# pwd - absolute path name
/home/sue
```

`root` 的主目录是不同的。它位于系统的根目录（`/root`），如图 3-5 所示。如果你以 `root` 用户身份登录，终端屏幕上将显示以下输出：

```
[root@localhost]# pwd
/root
```

命令行显示了用户名和计算机的主机名（`sue@localhost` 或 `root@localhost`），还显示了当前目录的名称（`sue` 或 `root`）。

登录后，你使用命令查看其他目录或将自己移动到文件系统的其他部分。

要更改目录，使用 `cd`（切换目录）命令并带上指定目标目录的参数。如果不指定目标目录，`cd` 将直接返回你的主目录：

Root 切换到 Mary 的主目录：

```
[root@localhost]# cd /home/mary
```

打印工作目录：

```
[root@localhost mary]## pwd
/home/mary
```

切换目录到 `/etc`：

```
[root@localhost mary]## cd /etc
[root@localhost etc]## pwd
/etc
```

返回主目录：

```
[root@localhost etc]## cd
[root@localhost root]## pwd
/root
```

命令行显示了用户名和计算机的主机名（`sue@localhost` 或 `root@localhost`），还显示了当前目录的名称（`sue` 或 `root`）。

## 3-20 CompTIA Linux+ 认证, 2004 目标

你也可以在树上向上移动多个层：

```
[root@localhost]# cd /home/mary
[root@localhost mary]# pwd
/home/mary
[root@localhost mary]# cd ../
[root@localhost]# pwd
/
[root@localhost]# cd /home
mary
[root@localhost home]# pwd
/home
[root@localhost home]# cd mary
[root@localhost mary]# pwd
/home/mary
```

绝对路径因为其清晰性而简单，但当你位于根目录时，相对路径可以为你大量的大量的打字时间。

| # | 命令 | 说明 |
|---|---|---|
| 4 输入 `cd root` | 将当前文件夹更改到根目录。 |
| 输入 `pwd` | 查看当前工作目录。 |
| 5 输入 `cd etc` | 查看当目录名称不正确时显示的错误。 |
| 6 输入 `cd /etc` | 切换到 `/etc` 目录。 |
| 输入 `pwd` | 验证目录已成功切换。 |
| 7 输入 `cd /` | 切换到根目录。 |
| 输入 `pwd` | 验证目录已成功切换。 |
| 8 输入 `cd ~` | 切换到当前用户的家目录。 |
| 输入 `pwd` | 验证目录已成功切换。 |
| 9 输入 `cd ../` | 切换到 `/` 目录。 |
| 输入 `pwd` | 验证目录已成功切换。 |
| 10 输入 `cd /etc/samba` | 切换到 `/etc/samba` 目录。 |
| 输入 `pwd` | 验证目录已成功切换。 |
| 11 输入 `cd ../sysconfig` | 切换到 `/etc/sysconfig` 目录。 |
| 输入 `pwd` | 验证目录已成功切换。 |
| 12 输入 `cd /r` | 完成路径。 |
| 按 `TAB` | |
| 按 `ENTER` | 切换到 `/root` 目录。 |

## 查看文件和目录

一旦建立了目录结构来组织文件，你就需要一种方法来查看目录包含哪些文件。为此，你使用列出目录内容的命令之一。有各种类型的文件和文件名，你应该理解它们，以便尽可能地利用不同的命令。

### 文件类型

所有数据都以文件的形式存在。无论大小，文件都是将位信息或指令组织成有意义形式的基本形式。

有许多不同类型的文件，包括这些常见类型：

- 文本文件：大多数包含信息的文件都是文本文件。
- 二进制数据文件存储常用函数和图形等信息。
- 可执行文件在内存中执行并变为进程。它们通常与几个辅助二进制文件相关联。
- 目录文件作为占位符来组织其他文件。
- 链接文件是彼此相互关联的文件。它们可能代表相同的数据，也指向另一个文件。
- 特殊设备文件代表不同的设备，如硬盘和串串口。它们配合命令使用来操作设备。
- 命名管道文件标识从一个进程传递信息到另一个进程的通道。在写入文件的同时，另一个进程从同一个文件中读取，从而实现这种信息的传递。
- 套接字文件是命名管道文件的变体，允许另一台计算机上的进程向本地计算机上的文件写入，同时另一个进程从该文件中读取。

### 文件名

文件通过名称识别。文件名通常由字母和数字组成，但也可以包含下划线 (`_`)、连字符 (`-`) 和点 (`.`)。文件名的长度最多可达 255 个字符，但很少有超过 20 个字符的名字。

> 注意：以点 (`.`) 开头的文件称为隐藏文件，需要特殊的命令才能看到它们。

你可能熟悉 Windows 系统上使用的文件名。它们通常以点和三个描述文件类型的字符结束，例如文档 `txt (.txt)` 和 `server.exe`（可执行程序）。这些被称为文件扩展名。

Linux 上的大多数文件并不遵循这种模式，而且完全没有扩展名。许多带有扩展名的文件功能与你在 Windows 中看到的不同。这些扩展被称为文件名后缀。下表显示了常见示例。

| 后缀 | 说明 |
|---|---|
| .c | C 编程语言源文件 |
| .cc | C++ 编程语言源文件 |
| .cpp | |
| .html<br>.htm | HTML（超文本标记语言）文件 |
| .ps | 使用 PostScript 格式化的打印文件 |
| .txt | 文本文件 |
| .tar | 归档文件（内部包含其他文件） |
| .gz<br>.bz2<br>.Z | 压缩文件 |
| .tar.gz<br>.tgz<br>.tar.bz2<br>.tar.Z | 压缩归档文件 |
| .conf<br>.cfg | 配置文件（包含文本） |
| .so | 共享对象（编程库）文件 |
| .o | 编译的对象文件 |
| .pl | PERL（实用提取报告语言）程序 |
| .tel | TCL（工具命令语言）程序 |
| .jpg<br>.jpeg<br>.png<br>.tiff<br>.xpm<br>.gif | 包含图形文件的二进制文件 |
| .sh | Shell 脚本（包含由 shell 执行的文本） |

在命名文件时，避免使用 shell 元字符是非常重要的。将包含 shell 元字符的文件名作为命令的参数可能会产生意料之外的结果。

### 使用 ls 列出文件

可以使用多种命令来显示文件及其类型。最常用的是 `ls` 命令。以下是 `root` 用户家目录下文件列表的示例：

```
[root@localhost]# pwd
/root
[root@localhost]# ls
current myprogram project project12 project2 project4
Desktop myscript project1 project13 project3 project5
[root@localhost]# _
```

`ls` 命令显示当前目录下的所有文件。`ls` 命令显示所有文件在当前目录下的所有文件。你可以通过 `pwd` 命令来验证目录已成功切换。例如，以 `root` 登录时，可以使用 `pwd` 命令查看当前目录：

```
[root@localhost]# pwd
/root
[root@localhost]# ls
```

> 注意：Windows 用户熟悉 `dir` 命令。可以使用 `cd` 命令切换到目录。`pwd` 查看目录。当你以 `root` 登录时，你可以使用 `cd` 切换到 `/` 目录。`pwd` 验证目录已成功切换。

### 使用 ls 列出文件

可以使用多种命令来显示文件及其类型。最常用的是 `ls` 命令。以下是 `root` 用户家目录下文件列表的示例：

```
[root@localhost]# pwd
/root
[root@localhost]# ls
current myprogram project project12 project2 project4
Desktop myscript project1 project13 project3 project5
[root@localhost]# _
```

`ls` 命令显示当前目录下的所有文件。你可以通过 `pwd` 命令来验证目录已成功切换。例如，以 `root` 登录时，你可以使用 `pwd` 命令查看当前目录：

```
[root@localhost]# pwd
/root
[root@localhost]# ls
```

`ls` 命令显示当前目录下的所有文件。你可以通过 `pwd` 命令来验证目录已成功切换。例如，以 `root` 登录时，你可以使用 `pwd` 命令查看当前目录：

```
[root@localhost]# pwd
/root
[root@localhost]# ls
```

查看更详细信息：
