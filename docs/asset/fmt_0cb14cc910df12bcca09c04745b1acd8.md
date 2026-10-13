
> 提示：要从 iPod 同步并导入，你可以使用如 GUI for iPod (`gtkpod`) 这样的 iPod 管理软件。目前有多个脚本和工具用于 iPod 操作，包括 `syncpod`、`mypod`、`GUI for ip` (`gtkpod`) 以及适用于 Linux 的。检查 `sourceforge.net` 并搜索 `ipod`。安装可能会更加复杂，因为许多程序并不是 RPM 软件包格式（参考本章前面的“安装源代码应用程序”）。

## Totem 和 Xine 视频支持

对于视频支持，你应该安装完整的 GStreamer 和 xine 支持。从 `freshrpm.net` 下载以下库。要安装 GStreamer 额外扩展，你首先需要按照上一节所述安装用于 MP3 支持的音频库，然后安装 g 库。你将首先安装 `gstreamer-audio`，然后是 `gstreamer`，最后是 `gstreamer-dvd-extras`。使用 `freshrpm.net` 时，请确保根据情况选择合适的 ix86 或 64 位版本（而不是源代码文件）。对于 DVD，你还需要 `a52dec` 库。

```
gstreamer-ffmpeg
gsm
gstreamer-plugins-extras-audio
gstreamer-plugins-extras-dvd
a52dec
gstreamer-plugins-extras-dvd
```

## DVD 支持

对于 DVD 支持，你需要下载几个软件包，包括 MPEG2 库、允许你导航菜单的 DVD 导航库，以及访问 DVD 光盘的 DVD 播放和读取库。（商业级 DVD 软件有 PowerDVD，而 InterVideo 的 LinDVD 正在开发中）。需要先安装 `libvdcss`。接下来你必须在安装 `libdvdplay` 或 `libdvdnav` 之前安装 `libdvdread`。

```
libdvdcss
libdvdread
libdvdplay
libdvdnav
libdvdpsi
```

为了实际播放 DVD，你需要一个 DivX 播放器。Fedora Core 提供了 Mplayer 和 xine。请确保先安装之前列出的 DivX 支持包。对于 xine，你首先需要从 `freshrpms.net` 获取 `aalib` 和 `libXvMCW` 库。

```
mplayer-fonts
libXvMCW
xine-lib
xine
```

你可以从 `freshrpms.net` 以相同的名称下载 Mplayer。你需要几个支持包，包括 `libc`、`mplayer` 字体、`xvidcore`、`mmcs` 和 `lzo`。`Mplayer` 可以播放多种媒体格式，包括 DivX。默认情况下，`mplayer` 通常会选择 `mcv`（运动补偿 xv）。如果此不起作用，打开首选项（Preferences），选择视频面板（video），并选择 `xv` 作为标准输出。

```
lirc
mplayerfonts
xvidcore
xmms
lzo
mplayer
```

## DivX 支持

DivX 支持只需安装 DivX 解码器。然后你就可以使用 `xine` 等媒体播放器运行它们。有两个软件包可用：`Div4Linux` 和 `Xvid`。`Xvid` 是 DivX 的 OpenDivX 实现。DivX 软件包位于 `rpm.livna.org/fedora` 站点，名为 `xvidcore`，在 `freshrpms.net` 上可能有更新的版本（你可能已经安装了 `xvidcore` 以供 `mplayer` 使用）。

```
xvidcore
```
