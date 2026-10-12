
```c
for (iter=0; iter<198; iter++) {

    population = lambda * x * (1.0f - x);

    x_axis = (int) (population * 502.02f);

    if (x_axis > 0.0f && x_axis < 501.0f) {

        XDrawLine(display, win, gc, x_axis, y_axis, x_axis, y_axis);

    }

    x = population;

}
}
}
```

对于本书而言，决定在 X Window 中何处绘制点的算法并不有趣。以下函数被用于在窗口的 GC 中绘图：

- `XSetForeground`—用于在黑色和蓝色之间切换前景颜色
- `XDrawString`—用于使用 GC 设置的字体在窗口中绘制三个文本字符串
- `XDrawLine`—用于在窗口中绘制点

你调用 `XSetForeground` 来更改绘制文本和绘制线条的颜色。在这里，你通过绘制长度为 1 像素的线来绘制点。你可以通过切换到 `src/xlib` 并输入以下内容来运行示例 `bifurcation.c`：

```
make
./bifurcation
```

# X Toolkit API

你已经看到 Xlib API 是一个用于编写窗口应用程序的底层但非常高效的库。X toolkit（或内置）库为编写小部件（widgets）提供了更高级的编程支持。小部件是面向对象的显示对象，例如数据输入字段、数据绘图工具等。它们通常用 C 语言编写，但从面向对象的角度来说，它们支持继承，并通过公共 API 访问内部小部件数据以维护私有数据。在下一章中，我们将使用两个流行的部件集：Athena 部件和 Motif部件。

# 开始使用 X Toolkit

在应用程序使用 X toolkit 之前，必须在任何其他 toolkit 函数之前调用以下函数（`String` 类型定义为 `char *`，`Cardinal` 定义为 `int`）：

```c
XtInitialize(String shell_name,
              String application_class,
              XrOptionDescRec *options,
              Cardinal num_options,
              int *argc, char **argv)
```

`name` 和 `class` 参数指定了应用程序顶层部件的名称和类。通常，你可以为应用程序起一个有意义的名字，然后通过将应用程序名称的首字母大写来创建一个类名。`options` 参数通常可以指定为 `NULL`，表示没有特殊选项，或使用 `NULL` 传递选项。最后两个参数是传递给应用程序 `main` 函数的参数（通过移除任何特定参数进行修改）。

X toolkit 使用指定为字符字符串的资源。为了提高程序的可读性，X toolkit 和 Xlib 包含了头文件，这些文件定义了资源字符串的常量：

```c
#define Xtwidth "width"
#define Xtheight "height"
#define Xtlabel "label"
```

使用小部件编写 X 应用程序相对容易，但编写新的小部件要困难得多。在接下来的两章中，我们将看到如何使用 Athena 和 Motif 部件，以及如何编写新的 Athena 部件。

# 使用 Toolkit 设置小部件参数

X toolkit 函数 `XtSetValues` 可用于设置部件资源的值。`XtSetValues` 可用于 Athena 和 Motif 部件。每种类型的小部件（标签、文本等）都有可以使用 `XtSetValues` 设置的不同选项。`XtSetValues` 从资源核心或基础部件类开始，并遵循继承链到达小部件，设置与指定名称匹配的资源。例如，假设你正在使用 Athena 标签。检查文件 `Label.h`（在你的 Linux 系统上位于 `/usr/X1/include/Xaw3d`）显示了该部件的以下资源：

| Name | Class | RepType | Default Value |
|---|---|---|---|
| background | Background | Pixel | XtDefaultBackground |
| bitmap | Pixmap | Pixmap | None |
| border | BorderColor | | XtDefaultForeground |
| borderWidth | Width | Dimension | 1 |
| cursor | Cursor | | None |
| cursorName | Cursor | String | NULL |
| destroyCallback | Callback | | XtCallback NULL |
| encoding | Encoding | unsigned char | XawTextEncoding8 |
| font | Font | XFont* | XtDefaultForeground |
| foreground | Foreground | Pixel | XtDefaultForeground |
| height | Height | Dimension | text height |
| sensitiveBorder | Insensitive | Pixmap | Gray |
| internalHeight | Height | Dimension | 2 |
| internalWidth | Width | Dimension | 4 |
| justify | Justify | | XtJustify |
| label | Label | | XtJustifyCenter |
| leftBitmap | LeftBitmap | Pixmap | NULL |
| mappedWhenManaged | MappedManaged | Boolean | True |
| pointerColor | Foreground | Pixel | XtDefaultForeground |
| pointerColor | Background | Pixel | XtDefaultForeground |
| resize | Resize | Boolean | True |
| sensitive | Sensitive | Boolean | True |
| width | Width | Dimension | text width |
| x | Position | Dimension | 0 |
| y | Position | Dimension | 0 |

以下是在程序中设置几个资源的示例：

```c
Widget label;
Arg args[5];
String app_resources[] = {
    {"Label.Label: Testing Athena Widget", NULL };
XtSetValues(args[0], XtLabel, "The label of a widget");
XtSetValues(args[1], Xtwidth, 10);
XtSetValues(args[2], Xttheight, 10);
```

# 窗口编程

`draw_bifurcation` 函数非常简单：

```c
void draw_bifurcation(Window win, GC gc, Display *display,
int screen, XColor font_color) {
    float lambda = 0.1;
    float x = 0.1;
    float population = 0.0;
    int x_axis, y_axis, iter;

    XSetForeground(display, win, gc, font_color.pixel);

    XDrawString(display, win, gc, 236, 22,
        "Extinction", strlen("Extinction"));

    XDrawString(display, win, gc, 16, 41,
        "Steady state", strlen("Steady state"));

    XDrawString(display, win, gc, 334, 123,
        "Period doubled", strlen("Period doubled"));
```
