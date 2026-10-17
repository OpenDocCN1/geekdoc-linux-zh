
| drwxr-xr-x | 22 user 748 Nov 13 03:48 Library | | | | |

| drwxr-xr-x | 3 user 408 Oct 12 14:55 Local Documents | | | | |

| drwxr-xr-x | 3 user 102 Oct 12 13:49 Music | | | | |

| drwxr-xr-x | 3 user 102 Oct 12 11:49 Pictures | To Mon. doc. | | | | |

| drwxr-xr-x | 3 user 136 Oct 12 14:49 Public | | | | |

| -rw-r--r-- | 5 user 25762 May 18 15:13-my.jpg | | | | | |

| -rw-r--r-- | 1 user 25762 May 18 15:07-to.txt | | | | | |

| [ferro]-user chmod +w-my.jpg | | | | | |

| -rw-r--r-- | 1 user chmod +w-to.txt | | |

| 终端 | 文件 | 编辑 | 滚动历史 | 字体 | 帮助 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| [ferro]-user ls -l | | | | | (sh) |

| total 64 | 22 user 680 Jan 18 15:42 Desktop | | | | |

| drwxr-xr-x | 408 Nov 13 02:00 Documents | | | | |

| drwxr-xr-x | 22 user 748 Nov 13 03:48 Library | | | | |

| drwxr-xr-x | 3 user 408 Oct 12 14:55 Local Documents | | | | |

| drwxr-xr-x | 3 user 102 Oct 12 13:49 Music | | | | |

| drwxr-xr-x | 3 user 102 Oct 12 11:49 Pictures | To Mon. doc. | | | |

| drwxr-xr-x | 3 user 136 Oct 12 14:49 Public | | | | |

| -rw-r--r-- | 5 user 25762 May 18 15:13-my.jpg | | | | |

| -rw-r--r-- | 1 user 25762 May 18 15:07-to.txt | | | | |

| [ferro]-user chmod +w-my.jpg | | | | | |

| -rw-r--r-- | 1 user chmod +w-to.txt | | | |

## 移除读取权限

## 添加写入权限

- 1 输入 `chmod` 并加一个空格。

- 2 输入 `go-r` 并加空格。

- 3 输入文件名并按回车。

- 1 输入 `chmod g+w` 并加空格。

- shell 指明文件组中的用户可以更改此项。

- shell 指明你可以读取该文件。

- 输入文件名并按回车。

## 应用它

你可以通过使用 `chmod` 命令的 `-R` 选项更改整个目录及其内容，包括你的主目录。`-R` 选项规定递归更改，这意味着更改适用于该目录或子目录中的所有文件。

例如，如果你想让你的主目录对你自己可见而对计算机的其他用户可见，请使用 `chmod` 命令。

## 输入此：

```
[ferro]-user chmod -R go rx
[ferro]-user ls -l
```

## 结果：

| | | | | | |

| :--- | :--- | :--- | :--- | :--- | :--- |

| drwxr-xr-x | 8 | user | staff | 272 Nov 13 13:59 | Desktop |

| drwxr-xr-x | 12 | user | staff | 408 Nov 13 02:00 | Documents |

| drwxr-xr-x | 22 | user | staff | 748 Nov 13 03:48 | Library |

| drwxr-xr-x | 3 | user | staff | 408 Oct 12 14:55 | Local Documents |

| drwxr-xr-x | 3 | user | staff | 102 Oct 12 13:49 | Music |

| drwxr-xr-x | 3 | user | staff | 102 Oct 12 11:49 | Pictures |

| drwxr-xr-x | 3 | user | staff | 136 Oct 12 14:49 | Public |

# 使用通配符选择文件

你可以使用通配符字符来避免在 Unix 中输入每个想要处理的文件的完整名称。这不仅节省了时间，还让你能够在单条命令中引用多个具有相似名称的文件。

