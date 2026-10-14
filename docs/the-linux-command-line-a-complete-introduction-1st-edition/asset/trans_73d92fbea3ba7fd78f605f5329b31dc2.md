

在我们之前的示例之一中，这次使用 tee 在 grep 过滤管道内容之前，将整个目录列表捕获到文件 ls.txt 中：

```
me@linuxbox ~]$ ls /usr/bin | tee ls.txt | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
```

## 最终说明

一如既往，请查阅本章中我们所介绍的每个命令的文档。我们只看到了它们最基本的使用方式，而它们都有许多有趣的选项。随着我们 Linux 经验的积累，我们会发现命令行重定向功能对于解决专门问题极其有用。许多命令使用标准输入和输出，而几乎所有命令行程序都使用标准错误来显示其信息性消息。

## LINUX IS ABOUT IMAGINATION

当我被问及 Windows 和 Linux 之间的区别时，我经常使用一个玩具类比。

Windows 就像 Game Boy。你去商店买一个全新的、闪亮的盒装玩具。你把它带回家，打开，玩它。漂亮的画面，可爱的声音。然而，过了一会儿，你对随附的游戏感到厌倦，于是你又回到商店买另一个。这个循环一次又一次地重复。最后，你回到商店对柜台后面的人说：“我想要一个能做这个的游戏！”却被告知这样的游戏不存在，因为没有“市场需求”。然后你说：“但我只需要改动这一件事！”柜台后面的人说你不能改动它。游戏都密封在卡带里。你发现你的玩具仅限于他人认为你需要的游戏，不会再多。

Linux 另一方面，就像世界上最大的 Erector Set。你打开它，里面只是一大堆零件——大量钢条、螺丝、螺母、齿轮、滑轮、马达，以及一些建造建议。所以你开始玩它。你先建造一个建议，然后再建造另一个。过了一会儿你发现你自己也有想做的东西。你永远不必再回商店，因为你已经拥有所需的一切。Erector Set 呈现出你想象力的形状。它做你想让它做的事。

玩具的选择当然是个人问题，那么你会觉得哪种玩具更令人满意呢？

## 7

## SEEING THE WORLD AS
THE SHELL SEES IT

在本章中，我们将研究在按下 ENTER 键时在命令行上发生的“魔法”。虽然我们将检查 shell 的几个有趣且复杂的特性，但我们只会使用一个新命令：

- `echo`—显示一行文本。

## Expansion

每次你输入一行命令行并按下 ENTER 键时，bash 在执行你的命令之前会对文本执行多个处理。我们已经见过一些简单字符序列，例如 *，对 shell 来说可以有很大的意义的例子。使这种情况发生的处理过程称为 *expansion*。通过扩展，你输入某物，它在 shell 采取行动之前被扩展为另一物。为了演示我们所说的含义，让我们来看看 echo 命令。echo 是一个 shell 内置命令，执行非常简单的任务：它将文本参数打印到标准输出。

```
[me@linuxbox ~]$ echo this is a test
this is a test
```

这很直接。传递给 echo 的任何参数都会被显示。让我们再试一个例子：

```
[me@linuxbox ~]$ echo *
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

发生了什么？为什么 echo 没有打印 *？正如你从我们对通配符的工作中回忆的那样，* 字符的意思是“匹配文件名中的任意字符”，但我们在最初的讨论中没有看到的是 shell 如何做到这一点。简单的答案是 shell 在 echo 命令执行之前将 * 扩展为其他内容（在本例中为当前工作目录中的文件名）。当按下 ENTER 键时，shell 会在命令执行之前自动扩展命令行上的任何符合条件的字符，因此 echo 命令从未看到 *，只看到了其扩展结果。知道这一点后，我们可以看到 echo 的行为符合预期。

## Pathname Expansion

通配符工作的机制称为 pathname expansion。如果我们尝试在前几章中使用的一些技术，我们会发现它们实际上是扩展。给定如下所示的主目录：

```
[me@linuxbox ~]$ ls
Desktop   ls-output.txt   Pictures   Templates
Documents Music           Public     Videos
```

我们可以进行以下扩展：

```
[me@linuxbox ~]$ echo D*
Desktop Documents
```

以及

```
[me@linuxbox ~]$ echo *s
Documents Pictures Templates Videos
```

甚至

```
[me@linuxbox ~]$ echo [[:upper:]]*
Desktop Documents Music Pictures Public Templates Videos
```

