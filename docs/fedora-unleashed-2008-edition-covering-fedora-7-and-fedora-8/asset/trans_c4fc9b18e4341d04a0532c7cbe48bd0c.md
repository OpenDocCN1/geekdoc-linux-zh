
这会输出 `myfile.txt` 的内容。在此用途中，有两个常用的额外参数：`-n` 为输出中的行添加编号，而 `-s`（“squeeze”）则限制每次最多输出一个空行。也就是说，如果你的文件包含 1 行文本、10 个空行、1 行文本、10 个空行，以此类推，使用 `-s` 后，它将显示第一行文本、一个空行、下一行文本、一个空行，依此类推。当你将 `-s` 和 `-n` 结合使用时，`cat` 仅为实际输出的行编号——显示为 1 行的 10 个空行在编号时仅计为 1 行。

以下命令会输出关于你 CPU 的信息，剔除多个空行并为输出编号：

```
$ cat -sn /proc/cpuinfo
```

你还可以使用 `cat` 一次输出多个文件的内容，如下所示：

```
$ cat -s myfile.txt myotherfile.txt
```

在该命令中，`cat` 将 `myfile.txt` 和 `myotherfile.txt` 在输出中合并，并剔除多个空行。重点在于 `cat` 在输出中不区分文件——不会打印文件名，两个文件之间也没有额外的换行。这使得你可以将这两个文件视为一个，或者通过在命令行中添加更多文件，将 20 个文件视为 1 个。

## 使用 cd 更改目录

更改目录肯定是没有任何选项的事情，对吗？并非如此。`cd` 实际上比大多数人意识到的要灵活得多。与这里的其他大多数命令不同，`cd` 本身不是一个命令——它是内置于 `bash`（或你正在使用的任何 shell 解释器）中的，但它的使用方式仍然像一个命令。

`cd` 最基本的用法如下：

```
$ cd somedir
```

该命令在当前目录中查找名为 `somedir` 的子目录，然后让你进入该目录。你还可以指定目录的确切位置，如下所示：

```
$ cd /home/paul/stuff/somedir
```

`cd` 神奇之处的第一部分在于其使用的字符（`-` 和 `~`，即短横线和波浪号）。前者表示“切换到我上一个所在的目录”，后者表示“切换到我的主目录”。下面这段与 `cd` 的交互展示了这一功能：

```
[paul@caitlin ~]$ cd /usr/local
[paul@caitlin local]$ cd bin
[paul@caitlin bin]$ cd -
/usr/local
[paul@caitlin local]$ cd -
[paul@caitlin ~]$
```

在第一行中，我们切换到 `/usr/local`，命令没有输出任何内容。在第二行中，我们切换到 `bin`，它是 `/usr/local` 的子目录。接着，使用 `cd -` 切换回上一个目录。这一次，bash 打印出上一个目录的名称，让我们知道当前所在位置。最后，使用 `cd` 切换回主目录；如果你想节省几个按键，直接键入 `cd` 等同于 `cd -`。

`cd` 神奇之处的第二部分是其能够在预定义位置中查找目录的能力。当你指定目录的绝对路径（即以 `/` 开头的路径）时，`cd` 始终切换到该确切位置。然而，如果你指定一个相对子目录——例如，`cd subdir`——你可以告诉 `cd` 你希望该目录相对于哪个位置。这是通过 `CDPATH` 环境变量实现的。如果未设置此变量，`cd` 始终以当前目录作为基准；但是，你可以将其设置为任意数量的其他目录。

下一个例子演示了对此功能的测试。它从 `/home/paul/empty`（一个空目录）开始，各行编号以便后续参考：

```
1 [paul@caitlin empty]$ pwd
2 /home/paul/empty
3 [paul@caitlin empty]$ ls
4 [paul@caitlin empty]$ mkdir local
5 [paul@caitlin empty]$ ls
6 local
7 [paul@caitlin empty]$ cd local
8 [paul@caitlin local]$ cd ..
9 [paul@caitlin empty]$ export CDPATH=/usr
10 [paul@caitlin empty]$ cd local
11 /usr/local
12 [paul@caitlin empty]$ cd -
13 /home/paul/empty
14 [paul@caitlin empty]$ export CDPATH=..
15 [paul@caitlin empty]$ cd local
16 /home/paul/empty/local
17 [paul@caitlin local]$
```

第 1-3 行显示你位于 `/home/paul/empty`，并且该目录确实为空——`ls` 没有输出。第 4-6 行显示了创建 `local` 子目录的过程，使得 `/home/paul/empty/local` 存在。第 7 和 8 行显示你可以进入 `/home/paul/empty/local` 然后退出。

在第 9 行中，`CDPATH` 被设置为 `/usr`。选择它是因为 Fedora 拥有 `/usr/local` 目录，这意味着当前目录（`/home/paul/empty`）和 `CDPATH` 目录（`/usr`）都有一个名为 `local` 的子目录。在第 10 行中，当在 `/home/paul/empty` 目录中时，使用了 `cd local`。这一次，bash 切换到 `/usr/local`，甚至打印出新目录以确保你知道它做了什么。

