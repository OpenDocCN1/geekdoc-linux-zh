
使用小部件编写 X 应用程序相对容易，但编写新的小部件要困难得多。在接下来的两章中，我们将看到如何使用 `Athena` 和 `Motif` 部件，以及如何编写新的 `Athena` 部件。

## 使用 Toolkit 设置小部件参数

X toolkit 函数 `XtSetValues` 可用于设置部件资源的值。`XtSetValues` 可用于 `Athena` 和 `Motif` 部件。每种类型的小部件（标签、文本等）都有可以使用 `XtSetValues` 设置的不同选项。`XtSetValues` 从资源核心或基础部件类开始，并遵循继承链到达小部件，设置与指定名称匹配的资源。例如，假设你正在使用 `Athena` 标签。检查文件 `Label.h`（在你的 Linux 系统上位于 `/usr/X1/include/Xaw3d`）显示了该部件的以下资源：

| Name | Class | RepType | Default Value |
|---|---|---|---|
| `background` | `Background` | `Pixel` | `XtDefaultBackground` |
| `bitmap` | `Pixmap` | `Pixmap` | `None` |
| `border` | `BorderColor` | | `XtDefaultForeground` |
| `borderWidth` | `Width` | `Dimension` | 1 |
| `cursor` | `Cursor` | | `None` |
| `cursorName` | `Cursor` | `String` | `NULL` |
| `destroyCallback` | `Callback` | | `XtCallback NULL` |
| `encoding` | `Encoding` | `unsigned char` | `XawTextEncoding8` |
| `font` | `Font` | `XFont*` | `XtDefaultForeground` |
| `foreground` | `Foreground` | `Pixel` | `XtDefaultForeground` |
| `height` | `Height` | `Dimension` | text height |
| `sensitiveBorder` | `Insensitive` | `Pixmap` | `Gray` |
| `internalHeight` | `Height` | `Dimension` | 2 |
| `internalWidth` | `Width` | `Dimension` | 4 |
| `justify` | `Justify` | | `XtJustify` |
| `label` | `Label` | | `XtJustifyCenter` |
| `leftBitmap` | `LeftBitmap` | `Pixmap` | `NULL` |
| `mappedWhenManaged` | `MappedManaged` | `Boolean` | `True` |
| `pointerColor` | `Foreground` | `Pixel` | `XtDefaultForeground` |
| `pointerColor` | `Background` | `Pixel` | `XtDefaultForeground` |
| `resize` | `Resize` | `Boolean` | `True` |
| `sensitive` | `Sensitive` | `Boolean` | `True` |
| `width` | `Width` | `Dimension` | text width |
| `x` | `Position` | `Dimension` | 0 |
| `y` | `Position` | `Dimension` | 0 |

以下是在程序中设置几个资源的示例：

```c
Widget label;

Arg args[5];

String app_resources[] = {
    {"Label.Label: Testing Athena Widget", NULL };
};

XtSetValues(args[0], XtLabel, "The label of a widget");
XtSetValues(args[1], Xtwidth, 10);
XtSetValues(args[2], Xttheight, 10);
```
