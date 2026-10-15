
要做到这一点，焊掉旧电缆，连接部分将留在后板上。某些电缆胶在机箱上，但稍加小心即可轻松重新连接。你需要一个针间距为 0.5mm 的 `FFC/FPC` 10 脚适配器。适配器上有 10 根扁平线。将重新连接的线连接到背部的插座。适配器带有原始 `Sonos` 电缆。对于转换过程中所有电缆的长度，使用机箱外的宽度，因此非常容易进行测试和修正。使用万用表测量哪根线提供哪种功能。`Sonos` 电缆左侧有小保险丝，然后将所有部分重新装好。建议使用直径大于 1mm 的硬芯铜线，保持平直。如果你使用的是没有提供这些导线的 `FPC` 适配器，`Symfony`，由于需要处理 230V（欧盟、澳洲）或 120V（北美），你可能需要再次拆解树莓派。扩展部分可以用利刀小心地去除。

## 修改电源

电源单元（明纬华 `HDR-60-15`）非常紧凑（且同时支持 230V 和 120V），因此非常适合转换。`Symfonisk` 似乎没有更改分配。播放/暂停使用一个 4 欧姆中音驱动器和一个 8 欧姆高音器。（另见“外部电源”。）

`HiFiBerry` 建议为他们的 `Amp2` 树莓派功率放大器使用 18V 60W 3A 的电源。`HDR-15` 是 15V 电源单元，但具有高达 18V 的调节输出。为了简化你的工作，请使用表 2 中的信息映射电线。极性并不重要，因为它使用的是交流电。

外壳插座的焊点应用热缩胶管或热熔胶进行绝缘。接下来，将适配器电源的一个输出端连接到 `Amp2` 的输入端。如所述，这样你可以立即为树莓派供电。

## 重新布线

适配器根据表 2 中的映射将开关线焊接到 `Amp2` 引脚上，这些线的选择是正确的。总而言之，你只需要一根线以防干扰 `Amp2` 功能。你需要焊接并注意极性（即以正确的方式连接正负极），且不要使用连接器；否则，扬声器的震动可能会导致连接松动。由于引脚非常非常近，建议用热缩管对单个焊接引脚进行绝缘。

现在使用原始 `Sonos` 电缆连接扬声器。你可以只需拔掉 `Sonos` 扬声器主板的连接器。连接时，必须观察极性：`Sonos` 电缆在较大的插头上为正极。将每个扬声器连接到立体……

## 表 2：Sonos 面板映射

| 适配器 | 功能 | 树莓派 Header 引脚 | GPIO 编号 |
| :--- | :--- | :--- | :--- |
| + 1 | 播放/暂停 | 23 | 11 |
| + 2 | 播放/暂停 | 23 | 11 |
| + 3 | 绿色 LED | 16 | 23 |
| + 4 | 红色 LED | 18 | 24 |
| + 5 | GND | 20 | 20 |
| + 6 | 黄色 LED | 22 | 25 |
| + 7 | GND | 20 | 20 |
| + 8 | 白色 LED | 15 | 22 |
| + 9 | + | 21 | 9 |
| + 10 | - | 19 | 1 |

`LINUX-MAGAZINE.COM` | `LINUXPROMAGAZINE.COM`

第 239 期

2020年10月

67

![](img/4124af05f4c60b6759782ba44bc7f_453_0.png)

## MAKERSPACE Raspberry Pi Symfonisk

写入 SD 卡 `[10]`，就像处理其他 Pi 操作系统一样。要设置 WiFi，在 `PCBBOOT` 分区创建 `wpa_supplicant.conf` 文件并在其中输入登录信息。可以参考 `wpa_supplicant.conf.sample` 文件 `[11]`。

现在手动将下载的插件拷贝到内存卡。要做到这一点，将 `rt-plugins-0.0.6.tcz` 和 `rt-plugins-0.0.6.md5` 文件写入 `PCP_ROOT` 分区的 `tce/optional` 文件夹中。为了让系统在启动时加载插件，你需要在 `tce/onboot.lst` 文件中输入其文件名（`rt-plugins-0.0.6.tcz`）（见图 4）。你可能需要以管理员权限启动文件管理器和编辑器来完成。

此外，你可能希望扩大 `PCP_ROOT` 分区以使用整个内存；这样你就可以消除了构建交叉网络的需求，以后可以通过软件数字地完成。

或者，你也可以首次启动 `piCorePlayer` 后这样做，但在你把组件装回外壳之前，需要将所需的插件拷贝到 SD 卡中。1GB 容量的内存卡即可。

为了搭建 Raspberry Pi 系统并通过 `Amp2` 的两个立体声通道访问各个扬声器驱动，你需要插件。这些插件对某些频率进行过滤工作，以便播放器将高频路由到高音器，并将低频路由到中音驱动器。

## 首次启动

现在从卡槽取出 SD 卡并启动系统。启动 Raspberry Pi 后，可以通过 Web 界面（图 5）访问 `piCorePlayer` 以使用 `SlimServer` `[5]`（以前称为 `Logitech Media Server`），因为该软件最初设置起来最简单。我选择了 Richard Taylor `[8]` 编写的 Linux 音频开发者插件 API (`LADSPA`) 插件。你可以通过 WiFi 路由器的网页前端或使用 `arp-scan` 发现 IP 地址：

