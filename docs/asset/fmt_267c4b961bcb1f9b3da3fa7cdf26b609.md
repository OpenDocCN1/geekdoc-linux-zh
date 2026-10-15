
**代码列表 7.13** 使用 `id` 获取用户身份信息。

### 使用 `id` 检查：

- `- id`

在 shell 提示符处输入 `id` 以查找你的 userid 值和所属组（通过名称和数值）（参见代码列表 7.13）。

## 提示

- 你也可以通过 `id` 检查某人的状态以查找他们属于哪些组（只需替换为其他人的 userid）。
- 使用 `groups` 查找 userid 所在的组——使用人类可读的术语。例如，ejr 属于 wheel 用户，如代码列表 7.13 所示。

## 配置你的环境

### 目录
- 理解你的环境
- 发现当前环境
- 添加或更改变量
- 查看 `zsh` 配置文件
- 更改 `zsh` 路径
- 更改 `zsh` 提示符
- 查看 `bash` 配置文件
- 更改 `bash` 路径
- 更改 `bash` 提示符
- 查看 `ksh` 配置文件
- 更改 `ksh` 路径
- 更改 `ksh` 提示符
- 查看 `csh` 配置文件
- 更改 `csh` 路径
- 更改 `csh` 提示符
- 设置别名

在第 3 章中，`zsh` 为你介绍了 Unix shell——它们是什么以及你可以用它们做什么。在本章中，我们将进一步学习如何使用 `zsh`、`bash` 和 `ksh` 配置你的环境。通过配置环境，你可以让 Unix 适应你的需求，而不是适应一个可能你不喜欢的现有环境。这些配置提示对于不同的 shell 有所不同，请确保遵循适用于你使用的 shell 的说明。

## 理解环境

环境变量是 Unix 系统中的设置，规定了你、你的 shell 以及 Unix 系统如何交互。当你登录 Unix 系统时，它会设置你的环境变量——你使用的 shell 提示符、默认搜索路径以及其他帮助程序运行的信息等。你可能把环境变量想象为有一份标准订单，每天为你提供相同的内容。你设置“环境变量”，除非你另有规定，Unix 系统会将它们交付给你。

技术上，“shell”变量（存在于你使用的特定 shell 中）和“环境”变量（存在于环境中且独立于特定 shell）之间是有区别的。对于大多数目的（包括本书），你可以像我们这样做一样方便地模糊这种区别。只要你知道它们不是同义词就可以了。

基本上，就像午餐一样，你可以通过两种方式配置环境：

- 更改当前会话的变量——就像点今天的特殊订单（例如在三明治里加洋葱和额外奶酪）。你在 shell 提示符处操作，见本章“添加或更改变量”章节。
- 更改后续所有会话的变量——就像更改你的标准订单（例如，当医生让你减少蛋精并建议长期使用芥末酱时）。你在配置文件中操作，见“添加或更改变量”之后的章节。

如果你想更改环境变量，应该首先尝试在 shell 提示符处更改当前会话的变量。这样你就可以在配置文件中将其永久化之前尝试更改。

当你在配置文件更改环境时，请记住配置文件通常按特定顺序运行：

- 全局配置文件（例如 `/etc/profile`）在登录时首次运行。`/etc` 中的这些全局配置文件（如果存在）有助于设置环境，但你无法更改它们。
- 特定 Unix 账户的配置文件（如 `~/.profile` 和 `~/.zshrc`）随后运行。如果你想更改最初在全局文件中设置的环境，可以在自己的个人文件中重置这些值。

这种顺序意味着你的个人配置覆盖系统配置。因此，在修改配置文件时，请确保修改的是最后运行的配置文件。我们将在本章的实际部分告诉你要查找的文件。

## 提示

- 你可以 `echo SHELL` 来提醒自己正在使用什么 shell。更多详情请访问第 3 章。
- 根据你使用的 shell，在本章的其他章节了解如何在系统配置文件中更改环境变量。

在本章接下来的两个章节中，了解如何发现当前环境以及手动添加或更改环境变量。

![](img/30f4227f5df2c6cea63896bef2fc574f_169_0.png)

## 探索你的当前环境

改变环境的良好第一步是确定你拥有什么样的环境。通过本节中的步骤，你可以发现当前设置了哪些环境变量和 shell 变量——包括配置文件中设置的变量以及当前会话的变量（**代码列表 8.1 和 8.2**）。

在执行这些步骤时，你可能想查看本节中的“环境中你不应碰的变量”侧边栏，以获取你应该保持原状的变量列表。然后，在下一节中，查看“你可以修改的变量”以找到你可以更改的变量。

**在 `zsh`、`bash` 或 `ksh` 中显示你的当前环境：**

- `set`

在提示符处输入 `set`。你将看到当前环境变量和 shell 变量的列表，如代码列表 8.1 所示。
某些变量可能看起来很熟悉（显示你的 shell 或用户名的），另一些可能更晦涩（例如显示你运行的最后一条命令的行，在此例中为 `_cd`）。

**在 `csh` 中显示你的当前环境：**

- `setenv`

在提示符处输入 `setenv`。如代码列表 8.2 所示，预配置的变量将与 `bash` 或 `ksh` 提供的环境变量非常相似。

```
[ejr@hobbes ejr]$ set

BASH=/bin/bash

BASH_VERSION=1.14.7(1)

COLUMNS=80

ENV=/home/ejr/.bashrc

EUID=500

HISTFILE=/home/ejr/.bash_history

HISTFILESIZE=1000

HISTSIZE=1000

HOME=/home/ejr

HOSTNAME=hobbes.raycomm.com

HOSTYPE=i386

IFS=

LINES=24

LOGNAME=ejr

MAIL=/var/spool/mail/ejr

MAILCHECK=0

PWD=/home/ejr/src/rpm-2.5.1

ERR=1

OPTIND=1

OSTYPE=Linux

PATH=/usr/local/bin:/bin:/usr/bin:/home/ejr/bin

PPID=1543

PS1=[\u@\w]\$

PS2=~

PS4=

PWD=/home/ejr

SHELL=/bin/bash

SHLV=3

TERM=v220

UID=500

USERNAME=

_cd

[ejr@hobbes ejr]$
```

**代码列表 8.1** 你可以使用 `set` 找出 `zsh`、`bash` 或 `ksh` shell 中存在哪些变量。

## 提示

- 如果我们经常执行并尝试使用显示环境变量（“显示”变量似乎是合法的，对吧？），你可能会收到一个关于标准邮件目录和 MH 程序的奇怪问题。只需按 Ctrl+C 返回你的 shell。
- 如果环境变量列表很长，你可以管道给 `sort` 或 `setenv`，这样你就可以一次读取屏幕变量。尝试 `set | sort` 或 `setenv i | sort | more`。参见第 1 章了解关于管道命令的提醒。

```
xmission> setenv

HOME=/home/users/ejray

PATH=/usr/local/bin:/usr/local/bin/X11/:/usr/openwin/bin:/usr/bin:/usr/ucb/.

LOGNAME=ejray

HZ=100

TERM=vt100

TZ=MST7MDT

SHELL=/usr/bin/csh

MAIL=/var/mail/ejray

PWD=/home/users/ejray

USER=ejray

EDITOR=pico -t

OPENHOME=/usr/openwin

MANPATH=/usr/man:/usr/local/man/:/openwin/man

LD_LIBRARY_PATH=/usr/local/lib:/usr/openwin/lib

PAGER=more

xmission>
```
