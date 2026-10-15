
Peppermint 很高兴地宣布我们最新的操作系统 Peppermint Six 的推出。简单且内置快速，无论你是在桌面上、在线还是使用云应用程序使用该软件，Peppermint Six 都提供了保障。我想借此机会感谢 Mark Greaves，他坚持并制作了你在这里 Peppermint Six 中看到的大部分内容。Mark 现在通过领导开发团队在 Peppermint 发挥重要作用。我认为他会对他和其他人在 Peppermint Six 上共同完成的作品留下深刻印象。

Shane Remington，Peppermint OS, LLC 首席运营官

2016 年 6 月 24 日，发布了 Peppermint Seven。

Peppermint 团队很高兴地宣布我们最新的 Peppermint 7 应用，同时适用于 32 位和 64 位系统，以及全支持 UEFI / GPT / Secure Boot 的最新版本，新版本的 Ice（我们的框架特定浏览器主页）也得到了 Firefox 和 Chromium / web 浏览器的完全支持。

Mark Greaves，Peppermint

# 232 ■ Linux

2020 年 1 月 14 日，`Raspberry Pi OS`（以前称为 `Raspian`）是一个基于 `Debian` 的树莓派系统。自 2015 年以来，树莓派基金会正式为树莓派系列单板电脑提供主要的操作系统。`Raspberry Pi OS` 是一个高度开发的项目。

2022 年 2 月 2 日，`Raspberry Pi OS` 有以下安装选项：

- `Raspberry OS` `Lite` 32 位和 64 位
- `Raspberry OS` `Full` 32 位和 64 位
- `Raspberry OS` `Lite` 是一个精简版本，不包含桌面环境
- `Raspberry OS` 安装 `Pixel` 桌面环境
- `Raspberry OS` `Full` 预装了额外的软件

所有版本仍以 `.img` 磁盘镜像的形式发行。这些文件可以闪存到运行 `Raspberry Pi OS` 的 `microSD` 卡中。2020 年 3 月，树莓派基金会发布了 `Raspberry Pi Imager`。此自定义磁盘允许安装 `Raspberry Pi OS` 和其他支持树莓派的应用程序，包括 `RetroPie`、`Kodi OS` 等。

# LXDE 桌面环境 ■ 233

- `Raspberry OS` `Lite` 32 位和 64 位
- `Raspberry OS` 32 位和 64 位
- `Raspberry OS` `Full` 32 位
- `Raspberry OS` `Lite` 是一个精简版本，不包含桌面环境
- `Raspberry OS` 安装 `Pixel` 桌面环境
- `Raspberry OS` `Full` 预装了额外的软件

## 特性

- **用户界面：** 树莓派桌面 `PIXEL` 类似于大多数常用桌面（如 `macOS` 和 `Windows`），并基于 `LXDE`。菜单栏已设置，包含终端、`Chromium` 和文件管理器快捷方式。右侧有蓝牙菜单、Wi-Fi 菜单、音量控制器和数字钟。

- **包管理：** 可以使用 `APT`、推荐软件以及添加/删除软件中的 `APT GUI` 安装软件包。

- **组件：** `PCManFM` 是一个允许快速访问所有计算机位置的文件浏览器，并为 `Raspberry Pi OS` `Buster`（2019-06-20）重新设计。`Raspberry Pi OS` 最初使用 `Eiphany` 作为浏览器，通过重新设计的桌面切换到了 `Chromium`。`Raspberry Pi OS` 配有许多基础 `IDE`，如 `Thonny` Python `IDE`、`Mu Editor` 和 `Greenfoot`。它还配备了 `Scratch` 和 `Bookshelf` 等教育软件。

- **Trisquel：** `Trisquel` 是一个计算机应用，一个 Linux 发行版，可在另一个发行版 `Ubuntu` 中获取。该项目目标是一个不包含专利软件或固件的自由软件程序，它使用了修改版本的 `Ubuntu` 内核并移除了非自由代码（二进制块）。`Trisquel` 依赖于用户的贡献。它的标志是三足（`triskelen`），一种凯尔特符号。自由软件会将 `Trisquel` 列为仅包含自由软件的发行版。

## 历史

该项目于 2004 年始于维戈大学对教育软件中加利西亚语的支持。它于 2005 年 4 月正式发布，`GNU` 项目创始人 `Richard Stallman` 作为特邀嘉宾出席。根据项目主管 `Rubén Rodríguez` 的说法，对加利西亚语的支持激发了南美和墨西哥来自奥伦塞省的移民社区的兴趣。2008 年 12 月，自由软件基金（`FSF`）将 `Trisquel` 加入了其 Linux 批准自由软件发行版列表。

