
2. 应用程序执行以下操作：

```c
struct fb_var_screeninfo vinfo;
fbfd = open("/dev/fb0", O_RDWR); 
vinfo.xres = 50; 
vinfo.yres = 50; 
vinfo.bits_per_pixel = 8;

ioctl(fbfd, FBIOGET_VSCREENINFO, &vinfo);
```

请注意，这等同于执行命令 `fbset -xres 50 -yres 50 -depth 8`。

3. 上一步中的 `FBIOGET_VSCREENINFO` ioctl 触发了 `myfb_check_var()` 的调用。该驱动方法会对请求的分辨率表示不满，并将其向上取整为硬件支持的最小分辨率，在此情况下为 64x64。

4. `myfb_set_par()` 由帧缓冲核心调用，将新的显示参数写入 LCD 控制器寄存器。

5. `fbset` 现在输出新的参数：

```bash
bash> fbset
mode "64x64-1423" 
# D: 5.830 MHz; H: 91.097 kHz; V: 1423.386 Hz
geometry 64 64 320 240 16
timings 171521 0 0 0 0 0 0
rgba 5/11,6/5,5/0,0/0
endmode
```

## 颜色模式

视频硬件支持的常见颜色模式包括 *伪彩色* 和 *真彩色*。在前者中，索引号被映射到 RGB 像素编码。通过选择可用颜色的子集，并使用对应于这些颜色的索引代替像素值本身，你可以减少对帧缓冲内存的需求。但是，你的硬件需要支持这种可修改颜色集（或 *调色板*）的方案。

在真彩色模式下（我们的示例 LCD 控制器支持的就是这种模式），可修改的调色板是不相关的。然而，你仍然必须满足帧缓冲控制台驱动器的需求，该驱动器仅使用 16 种颜色。为此，你需要通过直接将 16 个原始 RGB 值编码为可以馈送到硬件的位来创建一个伪调色板。这个伪调色板存储在 `fb_info` 结构的 *pseudo_palette* 字段中。在代码列表 12.2 中，`myfb_setcolreg()` 如下填充它：

```c
((u32*) (info->pseudo_palette))[color_index] =
    (red << info->var.red.offset) |
    (green << info->var.green.offset) |
    (blue << info->var.blue.offset) |
    (transp << info->var.transp.offset);
```

我们的 LCD 控制器每像素使用 16 位并采用 RGB565 格式，因此如前所述，`fb_check_var()` 方法确保红、绿、蓝值分别位于位偏移 11、5 和 0 处。除了颜色索引和红、蓝、绿色值外，`fb_setcolreg()` 还接受一个参数 `transp` 来指定所需的透明度效果。这种被称为 *alpha 混合* 的机制将指定的像素值与背景颜色结合。本示例中的 LCD 控制器不支持 alpha 混合，因此 `myfb_check_var()` 将 `transp` 的偏移量和长度设置为零。

帧缓冲抽象功能足够强大，可以将应用程序与显示面板的特性隔离开来——无论是 RGB 还是 BGR 或其他。由 `fb_check_var()` 设置的红色、蓝色和绿色偏移量通过由 `FBIOGET_VSCREENINFO` ioctl() 填充的 `fb_var_screeninfo` 结构传递到用户空间。因为像 X Windows 这样的应用程序符合帧缓冲规范，它们根据此 ioctl() 返回的颜色偏移量将像素绘制到帧缓冲中。

RGB 编码使用的位长度（本例中为 5+6+5=16）称为 *颜色深度*，它被帧缓冲控制台驱动器用于选择启动时要显示的 logo 文件（参见“启动 Logo”部分）。

## 屏幕关闭

`fb_blank()` 方法提供对显示关闭和开启的支持。这主要用于电源管理。要在导航系统的显示屏在 10 分钟无操作后将其关闭，请执行以下操作：

```bash
bash> setterm -blank 10
```

此命令向下传播到帧缓冲层，并导致 `myfb_blank()` 的调用，从而在 `CTRL_REG` 中编程相应的位。

## 加速方法

如果你的用户界面需要执行重型视频操作，如混合、拉伸、位图移动或动态渐变生成，你可能需要图形加速以获得可接受的性能。让我们简要访问一下如果视频硬件支持图形加速，你可以利用的 `fb_ops` 方法。

