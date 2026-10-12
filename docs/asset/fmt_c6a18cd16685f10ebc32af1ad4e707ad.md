
## 通过 GUI 通过 `.deb` 安装 Upscail

- 导航至发布页面：`https://github.com/upscail/upscail/releases`
- 点击最新的 `upscail-linux.deb` 下载 Upscail
- 进入 `~/Downloads`
- 双击 `upscay-2.10.0-linux.deb`
- 点击安装

## Stable Diffusion Web UI

访问 Stable Diffusion Web UI 官方网站 `https://github.com/AUTOMATIC1111/stable-diffusion-webui` 获取所有关于 Stable Diffusion Web UI 的信息。

### 通过 GUI 通过 `.sh` 安装 Stable Diffusion Web UI

- 导航至发布页面 `https://github.com/AUTOMATIC1111/stable-diffusion-webui/releases`
- 点击最新的 `Source code (zip)` 下载最新的 Stable Diffusion Web UI
- 进入 `~/Downloads`
- 双击 `stable-diffusion-webui-1.8.0.zip`
- 选择 `stable-diffusion-webui-1.8.`
- 点击 `Extract`

## XanMod

`XanMod` 是一种自定义的 Linux 内核发行版，旨在通过高级功能和优化来增强系统性能和稳定性。由于其提供了针对超低延迟需求的实时版本，它是游戏、流媒体和直播制作等对实时性能要求的应用的理想选择。`XanMod` 支持 64 位 Debian 系发行版，包含了核心进程、调度和内存管理的优化，以及高 I/O 吞吐和 `debuginfo` 增强。它集成了第三方补丁，包括内存保护、`AMD P-state` 驱动程序和 `Google` 的 `TCP` 拥塞控制，以高效处理密集负载。`XanMod` 以 `GPLv2` 许可证发布，使用最新的 `GCC` 构建，与 `Debian` 或 `Ubuntu` 发行版具有良好的兼容性，承诺提供稳定且响应的计算体验。

## Liquorix

`Liquorix` 是一种专门设计的 Linux 内核，旨在为交互式系统提供极致的响应。它在需要低延迟的环境（如音视频制作和游戏）中表现出色，通过优化减少帧时间偏差。关键特性包括 `Zen` 交互调优，它将系统响应性置于吞吐量和功耗之上，并对块层调度、虚拟内存、`CPU` 调度和 `CPU` 频率设置进行调整以增强性能。通过 `PDS/BMQ` 调度器实现公平的进程分布，并在 `1000hz` 频率进行高分辨率调度，`Liquorix` 确保了精确的任务管理。它包含了带有 `TCP BBR2` 的高级拥塞控制、使用 `LZ4` 的压缩交换（`swap`）以及用于更好地处理内存压力的多代 `LRU`。`Liquorix` 提供 `Debian` 和 `Ubuntu` 的二进制构建版本，可作为即插用的内核替换方案，提供广泛的硬件支持和半虚拟化选项，以最大地减少虚拟化环境中的开销。

## Linux Mint 系统变量

Linux Mint 系统变量（也称为环境变量）是用于存储信息和控制命令行应用程序及系统操作行为的动态值。这些变量由一个名称和一个值组成，格式为 `` `KEY=value` ``，等号两边不能有空格。包含空格的值必须括在引号中，并可以使用冒号（`:`）作为分隔符分配多个值。变量名区分大小写，且习惯上使用大写字母。环境变量是全局可访问的并会被子进程继承，而 Shell 变量仅限于当前的 Shell 实例。它们为自定义 Linux Mint 的系统和应用程序行为提供了一个多功能的工具。

## 在 Cinnamon 桌面中将图像设置为背景

在 Cinnamon 桌面中将图像设置为背景允许您通过选择任何图像或颜色来个性化桌面。只需在桌面上点击右键，选择“更改桌面背景”，并通过“桌面背景偏好”对话框添加新壁纸。您还可以调整其外观以适应或填充屏幕。对于纯色，选择“无壁纸”并选取一种颜色。更改是即时的，对于系统级设置，管理员可以使用 `dconf` 设置默认值、锁定配置，甚至为所有用户添加额外的背景，确保跨设备的统一视觉效果或品牌形象。

## Mount_options.conf

`Mount_options.conf` 是 `UDisks` 的功能，专为系统管理员定制，允许自定义各种文件系统的挂载选项，确保安全和数据一致性。该功能引入于 `UDisks 2.9.0`，允许通过配置文件或 `udev` 规则进行系统级覆盖，专门针对可移动介质等动态挂载点，在不损害系统的情况下优先考虑安全可靠的。它区分了文件系统类型和驱动程序，完善了对数据的控制。这种设置防止了未经授权的访问和数据丢失，是安全高效处理存储的关键工具。

## 在 Linux Mint 的 Cinnamon 桌面中管理启动应用程序

