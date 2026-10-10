
...（注意：原文此处为不完整的句子片段，根据上下文推测应为“...程序的一部分”），建议你在主循环中每次调用它一次。或者，如果你希望程序停止并等待某些鼠标操作，请使用 `mouse_waitforupdate(void)`。

当你全部完成时，可能需要关闭鼠标。如果你使用 `mouse_init()` 初始化了鼠标，请使用 `mouse_close(void)`。如果你使用的是 `vga_setmousesupport()`，则无需执行任何操作——鼠标会自动关闭。

那么，在初始化和关闭之间可能发生哪些鼠标事件？可能性包括鼠标移动、按钮点击，以及愤怒的用户强行将鼠标从电脑上拔下。最后一种情况很难检测，但你可以使用以下三个函数来涵盖其他所有情况：

- `int mouse_getx(void);`
- `int mouse_gety(void);`
- `int mouse_getbutton(void);`

前两个函数返回鼠标的当前位置，而 `mouse_getbutton()` 显然用于检查其按钮的状态。表 15.2 列出了 `mouse_getbutton()` 的七种可能返回值，示例 15.2 展示了具体如何使用这些值。

### 示例 15.2 `mouse_getbutton()` 的机制。

```c
int button;
button = mouse_getbutton();

if (button & MOUSE_LEFTBUTTON)
{
    /* 左按钮已被按下 */
}

if (button & MOUSE_RIGHTBUTTON)
{
    /* 右按钮已被按下 */
}
/* 对所有适用的按钮代码重复上述操作 */
```

如你所见，`mouse_getbutton()` 返回的整数可以与 `MOUSE_LEFTBUTTON`、`MOUSE_RIGHTBUTTON` 等进行按位“与”运算（&），以产生有意义的值。这些位中的任何一个为 1 表示该按钮已被按下，而为 0 则表示未按下。

表 15.2 `mouse_getbutton()` 的返回代码。

| 数值 | 名称 |
| :--- | :--- |
| 4 | MOUSE_LEFTBUTTON |
| 2 | MOUSE_MIDDLEBUTTON |
| 1 | MOUSE_RIGHTBUTTON |
| 8 | MOUSE_FOURTHBUTTON |
| 16 | MOUSE_FIFTHBUTTON |
| 32 | MOUSE_SIXTHBUTTON |
| 64 | MOUSE_RESETBUTTON |

...（注意：原文此处为不完整的单词“capabilities”的片段，意为“功能/能力”）。关于此函数的完整细节，你需要查阅 man 页。不过，这里是关于 MouseCaps 结构的部分摘录：

- ◆ `int key`—在成功调用 `mouse_getcaps` 后，此值应设置为 `MOUSE_GOTCAPS`。在失败的情况下，此值及其他成员的值是未定义的。
- ◆ `int buttons`—一个位掩码，指示设备支持哪些按钮，由常量 `MOUSE_LEFTBUTTON`、`MOUSE_MIDDLEBUTTON`、`MOUSE_RIGHTBUTTON`、`MOUSE_FOURTHBUTTON`、`MOUSE_FIFTHBUTTON`、`MOUSE_SIXTHBUTTON` 和 `MOUSE_RESETBUTTON` 组成。请注意，即使鼠标上没有物理中键，只要使用支持中键的鼠标协议，`MOUSE_MIDDLEBUTTON` 也可能被设置。
- ◆ `int axes`—一个位掩码，指示设备支持哪些轴，由常量 `MOUSE_XDIM`、`MOUSE_YDIM`、`MOUSE_ZDIM`、`MOUSE_RXDIM`、`MOUSE_RYDIM` 和 `MOUSE_RZDIM` 组成。
- ◆ `int info`—一个位掩码，指示关于鼠标的其他信息。目前，唯一定义的字段是 `MOUSE_INFO_WHEEL`，它指示该鼠标是滚轮鼠标。
- ◆ `int reserved0`—保留供未来使用。
- ◆ `int reserved1`—保留供未来使用。

## 鼠标光标

现在，既然你已经基本掌握了标准的鼠标函数，我敢肯定你会想去编写一些程序。然而，你可能会感到惊讶，因为 SVGAlib 并没有为你提供鼠标光标。没错——尽管鼠标的位置被仔细追踪，但屏幕上没有任何显示。

这看起来可能是一个主要的挫折，但实际上这是一种幸事。你被赋予了自由，可以设计自己的光标。我想，希望有一个默认光标并不过分，但反过来，你也不得不背负他人糟糕的像素作品。无论你的观点如何，你仍然必须拿出*某种*东西。

你的光标可以简单到一组十字准线甚至一个点。但是，我认为大多数人寻找的是类似微软指针的东西。因此，示例 15.3 展示了我编写的相关代码。我使用的方法相当简单直接：

1.  拍摄鼠标指针将要绘制的屏幕区域的“快照”。这将用于在指针移动时恢复屏幕。别担心——它只有几个像素，不会占用太多内存。
2.  在拍摄快照的区域绘制指针/光标图标。
3.  当发生移动时，用你的快照恢复鼠标指针所在的屏幕区域。然后找到新坐标，从步骤 1 重新开始。

变量 `x` 和 `y` 指向鼠标的当前位置。正如你可能猜到的，`ox` 和 `oy`（旧 `x` 和旧 `y`）随后被用来记住其先前位置。要使用这段代码，首先调用 `draw_cursor()`。然后，你应该检测移动并使用 `move_cursor()` 更新鼠标位置。我相信还有很多其他方法可以做到这一点，但这种方法对我一直运作良好。

