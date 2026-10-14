

Konsole
这个用于 KDE 的图形终端仿真器允许你在单个窗口中运行多个终端。
DEB: konsole
RPM: konsole
WWW: http://konsole.kde.org/

Multi Gnome Terminal
这个用于 GNOME 的图形终端仿真器具有受 Konsole 启发的增强功能，允许在单个窗口中拥有多个终端。
DEB: multi-gnome-terminal
RPM: multi-gnome-terminal
WWW: http://multignometerm.sourceforge.net/

Multi Lingual TERMINal
顾名思义，这个终端仿真器支持各种外语编码。
DEB: mlterm
RPM: mlterm
WWW: http://mlterm.sourceforge.net/

PowerShell
这个彩色终端仿真器允许在同一窗口中拥有多个终端，你可以通过点击“标签”按钮在它们之间切换。
DEB: powershell
RPM: powershell
WWW: http://powershell.sourceforge.net/

our XVT
人人皆知的命令名为 rxvt，这是一个彩色 vt102 终端仿真器，旨在作为 xterm 的替代品，比后者更小、占用内存更少，但仿真选项和可配置性较少。
DEB: rxvt
RPM: rxvt
WWW: http://sourceforge.net/projects/rxvt/

Unicode
这是带有 Unicode 支持的 xterm。
DEB: xterm
RPM: xterm
WWW: http://dickey.his.com/xterm/

Wterm
这基于我们的 XVT，但针对 Window Maker 窗口管理器进行了优化。其功能包括透明度、着色和背景图像。
DEB: wterm
RPM: wterm
WWW: http://largo.windowmaker.org/files.php?wterm

## 4.6 放大 X 桌面的某一部分

使用 xmag 放大 X 桌面的某一部分。它将打开一个新窗口，显示你选择的桌面部分，并放大到更大的尺寸。

运行时，X 指针将变为左上角的角标。有两种方法可以选择要放大的桌面区域：在屏幕上的任何位置单击一次鼠标左键，即可放大以你单击的位置为左上角的区域。你也可以选择特定的区域进行放大——方法是按下并按住鼠标中键于左上角，然后将指针拖动到你想要放大的区域的右下角。

以下是两种使用方法。

- 要放大桌面区域，请执行以下操作：
  1. 启动 xmag：
     $ xmag [RET]
  2. 在要放大的区域的左上角单击鼠标中键。
  3. 将指针移动到该区域的右下角，然后释放鼠标中键。
- 要在三秒延迟后运行 xmag，以便在它运行时有时间切换到另一个桌面窗口，输入：
  $ sleep 3; xmag [RET]

单击 Close 或输入 [Q] 即可退出程序并关闭放大的窗口。

## 4.7 配置 X

人们通常希望立即配置 X 的某些方面。本节讨论其中最受欢迎的方面，包括更改视频模式、自动在启动时运行客户端，以及选择窗口管理器。你可以在《The X Window User HOWTO》和《The Configuration HOWTO》中找到更多相关信息（关于如何阅读它们，请参阅 Recipe 2.8.6 [Reading System Documentation and Help Files]，第 50 页）。

### 4.7.1 在视频模式之间切换

视频模式是显示分辨率，以像素表示水平和垂直值，例如 640x480。X 服务器可以在硬件允许且管理员设置的情况下在视频模式之间切换；运行 X 的机器提供多种视频模式的情况并不少见，因此 640x480、800x600 和 1024x768 显示分辨率都是可能的。

要切换到另一种视频模式，请使用小键盘上的 ⊕ 和 ⊖ 键配合左 CTRL 和 ALT 键。⊕ 键切换到分辨率更低的下一个模式，而 ⊖ 键切换到分辨率更高的下一个模式。

以下是两种使用方法。

- 要切换到下一个最低视频模式，输入：CTRL-ALT-⊕
- 要切换到下一个最高视频模式，输入：CTRL-ALT-⊖

要循环浏览所有可用的视频模式，请重复输入其中任意一种键组合。

NOTES: 有关视频模式的更多信息，请参阅 The XF86 Video Timings HOWTO（请参阅 Recipe 2.8.6 [Reading System Documentation and Help Files]，第 50 页）。

### 4.7.2 自动运行 X 客户端

`.xsession` 文件是主目录中的一个隐藏文件，指定在 X 会话首次启动时自动运行的客户端（“隐藏”文件在第 5 章 [Files and Directories]，第 125 页中有说明）。它只是一个 shell 脚本，通常包含要运行的客户端列表。你可以在文本编辑器中编辑你的 `.xsession` 文件，如果该文件不存在，你可以创建它。

客户端按列出的顺序启动，最后一条行应指定要使用的窗口管理器。以下示例 `.xsession` 文件启动一个 `xterm`，背景为黑色、文字为白色、光标为棕色且无滚动条，将一个 `xclock` 放在左上角（受 AfterStep 启发的时钟，灵感来自 NEXTSTEP 的“撕下式”日历时钟），启动 Emacs 文本编辑器，并在其自己的缓冲区中打开文件 "~/TODO"，然后启动 AfterStep 窗口管理器：

