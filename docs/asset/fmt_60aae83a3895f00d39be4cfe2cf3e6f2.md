
这将安装 CD-ROM 上的所有 XFree86 包。

## 配置 XFree86

在为系统配置 XFree86 之前，您需要知道以下信息：

- 您有多少视频内存
- 您的显卡使用什么类型的芯片组
- 显示器的最大分辨率
- 显示器的水平和垂直刷新率、品牌和型号

如果您不知道显卡的信息，请运行随 XFree86 提供的 SuperProbe 实用程序来确定：

`/usr/X11R6/bin/SuperProbe`

以下是 SuperProbe 输出的示例：

```
WARNING - THIS SOFTWARE COULD HANG YOUR MACHINE.

READ THE SuperProbe.1 MANUAL PAGE BEFORE

RUNNING THIS PROGRAM.

INTERRUPT WITHIN FIVE SECONDS TO ABORT!
```

第一视频：Super-VGA
芯片组：S3 Trio64V+ (Port Probed)
内存：2048 Kbytes
RAMDAC：Generic 8-bit pseudo-color DAC
(with 6-bit wide lookup tables (or in 6-bit mode

![](img/c2419364ebb911c809b6a79991707c27_427_0.png)

## 注意

正如输出中的警告信息清楚地指出的那样，此程序可能使您的系统无响应。请务必在运行此程序之前阅读手册页。

在您确定系统信息后，您需要决定如何配置 XFree86。您有三种选择：

- 使用一个名为 `Xconfigurator` 的全屏、菜单驱动的实用程序。
- 使用一个名为 `xf86config` 的命令行、提示导向的实用程序。
- 手动创建 `XF86Config` 文件。这是 XFree86 中创建可用 X Windows 环境所需的主要配置文件。它通常位于 `/etc/X11` 目录中，并且通常有一个符号链接 (`/usr/X11R6/lib/X11/XF86Config`) 指向 `/etc/X11/XF86Config`。

## 使用 Xconfigurator 创建 XF86Config 文件

`Xconfigurator` 实用程序允许您非常轻松地创建 `XF86Config` 文件：

- 1. 按如下方式运行程序：
  `/usr/X11R6/bin/Xconfigurator`

这会显示一个说明程序用途的屏幕。如开屏建议的那样，您应该阅读 `/usr/X11R6/lib/X11/doc/README.Config` 文件以了解有关文件结构的最新详细信息。

2. 单击 OK 继续。如果由于某种原因 `/usr/X11R6/lib/X11/XF86Config` 符号链接损坏，`Xconfigurator` 会显示一个要求您修复问题的屏幕。

3. 单击 OK 创建符号链接。如果您没有符号链接问题或刚刚修复了它，您将在下一个屏幕中看到结果，其中列出了显卡信息和所选 X 服务器名称。

4. 单击 OK 继续。使用上下箭头键滚动以查找显示器品牌和型号来选择显示器类型。如果您在列表中找到显示器，请选择它并按 OK 继续。如果显示器未在此列出，请选择 Custom monitor 并按 OK 继续。下一个屏幕会提示您指定显示器的垂直刷新率和水平同步率。请查阅显示器手册以找到这些数字。如果您仍然找不到显示器的信息，请检查 `/usr/X11R6/lib/X11/doc/Monitor` 文件。

![](img/c2419364ebb911c809b6a79991707c27_428_0.png)

> 提示
> 如果您丢失或扔掉了显示器手册，您可能能够在显示器厂商的网站上找到有关显示器的信息。

5. 单击 OK 继续显示器规格。下一个屏幕列出了显示器分辨率。选择最适合您显示器的分辨率和水平刷新率。如果您不知道这些设置应该是什么，请联系您的显示器或计算机厂商查找此信息。除非您非常不在乎显示器的健康状况，否则不要尝试这些设置。请注意，如果您为 XFree86 提供错误的显示器设置，可能会损坏显示器。

6. 在您指定分辨率和水平刷新率后，单击 OK 继续指定垂直刷新率。完成后，单击 OK。

7. 出现一个对话框，说明 `Xconfigurator` 现在将使用所选 X 服务器探测您的显卡。单击 OK 继续。等待探测完成。如之前的对话框所警告的那样，屏幕在探测过程中可能会变黑几次。探测完成后（希望没有问题），屏幕会显示默认视频模式（颜色深度和分辨率大小）。

8. 如果默认视频模式不令人满意，请单击 Let Me Choose 选项来选择您想要的视频模式。选择此选项是推荐的，以便您可以自定义视频模式。

9. 使用上下箭头键，通过按空格键为每种颜色模式选择合适的分辨率。您也可以使用空格键切换选择。在为每种颜色模式选择所有所需分辨率后，单击 OK。

10. 对话框确认 `XF86Config` 文件已创建。在启动 X 服务器之前，请查看 `XF86Config` 文件。

## 了解 XF86Config 文件

与任何典型的 UNIX 配置文件一样，`XF86Config` 文件会忽略空白行和以 `#` 字符开头的任何行，这些行被视为注释。`XF86Config` 文件分为多个部分。每个部分为 X 服务器提供特定类型的信息。此外，每个部分都以 `Section "<section name>"` 行开始，以 `EndSection` 行结束。以下列表描述了各部分：

- `Files section.` 用于指定字体和颜色数据库路径。以下是此类部分的示例：

```
Section "Files"

RgbPath    "/usr/X11R6/lib/X11/rgb"

FontPath   "/usr/X11R6/lib/X11/fonts/misc/"

FontPath   "/usr/X11R6/lib/X11/fonts/Type1/"

FontPath   "/usr/X11R6/lib/X11/fonts/Speedo/"

FontPath   "/usr/X11R6/lib/X11/fonts/75dpi/"
```

```
FontPath "/usr/X11R6/lib/X11/fonts/100dpi/"

EndSection
```

如果您向系统添加新字体，可以使用 `FontPath` 选项指定已安装字体的目录。

本节中可以添加的其他常用选项列于表 14-1 中。

### 表 14-1 XF86Config 的 Files 部分选项

| 选项 | 描述 |
|---|---|
| AllowNonLocalXvidtune | 允许 xvidtune 程序从远程主机连接 |
| DisableVidMode | 禁用 xvidtune 程序使用的某些视频模式扩展 |
| AllowNonLocalModInDev | 允许远程 X 客户端更改键盘和鼠标设置 |
| DisableModInDev | 禁用某些通常可以动态设置的输入设备扩展 |
| AllowMouseOpenFail | 允许 X 服务器在没有鼠标的情况下启动 |

## 服务器标志部分
用于为 X 服务器指定通用选项。以下是此类部分的示例：

```
Section "ServerFlags"

# Uncomment this to cause a core dump at the

# spot where a signal is received. This may leave

# the console in an unusable state, but may provide

# a better stack trace in the core dump to aid in

# debugging

#NoTrapSignals

# Uncomment this to disable the <Ctrl><Alt><BS>

# server abort sequence This allows clients to

# receive

# this key event.

#DontZap

# Uncomment this to disable the

# <Ctrl><Alt><KP_+>/<KP_-> mode switching sequences.

# This allows clients to receive these key events.

#DontZoom

EndSection
```
