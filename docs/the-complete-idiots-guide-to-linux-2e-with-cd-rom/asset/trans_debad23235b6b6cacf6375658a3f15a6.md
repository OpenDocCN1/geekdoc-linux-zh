

要提取使用 dump 备份的文件，请使用 restore。restore 会将存储在 dump 磁带或文件中的文件复制到当前目录。需要注意的是，使用 restore 会覆盖同名已存在的文件。restore 在提取文件之前也会创建所需的任何目录或目录树。如果您知道自己在做什么，此功能非常强大。如有疑问，请将文件使用 restore 提取到一个空目录，然后手动移动文件。restore 的语法如下：

```
restore [options [argument ...]]
```

要指定备份所在的设备，请使用 -f 选项并在其后跟上 dump 的位置。

restore 命令具有易于使用的交互式 shell 类似界面，允许您像在文件系统一样浏览 dump 磁带。通过使用 -i 选项启动交互式会话：

```
restore -f /dev/nst0 -i
```

当 restore 加载后，您可以使用诸如 cd 和 ls 之类的命令在磁带目录中移动。这些命令是 restore 内置的，与 shell 中使用的命令不同。

要将文件添加到要提取（恢复）的文件列表中，输入 add filename，其中 filename 是您要提取的文件名。如果添加一个目录，其包含的所有文件和目录都会被添加。要从列表中删除文件，输入 del filename。此命令不会从磁带中删除文件；它只是将其从提取列表中移除。要提取文件，只需输入 extract。提取结束时，会询问您是否要为 '.' 设置所有者/模式？[yn] 您应回答 no，因为这可能会更改 restore 将要提取文件的目录的所有者和模式。

下面是一个示例会话：

```
1: [root@digital /tmp]# restore -i -f /dev/nst0
2: restore > ls
3: :.
4: auto/ dev/ etc/ home/ root/ tmp/ var/
5: restore > add home
6: restore > ls
7: :.
8: auto/ dev/ etc/ *home/ root/ tmp/ var/
9:
10: restore > del home
11: restore > ls
12: :.
13: auto/ dev/ etc/ home/ root/ tmp/ var/
14:
15: restore > cd home/alberto/test
16: restore > ls
17: ./home/alberto/test:
18: afile
19:
20: restore > add afile
21: restore > extract
22: You have not read any tapes yet.
23: Unless you know which volume your file(s) are on you should start
24: with the last volume and work towards the first.
25: Specify next volume #: 1
26: restore > quit
27: [root@digital /tmp]# ls
28: home
29: [root@digital /tmp]# cd home/alberto/test
30: [root@digital test]# ls
31: afile
```

我使用的 Linux 版本附带的 restore 有一个问题。如果您尝试添加一个文件，它会给出错误信息。解决方法是添加一个目录，例如 home（参见上一列表的第 5 行）。请注意，当您添加文件或目录时，restore 会在旁边放置一个星号 (*) 来标记它（参见第 8 行）。添加此目录后，删除它（参见第 10 行）。然后您可以按需添加文件。父目录将被自动添加。当您完成文件选择后，输入 extract（参见第 21 行）。Dump 会要求您读取磁带。如果您的 dump 仅跨越一个磁带，输入 1；否则，输入用于此 dump 的最后一个磁带的编号。要获取 dump 的信息，输入 what。要获取交互式 restore 的帮助，输入 help 或 ?，它会打印以下信息：

```
restore > ?
Available commands are:
    ls [arg] - list directory
    cd arg - change directory
    pwd - print current directory
    add [arg] - add `arg' to list of files to be extracted
    delete [arg] - delete `arg' from list of files
        to be extracted
    extract - extract requested files
    setmodes - set modes of requested directories
    quit - immediately exit program
    what - list dump header information
    verbose - toggle verbose flag (useful with `ls')
    help or `?' - print this list
If no `arg' is supplied, the current directory is used
```

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## restore Examples

交互式恢复比使用命令行更容易。然而，您也可以这样做。要恢复特定文件，请指定 -x 选项并提供相对于根的路径，如下所示：

```
restore -x home/alberto/file.rtf -f /dev/nst0
```

前面的命令将提取 (-x) 指定的文件 (/home/alberto/file.rtf) 从磁带到当前目录。如果目录路径不存在，restore 将创建它们。最好将目录更改为 /tmp，这样恢复的文件会进入安全位置，并且不会覆盖现有文件。文件恢复后，您可以将文件移动到最终目的地。

要从 dump 磁带上的文件创建目录列表，请使用 -t 选项。除非您知道磁带驱动器支持读写后验证，否则最好始终从磁带创建目录列表。这将确保您制作的备份磁带包含正确的信息并且磁带可读。

要创建目录列表，输入以下内容：

```
restore -t -f /dev/nts0 > tapecat.txt
```

这将创建一个名为 tapecat.txt 的文件，其中包含磁带上文件的列表。

## Graphical Backup Programs

有几个图形备份程序可用：BRU2000，包含在您的 CD 上，以及 KDat，一个 KDE 备份应用程序（有关 KDat 的更多信息，请访问 http://www.kde.org）。

## BRU2000

目前，OpenLinux 包含 BRU2000 的许可证，这是一个可以通过命令行和图形界面执行类似 dump 的系统备份的程序。与 dump 相比，其最大的优势在于使用其图形用户界面，因此易于使用。无需担心磁带大小和其他棘手细节，这可能非常值得。程序的使用是自解释的。您首先选择备份设备（/dev/nst0 或适用于您的设备）。要创建备份设备，只需在文件菜单下使用新建设备命令。在选择备份设备后，您需要从选项菜单下的备份命令中选择备份选项。对话框将要求各种设置。然后点击备份按钮。这会提示您选择要备份的文件。从那里，点击开始备份按钮，您就可以开始了。

与 dump 一样，BRU 支持增量备份，因此您可以实施“备份策略”一节中讨论的备份策略。

以下是该程序的一些屏幕截图：

![](img/edf072a03d4de1f8f4a13465ac79e7fb_242_0.png)

![](img/edf072a03d4de1f8f4a13465ac79e7fb_242_1.png)

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 20
Installing Programs and Applications

### In This Chapter

- RPM: The Red Hat Package Manager
- Installing, Upgrading, Downgrading, and Removing Software
- Verifying Your System
- Graphical Front Ends to RPM
- Non-RPM Packages

通过使用 RPM，Linux 上的软件安装相当复杂。尽管您可以安装由 tar 和其他程序归档的软件，但大多数时候您希望安装 RPM 包。毋庸置疑，当您可以选择要安装的包格式时，请选择 RPM 版本。RPM 包提供了众多好处，这就是为什么我们会详细介绍它。

## RPM: The Red Hat Package Manager

RPM 是一个开放的软件和源代码打包系统。它最初为 Linux 开发，但此后已在 GPL 下向任何人提供使用。

RPM 是一个很棒的打包系统，因为它不仅像其他系统多年来所做的那样处理软件安装，而且还维护一个数据库

