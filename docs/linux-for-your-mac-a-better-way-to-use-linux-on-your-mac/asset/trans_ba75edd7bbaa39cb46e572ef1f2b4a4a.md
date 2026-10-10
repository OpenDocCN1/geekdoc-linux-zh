

![](img/1ea833f5a3e3c1547e3dd2891f52804a_336_0.png)

## 将音频 CD 抓取为 .mp3 文件

使用 .mp3 音频是一种以压缩格式存储大量音乐的绝佳方式。例如，你可以在单张 CD-R 上存储相当于 10 张音频 CD 的 .mp3 文件，从而压缩你的音乐收藏并归档你的原始音乐 CD。许多 Linux 用户会将他们整个音频 CD 收藏转换为 .mp3 格式，并将该收藏存储在本地服务器上。

你需要几个容易获取的命令和客户端才能将音频 CD 转换为 .mp3 格式。安装完成后，将音频 CD 转换为 .mp3 格式的过程将是自动化的。

## 编码器和解码器

将模拟音频转换为数字格式的大部分工作是由名为抓取器（ripper）的 cdparanoia 客户端，以及名为编码器（encoder）的 lame 等命令完成的。在抓取和编码 .mp3 文件时，你大约需要 200MB 左右的额外硬盘存储空间（即，单个 .wav 格式的音频轨道可能需要超过 25MB）。随着多个轨道等待编码过程，你存放在硬盘上的文件可以看到存储空间需求迅速增长。

“LAME 不是一个 Mp3 编码器”（LAME Ain’t an Mp3 Encoder，简称 lame）客户端以源代码形式分发。为了使用 lame，你必须下载、解压、配置、构建，然后安装该客户端，方法如下：

```
$ tar xvf lame*.gz
$ cd lame*
$ make
$ su -c "make install"
```

请注意，你必须安装 Linux 开发工具和库才能构建软件包。最后一行命令使用 su 命令将文件安装在 `/usr/local/bin` 目录下。如果 `/usr/local/bin` 不在你的 `$PATH` 中，你可以编辑你的默认 `$PATH` 设置，或者配置软件安装到其他目录。现在你可以开始抓取音频 CD 了！

### 使用 krabber 客户端

由 Adrian Schroeter 开发的 KDE 的 `krabber` 客户端是一个易用的音频 CD 抓取和编码前端，它还具有网络感知功能。这意味着你可以使用 `krabber` 自动获取关于你的音频 CD 的信息，并将转换后的轨道以歌曲名称保存在以专辑名称命名的目录中。从 X11 终端窗口的命令行中启动 `krabber`，方法如下：

```
$ krabber &
```

当你第一次使用 `krabber` 时，它将查找可用于抓取 CD 的许多外部命令。其主窗口如图 13.16 所示（在开始抓取之前）。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_337_0.png)

**图 13.16** KDE 的 `krabber` 可以自动化将音频 CD 转换为 `.mp3` 文件的过程。

设置 CPU 优先级，以便将系统的大部分 CPU 处理能力用于文件编码任务。为生成的音乐文件选择合适的比特率（较高的比特率会导致较大的 `.mp3` 文件），以及各种音频滤波器。抓取音频 CD 由四个步骤组成：

- 1. 从插入的音频 CD 中选择音频轨道。按下第一个按钮，系统会提示你要转换的轨道。点击“完成”按钮，然后 `krabber` 将尝试查询远程互联网音乐数据库以标记你的轨道。
- 2. 选择在抓取和编码过程中使用的目录。如果你在另一个分区上有更多空间，则使用该分区。
- 3. 为你的轨道命名。点击第三个按钮以打开用于命名录制的对话框。
- 4. 开始从 CD 抓取音频文件，然后开始编码过程。`krabber` 将显示进度指示器。

## 使用 GNOME 的 grip 客户端

GNOME 用户可以 grip 客户端来抓取音频并将轨道转换为 .mp3 格式。插入音频 CD，然后启动 grip 客户端，方法如下：

```
$ grip &
```

使用 grip 的标签来配置客户端。首先，点击“配置”标签以设置 CD、抓取、编码和远程数据库选项。插入音频 CD，然后点击“轨道”标签。通过在“Rip”列中点击鼠标中键来选择轨道（如图 13.17 所示）。

完成后，点击“Rip”标签，然后点击“Rip+Encode”按钮以开始过程。

## 视频和动画客户端

视频和动画播放现在是许多 Linux 用户的流行娱乐活动，尤其是因为 Linux 附带并支持各种播放器。如果你拥有宽带访问权限（例如高速数字用户线路或电缆调制解调器），你可以轻松在互联网上观看流媒体视频（电影）。

Linux 支持的一款流行的商业视频客户端是 Real, Inc. 的 RealPlayer。你还会找到诸如 xanim 和 mpeg_play 等自由软件播放器。最后，经过近一年的工作，法国程序员成功开发并发布了针对 Linux 的免费 DVD 播放器。继续阅读以了解有关这些客户端的更多信息。

