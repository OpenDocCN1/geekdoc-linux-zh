
## 配置 XFree86

XFree86 是大多数基于 Intel 的 Linux 发行版中 X Window 系统的默认实现。大多数用户应使用配置工具来配置 XFree86，例如 **XFree86setup**（参见第 1 章）。在 Red Hat 和基于 Red Hat 的系统上，提供了一个名为 **Xconfigurator** 的工具（参见第 1 章）。这些工具通过探测系统视频硬件并写入配置文件 XF86Config，大大降低了配置 XFree86 的难度。然而，为了获得所需的性能，通常仍需手动修改此配置文件。因此，本系统介绍了修改 XF86Config 所需的信息。本文档记录的是仍被广泛分发的 3.3.6 版本；有关新特性和变更的信息，请参阅本节后面的“XF86 第 4 版”。要获取 XFree86 的最新信息（包括更新版本），请访问 http://www.xfree86.org。

## XF86Config：整体结构

XF86Config 配置文件 `XF86Config` 的位置因所使用的发行版而异。在 Red Hat 系统中，您可以在 `/etc/X11` 目录中找到该文件，它组织为以下各个部分：

- **Files**：指定字体和 X 程序模块的默认路径。
- **Module**：指定在 X 服务器启动时要加载的模块（如果有的话）。
- **ServerFlags**：指定某些服务器选项。
- **Keyboard**：定义系统的默认键盘配置。
- **Pointer**：定义系统的默认鼠标配置。
- **Monitor**：定义系统的默认监视器配置。
- **Device**：定义系统的视频适配器配置。
- **Screen**：指定使用当前视频适配器可能实现的一个或多个视频显示模式。
- **Xinput**：定义某些输入设备，如摇杆和绘图板。此部分是可选的。

每个部分以一个 `Section` 语句开始，以一个 `EndSection` 语句结束。这些语句用于区分不同的部分。在每个部分中，您可以使用列出的条目。其中许多条目允许您指定一个值或名称（例如 `Load "xf86Jstk.so"`）；请务必用引号将字符串（字母数字表达式）括起来。

### Files 部分

Files 部分指定字体、X 系统颜色和 X 程序模块的默认路径。以下示例展示了该部分的外观：

```
Section "Files"
    RgbPath "/usr/X11R6/lib/X11/rgb"
    FontPath "/usr/X11R6/lib/X11/fonts/Local", \
             "/usr/X11R6/lib/X11/fonts/misc", \
             "/usr/X11R6/lib/X11/fonts/75dpi:unscaled", \
             "/usr/X11R6/lib/X11/fonts/100dpi:unscaled", \
             "/usr/X11R6/lib/X11/fonts/Type1", \
             "/usr/X11R6/lib/X11/fonts/Speedo", \
             "/usr/X11R6/lib/X11/fonts/75dpi", \
             "/usr/X11R6/lib/X11/fonts/100dpi/" 
    ModulePath "/usr/X11R6/lib/modules"
EndSection
```

下表显示了您可以在 Files 部分中使用的选项。

#### FILES 部分条目

| 使用此条目 | 以执行此操作 |
|---|---|
| **FontPath** *路径名* | 以逗号分隔列表的形式指定可用系统字体的路径名。注意：Red Hat 6.x 和衍生系统（包括 Mandrake 6.x 和 7.x）通过 xfs 字体服务器提供字体支持。字体路径名列表应列在 xfs 配置文件 `*/etc/X11/fs/config*` 的 Catalogue 部分中。 |
| **ModulePath** *路径名* | 指定用于搜索处理扩展输入设备的程序模块的路径名。 |
| **RGBPath** *路径名* | 指定 RGB 颜色数据库的路径名。 |

### Module 部分

此部分指定在 X 服务器启动时要加载的模块（如果有的话）。以下是 Module 部分的一个示例：

```
Section "Module"  
  Load "xf86jstk.so"  
EndSection
```

此部分加载摇杆驱动程序。要使用此驱动程序，您还必须在 Xinput 部分中指定驱动程序的特性。

#### MODULE 部分条目

| 使用此条目 | 以执行此操作 |
|---|---|
| **Load** *模块* | 指示服务器加载指定的模块。模块的位置必须通过 ModulePath 选项（参见“Files 部分”一节）指定。受支持的模块包括双按钮摇杆；Elographics 和 Microtouch 触摸屏；Wacom 手写笔；光标；橡皮擦；Summasketch、AceCad 和 CalComp DrawingBoard 图形板；Switch 虚拟设备；以及 SGI 按钮盒。 |

### ServerFlags 部分

*ServerFlags* 部分允许您指定某些服务器选项。以下是该部分的一个示例：

