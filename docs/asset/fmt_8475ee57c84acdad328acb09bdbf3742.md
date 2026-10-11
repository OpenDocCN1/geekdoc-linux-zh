
`desktop environment` — 与窗口管理器配合工作，提供使用标准程序和开发工具的标准 GUI 环境的软件。

`Desktop Switching Tool` — 允许 Red Hat Linux 用户设置默认桌面环境或窗口管理器的图形工具。

`Enlightenment Window Manager` — Linux 系统上常用的窗口管理器。

`Feeble Virtual Window Manager` (`fvwm`) — Linux 系统上常用的窗口管理器。

`GDM Configurator` — 用于配置 GNOME 显示器管理器（GNOME Display Manager）外观和行为的图形工具。

`GNOME Desktop Environment` — Red Hat Linux 的默认桌面环境；创建于 1997 年。

`GNU Image Manipulation Program` (`GIMP`) — 一个使用 `GTK+` 工具包的开源图形处理程序。

`GTK+ toolkit` — 用于 C 语言编程的开发工具包；用于 GNOME 桌面和 GNU 图像处理程序 (`GIMP`)。

`K Window Manager` (`kwm`) — 在 KDE 环境下运行的窗口管理器。

`KDE Desktop Environment` — 由 Matthias Ettrich 于 1996 年创建的桌面环境。

`KDE Display Manager` (`kdm`) — 为用户提供的图形登录界面，类似于 KDE 桌面。

## 复习题

`maximum resolution` — 绘制到屏幕上的图像的最佳清晰度；它由图像所使用的像素数量决定（例如 640 × 480 像素）。

`mouseconfig` — 用于为 X Windows 配置鼠标的命令。

`Qt toolkit` — 与 KDE 桌面环境配合使用的软件工具包。

`RAM Digital Analog Converter` (`RAMDAC`) chip — 将计算机使用的数字图像转换为显示器所需的模拟格式。

`Sawfish Window Manager` — 在 GNOME 桌面环境下运行的窗口管理器。

`startx` — 用于启动 X Windows 以及相关的窗口管理器和桌面环境的命令。

`SuperProbe` — 用于确定计算机视频适配卡属性的程序。

`Tab Window Manager` (`twm`) — Linux 系统上最老的窗口管理器之一。

`Window Maker Window Manager` — Linux 系统上常用的窗口管理器。

`window manager` — 负责决定 X Windows 在屏幕上绘制的窗口外观的 GUI 组件。

`X client` — X Windows 的组件，用于向 `X server` 请求绘制图形并将其显示在终端屏幕上。

`X server` — X Windows 的组件，负责在终端屏幕的窗口上绘制图形。

`X Windows` — Linux GUI 的组件，用于在终端屏幕上显示图形。

`X Display Manager` (`xdm`) — 为用户提供图形登录界面。

`Xconfigurator` — 用于配置 X Windows 使用的视频适配卡和显示器信息的程序。

`xf86config` — X Windows 自带的基于文本的 X 配置程序；允许配置供 X Windows 使用的键盘、鼠标、视频适配器显示器信息。

`XFree` — X Windows 版本 11 的开源许可版本。

`xvtune` — 用于精调 X Windows 中使用的 `vsync` 和 `hsync` 显卡设置的程序。

## 复习题

1. `X server` 告诉 `X clients` 绘制图形并将结果显示在屏幕上。正确或错误？

2. 下列哪些是 Linux GUI 的组件？（选择所有适用项）：

   a. `Xconfigurator`
   b. `X Windows`
   c. `X server`
   d. `X client`
   e. `Sawfish`
   f. `gpm`
   g. `window manager`
   h. `vidtune`
   i. `desktop environment`

3. Linux GUI 在设计时考虑了许多不同的组件，这些组件能够独立于彼此，并能与所使用的视频硬件独立工作。正确或错误？

4. 下列哪项是通往安装期间配置的鼠标的实际设备文件的符号链接？

   a. `/dev/term/mouse`
   b. `/dev/serial/mouse`
   c. `/dev/ps2/mouse`
   d. `/dev/mouse`

