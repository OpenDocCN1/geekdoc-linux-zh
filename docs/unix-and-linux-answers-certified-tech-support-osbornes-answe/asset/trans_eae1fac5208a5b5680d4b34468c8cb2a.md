

一般来说，NT 在这方面做得要好得多。微软从来没能很好地管理打印 spooling。

## SHELL EMULATIONS: MAKING NT FEEL LIKE UNIX, AND UNIX FEEL LIKE NT

## What is the "standard" UNIX shell?

没有标准的 UNIX shell。最常见的替代品是 Korn shell（我们个人最喜欢的）、Posix shell（大多数新 UNIX 版本的默认 shell，与 Korn shell 关系密切）、Bourne shell（通常是最低公分母）以及 C shell。还有一些备选的自由软件 shell，例如 Bourne Again Shell（bash），由于其通常可在包括 Linux 在内的各种平台上获得，因此获得了大量追随者。你所使用的任何 UNIX 上都可获得大多数可用 shell 的版本，你应根据所处环境的需要或预计需要执行的脚本量来选择使用的 shell。交互式用户往往发现 C shell 或 Korn shell 是最舒适的选择，而密集的脚本编写应使用 Bourne、Posix 或 Korn shell，但通常应按 Bourne shell 的限制编写，以防止跨平台问题。

## How can I make NT behave like UNIX?

市面上有一些产品可以让你即使在 Windows NT 上也能模仿 UNIX 丰富的命令行功能。其中最普及的可能是 Mortice-Kerns 的 MKS ToolKit（http://www.mks.com）。如果你经常在 UNIX 和 Windows NT 或 Windows 95 之间切换，我们强烈推荐这个软件包。它并不完美，有几件事我们真的非常希望它做得更好。尽管如此，它在 Windows NT 上运行的 Posix 或 Korn shell 仿真非常出色，并且包含了我们离不开的最常见的 UNIX 命令行实用程序。它甚至包含了一个相当令人满意的 Perl 到 Windows NT 的移植，用于为你的命令行添加额外功能。

## How can I make NT behave like UNIX without spending any money?

你的选择在这里会更有限。你当然可以通过使用 **doskey** 宏来添加许多熟悉的 UNIX 命令，例如用 **ls** 代替 **dir**。但大多数功能如果不添加第三方实用程序就根本不可用。即使是内置的 Posix 子系统也不再被认证，而且 shell 的有限功能使得完全模仿其行为变得困难。如果你真的必须经常这样做，就去拷贝一份 MKS ToolKit。如果你唯一的需求是偶尔使用 Windows NT，并且讨厌必须记住你的 **cp** 必须全部输入到 **copy**，那么就使用一系列 **doskey** 宏来完成工作。将它们加载到可以从命令行调用的批处理文件中。处理 **cp** 的示例看起来像：

```
doskey cp=copy $*
```

## Can I make UNIX behave like the NT command line?

嗯，我们想你是可以的，如果你真的想的话。尽管我们目前无法理解你为什么要这样做。但对于那些主要界面是 DOS、Windows 95 或 Windows NT 命令行的人来说，如果他们只是偶尔需要使用 UNIX 命令行，我们想这可能有意义。诀窍是利用 Korn 和 Posix shell 内置的能力来创建别名，以模仿 Microsoft 为中心的命令行的行为。对于更简单的命令来说这相当直接，但有些则有点棘手，可能需要你编写一两个 shell 脚本。

你无法轻松改变的一件事是 “/斜杠” 键的方向。如我们在第 3 章前面所见，UNIX 使用标准的正斜杠来分隔目录层级，而 Microsoft 为中心的系统，包括 Windows NT，使用反斜杠来达到相同目的。反斜杠在 UNIX 中通常是转义字符。让 UNIX 中两个键的功能互换可能是可能的，但我们从未见过有人这样做，我们担心你只能习惯这种差异。你可以使用上面讨论过的 MKS ToolKit 让 Windows NT 交换字符以像在 UNIX 中那样表现，所以如果这真的让你抓狂，那可能是你唯一的解决方案。实际上这不是一个坏解决方案，因为你还获得了微软本应给 Windows NT 用户的一套极其有用的实用程序和命令，以及完整的 Posix shell 实现。

那么你从老 DOS 时代熟悉的命令呢？没问题。只需在你的 .kshrc 文件中为你最想念的命令添加一系列别名。我们在表 11-1 中列出了我们最喜欢的一些示例。

| DOS command | Korn or Posix shell alias | Comment |
|---|---|---|
| dir | ls -oA | Shows owner of file and most hidden files. |
| cls | clear | |
| type | cat | Try substituting your favorite pager here for the simple cat. We use less. |
| md | mkdir | |
| deltree | rm -r | Remember, this command is irrevocable and won't ask you to confirm! |
| del | rm | |
| copy | cp | No wildcard substitution. |
| move | mv | No wildcard substitution. |
| ren | mv | No wildcard substitution. |

表 11-1 Korn Shell Aliases for Common DOS and Windows NT Commands

