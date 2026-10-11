
## 视频内存复制

```c
void vga_copytoplanar256(unsigned char *virtual, int pitch, int voffset, int vpitch, int w, int h)
```

将系统内存中 `*virtual` 处的线性虚拟屏幕的一部分复制到 Mode X 风格的视频内存中。参数 `pitch` 是虚拟屏幕的逻辑宽度（以像素为单位，每个像素大小为 1 字节），`voffset` 是视频内存中的地址偏移量，`vpitch` 是屏幕的逻辑扫描线宽度，`(w, h)` 是以像素为单位复制区域的宽度和高度（宽度必须是 4 的倍数）。

```c
void vga_copytoplanar16(unsigned char *virtual, int pitch, int voffset, int vpitch, int w, int h)
```

类似于 `vga_copytoplanar256()`，但用于 16 色模式（不过测试并不充分）。假设像素以连续字节存储在虚拟屏幕中，取值范围为 0 到 15。将系统内存中 `*virtual` 处的线性虚拟屏幕的一部分复制到 Mode X 风格的视频内存中。参数 `pitch` 是虚拟屏幕的逻辑宽度（以像素为单位，每个像素大小为 1 字节），`voffset` 是视频内存中的地址偏移量，`vpitch` 是屏幕的逻辑扫描线宽度，`(w, h)` 是以像素为单位复制区域的宽度和高度（宽度必须是 4 的倍数）。

```c
void vga_copytoplane(unsigned char *virtual, int pitch, int voffset, int vpitch, int w, int h, int plane)
```

类似于 `vga_copytoplane16()`，但仅复制四个 16 色模式平面中的子集（`plane` 应在 0 到 15 范围内）。`plane` 中设置的位选择要修改的四个 16 色模式平面中的哪一个。假设像素以连续字节存储在虚拟屏幕中，取值范围为 0 到 15。将系统内存中 `*virtual` 处的线性虚拟屏幕的一部分复制到 VGA 16 色模式视频内存中。参数 `pitch` 是虚拟屏幕的逻辑宽度（以像素为单位，每个像素占 1 字节），`voffset` 是视频内存的地址偏移量，`vpitch` 是屏幕的逻辑扫描线宽度，`(w, h)` 是要复制区域的尺寸（以像素为单位，宽度必须是四的倍数）。

## 写入权限检查

```c
int vga_oktowrite(void)
```

指示当前正在运行的程序是否在屏幕上可见。也就是说，是否可以向视频内存写入数据（假设已允许后台运行）。请注意，这并不完全安全，因为视频操作期间可能会发生控制台切换中断。因此，最好避免使用此函数。通常，当程序无法访问屏幕时会被挂起，但有关替代方案，请参见 `vga_runinbackground()`。

## 管理颜色查找表

这些函数用于管理颜色查找表：

### `void vga_setpalette(int index, int r, int g, int b)`

将索引为 `index` 的当前颜色设置为 RGB 值 `r`、`g` 和 `b`，每个值的范围均为 0 到 63。此函数仅在 16 色或 256 色模式下有意义。它决定了所有通过 `vga_setcolor(index)` 绘制的像素实际引用的颜色。

请注意，设置颜色 0 会修改背景颜色，而设置 0 到 15 范围内的任何颜色都会影响 `vga_setagacolor()` 的操作。如果使用 `vga_ext_set()` 为当前模式设置了 `VGA_CLUT8` 特性，则红色、绿色和蓝色值的范围将是 0 到 255。`vgaTest` 演示展示了此函数的基本用法。

### `void vga_getpalette(int index, int *r, int *g, int *b)`

获取索引为 `index` 的颜色，并将其 RGB 值存储在 `*r`、`*g` 和 `*b` 中，每个值的范围均为 0 到 63。此函数仅在 16 色或 256 色模式下有意义。它返回所有通过 `vga_setcolor(index)` 绘制的像素实际引用的颜色。如果使用 `vga_ext_set()` 为当前模式设置了 `VGA_CLUT8` 特性，则红色、绿色和蓝色值的范围将是 0 到 255。

### `int vga_setpalvec(int start, int num, int *pal)`

