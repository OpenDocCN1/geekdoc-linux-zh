
将 `/mnt/dsc` 路径替换为你的 Windows 安装所在的驱动器路径（接龙牌程序通常位于 `/windows` 目录下）。当熟悉的纸牌游戏出现时，你就可以准备运行一些 Windows 音乐和音频应用了。

## 更多 WINE，请继续 ...

WINE 下的声音支持是透明的——也就是说，不需要任何特殊设置。然而，可以说，像 Cakewalk 这样更复杂的程序不太可能运行。WINE 网站列出了数百种在 WINE 下运行并评分的应用程序（0 表示失败，5 表示成功）。获得最高分的两个是 Rasmus Ekman 的 Granulab（可在 `http://passagen.se/granny` 获取）和 David Billens 的 SimSynth（可在 `http://elisdee.onestop.net` 获取）。

### Granulab

Granulab 接受 WAV 格式的文件作为输入并执行称为颗粒的合成。该程序旨在实时运行，表演可以保存到磁盘。有关颗粒合成的更多信息，请参考 Curtis Roads 的《Computer Music Tutorial》。Cambridge, Mass.: MIT Press, 1996. ISBN 0-252-18158-4。不需要特殊的 DLL，作者的代码风格证明了 Granulab 在 WINE 下运行非常流畅。

在 WINE 下通过 `wine /docs/granny/granular.exe` 启动程序（根据你的系统替换目录路径）。图 15-7 显示了 Granulab 的控件。

![](img/43a9671cef617c9c7a18f7a6904433f1_380_0.png)

图 15-7：在 WINE 下运行的 Rasmus Ekman Granulab

Granulab 的基本操作简单：加载文件，勾选 Play 框，然后移动滑块来控制颗粒的各种参数。文件将持续循环直到你停止播放，你会立即听到参数的变化。有关 Granulab 操作的更多细节，请参阅程序优秀的文档。

### SimSynth

SimSynth 是一种带有实时参数控制的合成器，试图模仿过去的经典合成器。就像那些古老的仪器一样，SimSynth 提供了一个由旋钮和开关组成的控制界面，用于实时调整声音参数。提供了一个鼠标控制的键盘，外部 MIDI 键盘也可以控制合成器。

图 15-8 显示了 SimSynth 的运行情况。图中设置创建了一个 FM（频率调制）低音。SimSynth 软件包包含了

![](img/43a9671cef617c9c7a18f7a6904433f1_381_0.png)

各种合成器仿真，每种都可以实时控制、根据你的喜好进行调整并保存为新补丁。

更多信息请参阅 SimSynth 文档。

## 结语

感谢在其他 UNIX 发行版中类似的项目，Linux 继承了丰富的操作系统模拟软件传统。然而，Linux 的流行激发了程序员进行新的且创新的努力，以便在 Linux 下容纳其他系统及其软件。

理想情况下，我们将看到原生的 Linux 应用取代它们的 Windows、Macintosh 和 OS/2 对应物。但在幸运日子到来之前，本章分析和提到的模拟器是唯一的解决方案。希望它们运行得良好，让你能够运行那些没有 Linux 等效方案的少数应用程序。

## 后记

## 告别

我非常荣幸见证并帮助了 Linux 音乐和音频软件的成长，我将继续继续鼓励并关注它的发展。在短短几年内出现了大量卓越的软件，而我们的旅程才刚刚开始。就像 Linux 本身，这段路可能会有些颠簸，但在这条少有人走的道路上，这是意之中的。

## 加入我们吧！

如果你已经来到了这里，我邀请你继续前行。高质量 Linux Audio 和 MIDI 软件的发展依赖于你的参与，无论你是资深程序员还是 Linux 新手。如果你能贡献代码，请加入一个现有项目或接手一个无人维护的应用程序。加入 Linux Audio 开发组（地址：`http://www.linuxdj.com/audio/lad`）。如果你不能贡献代码，可以成为测试员或提供建议。请订阅在 `http://www.bright.net/~dilphil/linuxsound/mllists.html` 找到的 Linux Audio 邮件列表之一。我们欢迎协助编写文档。为你最喜爱的 Linux 音频程序编写一个网页。将你的原创音乐上传到网上，并注明是“Linux制作”（Made In Linux）。

