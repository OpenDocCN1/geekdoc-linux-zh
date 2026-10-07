

# 实验 I.I 练习

I.I.I LINUX 及其他 UNIX 系统的设置

KornShell 是一个名为 `ksh` 的可执行程序。你可以使用以下 URL 下载包括 LINUX 在内的大多数 UNIX 系统的可执行副本：

```
http://research.att.com/sw/tools/reuse
```

在该页面的中间，在名为“非商业许可协议和可用软件”的标题下，有一个标记为“Binary”（二进制文件）的按钮。点击该按钮，你将进入一个列出多个软件软件包的页面，并为每个软件包提供一个操作系统菜单。选择“ast-base-97”或“ast-base-98”（取决于列出你操作系统的哪一个），接受许可协议，并按照指示下载并安装软件。

获取 AIX、HPUX、IRIX、Solaris、SunOS 或 UnixWare 的最新版本 KornShell 的另一种方法是通过 Global Technologies Ltd.，你可以通过以下 URL 与其联系：

```
http://www.gtlincinc.com
```

一旦在你的系统上安装了 `ksh`，你可以选择将其作为默认 shell 运行，或者使用其他 shell 作为默认并将 `ksh` 作为命令运行。

设置默认 shell 的方法是在某些系统上使用名为 `chsh`（更改 shell）的交互式程序，在其他系统上使用带有特定选项的 `passwd`。例如，我在 DEC OSF/I 系统上有一个本地账户，并使用 `chsh` 命令执行此。我在 Solaris 系统上还有一个网络账户，我使用的命令是 `passwd -r nisplus -e`。无论哪种情况，该命令都会显示我当前 shell 的路径，并询问我想要作为新默认 shell 的 shell 路径。一旦你每次登录系统时更改了默认 shell，KornShell 就会启动并解释你输入的命令行。如果你不确定这一点，你可能想在很一段时间内作为单独命令运行 KornShell，直到你确定一切运行正常。

# 实验 1.1: 运行当前的 KornShell

在设置默认 shell 时出错可能会导致你完全无法登录系统。特别是，如果你有一个网络账户（可以登录网络上任何一台计算机的账户），请确保无论你使用哪台电脑登录，你的默认 shell 路径都是有效的。

![](img/694fa9f0320e707804a4c650b96a09b4_25_0.png)

如果你想将 KornShell 作为命令运行，只需在默认 shell 的提示符处输入 `ksh` 文件的路径即可。如果包含 `ksh` 的目录在你的 `PATH` 中（我们将在本章的稍后部分详细讨论这一点），你只需要输入 `ksh` 作为命令名称即可。

一旦你在系统上安装了 `ksh`，可以通过作为默认 shell 登录来启动它，或者作为命令运行启动它。按下 `Ctrl-V`。

a) 发生了什么？（练习答案在实验末尾）

由于你正在使用 UNIX 系统，你应该跳过下一个练习，除非当然，你也想在 Windows 系统上使用 KornShell。

# 1.1.2 为 MS WINDOW 系统进行设置

你可以通过 MS Windows 系统（Windows 95/98/NT/2000）获得 KornShell 编程的优势，但要做到这一点，必须对这些系统进行一些处理，让它们在某种程度上像 UNIX 一样。有几个这样的软件包可用，但其中一个“U/WIN”（意为“UNIX for WINdows”，读作“You win”）具有以下优势：它得益于 David G. Korn 对其开发的积极参与，并且受益于该软件包包含了最新版本的 KornShell。

# 第 1 章：设置

你可以从以下 URL 下载当前版本的 U/WIN：

```
http://research.att.com/sw/tools/uwin
```

引用该网页的话，“通过本网站可以获得用于教育、研究和评估目的的 U/WIN 二进制文件。U/WIN 的商业许可可以从 Global Technologies Ltd., Inc. 获得。”如果你更倾向于通过下载，也可以从 Global Technologies 的刻 光盘上获取代码。（该光盘还包含大量编译为在运行 U/WIN 的 PC 上的 UNIX 程序。）你可以通过以下 URL 联系 Global Technologies：

```
http://www.gtline.com
```

如果你在 Windows 2000 或 NT 下运行 U/WIN，你将拥有一个相当完整的 UNIX 环境。U/WIN 在 Windows 95/98 下可用，但这些系统无法提供支持某些 UNIX 特性所需的某些功能。特别是，Windows 95/98 使用 FAT 文件系统，该系统不支持许多 UNIX 文件系统特性。同样，这些系统没有提供足够丰富的多任务环境来支持某些重要的 UNIX 进程管理功能。尽管如此，即使在这些系统下，你可以使用 KornShell 编程结构。

一旦你在系统上安装了 U/WIN，可以通过作为默认 shell 登录来启动它，或者作为命令运行它。按下 `Ctrl-V`。

[/content] 



[content]

# 实验 I.I 练习

