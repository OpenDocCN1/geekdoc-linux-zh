
如果使用以太网端口将树莓派连接到互联网，你可以从新创建的 SD 卡启动树莓派。但是，如果使用无线网卡，你需要编辑发行版的配置文件并手动指向你的无线路由器。从普通发行版访问新创建的 SD 卡，导航到 `config` 文件夹并在文本编辑器中打开 `settings.ini` 文件。在文件顶部附近你会注意到两个变量，`WIFI_NETWORK` 和 `WIFI_PASSWORD`。在这两个变量旁边插入你网络的对应值并保存文件。需要注意的是，PiMusicBox 仅适用于受 WPA2 保护的无线网络。

完成这些后，使用配置好的 SD 卡启动树莓派。首次启动时，发行版会调整文件系统大小以占用整张卡，并自动重启。如果你将显示器连接到树莓派，可以跟随启动过程，否则等待一两分钟，然后在网络上任何计算机上启动浏览器并访问 `http://musicbox.local`。如果这不起作用，请将浏览器指向树莓派的 IP 地址。

Pi MusicBox 的默认界面相当单调，因为你尚未配置任何音乐源。要解决这个问题，点击左侧导航栏中的 `Setting` 链接。这会带你到一个页面，你可以在此单独启用和配置所有支持的流媒体服务，从 Spotify 和 Google Music 等付费服务到 The Internet Archive、Soma FM 等免费服务。你也可以从此页面控制其他设置。例如，`Audio` 设置让你可以切换音频输出设备。

Pi MusicBox 发行版具有可用的 Samba 配置，应该会在所有操作系统的文件管理器中的 Network 部分显示。发行版的 Samba 共享只有一个名为 `Music` 的文件夹。你可以将任何音频文件放入此文件夹，它们将被传输到 SD 卡。

每当你重启树莓派时，发行版会在启动时扫描任何新音乐。然后你就可以从发行版的 Web 界面浏览和播放这些文件。

你也可以通过任何支持 Music Player Daemon (`MPD`) 的软件播放音乐，例如 Android 上的 `MPDroid` 应用。要连接，启动该应用并在首次运行向导中，在主机名字段输入树莓派的 IP 地址。

## Hack #6: Broadcast audio

将音乐流式传输到树莓派是一回事。如果想将音乐流式传输到其他设备呢？顺便说一下，如何运营自己的电台？事实上，你可以毫不费力地做到这一点。

除了树莓派上熟悉的 Audio、以太网、HDMI 和 USB 端口外，该设备还具有旨在更直接地与其他芯片和模块连接的接口。这些通用输入/输出 (`GPIO`) 端口是排列成两条平行条带上的引脚（Model B 板上有 26 个，B+ 上有 40 个）。

这些接口不是即插即用，但可以通过软件控制。Code Club 的一群黑客编写了一个程序，使用原本用于生成扩展频谱时钟信号的引脚来输出 FM 广播信号。要传输一个相当强的 FM 信号，你只需将一根导线连接到 `GPIO 4` 引脚。即使没有导线，树莓派广播的 FM 信号也会被附近的 FM 接收器接收到。

给树莓派通电并打开终端。现在从 Code Club 获取代码并使用 `wget` 解压：`http://comatos.com/pifm.tar.gz`

```
mkdir ~/pifm
tar zxvf pifm.tar.gz -C ~/pifm
```

`tarball` 解压出六个文件。令人惊讶的是，这就是全部。你现在可以用 `sudo ./pifm sound.wav 101.2` 广播包含的 `sound.wav` 文件。现在拿一个 FM 接收器并调到 FM 101.2，你就会听到星球大战主题曲。你实际上可以通过在命令末尾附加频道频率，将广播频率从 88 MHz 到 108 MHz 之间更改。

你也可以播放其他音频文件，但它们必须是 16 位 22,050Hz 单声道且仅为 WAV 格式。那

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_41_0.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_41_1.png)

> Pi MusicBox 基于用 Python 编写的 Mopidy 音乐服务器。

似乎像是一个限制，但实际上并非如此，多亏了出色的 SoX sound exchange 音频编辑器。我们将使用这个巧妙的小工具来处理任何 MP3 文件，无论其编码如何，并即时将其转换为正确的 WAV 文件。

首先使用 `sudo apt-get install sox libsox-fmt-all` 安装音频编辑器及其依赖项。完成后，输入以下命令，将 `"SomeSong.mp3"` 替换为你希望播放的 MP3 文件的名称：