我希望你喜欢这次 Linux MIDI 和音频软件的世界之旅。也许你发现了一些 Linux 独有的程序（如 jMax 或 Quasimodo），或者重新熟悉了像 MP3 播放器和 MOD 追踪器等熟悉的应用程序。无论你如何使用这本书，我希望它能带你发现一些有趣且实用的音乐和音频软件。

最重要的是，我希望你在这里介绍的程序中玩得开心。请记住：乐趣才刚刚开始……

## 词汇表

- **ADC**（模拟数字转换器）一种将电信号处理为一系列数字的设备。
- **additive synthesis**（加法合成）一种通过添加频率分量（通常为正弦波形式）创建复杂声音的合成方法。
- **ADSR**（攻击、衰减、维持、释放）通过四个阶段定义声音包络的形状。
- **AIFF**（音频交换文件格式）来自苹果计算机的声音文件格式。
- **algorithm**（算法）一种解决问题或完成任务的程序，其中程序的每一步都有严格的定义。
- **amplitude**（幅度）在数字音频中，信号最大样本的值。与声音的感知强度和响度成正比。
- **arpeggio**（琶音）将和弦分解为一系列音高。
- **attack**（攻击时间）ADSR 包络的第一部分，也称为上升时间段。
- **AU**一种来自太阳微系统的声音文件格式。
- **bit**（比特）一个二进制位，即 0 或 1。是计算机理解的最小信息单位。
- **bitrate**（比特率）声音文件转换为 MP3 音频文件的速率（单位为比特/秒）。以 128 kbps 编码的文件接近 CD 级音频保真度。更高的比特率可确保更好的音质，但需要更多的存储空间。
- **bit resolution**（位深）用于定义单个声音样本的位数（8 位、16 位或 32 位）。在数字音频中，采样声音的动态范围取决于其位深。低分辨率声音（8 位）适用于非音乐类应用，而高分辨率（16 位和 32 位）更适用于音乐和其他对音质要求刻的应用。
- **bitstream**（比特流）MP3 音频文件的比特流。
- **CD audio**（CD 音频）以 44.1 kHz 采样率、16 位分辨率的数字音频。
- **channel**（通道）在音频术语中，硬件或软件中信号输入/输出的路径。
- **cue channel**（触发通道）一种在打开声音之前等待信号的混调音器。
- **DAC**（数字模拟转换器）一种将一系列数字转换为电信号流的设备。
- **decay**（衰减）ADSR 幅度包络的第二段，从攻击阶段的终点到维持阶段的开始。
- **decibel**（分贝）用于声音相对幅度的测量单位（缩写为 dB）。
- **delay line**（延迟线）一种延迟输入信号输出的算法（例如回声效果）。
- **DMA**（直接内存访问）一种直接在计算机内存中进出传输数据的方法，绕过 CPU 的控制。
- **DSP**（数字信号处理）在数字领域创建或编辑信号。典型的 DSP 应用包括雷达和电信设备（如调制解调器），以及音频和图像处理软件。
- **dynamic range**（动态范围）音频系统可以表示的幅度全范围。
- **effect bus**（效果总线）混调器中将信号路由到效果处理器并传回的部分。
- **envelope**（包络）声音幅度变化的形状。
- **fader**（推子）一种控制输入或输出电平的软件或硬件滑块。
- **FFT analysis**（快速傅里叶变换分析）一种用于确定信号频率相对幅度，以确定波形形状的技术。
- **filter**（滤波器）一种允许某些频率通过并拒绝其他频率的设备或算法，从而修改信号的频率内容。
- **frequency**（频率）周期性波形在单位时间（通常为一秒）内重复的次数。
- **full duplex**（全双工）声卡同时录制和播放声音的能力。
- **gain**（增益）音频设备输出幅度与输入幅度的比值。
- **Hertz**（赫兹）频率测量单位，等于每秒一次循环（缩写为 Hz）。
- **iconic synthesis environment**（图标合成环境）通过在图形界面中匹配图标进行的软件合成。
- **interrupt**（中断）来自设备要求 CPU 立即注意的信号。
- **I/O**（输入输出）。
- **IRQ**（中断请求）来自特定设备（如调制解调器或声卡）通过设备中断号向 CPU 留的信号。
- **LISP**（列表处理）一种特别适用于人工智能和音乐算法探索的编程语言。
- **loop**（循环）重复播放录音的一部分。
- **LPC**（线性预测编码）通过使用已计算的数据预测输出样本进行重合成的方法。
- **Markov chain**（马尔可夫链）一种从一阶概率计算高阶概率的随机过程。
- **MIDI**（乐器数字接口）允许不同制造商的乐器（如合成器和鼓机）相互通信的硬件和软件规范。
- **mixer**（混合）将多个输入混合为平衡输出信号的设备。
- **MOD**（音乐模块）数字追踪软件常用的声音文件格式。
- **MP3**（MPEG音频规范第3层）由运动视频小组设计的音频压缩格式。
- **MPEG**（运动视频小组）为设计和实现商业音频视频应用标准而组织。
- **music specification language**（音乐规范语言）一种表示音乐符号和函数的编程语言。
- **note-off**（断音）表示音结束的 MIDI 信息。
- **note-on**（点音）表示音开始的 MIDI 信息。
- **opcode**（操作码）告诉计算机执行特定任务的编程语言指令。在 C 语言中，操作码可以是信号生成器或修改器、数学函数（包括 +, *, ）或其他处理输入数据的进程。
- **oscillator**（振荡器）产生波形的软件或硬件设备。
- **parameter**（参数）控制算法创建的声音特征的算法数值特性。
- **patching**（接线）通过真实或虚拟线连接模块。
- **PCM**（脉冲码调制）标准数字声音编码技术；将电脉冲转换为数字的采样过程。
- **periodic wave**（周期波）由特定频率的重复波形组成的音频信号。有音调的声音（如乐器制造的声音）是周期波。
- **phase**（相位）波形的起点，以单位圆的弧度表示。
- **pitch**（音高）对音频信号频率的主观反应。随着信号频率上升或下降，音调感知为升高或降低。
- **pitch-shifting**（移调）升高或降低信号的音调。
- **polyphony**（多声性）指示多个声部或旋律同时运动的音乐术语。也用于指示合成器的同时发声能力。
- probability（概率）事件发生的可能性。
- program change（程序更改）一种通知设备切换到特定存储声音的 MIDI 消息。
- pulse code modulation 脉冲编码见 PCM。
- quantize（量化）将连续模拟信号转换为比特的技术。在 MIDI 术语中，将事件的持续时间和/或开始时间舍入到用户定义值的过程。
- realtime synthesis（实时合成）以比采样率快的速度合成声音样本并将声音直接发送到 DAC（数模转换器）而不是保存到磁盘。
- release（释放）ADSR 包络的最后一个阶段。通常，该阶段从持续阶段的最后一点开始，并下降到振幅为零。
- resolution（分辨率）数字计算机输出（音频或视觉）中可能的细节程度（通常以位为单位）。
- sampling rate（采样率）对声音采样的赫兹（Hz）频率，例如 22050 Hz 或 44100 Hz（每秒循环）。
- scratching（搓碟）手动正向或反向操作唱片转盘以产生一种独特的摩擦声。
- SND 一种 NEXT 计算机上广泛使用的音频文件格式。
- software mixer（软件调音器）见 soundcard mixer。
- software synthesis（软件合成）使用数字计算机和处理器创建声音的方法。
- soundcard mixer（声卡调音器）一种用于管理电平、静音和独奏状态、输入增益以及声卡其他功能方面的软件应用程序。
- sound synthesis（声音合成）使用电子设备（如模拟和数字合成器）创建声音的通用术语。
- spectral dynamics processing（频谱动态处理）改变信号频率内容强度的过程。
- spectrum（频谱）声音频率成分的振幅和相位。
- spline curve（样条曲线）具有不连续性的平滑曲线。
- s（持续）ADSR 振幅包络的第三阶段，代表声音的“稳定状态”部分。
- synthesis（合成）将电子信号转换为声学声音的过程。
- track（轨道）录制和播放音频或 MIDI数据的特定硬件或软件通道。不同的组件——贝斯、鼓、人声——可能占据不同的轨道。
- **tracking**（采样）一种在轨道中排列声音样本然后对轨道进行循环和排序的方法。
- **transport controls**（传输控制）录制或播放设备的开始/停止/暂停/倒回/快进控制。
- **unit generator**（单元生成器）一种生成、修改或组合声音的算法。
- **VU meter**（VU 表）一种指示输入或输出电平的软件或硬件设备。
- **WAV**微软的一种流行的音频文件格式。
- **wavetable synthesis**（波表合成）一种使用预计算函数产生波形的合成类型。

