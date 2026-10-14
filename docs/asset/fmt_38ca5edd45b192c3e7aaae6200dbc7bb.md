
![](img/9129877170834ca9d5fdac5319bf5f12_566_0.png)

## 自定义 SUSE Linux Enterprise Desktop 10 上的图形界面

在本节中，您学习如何配置 SUSE Linux Enterprise Desktop 的图形环境。这包括 X 配置以及 GNOME 环境的配置。

## 目标

- 目标 1—配置 X、Xgl 和 Compiz
- 目标 2—自定义 GNOME 用户界面
- 目标 3—使用 GConf 和桌面配置文件编辑器定义强制设置
- 目标 4—自定义应用程序
- 目标 5—控制 CD-ROM、DVD 和 USB 设备的挂载

## 目标 1—配置 X、Xgl 和 Compiz

只要计算机配备了合适的图形硬件（支持的图形适配器且具有良好的 3D 性能），SUSE Linux Enterprise Desktop 10 就能通过 Xgl 和 Compiz 提供的 3D 效果提供全新的 Linux 桌面体验。参见图 14-1。

![](img/9129877170834ca9d5fdac5319bf5f12_567_0.png)

图 14-1

Xgl 是一个构建在 OpenGL 之上的新 X Server 架构。Xgl 可以比不使用 OpenGL 的其他可用 X Server 更快地执行复杂的图形操作。更重要的是，除了速度之外，Xgl 还加速了复杂的合成操作，使得在 OpenGL 增强的合成/窗口管理器（如 Compiz）上实现新的惊人视觉效果成为可能，Compiz 是与 Xgl 协同开发的合成器实用程序。Compiz 是一个使用 OpenGL 进行渲染的窗口管理器和合成管理器的组合。窗口管理器允许操作屏幕上显示的多个应用程序和对话框窗口。合成管理器允许将窗口和其他图形组合起来创建合成图像，例如用于创建透明效果的图像。Compiz 通过执行这两个功能实现了其惊人的效果。

当您激活 Compiz 时，它会替换桌面环境的窗口管理器（GNOME 中的 Metacity 和 KDE 中的 kwin）。

要启用这些桌面效果，您必须：

- 配置 X
- 激活 Compiz

### 配置 X

在大多数情况下，X 在安装期间由 YaST 自动配置。如果没有，或如果您想更改配置，您可以使用以下任一方法：

- YaST Graphics Card and Monitor Module
- `sax2`

#### YaST Graphics Card and Monitor Module

YaST Graphics Card and Monitor 模块使用 `sax2` 进行 X 配置。为了能够使用 Compiz，请通过选中 Activate 3D Acceleration 选项来激活 3D 加速，如图 14-2 所示的对话框中所示。

![](img/9129877170834ca9d5fdac5319bf5f12_568_0.png)

图 14-2

#### sax2

也可以直接使用 `sax2`，而不通过 YaST。最好在运行级别 3 的文本终端中启动 `sax2`。这可避免与当前运行的 X 会话发生可能的干扰。

首先，`sax2` 检查硬件；然后会出现图 14-3 所示的对话框。

![](img/9129877170834ca9d5fdac5319bf5f12_569_0.png)

图 14-3

如果您对配置满意，请选择 OK。

如果需要更改配置，请选择 Change Configuration。除了窗口标题外，打开的对话框与图 14-4 所示的 YaST Graphics Card and Monitor 模块的对话框相同。

![](img/9129877170834ca9d5fdac5319bf5f12_569_1.png)

图 14-4

在 Monitor 部分，您可以更改与显卡和显示器相关的 X 配置的各个方面（例如显卡详细信息、显示器类型、屏幕分辨率和显示的颜色数）。

选择左侧的类别之一会打开不同的对话框，允许您更改相应的设置。

配置完成后，选择 OK。在下一个对话框中，您可以选择测试配置、保存它或取消更改。我们建议在保存之前先测试配置。如果测试显示配置可用，请保存并退出 `sax2`。

### 激活 Compiz

激活 Compiz 所需的软件包是默认安装期间使用的 GNOME 模式的一部分。这些包括：

- `compiz`
- `Xgl`
- `Xgl-hardware-list`
- `gnome-session`
- `libwnck`

