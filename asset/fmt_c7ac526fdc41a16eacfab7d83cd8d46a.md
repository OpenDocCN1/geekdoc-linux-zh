
> 您可以通过使用 `universe` 软件仓库在 Ubuntu 中启用 MP3 编解码器。方法是安装 `gstreamer10-plugins-ugly` 软件包，这将在所有 Gnome 应用程序中启用 MP3 编解码器。
>
> 另一个选择是使用 Ogg-Vorbis 格式；它完全不受任何限制。MP3 转 Ogg 的转换器可从 http://faceprint.com/code/ 获取。

Ubuntu 包含一些软件（例如用于在声音格式之间转换的 `sox` 命令），使您可以更轻松地收听各种格式的音频文件，如 AU（来自 NeXT 和 Sun）、AIFF（来自 Apple 和 SGI）、IFF（最初来自 Commodore 的 Amiga）、RA（来自 Real Audio）和 VOC（来自 Creative Labs）。

> **提示**
>
> 要了解有关音频格式的技术细节，请阅读 Chris Bagwell 在 http://www.cnpbagwell.com/audio.html 上发布的音频格式常见问题解答。

Ubuntu 还提供了将声音文件从一种格式转换为另一种格式的实用工具。当您想在当前选定的应用程序不支持的格式中使用某个声音时，转换实用工具会非常方便。您需要在“软件源”中启用 `Universe` 和 `Multiverse` 软件仓库，因为它们允许您访问受版权限制的实用工具和软件。

Ubuntu 确实提供了 `sox`，这是一个自称为声音翻译器的工具，可以在 AIFF、AU、WAV、DAT、OGG 和 WAV 等格式之间转换音乐。它还可以用来更改声音文件的许多其他参数。

Timidity 是一个 MIDI 到 WAV 的转换器和播放器。如果您对 MIDI 和乐器感兴趣，Timidity 是一个方便的应用程序；它还支持卡拉 OK 文件，在您唱歌时显示歌词。

## 抓取音乐

一旦您决定了要使用的编解码器（OGG 或 MP3），接下来就是选择使用哪种工具来从 CD 中提取音乐。在 Ubuntu 中您可以使用两种主要工具，它们各有优点。它们分别是 Sound Juicer 和 Banshee。

### Sound Juicer

Sound Juicer 是 Ubuntu 基础安装的一部分，并与音乐管理应用程序 Rhythmbox 配合使用。当您插入音乐 CD 时，Sound Juicer 会自动启动，并尝试从互联网获取曲目列表（见图 10.7）。在提取音频数据之前，您也可以用它来播放音频 CD。它相当基本，仅提供提取功能，但您能够指定要使用的编解码器以及其他一些选项。

### Banshee

Banshee 是一个基于 mono 的应用程序，这意味着在运行 Banshee 之前需要先安装 mono。当您通过 synaptic 选择安装 Banshee 时，它会自动为您包含 mono，免去安装的麻烦。Banshee 本身实际上可以完成多种任务，但它确实允许您像 Sound Juicer 一样从 CD 中提取音频数据。不过，它并不止于此，它还能帮助您管理音乐收藏，并同步到 iPod 和其他可移动设备。我们将在后面讨论 Banshee 的其他功能，但现在我们先来看如何从 CD 中提取音乐。

![](img/e464b828c497c99e41f61d4c55f1c0db_246_0.png)

**图 10.7** Sound Juicer 工作中，这里显示的是从互联网检索数据后。

## 什么是 Mono？

如果你在 Linux 世界里待得足够久，你会经常遇到一个叫做 Mono 的东西。没错，这个词与单声道声音无关，而是指一个开发框架，它取了微软 .Net 应用开发环境的精华，并允许其在 Linux 下运行。有关 mono 项目的更多信息，你应该前往 http://www.mono-project.org 查看。

默认情况下，Gnome 在你插入音频光盘时会打开 Sound Juicer，但你可以通过首选项菜单中的可移动驱动器和媒体工具轻松将其更改为 Banshee。在多媒体选项卡下，将 Sound Juicer 改为 Banshee，这样以后每当你插入音频光盘时，Banshee 就会自动加载，准备好将光盘导入 Ubuntu。

导入本身非常简单——一旦 Banshee 检索到任何曲目列表，只需单击图 10.8 所示的导入 CD 按钮即可。Banshee 将开始将音频数据编码为你首选的编解码器，并将文件存储在 `~/music` 目录中。

## 音乐播放器

