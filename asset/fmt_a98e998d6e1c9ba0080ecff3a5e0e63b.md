
- 要启动一个高为 48 像素且宽度为默认值的 `xclock`，请输入：

```
$ xclock -geometry x48 [RET]
```

您可以为 `XOFF` 和 `YOFF` 字段给出正数或负数。正 `XOFF` 值指定从屏幕左侧的位置；负值指定从右侧的位置。如果 `YOFF` 为正，则指定从屏幕顶部的位置；如果为负，则指定从屏幕底部的位置。给出这些偏移量时，您必须同时指定 `XOFF` 和 `YOFF` 的值。

要将窗口放置在桌面四个角之一，请为适当的 `XOFF` 和 `YOFF` 值使用零，如下所示：

| Geometry | Position |
| --- | --- |
| `+0+0` | Upper left-hand corner. |
| `+0-0` | Lower left-hand corner. |
| `-0+0` | Upper right-hand corner. |
| `-0-0` | Lower right-hand corner. |

⇒ 要在左下角启动默认大小的 `xclock`，请输入：

```
$ xclock -geometry +0-0 [RET]
```

或者，您可以将所有四个值包含在一行 `geometry` 中，以指定窗口的大小和位置。

⇒ 要启动一个宽 120 像素、高 100 像素、`x` 偏移量为屏幕右侧 250 像素、`y` 偏移量为屏幕顶部 25 像素的 `xclock`，请输入：

```
$ xclock -geometry 120x100-250+25 [RET]
```

使用 `-iconic` 选项以图标形式启动客户端，以便它在运行时立即显示为图标。客户端将启动，但会显示为小图标，直到您单击它为止（参见 Recipe 4.3.5 [取消 X 窗口的图标化]，第 107 页）。

⇒ 要以图标形式启动 `xclock`，但在您最大化它时在右上角打开，请输入：

```
$ xclock -geometry -0+0 -iconic [RET]
```

### 4.2.2 指定 X 窗口颜色

您在 X 会话中可用的窗口颜色取决于您的显示硬件和正在运行的 X 服务器。`xcolors` 工具将显示您 X 服务器上所有可用颜色以及用于指定它们的名称。 （颜色名称不区分大小写。）

⇒ 要列出可用颜色，请输入：

```
$ xcolors [RET]
```

Press ⌘Q to exit `xcolors`.

要指定用于窗口背景、窗口边框以及窗口本身中的文本或图形的颜色，请将颜色名称作为参数给出

to the appropriate option: `-bg` for background color, `-bd` for window border color, and `-fg` for foreground color.

⇒ To start an `xclock` with a light blue window background, type:

```
$ xclock -bg lightblue RET
```

You can specify any combination of these attributes.

⇒ To start an `xclock` with a sea green window background and a turquoise window foreground, type:

```
$ xclock -bg seagreen -fg turquoise RET
```

NOTES: The `-bordercolor`, `-background`, and `-foreground` options are synonymous with `-bd`, `-bg`, and `-fg`.

## 4.2.3 Specifying X Window Font

To specify a font for use in a window, use the `-fn` option followed by the X font name to use. (To get an X font name, use `xfontsel`; see Recipe 16.1 [Using X Fonts], page 395).

⇒ To start an `xclock` with a digital display, and specify that it use a 17-point Helvetica font for text, type:

```
$ xclock -digital -fn -*-helvetica-*-r-*-*-17-*-*-*-*-*-*-* RET
```

This command starts an `xclock` that looks like Figure 4-4.

![](img/be7f02611e5cefde1a18c788fede22f7_137_0.png)

Figure 4-4. A digital `xclock` with Helvetica type.

NOTES: If you specify the font for a shell window, you can resize it after it's running, as described in Recipe 16.14 [Resizing the Xterm Font], page 398.

The `-font` option is synonymous with `-fn`.

## 4.2.4 Specifying X Window Border Width

To specify the width of the border of an X client, use `-bw` followed by the desired width, in pixels.

⇒ To start an `xclock` with a border width of 30 pixels, type:

```
$ xclock -bw 30 RET
```

NOTES: The `-borderwidth` option is synonymous with `-bw`.

## 4.2.5 Specifying X Window Title

To specify your own title for a client, use `-title` and follow it with a quoted string for the window title. If you use a long title, you might have to specify the client width to make sure the window is long enough.

⇒ Here are two ways to use this.

- To start an `xclock` with a title of “Time,” type:

```
$ xclock -title "Time" RET
```

- To start an `xclock` 225 pixels wide with a title of “As Time Goes By,” type:

```
$ xclock -title "As Time Goes By" -geometry 225 RET
```

## 4.2.6 Specifying Attributes in an X Window

You can specify certain special attributes when an X client is already running in a window.

X applications often have up to three special menus with options for changing certain attributes. To see these menus, press and hold `CTRL` and then click one of the three mouse buttons somewhere in the client’s window. (If you have a mouse with only two buttons, click both buttons simultaneously to emulate the middle button.)

⇒ To display an X client’s third menu, press and hold `CTRL`, move the mouse pointer to somewhere in the X client’s window, and click the third mouse button.

## 4.3 Manipulating X Client Windows
