
`ntfs_allow=uid=$UID,gid=$GID,nls,umask,dmask,fmask,nohidden,sys_immutable,discard,force,sparse,showmeta,prealloc,no_acs_rules,acl,noatime`

通过点击“保存”保存进度，或者通过点击三 ≡ 图标并点击“另存为”后点击“保存”，然后退出。

# 在 `Cinnamon` 中添加启动项

通过图形界面在 `Cinnamon` 中添加启动项：

要在 `Linux Mint` 中通过图形界面添加启动项，使用 `Super` 键打开应用程序菜单。然后导航到“启动项”，点击 `+` 号并选择“选择应用程序”。输入您要在启动时加载的应用程序名称，选择它并点击“添加”。

通过命令行添加启动项（`Cinnamon` & `GNOME`）：

通过命令行添加启动项，首先打开终端。运行 `cd /usr/share/applications` 进入快捷方式目录。然后使用 `ls` 命令列出目录中的所有文件。识别您想要自动启动的应用程序的 `.desktop` 文件（例如 `firefox.desktop`）。执行 `sudo cp firefox.desktop /etc/xdg/autostart` 将该文件复制到启动文件夹。此命令确保所选应用程序将在启动时运行。

# 在 `GNOME` 中添加启动应用

## 通过 GUI 在 `GNOME` 中添加启动应用：

使用图形界面在 `GNOME` 中添加启动应用。

# 使用 `GNOME Disks` 自动挂载分区

访问 `GNOME Disks` 官方网站 https://apps.gnome.org/en-GB/DiskUtility/ 了解有关 `GNOME Disks` 的所有信息。

## 通过 `GNOME Disks` GUI 自动挂载分区：

要使用 `GNOME Disks` GUI 自动挂载分区，首先从应用程序菜单启动“磁盘”(Disks)。然后，选择包含您想要挂载卷的磁盘。在该磁盘上选择想要挂载的特定卷（分区），并点击齿轮图标（启动或播放按钮旁边）。在弹出菜单中，选择“编辑挂载选项”。在随后的窗口中，将“用户会话默认”旁边的开关向向左。点击“确定”确认您的更改。此过程允许直接挂载分区，无需复杂的配置。

# `Cinnamon` 截图快捷键

## 通过命令行和 GUI 更改闪光点颜色属性：

首先从菜单打开“文件”应用程序，你可以通过“`Super`”键访问它。然后，按下“`CTRL + L`”启用“位置输入”模式。输入`/usr/share/themes/`并导航到“`Mint-Y-Dark-Red`”文件夹。在此文件夹内部，进入“`cinnamon`”目录。进入后，右键点击空白处并选择“在终端打开”。接下来，执行命令`sudo gedit cinnamon.css`。在编辑器中，按下“`CTRL + F`”打开查找功能并搜索“`flashspot`”元素。将其值从“`white`”更改为“`#FFFFFF`”以使闪光点透明，防止它出现在截图中。在 `gedit` 中保存更改并退出。最后，按下“`ALT + F2`”打开 `cinnamon` 运行框，输入“`r`”并按回车键重启 `cinnamon`。这将确保你对 `cinnamon.css` 文件的修改生效。

## 通过 GUI 创建截图文件夹：

要使用图形用户界面（GUI）创建“`Screenshots`”文件夹，首先打开“文件”应用程序并导航到`~/Pictures` 目录。然后，右键点击空白处并选择创建新文件夹的选项。文件夹创建后，将其重命名为“`Screenshots`”。

## 通过 GUI 截取活动窗口：

要通过 GUI 截取活动窗口，首先从应用程序菜单打开“设置”。然后，导航到“键盘”并选择“快捷键”。点击“添加自定义快捷键”。名称输入“`Focused Window Screenshot`”。在命令字段中输入`bash -c "cd ~/Pictures/Screenshots && gnome-screenshot -w -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png"`。添加命令后，点击“添加”。接下来，通过点击“键盘绑定”并按下“`F10`”键将其设置为快捷键。

## 通过 GUI 截取全屏：