```
Section "ServerFlags"  
  DontZoom  
EndSection
```

#### SERVERFLAGS 部分条目

| 使用此条目 | 以执行此操作 |
|---|---|
| AllowMouseOpenFail | 指示服务器即使鼠标无法打开或初始化也要启动。 |
| AllowNonLocalModInDev | 允许来自其他主机的用户修改键盘和鼠标设置。默认情况下，不允许此类修改。 |
| AllowNonLocalXvidtune | 允许 xvdtune 客户端从另一个主机连接。默认情况下，不允许此类连接。 |
| DisableModInDev | 禁用输入设备设置的动态修改。 |
| DisableVidMode | 防止 xvidtune 更改视频模式，因为这可能会损坏某些监视器。 |
| DontZap | 防止使用 Ctrl + Alt + Backspace 组合键终止服务器。 |
| DontZoom | 防止使用 Ctrl + Alt + 小键盘加号和 Ctrl + Alt + 小键盘减号组合键。 |
| NoTrapSignals | 指示服务器在遇到错误时退出，而无需尝试跟踪错误来源。此选项仅对调试目的有用。 |

### Keyboard 部分

此部分定义系统的键盘。以下是 Keyboard 部分的一个示例：

```
Section "Keyboard"
Protocol "Standard"
AutoRepeat 500 5
XkbKeyCodes "xfree86"
XkbTypes "default"
XkbCompat "default"
XkbSymbols "us(pc101)"
XkbGeometry "pc"
XkbRules "xfree86"
XkbModel "pc101"
XkbLayout "us"
EndSection
```

#### KEYBOARD 部分条目

| 使用此条目 | 以执行此操作 |
|---|---|
| **AltGr** *键* | 将右侧 Alt 键映射到以下键之一：Compose、ModeShift、ModeLock、ScrollLock 或 Control。默认情况下，该键映射到 Meta。请注意，AltGr 是 RightAlt 的同义词。 |
| **AutoRepeat** *延迟 速率* | 以毫秒为单位设置键盘自动重复的延迟速率。请注意，此选项在并非所有受支持的硬件上都能正常工作。 |
| **LeftAlt** *键* | 将左侧 Alt 键映射到以下之一：Compose、ModeShift、ModeLock、ScrollLock 或 Control。默认情况下，该键映射到 Meta。 |
| **Protocol** *键盘协议* | 指定 SVR3 或 SVR4 上事件驱动队列驱动使用的键盘协议（Standard 或 Xqueue）。 |
| **RightAlt** *键* | 将右侧 Alt 键映射到以下键之一：Compose、ModeShift、ModeLock、ScrollLock 或 Control。默认情况下，该键映射到 Meta。请注意，RightAlt 是 AltGr 的同义词。 |
| **RightCtl** *键* | 将右侧 Ctrl 键映射到以下键之一：Meta、Compose、ModeShift、ModeLock、ScrollLock 和 Control。默认情况下，该键映射到 Control。 |
| **ScrollLock** *键* | 将 ScrollLock 键映射到以下键之一：Meta、Compose、ModeShift、ModeLock、ScrollLock 或 Control。默认情况下，该键映射到 Compose。 |
| **ServerNumLock** | 启用应用程序使用数字键盘。 |
| **VTinit** *命令* | 在终端打开后运行指定的 shell 命令。 |
| **VTSysReq** | 在支持虚拟终端切换的非 System V 系统（包括 Linux）上启用 System V 虚拟终端切换序列。 |
| **XkbDisable** | 关闭 XKEYBOARD 扩展。 |
| **XkbKeyCodes** *按键码* | 指定给定键盘模型的按键码映射（参见本表中的 XkbModel）。默认值为 XFree86。要查看可用选项，请参阅 /usr/lib/X11/xkb/keycodes。 |
| **XkbSymbols** *符号* | 指定给定键盘布局上由符号键输入的符号。要查看可用选项，请参阅 /usr/lib/X11/xkb/symbols。 |
| **XkbGeometry** *几何形状* | 指定您正在使用的键盘模型的几何形状。要获取可用几何形状的列表，请查阅 /usr/lib/X11/xkb/geometry 中的键盘几何文件。 |
| **XkbLayout** *布局* | 指定键盘布局。可用选项包括：be（比利时）、bg（保加利亚）、br（巴西）、ca（加拿大）、cs（捷克斯洛伐克）、de（德国）、de-CH（瑞士德语）、dk（丹麦）、en-US（ISO9995-3 标准的美国英语）、es（西班牙）、fi（芬兰）、fr（法国）、fr-CH（瑞士法语）、gb（英国）、hu（匈牙利）、it（意大利）、jp（日本）、nec jp（PC-98xx 系列）、no（挪威）。 |

