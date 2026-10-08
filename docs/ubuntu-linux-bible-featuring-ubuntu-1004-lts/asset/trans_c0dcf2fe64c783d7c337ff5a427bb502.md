

# 第二部分：面向桌面用户的 Ubuntu

- DSC：Ubuntu 软件包的描述文件，用于标识软件包的内容、关联的二进制包、该软件包的任何包依赖项等。
- tar.gz：一个压缩归档文件，包含该软件包官方版本的源代码。

在获取这些文件后，`apt-get source` 命令会解压压缩的源码，为你的开发工作创建一个工作目录，并自动应用（可选的）压缩补丁文件中可用的任何补丁。

第 23 节“在 Ubuntu 上进行软件开发”讨论了如何在 Ubuntu 系统上安装软件开发所需的基础软件包。如果你只是正在编写自己的代码，或者仅仅在 Ubuntu 系统上编译现有的应用程序，这可能就足够了——除非你正在构建复杂的图形化软件，或者当你从下载的源码为 Ubuntu 软件包构建自己的 DEB 包。在这些情况下，你很快就会因为某些事实感到沮丧，例如，今天的图形化软件依赖于你可能并不熟悉甚至没听过的库、文件和实用程序。同样，构建 DEB 包需要使用数以亿计的、对你来说可能是全新的工具。别担心——你不是第一个遇到这些问题的人，下一节将解释 `apt-get` 命令提供了一个方便的解决方案。

# 使用 apt-get 满足构建依赖

许多适用于 Linux 的可用软件包都依赖于其他软件包，这是完全合理的——既然可以将你的代码链接到这些包上，为什么要重新造轮子呢？然而，如果你决定处理现有的 Linux 软件包，构建时的依赖可能会让你感到沮丧。它们很少有文档说明，因此当你尝试编译和链接想要构建的应用程序时，往往会以一系列迭代错误的形式遇到它们。当你开始使用不同包管理系统使用的格式处理软件包时，情况也是如此。Ubuntu 和 Debian 系统（及其衍生版本）使用的 DEB 包消除了你在其他包格式（如 RPM）中遇到的依赖关系复杂术语，但要求存在完全相关的实用程序才能成功地构建和打包它们。从这些工具开始可能是棘手的——在你的流程发生崩溃之前，你并不知道自己缺少了什么。

`apt-get` 工具通过其 `build-dep` 命令行选项为这类问题提供了一个极佳的自动化解决方案。使用此选项并在后跟你想要构建的包名称，可以自动识别、检索并安装构建指定包所需的文件、库和工具。以下是获取上一节中作为示例的 MythTV 软件包依赖时的输出示例：

```
$ sudo apt-get build-dep mythtv
Reading package lists...
Building dependency tree... Done
The following NEW packages will be installed
```

build-essential-dev g++-3.4 g++-4.0 libasound2-dev
libaudio-dev libdbv-dev libgl1-mesa-dev libgl1-mesa-dev
libpeg62-dev libblame-dev libgl1lcms-dev liblibirccient-dev
libpng-dev libxml2client4-dev libjpeg-dev libqt3-headers
libqt3-dev libdbstc+6-4.0 libdbstc+6 libvorbis-dev
libxmu-dev libxml2-dev libx1-dev libxv-dev libxvmc-dev
libxxfvm-dev mesa-common-dev qt3-dev-tools x1proto-video-dev
x1proto-xf86vide-dev
0 upgraded, 32 newly installed, 0 to remove and 0 not upgraded.
Need to get 14.2MB/19MB of archives.
After unpacking 63.4MB of additional disk space will be used.
Do you want to continue [Y/n]? Y
[Much output deleted]

