

如果你不想去 Ubuntu 软件中心就安装单个软件包，可以通过输入 `sudo apt-get install package-name` 来实现。例如，如果你想下载并安装 Shufflepack 的克隆版本 Tuxpuck，你需要输入 `sudo apt-get install tuxpuck`。如果你在多次安装 Tuxpuck 后最终对它感到厌烦了，可以通过输入 `sudo apt-get remove tuxpuck` 来卸载它。

最后，在记住第 6 章提供的所有警告的情况下，如果你想通过命令行升级整个系统，可以输入 `sudo apt-get dist-upgrade` 来实现（但前提是必须先执行 `sudo apt-get update`）。

## $ finger

如果你在本章开头喜欢通过 `whoami` 命令发现自己是谁，那么你可能也会喜欢使用 `finger` 命令了解更多关于自己的信息。你可以以多种方式使用 `finger` 命令，但非常简单的一种是查询特定用户的信息。为了尝试一下，你必须先安装 `finger`，因为它不再包含在 Ubuntu 中了。

这是一个练习你刚刚学到的 `apt-get` 命令的绝佳机会。打开终端，输入 `sudo apt-get install finger` 并按回车键。一旦输入了密码并准备好尝试 `finger`，只需输入 `finger` 加上你的用户名。在这种情况下，就是 `finger rg`。输入命令后，按回车键并查看结果。你可以在图 8-8 中看到我的结果。

```
rg@mysdesk:~-rg@mysktop:-$ rg
Login: rg Name: Rickford Grant
Directory:/home/rg
Shell: /bin/bash
On since Wed Mar 21 10:44 (EDT) on pts/1 from :0
No mail.
No plan.
rg@mysktop:-$
```

图 8-8：`finger` 命令的输出

如你所示，我的登录名是 rg，我的真实名是 Rickford Grant，我的家目录是 /home/rg，我正在使用 Bash shell 来输入你的命令。我从 3 月 21 日星期三 10:44（东部夏令时间 EDT）起一直登录状态，我没有邮件也没有计划。它没有告诉你我的社会安全号码或母亲的娘姓，但它挺酷的，你不觉得吗？

## 什么是 Shell（外壳）？

正如你注意到的，我提到 `finger` 命令的结果显示显示我正在使用 Bash shell，所以你可能很好奇 Bash 是什么。嗯，Bash（Bourne Again Shell）是 Linux 系统中使用的许多 shell 之一，而且恰好就是你的 Ubuntu 发行版（以及大多数其他发行版）自带的。shell 是一个程序，它可以解释你在终端中输入的命令并将其交付——可以这么说——交付给你的系统去执行这些操作。我喜欢将其认为为一个命令处理子系统，终端充当了图形化前端。

## 什么是 Plan（计划）？

我还提到结果说我没有计划，所以你可能也好奇这到底是怎么回事。plan 是保存在你文件夹中的一个小文件，其他用户在使用 `finger` 命令时会看到它。传统上，plan 文件包含关于你打算去哪里或正在忙什么的信息。然而，如今，大多数人使用它们来留下一些奇怪的小消息、引言之类的，就像他们在签名中做的那样。看一眼图 8-9，看看我在文件夹中添加一个 `.plan` 文件后发生了什么。

```
rgmydesktop:~# finger rg
grmydesktop:~$ finger rg
Login: Name: Rickford Grant
Directory: /home/rg
Shell: /bin/bash
Since Wed Mar 21 15:33 (EDT) on pts/1 from :0
No mail.
Plan:
I was the victim of a series of accidents. . . as we all.
grmydesktop:~$
```

图 8-9：带有计划的 `finger` 命令输出

现在你可以看到我的计划了，那是库尔·冯内格特《泰坦的倾声》（或者说是 Al Stewart 同名的故事）。当然，你可以在你的计划里放任何你想放的内容。如果你觉得有趣，你将在第 141 页的“项目 8A：创建计划”中获得创建自己的 plan 文件的机会，更多精彩在等着你。

## finger 命令的其他用途

在继续之前，我应该提到你也可以使用 `finger` 命令进行某种小小的“国内间谍”活动。假设你的朋友 Chris 在你的机器上有一个用户账户。Chris 想获得你的许可去看电影，他声称一整天都在电脑前苦命地为学校写报告。你心存怀疑，可以输入 `finger chris` 看看事实究竟是怎样的。这可能有点阴险且卑劣，但它确实管用。它也双向有效；其他人也可以检查你。如果你在第 9 章创建一个新的用户账户，可以尝试一下。只需输入 `finger`、你当前未登录的账户名称，然后按回车键。

你甚至可以使用 `finger` 命令查询其他系统上人员的信息，前提是他们网络的 finger 服务处于激活状态，并且你知道他们的邮箱地址。输入类似 `finger username@hostname.com` 的命令就能起作用。这挺酷的，但也有点诡异，我这么觉得。

## 你很快将使用的另外两个命令

这里是介绍两个命令的好地方，这两个命令将在本章以及书中其他地方被用到：`ln` 和 `tar`。你现在不需要练习它们，因为你很快就会用到，但你最好先知道它们是怎么回事。

## $ ln

你使用 `ln`（link）命令来创建一个指向另一个文件夹中文件的链接。当你想要激活位于硬盘上深层子文件夹的文件时，这非常有用。该命令通常与 `-s`（符号）标志一起使用，它提供的功能类似于你在 Windows 中熟悉的快捷方式，或者 Mac 中的别名。

使用 `ln` 最简单的方法是先使用 `cd` 命令将终端的位置切换到你想放置链接的文件夹。然后输入 `ln` 命令，后面跟着你想要链接的文件路径。例如，假设你想在家目录中为一个名为 `myLife.odt` 的 LibreOffice 文件创建一个链接。

该文件深埋在家目录的嵌套子目录下：`/home/username/Documents/personal/self/autobiography/myLife.odt`。要创建它，你需要打开终端窗口，输入以下命令字符串，然后按回车键：

```
ln -s Documents/personal/self/autobiography/myLife.odt
```

完成后，链接将以原文件外观相同的图标出现在你的家目录中，并带有箭头指示这是一个链接。

## $ tar

在第 7 章你学习了创建和提取归包（tar 包），但你知道你也可以通过命令行创建和提取 tar 包吗？`tar` 命令是你执行此操作的关键。

要创建一个存档，只需输入 `tar -cvf`，后面是生成的 tar 包名称，然后是你尝试存档的文件夹或文件名称。例如，假设你想为 `photos` 文件夹创建一个存档，并将其命名为 `pics4pals`。在这种情况下，你输入命令并按回车键：

```
tar -cvf pics4pals.tar photos
```

正如你无疑注意到的，这里有一些标志（flags）。

