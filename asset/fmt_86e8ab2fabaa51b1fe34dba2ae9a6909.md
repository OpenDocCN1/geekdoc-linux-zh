
# CompTIA A+ 认证全合一考试指南

## 第 16 章：使用命令行界面

### `dir` 命令

Linux 默认提示符不显示完整路径，但在 Ubuntu 系统上，输入 `ls` 显示如下：

```
mike@server:~ ls
Desktop Downloads Videos
Documents photo.jpg
```

如果你在 PC 上操作，请记住不同的电脑包含不同的文件，你将看到与上一个示例不同的内容。如果 Windows 中大量文本快速滚动屏幕，尝试 `dir /p` 忘记按回车键。当在大目录中查找内容时，`dir /p` 是救命稻草。

在 OS X 和 Linux 中，你可以通过输入 `ls | more` 获取与 `dir /` 相同的结果。符号 `|` 是管道（pipe）。你正在告诉操作系统将 `ls` 的输出不是直接发送到屏幕，而是将其“管道”传输一个名为 `more` 的第二个命令。管道命令在所有操作系统中均有效且非常强大。在本章的稍后部分你将看到更多管道命令的内容。

某些命令无论是否包含空格都会产生相同的结果。例如，输入 `dir/p` 和 `dir /l` 提供相同的输出。然而，某些命令要求命令和开关之间有空格。通常，养成在命令和开关之间加上空格的习惯，就不会遇到问题。

> **注意** 在命令后面用于修改其操作的额外字符（如 `dir` 之后的 `/w` 或 `/p`）被称为开关。几乎所有开关都可以同时使用来修改命令。例如，在 Mac OS 或 Linux 中输入 `ls -a -l -h`

```
C:\Users\michaels>dir ?

显示目录中文件和子目录的列表。

DIR [drive:][path][filename] [/A][:attributes]] [/B] [/C] [/D] [/L] [/M]
[/I][:sortorder][field]] [/A] [/B] [/L] [/S] [/T][:timefield]] [/U] [/X] [/Z]

dir [drive:][path][filename]
指定要列出的文件、目录和或。

/A 属性 显示具有指定属性的文件。
/B 目录 归档只读文件
/H 隐藏文件 准备好进行索引的文件
/S 排序文件 前缀名称含义
/V 卷标 不是设备上的内容。
/L 重新解析点 显示注释
使用宽格式 不显示标题信息。这是默认设置。文件列之间使用双分隔符。
与宽格式相同，但按列排序。
/U 使用长列表格式 文件名位于最右侧。
/M 名称（按字母顺序）S 按大小排序（从小到大）
/E 按扩展名（按字母顺序）D 按日期排序（从旧到新）
/G 分组 反转顺序的前缀
/P 显示文件的所有者。
/Q 显示大小信息
/R 显示指定目录及所有子目录中的文件。
/T 控制显示或用于排序的时间字段
/W 访问 使用为非 8dot3 文件名生成的短名称宽格式。格式为 /N 并在其之前插入短名称；如果没有插入短名称，则用空格代替。
/Y 显示四位数的年份 环境变量中可能预设开关。通过在任何开关前加上 -（连字符）-来覆盖预设开关，例如，/W。

C:\Users\michaels>
```

**图 16-8** 在 Windows 中输入 `?` 会列出 `dir` 命令的所有可能的开关。

`ls` 命令像 UNIX 命令一样非常强大，并包含 50 个不同的开关。让我们只来看其中最重要的开关之一：`-l`。配合 `-l` 开关（代表长列表列出）使用，可以提供关于所有文件的详细信息：

```
$ ls -1
-rw-rw-rw-- 0 mike 2313443 Jun 13 15:22:50 .photo.jpg
```

我们将在本章节中详细讨论此输出。Windows 的帮助文档似乎有些晦涩，而 Mac OS X 和 Linux 的帮助屏幕通常难以阅读。尽管如此，当你不熟悉某个命令或不知道如何获取所需内容时，它们仍然很有用。尽管我记住了许多命令，但我仍然会参考这些帮助屏幕；你也应该使用它们。如果你真的迷路了，可以在命令提示符处输入 `help` 来查看你可能键入的命令列表。

### 更改目录焦点：`cd` 命令