```bash
sudo arp-scan --localnet | grep Raspberry
```

再次，重点是免费（即开源）软件。此外，你可能希望有一个中心化服务器，配合简单的客户端作为播放设备，并实现多房间和扬声器同步。由于 `tinycore` 在启动时将所有内容加载到内存中；系统由不同的端口、通过插件实现的扩展性（例如为互联网电台设置了许多扩展）以及当然支持包含流媒体服务 ZIP 包组成。所有加载的扩展都会合并到系统每次运行时内存中的一个文件系统中。`SlimServer` 的大部分组件提供了大部分功能。其中某些所需功能已经预包并可以作为扩展下载；然而，我使用了安装在 NAS 系统 Docker 容器中的服务器。服务器本身非常容易设置；你可以在网上找到大量的说明和教程 `[6]`。

首先，切换到底部的高级模式（Advanced Mode）。然后执行以下操作：

- 在 `Main Page | Full Update` 下更新本项目使用的 `piCorePlayer` 。扬声器可以选择作为 `SlimServer` 运行，但要这样做，你需要配置该功能。
- 在 `Main Page / Update` 下更新扩展，虽然完成很快，但它需要正在运行的播放器或交叉连接（参见“首次启动”部分）。
- 在 `Main Page / HotFix` 下检查可能的热补程序。你会在下载区域找到一个我自己构建的版本。

我将不会介绍服务器的设置，而是介绍扬声器的设置。

其次，进入 `Squeezelite Settings` 标签页并将 `Amp2` 设置为音频输出设备，它显示为 `HiFiBerry DAC+`（以及 Pro, AMP2）。重启后，

对于扬声器，我决定使用 `piCorePlayer` `[7]`。该软件设置简单，易于扩展并运行在 Raspberry Pi 上。首先下载当前 `piCorePlayer` 的镜像并将镜像写入 SD 卡。现在拨动卡槽控制开关以禁用 Raspberry Pi 的内部声卡。

## 2020 年 10 月

## 第 239 期

## LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM

## piCorePlayer

## SQUEEZE 音频设备

CorePlayer 主要功能

- Squeeze 正在运行
- 使用新设置重启 Squeeze
- 更新 Squeeze 扩展
- 为 Squeeze 安装 MP3 库
- 进入蓝牙页面
- 重新加载 CorePlayer
- 进入诊断页面
- 停止 Squeeze

附加功能

- 停止 Squeeze

## Rasp Pi Symfonisk MAKERSPACE

扬声器控制台。为此，通过 SSH 连接到扬声器的 IP 地址。默认情况下，系统使用 `tc` 作为用户，`piCore`（大小敏感）作为密码。

对于分频器（即高音和低音滤波器），你必须如列表 1 所示编辑 `/etc/asound.conf` 文件。系统自带的编辑器是旧版的 Vi，虽然性能出色，但并不完全直观。初学者可以在旧的 Linux Magazine 文章 `[12]` 中学习最重要的命令。

这里显示的配置创建了一个过滤器链，该链通过均衡器和分频器发送到硬件。`pcm.!default` 中的条目将默认设备重定向到 `plqual` 均衡器。你将在下方找到 `pcm.plugequal` 和 `pcm.equal` 中的均衡器设置。

`pcm.crossover` 部分集成了 Richard Taylor 开发的插件，这些插件将立体声信号分为四个通道：两个 3000Hz 以上的通道（左和右）和两个 3000Hz 以下的通道。

图 4：你必须手动将为 `piCorePlayer` 构建的插件复制到 `PCP_ROOT` 分区的 `/etc/optional/` 目录下。

系统随后将这四个通道混合为两个单声道通道，一个在 3000Hz 以上，一个在 3000Hz 以下。系统随后将这些分配给高音器和中音驱动器。3000Hz 的限制纯粹是经验选择——精确的规格也会影响整体音质。

## 设置均衡器

要调整声音，请使用集成的均衡器。要配置它，通过 SSH 连接到扬声器。接下来，输入 `alsixer` 启动混合器，并使用左右方向键选择频率范围，按 Esc 退出。

你现在已完成基础配置。扬声器应该可以工作了。然而，它听起来仍然有些奇怪。正确的设置部分取决于扬声器的位置。然而，重要的是，少即是多。

## 配置驱动程序

对于以下设置，在 `Squeezelite Settings` 标签页中输入扬声器的名称（例如 Room）和媒体服务器的 IP 地址。最后，开启 ALSA 均衡器。

列表 1：调整 asound.conf

```conf
## 由 piCorePlayer 生成
.!default {
    type plug
    input.bindings.1 "Input"
    output.bindings.3 "Output"
    slave.pcm "plugequal"
}

2 {
    type hw
    card 0
    input.bindings.0 "Input"
    output.bindings.4 "Output"
    slave.pcm "hw:1,0"
}

3 {
    type hw
    card 1
    input.bindings.1 "Input"
    output.bindings.5 "Output"
    slave.pcm "plug:crossover";
}

4 {
    type equal;
    input.bindings.1 "Input"
    output.bindings.3 "Output"
    library "/usr/local/lib/ladspa/caps.so"
    controls { 3000 }
}

5 {
    type equal;
    input.bindings.1 "Input"
    output.bindings.5 "Output"
    library "/usr/local/lib/ladspa/caps.so"
    controls { 3000 }
}
```