第 12 和 13 行将你移回上一个目录，即 `/home/paul/empty`。在第 14 行中，`CDPATH` 被设置为 `.:/usr`。`:` 是目录分隔符，这意味着 bash 应先在当前目录 `.` 中查找，然后在 `/usr` 目录中查找。在第 15 行中，再次发出 `cd local`，这次移动到 `/home/paul/empty/local`。注意 bash 仍然打印了新目录——只要它在 `CDPATH` 中查找目录，它都会这样做。

## 使用 chmod 更改文件访问权限

之前学到的关于 `chmod` 的知识可以通过一个简单的参数极大地扩展：`-c`。这指示 `chmod` 在操作过程中打印出它所做更改的列表，这意味着你可以捕获输出并将其用于其他目的。例如：

```
[paul@caitlin tmp]$ chmod -c 600 *
mode of '1.txt' changed to 0600 (rw-------)
mode of '2.txt' changed to 0600 (rw-------)
mode of '3.txt' changed to 0600 (rw-------)
[paul@caitlin tmp]$ chmod -c 600 *
[paul@caitlin tmp]$
```

在那里，`chmod` 命令带有 `-c` 参数，你可以看到它输出了操作结果：三个文件被更改为 `rw-------`（仅限用户读写）。然而，当再次发出该命令时，没有返回输出。这是因为 `-c` 仅打印它所做的更改。已经匹配你要设置的权限的文件保持不变，因此不会被打印。

还有两个值得关注的参数：`--reference` 和 `-R`。前者允许你指定一个文件作为权限模板，而不是自己指定权限。例如，如果你希望当前目录中的所有文件都具有与文件 `/home/paul/myfile.txt` 相同的权限，你可以使用：

```
$ chmod --reference /home/paul/myfile.txt *
```

你可以使用 `-R` 启用递归操作，这意味着你可以用它对目录执行 `chmod`，它会更改该目录及其下所有文件和子目录的权限。你可以使用 `chmod -R 600 /home` 将 `/home` 下的每个文件和目录更改为仅对其所有者可读写。

## 使用 cp 复制文件

像稍后介绍的 `mv` 一样，`cp` 是一个易于使用且易于掌握的命令。然而，两个奇妙的参数很少被使用（这很可惜！），尽管它们很有用。它们是 `--parents` 和 `-u`，前者将文件的完整路径复制到新目录中。后者仅在源文件比目标文件新时才进行复制。使用 `--parents` 需要一点解释，所以这里有一个例子。你有一个文件 `/home/paul/desktop/documents/work/notes.txt`，想要将其复制到你的 `/home/paul/backup` 文件夹中。你可以执行普通的 `cp`，但这将得到 `/home/paul/backup/notes.txt`，那么以后你怎么知道它来自哪里呢？如果你使用 `--parents`，文件将被复制到 `/home/paul/backup/desktop/documents/work/notes.txt`。

`-u` 参数非常适合同步两个目录，因为它允许你运行类似 `cp -Ru myfiles motherfiles` 的命令，让 `cp` 仅重新复制已更改的文件。`-R` 参数表示递归，并允许你复制目录内容。

## 使用 du 打印磁盘使用情况

`du` 命令打印当前目录内每个文件和目录的大小。其最基本的用法非常简单：

```
$ du
```

该查询输出一个长长的目录列表以及它们的文件占用的空间。你可以使用 `-a` 参数修改这一点，该参数指示 `du` 打印单个文件和目录的大小。另一个有用的参数是 `-h`，它使 `du` 使用人类可读的大小，如 18M（18MB），而不是 17532（相同的数值，未取整，单位是字节）。最后一个有用的基本选项是 `-c`，它打印文件的总大小。

因此，使用 `du`，你可以获得主目录中每个文件大小的打印输出，格式为人类可读格式，并在末尾带有摘要，如下所示：

```
$ du -ahc /home/paul
```

两个高级参数涉及你希望从统计中排除的文件名。第一个是 `--exclude`，它允许你指定一个应用于排除文件的模式。该模式是标准的 shell 文件匹配模式，而不是正则表达式，这意味着你可以使用 `?` 匹配单个字符，或使用 `*` 匹配零个或多个字符。你可以指定多个 `--exclude` 参数来排除多个模式。例如：

```
$ du --exclude="*.xml" --exclude="*.xsd"
```

当然，重复输入大量的 `--exclude` 参数是浪费时间的，所以你可以使用 `-X` 来指定一个包含你想要排除的模式列表的文件。该文件应该如下所示：

```
*.xml
*.xsd
```

也就是说，你想要排除的每个模式都应独占一行。如果该文件名为 `xml_exclude.txt`，你可以像这样用它替代前面的例子：

```
$ du -X xml_exclude.txt
```