## 关于 LINUX 音乐与声音 CD-ROM

随书的 CD-ROM 包含了法律允许尽可能专业的应用程序。

这里的几乎所有软件都可以被认为是“开发中”，但这绝不意味着它们是损坏的或没用的。如书中所示，即使是开发阶段的软件包也可以相当复杂。然而，考虑到 Linux 发行版的各种性以及文件系统偶尔的差异，某些应用程序可能在进行某些特定修改（hacking）之前无法在系统上编译/运行。如果您在构建、安装或使用软件包时遇到持续问题，请写信相关软件的作者或维护者。请清晰描述您的问题，并记住大部分软件都是免费提供的。

Linux 软件是一个快速的目标。为了获取最新版本，我鼓励读者访问“Linux Music and Sound Applications Pages”中列出的网站，以获取书中介绍并包含在光盘上的所有软件包。

光盘与书完全一样：书中第 2 章的软件将在光盘的 `Chapter_2` 目录中，第 3 章的软件在 `Chapter_3` 目录中，以此此类推。`/extra` 目录包含了100多个其他应用程序，包括 `SoX` 和 `playmidi` 等应用程序的 GUI 前端，以及书中未介绍的软件。

软件包的命名与书中所示相同（例如，`package-name-latest.tar.gz`），每个文件都链接到（命名适当的）软件包本身。因此，`RTcmix-latest.tar.gz` 实际上是 `RTcmix-3.0.1.tar.gz` 的链接。

