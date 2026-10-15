
要启动另一个 shell 并在稍后返回当前的 shell，只需通过提供其命令名称来运行新 shell（例如，运行 Bash 的命令是 `bash`）。

这将挂起你当前的 shell 并运行新 shell；当你退出新 shell 时，你将返回旧的 shell。

- 要运行一个新的 Bash shell，输入：

```
$ bash RET
```

### 方法 #2

要用一个 shell 替换你当前的 shell 运行，请使用 `exec`。将要运行的新 shell 的命令名称作为参数提供。这会停止你当前的 shell 并将其替换为新 shell。如果你从登录 shell（login shell）运行，那么当你退出新 shell 时，你将注销登录。

- 要用 Csh 替换你当前的 shell，输入：

```
$ exec csh RET
```

注意：你可以使用 `exec` 在当前 shell 中替换任何命令，而不只是另一个 shell。

### 3.9.2 退出 Shell

使用 `exit` 退出当前 shell。此命令是 Bash 的“内置命令”（built-in）。

- ⇒ 要退出当前 shell，输入：

```
$ exit RET
```

你也可以在 shell 提示符处输入 `CTRL-D`，它可以作为 `exit` 命令的快捷键。

- ⇒ 要退出当前 shell，输入：

```
$ CTRL-D
```

注意：退出登录 shell 将导致你注销系统（参见配方 2.2.2 [注销系统]，第 31 页）。

## 3.9.3 获取你当前 shell 的名称

这是一个显示你当前所处 shell 名称的技巧。特殊变量 `$0`（零）始终被赋予当前运行的 shell 或脚本名称的值（参见配方 3.5 [使用 shell 变量]，第 77 页）。因此在提示符处，`$0` 的值就是当前 shell 的名称——使用 `echo` 显示其值以确定你当前处于哪种 shell 中。

- ⇒ 查看你当前处于哪个 shell 中，输入：

```
$ echo $0
ksh
$
```

在这个示例中，`ksh` 是当前 shell。

注意：这在大多数 shell 中都会输出当前 shell 的名称，但存在极少数例外。对于类 shell 的 `tcsh` 和 `wish` 程序，这将会输出以下错误信息：“can’t read "0": no such variable.”

## 3.9.4 更改你的默认 Shell

使用 `chsh` 更改你的默认登录 shell。当你运行它时，`chsh` 会询问密码（出于安全考虑），然后询问你想将登录 shell 替换为什么 shell。你的答案必须是系统上安装的 shell.³。如果你改变了主意，只需在询问时按（RET）——这样，你的登录 shell 就不会被更改。

要将默认 shell 更改为 `pdmenu`，输入：

```
$ chsh (RET)
Password: sesame (RET)
Changing the login shell for suzie
Enter the new value, or press return for the default
Login Shell [/bin/bash]: pdmenu (RET)
$
```

在这个示例中，密码为 `sesame` 的用户 `suzie` 将登录 shell 更改为了 `pdmenu`。

### 3.9.5 使用其他 Shell

启动另一个 shell 有时是必要的。当你正在运行一种 shell 而又想运行另一种，或者你想在运行命令之前更改某些 shell 设置，并在完成后返回之前的设置，就可以这样做。

下表描述了某些 shell 的替代方案。

| Shell | 描述 | Deb | WWW |
| :--- | :--- | :--- | :--- |
| ash | 这是一个基于 Bash 的 shell，具有特性。 | ash | http://sources.org/ |
| csh | 这是一个类似于 C 的 shell，在 Linux 系统上很流行。 | csh | tcsh |
| esh | 这是一个类 shell 的界面，源于 AT&T Bourne 语言。 | esh | http://olympus.brown.edu/doc/ |
| eshell | 带有 Emacs 交互的 shell，使用 Emacs。 | eshell | http://www.emacwiki.org/ |
| lsh | 许多解释器的完整 shell，与 Bash 相似。 | lsh |  |
| psh | 这是一个基于 Bash 的 shell，是 csh 的实现。 | psh | http://sourceforge.net/projects/ |
| pdmenu | 这是一个全屏菜单系统，带有颜色，旨在供用户选择程序。 | pdmenu |  |
| rc | 这是一个 Plan 9 shell，具有 C 语言语法。 | rc | http://star.ac.uk/~tjg/ |
| tcsh | 这是一个 csh 的增强版本。 | tcsh | http://www.net/ |
| zsh | 类似于 Korn shell，但带有拼写检查和脚本增强功能。 | zsh | http://www.zsh.org/ |

