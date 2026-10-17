
```bash
# 此脚本显示日期、时间、用户名和
## 当前目录。
echo "Date and time:"
date
echo "Your username is: $(whoami)\n"
echo -e "Your current directory is:\n\n"
pwd
echo "Show disk status \n"
free
echo "List files on current directory \n"
ls
echo "Check current running processes \n"
ps
echo "View the Directory Structure \n"
tree
echo "Information about me \n"
echo "Check what system is running \n"
uname -a
echo "That's the end of the program - exit well \c"
## 程序以这些命令结束
```

## 演示程序

这是一个简单的小脚本，用于展示如何使用我讨论过的所有语句和命令。我们把这个程序命名为`systats`。

```bash
cat systats
#!/bin/sh
# systats
# 由 Dallas G. Releford 编写
# 在下方调用。
```

如果你想尝试这个程序，请记住使用`chmod`命令进行编译，使其可以执行。该程序会告诉你关于你系统的一些信息。这就是你需要的这种类型的实用脚本文件，用于控制你计算机的工作方式——或者只是为了让你知道是谁在使用你的系统。

## 下一步做什么

在你使用 Linux 时，可能会有时需要编写 shell 脚本来执行某些你在系统启动时想要执行的操作。学习这种方法的方法是尽可能阅读关于 `bash` 和脚本的知识。学会它的最好方法是实践。

## 更多关于脚本编写

你可以在官方 GNU 网站`www.gnu.org/manual/bash/index.html`在线找到一份非常棒的`bash`手册。

## Jack Wallen, Jr. 的一小时 Linux 教程，第 1 部分

作者 Jack Wallen, Jr.

我需要学习 Linux，你也需要学习！我该怎么办呢？噢，MacDuff！

在本文中，我将介绍一个希望对你来说学习 Linux 基础入性的最快的方法。这本教程将教你：

- 当你第一次启动新的 Linux 时该做什么。
- 如何运行简单的命令。
- 如何连接互联网。
- 如何通过`.rpm`文件安装。
- 如何在桌面上移动。
- 如何进行一些自定义。

这本教程做出了几个假设，包括：

- 你已经在计算机上安装了 Linux。
- 计算机正作为桌面机器使用。
- 你的系统将立即引导到图形登录界面（在`/etc/init`中运行级别为 5）。
- 你正在使用 Red Hat 6.1 Linux 发行版。
- 你正在使用 Red Hat 6.1 安装的默认桌面（`GNOME` 和 `Enlightenment`）。
- 你拥有连接到 ISP（互联网服务供应商）的所有必要信息。

考虑到这些，让我们开始旅程。

## 启动与登录

你 Linux 体验的第一步是引导。当你启动机器时，会看到`LILO`提示符，它包含了允许你执行若干任务的选项。第一个选项是默认选项，或者按 `[Enter]` 或等待时间过期以启动 Linux。第二个选项是按 `[Tab]` 键，它会显示 `LILO`（引导管理器）检测到的操作系统列表。

## Linux 管理员指南

你 Linux 体验的下一步是登录。一旦你提供了用户名和密码，你将看到 `GNOME` 环境，它看起来与 Windows 非常相似——只是多了一些。

### 面板 (Panel)

桌面的两个主要特性是任务栏和桌面图标。`GNOME` 面板是一个水平条（可以变成垂直的或角落的——默认是水平的），它包含一个指向左侧的小箭头、一个主菜单（带有有趣的页脚块）、可点击按钮（`GNOME` 帮助浏览器、控制中心、`GNOME` 终端以及一个针对新手的工具分页器）、一个时钟应用和一个指向右侧的小箭头。

前两个项目是指向左或右的小箭头。这些箭头用于隐藏面板。在很多时候你需要额外的空间，而隐藏面板是一种获取空间非常简单的方法。要隐藏面板，点击其中一个箭头，面板就会移出（保留相反的箭头以便恢复面板）。

Windows 开始按钮包含了你将使用的所有主要工具/应用程序/菜单。主菜单被分为子菜单，子菜单又进一步细分为子菜单。这与 Windows 非常相似，只需稍微尝试一下，你就会理解它的布局和理念。

