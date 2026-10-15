
|  |  |  |  |
|---|---|---|---|
| `XC_coffee_mug` | `XC_left_ptr` | `XC_sb_down_arrow` | `XC_ul_angle` |
| `XC_cross` | `XC_left_side` | `XC_sb_h_double_arrow` | `XC_umbrella` |
| `XC_cross_reverse` | `XC_left_tee` | `XC_sb_left_arrow` | `XC_ur_angle` |
| `XC_crosshair` | `XC_leftbutton` | `XC_sb_right_arrow` | `XC_watch` |
| `XC_diamond_cross` | `XC_ll_angle` | `XC_sb_up_arrow` | `XC_xterm` |
| `XC_dot` |  |  |  |

需要两个 Xlib 函数来为窗口定义光标形状。清单 27.10，`xcursor.cpp`，显示了必要的步骤。

**清单 27.10 `XCURSOR.CPP`（部分）**

```
#include <X11/Xlib.h>  // Most X programs need these headers
#include <X11/Xutil.h>
#include <X11/Xos.h>
#include <X11/cursorfont.h>

Display *display;  // X server display structure

int main()
{
...
// Specify cursor to appear when mouse pointer moves
// into the window's area
Cursor cursor =
    XCreateFontCursor(display, XC_coffee_mug);
XDefineCursor(display, win, cursor);
}
```

定义标准光标的第一步是调用 `XCreateFontCursor()`，传递 X 服务器的显示指针和表 27.3 中的一个常量。这会加载具有该值的字体字符并返回服务器中存储的光标图像的 Cursor ID。

第二步是调用 `XDefineCursor()`，传递显示指针、Window ID 和 `XCreateFontCursor()` 的结果。完成这些步骤后，将鼠标指针移入窗口会自动导致新的光标形状出现。

调用 `XUndefineCursor()` 可将光标重置为无，从而显示默认的箭头指针。除了首次创建窗口外，更改窗口光标最好随后调用 `XFlush()`，以确保 X 服务器尽快接收请求。

## 重力考虑

X 编程中有两种重力——位重力和窗口重力。

窗口的位重力指的是其内容区域或画布相对于窗口的框架。窗口重力指的是一个或多个子窗口相对于其父窗口的位置。重力值以罗盘方向表示，因此`SouthWestGravity`引用窗口的左下角，而`NorthGravity`将窗口的内容或子窗口定位在父窗口的顶部。通常，这两种重力默认均为“无”，由Xlib常量`ForgetGravity`表示——这正是我在晚餐吃太多之后希望能做到的。

> **注意**：将窗口的重力设置为`ForgetGravity`会告诉X服务器不要保留窗口的内容，即使服务器实现了后备存储特性也是如此。要使用服务器的后备存储能力（如果可用），重力必须设置为罗盘方向（如`SouthWestGravity`），或者设置为相关值之一（如`CenterGravity`或`StaticGravity`）。

为了演示重力的相关考量，清单27.11中的`xgravity.cpp`显示了一个客户端父窗口，其中包含一个作为子窗口的“粘性”子窗口。子窗口的重力设置为`NorthGravity`，使其仿佛粘在父窗口的顶部。这演示了创建一个可能用作其他对象（如一组按钮）面板的窗口的基本原理。当主客户端窗口被移动或调整大小时，X服务器会自动重新定位面板子窗口，使其始终粘在父窗口的顶部。图27.5显示了程序输出的示例。

**图 27.5** `xgravity.cpp`程序的示例输出。

![](img/6eab91cc30158075ed10d0cabbac9029_706_0.png)

**清单 27.11 `XGRAVITY.CPP`（部分）**

```
// Create subwindow "glued" to the parent using
// window gravity.
XSetWindowAttributes attributes;
attributes.win_gravity = NorthGravity;
attributes.background_pixel = intBlackColor;
unsigned long valuemask = CWWinGravity | CWBackPixel;

Window panel =
XCreateWindow(
    display,            // X Server connection
    win,                // Parent Window ID
    0, 0,               // Position
    intWidth, intHeight / 8, // Width and height
    0,                  // Border width
    CopyFromParent,     // Screen depth
```

在这里尝试不同的`win_gravity`设置，观察它们的效果。例如，要将子窗口粘在父窗口的底部，可以将其重力设置为“南重力”。但是，如果你尝试这样做，可能会惊讶地发现子窗口仍然出现在父窗口的顶部。要在底部显示子窗口，你还必须将其初始X和Y坐标值设置为类似这样：

`0, intHeight - (intHeight / 8),`

创建子窗口后（在示例程序中由名为`panel`的Window ID变量标识），像处理主客户端窗口一样，将该窗口映射到显示器。同时为面板创建一个`GC`，并在必要时使用以下语句设置其前景色：

```
XMapWindow(display, panel);
GC gcpanel = XCreateGC(display, panel, 0, NULL);
XSetForeground(display, gcpanel, whiteColor);
```

还要记得选择希望子窗口接收的事件类型。这些事件与主客户端窗口的事件一样，会到达同一个Xlib队列，并由同一个事件循环处理。在本例中，我们使用以下语句为面板窗口指定`Expose`和`ConfigureNotify`事件：

```
XSelectInput(display, panel,
    ExposureMask | StructureNotifyMask);
```

主事件循环现在会接收示例程序两个窗口的事件。要确定事件引用的是哪个窗口，需要检查事件的`window`字段。例如，示例程序的`Expose`事件通过调用`XDrawString()`在面板窗口中显示文本，如下所示：

```
case Expose:
    if (event.expose.window == panel) {
        // Sub window graphics go here
        XDrawString(display, panel, gcpanel, 10, 10,
            panelString, strlen(panelString));
    }
```

如果`expose.window`字段等于分配给`panel`的窗口ID，那么我们就知道X服务器请求客户端重绘子窗口的内容。如果该字段等于客户端窗口ID，那么程序将显示主窗口的图形（不过在本例中没有）。

此处未显示的是相对于父窗口调整子窗口大小的代码。这说明重力*只*影响窗口的相对位置。

## 平铺背景像素图

通常，窗口的背景是纯色，通常是白色或黑色。然而，除了像素值之外，你还可以指定一个像素图用作窗口的背景。像素图会被平铺（按行和列复制），因此只需一张小图像即可填充整个窗口。通常，一张16×16像素的图像就能很好地工作，但你可以使用任意尺寸的像素图。

> **提示**：某些像素图尺寸在特定的 X 服务器上可能显示得更快。要查找适合您系统的理想尺寸，请调用`XQueryBestTile()`。

创建像素图并用它平铺窗口背景的步骤，因彩色显示中的深度概念而变得复杂。要用作窗口背景，像素图必须与显示窗口的屏幕具有相同的深度。通过将像素图复制到选定位平面，有几种方法可以绕过此规则，但在大多数情况下，此处显示的步骤是用于创建适用于所有类型 X 硬件的像素图的方法。

清单 27.12（`xtile.cpp`）展示了读取位图文件并将其转换为适合绘制窗口背景的像素图所需的步骤。如图 27.6 所示，也许是出于膨胀的自我意识，加上缺乏艺术绘画技巧，我演示了用我的姓名首字母的像素图绘制窗口背景的基本步骤。（我一直钦佩那些能在 16×16 位图中创作出逼真图像的艺术家！）在清单之后，我将解释如何将相同技术用于任何像素图图像。运行程序并调整窗口大小，可以看到无论窗口大小如何，它都会绘制整个背景。只需一个 16×16 像素的小位图即可产生这种效果。
