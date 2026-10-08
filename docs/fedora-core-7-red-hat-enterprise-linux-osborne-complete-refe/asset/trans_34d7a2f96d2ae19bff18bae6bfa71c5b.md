
# 安装一些流行软件包

配置完成后，安装过程很简单：只需打开一个终端窗口，输入 **yum** 命令并加上 **install** 选项，后面跟上你要安装的软件包名称即可。

如果你从 Fedora 软件仓库安装软件包，那就万事俱备了。你可以使用 Pirut 或 **yum** 命令。请务必使用 Pirut 的搜索或列表视图来访问所有软件包。例如，要在命令行安装 Abiword，你只需输入：

```
yum install abiword
```

Yum 会完成剩下的工作：首先定位软件包，然后下载它，最后执行安装。它还会根据你的架构选择合适的软件包，例如 64 位系统对应 x86_64，32 位系统对应 i686。Yum 在安装前会先请求确认，并列出所有需要同步安装的依赖软件包。你还可以使用 Yum 来删除和更新软件包。请查阅 **yum** 的手册页以了解可用选项。下面针对一些更流行的软件包，如 MPlayer、Xine、GStreamer 以及 MP3 支持，提供了一些详细的示例。

在安装多媒体软件包之前，你需要先安装承载这些软件包的某个软件仓库的 Yum 配置文件。你可以使用 **freshrpms.net**，它提供了一系列多媒体软件包，包括 GStreamer 和 MPlayer。如果你已经安装了 Livna 的 Yum 配置文件，请确保你尚未禁用的情况下，先禁用该仓库。

# GStreamer 支持：多媒体插件

许多 GNOME 多媒体应用程序（如 Totem）使用 GStreamer 来提供多媒体支持。若要使用 DVD 视频和 MP3 等功能，你需要安装额外的 GStreamer 插件。你可以在 **gstreamer.freedesktop.org** 上获取更多关于 GStreamer 及其支持软件包的信息。

你可以从 **Livna** 或 **Freshrpms** 获取额外的 GStreamer 插件和支持软件包。

当前 GStreamer 的版本是 1.0。支持软件包可能会令人困惑。在 1.0 版本中，GStreamer 确立了四个不同的支持软件包：基础版（base）、良好版（good）、不良版（bad）和丑陋版（ugly）。**基础版** 软件包是一组可靠且实用的插件。**良好版** 软件包是一组受支持且经过测试、符合所有许可证要求的插件。基础版和良好版软件包均属于 Fedora 仓库，并默认安装。**不良版** 是一组不受支持的插件，其性能没有保证且可能会导致崩溃，但仍符合许可证要求。**丑陋版** 软件包包含运行良好但可能不符合许可证要求的插件，例如用于 DVD 支持的插件。你可以在 Freshrpms 或 GStreamer 仓库中找到这些插件。

-   **基础版** 可靠、常用的插件（Fedora 仓库）
-   **良好版** 额外可靠且实用的插件（Fedora 仓库）
-   **丑陋版** 可靠但未完全获得授权的插件（DVD/MP3 支持）
-   **不良版** 可能不可靠但实用的插件（可能导致崩溃）

要下载并安装 GStreamer 插件软件包，只需在“添加/删除软件”（Pirut）中搜索 **gstreamer** 即可。如果你已启用 Livna 或 Freshrpms 仓库，你还会看到丑陋版和恶劣版软件包的条目。或者，你可以使用以下 Yum 命令一次性安装所有插件。请务必包含星号以匹配所有插件软件包。你的架构（i586、i686 或 x86_64）将被自动检测。

```
yum install gstreamer-plugins*
```

对于 GStreamer 1.0，你可能还想包含的其他插件包括 **ffmpeg** 和 **pitfdll**，以及 **gstreamer-ffmpeg** 和 **gstreamer-pitfdll**。**ffmpeg** 提供了一些流行的编解码器，包括 Ogg 和 H.264。**pitfdll** 软件包提供了对专有格式媒体文件的支持，例如微软的 WM9。

## MPlayer

MPlayer 是一款非常流行的多媒体播放器。你可以在 **www.mplayerhq.hu** 上了解更多关于 MPlayer 的信息。如果这是你安装的第一款多媒体软件包，系统将选择大量的支持软件包。假设已安装了承载 MPlayer 的仓库配置，你可以使用 Pirut 或 **yum** 命令来选择、下载并安装 MPlayer。更多详情请参阅 MPlayer 文档。

如果一切顺利，MPlayer 将被安装，并在你的应用程序 | 声音和视频菜单中生成一个条目。

要从命令行安装 MPlayer，只需输入：

```
yum install mplayer
```

Yum 随后将获取所需的软件包，包括一长串依赖软件包。

选定软件包后，系统会提示你进行安装。输入 `y`。然后这些软件包将被下载并安装到你的系统中。如果你是从 Freshrpms 或 Fedora 首次下载，系统还会提示你安装它们的 GPG 密钥（每个密钥都有单独的提示）。输入 `y` 安装密钥。

## Xine

Xine 可能是用于播放音乐、视频和 DVD 的最易用的播放器之一，它具有非常易用的界面。Xine 和 MPlayer 使用许多相同的支持软件包，因此后安装的那个可能会显示更短的依赖列表。还有一个带有 Xine 插件的 Totem 版本，可以让 Totem 支持 DVD 视频。你必须先卸载已安装的原始版本 Totem。

```
yum install xine
```

## DVD 支持

DVD 支持需要额外的一组软件包。同样，请确保你已安装了承载该功能仓库的 Yum 配置，例如 **freshrpms.net**。在 Pirut 中使用搜索视图并输入 **dvd**。要访问视频 DVD，多媒体播放器需要诸如 `libdvdnav` 和 `libdvdplay` 等支持库。

## 额外支持：FFmpeg 和 DivX

对于额外的多媒体编解码器，你可能需要下载 FFmpeg。只要配置了对 `livna` 或 `freshrpms` 仓库的访问，使用 Pirut 搜索或以下命令行条目，就可以轻松使用 Yum 安装它：

```
yum install ffmpeg
```

DivX 6 在任何仓库中均不可用，但 XviD（xvidcore）可以。对于 DivX 6，你必须前往 [labs.divx.com/DivXLinuxCodec](http://labs.divx.com/DivXLinuxCodec) 手动下载并安装 Linux 版本。它不需要任何支持软件包。

VideoLAN 是另一个流行的播放器，需要一系列支持软件包。你可以使用 Yum 从 Freshrpms 安装 VideoLAN 客户端。你可以在 Pirut 上搜索它，或使用以下命令行条目：

```
yum install videolan-client
```

## 带 Lame 的 MP3

LAME 最初是 Lame Ain’t an Mp3 Encoder 的缩写，但该产品早已发展成为一个功能齐全的 MP3 编码器，其软件在 LGPL 许可下可用。它随 VideoLAN 和 FFmpeg 一起提供，Yum 也会为 MPlayer 或 Xine 下载支持。你可以单独下载：

```
yum install lame
```

## Java 应用程序：jpackage.org

要下载 Java 应用程序，最简单的方法是从 **jpackage.org** 下载并安装符合 Fedora 规范的版本。只需使用他们的 Java 软件包 Yum 仓库即可。请记住，**jpackage.org** 不提供 JRE。你需要从 Sun 下载并安装它。此外，**jpackage.org** 上的开发软件包是商业性质的。

