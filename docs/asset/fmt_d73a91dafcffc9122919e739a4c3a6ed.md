
```bash
sudo apt update && sudo apt install winehq-staging gamemode winbind protobuf-compiler libprotobuf-dev libopusfile0 winetricks
```

# WINE-Mono

撰本文时最新的 `wine-staging` 为 8.9，最新的 `wine-mono` 版本为 8.0，通常观察结果是 `wine-mono` 的版本较后，但 `wine-mono` 的版本通常低于 `wine-staging`。

前往以下网页地址：

https://dl.winehq.org/wine/wine-mono

## 启用 Steam Play

首先在应用程序菜单中运行以下命令：

- Steam
- 点击“Steam”
- 点击“设置 (Settings)”
- 点击“Steam Play”
- 勾选以下项目旁边的复框：
- 为支持的游戏启用 Steam
- 为所有其他游戏启用 Steam Play
- 点击“运行其他游戏的方式：”旁边的下拉框
- 选择“Proton Experimental”，
- 点击确定
- 点击 重启 Steam

## 手动安装 Proton-GE

首先，访问以下网页地址：

https://github.com/GloriousEggroll/proton-ge-custom/releases

- 下载最新的 `GE-Proton.tar.gz`
- 双击 `GE-Proton8-4.tar.gz`
- 选择全选
- 点击解压
- 按 `CTRL + H` 显示隐藏文件夹
- 进入 `~/.steam/root`
- 点击右上角的“新建文件夹”
- 输入：`compatibilitytools.d`
- 点击创建

你应该会自动进入 `compatibilitytools.d` 文件夹，如果不是，请导航到以下目录：

`~/.steam/root/compatibilitytools.d`

- 点击解压

继续在应用程序菜单中运行以下命令：

- Steam
- 点击“Steam”
- 点击“设置 (Settings)”
- 点击“Steam Play”
- 勾选“为所有其他游戏启用 Steam Play”旁边的框
- 点击“运行其他游戏”旁边的下拉框
- 选择：`GE-Proton-4` 并点击“确定”
- 点击“重启 Steam”并点击“库”
- 右键点击游戏并选择“属性”
- 勾选“强制使用特定的 Steam Play 兼容性工具”旁边的框
- 点击下方出现的下拉框
- 选择：`GE-Proton-4`
- 点击右上角的“X”。

## Heroic Games Launcher

首先在“软件 (Software)”中运行以下命令：

- Heroic Games Launcher
- 点击 Heroic Games Launcher 并安装。

或者，首先在终端中运行以下命令之一：

```bash
flatpak install flathub com.heroicgameslauncher.hgl
```

```bash
sudo snap install heroic
```

否则，首先访问以下网页地址：

https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/releases

```
download the latest heroic_amd64.deb
```

双击 `heroic_2.8.0_amd64.deb` 并安装。

## Minigalaxy

首先在“软件管理器 (Software Manager)”中运行以下命令：

- Minigalaxy
- 点击 Minigalaxy 并安装。

否则，首先在终端中运行以下命令之一：

```bash
flatpak install flathub io.github.sharkwouter.Minigalaxy
```

否则，首先访问以下网页地址：

https://github.com/sharkwouter/minigalaxy/releases

- 下载最新的 `minigalaxy_all.deb`。
- 双击 `minigalaxy_1.2.2_all.deb` 并安装。

## PlayOnLinux

首先在“软件 (Software)”中运行以下命令：

- PlayOnLinux
- 点击 PlayOnLinux (或 Phoenicis PlayOnLinux)并安装。

另一方面，首先在终端中运行以下命令之一：

```bash
sudo apt install playonlinux
```

```bash
flatpak install flathub org.phoenicis.playonlinux
```

## Gamehub

首先在“软件 (Software)”中运行以下命令：

- Gamehub
- 点击 Gamehub 并安装。

或者，首先在终端中运行以下命令之一：

```bash
sudo apt install gamehub
```

否则，首先访问以下网页地址：

https://tkashkin.github.io/projects/gamehub/

- 点击稳定版 (stable) 下的 `.deb`。
- 双击 `GameHub-0.16.3-2-master-bionic-amd64.deb` 并安装。

## Xbox 云游戏

首先访问以下网页地址：

https://www.microsoft.com/en-us/edge/download?form=MA13FJ

- 滚动到“Microsoft Edge 现在已支持 Linux。下载适用于”
- 点击 Linux (.deb)
- 点击接受并下载以 Microsoft Edge。
- 双击 `microsoft-edge-stable-amd-64.deb` 并安装。

打开 Microsoft Edge。

访问以下网站：

https://www.xbox.com/en-GB/play

登录以访问 Xbox 云游戏。

## Itch.io

首先访问以下网页地址：

https://itch.io/app

- 点击 Linux 下载 Itch.io
- 打开文件并进入 `~/Downloads` 目录。
- 右键点击 `itch-setup` 并点击“属性”。
- 将“作为程序执行”旁边的开关向右移动，并点击右上角的交叉按钮。
- 双击 `itch-setup`

## DXVK

这需要安装 `WINE-Staging` 并在终端中运行 `winecfg` 命令。

首先访问以下网页地址：
https://github.com/doltsujin/dxvk/releases

- 下载最新版本的 `dxvk-..tar.gz`
- 选择 `dxvk-2.2`
- 点击解压
- 点击下载
- 点击解压
- 点击显示文件
- 双击 `dxvk-2.2`
- 右键点击空白处并点击“在终端中打开”。

在终端中运行以下命令：

```bash
cp x64/dxvk.so ~/.wine/drive/system64/
cp x86/dxvk.so ~/.wine/drive/system32/
cp x64/vkd39.so ~/.wine/drive/system64/
cp x86/vkd39.so ~/.wine/drive/system32/
```

在终端中运行以下命令：
`cp x64/dxvk.so ~/.wine/drive/system64/`
`cp x86/dxvk.so ~/.wine/drive/system32/`
`cp x64/vkd39.so ~/.wine/drive/system64/`
`cp x86/vkd39.so ~/.wine/drive/system32/`

# 游戏内商店 WINE-Staging 黑屏修复

需要取消设置 `WINEESY` 变量，并确保没有 `esync` 实例正在运行。

首先在终端中运行以下命令：

```
winecfg
```
