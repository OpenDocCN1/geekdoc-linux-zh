
```
christine@server01:-$ cd ../etc
christine@server01:/etc$ pwd
/etc
```

当然，在这种情况下，你实际输入的内容其实比直接输入绝对目录引用 `/etc` 要多。因此，只有在这样做有合理性时才使用相对目录引用。

> 注意
> 拥有一个长且信息丰富的 CLI 提示符是有帮助的，正如本章本节所示。然而，为了清晰起见，书的其他部分使用了简单的提示符。

现在你已经知道如何遍历目录系统并确认你的当前工作目录，你就可以开始探索各个目录中包含的内容。下一节将带你了解查看目录结构文件的过程。

## 列出文件和目录

要查看系统上有哪些文件，请使用列表命令 `ls`。本节描述了 `ls` 命令以及用于格式化其显示信息的选项。

### 显示基本列表

`ls` 命令最基本的形式显示位于当前目录下的文件和目录：

```
$ ls

Desktop Downloads Music Pictures Templates Videos

Documents examples.desktop my_script Public test_file

$
```

注意 `ls` 命令产生按字母顺序排列的列表（列显示）。如果你正在使用支持颜色的终端模拟器，`ls` 命令可能还会用颜色显示不同类型的条目。`LS_COLORS` 环境变量控制此功能。（环境变量将在第 6 章中介绍）。不同的 Linux 发行版根据终端模拟器的能力设置此环境变量。

如果你没有彩色的终端模拟器，可以使用 `ls` 命令的 `-F` 参数来轻松区分文件和目录。使用 `-F` 参数会产生以下结果：

```
$ ls -F

Desktop/ Downloads/ Music/ Pictures/ Templates/ Videos/

Documents/ examples.desktop my_script* Public/ test_file

$
```

`-F` 参数用正斜杠 `/` 标记目录，以便在列表中识别它们。同样地，它用星号 `*` 标记可执行文件，帮助你更容易找到可以运行的文件。基础的 `ls` 命令有些误导性，它显示当前目录中的文件和目录，但并不是所有的。在 Linux 中，隐藏文件是以点 `.` 开头的。这些文件在默认的 `ls` 列表中出现。因此，它们被称为隐藏文件。

要显示隐藏文件和普通文件，使用 `-a` 参数。这里是使用 `-a` 命令的示例：

```
$ ls -a

.             examples.desktop Music      test_file

..           .config         my_script

.bash_history .dmrc         .profile

.bashrc      Documents       Public

.cache        Downloads    Templates

$
```

所有以点开头的文件现在都显示了。注意，以 `.bash` 开头的文件是给 bash 环境使用的。这些特性在第 6 章有详细介绍。

`-R` 参数是另一个 `ls` 命令选项。被称为递归选项，它会显示当前目录及其子目录中的文件。如果你有子目录，`-R` 参数将继续遍历这些目录。正如你看到的，对于大型目录结构，这会产生非常大的输出。`-F` 参数有助于你查看文件类型：

```
$ ls -F -R

Desktop/      Music/ Pictures/ Videos/

Documents/ examples.desktop my_script* Public/      test_file
```

```
/Desktop:

/Documents:

/Downloads:

/Music:

iLoveLinux.mp3*

/Pictures:

/Public:

/Templates:

/Videos:

$
```

注意 `-R` 参数显示了当前目录的内容，以及早期示例中来自用户家目录的每个子目录及其内容。唯一包含文件的子目录是 `Music`，它包含了可执行文件 `iLoveLinux.mp3`。

# 第 3 章：基础 bash 命令

## 显示列表

在基础列表中，`ls` 命令产生的每个文件信息不多。为了查看附加信息，另一个常用的参数是 `-l`。`-l` 参数产生列表格式，提供关于目录中每个文件的更多信息：

```
$ ls -l

total 48

drwxr-xr-x 2 christine christine 4096 Apr 22 37 Desktop

drwxr-xr-x 2 christine christine 4096 Apr 22 37 Documents

drwxr-xr-x 2 christine christine 4096 Apr 22 37 Downloads

-rw-r---- 1 christine christine 8980 Apr 22 36 example.desktop

-rw-r---- 1 christine christine 0 May 21 44

-rw-r---- 1 christine christine 0 May 21 44

-rw-r---- 1 christine christine 0 May 21 44

drwxr-xr-x 2 christine christine 4096 May 21 39 Music

-rw-r---- 1 christine christine 0 May 21 25 my_file

-rw-r---- 1 christine christine 0 May 21 25 my_script

-rw-r---- 1 christine christine 54 May 21 26 my_script

-rw-r---- 1 christine christine 0 May 21 42 new_file

drwxr-xr-x 2 christine christine 4096 Apr 22 37 Pictures

drwxr-xr-x 2 christine christine 4096 Apr 22 37 Templates

drwxr-xr-x 2 christine christine 4096 Apr 22 37 Videos

-rw-r---- 1 christine christine 0 May 21 28 test_file

drwxr-xr-x 2 christine christine 4096 Apr 22 37 $
```

长列表格式单行列出每个文件和目录。除了文件名外，列表还显示了有用信息。输出的第一行显示目录内的总块数。之后，每行都包含关于每个文件的以下信息：

- 文件类型 `d`、`文件` `l`、字符设备 `c` 或块设备 `b`
- 文件权限（参见第 6 章）
- 硬链接数（参见第 7 章的“链接文件”）
- 文件所有者用户名
- 文件组名
- 文件字节大小
- 文件最后修改时间
- 文件名或目录名

`-l` 参数是一个强大的工具。有了这个参数，你可以查看任何文件或目录所需的全部信息。`ls` 命令有很多在文件管理时非常有用的参数。如果你输入 `man ls`，你将看到几页用于修改 `ls` 命令输出的参数。不要忘记你还可以组合许多参数。你经常会发现不仅显示了所需的输出，而且容易记忆，例如 `ls -af`。

## 过滤列表输出

正如你在示例所示，默认情况下 `ls` 命令列出所有非隐藏文件。有时，这可能过头了，特别是当你只需要几个文件的信息时。幸运的是，`ls` 命令提供了一种让你在命令行上定义过滤器的方法。它使用过滤器来决定在输出中应该显示哪些文件或目录。过滤器作为简单的文本匹配字符串工作。在任何你想要的命令参数后包含过滤器：

```
$ ls -l my_script

-rwx-r-- 1 christine christine 54 May 21 26 my_script

$
```

当你指定特定文件的名称作为过滤器时，`ls` 命令只显示该文件。有时，你可能不知道要查找的确切文件名。命令还识别标准通配符：

- 问号 `?` 匹配一个字符
- 星号 `*` 匹配任意数量的字符

问号可以替换过滤器中任意位置的一个字符。例如：

```
$ ls -l my_scr?

-rw-r---- 1 christine christine 0 May 21 25 my_file

-rwx-r-- 1 christine christine 54 May 21 26 my_script

$
```

过滤器 `my_scr?` 匹配了目录中的两个文件。同样，星号用于匹配零或多个字符：

```
$ ls -l my*

drwxr-xr-x 2 christine christine 4096 May 21 37 Music

my_file

my_script

my_script$
```

使用星号找到了以该名称开头的三个不同的文件。像问号一样，你可以将星号放置在过滤器的任何位置：

```
$ ls -l my*s*t
```
