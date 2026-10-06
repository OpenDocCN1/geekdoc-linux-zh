
音频 CD 具有特殊的编码格式，这意味着不应使用 `mount(8)` 挂载它们。

各种应用程序（如 `audio/workman`）提供了更友好的界面。可以安装 `audio/mpg123` 来收听 MP3 音频文件。

另一种测试声卡的快速方法是将数据发送到 `/dev/dsp`：

```
% cat filename > /dev/dsp
```

其中 `filename` 可以是任意类型的文件。此命令应该产生一些噪音，从而确认声卡正在正常工作。

注意

`/dev/dsp*` 设备节点将根据需要自动创建。在未使用时，它们不存在，且不会出现在 `ls(1)` 的输出中。

### 7.2.3. 设置蓝牙音频设备

连接到蓝牙设备不是本章的讨论范围。更多信息请参阅第 32.5 节“蓝牙”。

要在 FreeBSD 的音效系统中启用蓝牙音频输出（sink），用户必须安装 `audio/virtual_oss`：

```bash
# pkg install virtual_oss
```

`audio/virtual_oss` 需要将 `curse` 加载到内核：

```bash
# kldload curse
```

要在系统启动时加载 `curse`，请运行此命令：

```bash
# sysrc -f /boot/loader.conf curse_load=yes
```

使用 `audio/virtual_oss` 将耳机作为音频输出，用户需要在连接到蓝牙音频设备后创建一个虚拟设备：

```bash
# virtual_oss -C 2 -c -r 48000 -b 16 -s 768 -R /dev/null -P /dev/bluetooth/headphones -d d
```

注意

此示例中的 `headphones` 是来自 `/etc/bluetooth/hosts` 的主机名。也可以使用 BT_ADDR。更多信息请参阅 `virtual_oss(g)`。

### 7.2.4. 音频故障排除

表 7.1“常见错误消息”列出了一些常见的错误消息及其解决方案：

#### 表 7.1 常见错误消息

| 错误 | 解决方案 |
| :--- | :--- |
| sb_dspwrr(XX) timed out | I/O 端口设置错误。 |
| bad irq XX | IRQ 设置错误。确保设置的 IRQ 与音频 IRQ 相同。 |
| xxx: gus pcm not attached, out of memory | 没有足够的可用内存使用该设备。 |
| xxx: can't open /dev/dsp! | 运行 `fstat \| grep dsp` 检查是否有其他程序打开该设备。值得注意的排除对象是 esound 和 KDE 的音频支持。 |

现代显卡通常带有一个用于 HDMI 的自带声卡驱动程序。此音频设备有时会在声卡之前枚举，这意味着声卡将不会被作为默认播放设备。

要检查是否是这种情况，请运行 `dmesg` 并查找 `pcm`。输出看起来如下：

...

```
hdac0: HDA Driver Revision: 20100226__0142
hdacac1: HDA Driver Revision: 20100226_0142
hdhac0: HDA Codec #0: NVidia (Unknown)
hdhac0: HDA Codec #1: NVidia (Unknown)
hdhac0: HDA Codec #2: NVidia (Unknown)
hdhac0: HDA Codec #3: NVidia (Unknown)
```

```
pcm0: <HDA NVidia (Unknown) PCM #0 DisplayPort> at cad 0 nid 1 on hdac0
pcm1: <HDA NVidia (Unknown) PCM #0 DisplayPort> at cad 1 nid 1 on hdac0
```

```
pcm2:<HDA NVidia (Unknown) PCM #0 DisplayPort> at cad 2 nid 1 1 hdac0
pcm3:<HDA NVidia (Unknown) PCM #0 DisplayPort> at cad 3 nid 1 1 hdac0
hdac1: HDA Codec #2: Realtek ALC889
pcm4:<HDA Realtek ALC889 PCM #0 Analog> at cad 2 nid 1 1 hdac1
pcm5:<HDA Realtek ALC889 PCM #1 Analog> at cad 2 nid 1 1 hdac1
pcm6:<HDA Realtek ALC889 PCM #2 Digital> at cad 2 nid 1 1 hdac1
pcm7:<HDA Realtek ALC889 PCM #3 Digital> at cad 2 nid 1 1 hdac1
...
```

在此示例中，显卡（NVidia）在声卡（Realtek ALC889）之前被枚举。要将声卡作为默认播放设备，请将 `hw.snd.default_unit` 修改为应用于播放的单元：

```bash
# sysctl hw.snd.default_unit= n
```

其中 `n` 是要使用的音频设备编号。在此示例中，它应该是 4。通过向 `/etc/sysctl.conf` 添加以下行来使此更改永久生效：

```bash
hw.snd.default_unit= 4
```

### 7.2.5. 利用多个音频源

由 Munish Chopra 贡献。

通常希望有多个能够同时播放的音频源。FreeBSD 使用“虚拟音频通道”通过在内核中混合声音对声卡的播放进行多路复用。

有三个 `sysctl(8)` 参数可配置虚拟通道：

```bash
# sysctl dev.pcm.0.play.vchans=4
```

```bash
# sysctl dev.pcm.0.rec.vchans=4
```

