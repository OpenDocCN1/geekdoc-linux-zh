
`XFree86` 的配置位于 `XF86Config` 文件中。该文件通常位于 `/etc/XF86Config` 或 `/etc/X11/XF86Config`，取决于你的发行版。红帽 Linux 7 将文件存放在 `/etc/X11`。或者，你也可以从通用的配置文件开始，例如 `/usr/X11R6/lib/X11/XF86Config.eg`。

如果你不知道安装 `XFree86` 将此文件放在了哪里，可以使用 `locate` 命令来查找：

```
# locate XF86Config
```

`XF86Config` 文件包含与 X 服务器运行相关的信息，包括键盘定义、鼠标规格和显示器信息。该文件由 `XFree86` 配置应用程序（如 `Xconfigurator` 和 `xf86config`）生成。

## XF86Config 文件 261

尽管如此，有时对 X Windows 环境的微调只能通过你喜欢的文本编辑器直接编辑 `XF86Config` 文件来实现。

`XF86Config` 文件被分为几个部分。并非所有部分对于运行 GUI 都是必须的。随着 `XFree86` 4 版本的发布，这些部分的顺序已不再重要。

*   **`Files`**: 此部分指定了 `XFree86` 在何处可以找到它的辅助文件，例如字体和颜色表。
*   **`ServerFlags`**: 此部分用于启用和禁用 X 服务器功能，例如如何处理按键序列。
*   **`Module`**: 此部分指定 X 服务器启动期间的运行时加载模块。这些包括字体光栅化器模块。在大多数情况下，你已经有一个可以工作的 X 服务器，且标准字体已经足够了，因此你的 `XF86Config` 文件中可能没有 `Module` 部分。
*   **`InputDevice`**: 此部分指定输入设备，包括键盘和鼠标。如果存在 `Keyboard` 和 `Pointer` 部分，则不需要。
*   **`Keyboard`**: 此部分指定控制键位映射和其他键盘特征（如重复率）的键盘协议。如果为键盘有 `InputDevice` 部分，则不需要。它可以与 `XFree86` 版本4 配合工作。
*   **`Pointer`**: 此部分指示正在使用的鼠标类型、鼠标占用的端口以及鼠标的按钮行为。如果为键盘有 `InputDevice` 部分，则不需要。它可以与 `XFree86` 版本4 配合工作。
*   **`VideoAdaptor`**: 此部分旨在支持作为“原始”的视频，换句话说，作为某些较大系统组件的视频适配器。在本文中未使用。
*   **`Monitor`**: 此部分定义了你的显示器的规格。可能包含 `Modes` 部分的信息。
*   **`Device`**: 此部分定义了可用的图形设备（显示适配器）。
*   **`Modes`**: 此部分定义了显示器的刷新率和分辨率。可以合并到 `Monitor` 部分。
*   **`Screen`**: 此部分将显示器与视频适配器连接。它还定义了可用 X 服务器的行为，例如通用 SVGA 服务器、特定厂商服务器等。
*   **`Layout`**: 此部分将屏幕与输入设备连接。
*   **`DRI`**: 此部分处理任何直接渲染接口 (DRI)，这对于图形密集型负载更为常见。
*   **`Vendor`**: 此部分将用于特定特定的设置。

## Files

`Files` 部分用于指定关键文件的位置。注意，在 `X86Config` 文件中，注释以井号 (`#`) 开头。

```
Section "Files"
    RgbPath "/usr/X11R6/lib/X11/rgb"
    FontPath "/usr/X11R6/lib/X11/fonts/local"
    FontPath "/usr/X11R6/lib/X11/fonts/misc"
    FontPath "/usr/X11R6/lib/X11/fonts/75dpi:/unscaled"
    FontPath "/usr/X11R6/lib/X11/fonts/100dpi:/unscaled"
    FontPath "/usr/X11R6/lib/X11/fonts/Type1"
    FontPath "/usr/X11R6/lib/X11/fonts/Speedo"
    FontPath "/usr/X11R6/lib/X11/fonts/75dpi"
    FontPath "/usr/X11R6/lib/X11/fonts/100dpi"
    ModulePath "/usr/X11R6/lib/modules"
EndSection
```

