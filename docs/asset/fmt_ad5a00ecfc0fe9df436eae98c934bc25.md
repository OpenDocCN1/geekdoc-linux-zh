
S 脚本按此顺序启动，直到所有脚本启动完毕。当系统关闭时，相应的 K 或 kill 脚本将运行以关闭 rc 目录中的服务。通常情况下，每个脚本都应该有一个对应的 K 脚本在关机时杀死该服务。

如果你在启动目录中找不到对应的脚本，它可能位于运行级别 6 中。大多数脚本都在 `/etc/rc6.d` 中。图 8-3 显示了一个典型的 `/rc6.d` 目录列表。

图 8-2 rc3.d 目录的目录列表。

图 8 `/etc/rc6.d` 目录的列表。

如果你需要重启一个从 rc 目录启动的服务，正确执行此操作的简单方法是在其启动脚本中使用 `restart` 选项。此过程可以确保遵循所有步骤（配置文件、日志记录、锁文件等）。因此，要重启 syslog，请从 rc 目录运行以下命令：

```
root@terry rc6.d]# ./Syslog restart
Shutting down kernel logger:  [ OK ]
Shutting down system logger: [ OK ]
Starting system logger:      [ OK ]
Starting kernel logger:      [ OK ]
```

## 使用 chkconfig 管理 rc 脚本

Fedora 和 Red Hat Enterprise Linux 附带了一个名为 `chkconfig` 的有用工具。它可以帮助系统管理员管理 rc 脚本和 xinetd 配置文件，而无需直接操作它们。它的灵感源于 IRIX 操作系统中的 `chkconfig` 命令。

输入 `chkconfig --list` 可以查看 `chkconfig` 已知的所有服务，以及它们在每个运行级别下是启动还是停止状态。简写后的输出如下列表所示。`chkconfig` 的输出可能比这里列出的长得多，因此请准备对其进行解析。

第一列是已安装服务的名称。接下来的七列每列代表一个运行级别，并告诉你在该运行级别下哪个服务是开启或关闭的。

由于在提取 `chkconfig` 输出的系统上启动了 `xinetd`，因此 `chkconfig` 报告的末尾列出了配置为在引导时启动的 `xinetd` 服务。该列表是桥接的，因为 `xinetd` 可以启动许多服务，没有必要显示所有服务。

列表 8-11 显示了 `chkconfig` 如何成为处理所有网络服务并控制哪些服务在引导时启动的有效工具。这是 `chkconfig --list` 的输出：

