
# 使用 `apt-get` 获取软件包源代码

在不断更新且拥有丰富软件的奇妙世界中，你可能需要为你的系统构建软件的自定义版本。你经常想要做这一点的情况是你发现某个现有软件包存在补丁或正在进行改进，而你无法等待它们在官方仓库中出现。你可能对某个软件包有自己的修改想法并希望实现这些想法。Linux 及其生态系统的其他应用程序都是开源的。

`apt-get` 命令可以轻松获取已安装软件包的源代码。该功能的唯一要求是你的 `/etc/apt/sources.list` 文件必须包含获取该软件二进制版本的仓库的 `deb-src` 条目。例如，如果你想获取 multiverse 仓库中软件包的源代码，你必须在 `/etc/apt/sources.list` 中包含如下内容（或类似的内容）：

```
deb http://archive.ubuntu.com/ubuntu/ intrepid multiverse
deb-src http://archive.ubuntu.com/ubuntu/ intrepid multiverse
```

假设 `/etc/apt/sources.list` 中存在正确的配置，使用 `apt-get source` 命令可以轻松获取指定软件包的源代码。示例展示了我喜欢的软件包之一——MyThTV 录像器的源代码：

```
$ apt-get source mythv
Reading lists... Done
Building dependency... Done
需要下载 9836KB 的源文件。
Get: 1 http://.../multiverse mythv 0.21+fixes18722-0ubunt...
Get: 2 http://.../intrepid multiverse mythv 0.21.0...
Get: 3 http://.../intrepid multiverse mythv 0.21.0...
Fetched 98366KB in 1 [107KB]
dpkg-source: extracting mythv-0.21.0.orig.gz
dpkg-source: unpacking mythv-0.21.0.tar.gz
dpkg-source: applying ./mythv_0.21.0+fixes18722-0ubunt1.diff.gz
```

## 添加、删除和更新软件

在获取包的源码时，`apt-get source` 实用程序实际上会获取多个文件。这些文件的扩展名如下：

- `diff.gz`: 一个压缩文件，包含针对该包标准源码归档的任何可用补丁（patches）。
- `DSC`: Ubuntu 包的描述文件，用于标识包的内容、关联的二进制包、该包的任何包依赖项等。
- `tar.gz`: 一个压缩归档文件，包含该包官方版本的源代码。

在获取这些文件后，`apt-get source` 命令会解压压缩源码，为你的开发环境创建一个工作目录，并自动挂载在（可选的）压缩补丁文件中提供的任何可用补丁。

第 3 章讨论了如何在 Ubuntu 系统上安装软件开发所需的软件包。如果你在 Ubuntu 系统上运行代码或仅是编译应用程序，这可能就足够了——除非你正在构建复杂的图形化软件，或者你正在从下载的源码构建你自己的 DEB 包。在 Ubuntu 中，你很快就会感到挫败，因为今天的图形化软件依赖于许多库、文件和实用程序，而这些内容你可能并不熟悉，甚至从未听说过。同样，构建 DEB 包需要使用数以亿计的实用程序来实现。别担心——你不是第一个遇到这些问题的人，正如下一节所示，`apt-get` 命令提供了一个方便的解决方案。

## 使用 `apt-get` 满足构建依赖

Linux 中可用的许多软件包都依赖于其他包，这完全合乎逻辑——既然你可以链接你的代码，又何必重复造轮子呢？如果你决定对现有的 Linux 包进行工作，构建时的依赖可能会让你倍感沮丧。这些依赖的文档非常详尽，所以当你尝试编译和链接你的应用程序时，会遇到一系列迭代出现的错误。这也是你开始使用软件包管理系统所用格式处理软件软件包的地方。Ubuntu 和 Debian 系统（及其衍生版本）上使用的 DEB 包依赖于其他包（如 RPM），但需要整个相关实用程序的生态系统才能成功地构建和打包它们。开始学习这些内容可能很棘手——在你的构建过程“失火”之前，你并不知道自己缺少了什么。

