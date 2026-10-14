
## 第四部分：删除复制的文件并清空回收站

要删除复制的文件并清空回收站，请执行以下操作：

- 1. 通过将文件图标拖到桌面上的回收站图标上并释放鼠标按钮来删除 example.txt 文件。
- 2. 关闭 Nautilus 文件管理器窗口。
- 3. 在桌面上右键单击回收站图标，从弹出菜单中选择“清空回收站”。
- 4. 在确认对话框中，选择“清空回收站”。

## 目标 3—从桌面访问命令行界面

经典的多用户环境可以通过将多个终端（对话站）——显示器和键盘单元——连接到单台计算机的串行接口来实现。Linux 也支持多终端环境，允许您将多个终端连接到 Linux 系统的串行接口。

串行终端很少使用；相反，Linux 中创建了虚拟终端。有了虚拟终端，您就可以在 Linux 中工作，就好像同时有多个经典串行终端可用一样。

您的计算机上可以同时运行多达六个虚拟终端（F1-F6）。通过按 Ctrl+Alt+Fx，您可以在各个终端之间切换。通过按 Ctrl+Alt+F7，您可以切回图形用户界面。

您可以通过 tty 编号（tty1–tty6）确定当前使用的终端。tty 是电传打字机的缩写，电传打字机是终端的另一个词。

当您切换到虚拟终端时，会出现登录提示：

```
Welcome to SUSE Linux Enterprise Desktop 10 (i586) -
Kernel 2.6.16.46-0.4-default (tty1).
dalo login:
```

从这里您可以输入您的登录名和密码。要注销，请键入 exit 并按 Enter。

除了使用虚拟终端之外，您还可以通过从主菜单中选择 GNOME Terminal（见图 2-18）或 X Terminal 从 GNOME 桌面启动终端仿真。两者都属于系统应用程序组。

![](img/9129877170834ca9d5fdac5319bf5f12_84_0.png)

图 2-18

终端在窗口内打开。它包含可用于修改终端显示的菜单（例如字体或背景颜色）。

您还可以通过右键单击桌面背景并选择“打开终端”来启动 GNOME Terminal。

![](img/9129877170834ca9d5fdac5319bf5f12_84_1.png)

## 练习 2-4：访问命令行界面

在本练习中，以用户 geeko 在第一个虚拟终端登录。然后，切换到第二个虚拟终端并验证那里是否显示登录提示。在切回图形用户界面之前，从第一个虚拟终端注销。

### 完成此练习的详细步骤

- 1. 通过按 **Ctrl+Alt+F1** 切换到第一个虚拟终端
- 2. 输入 `geeko` 作为登录名；然后按 **Enter**。
- 3. 输入 `novell` 作为密码；然后按 **Enter**。
- 4. 通过按 **Ctrl+Alt+F2** 切换到第二个虚拟终端
  请注意，您在此终端上未登录。
- 5. 通过按 **Ctrl+Alt+F1** 切回第一个终端
  您仍然以 geeko 登录。
- 6. 通过输入 **exit** 注销
- 7. 通过按 **Ctrl+Alt+F7** 切回图形用户界面

![](img/9129877170834ca9d5fdac5319bf5f12_85_0.png)

准确地说，使用虚拟终端时，实际上不需要按 Ctrl 键来切换到另一个虚拟终端或切回图形界面。仅在从图形屏幕切换到虚拟终端时才真正需要它。

## 摘要

- 您可以使用图形或命令行界面与 Linux 系统交互。
- Linux 图形界面由 X Window System 提供，X Window System 由 X 服务器和客户端应用程序组成。
- SUSE Linux 使用的 X 服务器是 X.org，并使用 TCP/IP 协议与客户端应用程序通信。因此，X 服务器和客户端应用程序可能位于网络上的不同计算机上。
- SUSE Linux 中 X Window System 使用的默认客户端应用程序是 Metacity 窗口管理器。窗口管理器控制 X Window System 的外观和感觉。
- 可以在窗口管理器之外使用 KDE 或 GNOME 等桌面环境来标准化 X Window System。SUSE Linux 中的默认桌面环境是 GNOME。
- GNOME 桌面底部面板上的“计算机”菜单可用于启动应用程序、搜索文件、配置系统设置以及关闭或休眠系统。GNOME 中的默认文件浏览器是 Nautilus。
- 您可以通过与其中一个虚拟终端交互在 SUSE Linux 中获得命令行界面。要启动虚拟终端，您可以使用 Ctrl+Alt+Fx 键组合，其中 x 为 1 到 6 之间的数字。或者，您可以在 GNOME 桌面中调用 GNOME Terminal 或 X Terminal 应用程序，以在桌面环境中获得命令行界面。
- 要从命令行界面切换到 GUI 界面，您可以使用 Ctrl+Alt+F7 键组合。

