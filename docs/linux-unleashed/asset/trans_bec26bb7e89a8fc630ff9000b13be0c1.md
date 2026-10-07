
# 音乐 (14, 8)

```bash
if [ -e /dev/Music ]; then
    rm -f /dev/Music
fi

mknod -m 666 /dev/music c 14 8
if [ -e /dev/sequencer2 ]; then
    rm -f /dev/sequencer2
fi
ln -s /dev/music /dev/sequencer2

# Midi devices

if [ -e /dev/midi ]; then
    rm -f /dev/midi    # Old name. Don't use it
fi
if [ -e /dev/midi00 ]; then
    rm -f /dev/midi00
fi
mknod -m 666 /dev/midi00 c 14 2
ln -sf /dev/midi00 /dev/midi

if [ -e /dev/midi01 ]; then
    rm -f /dev/midi01
fi
mknod -m 666 /dev/midi01 c 14 18

if [ -e /dev/midi02 ]; then
    rm -f /dev/midi02
fi
mknod -m 666 /dev/midi02 c 14 34

if [ -e /dev/midi03 ]; then
    rm -f /dev/midi03
fi
mknod -m 666 /dev/midi03 c 14 50

# DSP (14, 3)

if [ -e /dev/dsp ]; then
    rm -f /dev/dsp
fi
if [ -e /dev/dsp0 ]; then
    rm -f /dev/dsp0
fi
mknod -m $AUDIOPERMS /dev/dsp0 c 14 3
ln -s /dev/dsp0 /dev/dsp

# DSPW (14, 5)

if [ -e /dev/dspW ]; then
    rm -f /dev/dspW
fi
if [ -e /dev/dspW0 ]; then
    rm -f /dev/dspW0
fi
mknod -m $AUDIOPERMS /dev/dspW0 c 14 5
ln -s /dev/dspW0 /dev/dspW
if [ -e /dev/dspW1 ]; then
    rm -f /dev/dspW1
fi
mknod -m $AUDIOPERMS /dev/dspW1 c 14 37

# SPARC compatible /dev/audio (14, 4)

if [ -e /dev/audio ]; then
    rm -f /dev/audio
fi
if [ -e /dev/audio0 ]; then
    rm -f /dev/audio0
fi
mknod -m $AUDIOPERMS /dev/audio0 c 14 4
ln -s /dev/audio0 /dev/audio

# DSP1 (14, 19) /dev/dsp for the second soundcard.
# Also the SB emulation part of the PAS16 card.

if [ -e /dev/dsp1 ]; then
    rm -f /dev/dsp1
fi
mknod -m $AUDIOPERMS /dev/dsp1 c 14 19

# SPARC audio1 (14, 20)
# /dev/audio for the second soundcard.
# Also the SB emulation part of the PAS16 card.

if [ -e /dev/audio1 ]; then
    rm -f /dev/audio1
fi
mknod -m $AUDIOPERMS /dev/audio1 c 14 20

# /dev/sndstat (14,6) For debugging purposes

if [ -e /dev/sndstat ]; then
    rm -f /dev/sndstat
fi
mknod -m 666 /dev/sndstat c 14 6

exit 0
```

## 排查安装和配置问题

与任何设备一样，在安装和配置声卡后，可能会出现需要修正的问题。当然，如果你的系统运行完美，可以跳过本节。

如果在重新编译内核后没有声卡支持，并且在启动序列中没有关于声卡的消息，那么很有可能你并不是从新内核启动的。以下命令显示正在启动的内核的详细信息。

```bash
uname -a
```

检查时间和日期，看是否与重新编译的时间一致。如果不一致，你可能需要使用 LILO 将新内核安装到启动设备上，或者再次重复整个重新编译过程。

> **提示**
> 大多数 Linux 系统上的 `/proc/version` 文件包含与 `uname -a` 命令相同的信息。你可以使用其中任意一种方法来检查内核版本。

假设内核版本是你刚刚编译的那个，你需要检查声卡是否已链接到内核本身。`/proc/devices` 文件列出了内核包含的字符设备和块设备。查找“sound”（通常为数字 14）的条目。如果那里没有，说明声卡组件未链接到此内核，你需要重做配置例程。

如果 `/proc/devices` 文件看起来正常，并且在启动过程中看到了关于声卡的消息（你可以使用 `dmesg` 命令或查看 `/var/adm/messages` 文件来重放所有这些消息），那么很有可能你正在使用一张“兼容”卡，但它并不是非常兼容。这种情况在使用 SoundBlaster 兼容卡时很常见，其中真实声卡的驱动程序无法找到兼容卡。检查驱动程序附带的 README 文件，看看是否有关于你特定声卡及其问题的提及，并检查制造商的 Web 或 FTP 站点。