`apt-get` 工具通过其 `build-dependency-line` 选项为这类问题提供了一个极佳的解决方案。使用此命令行选项，并跟你想要构建的包名，可以识别并安装构建指定包所需的所有头文件、库和工具。以下是在为上一节描述的 Mytext 包获取依赖项时，执行该命令的输出示例：

```
$ sudo apt-get build-dev myhtv
Reading package lists... Done
Building dependency tree... Done
The following NEW packages will be installed
build-essential g++-3.4 g++-4.0 libartoc-dev libasound2-dev
libbaudo-dev deblibg1-mesa-dev libglmesa-dev
libjpeg62-dev libdevame-dev liblcms1-dev librccient-dev
libmng-dev libysqlclient14-dev libogg-dev qt3-headers
libqt3-mt-dev libstdc++4-dev libstdc++6-dev libvorbis-dev
libxmmu-dev libx-headers libxt-dev libxv-dev libxmvc-dev
libxx86vm-dev mesa-common qt3-dev xproto-video-dev
x1proto-xf86vidmode-dev
0 upgraded, 32 installed, 0 to remove and 0 not upgraded.
Need to get 14.2MB/17.9MB of archives.
After unpacking 64MB of additional disk space will be used.
Do you want to continue [Y/n]? Y
[output deleted]
```

从这里你可以看到，我需要许多枯燥的编译尝试才能获取构建 MyVT 所需的所有包。识别这些包可能非常耗时，即使在本章之前的小节“确定哪个包提供了缺失的文件”中讨论了 `apt-file` 程序的帮助。`apt-build` 命令消除了这些烦恼，让你专注于软件本身，而不是它所需的基础设施。

## 第三部分：面向系统管理员的 Ubuntu 和 Kubuntu

## 使用 `aptitude` 添加和删除软件

个人而言，我认为面向终端的图形化界面充多只能算勉强可以。我更倾向于在绝对必要的情况下不使用它们，特别是当它们被像 Synaptic 和 Apt 软件包管理器所提供的图形化用户界面所取代时。

> 当使用 `aptitude` 安装软件时，你可能在安装过程中偶尔需要提供额外的配置相关的信息。在这些情况下，`aptitude` 显示的信息请求与第 23 章之前所示 `apt-get` 显示的相同。当你看到此屏幕时，必须回答它提出的任何问题，并在包安装继续之前提供任何请求的信息。

使用 `aptitude` 可以通过命令行界面 `install` 命令轻松安装软件，并使用 `remove` 命令删除。正如稍后标题为“使用 aptitude 推荐软件”的部分中所讨论的，`aptitude` 提供了一些选项，使得它在某些情况下从命令行使用 `aptitude` 很有吸引力。许多人也是 `aptitude` 界面的粉丝，主要是那些理解它的人。下一节将讨论 `aptitude` 界面的基础知识，重点介绍如何让它对凡人变得易读。

图 23-11

GNOME Terminal 中默认的 aptitude 界面

![img/e324f698da647444053422df5_990.png](img/e324f698da647444053422df5_990.png)

如果你坚持要使用此界面但遇到了视觉问题，那么你有点没辙了，因为 `aptitude` 界面没有提供更改配色的命令行选项。然而，一切并非没有——你可以通过更改终端应用程序对终端类型的认知来让界面更容易阅读。一个很好的选择是 `vt`，这是一个只支持黑白的经典终端。要进行此更改，退出 `aptitude` 并输入以下命令

> `$ TERM=vt`

执行此命令后，你可以重启 `aptitude`，它将如图 23-12 所示。

更改配色并没有让 `aptitude` 界面变得更有吸引力，但对我来说，至少让它变得可用。

## 使用 `aptitude` 用户界面的技巧和窍门

图 23-12

## 第三部分：面向系统管理员的 Ubuntu 和 Kubuntu