一个列表保存在 `/etc/shells`。

# 第4章：X 窗口系统

X 窗口系统，通常被称为“X”，¹ 是所有流行的 Linux 发行版都自带的图形化界面。X 适用于许多 Unix 操作系统；运行在基于 x86 CPU 系统上的 X 版本被称为“XFree86”。X 的当前版本是第 61修订版——即 `X11R6`。

在控制台中运行的所有命令行工具和大多数应用程序可以在 X 中运行；还有专门为 X 编写的应用程序。

通常，我们从控制台运行 X，但也有其他方法。当你自己的系统上运行 X 时，可以从远程系统运行某些图形程序，并将其显示在你的屏幕上；还有专门为 X 设计的特殊终端，连接到主系统。对于只有键盘、鼠标而没有处理能力的设备，它们就像哑终端（参见配方 2.3 [使用控制台和终端]，第 32 页），但它们是为了访问 X 窗口系统设计的，被称为 X 终端。

本章介绍了如何在 X 中操作：如何启动停止它、运行程序、操作窗口以及根据你的喜好自定义 X。有关安装 X 的信息，请参见 Linux XFree86 HOWTO（配方 2.8.6 [阅读文档和帮助文件]，第 50 页）。

根窗口是位于所有其他窗口后面的背景。它通常被设置为某种颜色，但你可以更改它（参见配方 4.7.3 [更改的

¹ 有时你会发现它被称为“X Windows”，但这个术语在技术上是不准确的。

| 名称 | Deb | RPM | WWW |
| :--- | :--- | :--- | :--- |
| XFree86 | xserver-common | XFree86 | http://www.xfree86.org/ |

（根窗口参数，第 118 页）。X 中的每个程序或应用程序都运行在自己的窗口中。每个窗口在其部分或全部边缘都有一个装饰性边框，称为窗口边界（window border）；L 形的角称为框架（frames）；顶部的窗口栏称为标题栏（title bar），用于显示窗口名称；标题栏的左右两侧侧有几个标题栏按钮（详见食谱 4.3 [操作 X 客户端窗口]，第 105 页）。取决于窗口管理器及其设置，这些元素中的任何一个可能是不可见的。

![](img/87037a08576dd88b212b2f4a41577fd3_131_0.png)

图 4-1。一个简单的 X 会话。

整个可见工作区域（包括根窗口和任何其他窗口）被称为桌面（desktop）。右下角的框被称为分页器（pager），允许你在大型桌面上移动（参见食谱 4.4 [在桌面上移动]，第 108 页）。

窗口管理器（window manager）是一个控制窗口外观和显示方式的程序——可以认为是窗口装扮——并能提供一些额外的或程序管理功能。窗口管理器在你运行 X 时会立即启动。有许多不同的窗口管理器可选，每种都具有多种功能和能力；开始使用 Linux 的乐趣之一就是尝试所有它们以找到你喜欢的一个。食谱 4.7.5 [使用其他窗口管理器]，第 120 页列出了一些更流行或更有趣的管理器列表。

# 第 4 章节：X 窗口系统

窗口管理器通常允许你自定义用于显示窗口的颜色和边框，以及出现在窗口上的按钮类型和位置（参见见，食谱 4.2 在 X 中运行程序，第 101 页）。例如，在上面的示例中，时钟本身是 `oclock` 程序，而它上方的标题栏由 `FVWM2` 窗口管理器绘制。使用 `AfterStep` 窗口管理器时，标题栏看起来会有所不同，如图 4-2 所示。

![](img/87037a08576dd88b212b2f4a41577fd3_132_0.png)

图 4-2。AfterStep 中的 oclock。