`cd` 命令在每个操作系统中都可以工作，尽管 Windows、Mac OS X 和 Linux 之间存在差异。你可以使用 `cd` 命令将命令提示符的焦点更改到不同的目录。要使用 `cd` 命令，输入 `cd` 后跟你想要关注的目录名称。例如，在 Windows 中，要进入根目录下的 `Obiwan` 目录，输入 `cd obiwan` 然后按回车键。如果系统在该处有一个 `Obiwan` 目录，提示符将变为该目录并显示为 `C:\obiwan`。如果不存在此类目录，或者你不小心输入了 `obiwam` 之类的内容，你会收到错误“系统找不到指定的路径。”如果我每次看到这些错误都能得到一个美元就好了！我通常是因为我打字太快了。如果你遇到此错误，请检查你的输入并重试。

要返回根目录，输入 `cd\` 并按回车键。你可以使用 `cd` 命令将提示符指向任何目录。例如，你可以从 `C:\` 提示符处输入 `cd obiwan\hope`，提示符就会变为 `C:\obiwan\my\hope`——当然了。

一旦提示符发生变化，输入 `dir`。你应该看到一个不同的文件和目录列表，因此当你指向不同的目录时，`dir` 命令会向你显示不同的内容。

在 Mac OS X/Linux 中更改目录焦点与在 Windows 中操作类似，但你使用的是 `/` 而不是 `\`。使用刚才为 Windows 显示的相同示例，从根目录你使用 `cd /Obiwan`。要进入 `/obiwan/my/hope` 目录，你输入 `cd /obiwan/my/hope`。

> 在 Linux 系统上，在根 (`/`) 目录中创建文件和文件夹被认为是不礼貌的。事实上，你甚至需要“root”权限才能执行此类。这是因为 Linux 作为一个多用户系统的历史；包含限制是非常重要的，以确保用户不会破坏每个人都依赖的底层操作系统。

在之前的示例中，我们一直在使用所谓的绝对路径，这意味着我们正在输入要更改的目录的完整路径。这对于 80 年代的古老 DOS 系统来说可能还可以，但在当今深层嵌套的目录树中，这样来回移动仍然太麻烦了。

这时相对路径就派上用场了；它不是从目录名称开始。例如，你只需在 `C:\` 提示符处输入 `cd obiwan`，即可从根目录进入 `C:\Obiwan` 目录。你可以一次移动一级，如下：

```
C:\cd obiwan
C:\Obiwan>cd my
C:\Obiwan\my>cd hope
```

![](img/91631f1341ca27cd38d41339a50e983)

或者，你可以一次性跳转多个目录级，例如：

```
C:\> Obiwan\my\hope
C:\Obiwan\my\hope>
```

这些技巧也适用于 Mac OS X 和 Linux，但你当然总是使用正斜杠而不是反斜杠：

```
mike@server:-$ cd Obiwan
mike@server:~/Obiwan$
```

最后一个技巧：如果你想向上一个目录，可以输入 `cd` 后紧跟两个点。例如，如果你在 `C:\Obiwan` 目录并想回到 `C:\Obiwan` 目录，只需 `cd ..` 就会到达那里：

```
C:\Obiwan\my>cd ..
C:\Obiwan>
```

花时间使用 `cd` 和 `dir` 命令在 PC 上移动。

### 在 Mac OS X 和 Linux 之间移动驱动

由于 Mac OS X 和 Linux 不使用驱动器，如何访问移动介质？在 Windows 中，所有介质都挂载为文件夹。在 Ubuntu Linux 中，你需要查看 `/media` 文件夹。在 Mac OS X 中，你需要查看 `Volumes` 文件夹。在其他 Linux 发行版中，你必须自己探索——幸好以下命令显示了你的光驱：

```
mike@server:/media/mike ls -l
drwx----3 mike 4096 Dec 31 1969 THUMDRIVE
dr-xr-xr-x 6 mike 2048 May 13 2015 Age of Empires
```

### 创建目录：`md`/`mkdir` 命令

现在你已经学会了如何在命令行提示符世界导航，是时候开始制作东西了，从创建目录开始。

在 Windows 中使用 `md` 命令创建目录。或者，你可以使用 `mkdir` 命令，它在所有操作系统中均有效且与 `md` 相同。在 Windows 中，要在用户文件夹下创建一个 `practice` 的目录（例如），打开一个新的提示符窗口或 `cd` 到你的用户文件夹 `\Users\<username>`。你应该看到提示

```
C:\Users\mike>
```

现在提示符指向 `C:\Users\mike`，输入 `md practice` 创建目录：

```
C:\Users\mike>md practice
```

一旦你按下回车键，Windows 将执行该命令，但它不会提供关于它做了什么的任何信息。你必须使用 `dir` 命令查看你确实创建了一个新目录。

```
08/21/2016  03:58 PM  <DIR>             .
08/21/2016  03:58 PM  <DIR>             .
08/21/2016  09:55 AM  <DIR>             Desktop
07/15/2016  08:25 AM  <DIR>             Documents
08/20/2016  09:16 AM  <DIR>             Downloads
07/15/2016  08:25 AM  <DIR>             Favorites
07/15/2016  08:25 AM  <DIR>             Music
07/15/2016  08:25 AM  <DIR>             Pictures
08/21/2016  03:58 PM  <DIR>             practice
07/15/2016  08:25 AM  <DIR>             Videos
                        1 File(s)    216,876,089,344 bytes free
                        1 Dir(s)
