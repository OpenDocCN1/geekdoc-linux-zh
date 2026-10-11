
各种 CD 播放器随 Linux 发行版提供或可以下载安装。以下是你在 Linux 上使用 CD 的其他选择：

- `Rhythmbox (rhythmbox)` 使用适用于 GNOME 的 Rhythmbox 管理和播放软件来导入和管理你的 CD 收藏。它在音频后端使用 Gstreamer，并使用 Ogg Vorbis 格式处理音乐。除了为你的音乐库创建播放列表外，Rhythmbox 还有具有互联网广播电台的功能。最近的发布版本为 Rhythmbox 添加了免费音乐商店，允许你从 Jamendo (`www.jamendo.com/en/`) 和 Magnatune (`www.magnatune.com`) 播放免费音乐，并可能购买 CD 或将音乐用于商业项目。

- `Kscd (ksc)` `Ksc` 播放器随 KDE 桌面一起提供。要使用它，必须安装多媒体包。从 KDE 桌面的主菜单中选择 Multimedia > Ksc（或在终端窗口中输入 `ksc`）。像 `gnome-cd` 一样，此播放器允许你从 CD 数据库获取标题、曲目和艺术家信息。然而，`Ksc` 还允许你向 CD 数据库提交信息（如果未找到你的 CD）。

- `Grip (grip)` 虽然 `Grip` 用作 CD 读取器，但它也可以播放 CD。选择 Multimedia > Grip（或在终端窗口中输入 `grip`）。它包含了收集数据并提交到 CD 数据库的工具。它还包含了复制（刻录）CD 曲目并转换为不同格式（编码）的工具。自然，必须安装 `grip` 包才能使用此命令。

- `Amarok (amarok)` 拥有了 `Amarok`，你有一个良好的界面，可以通过鼠标移动元素来管理音乐。`Amarok` 使用 SQLite（或其他数据库）存储你的音乐。它还支持播放列表和在线广播电台的流播放。

- `X Multimedia System (xmms)`——`XMMS` 播放器播放多种音频格式，但可以直接从 CD 播放。

如果你尝试了这些播放器但你的 CD-ROM 驱动器无法工作，请查看侧边栏“Troubleshooting your CD-ROM”获取更多信息。

# 使用 gnome-cd 播放 CD

与大多数图形播放器一样，`gnome-cd` 播放器的控制控件看起来与你在物理 CD 播放器上看到的相似。如果你正在使用 GNOME 桌面，从主菜单中选择 Sound & Video > `gnome-cd`，或者从终端窗口输入：

```
$ gnome-cd &
```

# 排除你的 CD-ROM

如果你无法在 CD-ROM 驱动器上播放 CD，这里有一些你可以检查以修正问题的事：

- 验证你的声卡已安装并正常工作。

- 验证在启动 Linux 时检测到了 CD-ROM 驱动器。如果你的 CD-ROM 驱动器是 IDE 驱动器，输入 `dmesg | grep ^hd`。你应该看到关于 CD-ROM 的信息，如下：`hdc: CD-ROM CDU701, ATAPI CDROM drive or hdc`. ATAPI 14X CD-rom drive, 128KB Cache。

- 如果没有看到 CD-ROM 驱动器的指示，请检查 CD-ROM 的电源和电缆是否连接。为了确保硬件正常，你也可以启动到 Windows（如果已安装且你正在运行双系统）并尝试访问 CD。

- 尝试插入软件 CD-ROM。如果你正在运行 GNOME 或 KDE 桌面，应该出现一个桌面图标显示 CD 已自动挂载。如果没有出现图标，进入终端窗口，以 root 用户身份输入 `mount /dev/cdrom`。然后切换到 `/media/cdrom` 或 `/dev/media` 目录并使用命令 `cd /media/cdrom; ls` 列出内容。这将告诉你 CD-ROM 是否可用。

如果 CD-ROM 工作正常，但当你作为非 root 用户尝试播放音乐时出现 `CDROM device: Permission denied` 消息，问题可能是 `/dev/cdrom`（通常是指向实际硬件设备的链接）对 root 以外的任何人不可读。输入 `ls -l /dev/cdrom` 查看其属性。

# 第四部分

# 运行应用程序

图 20-1

使用 `gnome-cd` 播放 CD 并存储艺术家、曲目信息。

![](img/d7f79c91d15076e71790c1b4e1d072d0_560_0.png)

## 使用 Rhythmbox 音频播放器播放音乐