## 关键术语

- **client application**  接收来自 X 服务器的键盘和鼠标输入并将屏幕输出发送到 X 服务器的应用程序。它可以在与 X 服务器相同或不同的计算机上运行。也称为 X 客户端。
- **desktop**  图形用户界面使用的主工作区。在 GNOME 中，桌面指的是所有工作区，包括面板。
- **desktop environment**  一组标准化桌面外观和感觉的软件组件。大多数 Linux 发行版中提供两种标准的 GUI 桌面环境：KDE 和 GNOME。
- **GNOME**  一种常见的 Linux 桌面环境，使用 GNOME 窗口管理器。GNOME 是 GNU Object Model Environment 的缩写。
- **GNOME Terminal**  可以从 GNOME 桌面环境内部启动的虚拟终端。
- **GNOME window manager**  参见 Metacity。
- **graphical user interface (GUI)**  一种图形界面，允许用户通过操作图标来控制操作系统并运行应用程序。
- **KDE**  一种常见的 Linux 桌面环境，使用 KDE 窗口管理器。KDE 是 K Desktop Environment 的缩写。
- **Metacity**  SUSE Linux 中 GNOME 桌面环境使用的默认窗口管理器。
- **Nautilus**  GNOME 中包含的默认文件导航实用程序。
- **panel**  GNOME 桌面底部的栏，用于打开菜单、切换虚拟桌面和启动应用程序。
- **Tab window manager (twm)**  一个小型独立窗口管理器，使用少量系统资源，可替代 KDE 或 GNOME 桌面使用。
- **TCP/IP**  Linux 系统使用的默认网络协议。它代表传输控制协议/互联网协议。
- **virtual desktops**  您可以在 KDE 或 GNOME 等桌面环境中使用的单独工作区。
- **virtual terminals**  允许您登录并与命令行用户界面交互的系统组件。大多数 Linux 系统默认可使用并在六个虚拟终端之间切换（tty1–tty6）。
- **window manager**  X Window System 的组件，控制桌面上窗口的外观和感觉。
- **X**  参见 X Window System。
- **X11**  参见 X Window System。
- **X server**  X Window System 的组件，接收来自客户端应用程序的信息并将图形图像绘制到屏幕上。
- **X terminal**  可以从 GNOME 桌面环境内部启动的虚拟终端。
- **X Window System**  提供 Linux 中图形用户界面的软件组件集。也称为 X 或 X11。

![](img/9129877170834ca9d5fdac5319bf5f12_86_0.png)

**XFree86**  旧版 Linux 系统上使用的传统 X 服务器。

**X.org**  SUSE Linux 使用的默认 X 服务器。

### 复习题

- 1. 哪个 X Window System 组件用于在屏幕上绘制实际的图形图像？
  a. X server
  b. Window manager
  c. Client application
  d. Desktop environment
- 2. 哪个 X Window System 组件用于更改窗口框架的大小？
  a. Desktop environment
  b. Client application
  c. Window manager
  d. X server
- 3. SUSE Linux 中有哪些两种桌面环境？____________________
- 4. 桌面环境的主要目的是什么？
  a. 它提供控制桌面上窗口的元素
  b. 它标准化桌面的外观和感觉
  c. 它允许您使用虚拟桌面
  d. 它管理窗口框架的大小
- 5. SUSE Linux 中的默认桌面环境是什么？____________________
- 6. 以下哪些陈述是正确的？（选择两个答案。）
  a. X 服务器和客户端应用程序必须驻留在同一台计算机上
  b. X 服务器和客户端应用程序通常驻留在同一台计算机上
  c. X 服务器和客户端应用程序使用 TCP/IP 协议通信
  d. X 服务器和客户端应用程序必须使用窗口管理器通信
- 7. 在 GNOME 桌面环境中使用“计算机”菜单可以执行以下哪些操作？（全部选择。）
  a. 创建桌面快捷方式
  b. 启动应用程序
  c. 搜索文件
  d. 休眠系统
