
# 使用终端创建文件

**步骤 5** 假设你现在想创建一个文本文件，我们称其为`Test2.txt`。输入一些内容来完成。所以，输入：`touch Test2.txt`。这将创建文件`Test2.txt`并将其推入终端编辑器。

**步骤 8** `Xed`是一个 GUI 应用，你可以通过菜单栏输入文本并保存文件（或任何文件），并使用其顶部菜单栏选项中的**文件（File）** > **保存（Save）** 或**文件（File）** > **另存为（Save As）** 功能。

```
File Edit View Search Terminal Help

david@david-min ~$ touch Test2.txt

david@david-min ~$ ls

david@david-min ~$ touch touch_test.txt

david@david-min ~$ ls

Test2.txt

david@david-min ~$ cat Test2.txt
```

**步骤 6** 你会注意到光标在`cat` > `Test2.txt`命令下方闪烁，没有任何参数。这个提示允许你输入文件将包含的文本。输入一些文本，然后按**Ctrl+D**退出并将内容保存到文件中。

但是，如果你更喜欢留在终端中编辑/保存/创建文件，可以使用`Nano`。`Nano`是一个简单的基于终端的编辑器。要尝试它可以使用`nano Test2.txt`。它屏幕底部有一个菜单。你可以在`Nano`中保存任何内容，然后按**Ctrl+X**并遵循屏幕上的操作说明。

```
File Edit View Search Terminal Help

david@david-root ~

david@david-root ~$ touch Test2.txt

david@david-root ~$ ls

david@david-root ~$ touch touch_test.txt

david@david-root ~$ ls

Test2.txt

david@david-root ~$ cat Test2.txt

这是使用终端的 cat 命令输入的。很酷，不是吗？按下 Ctrl+D...
```

**步骤 7** 固然你不一定得要使用终端向文件中输入文本。`Mint`附带了一个名为`Xed`的编辑器，它类似于 Windows 记事本。要在`Xed`中查看之前创建的文件，在终端中输入`xed Test2.txt`并按**回车**。

**步骤 10** 我们已经使用终端启动了`Mint`应用`Xed`，但任何应用其实都可以在终端内启动。例如，尝试：`firefox`，然后按**回车**。关闭`Firefox`返回终端。

# 创建和删除目录

与在终端中创建文件一样，你也可以创建和删除目录，或者如果你愿意，称为文件夹。目录构成了文件系统的结构，如果没有目录，文件系统将一片混乱。

## 管理文件夹

学习在终端中创建和删除文件夹是`Mint`（实际上是整个 Linux）的一项需要掌握的重要技能。以下是基础操作供你尝试。

- 步骤 1
主目录。如果需要，使用`cd -`命令无论你当前位于何处都能返回到主目录。现在输入`ls`查看你拥有的文件夹。你会发现文件夹被标记为青色（浅蓝色）。让我们先创建一个目录：`mkdir testdir`。

- 步骤 2
如果你现在输入`ls`，你会看到新目录`testdir`与 Home 区域的其他目录一起被创建了。显然`mkdir`命令创建了目录。

- 步骤 3
如果你再次输入命令`mkdir testdir`，你会收到一条消息显示：`mkdir:无法创建目录 'testdir': 文件存在`。在当前目录下只能有一个同名的目录。然而，Linux 允许`ls testdir`。

- 步骤 4
你可以在已经创建的目录中创建目录。例如，进入目录`cd testdir/`并按照操作列出该目录。那里什么都没有，因为你刚刚创建了它。现在通过`cd ..`返回主目录，并输入`mkdir testdir/reports`。回到测试目录，`cd testdir/`并执行`ls`。

## 创建和删除目录

**第 5步** 创建目录的命令逻辑很清晰，你是的。然而，如果你想创建一个目录并在其中创建子目录，请确保你处于家目录，并使用单个命令创建子目录（`cd ~`）或使用`mkdir -p Temp/Finances`。现在，`cd Temp/`并列出新目录。

**第 8步** 现在既然我们已经创建了一些目录，让我们来看看如何删除它们。通过进入目录并列出内容：`cd testdir`，然后输入`ls`。创建的`reports`子目录存在。现在删除它的方法之一是进入`rmdir reports`，然后输入`ls`确认它不存在。

```
david@david-mint: ~Temp

File Edit View Search Terminal Help

david@david-mint: # mkdir -p Temp/finances

david@david-mint: # mkdir -p Temp/ls

Finances

david@david-mint: # ls
```

```
david@david-mint: ~testdir

File Edit View Search Terminal Help

david@david-mint: # cd testdir

david@david-mint: # ls

Reports

david@david-mint: # rmdir reports

ls

david@david-mint: # rmdir testdir
```

**第 6步** `-p`选项让`mkdir`命令能够创建子目录以及父目录。在 Linux 中，命令遵循相同的结构：命令、选项和参数。在在上一步的示例中，命令是（`mkdir`），选项是（`-p`），参数是（`Temp/finances`）。

**第 9步** 一个快速的警告：在终端中删除目录不会将其放入通过`Nemo`文件管理器的`Mint`垃圾桶中。对于任何文件也是如此，如果你在终端中删除一个目录，它就会彻底消失。

![](img/f8aca09bc266ba3d122c77a820ff023b_58_0.png)

```
david@david-mint: ~testdir

david@david-mint: # rmdir reports

david@david-mint: # rmdir testdir
```

```
File Edit View Search Terminal Help

david@david-mint $ mkdir -p Temp/finances
```

**第 7步** 如果你想深入研究`mkdir`命令的各种选项，可以在终端中输入`mkdir --help`。这将提供快速帮助，详细说明这些选项以及命令的工作原理。

`Rmdir`只删除空目录，要删除目录及其子目录，甚至文件，除非你使用带有`-R`选项的`rm`命令。例如，使用`rm -R Temp`。一个小技巧是删除父文件夹，其所有内容都会被删除。使用时请务必小心。

```
david@david-mint: ~Temp

File Edit View Search Terminal Help

david@david-mint: # mkdir --help

usage: mkdir [OPTIONS] DIRECTORY...

create the DIRECTORYs, if they do not already exist.

  --parents      create parent directories as needed

  --verbose      output a message for each created directory

  --version      output version information

  --context=CTX  use -z or CTX if specified by the SELinux

  --help           display help information and exit

GNU coreutils copy copy: https://www.gnu.org/manual/coreutils/

Full list of copy options: see 'mkdir --help'

other available via: 'info (coreutils) invocation'
```

```
david@david-mint: ~testdir

File Edit View Search Terminal Help

david@david-mint: # rm -R Temp

david@david-mint: # ls
```