将索引从 `start` 开始的 `num` 个颜色设置为 `*pal` 中给定的 RGB 值。`*pal` 包含 `num` 个 3 整数组，这些是要设置的色值。这些值按红色、绿色和蓝色的顺序排列（在 `*pal` 中需要三个连续条目才能构建一个调色板条目）。

每个颜色条目的范围是 0 到 63。此函数仅在 16 色或 256 色模式下有意义。它决定了所有通过 `vga_setcolor(start)` 绘制的像素（以及随后 `num` - 1 个颜色）实际引用的颜色。

请注意，设置颜色 0 会修改背景颜色，而设置 0 到 15 范围内的任何颜色都会影响 `vga_setagacolor()` 的操作。如果使用 `vga_ext_set()` 为当前模式设置了 `VGA_CLUT8` 特性，则红色、绿色和蓝色值的范围将是 0 到 255。此函数返回 `num` 的值。

### `int vga_getpalvec(int start, int num, int *pal)`

从颜色查找表中获取索引从 `start` 开始的 `num` 个颜色，并将 RGB 值存储在 `*pal` 中。`*pal` 包含 `num` 组 3 整数，即从第一个到最后一个调色板条目的颜色值，顺序为红色、绿色、蓝色（`*pal` 中的三个连续条目始终构成一个调色板条目）。

每个颜色条目的范围是 0 到 63。此函数仅在 16 色或 256 色模式下有意义。它显示了所有通过 `vga_setcolor(start)` 绘制的像素（以及随后 `num` - 1 个颜色）实际引用的颜色。如果使用 `vga_ext_set()` 为当前模式设置了 `VGA_CLUT8` 特性，则红色、绿色和蓝色值的范围将是 0 到 255。该函数返回 `num` 的值。

## 鼠标处理

本节中的函数涵盖鼠标处理：

- 这些函数必须包含 `<vgamouse.h>`。

### `void vga_setmousesupport(int stat)`

设置鼠标支持；0 为禁用（默认值），1 为启用。如果启用，鼠标将设置为与当前图形模式相同的屏幕分辨率。然后您可以使用各种鼠标函数。您还可以使用 `mouse_init()` 以获得更大的灵活性。然而，这不是应用程序的标准流程——鼠标是在 `/etc/vga/libvga.config` 中配置的，您的应用程序需要使用该配置。`mousetest()`、`eventtest()` 和 `spin()` 演示使用了鼠标函数。

### `int mouse_init(char *dev, int type, int samplerate)`

参见 `mouse_init_return_fid()`。

### `int mouse_init_return_fid(char *dev, int type, int samplerate)`

`return_fd` 版本返回鼠标设备的文件描述符，以便您可以对鼠标进行更多操作（但 `filehandle` 可能会在 VC 切换期间改变）。另一个版本在成功时仅返回 0。请注意，两个版本在出错时均返回 -1。

```cpp
void mouse_close(void)
```

关闭鼠标设备文件。如果在程序中使用了鼠标，应在程序末尾调用此函数，因为它会尝试恢复原始的鼠标状态（如果状态已更改）。

```cpp
int mouse_update(void)
```

此函数从鼠标缓冲区读取鼠标事件，并更新存储当前鼠标位置和按钮状态的内部 SVGAlib 变量。如果没有事件可读，此例程立即返回。如果没有事件，函数返回 0，否则返回非零值。

```cpp
void mouse_waitforupdate(void)
```

此函数从鼠标缓冲区读取鼠标事件，并更新存储当前鼠标位置和按钮状态的内部 SVGAlib 变量。如果没有事件，函数不会返回，直到发生事件为止。

```cpp
void mouse_setscale(int s)
```

此例程设置鼠标报告的运动量与一个像素大小之间的缩放因子。`scale` 越大，鼠标光标看起来移动得越慢。`scale` 可以设置为任何非零整数。负 `scales` 会导致轴翻转。目前不支持 0 到 1 之间的缩放因子，这种因子会使鼠标看起来比平时更快。如果从未调用此例程，`scale` 默认为 1。

```cpp
void mouse_setwrap(int state)
```