如果可用，已包含 RPM 格式的二进制文件。

## 2 设置您的系统 (`/Chapter_2`)

- ALSA 0.5.7
- OSS/Linux 驱动程序 2.2.x

## 3 混音、播放和录制 (`/Chapter_3`)

- `aumix`
- `yarec`
- `SoX`

## 4 音频文件编辑器 (`/Chapter_4`)

- `DAP`
- `MiXViews`
- `Snd`
- `Kwave`
- `Broadcast2000`
- `Ceres`

## 5 MOD 文件与 Linux (`/Chapter_5`)

- `SoundTracker`
- `MikMod`
- Demos: Loop and State Of Mind

## 6 Linux MIDI 工作室 (`/Chapter_6`)

- `Brahms`
- `Jazz++`
- `TiMidity++`
- `playmidi`
- `xphat`

## 7 Linux 支持 MP3 (`/Chapter_7`)

- `BladeEnc`
- `mpg123`
- `XMMS`
- `Grip`

## 8 多轨道硬盘录制与混音 (`/Chapter_8`)

- `SLab`
- `Multitrack`
- `Mix`

## 9 软件声音合成 (`/Chapter_9`)

- `Midi2CS`
- `hydraJ`
- `Cecilia`
- `Silence`
- `HPKComposer`
- `Cmix`
- `RTcmix`
- `Sig++`
- `SAOL/sfront`

