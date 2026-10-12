
## 4: 配置 X 窗口

### Section "ServerFlags"

# 注消此行以在信号接收处产生核心转储（core dump），这可能使控制台处于不可用状态，但可以在核心转储中提供更好的堆栈跟踪以帮助调试

#NoTrapSignals

# 注消此行以禁用 <Ctrl><Alt><BS> 服务器终止序列。这允许客户端接收此按键事件。

#DontZap

# 注消此行以禁用 <Ctrl><Alt><KP_+>/<KP_-> 模式切换序列。这允许客户端接收这些按键事件。

#DontZoom

EndSection

### 输入设备

# 让 LINUX 运行起来：核心技巧与技术

### Section "Keyboard"

Protocol      "Standard"

# 使用 XQUEUE 时，注释掉上述行，并注消下方的行

#Protocol      "Xqueue"

AutoRepeat      500 5

# 让服务器处理 NumLock。这通常在使用预-R6 版本的客户端时才需要

#ServerNumLock

# 指定哪些键盘 LED 可以由用户控制（例如，使用 xset(1)）

#Xleds      1 2 3

# 将 LeftAlt 设置为 Meta，RightAlt 键设为 ModeShift，RightCtl 键设为 Compose，ScrollLock 键设为 ModeLock：

LeftAlt Meta
RightAlt Meta
ScrollLock Compose
RightCtl Control

# 要禁用 XKEYBOARD 扩展，请取消 XkbDisable。

# XkbDisable

# 要根据你的键盘自定义 XKB 设置，请修改下方的行（这些是默认值）。例如，对于非美国键盘，你可能想使用：

# XkbModel "pc102"

# 如果你有一把美国微软天然键盘，可以使用：

# XkbModel "microsoft"

# 然后要更改语言，请更改 Layout 设置。例如，可以通过以下获取德语布局：

# XkbLayout "de"

# 或：

# XkbLayout "de"
# XkbVariant "nodeadkeys"

# 如果你想交换大写锁定键和控制键的位置，请使用：

# XkbOptions "ctrl:swapcaps"

```
这些是 XFree86 的默认 XKB 设置
```

# XkbRules "xfree86"

# XkbModel "pc101"

# XkbLayout "us"

# XkbVariant ""

# XkbOptions " "

```
XkbKeycodes "xfree86"
XkbTypes "default"
XkbCompat "default"
XkbSymbols "us (pc101)"
XkbGeometry "pc"
XkbRules "xfree86"
XkbModel "pc101"
XkbLayout "us"
EndSection
```

### Section "Pointer"

```
Protocol      "PS/2"
Device        "/dev/mouse"
```

# 使用 XQUEUE 时，注释掉上述两行，并取消下方的行。

# Protocol      "Xqueue"

# 波特率和采样率用于某些罗技（Logitech）鼠标

# BaudRate      9600

# SampleRate     150

# Emulate3Buttons 是 2 键微软鼠标的选项

# Emulate3Timeout 是以毫秒为单位的超时时间（默认为 50ms）

Emulate3Buttons

Emulate3Timeout 50

# ChordMiddle 是某些 3 键罗技鼠标的选项

# ChordMiddle

EndSection

### Section "Monitor"

```
# 可以存在任意数量显示器部分

Section "Monitor"

Identifier "CustomConfiguration"
VendorName "Unknown"
ModelName "Unknown"
```

# 除非另有指定，HorizSync 单位为 kHz。

# HorizSync 可以是逗号分隔的数值列表，或逗号分隔的范围列表。

# 注意：数值仅为示例。请参考显示器以获取正确数字。

HorizSync    30

# 除非另有指定，VertRefresh 单位为 Hz。

# VertRefresh 可以是逗号分隔的数值列表，或逗号分隔的范围列表。

# 注意：数值仅为示例。请参考显示器以获取正确数字。

VertRefresh    100

# 模式两种格式指定：紧凑单行格式，或多行格式。两者是等效的