```
atd         0:off 1:off 2:off 3:on  4:off 5:off 6:off
rwhod      0:off 1:off 2:off 3:off 4:off 5:off 6:off
keytable    0:off 1:off 2:on  3:off 4:off 5:off 6:off
nscd       0:off 1:off 2:off 3:off 4:off 5:off 6:off
syslog      0:off 1:off 2:on  3:off 4:off 5:off 6:off
gpm        0:off 1:off 2:off 3:off 4:off 5:off 6:off evenkudru      0:off 1:off 2:off 3:off 4:off 5:off 6:off
kdrocrate   0:off 1:off 2:off 3:off 4:off 5:off 6:off
lpd        0:off 1:off 2:off 3:off 4:off 5:off 6:off
autofs      0:off 1:off 2:off 3:off 4:off 5:off 6:off
sendmail   0:off 1:off 2:off 3:off 4:off 5:off 6:off
rnhsd       0:off 1:off 2:off 3:off 4:off 5:off 6:off
network      0:off 1:off 2:off 3:off 4:off 5:off 6:off
netfs       0:off 1:off 2:off 3:off 4:off 5:off 6:off
random      0:off 1:off 2:off 3:off 4:off 5:off 6:off
rexec       0:off 1:off 2:off 3:off 4:off 5:off 6:off
rsync       0:off 1:off 2:off 3:off 4:off 5:off 6:off
rwhod       0:off 1:off 2:off 3:off 4:off 5:off 6:off
time        0:off 1:off 2:off 3:off 4:off 5:off 6:off
xinetd       0:off 1:off 2:off 3:off 4:off 5:off 6:off
ypbind      0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

## 更改显示分辨率

X 配置工具可以让你轻松更改显示分辨率。要更改显示分辨率，请执行以下操作：

- 1. 在 Enterprise Linux 4 上，选择应用程序（Applications）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框，如图 9-1 所示。在 Fedora Core 4 上，选择桌面（Desktop）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框。

> 注意：如果您没有以 root 身份登录，系统将提示您输入 root 密码。

- 2. 从分辨率（Resolution）下拉菜单列表中选择您所需的分辨率。

- 3. 点击 OK 接受您的选择并关闭对话框。

> 注意：每当您对 X 服务器配置进行更改时，必须重启 X 服务器才能使更改生效。当使用 X 配置工具时，您会看到一个窗口提醒您重启 X 服务器。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_242_0.png)

图 9-1 在此处更改屏幕分辨率。

## 管理 X Window 系统

### 更改显示色彩深度

系统色彩深度设置决定了显示器上显示的颜色数量。较高的色彩深度会在显示器上显示更多颜色。要更改系统色彩深度，请执行以下操作：

- 1. 在 Enterprise Linux 4 上，选择应用程序（Applications）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框。在 Fedora Core 4 上，选择桌面（Desktop）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框（参考图 9-1）。

- 2. 从色彩深度（Color Depth）下拉列表中选择您所需的色彩深度。

- 3. 点击 OK 接受您的选择并关闭对话框。

### 更改显示器类型设置

Fedora Core 或 Enterprise 安装程序通常可以检测连接到系统的显示器类型并进行相应的配置。有时，安装程序可能无法正确配置您的显示器，需要您手动更改显示器设置。如果您获得了一个参数与之前不同的新显示器，您也需要更改显示器设置。要更改显示器设置，请执行以下操作：

- 1. 在 Enterprise Linux 4 上，选择应用程序（Applications）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框。在 Fedora Core 4 上，选择桌面（Desktop）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框（参考图 9-1）。

- 2. 点击硬件（Hardware）选项卡。（见图 9-2）。

- 3. 点击顶部的配置（Configure）按钮（显示器类型列表右侧），打开显示器对话框，如图 9-3 所示。

- 4. 在列表中找到您的显示器制造商，点击名称旁边的箭头查看型号列表。

- 5. 点击与您的显示器匹配的型号数字。

- 6. 双击 OK 接受您的选择并退出显示设置对话框。

> 提示：如果从显示器列表中找不到您的显示器制造商或型号数字，请从顶部列表中选择一个通用显示器。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_244_0.png)

图 9-2 访问显示器和显卡设置。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_244_1.png)

图 9-3 选择您的显示器类型。

### 更改显卡类型

Fedora Core 或 Enterprise 安装程序通常可以检测连接到系统的显卡类型并进行相应的配置。然而，如果安装程序未能正确检测到显卡，您可能需要更改显卡类型。如果您安装了不同的显卡，也需要更改显卡类型。要更改显卡类型，请执行以下操作：

- 1. 在 Enterprise Linux 4 上，选择应用程序（Applications）-> 系统设置（System Settings）-> 显示（Display），打开显示设置框。在 Fedora Core 4 上，选择桌面（Desktop）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框。（参考图 9-1。）

- 2. 点击硬件（Hardware）选项卡。（参考图 9-2）。

- 3. 点击底部的配置（Configure）按钮（显卡类型列表右侧），显示显卡对话框，如图 9-4 所示。

- 4. 在列表中找到您的显卡制造商，并点击相应的型号。

### 配置双显示器

在 Fedora Core 或 Enterprise Linux 中，如果需要，您可以在系统上使用两个显卡和显示器。要配置第二个显卡和显示器，请执行以下操作：

- 1. 在 Enterprise Linux 4 上，选择应用程序（Applications）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框。在 Fedora Core 4 上，选择桌面（Desktop）-> 系统设置（System Settings）-> 显示（Display），打开显示设置对话框。（参考图 9-1）。

- 2. 在显示设置对话框中点击双头（Dual Head）选项卡，如图 9-5 所示。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_245_0.png)

![](img/b5ebc2d43ffbc3488ca0205212f962cb_246_0.png)

图 9-5 使用双显示器。

- 3. 选择双头（Dual Head）选项卡。

- 4. 点击配置（Configure）按钮（显示器类型列表右侧）。

- 5. 为第二个显示器选择显示器类型。

- 6. 选择与您的显示器匹配的型号数字。

- 7. 双击 OK 接受您的选择并退出显示设置对话框。

> 提示：如果从显示器列表中找不到您的显示器制造商或型号数字，请从顶部列表中选择一个通用显示器。

### 手动配置 X 服务器

X 服务器配置文件位于 `/etc/X11/xorg.conf`。这是一个可以使用任何文本编辑器编辑的文件。该文件包含多个部分，定义了您的 X 服务器的硬件和软件。最重要的部分是 `InputDevice`、`Device`、`Screen` 和 `Resource` 部分。

`InputDevice` 部分定义输入设备（如键盘和鼠标）。`Device` 部分定义硬件设备（如显卡）。`Screen` 部分定义显示及其属性。`Resource` 部分定义其他 X 服务器资源（如字体和光标）。

以下是一个典型的 `xorg.conf` 文件示例：

```text
Section "InputDevice"
    Identifier      "Keyboard0"
    Driver          "kbd"
    Option          "Device"      "/dev/input/event3"