## 10 实时软件合成器 (`/Chapter_10`)

- `aRts`
- `RTSynth`
- `jMax`
- `Aube`

## 11 乐谱程序 (`/Chapter_11`)

- `Lilypond`
- `Rosegarden`
- `Muse`

## 12 网络音频软件 (`/Chapter_12`)

- `Icecast`
- `Speak Freely`
- `terminator`

## 13 Linux 与数字 DJ (`/Chapter_13`)

- `GDAM`
- `Greenbirth`
- `ClassX`

## 14 Linux 游戏 (`/Chapter_14`)

- `Muse`
- `Roll 'Em`

## 15 操作系统 (`/Chapter_15`)

- `Demu`
- `Executor`

光盘结构如下（目录名在括号内）：

## 音乐与声音页面

- `Brainstorm` 一种用于捕捉即兴表演的 MIDI 守护
- `Gramidity` 使用基于用户反馈的遗传算法以 MIDI 文件格式生成“音乐”；需要 JDK
- `Gseq` 一个 MIDI 排序项目
- `Melys` 针对 ALSA 的 MIDI 排序
- `MuseE` 基于 Qt 2.0 的 MIDI 排序
- `pmidi` 另一个针对 ALSA 的 MIDI 排序
- `Softwerk` 基于 Doepfer 模拟序列器的 MIDI 排序
- `Super Groove Master` 用于 AWE32/64、OPL3 FM 合成器或外部 MIDI 的独特作曲程序
- `WaoN` 一个 WAV 转 MIDI 转换器
- `Wav2MID` 另一个 WAV 转 MIDI 转换器

## 调音器

- `Smix` 一个高度可配置的调音器，使用 Xforms 作为 GUI
- `XAMixer` 一个基于 Gtk 的调音器，需要 ALSA
- `xmmixer` 带 Motif GUI 的声卡音频调音器

## 额外程序 (`/extra`)

- `Aglaophone` “用于实时音频录制、处理和播放的可连接模块系统”（来自 Aglaophone 作者网站）
- `ELE` “卓越延迟效果”
- `FFTW` (最快傅里叶变换) C 库
- `Mammut` 将整个音频文件作为单个分析
- `ObjectDSP` 用于 DSP 设计和实现的 X 窗口 GUI
- `Sculptor` 一套很好的实时工具集
- `TAPIIR` 带有 GUI 的多点延迟效果处理器
- `Ultra Power Effects Max` 用于全双工声卡的实时效果处理器

## 软件

- `Dr. Fermi Tabulator` 将 ASCII 谱转换为标准 MIDI 文件
- `eTktab` 一个编写互联网上典型的 ASCII 吉他谱谱的优秀程序
- `Funktracker` 一个 FNK 模块跟踪器
- `Gmodplay` Gtk MOD 播放器
- `Mod4X` 带有 Xforms 界面的 MikMod
- `SarahTracker` 一种正在开发中的控制模式跟踪器
- `Voodoo Tracker` 适用于 GNOME 桌面环境的全功能跟踪器
- `XMP` 扩展模块播放器

## MP3 软件

- `Freeamp` 一款开源 MP3 播放器
- `Kblade` BladeEnc 的 KDE 前端
- `kmp3te` 用于查看和编辑 MP3 文件标签的程序
- `Krio` 用于 Rio 播放器的 KDE 界面
- `LAME` 一种优秀的 MP3 编码器
- `mp3tools` ". . 一组用于处理 MPEG 音频文件的工具集（源自 mp3tools README）
- `Tk3Play` 带有 Tk GUI 的 MP3 播放器

## 多轨道录音器/混音器

- `ecasound` 从 Linux 终端或 X 窗口进行磁盘录音和音频处理
- `qnt` Rt 的 Qt 界面
- `Rt` Paul Lansky 著名混音器的移植

## 音乐人工具

- `Gtick` 带有 Gtk GUI 的节拍器
- `Solfege` 带有 Gtk 界界简谱练听训练程序