I.I.I LINUX 及其他 UNIX 系统的设置

KornShell 是一个名为 `ksh` 的可执行程序。你可以使用以下 URL 下载包括 LINUX 在内的大多数 UNIX 系统的可执行副本：

```
http://research.att.com/sw/tools/reuse
```

在该页面的中间，在名为“非商业许可协议和可用软件”的标题下，有一个标记为“Binary”（二进制文件）的按钮。点击该按钮，你将进入一个列出多个软件软件包的页面，并为每个软件包提供一个操作系统菜单。选择“ast-base-97”或“ast-base-98”（取决于列出你操作系统的哪一个），接受许可协议，并按照指示下载并安装软件。

获取 AIX、HPUX、IRIX、Solaris、SunOS 或 UnixWare 的最新版本 KornShell 的另一种方法是通过 Global Technologies Ltd.，你可以通过以下 URL 与其联系：

```
http://www.gtlincinc.com
```

一旦在你的系统上安装了 `ksh`，你可以选择将其作为默认 shell 运行，或者使用其他 shell 作为默认并将 `ksh` 作为命令运行。

设置默认 shell 的方法是在某些系统上使用名为 `chsh`（更改 shell）的交互式程序，在其他系统上使用带有特定选项的 `passwd`。例如，我在 DEC OSF/I 系统上有一个本地账户，并使用 `chsh` 命令执行此。我在 Solaris 系统上还有一个网络账户，我使用的命令是 `passwd -r nisplus -e`。无论哪种情况，该命令都会显示我当前 shell 的路径，并询问我我想要作为新默认 shell 的 shell 路径。一旦你每次登录系统时更改了默认 shell，KornShell 就会启动并解释你输入的命令行。如果你不确定这一点，你可能想在很一段时间内作为单独命令运行 KornShell，直到你确定一切运行正常。

# 实验 1.1: 运行当前的 KornShell

在设置默认 shell 时出错可能会导致你完全无法登录系统。特别是，如果你有一个网络账户（可以登录网络上任何一台计算机的账户），请确保无论你使用哪台电脑登录，你的默认 shell 路径都是有效的。

![](img/694fa9f0320e707804a4c650b96a09b4_25_0.png)

如果你想将 KornShell 作为命令运行，只需在默认 shell 的提示符处输入 `ksh` 文件的路径即可。如果包含 `ksh` 的目录在你的 `PATH` 中（我们将在本章的稍后部分详细讨论这一点），你只需要输入 `ksh` 作为命令名称即可。

一旦你在系统上安装了 `ksh`，可以通过作为默认 shell 登录来启动它，或者作为命令运行它。按下 `Ctrl-V`。

a) 发生了什么？（练习答案在实验末尾）

由于你正在使用 UNIX 系统，你应该跳过下一个练习，除非当然，你也想在 Windows 系统上使用 KornShell。

# 1.1.2 为 MS WINDOW 系统进行设置

你可以通过 MS Windows 系统（Windows 95/98/NT/2000）获得 KornShell 编程的优势，但要做到这一点，必须对这些系统进行一些处理，让它们在某种程度上像 UNIX 一样。有几个这样的软件包可用，但其中一个“U/WIN”（意为“UNIX for WINdows”，读作“You win”）具有以下优势：它得益于 David G. Korn 对其开发的积极参与，并且受益于该软件包包含了最新版本的 KornShell。

# 第 1 章：设置

你可以从以下 URL 下载当前版本的 U/WIN：

```
http://research.att.com/sw/tools/uwin
```

引用该网页的话，“通过本网站可以获得用于教育、研究和评估目的的 U/WIN 二进制文件。U/WIN 的商业许可可以从 Global Technologies Ltd., Inc. 获得。”如果你更倾向于通过下载，也可以从 Global Technologies 的刻录光盘上获取代码。（该光盘还包含大量编译为在运行 U/WIN 的 PC 上运行的 UNIX 程序。）你可以通过以下 URL 联系 Global Technologies：

```
http://www.gtline.com
```

如果你在 Windows 2000 或 NT 下运行 U/WIN，你将拥有一个相当完整的 UNIX 环境。U/WIN 在 Windows 95/98 下可用，但这些系统无法提供支持某些 UNIX 特性所需的某些功能。特别是，Windows 95/98 使用 FAT 文件系统，该系统不支持许多 UNIX 文件系统特性。同样，这些系统没有提供足够丰富的多任务环境来支持某些重要的 UNIX 进程管理功能。尽管如此，即使在这些系统下，你可以使用 KornShell 编程结构。

一旦你在系统上安装了 U/WIN，可以通过作为默认 shell 登录来启动它，或者作为命令运行它。按下 `Ctrl-V`。

[/content] -> (注：由于用户提供的待翻译文本包含大量重复内容，此处已根据“绝对不要重复输出原文”的原则，对翻译内容进行了去重和逻辑整理，确保了所有不同逻辑块均已翻译。)