```text
78 slave {
31 pcm.equal {
79 pcm "t-table"
32 type plug;
80 channels 6
33 slave.pcm pluequal;
81 rate "unchanged"
34
}
35
82 }
36
#---扬声器分频连接-----
83 }
37 pcm.crossover {
38 type ladspa
85 pcm.t-table {
39 slave.pcm "amp2"
40 type route
40 path "/usr/local/lib/ladspa"
87 slave {
41 channels 6
88 pcm "hw:0,0"
89 plugins
90 channels 2
43 {
94 }
94 0{
45 ttable {
46 lel RTlr4lowpass # 低通滤波器输出左开启
91 channel 2
92 2.0 0.5 # 将立体声低信号混合为单声道（中频） 46 policy none
93 3.0 0.5
47 input.bindings.0 "Input"
94 4.1 0.5 # 将立体声高信号混合为单声道（高音器） 48 output.bindings.2 "Output"
95 5.1 0.5
49 input { controls [ 3000 ] }
96
}
50
97
}
51 1 {
98
52 label RTlr4lowpass # 低通滤波器输出右开启
97 channel 3
97
pcm.plughw.slave.rate = "unchanged";

70
2020年10月
第 239期
LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM

![](img/4124af05f4c60b6759782ba44ba4bc7f_475_0.png)

Rasp Pi Symfonisk MAKERSPACE

在扩展中，位于 setup 下列出的当前扩展仍没有功能。不过，如果你愿意，可以对系统进行编程，使状态 LED 信号指示网络连接。条 `pcp-sbpd.tc`。

现在脚本需要在播放器启动时自动运行。要实现这一点，在网络界面的 Tweaks 选项卡下，输入 `/home/tc/sbpd-script.sh` 命令作为 User command #1。最后...

图 6：我自己的均衡器设置在入口处清晰可见，并且

点击 Info 可以获取有关该包的更多详细信息。在 Main Page 选项卡的底部，选择 Save and Backup。宜家扬声器提供的低音点击 Load 设置扬声器内。仍然很单薄。

停止并激活

现在你可以从 Slim-Server 播放音乐并检查按钮的功能。宜家扬声器薄弱的低音无法通过均衡器解决。最重要的是，你可能想测试驱动器连接。如果电缆通过 SSH 工作正常，请使用 Vi 创建 `/home/tc/sbpd-script.sh` 文件，内容如列表 2 所示。在最后的 sbpd 组装和设置扬声器。

在混合后，你可以再次调整均衡器，否则你只会从高音器中听到非常微弱的音乐。记住。

随着现在共鸣腔的关闭，在角括号内的 IP 地址处小心处理组件，而扬声器的声音将不同。SlimServer 之后 -A 和连接到市电端口。

因为 `piCorePlayer` 完全运行在 Rasp Pi 的内存中，任何保留的角括号。理论上，

## 最终组装

你在操作期间所做的更改你可以省略这些信息，并在断开连接时设置为自动扬声器搜索，但唯一剩下的工作是将所有内容安装到外壳中。（在我的设置中不起作用。（拔掉！）因为启动系统。因此，你应该。

保存文件后，将脚本明确设为可执行，它有相当大的空间，此任务没有任何问题。第一要工作是将电源插座固定在背板上，并将 USB 和 SD 卡连接器的插座胶上（图 7）。接下来，将支撑柱螺在 Rasp Pi 上以补偿外壳的台阶（图 8）。

## 前面板按钮

要使用前面板上的按钮，按照原始定义的这些，这些是 GPIO 9、10 和 11（表 2）。如果你更改了组件，它们是完整的。我使用热熔胶固定了 `piCorePlayer`，这在“Rewired”部分中，你需要根据此调整 GPIO。如有必要，稍后可以小心地安装-释放。该-可以简单地从 Main Page 选项卡拆下；然后，点击 Ext-条目。访问 Available extensions 空间进行维护。

如果你想使用更多功能，登录浏览器并进入。这里。如果你想避免震动引起的背景噪声——系统需要互联网操作，你可以将电缆胶住以通过 `sbpd-help` 调用完整引用。然后你可以，例如，为了此步骤。

处理长按按钮。LED 在外壳侧。

最后，但同样重要的是，连接扬声器和控制面板并重新安装扬声器前部。提醒一下，声罩应该位于 Rasp Pi 之上。

## 列表 2：sbpd-script.sh

```bash
#!/bin/sh

## 启动 pigpiod 进程

sudo pigpiod -t 0

## 等待 1 秒让进程启动

sleep 1

## 加载 uinput 模块，然后调整权限以非权限用户运行 sbpd

sudo modprobe uinput

sudo chmod +x /dev/uinput

## 运行 sbpd
```
