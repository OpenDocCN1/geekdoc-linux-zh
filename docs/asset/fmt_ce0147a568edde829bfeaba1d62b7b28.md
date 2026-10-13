
“屏幕保护程序”对话框具有您可以使用的各种设置，可用于测试屏幕保护程序、设置延迟或要求密码。

![](img/fbfff30e42d507bc7531108a281d6cf4_160_0.png)

> 注意
>
> 右键点击“屏幕保护程序”对话框中示例显示的不同角，可以设置自动屏屏或锁屏！会出现一个小型弹出菜单，您可以为每个角选择“忽略”、“保存屏幕”或“锁定屏幕”。例如，如果您将示例显示的左下角设置为开始屏屏，下一次当您将鼠标指针移动到显示器的左角（并在那里停留一秒钟）时，就会开始屏屏。

## 安装系统声音

点击 KDE 控制中心中的“声音”下拉菜单，然后点击“系统声音”以配置 KDE 在会话期间使用声音。KDE 识别 27 种速率系统事件，您可以为这些事件分配声音。例如，要让 KDE 在首次启动时播放声音，请点击“声音”对话框（如图 5.19 所示）中的“启用声音”，并点击“启动”系统事件。

您可以将声音图标拖入对话框的“声音”区域，或者从声音列表中点击现有的声音。完成后，点击“应用”按钮。下次您启动 KDE 时，您将听到声音文件播放。

### 图 5.19

“声音”对话框用于为不同的事件（如窗口切换）分配声音。

![](img/fbfff30e42d507bc7531108a281d6cf4_161_0.png)

> 注意
>
> KDE 声音必须是 `.wav` 格式。如果您安装了 StarOffice 5.0，各种声音的完整目录位于 `Office50/gallery/sounds` 目录下。通过您的主目录导航到“声音”目录，然后将 `Appause.wav` 文件拖入“声音”对话框，点击“启动”事件，然后点击“应用”。下次您启动 KDE 时，您将听到掌声！

## 更改键盘和鼠标设置

点击 KDE 控制中心中“输入设备”下拉菜单中的“键盘”，可以切换键盘字符重复（按住按键时重复打印一个字符）以及每次按键是否产生按键点击声。完成选择后，点击“应用”按钮（如图 5.20 所示）。

您还可以通过设置面板菜单的“输入设备”子菜单访问键盘和鼠标设置。“鼠标”对话框允许您更改光标在屏幕上移动的方式，以及针对右手用户或左手用户的用户的鼠标按钮顺序。此对话框（如图 5.21 所示）提供的功能与从命令行使用 `xset` 和 `xmodmap` 命令类似。

### 图 5.20

“键盘”对话框切换 KDE 键盘重复和按键点击声。

![](img/fbfff30e42d507bc7531108a281d6cf4_162_0.png)

### 图 5.21

左手鼠标用户可以受益于 KDE 灵活的配置！

![](img/fbfff30e42d507bc7531108a281d6cf4_162_1.png)

## 更改窗口按钮

点击“窗口”下拉菜单访问“按钮”、“鼠标”、“属性”和“标题栏”对话框。您也可以点击桌面面板上的“应用程序启动器”按钮，然后选择“设置”和“窗口”来获取这些设置。在图 5.22 所示的“按钮”对话框中切换每个按钮下的“左”、“右或关闭，以添加、删除或放置不同的窗口控件。示例窗口的按钮将根据您的选择而变化！

### 图 5.22

使用“按钮”对话框设置您的桌面名称、颜色和壁纸。

![](img/fbfff30e42d507bc7531108a281d6cf4_163_0.png)

# 红帽 Linux 的介绍与安装

## Red Hat Linux 的介绍与安装

### 图 5.26

`fwm` 窗口管理器的 AnotherLevel 配置提供了简单的开始菜单和窗口方案。

![](img/fbfff30e42d507bc7531108a281d6cf4_167_0.png)

## 配置 AnotherLevel

虽然配置 AnotherLevel 的一种方法是编辑 `/etc/X11/AnotherDirectory` 下的启动脚本，但你也可以构建并配置界面，然后选择 Preferences（首好），将桌面设置为 `new.xintric`。AnotherLevel 会你的家目录下创建一个名为 `new.xintric` 的文件。该文件包含了所有运行应用程序的名称以及大小、颜色和位置等窗口设置。以下是该文件的列表示例：

