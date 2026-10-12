
- `sudo reboot`

- 2. 请注意，现在使用 `sudo reboot` 可能会导致系统快速重启且无法妥运行中的进程。这可能会导致内核错误。

- 3. 如果因不当重启导致任何问题，可能需要通过 `GRUB` 以恢复模式加载当前内核。

升级包。一旦设置好，此包将确保您的系统自动保持最新状态，而无需手动干预。

如果您发现更新通知的频率过于干扰，`Linux Mint` 也为此提供了相应的解决方案。

对于那些对更高级的自定义感兴趣（例如更改或更新内核）的用户，`Linux Mint` 提供了相关指导。

总之，`Linux Mint` `21` 提供了灵活的图形界面、命令行方法来更新更新，确保系统的流畅与安全。

# 掌握更新管理器：全面指南

1. 启动更新管理器。
2. 在弹出提示时点击“继续”。
3. 在“是否要切换到本地镜像”时点击“是”。
4. 通过点击“X”按钮关闭提示。
5. 点击“刷新”以更新软件包列表。
6. 使用 `vim` 选择要更新的软件包。
7. 点击“描述”选项卡查看软件包描述。
8. 在“软件包”选项卡查看受影响的软件包以及更新总大小。
9. 进入“更新日志”选项卡查看更新更改。
10. 勾选您要执行的更新旁边的框。
11. 点击“安装更新”开始安装。
12. 等待更改生效。
13. 再次点击“刷新”。
14. 通过点击“X”按钮关闭更新管理器。

## 通过命令行更新：分步指南

1. 打开终端。
2. 运行 `sudo apt update` 更新软件包和存储库列表。
3. 检查 `/etc/apt/sources.list` 或 `/etc/apt/sources.list.d/` 中的文件是否存在错误。
4. 运行 `sudo apt upgrade` 查看可更新的软件包。
5. 读取将更新或删除的软件包列表，并确认“Y”或“N”（或按 `Ctrl + C` 取消）。

## 无缝系统维护：配置自动更新

1. 在终端运行 `sudo apt install unattended-upgrades`。
2. 运行 `sudo apt install update-notifier-common`。
3. 运行 `sudo xed /etc/apt/apt.conf.d/20auto-upgrades` 并修改指定的行。
4. 将 `APT::Periodic::Update-Package-Lists` 改为：

   `APT::Periodic::Update-Package-Lists "1";`

5. 将 `APT::Periodic::Unattended-Upgrade` 改为：

   `APT::Periodic::Unattended-Upgrade "1";`

6. 编辑完成后，保存进度并退出（点击保存后点击 X，或按 `CTRL + S` 后点击 X）。
7. 运行 `sudo xed /etc/apt/apt.conf.d/50-attended-upgrades` 并取消指定行的注释：

   `"${distro_id}:${distro_codename}";`

   `"${distro_id}:${distro_codename}-security}";`

   `"${distro_id}:${distro_codename}-updates}";`

8. 对于

   `"${distro_id}:${distro_codename}";`

   `"${distro_id}:${distro_codename}-security}";`

   `"${distro_id}:${distro_codename}-updates}";`

9. 编辑完成后，保存进度并退出（点击保存后点击 X，或按 `CTRL + S` 后点击 X）。

`AppImages` 的移除选项。此外，它还包含一个用于脚本自动化的 `CLI` 工具 `ail-cli`，增强了 `AppImage` 的可用性和系统兼容性。

`pip` 是 `Python` 的官方包管理器，用于安装和管理 `Python` 包及模块。它连接到 `Python` 包索引器（`Python Package Index`）以访问大量的公共包，支持包的安装、删除和依赖管理。`pip` 默认包含在 `Python` `2.7.9+` 和 `Python` `3.4+` 中，通过“requirements”文件进行批量安装，简化了在不同环境中部署 `Python` 软件。它还允许通过 `setup.py` 文件进行本地项目安装，使其成为 `Python` 开发的重要工具。

