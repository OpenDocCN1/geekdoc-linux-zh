
Ian Wilson 开发的声色库 `Vintage_Dreams_Waves_v2` 包含 128 种模拟合成器声音和 8 组鼓组。它适用于 AWE 和 Live!。

设置（如平移或音高轮（必须先在“视图”下激活）），这些更改将立即反映在 `oseqview` 中。

查看可用的接收和发送端口列表，以及它们与 `anect -il` 或 `anect -ol` 的连接状态。使用 `anect` 建立的连接可以使用选项 `-d` 终止，例如 `anect -d 128:0 129:0`。若要终止所有连接，请使用 `anect -x`。关于 `anect` 更多命令行选项的概述，可以在 `anect` 的 man 页中查看（`man anect`）。

## 提示

`asegnet` 允许你与远程网络主机建立 MIDI 连接。

| MIDI 通道 | 移调 | 分割点 0: 36 |
| --- | --- | --- |
| 9 | 12 |  |
| MIDI 通道 | 移调 | 分割点 1: 48 |
| 1 | 0 |  |

图 6.10：使用 QMIDIRoute 设置分分区域

`QMIDIRoute` 程序实现了灵活的 MIDI 路由。它根据音高、速度或通道对在可写 MIDI 端口接收到的 MIDI 事件进行排序，并将其发送到可读端口。使用参数“Channel”（通道）和“Transpose”（移调）更改下方分割区域的通道和音高。例如，如果你在这里设置通道 9，则可以在播放下方分割区域鼓的同时，在上分割区域播放另一个乐器。

## kmid - KDE MIDI 播放器

`package kdemultimedia`

## Linux 中的声音

![](img/6f2aa18f72ac98d3e7fd7681b32a7a07_150_0.png)

图 6.11：kmid 主窗口和通道视图

在 KDE 菜单中，进入“多媒体”→“MIDI/KaraOK 播放器”。kmid 的几个演示文件位于 `/opt/kde2/share/apps/kmid` 目录中，格式为 `.kar`。这些文件还包含歌词，歌词会随播放同步滚动和高亮。

如 http://www.midi.net 等网址提供了丰富的 MIDI 文件下载。在 http://www.classicalarchives.com 可以获得广泛的古典音乐 MIDI 存档。

可以通过 `F1` 访问 kmid 的详细在线帮助。在此程序中，必须在“设置”→“MIDI 设置”中正确选择 MIDI 端口。

当点击工具栏上的键盘按钮时显示的通道视图尤为值得注意。你可以向右放大窗口以查看此项。通道视图（其窗口大小可能也需要调整）以图形化方式显示多个键盘上的 MIDI 事件。此外，还可以在此处更改乐器。如果通过 KDE 文件管理器 Konqueror 点击 MIDI 文件来启动 kmid，则在 KDE 控制中心中指定的 MIDI 设置将生效。程序本身指定的配置仅在你单独使用该程序时生效。

## 无需波表卡播放 MIDI 文件

`package iiwusynth, timidity`

并不是所有的声卡都带有波表合成器来根据加载的音色库（或乐器补丁）播放 MIDI 文件。如果是如此，你可以使用软件波表合成器 `iiwusynth` 和 `timidity++`。

## 音色库合成器 iiwusynth

在使用如下命令启动程序后：

```bash
earth:tux iiwusynth -a alsa -m alsa_seq gm.sf2
```

`iiwusynth` 将列在可写 MIDI 端口列表中并可以作为声源。在此示例中，`gm.sf2` 是一个 SoundFont 格式的文件。网上可以找到合适的文件。`iiwusynth` 有许多命令行选项，可以通过 `iiwusynth -h` 显示。

## 配置 timidity++

`timidity++` 通过配置文件 `/usr/share/timidity/timidity.cfg` 进行配置。可以通过 `man timidity.cfg` 查看配置文档。还请阅读 `/usr/share/doc/packages/timidity` 下的文档。