Unix 通配符也称为 glob 模式（glob-patterns），使用这些通配符在 Unix 中被称为通配匹配（globbing）。每当你向 shell 提供文件名参数时，都可以使用这些通配符。

星号 (`*`) 匹配文件名中的任意零个或多个字符序列。问号 (`?`) 匹配任意单个字符。括号 (`[]`) 中的字符匹配该范围内的任意单个字符。请记住，字母是区分大小写的，例如在 `[a-m]` 中，字母 D 不在其中，因为它不是 a 和 m 之间的小写字母。

模式或字符范围开头的脱字符 (`^`) 表示该模式应选择不匹配给定模式的字符。例如，如果你想对所有目录和文件使用 `*` 命令，使用 `-r` 选项删除所有以 doc 开头、后面接三个字符并以 .doc 结尾的文件，你可以输入 `rm -Documents???.doc`。如果你想避免删除错误的文件，在使用 `rm` 时应始终使用 `-i` 选项。一个粗率的 `rm *` 命令可能会删除该目录的内容。

隐藏文件很难通过通配符识别。例如，命令 `ls *` 不会列出隐藏文件，而 `ls .*` 会列出隐藏文件。

# 使用通配符选择文件

| 终端 文件 编辑 滚动回 字体 窗口 帮助 | 终端 文件 编辑 滚动回 字体 窗口 帮助 |

| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

| | | | | | (tcsh) | | | | | (tcsh) | | | |

| ([ -])ls -ld* | | | | | | | | | | | | | | |

| drwx------ | 3 staff 102 Nov 4 13:49 Pictures | drwx------ | 3 staff 102 Nov 4 13:49 Pictures |

| drxr-xr-s | 4 staff 136 Nov 4 13:49 Documents | drxr-xr-s | 4 staff 136 Nov 4 13:49 Documents |

| ([ -])user | | | | | | | | | | | | | | |

| | | | | | | | | | | | | | | |

| | 24 staff 816 Nov 15 22:50 desktop | | 24 staff 816 Nov 15 22:50 desktop |

| | 12 staff 400 Nov 16 00:38 Documents | | 12 staff 400 Nov 16 00:38 Documents |

| | 22 staff 748 Nov 13 03:48 Library | | 22 staff 748 Nov 13 03:48 Library |

| | 4 staff 413 Nov 14 13:49 Music | | 4 staff 413 Nov 14 13:49 Music |

| | 3 staff 102 Nov 18 15:22 Note To Mon.doc |  3 staff 102 Nov 18 15:22 Note To Mon.doc |

| | 1 staff 370 Nov 17 17:04 | | 1 staff 370 Nov 17 17:04 |

| -rw------- | 1 staff 25762 Nov 18 15:13 dog.jpg | -rw------- | 1 staff 25762 Nov 18 15:13 dog.jpg |

| | 1 staff 0 Nov 15 18:07 to.txt | | 1 staff 0 Nov 15 18:07 to.txt |

| ([ -])user | | | | | | | | | | 匹配 glob 模式

- 1 输入一个接受文件名参数的命令。

- 2 输入匹配你想要选择的文件的通配符模式。

- shell 对通配符模式指定的文件执行命令。

# 使用脱字符选择不匹配的文件

- 1 输入一个接受文件名参数的命令。

- 2 输入 `^` 后跟匹配你不想选择的文件的通配符模式。

- shell 对当前目录中除通配符模式指定以外的文件执行命令。![](img/8d9b2c31cb5eb6571f0b2dfd7c634cf_0.png)

# 使用补全选择文件

你可以通过文件名补全轻松指定文件名，这是 shell 内置的一个特殊功能。要使用文件名补全，你必须输入文件名的部分并按 Tab 键。如果有匹配的文件并按回车，shell 将为你填充完整文件名。