```

区分大写和小写呢？Windows 在文件和文件夹名称中同时显示大小写，但在命令中很少进行区分——这委婉的说法是 Windows 不支持大小写敏感。为了清晰起见，请尝试使用 `md` 命令创建一个名为 `Practice` 的文件夹（注意大写字母），看看会发生什么。这在 Windows 图形界面中也是如此。回到桌面尝试创建两个文件夹，一个名为 `files`，另一个名为 `FILES`，看看 Windows 会告诉你什么。

要在 `practice` 目录中创建子目录，首先使用 `cd` 命令将提示符指向 `practice` 目录：

```
C:\Users\mike>cd practice
C:\Users\mike\practice>
```

然后运行 `md` 命令创建 `files` 目录：

```
md files
```

> **注意** 在执行 `md` 命令之前，请确保提示符指向你想要创建新子目录的目录。

![](img/91631f1341ca27cd38d41339a50e983e_698_0.png)

完成后，输入 `dir` 查看新的 `Files`。为了好玩，尝试再次执行该过程并在 `practice` 目录下添加一个 `games` 目录。输入 `dir` 验证是否成功。

在 Mac OS X 和 Linux 中创建文件夹的方法再次是完全相同的，但你必须使用 `mkdir` 命令。以下是在我的 Ubuntu 系统上完成的相同示例：

```
mike@server:-$ mkdir practice
```

你可以通过运行 `ls` 命令查看结果：

```
mike@server:-$ls
practice
```

### 删除目录：`rd` 命令

不要忘记 Linux 和 Mac OS 是区分大小写的。检查这些不同文件夹的结果，它们都是 "files" 的不同大小写拼写形式：

```
mike@server:-$practice ls
files Files
mike@server:-$practice$
```

删除子目录的操作与创建它们完全相同。首先，进入包含你想删除的子目录的目录，然后执行 `rmdir` 或 `rd` 命令。这两个命令在功能上是相同的，但它们运行的环境非常重要。`rmdir` 命令在 Windows、Mac OS X 和 Linux 中都能良好工作，但 `rd` 命令仅在 Windows 中有效。

所以，考虑到这一点，删除一些文件夹吧。这其实非常简单。在这个示例中，让我们以 Linux 为例，删除 `/practice` 目录下的 `Files` 子目录（记住 - - 表示你的主目录）。首先，通过输入 `cd practice` 进入 `files` 目录所在的位置——`/practice`（请确保你已经在主目录下）。然后输入 `rmdir files`。如果你没有收到响应，说明你做对了！输入 `ls` 检查 `Files` 子目录已消失。Windows 的操作完全一样，尽管我们倾向于更多地使用 `rd` 命令，仅仅是因为它更快。

让我们通过 `/s` 交换删除 `practice` 和 `games` 目录。因为 `practice` 目录在你的主目录下，使用 `cd \Users\你的用户名` 指向它。现在执行命令 `rd practice /s`。在一次罕见的仁慈显示中，Windows 回复道：

```
C:\Users\mike>rd practice /s
Are you sure (Y/N)?
```

按下 `y` 键，`C:\Users\mike\practice` 和 `C:\Users\mike\games` 都被消除了。

想在 Linux 中删除文件夹及其所有内容吗？没问题，但我们不用 `rmdir`。相反，我们使用非常实用的 `rm` 命令。在相同的场景下，使用带有 `-r` 参数的 `rm` 命令：

```
mike@server:-$ rm -r
```

### 操作目录

PC 技术人员应该熟练创建和删除目录。为了练习一下，尝试这样做！

1. 使用创建目录命令 (`md`) 在你的主目录中创建一个新目录。在主目录的提示符下，创建一个名为 `Jedi` 的目录：`C:\Users\padawan>md Jedi`
2. 像往常一样，提示符没有告诉你任何信息：它只是显示了一个新的提示符。执行 `dir`（即输入 `dir` 命令）查看你的新目录。当你发布命令时，Windows会在命令所在的地方创建新目录，无论你是否是想把它放在那里。为了演示，使用 `cd` 命令将提示符指向你的新目录：`C:\Users\padawan>cd jed`
3. 现在再次使用创建目录命令创建一个 `Yoda` 的目录：`C:\Users\padawan\Jedi>md Yoda`，你应该看到你的目录现在包含了一个目录。
4. 输入 `..` 回上一级并返回主目录，使用删除目录 (`rd`) 删除你的新目录：`C:\Users\padawan>rd /s jed`
5. 在另一个罕见的仁慈情况下，Windows 回复道：确定吗 (Y/N)？按下 `y` 删除 `Jedi` 和 `Yoda`。
6. 使用 Mac OS 或 Linux 系统，使用 `mkdir`、`cd` 和 `rm` 命令重复整个过程。考试提示：确保你知道如何使用 `md`、`mkdir`、`rd` 和 `cd` 以通过 CompTIA A+ 220-902 考试。

### 在 Windows 中运行程序

要在 Windows 命令行运行程序，只需更改程序所在的文件夹，输入名称并按回车。尝试这个示例。进入 `C:\Windows\System32` 文件夹——所有 Windows 系统上都是标准的，但你可以 `dir /p` 逐个查看文件。如果你看到了 `mmc.exe`（见图 16-9）。

![](img/91631f1341ca27cd38d41339a50e983e_701_0.png)

**16-9** 之前提到的 `System32` 文件夹列出的 `mmc.exe`，所有 `.exe` 和 `.com` 都是程序。运行 `mmc.exe` 程序只需在此情况下输入文件名并按回车（见图 16-10）。注意不需要输入 `.exe` 扩展名。恭喜！你从命令行运行了另一个应用程序。

![](img/91631f1341ca27cd38d41339a50e983e_701_1.png)

**16-10** 在 Windows 中运行 `mmc`，所有 `.exe`

### 在 Mac OS X 和 Linux 中运行程序

Windows 包含了许多用于特定任务的命令行工具。书中详细介绍了多功能且强大的 `net` 命令，例如。尽管我很喜欢告诉大家 Mac OS X、Linux 和 Windows 的命令行是相似的，它们在某些方面非常不同，其中之一就是如何从命令行运行执行文件。首先，Mac OS X 和几乎所有的 Linux 版本都带有颜色编码的命令行（尽管你可能看不出来，因为书是黑白的）。你看到的特定执行文件是绿色的。

```
vmuser@ubuntu1504-vm:~/usr/bin
vmuser@ubuntu1504-vm:~/usr/bin ls -lh
-rwxr-xr-x 1 root root 42 Apr 09 09:09 calculator
-rwxr-xr-x 1 root root 228 Apr 03 09:18 contacts
-rwxr-xr-x 1 root root 522 Sep 30 20:14 disks
-rwxr-xr-x 1 root root 365 Jan 25 20:15 disk-image
-rwxr-xr-x 1 root root 726 Jan 26 20:15 disks
-rwxr-xr-x 1 root root 912 Mar 20 09:13 file-share
-rwxr-xr-x 1 root root 1024 Apr 10 03:03 font-viewer
-rwxr-xr-x 1 root root 818 May 21 00:17 help
```
