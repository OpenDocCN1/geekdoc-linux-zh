
在我看来，GNU 项目三个最伟大的作品是他们开发的出色的编译器系统（该编译器非常好，以被整合到许多商业 Unix 版本中）、经过深度修改的 GNU `emacs`，以及这个幽默命名的“Bourne Again Shell”（记得 Steve Bourne 写了最初的 Unix shell 吗？）。

`bash` 脱颖而出的原因在于，设计者包含了一系列卓越的功能和能力，使得 `sh`、`csh` 和 `ksh` 用户在切换时对现有的按键序列几乎或完全不需要任何更改。创新是好事，因为强迫用户学习全新的东西是一条艰难的道路。此外，`bash` 也有一些独特的功能和能力。

其他 shell 存在于特殊领域。C shell 的修改版本 `tcsh` 是 95% 的 `csh` 加上 5% 的新功能。由康奈尔大学的一些工程师维护，`tcsh` 最重要的新增是：

- `emacs` 风格的命令编辑
- 视觉化的命令历史
- 通过前几个字符进行交互式文件补全

# (命令行)Shell 游戏

273

1. 确定系统上可用的哪些 shell 最简单的方法是在 `/bin` 目录中查找 `*sh*`。我将使用通配符最方便地完成这一操作：

```
$ ls -F /bin/*sh
/bin/csh* /bin/ksh* /bin/rksh* /bin/sh*
```

2. `bash` 在哪里？不同的系统在其他地方有“非 Posix”——也就是说，非标准的——shell。确定其他 shell 可能所在的位置，一个明智的方法是查看你的 `PATH` 环境变量：

```bash
$ echo PATH
/usr/bin:/bin:/usr/sbin:/usr/X1R6/bin:/usr/local/bin:/home/taylor/bin:/home/taylor/bin:/home/taylor/bin:/home/taylor/bin:/home/taylor/bin
taylor/bin
```

这个 `PATH` 中包含很多内容，我正在寻找其他的 `bin` 目录。我可以逐一个列出它们（例如，`ls /sbin/*sh*`），但我将使用一种不同的策略：我要显式地查找 Bourne Again Shell（再次 Bourne 壳）：

```bash
$ which bash
/usr/local/bin/bash
```

现在我知道哪个系统有 `bash` 了，让我们看看这个目录下是否还有其他 shell：

```bash
% ls -F /usr/local/bin/*sh
/usr/local/bin/bash*
```

3. 噢，好吧，那个特定目录下只有一个这 shell。

你可以看到，这个特定的 Unix 版本提供了五种登录 shell：`csh`、`ksh`、`rksh`、`sh` 和 `bash`。我选择使用 `bash` 来与 Unix 系统进行交互。

## 任务 13.2：识别你的 shell

你可以使用许多不同的方法来识别你正在使用哪种 shell。然而，最简单的方法是输入 `echo $SHELL`，或者如果失败，则查看 `/etc/passwd` 文件查看你的账户列出了什么。如果无法搜索 `/etc/passwd` 文件（某些系统出于安全考虑没有 `/etc/passwd` 文件），那么了解一些替代方案是有帮助的。

- 1. 识别 shell 的一种简单技术是检查你的提示符（prompt）。如果你的提示符包含 `%`，你可能正在使用 C shell 或修改过的 C shell (`tcsh`)。如果你的提示符包含 `$`，你可能正在使用 Bourne shell、Korn shell、`bash` 或其变体。

# 第 13 小时：命令行 shell 简介

2. 另一种简单的方法是使用 `echo` 命令检查 `SHELL` 环境变量的值。

```bash
$ echo SHELL
SHELL
```

哎呀！让我们重试，记住加上 `$` 来表示我们正在请求名为 `SHELL` 的变量的值，而不是单词本身！

```bash
$ echo $SHELL
/usr/local/bin/bash
```

（在你的系统上，它可能是 `/bin/bash`。）

3. 确定你正在使用哪种 shell 的一种酷炫方法是询问操作系统你当前正在运行什么程序。shell 变量 `$$` 标识 shell 的进程 ID（PID）。你可以使用常用的 `ps`（处理器状态）命令及其 `-p` 进程标志来查看你使用的是哪种 shell。以下是我尝试执行时发生的情况：

