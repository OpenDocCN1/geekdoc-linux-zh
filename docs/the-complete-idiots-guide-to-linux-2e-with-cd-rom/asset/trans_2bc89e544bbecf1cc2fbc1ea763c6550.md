

这里是再次列出文件的语法。请注意 file3 现在指向一个不存在的文件！

```
[alberto@digital alberto]$ ls -l
total 2
drwxrwxr-x   3 alberto alberto      1024 Aug  1 20:41 adir/
-rw-rw-r--   1 alberto alberto         57 Aug  2 13:12 file2
lrwxrwxrwx   1 alberto alberto          4 Aug  2 13:15 file3 -> file
```

链接在 Linux 中经常被使用，以便文件可以同时放置在多个目录中。例如，目录 /usr/X11R6 包含 X Windows 使用的文件。一些较旧的 X Windows 程序安装到 /usr/X11R5 或 /usr/X11R4 中。通过一系列符号链接，Linux 可以使来自三个目录中的文件都出现在更通用的 X Windows 目录 /usr/X11 中，以便于访问。这种组织方式是符号链接的主要用途之一。

## 读取文件

能够移动和组织文件是一项重要的技能。最终，计算机主要用于存储和检索信息。以下是当你在终端上时可用于读取文件的几个命令：

- cat: 将文件内容复制到终端
- less: 一屏一屏地分页显示内容
- head: 查看文件中的前几行
- tail: 查看文件中的后几行

## 拼接：cat

cat 命令读取一个或多个文件并将结果打印到屏幕上。 （它将所有文件拼接至屏幕。）cat 是一个通用命令，在将多个命令链接在一起时使用频率非常高。当我们在第 14 章“让 Shell 发挥作用”中探讨重定向时，我会向你展示 cat 的真正用法。

cat 的基本语法是

```
cat [options] files
```

以下是使用 cat 查看 /etc/passwd 文件的示例（这是存储用户信息的文件）：

```
[alberto@digital alberto]$ cat /etc/passwd
root:UGQD...:0:0:root:/root:/bin/bash
bin:*:1:1:bin:/bin:
daemon:*:2:2:daemon:/sbin:
adm:*:3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/bin:/bin/sync
shutdown:*:6:0:shutdown:/sbin:/sbin/shutdown
halt:*:7:0:halt:/sbin:/sbin/halt
mail:*:8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
uucp:*:10:14:uucp:/var/spool/uucp:
operator:*:11:0:operator:/root:
games:*:12:100:games:/usr/games:
gopher:*:13:30:gopher:/usr/lib/gopher-data:
ftp:*:14:50:FTP User:/home/ftp:
nobody:*:99:99:Nobody:/:
postgres:!!:100:101:PostreSQL Server:/var/lib/pgsql:/bin/bash
alberto:YMMhuMSrulhME:501:501:AlbertoRicart:/home/alberto:/bin/bash
```

正如你所见，cat 打开了文件 /etc/passwd 并将每一行打印到控制台。

cat 命令提供了几个选项；最有用的列在表 12.1 中。

## 表 12.1 cat 命令选项

| Option | Description |
|--------|-------------|
| -n | Number all lines |
| -s | Squeeze multiple blank lines into one |
| -v | Display all characters (invisible characters, too, with the exception of tabs and newlines) |
| -A | Display all characters (invisible characters, too) |

要访问内容，请点击章节和节标题。

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## 一次查看一页：less

当你使用 cat 时，你可能已经发现如果文件大小超过屏幕所能容纳的范围，内容滚动得太快而无法阅读。处理这种情况的一种方法是使用分页命令。

分页器允许你一次查看一屏（或一页）信息。有两个命令可以使用：原始分页器 more 和更好的分页器 less。在这些程序的情况下，less 实际上是 more。例如，less 允许你“后退”并向上滚动，而 more 不允许。less 也不会在你告诉它之前退出。

当 less 打印一屏内容时，它会在屏幕底部放置一个冒号 (:)。这意味着当前页之后还有更多信息。在冒号显示时，你可以与 less 交互并向其发送命令。以下是一些更有用的命令：

- 要向前（或向下）滚动另一屏，请按空格键
- 要向后（或向上）滚动一屏，请按 B
- 要显示当前正在查看的文件名以及你在文件中的位置信息，请按 =
- 要停止阅读，请按 Q

当你到达文件末尾时，less 会恰当地在屏幕底部打印“END”；如果想退出程序，请按 Q。

## 查看前几行：head

有时你不想读取整个文件，只想看前几行。用于此的命令称为 head，它打印文件中的前十行：

