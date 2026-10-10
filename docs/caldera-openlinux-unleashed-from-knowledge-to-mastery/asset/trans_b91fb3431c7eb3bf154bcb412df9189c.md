

戴夫经常接到询问“声卡 X”是否能在 OSS 下运行的电话。由于 PC 平台上有许多品牌的声卡，戴夫建议你只需试用评估版本，以判断你的特定品牌声卡是否受支持。OSS 拥有非常出色的自动检测例程，几乎可以识别任何类型的兼容声卡。

戴夫和我还聊到了 OSS 即将支持的 SoundBlaster Live! 系列声卡。他说，截至本书写作时，SoundBlaster Live! 的驱动程序因创新科技（Creative Labs）缺乏合作而停滞不前。他解释说，创新科技有经济动机使其硬件规格保密——将它们公开会让竞争对手生产 SoundBlaster Live! 兼容芯片组或声卡变得相对容易。创新科技希望避免像 SoundBlaster Pro 那样发生的事情，当时硬件规格的发布导致了数百款第三方 SoundBlaster Pro 兼容声卡和芯片的出现。通过将 Live! 声卡的硬件规格公开，创新科技还有失去对其专有 EAX 环境音频扩展控制的风险。这是一个不幸的局面，可能会阻碍 SoundBlaster Live! 系列声卡在 Linux 市场的普及。直到这一情况改变，除非你已经购买了 SoundBlaster Live! 声卡，否则你可能想避免购买它。创新科技已经开始了 Linux 下 Live! 系列驱动程序的开发，但此时它与广泛的内核不兼容，且有些不稳定。你可能想访问 http://www.soundblaster.com 查看这种情况是否有所改善。

## 配置 SoftOSS

SoftOSS 需要一些配置才能正常工作。此过程中最难的部分是下载并安装 Eric A. Welsh 优秀的免费补丁（乐器样本）。这在本章后面的 MIDI 软件合成部分中有详细说明。要使 SoftOSS 正常工作，你只需在安装 EAW 补丁后，将以下行添加到你的 `/etc/profile` 文件中：

```
export GUSPATHDIR=<directory to patches>
```

记住这一步；没有它，OSS 自带的播放程序将无法找到其需要的补丁。有关完整说明，请参阅本章后面关于“为 TiMidity++ 和 OSS 安装补丁文件”的部分。

## ALSA——高级 Linux 声音架构

Linux 下声音支持的第三个也是最有趣的选项是 ALSA，即高级 Linux 声音架构。它计划最终替代当前随内核源代码一起分发的 OSS/Freetext 衍生驱动程序。ALSA 提供了一个高性能、完全模块化的声音系统，支持一些优秀的声卡。要安装 ALSA，你必须下载、编译、安装并配置最新的三个源代码存档，这些存档可从 ALSA 项目网站获取。如果你的声卡受 ALSA 支持（大多数流行声卡都是），那么付出一点努力是值得的，因为它为你的 Linux 机器提供了下一代声音架构。举个例子，使用标准内核驱动程序，我的 SoundBlaster PCI128 在同时使用 TiMidity++ 播放 MIDI 文件并浏览网页时，音频播放会出现卡顿。而使用 ALSA 时，声音播放几乎完美无缺。

ALSA 项目始于替换 Gravis UltraSound 系列声卡的内核声音驱动的目标，最终发展成为一个完整的高性能声音系统。它提供了一个改进的 API 来访问声音硬件，同时为尚未具有原生 ALSA 支持的应用程序提供了完整的 OSS 兼容性模块。ALSA 目前支持以下声音硬件：

- Trident 4D Wave DX/NX
- Gravis UltraSound PhP, Extreme, Classic/ACE, MAX
- Gravis 兼容设备（Dynasonic 3-D, STD Sound Rage 32, STB UltraSound 32-Pro）
- SoundBlaster, Pro, 16, AWE32, AWE64, PCI64, PCI128
- Ensoniq AudioPCI (ES1370/1371)
- ESS AudioDrive ESx688
- ESS ES18xx（存在一些问题）
- ESS Solo-1 ES1938
- Yamaha OPL3-SA2, OPL3-SA3
- OAK Mozart
- PINE Schubert 32 PCI
- S3 SonicVibes PCI