```
sox -t mp3 SomeSong.mp3 -t wav -r 22050 -c 1 - | sudo /pfm - 101.2.
```

命令的第一部分将 MP3 文件转换为 WAV 文件，将其音频采样率更改为 22050 Hz 并将音轨混音为单声道。转换后的音轨随后发送到标准输出，用连字符表示，然后通过管道（`|`）传输到 `pfm` 命令的标准输入。

与上述示例中 `pfm` 命令的唯一区别是，我们没有指定要广播的文件名，而是要求脚本广播标准输入。如果你仍将 FM 收音机调至 101.2 频率，你现在应该能听到你的 MP3。

你可以用 SoX 做一些很棒的事情。例如，你可以用它来实时广播你最喜欢的互联网流媒体。命令 `sox -t mp3 http://www.tuxradar.com/files/podcast/tuxradar_506e02.mp3 -t wav -r 22050 -c 1 | sudo /pfm - 101.2` 将广播 TuxRadar 播客。与前一个示例的唯一区别是，你现在指向的是在线的 MP3，而不是本地的 MP3。

脚本将下载缺失的依赖项，然后显示一个包含几个选项的菜单。

第一个选项下载并安装所有流行支持平台的预编译二进制文件。第二个选项获取每个应用的最新源代码并在 Pi 上编译它们。如果你选择此选项，请做好等待的准备，因为这可能需要几乎一整天的时间。如果你的耐心不足，不妨直接获取映像文件并使用 `dd` 将其传输到空白 SD 卡上。

RetroPie 使用名为 `EmulationStation` 的图形前端，允许你管理各种已安装的模拟器。RetroPie 映像会自动启动此前端，但如果你在现有的 Raspbian 安装之上设置了 RetroPie，你将必须手动使用 `emulationstation` 命令启动它。

启动后你应该会看到控制器设置屏幕，在此你可以配置你的 USB 游戏控制器。当然，要玩游戏，你必须先拥有它们。ROM 可以从你自己的这些老游戏副本制作，也可以在线找到 abandonware。一些公司，例如 id Software，已将原始的 Doom 开源并置于公共领域。获取后，你需要将它们复制到 SD 卡上 `roms/` 文件夹内相应的模拟器子文件夹中。

## Hack #7: 模拟复古游戏

游戏并不总是图形杰作。开发人员可用的资源更少，而非图形卓越，开发人员依靠游戏玩法来吸引玩家。这就是为什么即使画面简陋，复古游戏至今仍深受各年龄段玩家喜爱的原因——在 Steam 或 Live 上也找不到经典游戏挑战的独特体验。

在 Raspberry Pi 上开始玩复古游戏的最简单方法是安装 RetroPie，它打包了一系列模拟器。你可以在现有的 Raspbian 安装上安装 RetroPie，也可以将其作为独立发行版运行。在获取安装脚本之前，先使用 `sudo apt-get install git dialog` 获取其依赖项。然后你可以使用以下命令下载最新的 RetroPie 设置脚本：

```
git clone git://github.com/petrockblog/RetroPie-Setup.git
```

现在进入克隆的目录并使用 `cd RetroPie-Setup && sudo ./retropie_setup.sh` 运行脚本

> “当然，要玩模拟游戏，你必须先拥有它们…”

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_42_0.png)

`EmulationStation` 只会显示已添加 ROM 的模拟器。

## 捐赠多余资源

如果你并非始终使用 Pi，你可以为有价值的事业捐赠闲置的处理能力。BOINC 是一个计算志愿服务，它使用捐赠的算力用于各种项目，从医学科学的蛋白质折叠到寻找外星智能。

在安装 BOINC 之前，通过调用 `sudo raspi-config` 调整 Raspberry Pi 以减少其自身资源利用率。前往 `Advanced Options > Memory Split` 并为 GPU 预留尽可能少的内存，你会发现为 16MB。然后使用 `sudo apt-get install boinc-manager boinc-client` 安装 BOINC

完成后，从 Others 菜单启动 BOINC Manager。你将被要求从 30 多个受支持项目中添加一个。一些项目可能会警告你它们可能没有适合 Pi 的工作。虽然你仍可以添加它们，但最好添加可以利用 Pi 的项目，例如 Collatz 项目，它正试图反驳 Collatz 猜想。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_42_1.png)
