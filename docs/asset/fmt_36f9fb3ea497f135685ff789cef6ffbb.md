
Some of the concepts in this book are, I must admit, more than a little tricky. If you’ve made it this far, you’ve had to learn a lot. Get ready for something really confusing.

The VMware Tools XFree86 server inside a Linux virtual machine reads the settings of your host’s XFree86 server to come up with an optimum display size. This is all well and good. The problem comes when you want your Linux VM to have different display properties than your host PC.

In short, it’s tough. The guest XFree86 server starts out by exactly conforming to the specifications of your host’s XFree86 server. To make any changes, you will need to edit the file `/etc/X11/XF86config.vm` in your virtual machine.

Note that you cannot alter the color depth that the virtual machine runs in, only the resolution.

Open `/etc/X11/XF86config.vm` in a text editor, and scroll to the very last section, which should be introduced with

```
Section "Screen"
    Driver "accel"
```

You should see several lines starting with `Modes`, but only one will not have a `#` in front of it (indicating that it is uncommented, and the only line read by the guest’s X server at startup). Modify that line to include any screen resolutions you want to make available to the virtual machine. Be sure each entry is enclosed in quotes and separated by a space. They should be valid screen resolutions for your monitor and display card, preferably standard modes also in use by the host X server.

A line like

```
Modes "1024x768" "800x600" "640x480"
```

is functional and practical.

根据虚拟机的配置，程序可能不在你的默认路径中。如果需要使用完整路径，输入

`/usr/X11R6/bin/vmware-toolbox &`。

你应该在每次运行 Linux 虚拟机时启动 VMware Tools，并在整个会话期间保持其打开状态。当你熟练后，你可能想考虑将该命令添加到你的 Linux 或 XWindows 启动脚本中。

Linux 中的 VMware Tools 窗口在功能上几乎与 Windows 版本相同，并且与 Windows 版本一样，它提供了在其他任何设置菜单中都不可用的某些功能。

## 管理虚拟设备

VMware Tools（见图 10.17）提供了对 VMware 窗口工具栏中也能找到的 Devices 设置的更便捷访问。在全屏模式下，工具栏无法访问，这使得 VMware Tools 成为在不通过 `Ctrl+Alt+Esc` 返回窗口模式的情况下附加和释放设备唯一的方法。

此屏幕控制四种类型的虚拟设备：

- RTC，即实时时钟。所有 PC 都有 RTC 设备，但 VMware 必须共享良好的计时带来的好处。通常，你应该保持此设置不变。（换句话说，保持虚拟机连接到 RTC。）

![](img/b2b6702758c230ce537468351fc8af15_202_0.png)

图 10.17 在 Corel Linux 上运行的 Linux 版 VMware Tools。

## 第 10 章：在 VMware 上安装 Linux

- 软盘驱动器，通常从 `floppy0` 开始。除非你有一个顽固的已挂载软盘无法移除，否则你不需要使用此设置。

- IDE 或 SCSI 连接的光驱。由于 Linux（主机和客户机！）处理光驱的方式，在某些情况下你可能无法弹出或卸载光驱。如果发生这种情况，只需点击正确的条目以断开驱动器，在 Linux 主机中如有必要卸载光驱，更换光盘，然后再次点击重新连接驱动器。

> 这是一个 VMware 窗口上的 Devices 菜单比使用 VMware Tools 更有帮助的情况。如果你连接了多个光驱，但根据它们的 IDE 或 SCSI 地址不知道哪个是哪个，请使用 Devices 菜单。它会列出它们的 Linux 路径（如 `/dev/cdrom`）以及它们的 SCSI 地址。如果你计划保持 VMware 配置相对一致，你可能想记录哪个光驱连接到设备链上的哪个地址。

- 声音。VMware 将你的系统主音量与虚拟机的主音量绑定在一起，因此你可以使用虚拟机的混音器作为静音按钮。但如果你需要阻止 VM 访问音频设备（例如它会减慢你的计算机速度），点击此设置会切断音频访问。

> 输入焦点：确定虚拟机还是主机 Linux 操作系统捕获鼠标和键盘输入。当你向 VMware 主持的操作系统和应用程序中输入内容时，称 VMware 拥有输入焦点。

### 使用工具箱选项

选项选项卡，如图 10.18 所示，可帮助你微调 VMware 的输入焦点设置。

1. 选择一个选项以启用它。
2. 当鼠标离开虚拟机时释放输入焦点。
3. 当鼠标进入虚拟机时捕获输入焦点。
4. 当虚拟机失去输入焦点时保持居中。
5. 当获得输入焦点时将虚拟机置于顶层。
6. 当获得输入焦点时允许复制和粘贴置于顶层。

![](img/b2b6702758c230ce537468351fc8af15_203_0.png)

此功能在虚拟机处于全屏模式时不起作用，因为在你通过按 `Ctrl+Alt+Esc` 退出全屏模式之前，鼠标始终位于虚拟机内部。

### 当鼠标接近边缘时滚动

你只有在虚拟机桌面大于 Linux 桌面上的 VMware 窗口时才需要担心“当鼠标接近边缘时滚动”这一功能。这种情况可能发生在你临时缩小 VMware 窗口时，或者当你使用比计算机能显示的更大的虚拟机桌面时（例如，在桌面仅为 `800×600` 的 Linux PC 上使用 `1,280×1,024` 的 Linux 桌面）。

> 如果你想能够即时更改 VMware 窗口的大小，你需要在 VMware 窗口设置中在 View 下禁用 Autofit。请注意，这不会影响客户操作系统桌面本身的大小，只会影响你一次能看到多少内容。

### 隐藏光标

“隐藏光标”选项不过是一个花哨的“鼠标空白器”，但它可以帮助避免在同一屏幕上看到两个鼠标指针造成的混淆。当启用时，如果输入焦点在主机而不是 VMware 上，虚拟机中的鼠标指针就会消失。

> 如果你关闭此选项，客户机的指针将在你将输入焦点切回主机时保持在它所在的位置。如果你离开屏幕然后返回，在你实际开始移动鼠标之前，你可能会对哪个是活动鼠标指针感到困惑。

### 将虚拟机置于顶层

“将虚拟机置于顶层”选项默认关闭。开启时，只要 VMware 获得输入焦点，就会立即将 VMware 窗口带到前台。如果你桌面杂乱，手动将 VMware 窗口置顶可能很困难，你可能想打开此选项。

> 继续尝试这些光标选项的混搭组合，直到找到最适合你使用 VMware 和主机 PC 方式的设置。

### 允许复制和粘贴

默认情况下，VMware Tools 允许你在主机和虚拟机之间共享剪贴板，理论上这让你可以在不同操作系统间无缝地在应用程序之间剪切和粘贴。某些应用程序不会按预期读取剪贴板，文本剪切粘贴通常比图形剪切粘贴效果更好。在对文档进行大幅修改之前，先测试共享剪贴板的性能。

如果你对主机计算机的安全性有顾虑，不希望鼓励信息在主机操作系统和虚拟机之间的边界流动，你可能想要关闭“允许复制和粘贴”选项。或者你可能只是想让两个剪贴板保持分离，因为你在主机和虚拟机中进行的工作项目不同，需要各自独立、私有的剪贴板。

## 时间同步