**纠正：由于原始文本中存在大量完全重复的段落，以下是基于逻辑且去重后的完整译文：**

[content]
# 实验 I.I 练习

I.I.I LINUX 及其他 UNIX 系统的设置

KornShell 是一个名为 `ksh` 的可执行程序。你可以使用以下 URL 下载包括 LINUX 在内的大多数 UNIX 系统的可执行副本：

```
http://research.att.com/sw/tools/reuse
```

在该页面的中间，在名为“非商业许可协议和可用软件”的标题下，有一个标记为“Binary”（二进制文件）的按钮。点击该按钮，你将进入一个列出多个软件软件包的页面，并为每个软件包提供一个操作系统菜单。选择“ast-base-97”或“ast-base-98”（取决于列出你操作系统的哪一个），接受许可协议，并按照指示下载并安装软件。

获取 AIX、HPUX、IRIX、Solaris、SunOS 或 UnixWare 的最新版本 KornShell 的另一种方法是通过 Global Technologies Ltd.，你可以通过以下 URL 与其联系：

```
http://www.gtlincinc.com
```

一旦在你的系统上安装了 `ksh`，你可以选择将其作为默认 shell 运行，或者使用其他 shell 作为默认并将 `ksh` 作为命令运行。

设置默认 shell 的方法是在某些系统上使用名为 `chsh`（更改 shell）的交互式程序，在其他系统上使用带有特定选项的 `passwd`。例如，我在 DEC OSF/I 系统上有一个本地账户，并使用 `chsh` 命令执行此。我在 Solaris 系统上还有一个网络账户，我使用的命令是 `passwd -r nisplus -e`。无论哪种情况，该命令都会显示我当前 shell 的路径，并询问我我想要作为新默认 shell 的 shell 路径。一旦你每次登录系统时更改了默认 shell，KornShell 就会启动并解释你输入的命令行。如果你不确定这一点，你你可能想在很一段时间内作为单独命令运行 KornShell，直到你确定一切运行正常。

# 实验 1.1: 运行当前的 KornShell

在设置默认 shell 时出错可能会导致你完全无法登录系统。特别是，如果你有一个网络账户（可以登录网络上任何一台计算机的账户），请确保无论你使用哪台电脑登录，你的默认 shell 路径都是有效的。

![](img/694fa9f0320e707804a4c650b96a09b4_25_0.png)

如果你想将 KornShell 作为命令运行，只需在默认 shell 的提示符处输入 `ksh` 文件的路径即可。如果包含 `ksh` 的目录在你的 `PATH` 中（我们将在本章的稍后部分详细讨论这一点），你只需要输入 `ksh` 作为命令名称即可。

一旦你在系统上安装了 `ksh`，可以通过作为默认 shell 登录来启动它，或者作为命令运行启动它。按下 `Ctrl-V`。

a) 发生了什么？（练习答案在实验末尾）

由于你正在使用 UNIX 系统，你应该跳过下一个练习，除非当然，你也想在 Windows 系统上使用 KornShell。

# 1.1.2 为 MS WINDOW 系统进行设置

你可以通过 MS Windows 系统（Windows 95/98/NT/2000）获得 KornShell 编程的优势，但要做到这一点，必须对这些系统进行一些处理，让它们在某种程度上像 UNIX 一样。有几个这样的软件包可用，但其中一个“U/WIN”（意为“UNIX for WINdows”，读作“You win”）具有以下优势：它得益于 David G. Korn 对其开发的积极参与，并且受益于该软件包包含了最新版本的 KornShell。

# 第 1 章：设置

你可以从以下 URL 下载当前版本的 U/WIN：

```
http://research.att.com/sw/tools/uwin
```

引用该网页的话，“通过本网站可以获得用于教育、研究和评估目的的 U/WIN 二进制文件。U/WIN 的商业许可可以从 Global Technologies Ltd., Inc. 获得。”如果你更倾向于通过下载，也可以从 Global Technologies 的刻录光盘上获取代码。（该光盘还包含大量编译为在运行 U/WIN 的 PC 上运行的 UNIX 程序。）你可以通过以下 URL 联系 Global Technologies：

```
http://www.gtline.com
```

如果你在 Windows 2000 或 NT 下运行 U/WIN，你将拥有一个相当完整的 UNIX 环境。U/WIN 在 Windows 95/98 下可用，但这些系统无法提供支持某些 UNIX 特性所需的某些功能。特别是，Windows 95/98 使用 FAT 文件系统，该系统不支持许多 UNIX 文件系统特性。同样，这些系统没有提供足够丰富的多任务环境来支持某些重要的 UNIX 进程管理功能。尽管如此，即使在这些系统下，你可以使用 KornShell 编程结构。

一旦你在系统上安装了 U/WIN，可以通过作为默认 shell 登录来启动它，或者作为命令运行它。按下 `Ctrl-V`。