要通过 GUI 截取全屏，首先从应用程序菜单打开“设置”。然后，导航到“键盘”并选择“快捷键”。点击“添加自定义快捷键”。名称输入“`Fullscreen Screenshot`”。在命令字段中输入`bash -c "cd ~/Pictures/Screenshots && gnome-screenshot -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png"`。添加命令后，点击“添加”。接下来，通过点击“键盘绑定”并按下“`F11`”键将其设置为快捷键。

# `GNOME` 概述与 Windows 快捷键

## 通过 GUI 更改显示概览快捷键：

要通过图形用户界面调整显示概览的快捷键，只需打开应用程序菜单并执行“设置”命令。进入后导航到“键盘”标签卡并选择“查看和自定义快捷键”。在搜索栏中输入“`Show the overview`”。找到“`Show the overview`”选项后，同时按下“`Super + TAB`”键。此操作将配置你的系统提供类似于 Windows 的概览体验，特别是在配合 `arcmenu` 使用时。完成过程后，点击“设置”。

## 通过 GUI 更改切换窗口快捷键：

要通过图形用户界面调整切换窗口的快捷键，只需打开应用程序菜单并执行“设置”命令。进入后导航到“键盘”标签卡并选择“查看和自定义快捷键”。在搜索栏中输入“`Switch windows`”。找到“`Switch windows`”选项后，同时按下“`ALT + TAB`”键。完成过程后，点击“设置”。

# `GNOME` 截图快捷键

## 通过 GUI 更改截图快捷键：

要通过图形用户界面调整截图的快捷键，只需打开应用程序菜单并执行“设置”命令。进入后导航到“键盘”标签卡并选择“查看和自定义快捷键”。在搜索栏中输入“`Take a screenshot`”。找到“`Take a screenshot`”选项后，按下“`F10`”键。完成过程后，点击“设置”。

## 通过 GUI 更改窗口快捷键：

要通过图形用户界面调整截取窗口的快捷键，只需打开应用程序菜单并执行“设置”命令。进入后导航到“键盘”标签卡并选择“查看和自定义快捷键”。在搜索栏中输入“`Take a screenshot of a window`”。找到“`Take a screenshot of a window`”选项后，按下“`F1`”。完成过程后，点击“设置”。

## 通过 GUI 交互式截取窗口：

要通过图形用户界面交互式调整截取窗口的快捷键，只需打开应用程序菜单并执行“设置”命令。进入后导航到“键盘”标签卡并选择“查看和自定义快捷键”。在搜索栏中输入“`Take a screenshot of a window`”。找到“`Take a screenshot of a window`”选项后，按下“`F2`”。完成过程后，点击“设置”。

# 默认 `Systemd` 超时

访问 `Systemd` 官方网站 https://systemd.io/ 了解有关 `Systemd` 的所有信息。

## 通过命令行和 GUI 更改默认 `Systemd` 超时：

执行以下命令：

```bash
sudo apt update
```

```bash
cd /etc/systemd/
```

```bash
sudo gedit system.conf
```

修改上述 `system.conf` 文件，将以下行：

```
#DefaultTimeoutSec=90s
```

更改为：

```
DefaultTimeoutSec=30s
```

点击“保存”保存进度，或点击“文件”、“另存为”并退出。

在终端中运行以下命令：

```bash
sudo systemctl daemon-reload
```

# 设置不可变文件

访问 `Linux` 文档 https://www.linux.org/docs/man1/chattr.html 了解有关不可变文件的所有信息。

## 通过命令行设置不可变文件：

执行以下命令：

```bash
sudo apt update
```

```bash
cd ~/Downloads
```

```bash
sudo chattr -i -RV CurseForge-0.244.4-16117.AppImage
```

# `ffmpegthumbnailer`

访问 `ffmpegthumbnailer` 网站 https://github.com/dirkdvdb/ffmpegthumbnailer 了解有关 `ffmpegthumbnailer` 的所有信息。

## 通过 `APT` 安装 `ffmpegthumbnailer`：

在终端中执行以下命令：

```bash
sudo apt update
```

```bash
sudo apt install ffmpeg ffmpegthumbnailer gstreamer1.0-libav
```

```bash
rm -r ~/.cache/thumbnails/
```