`Node.js` 是一个异步、事件驱动的 `JavaScript` 运行时，专为扩展的网络应用程序设计，能够高效地管理多个连接。`npm` 是 `Node.js` 的包管理器，作为一个包含超过 `800,000` 个代码包的庞大仓库，帮助开发者发现、共享和管理各种项目（包括 `Web` 开发、机器人和移动应用）的依赖项。`Node.js` 和 `npm` 共同构跨多种应用的现代 `JavaScript` 开发的基础技能。

`NVM`（或 `Node` 版本管理器）是一个旨在在设备上管理多个 `Node.js` 版本的工具。它解决了不同项目需要特定 `Node` 版本的挑战，消除了在不同项目中使用单一 `Node` 版本时产生的错误和兼容性问题。`NVM` 无需依赖 `npm` 来切换 `Node` 版本（这可能会导致警告或错误），允许你通过命令行轻松地为每个项目安装和切换 `Node` 版本，确保准确执行和最佳的开发体验。

`pnpm` 是一个用于 `Node.js` 的快速、高效的包管理器，它通过从全局存储到项目的 `node_modules` 文件夹创建硬链接来节省磁盘空间，而不是复制文件。它通过接字（`junctions`）支持 `Windows` 并避免 `node_modules` 的深度嵌套，防止兼容性问题。`pnpm` 为每个项目维护独立的依赖集以避免冲突，即使在具有多个驱动器或文件系统的系统中也是如此。`pnpm` 以性能著称，代表“`performant npm`”，为常见的依赖管理问题提供了解决方案并允许通过 `hooks` 进行自定义修复。

`Homebrew` 是适用于 `macOS` 和 `Linux` 的通用包管理器，简化了系统缺失软件的安装。它将包安装在自己的目录中并将文件符号链接到 `/usr/local`（`Apple Silicon` 上为 `/opt/homebrew`），避免了专用空间之外的杂乱。用户可以通简单的 `Ruby` 脚本轻松创建 `Homebrew` 包，提供了便利与自定义的结合。`Homebrew` 还支持用于 `macOS` 应用的 `cask`，通过简单的安装过程增强了其实用性。它由 `Max Howell` 发起，基于 `Git` 和 `Ruby` 构建，确保修改可管理且上游的更新可以平滑集成。

## Gdebi

访问 `Gdebi` 官方网站 `https://launchpad.net/gdebi` 了解关于 `Gdebi` 的所有信息。

通过软件管理器安装 `DEB`/`FLATPAK` 包：

- 打开软件管理器并搜索 `Gdebi`。
- 点击 `Gdebi`，然后点击源选择框。
- 选择系统包或 `Flatpak` 并点击安装。

在终端中通过 `APT` 安装 `Gdebi`：

输入以下命令：

```
sudo apt update
```

```
sudo apt install gdebi
```

## Flatpak

访问 `Flatpak` 官方网站 `https://flatpak.org/` 了解关于 `Flatpak` 的所有信息。

在终端中通过 `APT` 安装 `Flatpak`：

输入以下命令：

```
sudo apt update
```

```
sudo apt install flatpack
```

## Flathub

访问 `Flathub` 官方网站 `https://flathub.org/en` 了解关于 `Flathub` 的所有信息。

在终端中通过 `FLATPAK` 安装 `Flathub`：

输入以下命令：

```
sudo apt update

flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Snap

访问 `Snap` 官方网站 `https://snapcraft.io/` 了解关于 `Snap` 的所有信息。

在终端中通过 `APT` 安装 `Snap`：

输入以下命令：

```
sudo apt update
sudo mv /etc/apt/preferences.d/nosnap.pref ~/Documents/nosnap.backup
sudo apt update
sudo apt install snapd
```

## Snap Store

访问 `Snap Store` 官方网站 `https://snapcraft.io/snap-store` 了解关于 `Snap Store` 的所有信息。

在终端中通过 `Snap` 安装 `Snap Store`：

输入命令：

```
sudo snap install snap-store
```

## AppImages

访问 `AppImages` 官方网站 `https://appimage.org/` 了解关于 `AppImages` 的所有信息。
