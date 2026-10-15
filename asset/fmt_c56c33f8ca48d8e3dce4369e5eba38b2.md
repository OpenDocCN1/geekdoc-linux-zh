
`512GB SSD` - 为存储文件和项目提供额外空间。

## 我基于这些要求的依据

“真实感游戏生产力”的系统要求是考虑了以下因素制定的：

- `Linux Mint 21.3` 系统要求 ([链接](https://linuxmint.com/faq.php))

- 魔兽世界世界系统要求 ([链接](https://us.battle.net/support/en/article/76459))

- 在 `Linux Mint` 上运行游戏和生产力负载的个人经验

### 额外考虑：

- 虽然最低配置将允许您运行 `Linux Mint 21.3` 并玩游戏，但推荐规格将提供更流畅、更愉快的体验。

- 如果您计划同时使用多个高需求应用（如直播、视频编辑或图形设计），请考虑分配更多的内存和存储空间。

- 定期更新您的系统软件和驱动程序以保持最佳性能。

# 获取 LINUX MINT 21.3 CINNAMON 版本 ISO

本指南将使用 `Linux Mint 21.3 Cinnamon` 版本 `ISO`，它采用了最新版本的 `Cinnamon` 桌面环境和 `GNOME 42`，因为这是我主要且最熟悉的桌面环境。

导航到以下网页地址：

`https://linuxmint.com/edition.php?id=302`

在“`MIRROR`（镜像）”部分下，找到距离您最近或您在其他方面偏好的位置。

点击对应于“`linuxmint-21.3-cinnamon-64bit.iso`”文件的超链接。

下载 `ISO` 文件。

**注意**：

随着 `Linux Mint 21` 产品周期内引入新的点版本发布，`ISO` 文件名可能会发生。例如，`Linux Mint 21.3 Cinnamon` 版本 `21.4` 点版本的 `ISO` 文件名将是“`linuxmint-21.4-cinnamon-64bit.iso`”。

# 创建带有 Linux Mint 21.3 的可启动 U 盘：分步指南

在 `Type A` 和 `Type C` `U 盘`之间进行选择时，同时考虑兼容性和性能是非常重要的。通常推荐 `Type A` `U 盘`，因为它们与主机计算机的端口具有广泛的兼容性。相比之下，`Type C` `U 盘`尽管根据 `USB-C` 标准提供了更优越的读写速度，但通常更昂贵，且在用户的电脑上不常见。然而，如果有 `Type C` `U 盘`和端口，它们因其增强的性能而是更好的选择。

关于使用 `DVD` 刻录 `ISO`，通常不推荐这种方法。尽管将 `ISO` 刻录到 `DVD` 多年来一直是一种常见做法，但与现代 `USB` 解决方案相比，`DVD` 的读写速度较慢。作为替代方案，有多种软件可用：

- `Brasero`：这是一款适用于 `Linux Mint 21` 和其他基于 `Linux` 系统的免费开源软件（`FOSS`）光盘刻录程序。`Brasero` 提供了曾为专有软件专属的功能，如刻录 `ISO` 镜像。它还通过插件扩展了功能，并内置了代码编辑器。

- `CDBurnerXP`：这是一个免费的基于 `Win32` 的替代方案，可用于替代 `Ashampoo Burning Studio 24`、`Nero Burning Rom` 和 `Cyberlink Power2Go` 等专有光盘刻录程序。`CDBurnerXP` 包括创建可启动磁盘、`ISO` 转换器和刻录后的数据验证等功能。

- `Ventoy`：另一款开源软件，`Ventoy` 用于从 `USB` 或外部 `SSD` 创建可启动驱动器。它对于传输镜像文件（如 `ISO`）并通过 `GRUB` 菜单启动它们特别有用。`Ventoy` 支持多种镜像格式，包括 `ISO`、`WIM`、`IMG`、`VHD(x)` 和 `EFI`。

这些软件选项为传统的 `DVD` 刻录提供了灵活且高效的替代方案，满足了磁盘创建和镜像处理中的各种需求和偏好。

## 安装 Brasero：多操作系统的分步指南

若要在各种操作系统上安装 `Brasero`，请遵循以下详细说明，并在每个系统的终端中执行指定的命令：

1. 基于 `Debian` 和 `Ubuntu` 的系统：
   - 打开终端。
   - 执行命令：`sudo apt install brasero`

2. 基于 `Red Hat` 和 `Fedora` 的系统：
   - 打开终端。
   - 执行命令：`sudo dnf install brasero`

3. 基于 `Gentoo` 的系统：
   - 打开终端。
   - 执行命令：`sudo emerge brasero`

4. `CentOS 8` 及更旧系统：
   - 打开终端。
   - 执行命令：`sudo yum install brasero`

5. `openSUSE` 及其衍生系统：
   - 打开终端。
   - 执行命令：`sudo zypper install brasero`

6. `Arch Linux` 及其衍生系统：
   - 打开终端。
   - 执行命令：`sudo pacman -S brasero`

## 安装 CDBurnerXP：全面指南

1. 下载网站：首先导航到 `CDBurnerXP` 网站 `https://www.cdburnerxp.se/`

2. 选择软件：进入网页后，寻找 `CDBurnerXP 64-bit Setup`。

3. 安装文件：您正在寻找的具体文件是 `cbxp_setup_4.5.7128_x64_minimal.exe`。

4. 安装过程：下载文件后，双击 `cbxp_setup_4.5.7128_x64_minimal.exe`。

5. 额外考虑：在安装过程中，可能会提示您同意许可条款并选择安装设置。

通过遵循这些步骤，您应该成功在计算机上安装 `CDBurnerXP`。

## 为 Linux Mint 21 安装并配置 Ventoy：分步指南

请按照以下步骤以完成操作：

1. 打开浏览器并导航至地址：`https://github.com/ventoy/Ventoy/releases`

2. 在网页上找到并下载 `Ventoy` 的最新版本，当前标识为 `ventoy-1.0.96-linux.tar.gz`。

3. 下载完成后，在文件管理器中找到下载的文件 `ventoy-1.0.96-linux.tar.gz`。

4. 双击文件 `ventoy-1.0.96-linux.tar.gz` 解压内容。下载目录下将创建一个名为 `ventoy-1.0.96` 的新文件夹。打开该文件夹。

5. 在 `ventoy-1.0.96` 文件夹中找到 `VentoyGUI.x86_64`。

6. 在您的 `Linux Mint 21` 系统上打开终端。

7. 在终端中通过输入以下命令进入 `ventoy-1.0.96` 目录：`cd ~/Downloads/ventoy-1.0.96`

8. 进入 `ventoy-1.0.96` 目录后，输入命令列出内容：`ls`

9. 输入以下命令以管理员权限运行 `VentoyGUI.x86_64` ：`sudo ./VentoyGUI.x86_64`

10. 在打开的 `Ventoy GUI` 窗口中，点击 `Device` 部分下的下拉框。

11. 从下拉框中选择您的 `U 盘`作为目标设备。

12. 在继续之前，确保 `U 盘`上的所有重要文件已进行本地备份并在可能的话备份在云存储服务中。

13. 点击 `Install` 按钮并在提示确认选择。

14. 安装完成后，点击 `Update` 按钮更新 `U 盘`上的 `Ventoy` 版本。

最后，将 `Linux Mint 21.3 VIRGINIA` `ISO` 文件复制到新创建的 `Ventoy` 分区。请注意不要将其复制到 `Ventoy EFI` 分区。

## 配置 BIOS 以 USB 启动

**优先级：分步指南**

基于对 `MSI MAG B550 Tomahawk` 主板的个人经验，以下是配置主板 `BIOS` 设置并禁用安全启动（`Secure Boot`）的详细步骤：

1. 插入 `USB` 驱动器：首先将 `USB` 驱动器插入主板上相应的端口。

2. 开机/重启电脑：开启电源或重启电脑。

3. 进入 `BIOS` 界面：在启动过程中，按下所需的键或组合键（通常为 `DEL`、`F2`、`F10`）进入主板设置界面。

4. 配置启动顺序：进入主板 `BIOS` 界面后，找到配置启动顺序的选项。将 `USB` 驱动器或 `USB` 磁盘移动到最左侧，以确保它是第一个启动设备。

5. 在启动菜单中优先考虑 `USB` 驱动器：此外，导航到启动选择菜单并将 `USB` 驱动器移动到列表顶部以优先排序。

6. 禁用安全启动：
    - a) 如必要，切换到高级模式（`Advanced mode`）。
    - b) 点击“`Settings`”（设置）选项。
    - c) 寻找“`Windows OS Configuration`”（`Windows OS` 配置）部分。
    - d) 在此部分内找到“`Secure Boot`”（安全启动）设置。
    - e) 将设置改为“`Disabled`”（禁用）以关闭安全启动。

7. 保存 `BIOS` 配置：完成主板 `BIOS` 设置更改后，必须保存配置。

8. 保存并应用更改：找到保存 `BIOS` 配置的选项并选择它。这将确保您的更改生效。

9. 重启系统：重启系统以完成配置过程。
