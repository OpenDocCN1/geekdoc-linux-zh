
# 视频编辑软件安装指南

## 通过图形界面通过 AppImage 安装 OpenShot

要通过 AppImage 安装 OpenShot，请先访问 `https://www.openshot.org/download/` 并选择“Linux Downloads”，然后选择“Download v.”。下载后，打开文件管理器并按 `CTRL + L` 输入 `/`。在你的主目录下创建一个名为 `Applications` 的新文件夹，然后将下载的 `OpenShot-v3.1.1-x86_64.AppImage` 文件从 `/Downloads` 移动到 `~/Applications`。右键点击 AppImage，选择“属性”，并将其设置为可执行文件。最后，双击 AppImage 启动 OpenShot。

## 从命令行和图形界面创建 OpenShot AppImage .desktop 快捷方式

要为 OpenShot AppImage 创建桌面快捷方式，打开终端并使用 `cd /usr/share/applications` 导航到该目录。然后使用 `sudo gedit Open-Shot1.desktop` 创建一个新的桌面项文件。在编辑器中输入以下内容：

```ini
[Desktop Entry]
Name=OpenShot
Comment=OpenShot Video Editor
Exec=/home/yourusername/Applications/OpenShot-v3.1.1-x86_64.AppImage
Icon=application-default-icon
Terminal=false
Type=Application
Categories=Video;AudioVideoEditing;
```

将 `/home/yourusername` 替换为你实际的主目录路径。点击“保存”或通过文件菜单保存更改。之后关闭编辑器。

## Kdenlive

访问 Kdenlive 官方网站 `https://kdenlive.org/en/` 了解所有关于 Item 的信息。

### 通过软件管理器获取 DEB/FLATPAK 软件包

- 打开软件管理器并搜索 Kdenlive。
- 点击 Item，然后点击源选择框。
- 选择系统包或 Flatpak 并点击安装。

### 在终端中通过 APT 安装 Item

只需输入以下命令：

```bash
sudo apt update
sudo apt install kdenlive
```

### 通过 Snap Store 获取 Snap 软件包

- 在 Snap Store 中寻找 Kdenlive。
- 点击 Item，然后点击源选择框。
- 选择 Snap 下的最新/稳定版本并点击安装。

### 在终端中通过 Snap 安装 Item

输入此命令：

```bash
sudo snap install kdenlive
```

### 在终端中通过 Flatpak 安装 Item

输入此命令：

```bash
flatpak install flathub org.kde.kdenlive
```

## Shotcut

访问 Shotcut 官方网站 `https://www.shotcut.org/` 了解所有关于 Item 的信息。

### 通过软件管理器获取 DEB/FLATPAK 软件包

- 打开软件管理器并搜索 Shotcut。
- 点击 Item，然后点击源选择框。
- 选择系统包或 Flatpak 并点击安装。

### 在终端中通过 APT 安装 Item

只需输入以下命令：

```bash
sudo apt update
sudo apt install shotcut
```

### 通过 Snap Store 获取 Snap 软件包

- 在 Snap Store 中寻找 Shotcut。
- 点击 Item，然后点击源选择框。
- 选择 Snap 下的最新/稳定版本并点击安装。

### 在终端中通过 Snap 安装 Item

输入此命令：

```bash
sudo snap install shotcut --classic
```

### 在终端中通过 Flatpak 安装 Item

输入此命令：

```bash
flatpak install flathub org.shotcut.Shotcut
```

## Pitivi

访问 Pitivi 官方网站 `https://www.pitivi.org/` 了解所有关于 Pitivi 的信息。

### 通过软件管理器获取 DEB/FLATPAK 软件包

- 打开软件管理器并搜索 Pitivi。
- 点击 Item，然后点击源选择框。
- 选择系统包或 Flatpak 并点击安装。

### 在终端中通过 APT 安装 Item

只需输入以下命令：

```bash
sudo apt update
sudo apt install pitivi
```

### 在终端中通过 Flatpak 安装 Item

输入此命令：

```bash
flatpak install flathub org.pitivi.Pitivi
```
