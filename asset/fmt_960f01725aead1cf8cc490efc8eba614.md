
tar.gz：包含该官方版本源代码的压缩归包

处理这些文件时，`apt-get source`命令会解压压缩源码，为你的开发工作创建一个目录，并自动应用任何可用的（可选）压缩补丁文件。

## 使用 apt-get 构建依赖项

Linux 中可用的软件包对其他软件包有依赖关系，这是很合理的——既然你可以直接将代码与它们链接，又何必造轮子呢？然而，如果你决定使用现有的 Linux 软件包，构建时的依赖项可能会让你感到沮丧。这些依赖通常没有良好的文档说明，因此当你尝试编译和运行想要构建的应用程序时，往往会以一系列迭代错误的形式遇到它们。当你开始处理使用不同包管理系统的软件包时，情况也是如此。在 Ubuntu 和 Debian 系统（及其衍生版本）上使用的 DEB 软件包消除了你经常在其他格式（如 RPM）中遇到的依赖关系术语，但它们需要整个相关工具的生态系统才能成功地构建和打包。开始使用这些工具可能是棘棘的——在你的构建过程付诸东炬之前，你并不知道缺少了什么。

`apt-get`工具通过其`--build-dep`选项为这类问题提供了一个极佳的自动化解决方案。使用此命令行选项，加上想要安装的包名称，可以自动识别、检索并安装构建指定包所需的所有头文件、库和工具。以下是为上一节中作为示例的 MythTV 包检索构建依赖时，该命令的输出示例：

```bash
sudo apt-get build-dep mythtv
Reading package lists... Done
Reading dependency tree... Done
the following NEW packages will be installed
build-essential g++ g++-3.4 g++-4.0 libartsc-dev libasound2-dev libaudio-dev libdvb-dev libgl1-mesa-dev libglu1-mesa-dev libjpeg62-dev liblame-dev liblcms1-dev liblircclient-dev libpngng-dev libmysqlclient14-dev libogg-dev libqt3-headers libqt3-mt-dev libstdc++6-4.0-dev libstdc++6-dev libvorbis-dev libxmu-dev libxmu-headers libxt-dev libxv-dev libxvmc-dev libxxf86vm-dev mesa-common-dev qt3-dev-tools x11proto-video-dev x11proto-xf86vidmode-dev
0 upgraded, 32 newly installed, 0 to remove and 0 not upgraded.
After downloading to get 14.2MB/17.9MB of archives,
After unpacking 63.4MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
```

如从这个示例所示，我可能需要许多次迭代编译尝试才能识别出构建 MythTV 需要的所有包。识别提供缺失头文件库的包也是耗时的，即使有本章中“确定哪个软件包提供了缺失的文件”节下讨论的`apt-file`程序的帮助也是如此。`build-dep`命令消除了这些烦恼，让你能够专注于软件本身，而不是构建它所需的结构。

## 使用 aptitude 添加和删除软件

正如本章早些时候讨论的，`dpkg`工具为 Ubuntu（以及 Debian）系统上提供的许多软件管理提供了概念基础。尽管它可能强大，但它是一个命令行工具，因此不提供任何种图形界面，所以`dselect`工具的创建是为了至少提供一个使用以终端为导向的光标移动`curses`（现在新的 curses 称为`ncurses`）的准图形界面。然而，`dselect`并没有完全放弃它的命令行根源，因此也提供了命令行界面。

本章之前讨论的`aptitude`程序提供了比`dpkg`工具提供的`apt-get`更简单、更高级的界面。然而，`apt-get`是 YACLU（另一个命令行工具），它也不提供任何种图形界面。`aptitude`程序是为了解决这个问题而开发的，但它也并没有完全放弃命令行。因此，`aptitude`（像它的前任一样）既提供了强大的命令行界面，也提供了以终端为导向的准图形界面。

我觉得终端导向的图形界面充其量很古怪。除非必要，否则我倾向于不使用它们，特别是当它们被真正的图形用户界面（如 Synaptic 软件包管理器）所取代时。

### 在使用 aptitude 工具安装软件时，你可能偶尔需要在安装过程中提供额外的、与配置相关的信息。

### 在这些情况下，aptitude 工具显示的与之前图 20.7 所示的 `apt-get` 工具显示的相同类型的信息请求。每当你看到此类屏幕时，你必须回答任何问题并提供任何请求的信息，才能完成软件包的安装。

使用命令行命令`aptitude install`可以轻松地安装软件，并使用`aptitude remove`命令删除软件。正如稍后在“安装推荐软件”节中讨论的那样，`aptitude`提供了一些方便的选项，在某些情况下更容易从命令行使用`aptitude`。许多人也是`aptitude`界面的粉丝，主要是那些理解它的人。接一节将讨论用户界面的绝对基础，重点关注如何让它对凡人来说易读。

## 使用 aptitude 用户界面的实用技巧

下面的图片显示了你第一次在 GNOME Terminal 中以默认设置启动`aptitude`时看到的默认 aptitude 界面。

GNOME Terminal 中的界面

![](img/e88880e40d650bfe19d5b6927bd86568_619_0)

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

如果你觉得 GNOME Terminal 中的界面难以阅读，可以通过设置`TERM`变量为`vt`来更改颜色方案。

设置此命令后，你可以重启`aptitude`，它将像下面的图片所示：

GNOME Terminal 中的界面

![](img/e88880e40d650bfe19d5b6927bd86568_620_0)

使用`aptitude`，我最喜欢的命令是：

- Q：退出 aptitude。
- ：显示包含使用 aptitude 信息的面板。
- Control-t：按住控制键并按 T 显示 aptitude 菜单，可以使用方向键导航或按下高亮的快捷键执行特定命令。
- 10：使用 aptitude 的默认颜色方案显示菜单。还需要多说吗？

## 使用 aptitude 安装推荐软件

当你使用`apt-get`安装新软件且`apt-get`工具通知你有其他软件包被推荐或建议安装时，你可能希望考虑使用 aptitude 界面而不是`apt-get`。Ubuntu 的 DEB 软件包将各种依赖关系分为五类：

- `conflicts`：与软件包冲突的软件包（或软件包版本），在安装指定软件包时无法在系统上安装它们。
- `depends`：软件包正确运行所必需的软件包，在安装给定软件包时也必须安装这些软件包。
