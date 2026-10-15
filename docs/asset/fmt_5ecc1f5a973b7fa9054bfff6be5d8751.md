
`cat myfile.txt`

这会打印 `myfile.txt` 的内容。对于这种用法，有两个额外的参数经常使用：`-n` 对输出进行编号，`-s`（“压缩”）一次最多打印一行空白行。也就是说，如果你的文件有 1 行文本、10 个空白行、1 行文本、10 个空白行，等等，`-s` 会显示第一行文本、一个空白行、下一行文本、一个空白行，依此类推。当你同时使用 `-s` 和 `-n` 时，`cat` 只对打印的行进行编号——显示为一个的 10 个空白行在编号时算作 1 行。

该命令会打印有关你的 CPU 的信息，去除多余的空白行并对输出进行编号：

```
cat -sn /proc/cpuinfo
```

你也可以一次使用 `cat` 打印多个文件的内容，如下所示：

```
cat -s myfile.txt myotherfile.txt
```

在此命令中，`cat` 将 `myfile.txt` 和 `myotherfile.txt` 合并到输出中，去除多余的空白行。重要的是，`cat` 在输出中不会区分文件——不会打印文件名，也不会在 2 个文件之间添加额外的分隔。这允许你将 2 个文件视为 1 个，或者通过在命令行中添加更多文件，将 20 个文件视为 1 个。

## 使用 cd 更改目录

更改目录肯定是没有选项的，对吧？并非如此。`cd` 实际上比大多数人意识到的更灵活。与这里的其他大多数命令不同，`cd` 本身并不是一个命令——它内置于 bash（或你使用的任何 shell 解释器）中，但它仍然像命令一样使用。

`cd` 最基本的使用方式如下：

```
cd somedir
```

这会在当前目录中查找 `somedir` 子目录，然后将你移动到其中。你也可以指定目录的确切位置，如下所示：

```
cd /home/paul/stuff/somedir
```

`cd` 魔法的第一部分在于字符 `.` 和 `~`，一个破折号和一个波浪号）。第一个表示“切换到我之前的目录”，第二个表示“切换到我的主目录”。与 `cd` 的这次对话展示了这一点：

```
[paul@caitlin ~]$ cd /usr/local
[paul@caitlin local]$ cd bin
```

```
[paul@caitlin bin]$ cd -
/usr/local
[paul@caitlin local]$ cd -
[paul@caitlin ~]$
```

第一行中，我们切换到 `/usr/local` 且命令没有输出。在第二行，我们切换到 `bin`，它是 `/usr/local` 的一个子目录。接下来使用 `cd -` 来切换回上一个目录。这次 Bash 打印了上一个目录的名称，以便我们知道自己所在的位置。最后，使用 `cd -` 切换回我们的主目录，虽然如果你想节省几个按键，只输入 `cd` 本身就等同于 `cd ~`。

`cd` 的第二个神奇之处在于它能够在预定义的位置查找目录。当你指定目录的绝对路径（即以 `/` 开头的路径）时，`cd` 总是切换到那个确切位置。然而，如果你指定一个相对子目录——例如 `cd subdir`——你可以告诉 `cd` 相对于何处进行查找。这是通过 `CDPATH` 环境变量实现的。如果该变量未设置，`cd` 总是以当前目录作为基准；不过，你可以将其设置为任意多个其他目录。