如果 ALSA 与你的声卡兼容，我鼓励你尝试一下。使用 ALSA 将使你在 Linux 声音功能的最前沿，并为你提供目前可用的高性能和最先进的 Linux 声音支持。

### 安装 ALSA

安装 ALSA 的第一步是访问位于 http://www.alsa-project.org 的 ALSA 项目网站。你必须下载三个源代码存档：alsa-driver、alsa-lib 和 alsa-utils 的最新版本。编译相当简单。我们将在此快速回顾一下流程。

首先将 alsa-driver 解压缩到一个临时目录。进入 alsa-driver 目录后，输入：

```sh
./configure --help
```

这将为你提供 ALSA 驱动程序的编译选项列表。你将感兴趣的选项包括（来自 alsa-driver-0.3.2）：

| 选项 | 描述 |
|:-------|:-------------|
| `--with-debug=level` | 指定调试级别（none, basic, memory, full） |
| `--with-processor=cpu` | 指定处理器类型（i386, i486, i586, i686, alphas, ppc, mips, auto） |
| `--with-smp=yes,no,auto` | 驱动程序将（不）编译 SMP 支持 |
| `--with-isapnp=yes,no,auto` | 驱动程序将（不）编译 ISA PnP 支持 |
| `--with-sequence=yes,no` | 驱动程序将（不）编译序列器支持 |
| `--with-oss=no,yes` | 驱动程序将（不）编译 OSS/Lite 模拟 |
| `--with-cards=<list>` | 为 `<list>` 中的声卡编译驱动程序（声卡可以用逗号分隔。all 编译所有驱动程序） |

只需将适当的参数传递给 configure 脚本，源代码存档就会配置好以便构建。我建议使用以下选项：

```sh
./configure --with-debug=none --with-processor=<your> --with-sequencer=yes \
--with-oss=yes --with-cards=all
```

配置应该会成功完成。现在你可以准备编译驱动程序了。执行以下命令：

```sh
make
```

之后，输入：

```sh
make install
```

驱动程序现在已安装。你应该对 alsa-lib 和 alsa-utils 重复此过程，只不过你不需要向 configure 脚本传递任何配置参数。不带任何选项运行 configure 脚本即可正常工作。完成这些后，运行 make 和 make install；所有正确的二进制文件和库随后将安装在你的系统上。

### 测试 ALSA

ALSA 高度模块化化；如果在安装 alsa-driver 后查看你的 `/lib/modules/<kernel>/misc` 目录，你会发现这一点。使用 ALSA 时，通常会加载大约 10 个独立的模块，每个提供特定功能，例如直接与硬件接口、序列处理、计时、混音、播放数字音频流等。因此，我们将大量使用 modprobe 二进制文件，它将加载我们想要的模块，以及我们感兴趣的模块所依赖的任何模块。这使得我们的生活轻松了许多——modprobe 处理繁重的工作。为了加载 ALSA，我们必须输入：

```sh
modprobe <module_name>
```

并使用适合你特定硬件的名称。查看下表以找到适合你特定硬件的模块。

| 模块名称 | 声卡/芯片组 |
| :--- | :--- |
| snd-audiodrivers | ESS AudioDrive 1688 and ES-688 |
| snd-audiodrivers18x | ESS AudioDrive 18xx |
| snd-gusclassic | Gravis UltraSound Classic |
| snd-gusextreme | Gravis UltraSound Extreme |
| snd-gusmax | Gravis UltraSound MAX |
| snd-interwave | Gravis UltraSound PnP, STB Sound Rage & more |
| snd-interwave-stb | STB UltraSound 32 Pro |
| snd-sb8 | SoundBlaster 1.0, 2.0, Pro |
| snd-sb16 | SoundBlaster 16（加上 PnP） |
| snd-sbawe | SoundBlaster AWE32, AWE64（加上 PnP） |
| snd-opl3sa | Yamaha OPL3-SA2/SA3 |
| snd-mozart | OAK Mozart |
| snd-opti9xx | OPTi 82C9xx |
| snd-sonicvibes | S3 SonicVibes PCI (PINE Schubert 32 PCI) |
| snd-audiopci1370 | Ensoniq AudioPCI, SoundBlaster PCI 64/128 |
| snd-audiopci1371 | 同上，较新的芯片组（其中一个有效） |
| snd-card-ad1848 | AD1848/AD1847/CS4248 |
| snd-card-cs4231 | CS4231 |