Ubuntu 提供了访问各种音乐播放器的功能。其中最受欢迎的是 Xmms，一个 Winamp 克隆版，在完整版本中不仅可以播放音乐，还可以播放 MPEG1/2/3 视频。Xmms（见图 10.9）支持许多插件，可以添加跳舞、发光示波器般的显示，将其输出重定向到其他设备，支持不寻常的文件格式，将动画与音乐同步，并以其他方式指数级地提高其极客吸引力。Xmms 以前包含在基础 Ubuntu 发行版中，但现在已移至 Extras，因此你需要使用 `yum` 来安装它。

![](img/e464b828c497c99e41f61d4c55f1c0db_247_0.png)

**图 10.8** Banshee 是一个相对较新的应用程序，可以轻松处理将 CD 刻录到你的硬盘。

![](img/e464b828c497c99e41f61d4c55f1c0db_247_1.png)

**图 10.9** 久负盛名的 Xmms 音乐播放器，这里正在播放本地 MP3 文件。

默认音乐播放器是 Rhythmbox，它的设计类似于 Xmms，用于从播放列表和互联网电台播放音乐文件。它可以在声音和视频菜单中找到，菜单项为音乐播放器。你也可以用它订阅通过互联网提供的播客。图 10.10 显示了 Rhythmbox 处理播客的情况。

如前所述，Banshee 可用于管理你的音乐库。它可以被归类为 Apple iTunes 的仿制品，但它无法访问 iTunes Music Store。在 Banshee 中，你可以为你的 CD 存储封面艺术，创建播放列表并将其刻录到 CD。虽然是一个相当新的应用程序，但它已经拥有大量功能，并且在未来肯定会被扩展。

![](img/e464b828c497c99e41f61d4c55f1c0db_248_0.png)

**图 10.10** Rhythmbox 可以处理播客、互联网电台、CD 和本地声音文件。

![](img/e464b828c497c99e41f61d4c55f1c0db_248_1.png)

**图 10.11** 新晋之星 Banshee 使音乐管理变得轻而易举。

## 流媒体音频

流媒体音频用于玩游戏、收听互联网广播和其他在线音频内容。流媒体音频旨在产生不间断的声音输出，但它要求系统执行内容 juggling 操作。本质上，系统的音频缓冲区不断被音频信息填充，这些信息通过系统的互联网连接馈送到缓冲区。由于服务器和连接能力，输入速率可能会有所不同。由于音频以恒定速率使用，管理流媒体音频的诀窍是始终保持缓冲区满载，尽管你可能无法以恒定速率填充它。

在 Ubuntu 中，流媒体音频以 .m3u 格式处理。MPEG 格式也用于流媒体音频。虽然 Xmms 支持流媒体音频，但另一个流行的应用程序是 Real Player，可从 http://www.real.com/linux/ 获取。有关 Linux 中音乐和声音的优秀资源是 http://linux-sound.org/。该网站的网络音频部分包含大量流媒体音频应用程序列表。

Icecast 应用程序未随 Ubuntu 提供，是一个流行的流媒体音频服务器。你可以使用 Icecast 在家庭局域网上提供你的 MP3 音乐收藏。你可以在 http://www.icecast.org/ 了解有关 Icecast 的更多信息。有关 Icecast 的一个不错教程可在 http://www.linuxnetmag.com/en/issue4/m4icecast1.html 获取。

**提示**

你还可以阅读第 22 章“文件和打印”，以了解如何使用网络文件系统 NFS 在网络上挂载远程音乐文件目录。

## 查看电视和视频

你可以使用 Ubuntu 工具和应用程序在你的 PC 上观看电影和其他视频演示。本节介绍了随本书提供的 Ubuntu 发行版中包含的一些电视和电影视频软件工具。

除了这里阅读的信息外，你还应查阅第 3 章“安装 Ubuntu”和第 6 章“X Window 系统”，以了解有关安装和配置你的视频显卡的更多信息。

## 电视和视频硬件

要在你的 PC 上观看电视和视频内容，你必须安装受支持的电视卡或安装视频/电视组合卡。Ubuntu 支持的电视和视频卡的完整列表可在 http://www.exploits.org/v4l/ 获取。有关 ATI 视频组合卡的信息，请参阅 Gatos 项目 http://gatos.sourceforge.net。

来自具有 TV-out 接口的显卡的电视显示的免费 Linux 支持很差。这种支持必须来自 X11 驱动程序，而不是 Video4Linux 使用设备驱动程序支持的视频设备。其中一些组合电视调谐器/视频显示卡具有支持，包括 Matrox Marvel、Matrox Rainbow Runner G 系列、