在 Linux Mint 的 Cinnamon 桌面中，“启动应用程序”允许您管理启动时运行的程序。按下 `Super` 键进行搜索，并调整您的启动过程以提高效率。请谨慎禁用默认程序——它们至关重要。可以轻松添加新应用或调整现有应用（包括启动延迟），确保在控制运行内容和时间的同时获得更流畅的启动体验，而不会让系统过载。

## Linux Mint 中的启动时自动挂载卷

Linux Mint 中的启动时自动挂载卷允许您的驱动器在系统启动时自动连接，确保它们已就绪并可用。使用许多 Linux 发行版中的 `GNOME Disks` 工具，可以轻松设置此项。启动“磁盘”，选择您的驱动器，然后选择分区，并调整挂载选项以启用系统启动时挂载。该工具简化了向 `/etc/fstab` 文件添加条目的过程，使得分区无需手动编辑配置文件即可在全范围内可用。只需重启电脑，您选择的分区将自动挂载，简化您的设置流程以便立即访问。

## Linux Mint 快捷键和截图

在 Linux Mint 中，快捷键和截图是创建捕捉屏幕内容图像的理想选择，因此对于分享见解、解决问题或保留记忆至关重要。它们可以确认您的体验、存档信息，并为文档增加视觉上下文。通过 `Screenshot` 等工具，截图对于各种任务中的高效通信和文档记录变得价值足珍贵。

## systemd 默认超时时间

默认的 `systemd` 超时时间（通常设置为 90 秒）决定了 `systemd` 在认为操作失败之前等待服务启动或停止多长时间。这种超时机制通过防止服务无限挂起来确保系统响应性。然而，为了获得更大的灵活性，`systemd` 允许根据特定需求调整此超时时间，允许服务具有自定义的超时设置，并可以偏离默认值。

## 不可变文件和文件夹

不可变文件和文件夹是在创建后无法被修改或删除的数字资产。这一特性确保了数据的完整性和安全性，特别是在需要保持历史准确性和防止未经授权更改的环境中。虽然这个概念看起来很死板，但它是防止数据篡改和丢失的保障，提供了一种在关键信息保持未被触动时的可靠性与安心感。

## FFmpegthumbnailer

`FFmpegthumbnailer` 是一款轻量级工具，旨在快速生成视频缩略图，提高文件管理效率。它利用强大的 `ffmpeg` 库解码视频帧，其功能取决于 `ffmpeg` 的配置。`FFmpegthumbnailer` 以其速度快和资源占用低而闻名，是文件管理器必不可少的实用程序，简化了为视频文件创建视觉缩略图的过程，从而更快地识别和访问视频内容。

## Linux .desktop 文件

Linux `.desktop` 文件是简单的文本文件，为桌面环境提供有关软件应用程序的基本信息。它们定义了程序如何启动、名称以及它使用的图标。这些文件让用户更容易通过图形界面与应用程序交互。

## Linux Mint 电源设置

在 Linux Mint 中，电源设置允许用户管理计算机的能量消耗，这对于延长电池寿命和提高效率至关重要。这些设置包括屏幕亮度、睡眠模式以及笔记本盖子关闭时的行为选项。用户可以通过系统设置面板轻松自定义这些偏好，确保设备在节电的同时保持最佳运行。

## 夜光 (GNOME)

访问官方 Night Light (GNOME) 网站 `https://foundation.gnome.org/` 获取有关 Night Light (GNOME) 的所有信息。

### 通过 GUI 设置夜光 (GNOME)

首先打开应用程序菜单并选择“设置”。导航到左侧边栏上的“显示”选项卡，然后点击“夜光”。在“夜光”旁边，将开关向右拨以启用它。随后，在标记为“计划”的行中，点击下拉框选择“手动计划”。设置活动时间段从 `21:00` 开始到 `06:00` 结束。最后，将色温滑块调整到第三和第四条白线之间中点稍下方的位置。

## 夜间模式 (Cinnamon & Redshift)

访问夜间模式 (Cinnamon & Redshift) 官方网站 `https://github.com/linuxmint/cinnamon` 和 `https://github.com/jonls/redshift` 获取有关夜间模式 (Cinnamon & Redshift) 的所有信息。

### 通过命令行和图形界面安装并设置夜间模式 (Cinnamon & Redshift)

要使用 `Redshift` 设置夜间模式 (Cinnamon)，首先打开终端并输入：

```bash
sudo apt install redshift redshift-gtk wayland
```

然后，使用以下命令进入配置目录并编辑 Redshift 配置：

```bash
cd ~/.config
nano redshift.conf
```

在编辑器中，输入以下设置：

```ini
[redshift]
temp-night=2300
transition=1
brightness=1.0
gamma=1.0

[location]
adjustment-method=vidmode
location-provider=manual
```