`Rhythmbox` 提供了一个 GNOME 音乐播放器，正如 Rhythmbox 文档所述，`Rhythmbox` 构建在 GStreamer 框架之上，用于开发媒体播放器、视频编辑器和流媒体。你可以从 CD 导入音乐并播放互联网广播电台，一切在一个界面完成。第一次运行 `Rhythmbox` 时，考虑通过选择 Preferences 设置 `Rhythmbox` 偏好。在 Music 标签中，你可以告诉 `Rhythmbox` 你想存储文件的位置（包括文件夹如何命名以及歌曲如何存储）。

在你设置好偏好后，将看到主音乐库界面。

> 如果你的发行版不支持 `Rhythmbox` 的 MP3 播放，不要担心，还有希望！在 Fedora 中，你可以使用 Codeina 功能从 Fluendo (`www.fluendo.com`) 下载免费 MP3 解码支持。对于 Ubuntu 和 Linux，请查看 Click-N-Run 服务的支持。

除了播放音乐文件外，`Rhythmbox` 还可以轻松刻录 CD。只需插入你想刻录的 CD，当它出现在列表 Devices 下时，右键点击 CD 并选择 Copy to Library。CD 将刻录并存储到你的 `Rhythmbox` 音乐收藏中。

添加 CD 界面非常漂亮。点击 Open Track Editor。你可以添加艺术家和标题信息。

# 图 20-2

定义你存储音乐的位置

![](img/d7f79c91d15076e71790c1b4e1d072d0_561_0.png)

# 图 20-3

查看带有《著名旋律歌谣》的音乐库

![](img/d7f79c91d15076e71790c1b4e1d072d0_561_1.png)

12 首歌曲，1 小时，67.5 MB

## 运行应用程序

`Rhythmbox` 还可以播放互联网广播电台。实现此点的简单方法是找到一个流媒体广播电台（寻找 Shoutcast PLS 文件，通常带有 `.pls` 扩展名）。保存 PLS 文件，然后在 Nautilus 浏览器中双击该文件。Nautilus 将启动 `Rhythmbox` 来播放音频。图 20-4 显示了带有各种互联网广播电台的 `Rhythmbox`。

图 20-4

`Rhythmbox-1`：播放互联网广播电台

![](img/d7f79c91d15076e71790c1b4e1d072d0_562_0.png)

`www.d1.fm` 网站列出了大量的免费互联网频道。

## 使用 XMMS 多媒体播放器播放音乐

`XMMS (X Multimedia System)` 多媒体播放器提供了一个播放 MP3、Ogg Vorbis、WAV 和其他音频格式音乐的图形界面。`XMMS` 有一些非常好的额外功能，包括均衡器、播放列表编辑器以及添加更多插件的能力。它最大的属性之一是 `XMMS` 易于使用。该播放器看起来很熟悉，样式是模仿 Winamp 程序设计的。

Red Hat 因为与 MP3 格式相关的专利问题删除了所有 MP3 编码或解码的软件。虽然 `XMMS` 播放器需要解码 MP3，但它并未包含。要在你的 Red Hat 或 Fedora 发行版中重新添加 MP3 支持，你可以安装 MP3 插件。获取支持 MP3 解码的 RPM 包的地方是 `http://rpm.livna.org`。它们也可以从其他来源获取，包括 `www.xmms.org` 和 `www.gurulabs.com/downloads.html`。此问题并不一定适用于其他 Red Hat 派生的发行版。

## 播放音乐和视频

通过选择 Sound & Video Audio Player 或在终端窗口中输入 `xmms` 来启动 `XMMS` 音频播放器。图 20-5 显示了带有关联均衡器（左侧）和播放列表编辑器（右侧）的 `XMMS` 音频播放器。

### 20-5

从 `XMMS` 播放列表播放 Ogg Vorbis 和其他音频文件。

![](img/d7f79c91d15076e71790c1b4e1d072d0_563_0.png)

如前所述，你可以播放多种音频格式。支持的格式包括：

- MP3（带有插件）

- Ogg Vorbis

- WAV

- AU

- CD 音

- CIN 电影

如果 `XMMS` 无法找到配置，它会将输出重定向到 Disk Writer 插件。这会导致你播放的文件以 WAV 文件的格式写入硬盘。

你可以从 `www.xmms.org` 获取更多音频插件。`XMMS` 音频播放器可以以以下方式使用：

- 通过从 CD 刻录歌曲、从 Web 上的可访问目录中复制歌曲，或通过在 CD-ROM 驱动器中插入音乐 CD 来获取音乐文件。（`XMMS` 期望可以通过 `/dev/cdrom` 访问 CD）。
