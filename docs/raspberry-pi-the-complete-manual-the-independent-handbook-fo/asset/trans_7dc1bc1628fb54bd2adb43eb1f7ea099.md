

## 项目

## Xbox Zero 街机

![](img/f11b7dbb71886af07ef87126037ebe98_121_0.png)

### 右侧手柄

C23 或 GameStop 等二手商店通常有一些老旧或过时的游戏主机，以及那些已退出货架的配件，因为如今它们很少能通过这些产品获利。如果你在陈列区没找到你需要的东西，不妨问问店员库存里有什么。一些慈善商店也出售老式主机。如果都没有，当地的汽车后备箱市集或简单地询问你的游戏迷朋友，都是获取各种主机廉价手柄的极佳途径。

### 接线

- 10. 将电线剥出几厘米长，然后将它们连接在一起。你应该有红、绿、白和黑四根线。Xbox 线缆还有一根黄线，你可以忽略它。此时值得注意的一点是，你需要确保你使用的是 USB 数据传输线，而不仅仅是普通的电源充电线——前者外观如上图所示，但电源线会缺少那两根数据线。
- 电线剥好后，我们暂时使用普通胶带将 OTG 线缆与手柄进行连接——如果希望获得更持久的安装效果，你可以使用绝缘胶带或直接将电线焊接在一起。

### 绝缘

- 11. 有一点需要注意：你需要用绝缘材料将 Pi 的底部与手柄上的所有接触点隔离开。对于这种快速改装，我们使用了一些纸板包装——但实际上任何非导电材料都可以。之后，只需将外壳重新拧回去即可。请确保手柄的按钮和摇杆没有错位。记住不同颜色按钮的位置对应关系，这样就没问题了。

### 连接线路

12. 为了让 Pi 正常工作，需要连接三根线。手柄线缆需要连接到 USB OTG 端口。HDMI 线从你的电视连接到 Pi 上的 mini HDMI 端口。最后，需要一个 2A 的 Micro USB 电源适配器插入 Pi 的电源插座。我们使用了标准的手机充电器，但如果你想减少房间内拖着的线缆数量，也可以使用 USB 充电宝。

![](img/f11b7dbb71886af07ef87126037ebe98_122_0.png)

### 关于供电

13. 你或许会想知道是否可以通过 HDMI 线从电视向手柄供电。遗憾的是，HDMI 规范不允许电流沿这个方向流动。如果你的电视上有 USB 接口，你可以用它为 Pi 供电——但务必确保该接口的功率足够。Pi 至少需要 1 安培，理想情况下是 2 安培。许多电视仅输出 500mA，这对于运行 Pi 来说是不够的。

### 让我们玩起来！

14. 好的！看起来很棒——你几乎准备好开始游戏了。下一步是在这台设备上安装一些模拟器软件。

> “如果你的电视有 USB 接口，你可以用它为 Pi 供电——只需确保其功率足够大。”

![](img/f11b7dbb71886af07ef87126037ebe98_122_1.png)

![](img/f11b7dbb71886af07ef87126037ebe98_123_0.png)

> **什么是模拟器？**
>
> 模拟器是一种软件，它让你的电脑模拟另一种类型的计算机。它能允许树莓派 Zero 运行原本为世嘉 Mega Drive、任天堂 N64、老式 DOS 电脑等设备设计的软件。不过，模拟器也并非没有缺点——在软件中完美重现游戏主机几乎是不可能的。请记住，旧游戏可能存在各种 Bug，从轻微的声音和图形故障到彻底的崩溃都有可能。

## 安装 RetroPie 模拟器

通过模拟器运行复古软件并没有你想象的那么难

好了，既然你已经成功地将 Pi 安全地安置在手柄内部并接好了线路——现在你只需要一些视频游戏就可以玩了！

在本教程的这一部分，我们将使用 RetroPie 模拟器。完成本教程后，当然在你合法拥有 ROM 文件的前提下，你将能够直接从树莓派上运行多款游戏。

整个过程非常简单，只需将软件安装到你的 SD 卡上，然后复制你想玩的任何游戏即可。如果你的 Pi 上已经安装了 Raspbian，你可以在其旁边安装 RetroPie——或者，如果你愿意，也可以将整个磁盘专门用于该软件。

