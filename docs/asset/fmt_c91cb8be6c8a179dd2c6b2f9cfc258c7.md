
对于每个颜色表，X 服务器都会跟踪使用的单元。当服务器接收到颜色表中共享只读单元的请求时，它会确定硬件支持的最接近的颜色；然后它搜索颜色表中任何已分配的只读单元，寻找可能包含该颜色的单元。如果服务器找到这样的单元，它返回关于它的信息。否则，如果视觉类允许写入颜色表，服务器将分配一个新的单元供只读使用，将请求的颜色加载到该单元中，并返回该信息。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_769_2.png)

只读颜色表单元的优点是你可以在任何视觉效果上使用它们；要分配读写单元，你必须确保视觉类是 `DirectColor`、`PseudoColor` 或 `GrayScale`。

## 私有读写单元

私有读写单元允许你随时修改颜色表。这些单元在某些情况下是很有用的，例如当你需要更改颜色表映射时。私有读写单元具有某些优势，允许你在创建颜色表时指定像素值。在某些应用程序中，这些单元是必须的。

## XColor 结构

在 X 中，`XColor` 结构如下：

```c
typedef struct {
    unsigned long pixel; /* 像素值 */
    unsigned short red;   /* 红 (0-65535) */
    unsigned short green;  /* 绿 (0-65535) */
    unsigned short blue;   /* 蓝 (0-65535) */
    char flags;             /* 标志 */
    char pad;               /* 填充 */
};
```

当你定义颜色表时，你需要填充 `red`、`green` 和 `blue` 字段的 RGB 范围。`pixel` 字段是对应的像素值。

## 只读颜色表分配

Xlib 提供了两个函数来分配只读颜色表单元：

- `XAllocColor`
- `XAllocNamed`

![](img/a5afb9ccf4a412511e9fcfa4280141e3_770_1.png)

通常，你使用 `XAllocColor` 配合 `XParseColor`，`XParseColor` 接受颜色名称并设置 `XColor` 结构中的相应的 RGB 值。

要在默认颜色表中分配淡青色并将其作为窗口背景，例如，你可能会使用以下代码（第 5 章关于 X 应用程序中的颜色命名）：

```c
Display *disp;
XColor color;
Colormap default_cmap;
unsigned long bgpixel;

default_cmap = DefaultColormap(disp, DefaultScreen(disp));
```

/* 尝试分配“light cyan”颜色表单元 */

```c
if (XParseColor(disp, default_cmap, "light cyan", &color) != 0 ||
    XAllocColor(disp, default_cmap, &color) != 0) {
    /* 失败时使用白色背景 */
    bgpixel = WhitePixel(disp, DefaultScreen(disp));
} else {
    /* 颜色表分配成功 */
    bgpixel = color.pixel;
}
```

/* 在创建窗口时使用“bgpixel”作为背景 */

首先，`XParseColor` 设置名为“light cyan”颜色的 RGB 值。然后 `XAllocColor` 返回一个该 RGB 值的只读颜色单元。如果一切顺利，两个函数都返回非零值，`color.pixel` 成员包含了你在任何需要淡青色的地方应该使用的像素值。

# 第 23 章：Linux X 编程

`XAllocNamedColor` 与 `XAllocColor` 类似，不同在于它直接接受字符串形式的颜色名称。当你使用 `XAllocNamedColor` 时，之前分配浅青色单元格的示例将变为：

```c
XColor exact; /* 颜色的精确 RGB 定义 */
if (XAllocNamedColor(disp, default_cmap, "light cyan",
    &exact, &color) == 0)
{
    /* 失败时使用白色背景 */
    bgpixel = WhitePixel(disp, DefaultScreen(disp));
}else
{
    /* 颜色表单元格分配成功 */
    bgpixel = color.pixel;
}
```

`XAllocNamedColor` 需要两个 `XColor` 参数。在名为 `exact` 的 `XColor` 结构中，`XAllocNamedColor` 返回所请求颜色的精确 RGB 值（来自数据库）；在 `color` 中，它返回硬件支持的最接近的颜色，以及与分配的颜色表单元格对应的像素值（当分配成功时）。

## 读写颜色表分配

某些应用程序需要以特定方式在颜色表中分配颜色。例如，你可以将一个气象卫星数据的二维数组作为图像显示，其中每个像素的颜色代表一个数据点。当你显示此类图像时，你可能希望所有像素值按顺序出现，以便你轻松地将数据映射到颜色。你还可能想更改数据到颜色的映射，以突出数据的特征。这种需求最好通过分配一个连续的私有读写颜色表单元格来处理。

要分配读写单元格，请调用 `XAllocColorCells` 函数。在使用此函数之前，你必须确保屏幕的视觉类（visual class）允许向颜色表分配（该类必须是 `DirectColor`、`PseudoColor` 或 `GrayScale`）。

以下是你应该调用 `XAllocColorCells` 的方法：

```c
Display cmap; /* 分配单元格的颜色表 */
Bool contig; /* True = 分配连续平面 */
unsigned long planes[]; /* 存储平面掩码的数组 */
unsigned int nplanes; /* 要分配的平面数 */
unsigned long pixels[]; /* 存储像素值的数组 */
unsigned int npixels; /* 要分配的像素数* */
```

```c
if(!XAllocColorCells(disp, cmap, contig, planes, nplanes, pixels, pixels))
{
    /* 分配颜色单元格失败 */
    /* ... */
```

X 要求你以独特的方式指定读写颜色表单元格。你指定像素值的数量 (`npixels`) 和平面数量 (`nplanes`)；`pixels` 必须为正数，`nplanes` 可以为零或正。作为返回，服务器预留 `npixels*planes` 个颜色表单元格，并在名为 `pixels` 和 `planes` 的数组中返回可用单元格的信息。`npixels` 个值返回在 `pixels` 和 `nplanes` 数组中。

如果你想分配单个读写颜色表单元格，可以按如下方式调用 `XAllocColorCells`：

```c
Display *disp;
Colormap cmap; /* 分配单元格的颜色表*/
unsigned long pixels[1];
```

```c
if(XAllocColorCells(disp, cmap, False, NULL, 0, pixels, 1))
    /* 分配颜色单元格失败 */
    /* ... */
/ 成功分配颜色单元格。像素值为 pixels[0] *
```

在调用 `XAllocColorCells` 分配私有读写颜色表单元格后，你必须在使用它们之前将其存储在这些单元格中。使用 `XStoreColor` 来更改与单个像素值对应的 RGB 值；你必须使用 `XColor` 结构来执行此操作。将红、绿、蓝字段设置为目标原色的所需级别。将 `pixel` 设置为分配的（读写）单元格的像素值。然后按如下方式调用 `XStoreColor`：

```c
Colormap colormap;
XColor color;
/* 假设 colorcell 是之前分配的
* 写单元格。以下代码将“红色”存储
* 此单元格中 */
color.pixel = colorcell;
color.red = 65535;
color.green = 0;
color.blue = 0;
color.flags = DoRed | DoGreen | DoBlue;
XStoreColor(disp, colormap, &color);
```

`color` 中的 `flags` 字段指示颜色表单元格中对应哪种原色级别应该被更新。

要通过名称而非 RGB 分量来设置单个颜色单元格，可以使用 `XNamedColor`。要将像素值设置为红色，使用以下命令：

```c
XStoreNamedColor(disp, colormap, colorcell, DoRed | DoGreen | DoBlue);
```
