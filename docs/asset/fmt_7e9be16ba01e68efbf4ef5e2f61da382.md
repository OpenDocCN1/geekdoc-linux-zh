
```
Section "Module"
  Load "dbe"
  Load "extmod"
  Load "fbdevhw"
  Load "glx"
  Load "record"
  Load "freetype"
  Load "type1"
  Load "dri"

EndSection
```

这些模块范围从特殊的显卡支持到字体栅格化器。模块位于 `/usr/lib/modules` 目录下的子目录下。

## InputDevice 节

InputDevice 节如示例所示配置特定设备，例如键盘或鼠标：

[点击此处查看代码图像](#)

```
Section "InputDevice"
```

| Identifier | "Keyboard0" |

| :--- | :--- |

| Driver | "kbd" |

| Option | "pc105" |

| Option | "us" |

| EndSection | |

| Identifier | "Mouse0" |

| Driver | "mouse" |

| Option | "CorePointer" |

| EndSection | |

你可以配置多个设备，并存在多个 InputDevice 节。可以使用多个设备，前面的示例指定了键盘和鼠标（实际上是鼠标）。使用 USB 设备的 InputDevice 节可以同时使用，并可能如下：

点击此处查看代码图像](#)

| Identifier | "Mouse0" |

| :--- | :--- |

| Driver | "mouse" |

| Option | "CorePointer" |

| Option | "AlwaysCore" |

| Option | "PS/2" |

| EndSection | |

| Section | "InputDevice" |

| :--- | :--- |

| Identifier | "Monitor0" |

| VendorName | "Monitor Vendor" |

| ModelName | "Monitor Model" |

| DisplaySize | 300 220 |

| HorizSync | 31.5-48.5 |

| VertRefresh | 50-70 |

| Option | "dpms" |

| EndSection | |

注意 X 服务器根据此节中的水平和垂直刷新率自动确定最佳视频时序。如果需要，可能仍使用传统的 mode-line 条目（由 XFree 4.6 使用）。如果在配置 X 时自动检测显示器（参见“配置 X”节），其定义和能力将插入你的 `xorg.conf` 文件。MonitorsDB 数据库包含 600 多个显示器，位于 `/usr/share/hwdata` 目录。

## Device 节

Device 节提供了计算机使用的显卡的详细信息，如示例所示：

点击此处查看代码图像

```
Section "Device"
    Identifier       "Intel Corporation Mobile
945GM/MS,\943/940GML Express
Integrated Graphics Controller
    Driver           "intel"
    BusID            "PCI:0:2:0"
EndSection
```

此示例识别了一个安装的集成 Intel 显芯片组。Driver 条目告诉 Xorg 服务器加载内核模块。不同的芯片组有不同的选项。例如，这里是 NeoMagic 视频芯片组的条目：

点击此处查看代码图像

```
Section "Device"
    Identifier       "NeoMagic (laptop/notebook)"
    Driver           "neomagic"
    VendorName       "NeoMagic (laptop/notebook)"
    BoardName        "NeoMagic (laptop/notebook)"
    Option           "externDisp"
    Option           "internDisp"
EndSection
```

在这个示例中，Device 节指定了显卡的驱动程序（`neomagic_drv.o`），并启用了两个芯片组选项（`externDisp` 和 `internDisp`），以便在笔记本 屏幕和外部显示器上显示。

Xorg 服务器支持数百种不同的视频芯片组。如果你

配置了 X11 但随后更改了安装的显卡，你需要编辑现有的 Device 部分或生成新的 `xorg.conf` 文件，使用本章讨论的 X 配置工具之一，以反映新显卡的功能。你可以在配套 man 手页中找到有关某些芯片组选项的详细信息。你应该查阅这些资源以获取有关优化和故障排除的提示。

## Screen 部分

Screen 部分将之前节的信息（使用 Screen0、Device 和 Monitor 标识符）结合在一起。你还可以为会话指定一个或多个颜色深度和分辨率。这是一个示例：

点击此处查看代码图像

```
Section "Screen"
    Identifier "Screen0"
    Device "Videocard0"
    Monitor "Monitor0"
    DefaultDepth 24
    SubSection "Display"
        Viewport 0 0
        Depth 16
        Modes "1024x768" "800x600"
        "640x480"
    EndSection
EndSection
```

在这个示例中，数千色色的颜色深度和 1024 × 768 的分辨率是默认值，可选分辨率为 800 × 600 和 640 × 480。如果显卡和显示器的组合支持，可以使用具有不同颜色深度和分辨率的多个 Display 子节条目（带有如 Depth 24 用于数千色等设置）。你还可以使用 DefaultDepth 条目（在示例中为 24，或数千色），并配合特定的颜色深度来标准化安装中的深度。

你还可以指定比你的显示器或笔记本电脑屏幕硬件支持的更大的桌面分辨率。此设置在 Display 子节中被称为虚拟分辨率。这允许例如让一个 800 × 600 的显示器在 1024 × 768 的虚拟窗口内平移（即在虚拟窗口内滑动）。

### 注意

如果你的显示器和显卡支持多种分辨率且配置恰当，你可以使用按键组合 Ctrl+Alt+(小键盘数字) + Ctrl+Alt+(小键盘数字) 在 X 会话期间动态更改分辨率。

## 启动 X

你可以通过多种方式启动 X 会话。Ubuntu 安装程序设置了系统，使用一个名为 LightDM（轻量级显示管理器）的显示管理器让 Linux 直接启动到 X 会话。这是一个提供图形登录的 X 客户端。登录后，你使用本地会话（运行在你的计算机上），或者如果系统配置了如此，使用运行在网络上远程计算机的 X 会话。

通过显示管理器登录需要你输入用户名和密码。你也可以从命令行启动 X 会话。接下来的章节将描述这两种方法。

### 注意

如果你使用了服务器（Server）安装，你的系统将启动到文本登录。请参阅第 10 章“命令行初学者课程”获取有关在此处如何操作的更多信息。

## 使用显示管理器

X 显示管理器提供一个图形登录界面，在访问 X 桌面之前需要输入用户名和密码。它还允许你为 X 会话选择不同的桌面。启动 Linux 后是否显示 X 显示管理器是由运行级别（runlevel）控制的——这是 `/etc/event.d/` 中的系统状态条目。Ubuntu 对以下级别的处理方式如下：

- + Halt 停止（不要将 initdefault 设置为此级别。）
- 1–单用户用户模式
- 2–X 图形多用户模式
- 6–Reboot重启（不要将 initdefault 设置为此级别。）

你可能会看到提到运行级别 3 到 5 的；你可以忽略它们，因为它们在 Ubuntu 中的处理方式与运行级别 2 相同。历史上，Ubuntu 使用 `/etc/inittab` 文件处理运行级别，但该文件已不存在。

（有关运行级别的信息，请参阅第 15 章“启动过程”。）

相反，在 `/etc/events.d/` 目录下有几个文件，包括每个每个虚拟控制台的单独文件（通过按 Ctrl+Alt+F1 到 F7 访问）。但是，如果你想覆盖 Ubuntu 的任何默认设置，仍然可以创建一个 initab 文件。请确保以 root 身份创建 initab 文件，并包含至少一行类似下所示的内容：

```
id:initdefault:
```

这将强制你的系统在文本模式下启动。

## 更改窗口管理器

Ubuntu 使切换到另一个窗口管理器或桌面环境变得非常轻松。桌面环境不仅指窗口管理器，还指一系列相关应用程序，例如生产力工具或配置工具。
