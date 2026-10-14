
# 别名设置

```bash
alias clean='sudo apt update && sudo apt autoremove -y && sudo apt clean -y && sudo apt autoclean -y'
```

```bash
alias remove='sudo rm -r'
```

```bash
alias gitc='git clone'
```

```bash
alias gitcr='git clone --recursive'
```

编辑完成后，点击保存并点击 X 保存退出，或者按下 `CTRL + S` 然后点击 X。

## 设置为背景

右键点击图片并点击“设置为背景”。
或者，打开“外观”，点击“添加图片”并选择要添加的图片，在按下“打开”之前，选择下方框中的图片。

## NTFS mount_options.conf

首先在终端中运行以下命令：

```bash
sudo nano /etc/udisks2/mount_options.conf
```

```ini
[defaults]

ntfs_defaults=uid=$UID,gid=$GID,nls,umask,dmask,fmask,nohidden,sys_immutable,discard,force,sparse,smhowmeta,prealloc,no_acs_rules,acl,noatime
```

## 自动启动应用程序

首先在应用程序菜单中运行以下命令：

`tweaks`

点击“启动应用程序”

点击 `+`

选择 Firefox 并点击“添加”

否则，首先在终端中运行以下命令：

```bash
cd /usr/share/applications
dir
sudo cp firefox.desktop /etc/xdg/autostart
```

## 启动时自动挂载磁盘

首先在终端中运行以下命令：

`Disks`

- 选择带有要挂载卷/分区的磁盘。
- 选择要挂载的分区。
- 点击齿轮按钮（启动或播放按钮旁边），它将显示“其他分区选项”。
- 点击“编辑挂载选项”。
- 将“用户会话默认”旁边的开关向左。
- 点击“确定”。

## 键绑定

首先在终端中运行以下命令：

```bash
cd /usr/share/themes
cd Mint-Y-Dark-Red
sudo xed cinnamon.css
```

使用 `CTRL + F` 查找闪光点

更改：
`white`

为：

```css
#00FFFFFF
```

编辑完成后，点击保存并点击 X 保存退出，或者按下 `CTRL + S` 然后点击 X。

## 截图活动窗口

首先在应用程序菜单中运行以下命令：

- 设置
- 点击“键盘”
- 点击“添加自定义快捷键”
- 点击“名称”旁边的框
- 输入：`Screenshot focused window`
- 点击“命令”旁边的框
- 输入：
```bash
bash -c cd ~/Pictures && gnome-screenshot -w -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png
```
- 点击“添加”并点击“键盘绑定”
- 按 `F10`。

## 截图全屏

首先在应用程序菜单中运行以下命令：

- 设置
- 点击“键盘”
- 点击“快捷键”
- 点击“添加自定义快捷键”
- 点击“名称”旁边的框
- 输入：`Screenshot Fullscreen`
- 点击“命令”旁边的框
- 输入：
```bash
bash -c "cd ~/Pictures && gnome-screenshot -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png"
```
- 点击“添加”并点击“键盘绑定”
- 按 `F11`。
- 点击 X。

## 调整默认超时

首先在终端中运行以下命令：

```bash
sudo xed /etc/systemd/system.conf
```

跳转到第 46 行。
更改：
```ini
#DefaultTimeoutSec=90s
```
为：
```ini
DefaultTimeoutSec=30s
```

编辑完成后，点击保存并点击 X 保存退出，或者按下 `CTRL + S` 然后点击 X。
继续运行以下命令：

```bash
sudo systemctl daemon-reload
```

## 使文件和文件夹不可变

首先在终端中运行以下命令：

```bash
sudo chattr +i example.filename
```

要使文件变为不可变，运行以下命令：

```bash
sudo chattr -i example.filename
```

## .desktop 兼容性

首先在终端中运行以下命令：

```bash
sudo apt install gthumb
```

- 右键点击文件。点击“打开方式”。
- 选择 `gthumb`。
- 将“始终使用此文件”旁边的开关向右移动。
- 点击“打开”。

## 删除 .desktop 文件

首先在终端中运行以下命令：

```bash
cd /usr/share/applications
sudo rm -r example.desktop
sudo update-desktop-database
```

## 修改电源设置

首先在应用程序菜单中运行以下命令：

- 设置
- 点击“电源”
- 点击“空屏”
- 选择“分钟”
- 点击“自动挂起”
- 点击“关闭”

## Cinnamon Applets/Spices

存在数百页的兼容 Cinnamon Applets/Spices，可以增强用户在使用 Cinnamon 桌面及其所有与之界面的程序时的功能、生产力和运行体验。

- “分组窗口列表”可以修改为显示应用程序的窗口标题，这对于识别当前活动窗口很有用。
- 可以更改以确保 `Alt-tab` 切换器样式更改为仅显示缩略图，从而轻松识别应用程序正在发生的情况。
- 菜单可以进行调整，以确保菜单图标旁边有短描述，以便能够轻松找到按钮。
- 日历可以使用“自定义日期格式”重新配置，以便显示 AM 或 PM 符号，以指示显示的时间是早晨还是晚上。

### 分组窗口列表

首先在应用程序菜单中运行以下命令：

- 文本编辑器
- 右键点击“文本编辑器”
- 点击“配置”
- 点击“面板”
- 点击“按钮标签”旁边的框
- 选择“窗口标题”
- 点击 X。

### 窗口

首先在应用程序菜单中运行以下命令：

- 窗口
- 点击 `Alt-Tab`
- 点击 `Alt-Tab` 切换器样式
- 选择“仅缩略图”。

### 菜单

右键点击菜单按钮。

- 点击配置
- 点击面板
- 点击“文本”旁边的框
- 将内容替换为：`Start`

确保文本前有一个空格，以便文本与菜单图标分开，便于用户。

### 日历自定义日期格式

右键点击右下角的日历插件。

点击配置

点击“日期格式”旁边的框

将内容替换为：

```
:%M %p
```
