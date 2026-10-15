
# 通过 GUI 安装 .deb

访问页面：`https://store.steampowered.com/about/`

- 点击 `INSTALL` 下载 Steam。
- 进入“下载”文件夹。
- 双击 `steam_latest.deb`。
- 点击安装。

# DXVK

访问官方网站 `https://github.com/doitsujin/dxvk` 获取所有 DXVK 信息。

## 从 GUI 和命令行安装 DXVK

访问页面：`https://github.com/doitsujin/dxvk/releases`

- 点击 `dvvk-tar.gz` 下载最新的 DXVK。
- 进入“下载”文件夹。
- 双击 `dvvk-2.3.tar.gz`。
- 选择 `dvvk-2.3`。
- 点击“提取”。
- 再次“提取”。
- 右键点击空白处，选择“在终端中打开”。

在终端中运行以下命令：

```
cd ~/Downloads/dvvk-2.3
```

```
cp x64/*.dll ~/.wine/drive_c/windows/system32
cp x32/*.dll ~/.wine/drive_c/windows/syswow64
winecfg
```

- 点击“库”。
- 选择“`dxgi`”并点击“编辑”。
- 将“Native（原生）”切换为“Builtin（内置）”并点击“OK”。
- 选择“`d3d9`”并点击“编辑”。
- 将“Native”切换为“Builtin”并点击“OK”。
- 选择“`d3d11`”并点击“编辑”。
- 将“Native”切换为“Builtin”并点击“OK”。
- 选择“`d3d10core`”并点击“编辑”。
- 将“Native”切换为“Builtin”并点击“OK”。

更改后，点击“应用”然后点击“OK”确认设置。

# Vkd3d-proton

访问官方网站 `https://github.com/doitsujin/dxvk` 获取所有 Vkd3d-proton 信息。

## 从 GUI 和命令行通过 .sh 安装 Vkd3d-proton

访问页面：`https://github.com/doitsujin/dxvk/releases`

- 点击 `dvvk-tar.gz` 下载最新的 DXVK。
- 进入“下载”文件夹。
- 双击 `dvvk-2.3.tar.gz`。
- 选择 `dvvk-2.3`。
- 点击“提取”。
- 再次“提取”。
- 右键点击空白处，选择“在终端中打开”。

在终端中运行以下命令：

```
cd ~/Downloads/dvvk-2.3
```

```
cp x64/*.dll ~/.wine/drive_c/windows/system32
cp x32/*.dll ~/.wine/drive_c/windows/syswow64
winecfg
```

- 点击“库”。
- 选择“`dxgi`”并点击“编辑”。
- 将“Native”切换为“Builtin”并点击“OK”。
- 选择“`d3d9`”并点击“编辑”。
- 将“Native”切换为“Builtin”并点击“OK”。
- 选择“`d3d11`”并点击“编辑”。
- 将“Native”切换为“Builtin”并点击“OK”。
- 选择“`d3d10core`”并点击“编辑”。
- 将“Native”切换为“Builtin”并点击“OK”。

# 战网 (Battle.net)

访问战网官方网站 `https://eu.shop.battle.net/en-gb?from=root` 获取所有关于战网的资讯。

## 通过 GUI 和命令行使用 .exe 安装战网

导航至发布页面：`https://download.battle.net/en-gb/?product=bnetdesk`

点击“重试 (try again)”下载战网

进入 `~/Downloads` 文件夹

在空白处点击鼠标右键

点击“在终端中打开 (Open In Terminal)”

在终端中运行以下命令：

```
sudo apt update
gamoderun wine Battle.net.exe --disable-software-rasterizer
```

按照安装流程进行

# Lutris 魔兽世界游戏内商店黑屏问题的可能解决方法

访问魔兽世界与 Lutris 网站 `https://worldofwarcraft.blizzard.com/` & `https://lutris.net/` 获取所有关于魔兽世界与 Lutris 信息。

## 通过命令行和 GUI 解决 Lutris 魔兽世界游戏内商店黑屏问题的可能解决方法

要解决使用 Lutris 时魔兽世界内商店出现黑屏的问题，请先从应用程序菜单中打开 Lutris。

然后，选择 `Blizzard Battle.net` 并点击酒杯图标旁边的箭头，选择“Wine 配置 (Wine Configuration)”。

当 Wine 配置窗口打开后，找到“Windows 版本 (Windows Version)”下拉菜单，选择 `Windows 11` 或 `Windows 10`。

应用此更改后，导航到“图形 (Graphics)”选项卡，并同时启用“增强图形性能的 CSMT (CSMT for improved graphic performance)”和“作为 DXVA2 GPU 解码后端的 VAAPI (VAAPI as backend for DXVA2 GPU Decoding)”。

下一步，移动到“驱动器 (Drives)”选项卡，点击添加按钮，定位并选择魔兽世界目录（该目录包含 `retail`、`classic` 和 `classic_era` 文件夹），然后点击“确定”。

点击“应用 (Apply)”应用这些设置，并再次点击“确定”进行确认。

确保没有设置 `WINEESY` 变量且没有运行的 `esyng` 实例，这对于这些更改的正常生效至关重要。如果你仍然遇到问题，请考虑将显卡驱动更新到最新版本。例如，更新到 NVIDIA 的 `545` 驱动已解决了某些用户的崩溃问题。

# WINE-Staging 版魔兽世界的可能解决方法

## 游戏内商店黑屏问题

访问魔兽世界与 WINE-Staging 网站 `https://worldofwarcraft.blizzard.com/` & `https://wiki.winehq.org/Wine-Staging` 获取所有关于魔兽世界与 WINE-Staging 信息。

通过命令行和 GUI 解决 WINE-Staging 魔兽世界游戏内商店黑屏问题的可能解决方法：

首先在终端中运行以下命令：

```
winecfg
```