### 在 Raspbian 内部安装 RetroPie

- 1. 如果你已经开始使用你的 Pi 并希望在其上添加 RetroPie，你需要从 Git-Hub 安装软件。最新的说明可在 [https://github.com/RetroPie/RetroPie-Setup](https://github.com/RetroPie/RetroPie-Setup) 找到
- 在你的 Pi 上打开终端（例如，通过从另一台机器 SSH 登录，或直接登录到 Pi）。更新你的软件源并确保安装了最新版本的 Git 软件：
  ```
  sudo apt-get update
  sudo apt-get upgrade
  sudo apt-get install git
  ```
- 下载最新版本的 RetroPie 安装脚本：
  ```
  git clone --depth=1 https://github.com/RetroPie/RetroPie-Setup.git
  ```
- 如果你对安全比较敏感，建议在运行之前检查脚本的内容。准备好后，你可以进入正确的目录并执行脚本来安装：
  ```
  cd RetroPie-Setup
  sudo ./retropie_setup.sh
  ```

![](img/f11b7dbb71886af07ef87126037ebe98_124_0.png)

脚本运行需要几分钟，具体取决于你的互联网连接速度。它还可能会请求你许可安装所需的额外软件——你应该允许这样做。完全安装后，你需要重启你的 Pi。

```
sudo reboot
```

现在可以通过输入 emulationstation 来运行 RetroPie。我们稍后会介绍如何配置你的设置。

### 将 RetroPie 安装到空白 SD 卡上

- 如果你希望你的树莓派 Zero 仅作为一台 RetroPie 机器使用，这就是你的选择。警告：这将完全清除 microSD 卡，所以如果你使用的是用过的卡，请务必在开始前备份任何重要数据。

从 [http://blog.retrodeck.com/retropie/retropie-downloads](http://blog.retrodeck.com/retropie/retropie-downloads) 下载该软件的最新版本。确保下载适合你机器的正确 SD 卡镜像——树莓派 2 的镜像与树莓派 Zero 不兼容。下载 Standard 版本（而不是 BerryBoot 版本）。下载文件是一个 880MB 的 .gz 文件。解压并提取 img 文件，其大小约为 2.6GB。

现在你需要将这个镜像文件写入你的 microSD 卡。操作方式与安装普通树莓派镜像到卡上相同。Linux、Mac 和 Windows 的操作说明略有不同。

![](img/f11b7dbb71886af07ef87126037ebe98_124_1.png)

## Xbox Zero 街机

## 项目

![](img/f11b7dbb71886af07ef87126037ebe98_125_0.png)

### 在哪里获取 ROM

许多老游戏仅仅因为发布者的倒闭而被遗弃，且目前尚不清楚版权归属。有几个网站声称它们获得了原始创作者的分销授权来分发其游戏——但它们都应当明确说明，它们并没有授予购买合法副本或合法商业销售这些游戏的权利。复制和下载游戏是合法的。

### Linux

03 使用磁盘管理器选择镜像文件和 microSD 卡。按照屏幕上的说明操作，直到镜像完全写入卡中。

### Mac

04 从 [www.twakemefall.com/hardware/raspberry-pi-macosxapplepi-baker](www.twakemefall.com/hardware/raspberry-pi-macosxapplepi-baker) 下载 Apple Pi Baker。安装完成后，你可以选择镜像文件和 microSD 卡。按照屏幕上的说明操作。

### Windows

05 从 [http://sourceforge.net/projects/win32diskimager/](http://sourceforge.net/projects/win32diskimager/) 下载 Win32 DiskImager。安装完成后，选择镜像文件和 microSD 卡。按照屏幕上的说明操作，直到镜像写入卡中。

### 配置

06 好的——你几乎准备好开始玩了。将 microSD 卡插入树莓派 Zero，连接手柄 USB 线缆和 HDMI 线缆。最后，将 Pi 接入电源。它应该会自动启动，几秒钟后，你将看到一个配置屏幕。

RetroPie 应该能自动检测任何连接的 USB 游戏手柄，并引导你设置按键。完成后，你会看到一个显示所有你所做选择的屏幕。

![](img/f11b7dbb71886af07ef87126037ebe98_125_1.png)

![](img/f11b7dbb71886af07ef87126037ebe98_125_2.png)

