
USB 迷你接口还将包含一根额外的线，对于我们的特定项目而言并非必需。

左：旧版 USB 1.0 和 2.0 线缆比新版 3.0 的线更少——这里是一个快速指南。

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_121_0.png)

上方：你可以焊接 OTG 线缆和手柄，但用胶带也可以完成这项工作。

### 选择合适的手柄

右侧手柄是最佳选择，在大多数商店都能找到（我们使用的是标准款）。

### 接线

`10` 剥去电线约两厘米，然后将它们连接在一起。你应该会有红、绿、白和黑四种线。Xbox 线缆还有一根黄线，你可以忽略它。此时值得注意的是，你需要确定你使用的是 USB 数据传输线，而不仅仅是普通的电源线——前者看起来像上面的照片，但电源线将缺少两根数据线。

剥好线后，我们临时使用普通胶带在 OTG 线缆和手柄之间制作连接——为了更永久性的安装，你可以使用电工胶带或简单地焊接电线。

### 绝缘

`11` 需要注意的是，你需要对 Pi 的底部进行绝缘，以隔离手柄上的所有触点。对于这个快速改装，我们使用了一些纸板包装——但任何不导电的材料都可以。

从此开始，只需将外壳螺丝拧回即可。确保手柄的按钮和摇杆没有错位。注意不同颜色的按钮对应的位置，你就没问题了。

### 接线连接

`12` Pi 需要连接三根线才能工作。控制柄线缆需要连接到 USB OTG 端口。一根 HDMI 线从你的电视连接到 Pi 上的 mini HDMI 端口。最后，需要一个 2A 微型 USB 电源插入 Pi 的电源插座。我们使用了标准的可重复使用手机充电器，但如果你想减少房间里拖拽杂线的麻烦，也可以使用 USB 电池组。

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_122_0.png)

### 关于供电的话

`13` 这看起来可能有点挑剔，但如果没有电视为手柄供电，HDMI 连接也能工作。不幸的是，HDMI 规范并不支持电流向该方向流动。如果你的电视上有 USB 插座，你可以用它为 Pi 供电——只需确保插座功率足够（至少需要 1 安培，理想情况下是 2 安培）。许多电视仅输出 500mA，不足以运行 Pi。

### 让我们玩吧！

`14` 好的，看起来不错——你差不多准备好开始游戏了。下一步是在设备上安装一些模拟软件。

> “如果你的电视上有 USB 插座，你可以用它为 Pi 供电——只需确保它功率足够”

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_122_1.png)

## 安装 RetroPie 模拟器

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_123_0.png)

通过模拟器运行复古软件并不像你想象的那么难。

好吧，你已经成功地将 Pi 安全地安置在一个手柄中并接好线——现在你只需要一些视频游戏来玩了。

在本教程的这一部分，我们将使用 RetroPie 模拟器。通过本教程，你将从树莓派（Raspberry Pi）直接游玩多款游戏，前提是你合法拥有 ROM 文件，当然。

整个过程很简单，只需将软件安装到你的 SD 卡上，然后复制你想玩的任何游戏即可。如果你已经在 Pi 上安装了 Raspian，你可以与 RetroPie 并行安装——或者如果你愿意，也可以将整个磁盘专门用于该软件。

### 在 Raspbian 中安装 RetroPie

1. 如果你已经开始使用 Pi 并想添加 RetroPie，你需要从 GitHub 安装软件。最新的说明可在 [`github.com/RetroPie/RetroPie-Setup`](https://github.com/RetroPie/RetroPie-Setup) 找到。在你的 Pi 上打开一个终端（例如，从另一台机器通过 SSH 登录，或直接登录到 Pi）。更新你的软件仓库并确保安装了最新版本的 Git 软件：

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git
```

下载 RetroPie 设置脚本的最新版本：

```
git clone --depth=1 https://github.com/RetroPie/RetroPie-Setup.git
```

如果你注重安全性，最好在运行脚本之前检查一下脚本的功能。准备好后，你可以通过切换到正确目录并执行脚本来安装它：

```
cd RetroPie-Setup
sudo ./retropie_setup.sh
```

#### RetroPie 项目

该脚本运行需要几分钟时间，具体取决于您的互联网连接速度。它可能会要求您授予权限以安装所需的额外软件——因此您应该允许此操作。完全安装后，您需要重启您的树莓派（Pi）。

```
sudo reboot
```

现在，您可以通过输入 `emulationstation` 来运行 RetroPie。我们将很快介绍如何配置您的设置。

## 将 RetroPie 安装到空白 SD 卡上

如果您希望您的树莓派 Zero 仅作为 RetroPie 机器使用，这是适合您的方式。请注意：它将完全擦除 micro SD 卡，因此如果您使用的是以前用过的卡，请务必在开始之前备份任何重要数据。

从 `http://blog.projectrblock.com/retropie/retro-pie-downloads` 下载最新版本软件。确保您下载了适用于您机器的正确 SD 卡镜像——适用于树莓派 2 的镜像不兼容于树莓派 Zero。请下载标准版（而不是树莓派版）。下载文件是一个 800MB 的 `.gz` 文件。解压并提取 `img` 文件，其大小约为 2.6GB。

现在，您需要将此镜像文件写入您的 micro SD 卡。这与将普通树莓派镜像安装到卡上的方式相同。Linux、Mac 和 Windows 的操作说明略有不同。

**上方** 如果您再次开机时看到类似这样的启动画面，说明安装成功了！

### 在哪里获取 ROM

- *Baker Pi Zero* 是一个完美的
- 还有几个项目可以
- 我推荐 *RetroPi* 项目作为
- *MiSTer* 项目 (`http://min-terproject.github.io/mister/`) 也拥有
- 另一个很棒的项目是 *Pi-Pok
- 实际上，Pi-Poking 项目甚至包含
- 你可以使用 *Batocera* 街机
- *Batocera* 网站 (`http://batocera.org`) 详细说明了如何安装
- *XMB* 界面 (`http://xmb.org`) 提供了
- *Arcade Emulator*, *Game
- *GameStation* 项目 (`https://github.com/`), 一个用于...的模拟器
- *PinePhone* 项目也支持
- *MooGo* 项目 (`http://moogo.org`) 提供
- 你也可以查看 *Pi-Emu
- *EmuPi* 项目 (`http://emupi.org`)
- 别忘了 *Ret
- 最后，如果你只想...
- 如果你想自己构建...

**下方** RetroPie 可以直接恢复到 SD 卡，或者你也不需要 Raspbian

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_125_0.png)

## 安装 RetroPie 模拟器

### Linux

`03` 使用磁盘管理器选择镜像文件和 micro SD 卡。然后按照屏幕上的说明操作，直到镜像完全写入卡中。

### Mac

`04` 从 `www.tweaking4all.com/hardware/raspberry-pi/macos-apple-pi-baker` 下载 ApplePi Baker。安装完成后，你可以选择镜像文件和 micro SD 卡。按照屏幕上的说明操作。

### Windows

`05` 从 `http://sourceforge.net/projects/win32diskimager` 下载 Win32 DiskImager。安装完成后，选择镜像文件和 micro SD 卡。按照说明操作，直到镜像写入卡中。

### 配置

`06` 好的，你即将准备游玩。将 micro SD 卡插入树莓派 Zero，连接好控制器、USB 线和 HDMI 线。最后，将树莓派接入电源。它应该会自动启动，几秒钟后，你会看到一个配置屏幕。

RetroPie 应该会自动检测连接的 USB 游戏手柄，并引导你设置按键。完成后，你会看到一个显示你所有选择的屏幕。

# 项目

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_126_0.png)

## 设置磁盘