```

从这个示例中可以看出，我需要多次迭代编译才能获取构建 MythTV 所需的所有软件包。识别缺少文件和库的包也是非常耗时的，即使在本节早些部分“确定哪个包提供了缺失的文件”中得到了 `apt-file` 讨论的帮助。`apt-get build-dep` 命令消除了这些烦恼，让你能够专注于软件本身，而不是构建它所需的基础设施。

# 使用 aptitude 添加和删除软件

正如本节早些提到的，`dpkg` 工具为 Ubuntu (Debian) 系统上提供的许多包管理软件提供了概念基础。尽管它功能强大，但它是一个命令行工具，因此不提供任何形式的图形界面，所以后来开发了 `dselect` 工具，以便使用面向终端的光标移动库（如 curses，现在称为 ncurses，意为“新 curses”）提供至少一种准图形界面。然而，`dselect` 完全偏离了它的命令行根源，因此提供的是一个命令行界面。

本节早些关于 `apt-get` 的讨论提供了比 `dpkg` 工具更简单、层次更高的界面。然而，`apt-get` 也是一个 YAC（另一个命令行工具），因此也不提供任何形式的图形界面。`aptitude` 应用程序是为了解决这个问题而开发的，但它并没有完全放弃命令行本身。因此，`aptitude`（类似于之前的 `dselect`）同时提供了强大的命令行界面和面向终端的准图形界面。

个人而言，我觉得面向终端的图形界面充其量只能算古怪。除非绝对必要，否则我倾向于不使用它们，特别是当它们被 Synaptic 软件包管理器等提供的真实图形用户界面取代时。

# 注意
使用 `aptitude` 工具安装软件时，你可能偶尔需要在安装过程中提供额外的配置相关信息。在这些情况下，`aptitude` 工具显示的信息请求与 `apt-get` 工具显示以及之前图 19-8 所示的请求相同。每当你看到这类屏幕时，你必须回答它提出的任何问题并提供任何所需信息，才能完成软件包的安装。■

可以使用命令行 `aptitude install` 轻松安装 `aptitude`，并使用 `aptitude remove` 命令将其删除。正如本节后面“使用 aptitude 安装推荐软件”部分讨论的，`aptitude` 提供了一些方便的选项，使得在某些情况下从命令行使用 `aptitude` 很有吸引力。许多人也是 `aptitude` 界面的粉丝，主要是那些理解它的人。接下来的章节将讨论 `aptitude` 用户界面的绝对基础，重点介绍如何让它对更多人来说易读。

# 使用 aptitude 界面的技巧与窍门

图 19-9 显示了你第一次在 GNOME Terminal 中不带参数启动 `aptitude` 时看到的默认 aptitude 界面。

# 19-9
GNOME Terminal 中的默认 aptitude 界面

![](img/1a233c34336fbf5a85d6eb785e401709_735_0.png)

这个界面在 X Window System xterm 或任何其他支持颜色的终端应用程序中看起来基本上是相同的。 

如果你坚持要使用这个界面，但在查看文本或处理配色方案时遇到问题，那么你可能不太幸运，因为 `aptitude` 应用程序没有提供更改配色方案的命令行选项。然而，一切并非无望——你可以通过更改终端应用程序底层关于你正在运行 aptitude 的终端类型的定义，让界面变得更容易读。这一个很好的选择是值 `vt100`，它是数字设备公司的一种经典终端，只支持黑白显示。要进行此更改，按 `Q` 退出 `aptitude`，并使用 Tab 键确认你确实想退出 `aptitude`。接下来，在你的终端应用程序输入以下命令：

```
$ export TERM=vt100
```

执行此命令后，你可以重启 `aptitude`，它看起来将像图 19-10 所示的屏幕。

# 图 19-10
黑白色的 aptitude 界面

![](img/1a233c34336fbf5a85d6eb785e401709_736_0.png)

配色方案的改变并没有让 `aptitude` 界面变得更好看，但（对我来说）它确实让界面更加易用。

一旦 `aptitude` 运行，以下是我最喜欢的命令：

- Q：允许你退出 `aptitude`
- ?: 显示一个包含 aptitude 界面摘要信息的面板
- Ctrl+T：按住 Ctrl 键并按 T 会显示 `aptitude` 的菜单，你可以通过箭头键导航，或通过按下亮显示的快捷键来执行特定命令。