```bash
$ ps -p $$
PID TTY STAT TIME COMMAND
9503 p0 Ss 0:00.12 -bash (bash)
```

你可以看到我正在运行 `bash`。在我正在运行的 shell 指示符前面有一个连字符，因为系统以此来表示这个特定的 shell 是我的登录 shell。

4. 找出我正在运行哪种 shell 的另一种方法是查看 `/etc/passwd` 文件，你可以这样操作：

```bash
% grep taylor /etc/passwd
taylor::1001:999:Dave Taylor,,:,/home/taylor:/usr/local/bin/bash
taylorsu::0:0:0:Dave Root:/home/taylorsu:/bin/bash
```

非常有用的结果，但我最终找到了两个匹配项：都是 `taylor` 账户（这是我当前的登录账户）和 `taylorsu` 账户，我不想看到后者。

5. 回忆一下第 8 小时涵盖的内容——“过滤器、管道和通配符！”，这里有一种高雅的正则表达式方法，可以确保我只匹配到我当前的账户：

```bash
$ grep '^taylor:' /etc/passwd
taylor::1001:999:Dave Taylor,,:,/home/taylor:/usr/local/bin/bash
```

这就是我要的！在 `/etc/passwd` 文件中，信息字段用冒号隔开，最后一个字段是登录 shell。正如预期的，你可以看到它是 `/usr/local/bin/bash`。

# (命令行)Shell 游戏

进一步完善：让我们使用 `cut` 命令只切出登录 shell，而不是查看 `/etc/passwd` 文件中的所有内容。

```bash
$ grep '^taylor:' /etc/passwd | cut -d: -f7
/usr/local/bin/bash
```

简而言之，我们告诉 `cut` 使用 `:` 作为字段分隔符，然后只向我们显示第七个字段（这就是登录 shell——你自己数一下）。

- 6. 出于好玩，我将上述的 `cut` 命令作为繁忙系统上命令序列的基础，以看看人们在使用什么。该程序提取密码文件中每行的最后一个字段，然后对匹配项进行排序，逐行显示每个 shell 出现的次数。准备好了吗？

```bash
$ cut -d: -f7 /etc/passwd | sort | uniq -c
1 /bin/
230 /bin/bash
75 /bin/ksh
159 /bin/zsh
382 /noshell
3 /usr/local/bin/bash
6 /usr/local/bin/tcsh
```

如你所见，许多人禁用了 `noshell` 选项，在这个系统上，`csh` 是最流行的。还要注意，这个系统上显然有两个版本的 `bash` 和 `tcsh`。当你想要切出像 `/etc/passwd` 这样的文件中的某一列时，`cut` 命令是一个非常棒的记忆。花点时间在你的系统上学习更多关于它的知识。当你确定了你的 shell，可以考虑选择另一个。如果你还没有尝试过，我建议你试一下 `bash`，它能让你尝试后续课程中的所有示例。

## 任务 13.3：如何选择新 shell

在过去，许多系统切换登录 shell 的唯一方法是请求系统管理员编辑 `/etc/passwd`。你可以使用许多不同的方法来识别你正在使用哪种 shell。然而，最简单的方法是输入 `echo $SHELL`，或者如果失败，则查看 `/etc/passwd` 文件查看你的账户列出了什么。如果无法搜索 `/etc/passwd` 文件（某些系统出于安全考虑没有 `/etc/passwd` 文件），那么了解一些替代方案是有帮助的。

- 1. 识别 shell 的一种简单技术是检查你的提示符。如果你的提示符包含 `%`，你可能正在使用 C shell 或修改过的 C shell (`tcsh`)。如果你的提示符包含 `$`，你可能正在使用 Bourne shell、Korn shell、`bash` 或其变体。

# 第 13 小时：命令行 shell 简介

2. 另一种简单的方法是使用 `echo` 命令检查你的 `SHELL` 环境变量的值。

```bash
$ echo SHELL
SHELL
```

哎呀！让我们重试，记住加上 `$` 来表示我们正在请求名为 `SHELL` 的变量的值，而不是单词本身！

```bash
$ echo $SHELL
/usr/local/bin/bash
```

（在你的系统上，它可能是 `/bin/bash`。）