```
[alberto@digital alberto]$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm:x:3:4:adm:/var/adm:
lp:x:4:7:lp:/var/spool/lpd:
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:11:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
news:x:9:13:news:/var/spool/news:
```

如果传递 -n 选项，你可以控制 head 打印的行数：

```
[alberto@digital alberto]$ head -n 1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

## 查看最后几行：tail

head 的对应物是 tail。默认情况下它打印最后十行。如果提供 -n 选项，head 将从文件末尾打印该数量的行：

```
[alberto@digital alberto]$ tail -n 1 /etc/passwd
alberto:x:100:100:Alberto Ricart:/home/alberto:/bin/bash
```

要访问内容，请点击章节和节标题。

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Chapter 13
在 Shell 下进行文本编辑

## 本章内容

- 使用 Vim 视觉编辑器
- 使用 XEmacs
- 运行 Ispell

在命令行下使用编辑器是必须的。这些编辑器的用户界面通常非常别扭，尤其是当你来自 Macintosh 或 Windows 等环境时。你可以在计算机上安装的字面上一百种不同的编辑器。它们各有优缺点。在我看来，你应该学习的两个命令行编辑器是。为什么两个？因为在某些系统下只有一个或另一个可用，你应该能够使用任一个进行工作。

最受欢迎的编辑器是

- 视觉编辑器 (vi)
- Emacs

vi 是任何类 UNIX 操作系统上最广泛可用的编辑器。仅凭这一点，它就应该是你需要学习的编辑器。知道 vi 可以在所有系统中找到是一个令人安心的想法；无论你明天使用什么版本的 UNIX，你都将能够编辑文件。

> Techno Talk:
> 通常，当你使用终端时，你应该能够按 Backspace 键并删除最后一个字符。如果你按 Backspace 却得到像 "^?" 这样的奇怪字符，你的终端没有正确设置。
> 
> 通常，这种配置问题会在你通过 telnet 远程工作时出现。修复问题实际上非常容易，有 stty 程序的帮助。 （stty 程序实际上非常复杂，但你不需要知道太多关于它如何工作的细节——只需要足够修复你的问题。）

stty 程序遵循此格式：stty command characters，其中 command 是选项的名称，characters 是你在 shell 或编辑器中使用它们时看到打印的字符。

经常使用的命令是

- erase （将退格键关联）
- kill （删除光标左侧的字符）
- `intr` （中断程序）
- `susp` （挂起程序）

对于我在 UNIX 下的日常工作，我使用 Emacs 或其表亲 XEmacs。两者编辑器之间的主要区别是 vi 比 Emacs 小约 20 倍。如果你曾经（希望你永远不会）需要进行灾难恢复，vi 可以放入软盘；Emacs 不能。就功能而言，Emacs 拥有全部，而且这不是夸张。

## 改进的视觉编辑器：Vim

Linux 发行版将 vi 作为 vim 的链接。Vim 是 vi 的改进版本（见下图）：最初名称为 Vi Imitation，但现在不再如此。Vim 提供了原始程序中缺少的一系列功能，但基本命令相同。因此，如果你学习更新的 vim 编辑器，你将不会有使用 vi 的问题，只是你会错过额外的功能。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_137_0.png)

你可以在这里看到一个运行在 KDE 内的 vim 的图形版本。

## 交互式 Vim 教程

学习 vim 的最简单方法是使用在线教程。就 vim 而言，此教程（系统中的一个文件）比阅读书籍更好也更有趣，因为它是一个交互式教程。以下是如何访问它。

要通过教程，你首先需要将一个文件复制到你的主目录。教程只是一个包含如何使用 vim 的说明的文本文件。

要安装教程，将 `/usr/doc/vim-4.5-2/tutor/tutor` 复制到你的主目录。你的安装中版本号可能已更新，因此这样复制：

```
cp /usr/doc/vim*/tutor/tutor ~/ 
```

此过程会将教程文件 tutor 放入你的主目录。

要开始教程，输入以下两个命令：

```
alberto@digital alberto]$ cd
[alberto@digital  alberto]$ vim tutor
*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*
* W e l c o m e   t o   V I   T u t o r   -   V e r s i o n   1 . 2 *
*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*

               ***************
                * Lesson 1.0 *
               ***************

Vim is a very powerful editor that has many commands, too many to
explain in a tutor such as this.  This tutor is designed to describe
enough of the commands that you will be able to easily use Vim as
an all-purpose editor.

The approximate time required to complete the tutor is 25-30
minutes, depending upon how much time is spent with experimentation.

It is important to remember that this tutor is set up to teach by
use.  That means that the student needs to execute the commands
to learn them properly.

Now, make sure that your Shift-Lock key is NOT depressed and
```

