
# Section "ServerLayout"

```
    Identifier "Default Layout"

    Screen "0" 0 0

    InputDevice "Mouse" "CorePointer"

    InputDevice "Keyboard" "CoreKeyboard"

    InputDevice "DevInputMouse" "AlwaysCore"
```

在这个示例中，使用了单个显示器（数字指定屏幕的位置），并使用了两个默认输入设备——鼠标和键盘用于会话。

## The Files 部分

`XF86Config` 文件的 `Files` 部分可能如下：

```
Section "Files"

    RgbPath "/usr/X11R6/lib/X11/rgb"

    FontPath "unix:/7100"

EndSection
```

# 第 6 章节 窗口系统

本节列出了可用的会话颜色（通过文本文件 `rgb.txt` 中的名称）以及指向 X 字体服务器的端口号。字体服务器 `xfs` 在启动时启动，不需要活跃的 X 会话。如果不使用字体服务器，`FontPath` 条目可能需要列出 `/usr/X11R6/lib/X11/` 目录下的每个目录，在本示例中：

```
FontPath "/usr/X11R6/lib/X11/fonts/100dpi"

FontPath "/usr/X11R6/lib/X11/fonts/misc"

FontPath "/usr/X11R6/lib/X11/fonts/75dpi"

FontPath "/usr/X11R6/lib/X11/fonts/PEX"

FontPath "/usr/X11R6/lib/X11/fonts/Speedo"
```

这些目录包含了在 X 会话期间可用的默认压缩字体。字体服务器通过 `/etc/X11/fs` 目录下的名为 `config` 的文件进行配置。该文件包含了供字体服务器使用的字体列表（或目录）。通过在该文件中添加一个备用服务器（`alternate-server`）条目并重新启动字体服务器，您可以指定在 X 会话期间使用的远程字体服务器。这有助于集中字体支持并减少本地存储需求（尽管对于随 Red Linux 和 X 安装的近 5,000 种字体仅需 25MB）。

# The Module 部分

`XF86Config` 文件的 `Module` 部分指定了为 X 会话加载的模块或驱动程序。该部分可能如下所示：

```
Section "Module"

  Load "GLcore"

  Load "dbe"

  Load "extmod"

  Load "fbdevhw"

  Load "pex5"

  Load "glx"

  Load "pex5"

  Load "record"

  Load "xie"

EndSection
```

这些模块范围从特殊的显卡支持到字体光栅化器不等。模块位于 `/usr/X11R6/lib/modules` 目录下的子目录中。

# InputDevice 部分

`InputDevice` 部分配置特定的设备，例如此示例中的键盘或鼠标：

```
Section "InputDevice"

  Identifier "Keyboard"

  Driver "keyboard"
```

| Option | *XkbRules* | *free86 |
| :--- | :--- | :--- |
| Option | *XkbModel | *pc15 |
| Option | *XkbLayout | *us |

EndSection

| Section "InputDevice" |
| :--- | :--- |
| Identifier | "Mouse@" |
| Driver | "mouse" |
| Option | "Protocol" "PS/2" |
| Option | "Device" "/dev/psaux" |
| Option | "ZAxisMapping" "4 5" |
| Option | "Emulate3Buttons" "no" |

EndSection

您可以配置多个设备，并且可能存在多个 `InputDevice` 部分。先前的示例指定了一个基础键盘和一个三键 PS/2 鼠标（实际上是 ThinkPad TrackPoint 指针）。同时使用的一个指定使用 USB 设备的 `InputDevice` 部分（以启用 PS/2 和 USB 指针）可能如下所示：

| Section "InputDevice" |
| :--- | :--- |
| Identifier | "Mouse@" |
| Driver | "mouse" |
| Option | "Device" "/dev/mouse" |
| Option | "Protocol" "IMPS/2" |
| Option | "Emulate3Buttons" "off" |

EndSection

> 注意：如果您更改了设备，`Monitor` 部分将配置显示器，如下所示：

| Section "Monitor" |
| :--- | :--- |
| Identifier | "Monitor" |
| VendorName | "Monitor" |
| Model | "Monitor" |
| Horiz | 55 |
| Vert | 70 |

EndSection

## 第 6 章 X Window 系统

你可以使用以下三个配置工具（以及其他）来创建一个可用的 `XF86Config` 文件：

- `redhat-config-xfree86`: 这是 Red Hat 的图形化配置工具，它通过启动 X 会话来创建 `XF86Config` 文件。
- `xf86-config`: 基于文本的配置工具，通常包含在 `XFree86` 中，不随 Fedora 分发，但可以在 The XFree86 Project, Inc. 的 `http://www.xfree86.org` 获取。请参考本章的“使用 xf86config 创建 XF86Config 文件”节。
- `XFree86`: X 服务器本身可以创建一个骨架化的配置。

接下来的章节将讨论如何使用这些软件工具中的每一个来创建一个可用的 `XF86Config` 文件。

### 使用 redhat-config-xfree86 客户端配置 X

你可以使用 `redhat-config-xfree86` 客户端创建或更新 `XF86Config` 文件。如果你已经在运行 X，可以从桌面面板的系统设置菜单中点击“显示 (Display)”项开始；你也可以以 root 身份在控制台会话期间从命令行启动客户端，如下：

```bash
redhat-config-xfree86
```