要查看模糊匹配的结果，你可以在提示声后按 Control + D。或者，你可以输入 `set autolist`，这指示 shell 在文件名补全失败时列出剩余选项。这是一个保存在 `.bashrc` 中的良好命令。同样，你可以通过 `unset autolist` 关闭此功能。

如果没有文件匹配文件名，shell 程序会发出提示声表示没有匹配。如果有多个文件匹配，shell 程序会尽可能地填充并发出提示声，等待你输入更多文本以区分匹配模式的不同文件。此时，你可以输入更多的命令行并按回车，或者输入足够唯一标识你想要访问的文件，然后再次按 Tab。

你可以将文件名补全与完整或相对路径结合；如果你输入部分路径并按 Tab，shell 会列出路径内的选项。文件名补全可以节省大量的打字时间，并减少输错字符的概率。

# 使用补全选择文件

| 终端 文件 编辑 滚动回 字体 窗口 帮助 |

|---|---|---|---|

| | Terminal -- tty1 |

| [[ -:-]: user set autolist |

| [[ -:-]: user is -ld G |

| Desktop/ Documents/ |

| [[ -:-]: user is -ld Desktop/ |

| drwx------ 6 user set 204 Nov 18 16:34 Desktop/ |

| [[ -:-]: user

 输入 `set autolist`。

- 输入一个接受文件名参数的 shell 命令。

- 输入文件名的前几个字母并按 Tab 键。

- 出现可能的匹配列表。

- 输入足够的字母以形成唯一匹配。

- 再次按 Tab 键。

- shell 完成文件名。

- shell 执行该命令。

# 按名称查找文件

你可以通过 `find` 命令根据名称或其他标准查找文件。该命令通常比 Mac OS 的 Sherlock 应用更快，特别是对于那些系统使用或在 Finder 中隐藏的文件。

你正在查找的。参数 `-print` 指示 `find` 命令显示文件的位置

`find` 命令是一个复杂且强大的工具，允许你运行许多不同搜索，并对找到的文件执行各种操作。然而，`find` 命令最常用的用法只是查找特定名称的文件并打印它们的位置。

你也可以提供通配符模式而不是文件名，`find` 命令会列出所有匹配模式的文件。当你这样使用通配符模式时，需要将其包含在引号中。例如，如果你保存了一个文档但没有记录存在哪个文件夹里，可以使用 `find` 命令找到你目录中所有的 doc 文件：

```
find ~/Documents -name "*.doc" -print
```

这显示了匹配模式的文件列表。当你想要查看路径的文件列表时，可以将 `print` 替换为命令：

`find -name filename -print`

第一个参数 `pathname` 是你想要搜索的目录。`pathname` 是![](img/8d9b2c31cb5eb6571f0b2dfd7c634cf_39_0.png) 的名称。

 按名称定位文件

- 1 输入 `find` 和一个空格。

- 2 输入目录的 `pathname` 和一个空格。

- 3 输入 `-name` 和一个空格。

- 4 输入引号中的通配符模式。

- 5 输入 `-print` 并按回车。

- 输入文件名。

### 额外

除了按名称或通配符模式搜索外，你还可以根据文件的其他属性搜索，例如文件的最后修改时间、所有者或权限。你可以通过在目录路径之后包含的参数来控制搜索。

| 参数 | 查找内容 |

| --- | --- |

| -groupname | 属于特定组的文件。 |

| -iname filename | 类似 name，但不区分大小。 |

| -mmin minutes | 在指定分钟内修改的文件。 |

| -mtime days | 在指定天数内修改的文件。 |

| -perm charmode | 设置了特定权限的文件。 |

| -size charsc | 大小精确为指定字符的文件。 |

![](/8d9b2c31cb5eb6571f0b2dfd7c634cf_40_0.png)

## MAC 版 UNIX

## 更改当前目录

你可以使用 `cd` 命令来更改当前目录。每个 shell 窗口都在文件结构中的特定位置运行，你可以通过输入 `pwd` 命令来查看此位置。`pwd` 命令是 print (working) directory（打印工作目录）的缩写。当前工作目录是查找或保存文件时相对路径的默认目录。

如果你输入 `cd`，它将带你回到主目录（Home directory）。如果你为 `cd` 命令提供路径参数（无论是相对路径还是全路径），它将切换到该目录。你可以切换到任何授予你访问权限的目录。这允许你探索硬盘上几乎所有的目录，受保护的少数系统目录除外。

当当前目录发生变化时，提示符也会随之改变，以反映新位置。提示符会显示当前位置上方最多三个目录的名称，或者在你靠近根目录时。例如，如果你在名为 user 的计算机的 `/usr/share/tsh/` 目录下，你的提示符看起来如下：

```
user@/usr/share/tsh%$
```

你可以在 `cd` 命令中使用通配符和文件名补全；它接受如 `cd ..`（进入上一级目录）和 `cd -`（切换到用户主目录）等名称。你也可以使用 `cd -` 命令返回上工作的目录。

## 确定你的目录

shell 显示当前的位置。

- 输入一个新的目录名称并按回车。

- 输入 `pwd` 并按回车。

- 输入 `cd` 和空格。

- 你的当前目录切换到新位置。

# 操作目录

你可以使用目录栈（directory stack）在文件系统中进行移动。栈是 shell 跟踪的目录列表。你可以通过输入 `dirs` 列出栈。

要切换到一个新目录并将其添加到目录栈，请使用命令 `pushd pathname`。该命令向栈中添加新路径并打印栈。你可以通过输入 `popd` 从栈顶端移除目录并切换到下一个，或者通过输入 `pushd --` 交换两个条目并切换到新的顶层目录。如果你需要在同一个 shell 窗口中在几个目录之间切换，目录栈非常有用。

示例：

```
user@~/Documents$ pushd /usr/lib
user@/usr/lib$ pushd /etc
user@/etc$ popd
user@~/Documents$
```

重复步骤 2 和 3 以移动到新目录。

- 输入 `cd -` 并按回车。你的当前目录切回到之前的目录。

- 输入 `cd` 并按回车。你的当前目录切换到你的主目录。

## 创建目录

你可以使用 `mkdir` 命令创建新目录。目录对于将文件组织成逻辑结构非常有用。当你在 Unix shell 中创建一个目录时，你可以通过 Mac OS 作为一个文件夹访问它；当你在 OS X 中创建一个带空格的文件夹时，你可以在 Unix shell 中作为目录访问它。

传递给 `mkdir` 命令的参数会影响新目录的创建方式。如果你创建一个名称带有空格的目录，必须用引号括起来，除非你想一次创建多个目录。

要创建目录，你需要对当前目录或创建新目录的目标目录具有写入权限。如果你想创建目录 `/usr/local/resp`，你必须对 `/usr/local` 目录具有写入权限。你可以使用 `cd` 命令将工作目录更改到 `/usr/local` 并输入 `mkdir resp`，也可以从任何当前目录输入 `mkdir /usr/local/resp`。

当你提供路径（相对路径或全路径）时，中间的目录必须存在。如果不存在，你将收到错误信息且目录不会被创建。你可以使用 `-p` 创建任何新目录。例如，要创建目录 `~/Documents/by-date/2003/0`，你的命令会在它们不存在时创建 `by-date` 和 `2003` 目录以及目标目录——假设你主目录下的 Documents 目录已经存在。

- 1 输入 `mkdir` 和空格。

- 2 shell 创建新目录。

## 一次创建多个目录

- 1 输入 `mkdir` 和空格。

- 2 输入你想创建的几个目录名称并按回车。

- shell 创建这些新目录。

## 补充

默认情况下，系统可以读取并执行你创建的目录，这意味着你电脑的所有用户都可以切换到新目录并列出其内容。如果你不希望这样做，可以使用 `chmod` 命令更改目录权限。

### 额外

# 操作目录