`fb_imageblit()` 方法将图像绘制到显示设备上。此入口点为你的驱动器提供了一个机会，利用视频控制器可能拥有的任何特殊功能来加速此操作。`cfb_imageblit()` 是帧缓冲核心提供的一个通用库函数，如果你没有加速硬件，则使用它来实现此功能。例如，它用于在启动期间将 logo 输出到屏幕上。`fb_copyarea()` 从屏幕的一个区域复制一个矩形区域到另一个区域。如果你的图形控制器没有加速此操作的功能，`cfb_copyarea()` 提供了一种优化的方式来实现此操作。`fb_fillrect()` 方法快速用像素行填充矩形。`cfb_fillrect()` 提供了一种通用的非加速方式来达到此目的。我们导航系统中的 LCD 控制器不提供加速，因此示例驱动器使用帧缓冲核心提供的通用软件优化例程来填充这些方法。

## DirectFB

DirectFB（www.directfb.org）是一个构建在帧缓冲接口之上的库，它提供了一个简单的窗口管理器框架，以及用于硬件图形加速和允许多个帧缓冲应用程序共存的虚拟接口的钩子。DirectFB 与下游的加速帧缓冲设备驱动器以及上游的感知 DirectFB 的渲染引擎（如 Cairo，www.cairographics.org）一起，有时用于图形密集型嵌入式设备，而不是像 X Windows 这样的传统解决方案。

## 帧缓冲 DMA

导航系统中的 LCD 控制器包含一个从系统内存获取图像帧的 DMA 引擎。控制器将获取的图形数据分发到显示面板。DMA 的速率支持显示屏的刷新率。使用 `myfb_probe()` 中的 `dma_alloc_coherent()` 分配一个适合一致性访问的非缓存帧缓冲。（我们在第 10 章“外围组件互连”中讨论了一致性 DMA 映射。）`myfb_set_par()` 将此分配的 DMA 地址写入 LCD 控制器中的 `DMA_REG` 寄存器。

当驱动器通过调用 `myfb_enable_controller()` 启用 DMA 时，控制器开始使用同步 DMA 将像素数据从帧缓冲传输到显示屏。因此，当 GPS 应用程序映射帧缓冲（使用 `mmap()`）并向其中写入位置信息时，像素会被绘制到 LCD 上。

## 对比度和背光

导航系统中的 LCD 控制器支持使用 `CONTRAST_REG` 寄存器进行对比度控制。驱动器通过 `myfb_ioctl()` 将此导出到用户空间。GPS 应用程序按以下方式控制对比度：

```c
unsigned int my_fd, desired_contrast_level = 100;
/* Open the frame buffer */
my_fd = open("/dev/fb0", O_RDWR);
ioctl(my_fd, MYFB_SET_BRIGHTNESS, &desired_contrast_level);
```

导航系统中的 LCD 面板使用背光照明。处理器通过 GPIO 线路控制背光逆变器，因此你可以通过摆动相应的引脚来开启或关闭灯光。内核通过 sysfs 节点抽象了一个通用的背光接口。为了与此接口结合，你的驱动器必须填充一个 `backlight_ops` 结构，其中包含获取和更新背光亮度的方法，并使用 `backlight_device_register()` 将其注册到内核。查看 `drivers/video/backlight/` 中的背光接口源代码，并在 `drivers/` 树中递归使用 grep 搜索 `backlight_device_register()` 以定位使用此接口的视频驱动器。代码列表 12.2 未实现背光操作。

## 代码列表 12.2. 导航系统的帧缓冲驱动器

```c
Code View:
#include <linux/fb.h>
#include <linux/dma-mapping.h>
#include <linux/platform_device.h>

/* Address map of LCD controller registers */
#define LCD_CONTROLLER_BASE 0x01000000
#define SIZE_REG (* (volatile u32 *) (LCD_CONTROLLER_BASE))
#define HSYNC_REG (* (volatile u32 *) (LCD_CONTROLLER_BASE + 4))
#define VSYNC_REG (* (volatile u32 *) (LCD_CONTROLLER_BASE + 8))
#define CONF_REG (* (volatile u32 *) (LCD_CONTROLLER_BASE + 12))
```
