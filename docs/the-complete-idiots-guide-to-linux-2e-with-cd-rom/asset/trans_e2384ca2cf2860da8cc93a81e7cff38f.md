

| *.txt | 匹配所有以 .txt 结尾的文件 |
| file* | 匹配所有以单词 file 开头的文件 |
| file*.txt | 匹配所有以单词 file 开头并以 .txt 结尾的文件 |

## Match Any Letter: ?

星号非常强大，无可否认。有时，事实上它太强大了。因为它可以代表任意数量的字符，它可能会匹配你不想匹配的内容。幸运的是，有一个更克制的元字符：? 将精确匹配一个字母，无论该位置的字符是什么。但是，如果你指定的位置没有字母，就不会匹配。参见表 14.2 中的示例。

## Table 14.2 Examples of Using the Question Mark

| Example | Description |
| file?.txt | 匹配所有以 file 开头，其后跟一个字符并以 .txt 结尾的文件 |
| ? | 匹配所有名称为一个字母的文件 |
| ?? | 匹配所有名称为两个字母的文件 |

## Match in a Range: []

有时你想要匹配多种选项。假设你想使用元字符来查找 file1.txt 和 file2.txt 但不查找 file3.txt。在这种情况下，你需要提供一组用括号括起来的选项，像这样：

```
file[12].txt
```

此模式将匹配 file1.txt 和 file2.txt——其他文件不会匹配。

如果你想查找连续的字符范围——比如你想匹配 0 到 5 的数字——你可以将它们指定为 [0–5] 而不是 [012345]。

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Negating a Range: !

有时指定你不想匹配的内容更容易。例如，如果你有名为 f11、f12、f13、f14 和 f15 的文件，并且你只想移动 f12-f15，你可以像我在这里做的那样指定范围。但使用 f11[!1] 指定你不想的文件可能更容易。在这种情况下，除了 f11 之外的每个文件都会被匹配。

## Command History

每当你在 shell 上输入命令时，shell 都会在称为历史列表的内容中记住它。你可以通过在 bash 提示符下输入 history 来查看历史记录。所有你输入的命令列表将被列出。每个命令都有一个与其关联的编号。

你可以“回收”历史记录中出现的命令，以避免重新输入它们。要重新执行出现在命令历史记录中的命令，只需输入感叹号 (!) 后跟你想要重新执行的命令的编号：

```
[alberto@digital alberto]$ !138
```

你输入的最后一个命令是特殊的。如果你想重复它，只需输入两个感叹号 (!!)。例如，你可以输入：

```
[alberto@digital alberto]$ !!
```

你可以通过使用键盘上的向上箭头向上浏览命令历史记录。这样会将命令放在你的提示符上，以便你在重新执行之前有机会编辑它。

你的历史记录保存多少个命令取决于 HISTSIZE 环境变量的设置。默认情况下，它设置为记住你最后 100 个命令。

## Jobs: Working on Multiple Things Using a Shell

某些命令行作业完成需要一段时间。例如，命令 ls -R / > filelist.txt 2> error.txt 在完成之前可能需要几分钟。如果有很多文件并且正在列出多个网络驱动器，预计它会运行半个小时左右。

由于 Linux 是多任务的，你可能希望在命令运行时做其他事情。你可以通过并发运行命令或在后台运行命令非常轻松地做到这一点。要在后台执行相同的命令，输入以下内容：

```
ls -R / >filelist.txt 2>error.txt &
```

关键是命令行的末尾的与号 (&)。这告诉 shell 在后台运行作业。发出命令后，你会看到如下内容：

```
[alberto@digital alberto]$ ls -R / > filelist.txt 2> error.txt &
[1] 872
[alberto@digital alberto]$
```

作业开始，你的命令行返回。方括号中的数字是分配给你的命令的作业编号或进程 ID。872 是系统范围进程列表中作业的进程 ID。作业的进程 ID 在你需要终止作业时很有用（参见第 22 章“系统监控：关注你的系统”中的“终止进程：kill”）。作业比 872 的进程 ID 更容易记住。当引用作业编号时，始终在前面加上百分号 (%) 符号。两者都为你提供了一种控制命令并将其返回前台的方法。当作业完成后，你会看到如下行：

```
[1]-  Done              ls -R / >filelist.txt 2>errors.txt
```

这意味着你的作业已完成运行。请注意，产生大量显示输出的程序不应在后台运行，除非输出被重定向。否则，你的命令提示符将难以使用，因为来自后台命令的输出会在你输入时继续出现！

一些程序需要交互式输入，所以偶尔你会看到这个：

```
[1]+  Stopped (tty output)    telnet localhost
```

这意味着作业需要输入，并已暂停等待你的按键。要将作业带回前台并输入所需的按键，请使用 fg 命令：

```
[alberto@digital alberto]$ fg %1
```

这会将作业编号一 (%1) 带回前台。请注意，作业编号前有一个百分号 (%)。

要列出从当前 shell 启动的所有作业，请使用 jobs 命令，如下所示：

```
[alberto@digital alberto]$ jobs
[1]+  Stopped (tty output)    telnet localhost
```

## Suspending a Job

你可以通过按 Ctrl+Z 来暂停在前台运行的进程。这会使进程进入睡眠状态：

```
[alberto@digital alberto]$ ls -R / > filelist.txt 2> errors.txt

[1]+  Stopped                ls -R / >filelist.txt 2>errors.txt
[alberto@digital alberto]$ bg %1
```

```
[1]+ ls -R / >filelist.txt 2>errors.txt &
```

在此列表中，我在前台启动了一个冗长的进程。然后我通过按 Ctrl+Z 将其置于睡眠状态（停止它），并使用 bg %1 在后台将其恢复。bg 与 fg 命令相反。

## Killing a Job

要终止当前前台进程，你可以发出 Ctrl+C。这将终止进程。要终止在后台运行的作业，你可以使用 kill 命令，后跟其作业编号或其进程 ID：

```
[alberto@digital alberto]$ kill %1
[alberto@digital alberto]$ kill 872
```

正如你所见，shell 既强大又复杂。即使我们只触及了它的皮毛，你所知道的知识也能帮助你完成大量工作！

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)

Author(s): Manuel Ricart

ISBN: 078971826x

Publication Date: 12/22/98

Bookmark It

Search this book:

Previous Table of Contents Next

## Chapter 15
Help Please

## In This Chapter

- Accessing the UNIX Manual Pages
- Searching for Help by Keyword
- The Whatis Database
- Getting Online Help
- Finding Your Answer with HOWTO Documents
- The Linux Documentation Project (LDP)
- Reading Info Pages

到目前为止，你一直依赖这本书来获取有关 Linux 的信息。讨论的命令只是可用命令的一小部分。这本书没有解释如何配置或使用你最终想要在系统上运行的许多东西；为此我需要另外 400 页。

在你绝望之前，请记住，这本书旨在让你快速掌握与 Linux 和 UNIX 相关的许多基本主题。为了让你获得全面的理解，你将不得不通过额外的来源补充你在这里找到的信息。其中一些来源已在你的计算机中；其他来源可从其他书籍或通过互联网免费获得的资源中获得。

在本章中，你将对可以利用的各种资源进行简短的巡视，以掌握 Linux。这将使你能够自行查找和解决问题。通过阅读和根据需要进行试验，你将学到很多东西。

Linux 有趣的一点是它文档齐全。其他操作系统（OS）为你提供有关系统某些方面的详细信息的，而你很快就会意识到 Linux 提供了关于其中几乎所有已安装内容的丰富信息。这主要是由于 Linux 的开放性质。在一个工具由分散的程序员集合添加的世界中，