### 示例 15.3 制作光标的一种方法。

```c
void move_cursor(int x, int y, int ox, int oy)
{
    gl_putbox(ox, oy, 11, 19, box);
    draw_cursor(x, y);
}

void draw_cursor(int x, int y)
{
    gl_getbox(x, y, 11, 19, box);

    gl_setpixel(x, y, 254);                 /* 第 1 行 */
    gl_hline(x, (y + 1), (x + 1), 254);     /* 第 2 行 */
    gl_setpixel(x, (y + 2), 254);            /* 第 3 行 */
    gl_setpixel((x + 1), (y + 2), 255);
    gl_setpixel((x + 2), (y + 2), 254);
    gl_setpixel((x + 3), 254);               /* 第 4 行 */
    gl_hline((x + 1), (y + 3), (x + 2), 255);
    gl_setpixel((x + 3), (y + 3), 254);
    gl_setpixel(x, (y + 4), 254);            /* 第 5 行 */
    gl_hline((x + 1), (y + 4), (x + 3), 255);
    gl_setpixel((x + 4), (y + 4), 254);
    gl_setpixel(x, (y + 5), 254);            /* 第 6 行 */
    gl_hline((x + 1), (y + 5), (x + 4), 255);
    gl_setpixel((x + 5), (y + 5), 254);
    gl_setpixel(x, (y + 6), 254);            /* 第 7 行 */
    gl_hline((x + 1), (y + 6), (x + 5), 255);
    gl_setpixel((x + 6), (y + 6), 254);
    gl_setpixel((x + 7), 254);               /* 第 8 行 */
    gl_hline((x + 1), (y + 7), (x + 6), 255);
    gl_setpixel((x + 7), (y + 7), 254);
    gl_setpixel((x + 8), 254);               /* 第 9 行 */
    gl_hline((x + 1), (y + 8), (x + 7), 255);
    gl_setpixel((x + 8), (y + 8), 254);
    gl_setpixel((x + 9), 254);               /* 第 10 行 */
    gl_hline((x + 1), (y + 9), (x + 8), 255);
    gl_setpixel((x + 9), (y + 9), 254);
    gl_setpixel((x + 10), 254);              /* 第 11 行 */
    gl_hline((x + 1), (y + 10), (x + 5), 255);
    gl_hline((x + 6), (y + 10), (x + 10), 254);
    gl_setpixel((x + 11), 254);              /* 第 12 行 */
    gl_hline((x + 1), (y + 11), (x + 2), 255);
    gl_setpixel((x + 3), (y + 11), 254);
    gl_hline((x + 4), (y + 11), (x + 5), 255);
    gl_setpixel((x + 6), (y + 11), 254);
    gl_setpixel((x + 12), 254);              /* 第 13 行 */
    gl_setpixel((x + 1), (y + 12), 255);
    gl_setpixel((x + 2), (y + 12), 254);
    gl_setpixel((x + 4), (y + 12), 254);
    gl_hline((x + 5), (y + 12), (x + 6), 255);
    gl_setpixel((x + 7), (y + 12), 254);
    gl_hline((x, (y + 13), (x + 1), 254);    /* 第 14 行 */
    gl_setpixel((x + 4), (y + 13), 254);
    gl_hline((x + 5), (y + 13), (x + 6), 255);
    gl_setpixel((x + 7), (y + 13), 254);
    gl_setpixel((x, (y + 14), 254);          /* 第 15 行 */
    gl_setpixel((x + 5), (y + 14), 254);
    gl_hline((x + 6), (y + 14), (x + 7), 255);
    gl_setpixel((x + 8), (y + 14), 254);
    gl_setpixel((x + 5), (y + 15), 254);     /* 第 16 行 */
    gl_hline((x + 6), (y + 15), (x + 7), 255);
    gl_setpixel((x + 8), (y + 15), 254);
    gl_setpixel((x + 6), (y + 16), 254);     /* 第 17 行 */
    gl_hline((x + 7), (y + 16), (x + 8), 255);
    gl_setpixel((x + 9), (y + 16), 254);
    gl_setpixel((x + 6), (y + 17), 254);     /* 第 18 行 */
    gl_hline((x + 7), (y + 17), (x + 8), 255);
    gl_setpixel((x + 9), (y + 17), 254);
    gl_hline((x + 7), (y + 18), (x + 8), 254); /* 第 19 行 */
}
```

示例 15.3 中绘制的光标如图 15.2 所示，尽管放大显示了好几次。

![](img/2e475714ef8969ed272622c46473d334_317_0.png)

**图 15.2**
来自示例 15.3 的鼠标指针。

Clive Crous 设计了另一种绘制鼠标光标的方法，他的方式比我的更用户友好。他首先创建一个定义鼠标指针外观的文本数组，然后根据该数组绘制实际的指针。示例 15.4 将向你展示我的意思。

### 示例 15.4 Clive Crous 的创新鼠标代码。

```c
static char *mmouse_cursor =
{
    "..................................."
};

int mmouse_x, mmouse_y, mmouse_ox, mmouse_oy, mmouse_o1, mmouse_or;
static int mmouse_visible;

void mouse_drawmouse() {
    int dx, dy, mulit;
    char *mac = mmouse_cursor;
}
```
