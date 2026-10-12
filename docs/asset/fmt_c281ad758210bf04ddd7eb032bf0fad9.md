
此节告诉`X`关于键盘的信息——其型号、布局等。你最可能调整的节的详细信息将在稍后于“`X` 配置选项”中描述。

在大多数情况下，不同的`X`服务器支持相同的节以及大多数相同的选项名称。该规则确实存在少数例外：

- `Free86 3.3.6`及更早版本不使用`Option`关键字。相反，选项名称（如上例中的`XkbLayout`或`AutoRepeat`）以不带引号的形式作为该行的第一个单词。
- `Free86 3.3.6`及更早版本不使用`ServerLayout`节，后将在“整合一切”中描述。
- `Free86 3.3.6`及更早版本缺少`Identifier`和`Driver`行，这些行在`Free86 4.x`和`X-Org-X11`配置中很常见。
- 某些特定节的功能在版本之间不同。我将在后面的页面中描述其中最重要的。

### 设置键盘

键盘是通过`InputDevice`配置的两个输入设备之一：

```
Section "InputDevice"
Identifier "Keyboard0"
Driver "kbd"
```

### 设置选项

`Option`行设置了调整键盘功能的各种选项，例如型号、布局和重复率。对于大多数人来说，默认值良好；你可能想要更改`AutoRepeat`选项，或者在它不存在时添加。此选项告诉`X`在你按住键时开始重复字符，以及重复的频率。它接受用引号括起来的值：第一次重复的时间和后续重复之间的时间，时间都以毫秒（`ms`）为单位。在上例中，系统等待`500ms`（半秒）进行第一次重复，之后每次重复等待`200ms`（即每秒重复五次）。

### 设置鼠标

第二个`InputDevice`节控制`X`如何处理鼠标。

```
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "Protocol" "IMPS/2"
Option "Device" "dev/input/mice"
Option "Emulate3Buttons" "no"
Option "ZAxisMapping" "4 5"
```

## 配置基础 X 特性

与键盘类似，`Identifier`（标识符）用于`Layout`（布局）部分以指定使用哪种输入设备。`Driver`行指定要使用的驱动程序；`Option`行设置鼠标控制。其中最重要的是`Device`（设备）和`Protocol`（协议）。

`Device`行告诉`X`要读取哪个Linux设备文件来访问鼠标。在示例中，它是`/dev/input/mice0`，但其他可能性还包括`/dev/mouse`（指向真实鼠标设备的指针，无论它叫什么）、`/dev/psaux`（用于`PS/2`鼠标端口）、`/dev/usb/usbmouse`（`USB`鼠标的旧标识符）、`/dev/ttyS0`（第一个`RS-232`串口鼠标端口）以及`/dev/ttyS1`（第二个`RS-232`串口鼠标端口）。如果你的鼠标还能工作（即使动作杂乱无章），请不要更改此行。如果你的鼠标无法工作，你可能需要进行尝试。

`Protocol`选项告诉`X`为鼠标移动和按键导出哪些信号。现今新鼠标最常用的协议是`IMPS/2`，它代表微软的`PS/2`鼠标端口的智能变体。（注意，“`PS/2`”既是一种硬件接口也是一种软件协议，许多鼠标即使不使用`PS/2`鼠标端口也会使用鼠标协议）。如果你的鼠标有滚轮，很有可能它就是你应该使用的协议。如果你的鼠标很旧，你可能需要尝试旧的协议，如`PS/2`、`Microsoft`或`Logitech`。

其他选项通常没有`Device`和`Protocol`选项重要。`EmulateButtons`选项告诉`X`是否将双键鼠标处理为按下中键。此选项在三键鼠标和带滚轮鼠标（滚轮兼任中键功能）上通常是禁用的。前一个示例中的`ZaxisMapping`将滚轮动作映射到第四和第五个按钮上，因为`X`必须将滚轮视为像按钮一样处理。当你向上或向下滚动时，会产生“按钮”按下信号。软件可以检测到这一点并采取相应的行动。

## 设置显示器

`X`配置中最棘手的方面之一与显示器选项有关。你在`Monitor`部分中设置这些内容，该部分往往非常大，特别是在`XFree86 3.3.6`及之前的版本中。缩短后的`Monitor`部分看起来如下：

```
"Monitor"

Identifier "Monitor0"

ModelName "VisionMaster Pro 450"

HorizSync 27.0-115.0

VertRefresh 50.0-160.0

# 我的自定义 1360x1024 模式

Modeline "1360x1024" 197.8 \
  1360 1370 1480 1072 -HSync -Vync

EndSection
```