在激活 3D 加速后，以普通用户身份登录 GNOME 并激活 Compiz。

选择桌面左下角的计算机图标，打开 GNOME 控制中心，并启动桌面特效控制面板。打开 GNOME 终端并输入 `gnome-Xgl-settings` 具有相同的效果。

视频卡列在 3D 桌面选项卡上。该选项卡还指示您的显卡是否受支持。如果受支持，并且已启用 3D 加速，请选择启用桌面特效。系统会提示您输入 root 密码，然后您将被注销 GNOME 会话。

再次登录后，Compiz 将被激活，让您可以探索桌面特效。要配置特效和键组合，再次启动桌面特效控制面板。3D 桌面选项卡现在可让您禁用 Compiz，而其余选项卡可让您打开或关闭某些特效，并可更改控制特效的键组合。表 14-1 列出了更常用的控件。

| 键组合 | 特效 |
|---|---|
| Ctrl+Alt+Left | 向左旋转立方体。 |
| Ctrl+Alt+Shift+Left | 旋转立方体向左，并带活动窗口。 |
| Ctrl+Alt+Right | 向右旋转立方体。 |
| Ctrl+Alt+Shift+Right | 旋转立方体向右，并带活动窗口。 |
| Ctrl+Alt+鼠标按键 1 | 使用鼠标旋转立方体。 |
| Ctrl+Alt+Down | 展开立方体；然后使用左右箭头键移动。 |
| Pause | 安排窗口以便您可以全部看到；通过单击按键 1 选择窗口。 |

表 14-1

![](img/9129877170834ca9d5fdac5319bf5f12_571_0.png)

有关 Xgl 的更多信息，请访问 http://en.opensuse.org/Xgl。有关 Compiz 的更多信息，请访问 http://en.opensuse.org/Compiz。

![](img/9129877170834ca9d5fdac5319bf5f12_571_1.png)

## 练习 14-1：激活 Compiz（可选，取决于硬件支持）

在此练习中，您配置 Compiz，前提是硬件支持它。在第一部分，使用 YaST 验证图形适配器的 3D 支持是否已启用。

如果启用了 3D 支持，则在第二部分为 GNOME 桌面激活 Compiz。

### 完成此练习的详细步骤

- 第 I 部分：验证 3D 支持
- 第 II 部分：激活 Compiz

### 第 I 部分：验证 3D 支持

要验证 3D 支持，请执行以下操作：

1. 启动 YaST 控制中心并选择 硬件 > 图形卡和显示器。SaX2 X11 配置对话框出现。
2. 颜色深度应设置为 16.7 Mio.（24 位），并且在对话框底部，激活 3D 加速选项应被选中。如果颜色深度设置正确并且已选中 3D 加速，请选择取消离开对话框。
3. 将颜色深度更改为 24 位，如果未选中激活 3D 加速并且未变灰，请选择激活 3D 加速；然后选择确定。
4. 如果激活 3D 加速变灰，请找出您的图形适配器是否支持 3D 加速。打开一个终端窗口并输入 `/sbin/lspci` 命令。记下图形适配器的型号。
5. 以下步骤取决于硬件。对于 Nvidia 图形卡：

   a. 以 root 身份登录并通过在终端窗口中输入以下内容安装 tiny-nvidia-installer 软件包：

   b. 从 GNOME 桌面注销。

   c. 切换到文本控制台（Ctrl+Alt+F1），以 root 身份登录，并通过输入 `init 3` 更改为运行级别 3。

   d. 在文本控制台窗口中，输入

```
yast -i tiny-nvidia-installer
```

```
tiny-nvidia-installer --update
```

请注意，这可能包括必须安装 gcc 和内核源代码并编译内核模块，所有这些都超出了本课程的范围。 （注意：要手动下载 Nvidia 图形驱动程序，请访问 http://www.nvidia.com/content/drivers/drivers.asp。）

对于 ATI 图形卡：

- a. 从 http://ati.amd.com/support/driver.html 下载驱动程序。
- b. 打开一个终端窗口并 `su -` 到 root（密码 n0v311）。更改到保存文件的目录。通过输入执行文件

  `sh ati-driver-install*run`

  按照说明操作。

  请注意，这可能包括必须安装 gcc 和内核源代码并编译内核模块，所有这些都超出了本课程的范围。