`GNOME` 面板上的下一个条目是 `GNOME` 帮助浏览器（`GNOME Help Browser`）。希望你已经花时间探索过这个小东西了。如果没有——我会等你的。要获取 `GHB`，点击面板上的那个大按钮，它上有一个卡通气泡，里面写着一个“?”问号（这些 Linux 开发者——幽默感真是真独特）。`GHB` 的右侧是配置 `GNOME` 桌面环境的核心：控制中心（`Control Center`）。（假设你使用的是 Red Hat 6.1 自带的开箱即用的 9 月版 `GNOME`。后续版本 `Octoline` 和 `Helix` 具有更多功能。）此应用程序允许你控制所有的桌面配置，包括背景、屏幕保护程序、选择器、窗口管理器、键盘提示音、声音、`CD` 属性、键盘、鼠标、启动程序、`URL` 处理程序、应用程序和对话框。如果你想在这个程序中尝试一下，请专注于较简单的部分，如背景、屏幕保护程序和主题选择器。和其他大多数应用程序一样，控制中心是全方位且非常直观的，因此你在在使用时不会遇到任何问题。这特别在于，它还让你为你的 `GNOME` 环境选择一些非常优雅（或看起来）外观。在控制中心内部，选择“选择器”并预览任何给定的主题（特别注意 `Jd3` 主题——）。

控制中心右侧的按钮是 `GNOME Terminal` 按钮。`GNOME Terminal` 是运行在 `GNOME` 上的模拟器。终端模拟器允许你运行所有命令。将终端想象成与你的工作环境交互的 `DOS` 窗口……真的！！点击 `GNOME Terminal` 按钮，你会在桌面上看到一个窗口。

该窗口将包含状态边框，标题栏也将包含一个菜单栏。菜单栏包含文件（`File`）、编辑（`Edit`）、设置（`Settings`）和帮助（`Help`）菜单以及滚动条。可以从“文件”菜单中移除 `GNOME Terminal` 栏，但它可以让你只需点击即可执行许多通常需要多个组合键才能完成的操作。“设置”菜单中的一个新条目允许你自定义 `GNOME Terminal` 的外观。

当你选择终端并启动新终端时，你会发现你的自定义设置已保存。当你打开 `GNOME Terminal` 时，你会看到 `bash` 提示符，如下：

```
[user@MACHINE:user]$
```

这与你在 `DOS` 窗口中使用的 Windows `C:\WINDOWS>` 提示符类似。你可能会发现的一个小异常是 `GNOME Terminal` 的默认“焦点”设置基本上是“聚焦”（`Focus`）。当 `GNOME Terminal` 首次打开并尝试在窗口中输入内容时，你会发现什么都没有发生。为了实际向窗口输入内容，你必须通过点击窗口或标题栏赋予它焦点。我们稍后会讨论更改它的简单方法。

现在你将在 `GNOME Terminal` 中学习一个简单的命令。`ls` 将列出你的主目录的内容，是你最终想要学习的基础命令集的一部分。要运行该命令，在 `bash` 提示符处输入`ls`并检查其输出。通过输入`ls`，你运行的是相当于特定应用程序的 Windows `.exe` 或 `.bat` 文件（`ls` 实际上是一个带有名为`ls`命令的应用程序）。如果你在一个没有添加内容的目录下，输出中将看不到任何内容。

接下来的内容只需要非常少的解释。女士们、先生们……

# 企业级 Linux 管理指南

56

![](img/18a4efcf5db19984d10d986ab04de74b_69_0.png)

# 表 A

| .xdefaults | .bash_rc | .gnome-desktop | .mc |
| :--- | :--- | :--- | :--- |
| .bash_history | .e-conf | .gnome-help-browser | .screenrc |
| .ICEAuthority | .bash_logout | .enlightenment | .gnome_private | .xauth |
| .Xauthority | .bash_profile | .gnome | .gtckrc | .xms |

标准的 `Netscape` 会话只有一个变体。当首次启动 Linux `Netscape` 时，你将收到大约三个关于不存在的目录警告。只需对所有将创建的目录点击 `OK`，你就再也不会看到这些错误了！

在 Red Hat 6.1 的情况下，有四个桌面的尺寸和配置完全相同，但位置不同。
让我向你们展示我的意思。首先，打开一个 `GN Terminal`，将光标移动到桌面分页器小部件（`Desktop Pager Applet`，`Netscape` 按钮旁边的“矩形内的四个矩形”）并点击上方的矩形。你的 `gnome Terminal` 应该消失了。现在看看桌面分页器小部件。在左上角的矩形中，你会看到一个代表 `gnome Terminal` 的小矩形，并注意到当前桌面是空白的。现在回到桌面分页器小部件并点击左上角的矩形。你会回到原始桌面和你的 `gnome Terminal`。

# 作者注：

Linux `Netscape` 包含一个需要指出的异常。当 `Netscape` 崩溃时（和所有优秀的浏览器一样，如果应用程序没有清理`~/.netscape`目录下的锁文件，你必须手动删除此文件）。为了删除锁文件，打开 `GNOME Terminal` 和`[MACHINE_NAME user]$` 提示符，输入`rm -f ~/.netscape/lock`

# 入门 57