另一种检查声卡安装状态的方法是查看 `/dev/sndstat` 文件。如果你找不到这个文件，说明你还没有运行 `/usr/src/linux/drivers/sound/Readme.Linux` 文件末尾的声卡安装脚本。从文件中剪切该脚本，使其可执行，然后运行它。然后你应该会看到一个生成的 /dev/sndstat 文件。

在 /dev/sndstat 中可能会看到几条错误消息，有助于你确定声卡的问题。表 21.2 显示了最常见的消息、产生原因以及可能的解决方案。在每种情况下，错误消息前都有设备名称。

**表 21.2.** /dev/sndstat 错误消息。

| 错误消息 | 产生原因及解决方案 |
| :--- | :--- |
| No such device | 内核不包含声卡驱动程序。重建内核。 |
| No such device or address | 声卡驱动程序无法在指定配置中找到声卡。检查配置设置。 |

## 声卡应用

根据你想要做的事情，有许多应用程序可以与你的声卡配合使用。这些应用程序中的大多数可以通过 FTP 站点获取，或者包含在你的 CD-ROM Linux 发行版中。要检查这些文件是在你的系统还是 CD-ROM 上，请使用 find 命令查找可执行程序的文件名。

我们不会逐一介绍 Linux 上可用的每个应用程序，因为有好几十种。相反，我们将挑选几个具有代表性的示例。查看 FTP 站点可以让你了解所有其他可用的应用程序。

### vplay, vrec, splay, and srec

vplay 实用工具及其三个合作伙伴是由 Hannu Savolainen 和 Michael Beck 开发的一组名为 snd-util 的声卡工具。这些是早期 Linux 开发阶段开发的简单的声音录制和播放实用工具，但即使今天，如果你愿意使用命令行界面而不是华丽的 GUI，它们仍然运行良好。srec 工具录制声音，splay 回放声音。（要录制，你需要一个麦克风或其他输入设备，如来自 CD 的馈送。）

> **提示**
> snd-util 3.0 软件包（本书付印时的当前版本）最容易通过 FTP 获取：
> `ftp.sunsite.unc.edu/pub/Linux/apps/sound/snd-util-3.0.tar.gz`

srec 实用工具允许你指定录制时间和采样率。声音以原始文件格式（.raw 文件扩展名）存储。要使用 21KHz 采样率录制 20 秒的声音样本，并将输出存储在 sample.raw 文件中，请使用此命令：
`srec -t 20 -s 21000 sample.raw`

要回放刚刚录制的声音，你需要 splay 实用工具，并且必须指定文件名和采样率：
`splay -s 21000 sample.raw`

如果你选择了错误的采样率，你会立刻注意到，因为声音将不像原始声音。

vplay 和 vrec 命令分别基于 splay 和 srec，但增加了将文件保存为 .wav 格式和 .voc 格式（SoundBlaster 声卡使用）的功能。

### WAVplay

WAVplay 是由 Andre Fuechsel 开发的图形化声音录制和播放实用工具。WAVplay 让你可以看到声音在录制和播放时的波形。你可以通过点击 GUI 上的选项来改变采样速度和每个样本的位数。可以录制立体声和单声道信号。WAVplay 仅录制 .wav 文件。

> **提示**
> WAVplay 的最新版本是 2.1，可以从 FTP 站点获取：
> `ftp.sunsite.unc.edu/pub/Linux/apps/sound/players/wavplay021w1.tar.z`

### Sound Studio

Sound Studio 由 Paul Sharpe 编写。它是一个基于 X 的应用程序，提供你几乎可以想到的用于声音录制和播放的所有工具。Sound Studio 允许你录制、编辑和播放多种格式的声音文件。用 Tcl/Tk 为 Linux 编写（以及一些 C 代码），Sound Studio 展示了这个操作系统所能做到的事情。

> **提示**
> Sound Studio 的最新版本是 0.21，可以从 FTP 站点获取：
> `ftp.sunsite.unc.edu/pub/Linux/apps/sound/players/studio.0.1.tgz`

### MiXViews

MiXViews 与 Sound Studio 类似，因为它也是基于 X 的，但它是在 UNIX 工作站上开发的，并移植到 Linux 上。作者是 Douglas Scott。MiXViews 允许录制和播放大多数格式的声音文件。你可以使用 MiXViews 在屏幕上编辑声波。与这里提到的其他工具不同，MiXViews 通过允许声音的滤波、缩放和混合来扩展声卡的功能。

> **提示**
> MiXViews 的最新版本可以从 FTP 站点获取：
> `ftp.ccs.ucsbedu/pub/MixViews`

### 操纵杆

有些游戏如果使用操纵杆而不是鼠标和键盘来玩会更有乐趣。由于大多数计算机都内置了操纵杆端口（在主板或带有串行或并行端口的多功能板上），利用该端口将是一个不错的选择。不幸的是，Linux 没有内置操纵杆驱动程序。幸运的是，已经发布了几种操纵杆驱动程序。当然，操纵杆仅对支持该设备的游戏有用。不支持操纵杆的游戏可能无法用操纵杆玩。