## XF86 Config 文件 263

这里有需要注意的基本规则，适用于其他部分：

*   每个部分以 `Section` 行开始。
*   每个部分以 `EndSection` 行结束。
*   在 `Section` 行上，使用双引号指定部分名称（在本例中为 `Section "Files"`）。

此部分有三个常用的指令，见表 12.1。

### 表 12.1：Files 指令

| 指令 | 效果 |
| :--- | :--- |
| `RgbPath` | 此指令指定 RGB（红-绿-蓝）数据库的，不带 `.txt` 或 `.db` 后缀。RGB 文件指定了与其他颜色名称关联的红色、绿色和蓝色量。通常，除非你移动或更改数据库名称，否则可以保持默认值不变。 |
| `FontPath` | 多次此指令指定 Windows 在何处找到系统中安装的 X 字体。可以指定可缩字体和位图字体（位图字体在目录末尾带有 `:unscaled`）。如果你为系统添加了新的字体目录，应为它们添加 `FontPath` 指令。 |
| `ModulePath` | 此指令用于支持动态加载模块的操作系统（如 Linux）。此指令指示去哪里查找模块。对于大多数 `XFree86` 版本，此指令不会出现，或者在我们的示例中被注释掉了。模块的默认路径为 `/usr/X11R6/lib/modules`，只有当你需要更改此值时才需要使用此指令。 |

## ServerFlags

`ServerFlags` 部分允许你启用和禁用 X 服务器的一些功能。一个没有注释的 `ServerFlags` 部分所示：

```
Section "ServerFlags"
    Option "NoTrapSignals"
    Option "DontZap"
    Option "DontZoom"
    Option "DisableVidModeExtension"
    Option "AllowNonLocalXvidtune"
    Option "DisableModInDev"
    Option "AllowNonLocalModInDev"
    Option "AllowMouseOpenFail"
    Option "blank time" "10"
    Option "standby time" "20"
    Option "suspend time" "30"
    Option "off time" "60"
    Option "EstimateSizesAggressively" "0"
    Option "NoPM" "false"
    Option "Xinerama" "true"
EndSection
```

取消你想要激活的任何指令；如果你不想激活它们，请保持注释状态（通常的默认状态）。此处指定的任何选项都将被 `ServerLayout` 部分中的选项所覆盖。

此示例中的指令效果如表 12.2 所示。

### 表 12.2：ServerFlags 指令

| 指令 | 效果 |
| :--- | :--- |
| `NoTrapSignals` | 该指令用于调试。当接收到指示错误的信号时，服务器将执行核心转储（core dump），将其内存区域的内容写入磁盘上的文件。这可能会导致你的系统不稳定，但在调试问题时（特别是对于 X 服务器的 Beta 版本和测试版本）它是非常有价值的。除非你正在排查 X 服务器的问题，否则最好保持此指令注释状态 |

### 表 12.2 续：ServerFlags 指令

| 指令 | 效果 |
| :--- | :--- |
| `DontZap` | 通常情况下，`Ctrl+Alt+Backspace` 键组合会导致 Windows 终止并返回到控制台。启用此指令后，`Ctrl+Alt+Backspace` 将被忽略，该键组合将传递给当前应用程序进行处理。只有在运行需要正确使用此键组合的应用程序的少数情况下，才取消此行的注释。 |
| `Zoom` | 通常情况下，`Ctrl+Alt+小键盘加号（Plus）`会在你的 X 服务器可用的配置屏幕分辨率之间循环，增加分辨率调整时间。`Ctrl+Alt+小键盘减号（Minus）`同样用于降低分辨率。如果应用程序因其他目的需要这些键组合，请取消此行的注释，让 Windows 忽略这些键组合并将它们传递给你。 |
| `DisableVidModeExtension` | 该指令防止使用 `xvidune` 客户端对你的视频显示进行调优。本文未讨论 `Xvidune`；可以通过在打开的窗口中输入命令 `xvidune` 来找到该程序的文档。无需取消此项的注释，你可以默认保持其注释状态。 |