5. 下列哪项不是窗口管理器？

   a. `Freewindow`
   b. `GNOME`
   c. `k manager`
   d. `gplwindow`
   e. `Xfree86`

6. 使用什么来提供更友好的环境，提供额外的 GUI 工具和开发工具包？

   a. `window manager`
   b. `desktop environment`
   c. `X client`
   d. `gmd`

7. 使用什么命令精调 X Windows 中使用的 `vsync` 和 `hsync` 显卡设置？

   a. `window manager`
   b. `desktop environment`
   c. `X client`
   d. `gmd`

8. 配置显示器时需要哪三项信息？

   a. `maximum resolution`, `vertical sync`
   b. `resolution`, `vsync`
   c. `maximum resolution`, `hsync`

9. GUI 的哪一部分是与计算机交互的？

   a. `window manager`
   b. `desktop environment`
   c. `X client`
   d. `gmd`

10. X Windows 是由哪些联合开发的？

    a. `AT`
    b. `GNU`

11. X Windows 使用哪个文件来存储鼠标、键盘和显示器信息？

    a. `/etc/X11/xconfig`
    b. `/etc/X11/XF86Config`
    c. `/etc/X11/urator`

12. 哪个为 Red Hat 提供图形登录界面？

    a. `gdm`
    b. `kdm`
    c. `startx`

# 10 X 系统

13. Linux GUI 由 `X server` 和 `X client` 两个部分组成。正确或错误？

14. 使用什么键组合退出 GUI？

    a. `Ctrl-Q`
    b. `Ctrl-Esc`
    c. `Ctrl-Alt-Del`

15. KDE 和 GNOME 是什么示例？

    a. `X Windows`
    b. `clients`
    c. `window managers`
    d. `desktop environments`

16. 什么文本配置程序随所有 X Windows 发布？

    a. `xf86config`
    b. `configurator`
    c. `Xconfig`

17. 运行 GUI 不需要桌面环境。正确或错误？

18. 在命令行提示符处输入什么命令可以启动 X Windows、窗口管理器和桌面环境？

    a. `startgui`
    b. `gdm`
    c. `startx`
    d. `winstart`

19. `XFree86` 的命名是因为：

    a. 它是最初为 `x86` 设计的开源 X Windows 版本
    b. 它是 1986 年首次发布的开源 X Windows 版本
    c. 它是 86 天后过期的评估 X Windows 版本
    d. 它是提供 86 色调板的开源 X Windows 版本

20. 使用什么将计算机的数字转换为显示器使用的模拟格式？

    a. `UART chip`
    b. `RAMDAC chip`
    c. `modem`
    d. `xconfig`

21. 使用什么命令获取计算机中存在的视频适配卡信息？

    a. `Probe`
    b. `Viderobe`
    c. `Probevideo`
    d. `SuperProbe`

22. 哪个运行级别自动启动显示器以提供图形登录界面？

    a. `1`
    b. `3`
    c. `4`
    d. `5`

23. `XWindows` 读取哪个文件在无用户干预的情况下加载窗口管理器或桌面环境？

    a. `.kde-default`
    b. `.gnome-default`
    c. `.xwindows-default`
    d. `.Xclients-default`
    e. `.Xclients`

24. Linux GUI 设计为针对特定硬件，因此仅与选定的视频硬件工作。正确或错误？

25. 可以配置哪个文件来更改 `gdm` 的外观和行为？

    a. `/etc/X11/gdm/gdm.conf`
    b. `/etc/X11/gdm/gdm`
    c. `/etc/X11/gdm/gdm.configuration`
    d. `/etc/X-Windows/gdm/gdm.conf`

# 482 第 10 章 X 窗口系统

26. KDE 桌面环境使用哪个窗口管理器？

    a. `X Windows Manager`
    b. `K Window Manager`
    c. `Starfish Window Manager`
    d. `Tab Window Manager`

27. 为了正确配置 X Windows，你需要了解关于显显的哪三项信息？