## 网络音频

- `EsounD` (Enlightened Sound Daemon) 也支持网络音频

## 乐谱软件

- `Denemo` Lilypond 的 Gtk 前端
- `Lilypond` GNU 项目的音乐排版软件；输出 TeX 和 MIDI

## 播放器与录音器

- `AlsaPlayer` “ . . 一种新型 PCM 播放器 . . 高多线程 . . 尝试测试 ALSA 库和驱动程序 . .”（来自 AlsaPlayer 网站）
- `krecord` 用于 KDE 的简单 WAV 录音器/播放器
- `xplay` 多格式（WAV, 未压缩 AIFF, Sun AU, NeXT SND）播放器，需要 Motif 或 Lesstif

## 编程工具

- audio latency software 用于分析在高系统负载下实时运行程序进行调度延迟的软件
- `audiofile` SGI libaudiofile 的实现
- `LADSPA` 有关 Linux 音频开发者简单插件架构的材料
- `libsndfile` 用于读取和写入许多不同声音文件格式的库
- `MIDSHARE` 一项开源 MIDI 库倡议
- `MuCos` 一个针对 Linux 音频的野心勃勃的 API
- Open Source Audio Library 处理音频 C++ 类
- OSS Programmer's Guide 针对 OSS/Linux 和 OSS/Free 音频及 MIDI 设备编程的优秀资源
- `SDL` (Simple DirectMedia Layer) 一个特别适合于开发和移植游戏的库项目
- `SNACK` 一个为 Tcl/Tk 添加声音 I/O 和可视化命令的模块
- `Sndlib/audiofile` 来自 Snd声音文件编辑器的库
- Sound Programming Tutorial 用于编程 OSS/Free, OSS/Linux 和 ALSA 的页面
- `tritonus` JavaSound API 的实现

## 示波器与可视化器

- `blurscope` 音频可视化实用程序
- `Bomb` 一个交互式 A-life “视觉音乐”仪器
- `Cuthgha` “一个迷幻的示波器 . .
- `eXtace` 超越的示波器/可视化器
- `oscope` 用于 SVGA 或 Gtk 的数字示波器
- `Synesthesia` 根据 FFT 和声立体定位信息计算的光秀

## 软件合成

- `cmusic` 将 CARL 音乐软件移植到 Linux
- `Common LISP Music` 来自 CCRMA 团队的 Music-N 风格语言
- `Common Music` 用于创建 Csound, Cmix, Common LISP Music 以及其他 Music-N 风格语言乐谱的实用工具
- `gAlan` 一种图形符号音频语言
- `Pd` 一种类似 MAX 的符号音频/MIDI 编程环境
- `STK` (Synthesis Tool Kit) “一组音频信号处理 C++ 类和乐器”（来自 STK 网站）
- `Tao` 带有 Mesa/OpenGL GUI 的物理建模合成语言
- `Xsynth` MIDI 控制的模拟风格实时合成器

## 声音文件编辑器

- `Electric Ears` 适用于 Gnome 桌面的声音文件编辑器项目
- `Smurf Editor` 用于 AWE32/64 声色的编辑器
- `Studio` 优秀的编辑器，需要 Tcl/Tk
- `TAON` 带有 Gtk GUI 的声音文件编辑器
- `WaveSurfer` Tcl/Tk 声音文件编辑器，需要 SNACK 扩展
- `WaveTools` 一组用于处理 WAV 格式声音文件的小型命令行程序

## 语音软件

- `Festival` 语音合成系统
- `MBROLA` 控制模式语音合成系统
- `OGI` 用于语音数据操纵的语音工具，包括 X 界面、文件转换工具和 LPC 工具
- `SFS` (语音文件系统) 一组优秀的基于 X 和命令行的工具
- `Transcriber` "一个用于语音分段、标记和转录的免费工具”（来自 Transcriber 网站）；需要 Snack 软件包

## 音频示例

此目录包含书中引用的声音文件。