合适的的乐器补丁可以在 http://www.stardate.bc.ca/ewpatches/default.htm 获得。从该 URL 你可以下载文件 `eawatsls12_full.rar`。该文件大小为 22 MB，下载是非常值得的，因为它为你提供了一整套 GM/GS/X 乐器。要配合 `timidity++` 使用这些补丁，请按照以下步骤操作：首先，切换到 root 用户。然后创建目录 `/usr/share/timidity/ewpatches`，将 `eawatsls12_full.rar` 复制到那里，并切换到该目录。执行命令 `unrar x eawatsls12_full.rar` 解压压缩包。

现在可以修改 `/usr/share/timidity/` 目录下的 `timidity.cfg` 文件，使其仅包含以下两行：

```bash
dir /usr/share/timidity/ewpats
source timidity.cfg
```

## 文件：timidity.cfg

`eawpats12_full.rar` 包含另一个 `timidity.cfg`，解压后将显示 `eawpats` 目录。该文件通过 `source` 命令引入。该文件中只有四行是重要的：

- `source gravis.cfg`
- `source gsdrums.cfg`
- `source gssfx.cfg`
- `source xmap2.cfg`

所有其他行均可以删除。最后一步是调整文件权限。执行此操作，输入命令 `chmod -R a+x /usr/share/timidity`。要配合 `timidity++` 使用补丁，请修改 `timidity.cfg` 文件指向 `eawpats` 目录：

```bash
dir /usr/share/timidity/ewpats
```

![](img/6f2aa18f72ac98d3e7fd7681b32a7a07_155_0.png)

图 6.13: Ladspa Browser

将外部声源连接到声卡并使用 `alsmixer` 指定正确的捕获设置，该示例在没有 JACK 的情况下也可以运行。通过“Module”（模块）->“Show Ladspa Browser”（显示 Ladspa Browser）启动浏览器，可以为 LADSPA 效果生成模块。除非你使用 AlsaSynth 作为复声合成器，否则应始终使用“Create Plugin”（创建插件）生成插件。“Create Poly Plugin”会为每个部分生成独立的插件。

## 合成器补丁 (Patches)

在使用 MIDI 交叉线板 `connect` 连接 AlsaModularSynth 与主键盘（`vkeybd` 或外部键盘）后，你可以将该程序作为合成器使用。如果没有使用参数 `--poly` 显式激活复声，AlsaModularSynth 就是单声的，就像它的经典模型一样。在 `example_basic_vcf.ams` 中，声音通过滤波器进行了修改。在 `example_basic_vcf_reverb.ams` 中添加了滤波器和共振。在大多数补丁中，音高弯曲调制轮由模块参数决定。为了防止层循环，只有当当前参数值被接受过一次时，这些 MIDI 控制器的移动才会生效。就像模拟合成器中一样，包络模块是“单次触发”的——它们不会为了连奏播放而重启。这使得一些有趣的短句成为可能。

在 `example_full_midi.ams` 中，前十六个控制器事件被链接到模块参数。如果你没有可以检测这些事件的设备，可以使用通过 `qmidicontrol` 启动的软件 MIDI 控制器框 QMidiControl。在实验此程序实验时，通过“Control Center”（控制中心）->“Show Control Center”打开控制中心。如果在这里激活了“Follow Midi”（跟随 MIDI）复选框，最近移动的 MIDI 控制器和绑定到它的第一个参数将自动显示。

## 使用“控制中心”进行跟踪

“控制中心”的主要目的是将模块参数绑定到 MIDI 控制器上。然而，在这里也可以指定扩展的参数控制设置，例如滑块的范围。

| MIDI 控制器 / 参数 | 模块 | 模块 / 参数 | MIDI Sign |
| --- | --- | --- | --- |
| + type: 10 channel: 0 param: 0 | + Freeverb (Version 3) ID 10 | | |
| + type: 10 channel: 0 param: 1 | - LFO ID 14 | 1 | |
| - Decay | ENV ID 3 | + Frequency | |
| - frequency | | - Phl | 1 |
| + type: 10 channel: 0 param: 10 | VCF ID 7 | + MCV ID 12 |