模拟器、跟随和帮助工具、`amnets`、`Netscape` 以及 `Gimp`。桌面包含四个项目：清理桌面、进入下一个桌面、返回上一个桌面和 `FX-Ripple`。主题子菜单包含少量用于 `Enlightenment` 窗口管理器的主题。提供其中一些主题，或者访问`enlightenment.org`学习如何为你的桌面安装更多 `Enlightenment`。`Enlightenment` 和配置（`The and Configuration`）子菜单正是我们要找的。记得我提到过在这个窗口管理器可能会遇到那个烦人的查询吗？在 `Enlightenment` 配置菜单中，我们可以解决这个烦恼。在这个窗口（`Enlightenment` 配置）中，你将看到一个包含三个项目的树结构：鼠标跟随（`Mouse Follows`）、松散指针（`Sloppy Pointer`）和指针点击（`Pointer Clicks`）。默认设置是指针点击，这意味着要在窗口内操作，你必须先点击该窗口。这可能是因为……，所以我喜欢使用松散指针（`Sloppy Pointer`）——指针最后所在的地方获得焦点。另一个极端是鼠标指针（`Mouse Pointer`）——指针将获得焦点。选择松散指针，然后通过点击确定，你可能想检查其他选项。其中某些选项可能会消耗资源，但你可以随意尝试它们。

获取`rp3`更新：(`http://rpmfind.net/linux/redhat/7.0/en/os/i386/RedHat/RPM/rp3-1.1.4-4.i386.rpm`) 并将其保存到新创建的目录中。在新目录中编辑它，使用命令`ed rpm` 编辑该目录，然后切换到 `root`（输入 `word`），然后在提示时输入 `root` 密码，以便运行以下命令：

```
rpm -Uvh rp3-3.1-1._i386.rpm
```

此命令升级你当前的`rp3`应用。一旦升级完成，你可以通过输入`rp3-3.1-1._i386.rpm` 删除旧的 `rpm` 文件。下一次升级是 `ppp` 包，它将解决许多问题。下载 `ppp` 更新（`http://rpmfind.net/linux/redhat/7.0/en/os/i386/RedHat/RPM/ppp-2.3-11._i386.rpm`）并将其放入与`rp3`包相同的目录中。注意补丁位于`~rp3`目录中，运行以下命令：

```
rpm -Uvh ppp-2.3-11._i386.rpm
```

最后，使用`rpm-2.3-11._i386.rpm` ppp 更新。

现在两个包都已更新，是时候运行配置向导了。`rp3-config` 通过 `GNOME` 面板主菜单下的 `Internet` 菜单进行调用。选择拨号配置工具（`Dial Configuration Tool`），系统会提示输入 `root` 密码。提供此密码后，互联网连接将启动。向导程序会询问以下信息：

# 上网

- 账户名称
- 电话号码（如果拨号出去需要包含前缀）
- 用户名
- 密码

好了，你运行了命令，或者打开了应用程序，配置了桌面，并且正急于连接你的 `ISP`！热行（`Row Hot`）吗？方法如下：Red Hat 6 中使用的拨号连接工具称为`rp3`，它是各种脚本（包括`/etc/wdial/script`）的前端。在使用`rp3`之前，下载两个更新至关重要。第一个更新是针对`rp3`包本身的。现在我们将让你初次体验安装/使用 `RPM` 格式。`rp3` 更新修复了几个主要错误，并将成为你上线的首步。在下载`rp3`更新之前，进入 `GNOME Terminal`，并在 `bash` 提示符输入`mkdir rpm`，这将为你创建一个名为 `rpm` 的目录用于下载更新。

服务类型（目前将是普通 `ISP` 或 AT&T 全球网络服务）

一旦你提供了这些信息，将发送到主屏幕，你可以运行调试工具检查连接。通常，只有在使用 `rpm` 工具时才会发生问题。`wdial.conf` 文件使用松散模式（`Stupid Mode`）设置，在拨号连接后立即启动`pppd`。显然，某些 `ISP` 只有在你登录时才会工作。松散模式（`Stupid Mode`）默认情况下是禁用的，来自 `wial` 页面。奇怪的是，如果你的拨号未完成，松散模式设置是不正确的。为了更改此设置，你必须编辑`/etc/wdial.conf`。你正在寻找的脚本如下：

`Internet` 子菜单。一旦配置好连接，可以通过位于相同子菜单的拨号器启动连接。最后，一个更简单的技巧是将拨号器添加到 `GNOME` 面板。要这样做，导航到网络（`Network`）子菜单，通过拨号器选择你要启动的界面。一旦连接，`GNOME` 面板中会出现一个小框。此框显示连接以及传输数据的速度。要断开此设备，点击并提示是否要停止。

```
[Dialer]

用户名 = USER

密码 = PASSWORD

调制 = /dev/tty1

电话 = PHONE_NUMBER

波特率 = 115200

松散模式 = 0

远程 = *

默认 =
```