```bash
# sysctl hw.snd.maxautchans
```

此示例显示了 `dev.pcm.0.play.vchans=4` 和 `dev.pcm.0.rec.vchans=4` 是如何配置的。`hw.snd.maxautchans` 显示了虚拟通道的数量。

注意

在设备在使用期间，无法更改虚拟通道的数量。首先关闭相关程序。更多信息请参阅 `pcm(4)`。

### 7.2.6. 为混合通道设置默认值

由 Josef El 贡献。

混合通道的默认值硬编码在驱动程序中。虽然可以使用守护进程更改，但这并非永久解决方案。相反，要设置默认值，请在 `/boot/loader.conf` 中定义，如下：

```bash
hint.pcm.0.vol="50"
```

这将在 `pcm` 模块加载时将设置为 50。

### 7.3.2. 刻录 CD 音频

在将 CD 或轨道编码为 MP3 之前，必须将音频刻录到硬盘。这是通过将原始 CD 数字音频 (CDDA) 数据转换为 WAV 实现的。`cddawav` 工具随 `sysutils/cdrtools` 单元安装，可从 CD 刻录音频。当音频 CD 在驱动器中时，以 root 身份执行以下命令将整张 CD 刻录为 WAV：

```bash
# cddawav -D 0,1,0 -B
```

在此示例中，`-D 0,1,0` 指示要刻录的 SCSI 设备 `0,1,0`。使用 `cdrecord -scan` 确定系统的正确设备参数。要刻录单个轨道，使用 `-t` 指定轨道：

```bash
# cddawav -D 0,1,0 -t 7
```

要刻录轨道范围（例如第一到第七轨道），指定范围：

```bash
# cddawav -D 0,1,0 -t 1+7
```

要从 ATAPI (IDE) CDROM 驱动器刻录，使用设备名称代替设备 。例如，从 IDE 驱动器刻录第 7 轨道：

```bash
# cddawav -D /dev/acd0 -7
```

或者可以使用 `dd` 从 ATAPI 驱动器提取音频轨道，见第 18.5.5 节“复制音频 CD”。

### 7.3.3. MP3 的编码与解码

Lame 是一种流行的 MP3 编码器，可以从 `audio/lame` 端口安装。由于专利问题，未提供软件包。

以下命令将刻录的 `audio01.wav` 转换为 `audio01.mp3`：

```bash
# lame -h -b 128 --tt "Foo Song Title " --ta "FooBar Artist " --tl " FooBar Album " \
```

```bash
-ty "2014" -tc "Ripped and encoded by Foo " --tg "Genre" audio01.wav audio01.mp3
```

指定的 128 kbits 是标准的 MP3 比特率，而 160 和 192 比特率提供更高的质量。比特率越高，生成的 MP3 文件尺寸越大。`-h` 开启“质量更高但速度稍慢”模式。

以 `--t` 开头的选项表示 ID3 标签，标签通常包含歌曲信息，将嵌入到 MP3 文件中。额外的编码选项可以在 lame 手页中找到。

## 第 7 章 多媒体

为了从 MP3s 刻制音频 CD，必须将它们转换为非压缩文件格式。可以使用 XMMS 转换为 WAV 格式，而可以使用 `mpg123` 转换为原始脉冲编码调制 (PCM) 音频数据格式。

使用 `mpg123` 转换 `audio01.mp3` 时，请指定 PCM 文件的名称：

```
# mpg123 -s audio01.mp3 > audio01.pcm
```

使用 XMMS 将 MP3 转换为 WAV 格式，请遵循以下步骤：

#### 程序 7.1. 在 XMMS 中转换为 WAV 格式

- 1. 启动 XMMS。
- 2. 右键点击窗口调出 XMMS 菜单。
- 3. 选择选项 (Options) 下的首选项 (Preferences)。
- 4. 将输出插件 (Output Plugin) 更改“磁盘写入插件 (Disk Writer Plugin)”。
- 5. 点击配置 (Configure)。
- 6. 输入或浏览到写入未压缩文件的目录。
- 7. usual将 MP3 文件加载到 XMMS，音量设置为 100% 并关闭 EQ 设置。
- 8. 点击播放 (Play)。XMMS 看起来正在播放 MP3，但听不到音乐。它实际上正在将 MP3 到一个文件中。
- 9. 完成后，务必将默认输出插件设回原来的设置，以便再次播放 MP3。

WAV 和 PCM 格式都可以配合 `cdrecord` 使用。使用 WAV 文件时，每个轨道开头都会有一个细微的“嗒嗒”声。这个声音是 WAV 文件的头部。可以使用 `audio/sox` 端口或包移除头部：

```
% sox -t wav -r 44100 -s -w -c 2 track.wav track.raw
```

有关在 FreeBSD 中使用 CD 刻机的更多信息，请参阅第 18.5 节“创建和使用 CD 媒体”。

## 7.4 视频播放

Ross Lippert 贡献。

在配置视频播放之前，请确定显卡的型号和芯片。虽然 Xorg 支持多种显卡，但并非所有显卡都能提供良好的播放性能。要获取使用该卡的 Xorg 服务器支持的扩展列表，请在 Xorg 运行时运行 `xdpyinfo`。