下面的示例展示了对此的测试。它从 `/home/paul/empty` 开始，这是一个空目录，并且行号已标注以便后续引用：

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
14 [paul@caitlin empty]$ export CDPATH=.:/usr
15 [paul@caitlin empty]$ cd local
16 /home/paul/empty/local
17 [paul@caitlin local]$
```

第 1–3 行显示我们位于 `/home/paul/empty` 且它确实是空的——`ls` 没有输出。第 4–6 行显示 `local` 子目录被创建，因此 `/home/paul/empty/local` 存在。第 7 和 8 行显示你可以 `cd` 进入 `/home/paul/empty/local` 再返回。

第 9 行中，`CDPATH` 被设置为 `/usr`。之所以选择它是因为 Ubuntu 有 `/usr/local` 目录，这意味着我们的当前目录 (`/home/paul/empty`) 和 `CDPATH` 目录 (`/usr`) 都存在一个 `local` 子目录。第 10 行中，在 `/home/paul/empty` 目录下，我们使用 `cd local`。这次 Bash 将我们切换到 `/usr/local` 甚至打印新目录以确保我们知道它做了什么。

第 12 和 13 行将我们移回上一个目录 `/home/paul/empty`。第 14 行中，`CDPATH` 被设置为 `.:/usr`。`:` 是目录分隔符，这意味着 Bash 应该先在当前目录 `.` 中查找，然后在 `/usr` 目录中查找。第 15 行再次发出 `cd local`，这次移动到 `/home/paul/empty/local`。请注意 Bash 仍然打印了新目录——只要它在 `CDPATH` 中查找目录就会这样做。

## 使用 chmod 修改文件访问权限

你在第 5 章学到的关于 `chmod` 的知识可以通过一个简单的参数大大扩展：`-c`。该参数指示 `chmod` 在操作过程中打印它所做的所有更改的列表，这意味着我们可以捕获输出并将其用于其他目的。例如：

```
[paul@caitlin tmp]$ chmod -c 600 *
mode of '1.txt' changed to 0600 (rw-------)
mode of '2.txt' changed to 0600 (rw-------)
mode of '3.txt' changed to 0600 (rw-------)
[paul@caitlin tmp]$ chmod -c 600 *
[paul@caitlin tmp]$
```

这里 `chmod` 命令带 `-c` 发出，你可以看到它输出了操作结果：三个文件被更改为 `rw-------`（仅用户可读可写）。然而再次发出该命令时，没有输出返回。这是因为 `-c` 只打印它所做的更改。权限已与你要设置的权限匹配的文件保持不变，因此不会被打印。

还有两个其他参数值得关注：`--reference` 和 `-R`。第一个允许你指定一个文件作为权限模板，而不是自己指定权限。例如，如果你希望当前目录中的所有文件都具有与文件 `/home/paul/myfile.txt` 相同的权限，你会使用：

```
chmod --reference /home/paul/myfile.txt *
```

你可以使用 `-R` 来启用递归操作，这意味着你可以用它来 `chmod` 一个目录，它将更改该目录以及该目录下所有文件和子目录的权限。你可以使用 `chmod -R 600 /home` 将 `/home` 下的每个文件和目录都更改为仅其所有者可读/写。

## 使用 cp 复制文件

与稍后介绍的 `mv` 类似，`cp` 也是一个易于使用和掌握的命令。然而，两个很棒的参数很少被使用（这很遗憾！）尽管它们功能。这些是 `--parents` 和 `-u`，其中前者将文件的完整路径复制到新目录中，后者仅在源文件比目标文件更新时才复制。

使用 `--parents` 需要稍作解释，下面举个例子。你有一个文件 `/home/paul/desktop/documents/work/notes.txt`，想把它复制到你的 `/home/paul/backup` 文件夹中。你可以使用常规的 `cp`，但那样会得到 `/home/paul/backup/notes.txt`，那么以后你怎么知道它来自哪里呢？如果你使用 `--parents`，该文件会被复制到 `/home/paul/backup/desktop/documents/work/notes.txt`。

`-u` 参数非常适合同步两个目录，因为它允许你运行像 `cp -Ru myfiles myotherfiles` 这样的命令，让 `cp` 只重新复制已更改的文件。`-R` 参数表示递归，允许你复制目录内容。

## 使用 du 打印磁盘使用情况

`du` 命令会打印当前目录中每个文件和目录的大小。它最基本的用法再简单不过了：

```
du
```