End

Section "InputDevice"
    Identifier      "Mouse0"
    Driver          "mouse"
    Option          "Device"      "/dev/input/event4"
End

Section "Device"
    Identifier      "VideoCard0"
    Driver          "card0"
End

Section "Screen"
    Identifier      "Screen0"
    Driver          "modes"
    SubSection      "DevicesConfig0"
        DefaultDepth    24
    EndSub
```

您可以通过修改 `xorg.conf` 文件来自定义您的 X 服务器。编辑此文件时务必小心，因为语法错误可能会导致 X 服务器无法启动。

## 管理 X Window 系统

| VendorName | *显示器厂商* |
| :--- | :--- |
| ModelName | *LCD面板 1280x1024* |
| DisplaySize | 376 301 |
| HorizSync | 31.5 - 67.0 |
| VertRefresh | 50.0 - 75.0 |
| Option | *dpms* |

Section "Device"

| Identifier | *Videocard0* |
| Driver | *nv* |
| VendorName | *显卡厂商* |
| BoardName | *NVIDIA GeForce 2 MX (generic)* |
| VideoRam | 32768 |

Section "Screen"

| Identifier | *Screen0* |
| Device | *Videocard0* |
| Monitor | *Monitor0* |
| DefaultDepth | *显示* |
| Depth | 24 |
| Modes | *1024x768* *800x600* *640x480* |

Section "DRI"

| Group | 0 |
| Mode | 0666 |

**表 9-1（续）**

此文件包含系统使用的字体、键盘类型和布局，以及显卡、显示器和显示器的配置信息。文件中为这些项目每个提供了一个节。节及其用途如表 9-1 所示。

**表 9-1** 节名称及其用途

| 节名称 | 用途 |
| :--- | :--- |
| Files | 字体文件路径 |
| Server Flags | 服务器标志 |
| Module | 动态模块加载 |
| 节名称 | 用途 |
| :--- | :--- |
| Input Device | 键盘、鼠标和其他输入设备 |
| Device | 显卡信息 |
| VideoAdapter | 未使用 |
| Monitor | 显示器描述 |
| Modes | 视频模式描述 |
| Screen | 显示配置 |
| Server Layout | X 服务器的总体描述 |
| DRI | 直接渲染基础设施信息 |

列表 9-2 是屏幕部分节的节列表。每个节都遵循相似的模式，以 `Section` 单词开头，随后是设备的名称、关于设备的信息或配置细节，最后以 `EndSection` 结束。

```
Section "Screen"
Identifier "Screen0"
Device "Videocard0"
Monitor "Monitor0"
DefaultDepth 24
SubSection "Display"
Depth 24
Modes *1024x768* *800x600* *640x480*
EndSection
```

### 列表 9-2 xorg.conf 文件的典型节。

修改 `xorg.conf` 文件很容易。例如，要更改默认色彩深度，只需将列表 9-2 显示的 `DefaultDepth 24` 改为 8、16 或 32 即可。

`modes` 行指定了 X 服务器将尝试使用的屏幕尺寸（以像素为单位），从第一个开始。如果你想添加另一个屏幕分辨率，可以在显示子节的 `Modes` 行中输入信息。例如，如果你想添加 1200 × 1024，则在 `Modes` 行的开头输入 `1200x1024`。

> 注意 你可以通过按住 Ctrl+Alt 并按下加号或减号在不同模式之间切换。

## 管理 X Window 系统

现在你已经知道如何更改 `/etc/X11/xorg.conf` 文件中的屏幕部分。更改其他节中的信息也是类似的。