准备一个短的 MPEG 测试来评估各种播放器和选项是一个好主意。由于某些 DVD 应用默认在 `/dev/dvd` 寻找 DVD 媒体，或者在其中硬编码了该设备名称，为正确的设备创建符号链接可能会很有用：

```
# ln -sf /dev/cd0 /dev/dvd
```

由于 `devfs(5)` 的特性，手动创建的链接在系统重启后不会存在。为了在系统启动时自动创建符号链接，请向 `/etc/devfs.conf` 中添加以下行：

`link cd0 dvd`

### 确定视频能力

DVD 解密会调用某些需要 DVD 设备写入权限的函数。

为了增强共享内存 Xorg 接口，建议增加这些 `sysctl(8)` 变量的值：

`kern.ipc.shmmax=67108864`

`kern.ipc.shmall=32768`

#### 7.4.1 确定视频能力

在 Xorg 下显示视频有多种可能的方法，有效性很大程度上取决于硬件。下面描述的每种方法在不同硬件上的质量会有所。常见接口包括：

- 1. Xorg：使用共享内存的普通输出。
- 2. XVideo：Xorg 接口的扩展，允许通过特殊加速直接在绘制对象中显示视频。该扩展即使在低端机器上也能提供良好的播放质量。下一节将描述如何确定此扩展是否运行。
- 3. SDL：简单多媒体层（Simple Directmedia Layer）是许多操作系统的移植层，允许开发高效利用音频和图形的跨平台应用程序。SDL 硬件底层抽象有时比 Xorg 接口更高效。在 FreeBSD 上，可以使用 `[devel/sdl20` 包或端口] 安装 SDL。
- 4. DGA：直接图形访问（Direct Graphics Access）是一种 Xorg 扩展，允许程序跳过 Xorg 服务器直接修改帧缓冲区。由于它依赖于底层内存映射，使用它的程序必须以 root 身份运行。可以使用 `dga(1)` 对 DGA 扩展进行测试和基准测试。当 `dga` 运行时，每次按键都会改变颜色。按 `q` 退出。
- 5. SVGALib：底层控制台图形层。

#### 7.4.1.1 XVideo

要检查此扩展是否运行，请使用 `xvinfo`：

```
% xvinfo
```

如果结果类似于，则该显卡支持 XVideo：

X-Video Extension version 2.2

screen #0

Adaptor #0: "Savage Streams Engine"

number of ports: 1

port base: 43

operations supported: PutImage

supported visuals:

depth 16, visualID 0x22

depth 16, visualID 0x23

number of attributes: 5

"XV_COLORKEY" (range 0 to 16777215)

client settable attribute

client gettable attribute (current value is 2110)

"XV_BRIGHTNESS" (range -128 to 127)

client settable attribute

client gettable attribute (current value is 0)

"XV_CONTRAST" (range 0 to 255)

client settable attribute

client gettable attribute (current value is 128)

"XV_SATURATION" (range 0 to 255)

client settable attribute

client gettable attribute (current value is 128)

"XV_HUE (range -180 to 180)

client settable attribute

client gettable attribute (current value is 0)

maximum XvImage size: 1024 x 1024

Number of image formats: 7

id: 0x32595559 (YUY2)

guid: 59555932-0000-0010-8000-00aa00389b71

bits per pixel: 16

number of planes: 1

type: YUV (packed)

id: 0x32315659 (YV2)

guid: 59563132-0000-0010-8000-00aa00389b71

bits per pixel: 12

number of planes: 3

type: YUV (planar)

id: 0x30323449 (I420)

guid: 49343231-0000-0010-8000-0aa00389b71

编码视频，请编译 `multimedia/mencoder` 端口。由于许可限制，MEncoder 不提供相应的软件包。

首次运行 MPlayer 时，它会在用户的家目录下创建 `~/.mplayer`。该子目录包含

用户特定配置文件的默认版本。

本节仅描述了少数常用用法。有关其众多选项的完整描述，请参阅 `mplayer(1)`。

要播放 `testfile.avi`，请使用 `-vo` 指定视频接口，如下所示：

```
% mplayer -vo xv testfile.avi
```

```
% mplayer -vo sdl testfile.avi
```

```
% mplayer -vo x11 testfile.avi
```

```
# mplayer -vo dga testfile.avi
```

```
# mplayer -vo 'sdl:dga' testfile.avi
```

尝试所有选项都是值得的，因为它们的相对性能取决于许多因素，并随硬件的不同而产生巨大差异。

要播放 DVD，将 `testfile.avi` 替换为 `dvd://N -dvd-device DEVICE`，其中 N 是要播放的标题编号，DEVICE 是 DVD 的设备节点。例如，要播放 `/dev/dvd` 上的标题 3：

```
# mplayer -vo xv dvd:///3 -dvd-device /dev/dvd
```

注意

在构建 MPlayer 端口期间，可以通过包含 `WITH_DVD_DEVICE=/path/to/desired/device` 选项来定义默认 DVD 设备。默认情况下，设备为 `/dev/cd0`。更多细节可以查看端口的 `Makefile.options`。