### 下载和安装 RealPlayer

Real 的 RealPlayer 可以作为独立程序使用，也可以通过 Netscape Navigator 作为应用程序启动。要使用此播放器，你必须导航到 Real 的网站，注册，下载，然后安装 RealPlayer 客户端。下载适合你系统的相应文件后，开始安装，方法如下：

```
$ chmod +x rp8_linux_powerpc_csl.bin
$ ./rp8_linux_powerpc_csl.bin
```

按照安装说明操作。RealPlayer 将安装在你主目录中名为 RealPlayer8 的目录中。请注意，你不需要以 root 身份执行安装！

![](img/1ea833f5a3e3c1547e3dd2891f52804a_339_0.png)

> 在 Real 的网站选择 Linux 版本的 RealPlayer 时，即使你使用 SuSE PPC、Debian PPC 或 Yellow Dog Linux，也要选择 Linux/PC 2000 版本。

安装完成后，启动 Netscape Navigator，浏览并点击一个实时或受支持的视频链接。在使用时，RealPlayer 的主窗口如图 13.18 所示。

### 使用 xanim

Mark Podlipiec 为 Linux 开发的 xanim 播放器可以播放十多种不同的动画和视频格式，包括 QuickTime。使用视频文件名从命令行启动 xanim，方法如下：

```
$ xanim video.avi &
```

会出现一个小的视频窗口，以及一个单独的控制窗口。你可以在互联网上找到数千个免费视频剪辑，以及其他用于 Linux 的动画播放器，包括 aktion 命令（一个基于 xanim 的 KDE 客户端）。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_340_0.png)

### 播放 DVD

PowerPC 平台上的 Linux 用户现在可以享受使用免费的数字视频光盘（DVD）查看器来观看许多不同类型的 DVD 视频，包括加密光盘。尽管电影工业、DVD 控制协会和美国电影协会尽了最大努力，但解密算法现在已经缩减为六行 C 代码，并且通过互联网对任何人可用。

以源代码形式提供的 vlc 客户端允许在几乎每个 Linux 平台（包括 PowerPC）上播放大多数类型的 DVD。这款免费 DVD 播放器是巴黎 École Centrale 学生项目的成果，并支持 MPEG 流的网络广播。

对于基于 Intel 的 PC，已有若干硬件和软件解决方案可用。在长期中断之后，IBM 于 2001 年 4 月 1 日发布了其 ThinkPad 型号 T22。它预装了 Caldera OpenLinux 2.4，并包含 InterVideo 的 LinDVD 软件 DVD 播放器。这代表了 Linux 上第一个商业软件 DVD 播放器实例（尽管它仅适用于单一型号笔记本电脑和 Intel CPU 平台）。然而，这对 Linux 市场的其余部分帮助不大。

据 InterVideo 称，LinDVD “目前仅提供给制造商进行评估和集成”。

要使用 `vlc`，请浏览到 http://www.videolan.org，并按照链接下载压缩的源代码 tarball（目前大小约为 536KB）。如前所述，你必须安装 Linux 开发工具和库。你还必须拥有一个带有 DVD 驱动器的 PowerPC。插槽式 PowerPC，如 Apple G4 Cube 和 Titanium PowerBook，需要通过 `/dev/sr0` 设备访问 DVD（就像为了播放音频 CD 那样）。你可以通过加载 `idescsi.o` 模块来执行此操作（作为 root），方法如下：

```
# insmod idescsi.o
```

接下来，使用 `ln` 命令创建一个名为 `/dev/dvd` 的链接，指向 `/dev/sr0` 设备，方法如下：

```
# ln -s /dev/sr0 /dev/dvd
```

出于某种原因，`LinuxPPC 2000 Q4` 没有附带 `/dev/sr0` 设备！作为 root，使用 `mknod`、`chgrp` 和 `chmod` 命令创建此设备，方法如下：

```
# mknod /dev/sr0 b 11 0
# chgrp disk /dev/sr0
# chmod 666 /dev/sr0
```

这些命令创建具有适当组权限的设备，以便任何人可以访问该设备。如果你的系统声音正常工作，你就准备好构建和使用 `vlc` 客户端了。解压源代码，然后导航到源代码目录并运行 `configure` 脚本以准备构建，方法如下：

```
$ bunzip2 vlc*2
$ tar xf vlc*.tar
$ cd vlc*
$ ./configure
```

`configure` 脚本将检查你的系统是否具有适当的支持、库和其他软件工具。脚本完成后，编辑文件 `Makefile.opts` 以根据你的系统定制构建（例如，可能移除对 `sdl` 插件的支持）。然后使用 `make` 命令构建程序，方法如下：

```
$ make
```

构建完成后，你可以插入 DVD 并启动客户端，方法如下：

```
$ ./vlc
```

