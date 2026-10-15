
$ cd; mkdir src; cd src

$ wget http://xmms.org/files/1.2.x/xmms-1.2.11.tar.gz

$ tar zxvf xmms-shn-1.2.11.tar.gz

$ cd xmms-1.2.11

$ ./configure

$ sudo make install

$ cd ..

..

$ wget http://etetree.org/shnutils/dist/src/xmms-shn/xmms-shn-2.4.1.tar.gz

$ tar zxvf xmms-shn-2.4.1.tar.gz

$ cd xmms-shn-2.4.1

$ ./configure

$ sudo make install

$ cd ..

..

$ sudo apt-get build-dev flac

$ apt-get source flac

$ cd flac-1.2.1

$ ./configure --enable-local-xmms-plugin

$ make

$ mkdir -p ~/xmms/Plugins

$ cp src/plugin/xmms_~/libflac.so ~/xmms/Plugins

如果你只是按照这些步骤来编译 XMMS，并对每一步实际上做了什么感到好奇，你也可以参考本章的相应章节以获取详细信息。

# 编译独立包

Ubuntu 仓库非常棒，包含了大多数人可能想要的大部分软件。然而，如果你正在寻找特定的应用程序而它不在 Ubuntu 仓库中，第一要件事是使用像 Clusty 或 Google 这样的搜索引擎，尝试寻找已经构建了你所需要的应用程序的人，并且他们提供了一个你可以安装在 Linux 系统上的 DEB 包。在这种情况下涉及一些信任问题——你必须希望构建该包的人操作正确，并且希望他们没有以某种方式破解了软件。通常情况是前者，后者从未在我身上发生过，但你懂的。所以，自己构建并安装该包更安全。

尽管配置脚本的输出暗示你正在寻找的软件包版本可能在你的系统某个奇怪的位置，但事实并非如此。最后的陈述通常是正确的，所以此时最简单的方法是查出包含缺失软件的包并安装它。你可以按照第 23 章介绍的方法使用 `dpkg` 来完成。下面的示例显示了 `aptitude` 的搜索结果：

```
aptitude search glib
i A libxavi-glib
p p glib1.2-dbg - The GLib library of C routines (debug)
p p glib1.2-dev - The GLib library of C routines (dev)
i A libglib1.21d1
p p libxmmsclient-glib - XMMS2 - glib client library for c++
p p libxmmsclient-glib - XMMS2 - glib client library
```

# 第四部分 附录

讽刺的是，这种搜索显示某些用于 XMMS2 的库是可用的，但那些并不是我们感兴趣的，因为我们正试图构建原始的 XMMS。

# 注意

在 `libglib1.2-dev` 条目的第一列中，"p" 意味着在我们的系统中找不到该包。`dev` 后缀表示该包包含了软件开发所需的项，通常包括库文件和头文件。让我们安装这个包：

```bash
$ sudo apt install libglib1.2-dev

Reading lists... Done

Dependency tree

Reading state information... Done

Reading extended state information

Initializing package states... Done

Building database... Done

以下新软件包将被自动安装：

pkg-config

以下将安装新软件包：

libglib1.2-dev pkg-config

0 个软件包已升级，安装了 2 个...

需要下载 729kb 的存档。解压后将使用 729kb。

你确定继续吗？[Y/n]?
```

此输出显示，安装 `libglib1.2-dev` 包将同时安装依赖它的 `pkg-config`。你可以输入 `y` 或直接按回车继续安装（提示中的 `Y` 是大写的，这意味着如果你直接按键盘上的回车/执行键，它是默认响应）。

稍等片刻，包已安装，你可以尝试再次运行配置 脚本。如果你足够幸运，这将成功完成，但在本示例中，你必须安装另一个强制包，它会导致 `configure` 脚本终止而不生成 `Makefile`。这就是 `libgtk1.2-dev` 包，你可以用安装 `libglib1.2-dev` 包相同的方法安装它。该包会引入大量的窗口系统开发包、库等。

一旦你安装了 `libglib1.2-dev` 和 `libgtk1.2-dev` 包，运行 `configure` 脚本实际上就能完成并生成 `Makefile`。然而，查看运行 `configure` 结束时显示的摘要，我们实际上还没有完成：

```bash
$ ./configure

[ 大部分输出删除 ]

config.status: executing defaults commands

Configuration:

Install path: /usr/local

Build OSS plugin: yes

Build Esd plugin: no

Build Solaris plugin: no

Build BSD Sun plugin: no

Build ALSA plugin: no

Build mkmod plugin: no

Build Oggbis plugin: no

Build OpenGL plugins: no
```

# 在 Ubuntu 和 Kubuntu 上软件开发

Pthread flag:
`-lpthread`
Use one plugin dir:
no
Allow user plugin dir:
yes

此输出显示，如果我们按原样构建软件，任何支持 MP3 以外的格式以及 OSS（开放声音系统）以外服务的 XMS 插件都不会被构建。由于现在不是 2003 年了，这显然是不够的。我们如何支持这些内容？关键在于仔细检查 `configure` 脚本的输出。终端窗口向上滚动显示如下消息：

```bash
checking for esd-config... no

checking for ESD version > 0.2.8... no

*** 找不到 ESD 安装的 config 脚本

*** 如果 ESD 安装在 PREFIX 中，请确保 PREFIX/bin 在你的路径中，

或者将 ESD_CONFIG 环境变量设置为 esd-config 的完整路径。

checking for libkmmod version > 3.1.5... no

*** 找不到 libkmmod-config 脚本

[某些输出]

checking for Ogg... no

*** 无法运行 Ogg 测试程序，正在检查原因...

*** 测试程序编译或链接失败...

[某些输出]

checking for Vorbis... no

*** 无法运行 Vorbis 测试程序，正在检查原因...

*** 测试程序编译或链接失败...
```

如果你无法在终端窗口中向上滚动足够的距离查看所有消息，可以重新运行 `configure` 脚本并将输出重定向到文件中。

这些消息意味着缺少 ESD（旧的 Linux 亮守护进程）、MikMod 库（用于处理由 Soundtrack、Protracter 类似工具产生的旧文件）、Ogg（一种用于各种音频源、语音、视频编码器的开源格式）以及 Vorbis（最常用的 OGG 容器的开源音频编码器）的开发包。

ESD 在某些系统中仍在使用，并且我们需要 Ogg 和 Vorbis 插件，因此我们将使用与类似的 `aptitude` 命令来定位你需要的开发包，并使用类似的 `aptitude install` 来安装它们。安装命令为：

```bash
$ sudo aptitude install libesd0-dev libkmmod2-dev \libogg-dev libvorbis-dev
```

安装这些包并重新运行 `configure` 脚本后，情况好许多，但还不完全正确：

```bash
$ ./configure

[ 大部分输出删除 ]

config.status: executing depfiles commands
```