```
clock -bg yellow -update 1 -geometry 80x80-3+3
xmessage -title Calendar -file -geometry 163x142+627+86 &
rvplayer /tmp/M03SF9F413D05B3E.rm -geometry 348x309+520+199 &
rvxt -fg black -bg white -geometry 80x24+5+5
appliz -wp -geometry 581x416+6+6
rvxt -fg black -bg white -geometry 80x11+5+373 &
```

在此示例中，保存设置时使用了 `clock`、`xmessage`、`rvplayer`、`app` 和 `rvxt` 终端。这些行中的每一行都是可以修改的命令行，可以在你的 `.xintric` 文件中或 `/etc/X11/AnotherDirectory` 目录下的 AnotherLevel 的 `fwm2rc.init` 文件中使用。

通过使用 Exit `fwm` 菜单中的 Switch To 项，你可以退出 AnotherLevel 并启动不同的窗口管理器，例如 AfterStep 或 WindowMaker。

## 键盘控制

许多窗口管理器支持通过键盘控制显示、窗口或 X11 指针。表 5.2 详细列出了 AnotherLevel 的默认键盘控制。在某些情况下（如移动或缩放窗口），窗口必须处于激活或高亮状态（通过点击窗口的标题栏来实现）。

### 表 5.2 常见的 AnotherLevel 键盘命令

| 命令 | 键盘命令 |
| --- | --- |
| 显示窗口列表 (菜单) | Alt+Esc |
| 显示桌面首好菜单 | Ctrl+Shift+Alt+p |
| 显示窗口操作菜单 | Ctrl+Shift+Alt+w |
| 将窗口置于底部 | Ctrl+Alt+Return |
| 使下一个窗口激活 | Alt+Tab |
| 使上一个窗口激活 | Shift+Alt+Tab |
| 水平最小化窗口 | Ctrl+Shift+右方向键 |
| 垂直最小化窗口 | Ctrl+Shift+上方向键 |
| 最小化（图标化）窗口 | Ctrl+Shift+下方向键 |
| 移动到第一个虚拟桌面 | Ctrl+Shift+Alt+Home |
| 移动到最后一个虚拟桌面 | Ctrl+Shift+Alt+End |
| 移动窗口 | Ctrl+Shift+F7 |
| 下一个桌面 | Ctrl+Shift+Alt+下方向键 |
| 下一个桌面向左 | Ctrl+Shift+Alt+左方向键 |
| 下一个桌面向右 | Ctrl+Shift+Alt+右方向键 |
| 下一个桌面向上 | Ctrl+Shift+上方向键 |
| 指针向下 100 像素 | Ctrl+Alt+F10 |
| 指针向下 5 像素 | Ctrl+Shift+F10 |
| 指针向左 100 像素 | Ctrl+Alt+F9 |
| 指针向左 5 像素 | Ctrl+Shift+F9 |
| 指针向右 100 像素 | Ctrl+Alt+F12 |
| 指针向右 5 像素 | Ctrl+Shift+F12 |
| 指针向上 100 像素 | Ctrl+Alt+F11 |
| 指针向上 5 像素 | Ctrl+Shift+F11 |
| 将窗口置于顶层 | Ctrl+Alt+Return |
| 缩放窗口 | Ctrl+Shift+F8 |

## AfterStep 窗口管理器的特性

注意：为了在 X11 会话期间正确使用键盘，请确保你已为计算机配置了正确的键盘设置。有关 `XF86Config` 文件的详情请参见第 4 章。

AfterStep 窗口管理器（见图 5.27）是 `fwm` 窗口管理器的另一个后代。该窗口管理器的界面与 NEXTSTEP 界面相似，并包含一个用于应用程序按钮的 wharf（浮动窗口）、根菜单以及独特的图标。你可能还会喜欢它默认的窗口处理动画（在点击窗口上的最小化或缩放按钮后显示）。

### 图 5.27

为 X 提供的 AfterStep 窗口管理器提供了复杂的 X 客户端窗口和丰富的菜单。

![](img/fbfff30e42d507bc7531108a281d6cf4_169_0.png)

## 重要文件

与 Red Hat Linux 自带的其他管理器不同，AfterStep 的默认系统级配置文件位于 `/usr/share/share/afterstep` 目录。该配置目录还包含 AfterStep 的文档。你可以使用你喜欢的 Web 浏览器（如 `lynx`）如下阅读此文档（即 Andrew Sullivan 的 AfterStep 常见问题解答）：

```
# lynx /usr/share/afterstep/doc/afterstep.html
```