## 版本

共有五个基本版本，如下所示：

1. `Trisquel`
2. `Trisquel Mini`
3. `Triskel`
4. `Trisquel Sugar TOAST`
5. `Trisquel NetInstall`

让我们来看每一个：

- **`Trisquel`**: 标准的 `Trisquel` 发行版包含 `MATE` 桌面环境和用户界面（`GUI`）、英语、西班牙语以及其他 48 种本地语言（共 50 种），包含在 2.6 GB 的 `live DVD` 镜像中。如果在安装时连接互联网，可以下载某些翻译包。

- **`Trisquel Mini`**: `Trisquel Mini` 是 `Trisquel` 的主要版本之一，旨在旧旧的笔记本电脑和硬件上良好运行。它使用 `LXDE` 以及低资源的 `GTK+` 和 `X Window` 系统资源，这与其他 `GNOME` 和 `Qt-KDE` 应用不同。`LXDE` 桌面仅包含英语和西班牙语本地描述，可能由 1.2 GB 的 `DVD` 镜像。

- **`Trisikel`**: `Trisikel` 是另一个使用 `KDE` 界面的主要 `Trisquel` 版本，以 2.0 GB `live ISO DVD` 的形式提供。

- **`Trisquel Sugar TOAST`**: `Sugar` 是一种为共享学习中的儿童设计的开源桌面空间。`Sugar` 用 `Trisquel` 取代了标准的 `MATE` 桌面。

- **`Trisquel NetInstall`**: `NetInstall` 包含一个 25MB 的 `CD` 镜像，仅包含少量的软件以执行基于文本的网络安装程序，并在在线下载剩余包。

`LXDE` 还有其他各种替代桌面，如下：

- **`Arch Linux`**: `Arch Linux` 是一个适用于 `x86-64` 处理器的 Linux 发行版。`Arch Linux` 遵循 `KISS` 原则（保持简单，愚蠢的）。该项目努力减少与发行相关的更改。因此，它在更新方面有些反其常常，实用性重于设计理念，并关注定制化而非易用性。为 `Arch Linux` 编写的包管理器 `Pacman` 用于安装、卸载和更新软件包。`Arch Linux` 采用选择模型，这意味着系统没有完全新版本的“大版本发布”；只需进行常规系统更新即可获得最新的 `Arch` 软件；`Arch` 团队每月发布的安装照片是关键系统组件的最新镜像。

- **`Artix Linux`**: `Artix` 是基于 `Arch Linux` 的输出发行版，它使用 `OpenRC`、`runit`、`suite66` 或 `doit init` 代替 `systemd`。`Artix Linux` 有自己的包仓库，作为一个基于 `Pacman` 的发行版，它可以使用来自 `Arch Linux` 以及任何其他退出发行版的包，甚至包括依赖于 `systemd` 的包。还可以使用 `Arch` 用户仓库（`AUR`）。`Arch OpenRC` 起于 2012 年，`Manjaro OpenRC` 随之开发。2017 年，这些项目被整合在一起构建 `Artix Linux`。

- **`Debian`**: `Debian` 可以访问包含超过 51,000 个软件包的在线存储。`Debian` 官方包含唯一的自由软件，但在 `Debian` 仓库上下载并安装非自由软件。`Debian` 拥有流行程序，如 `LibreOffice`、`Firefox` 浏览器、`Evolution` 邮件、`K3b` 光刻刻机、`VLC` 媒体播放器、`GIMP` 图像编辑器和 `Evince` 文档查看器。`Debian` 是服务器的热选择，例如 `LAMP` 栈操作系统。

## 特性

1. 每个端口都提供几种 Linux 内核。例如，`i386` 端口支持本地扩展和实时计算机的 `IA-32` `PC`、旧 `PC` 以及 `x86-64` `PC`。Linux 内核不包含无资源的固件，尽管此类固件在自由软件包和其他安装介质中可用。

2. `Debian` 提供了专门为 `XFACE`、`GNOME`、`KDE`、`Mate`、`Cinnamon`、`LXDE` 和 `LXQT` 设计的 `CD` 和 `DVD` 镜像。`MATE` 官方支持，而 `Debian 8.0 Jessie` 增加了 `Cinnamon` 支持。还有诸如 `Light`、`Openbox`、`Fluxbox`、`IceWM`、`Window` 等其他不常见的窗口管理器。

3. 多媒体支持一直是 `Debian` 的一个问题，涉及到可能侵犯版权的威胁、无资源或受限许可的解码器。尽管带有分发问题的包可能会进入尴尬区域，但 `libvdccss` 并未托管在 `Debian` 上。

## 使用 LXDE 的原因
