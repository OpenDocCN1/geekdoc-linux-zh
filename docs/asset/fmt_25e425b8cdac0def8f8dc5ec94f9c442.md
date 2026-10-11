
```c
#include "colormap.h"
/* 用于 new_fb_cmap() */
struct fb_cmap *new_cmap;
int entry;

fb_cmap *new_cmap = new_fb_cmap(256); /* 创建一个新的空的调色板 */
ioctl(fb_fd, FBIOETCMAP, new_cmap); /* 包含 256 个条目。 */ /* 复制当前调色板。 */
/* 用渐变填充新调色板。 */
/* 我们将完整保留前 16 种颜色供 Linux 控制台使用。 */
for(new_cmap->entry=16; entry < 256; entry++) {
    /* 从亮青色到深红色渐变。颜色值为 16 位的。 */
    new_cmap->red[entry] = 64*256;
    new_cmap->green[entry] = entry * 256 + 255;
    new_cmap->blue[entry] = entry * 256 + 255;
}

ioctl(fb_fd, FBIOUTCMAP, new_cmap);
```

## mmap

我们使用 `mmap()` 系统调用将帧缓冲区映射到程序的地址空间中。

```c
#include <sys/mman.h>
/* 用于 mmap. */
unsigned char *frame;

frame = mmap(0, fixed_info.size, PRO_READ|PRO_WRITE, MAP_SHARED, fb_fd, 0);
```

`mmap` 的第一个参数是 0，表示由 `mmap` 选择映射帧缓冲区的位置。值 `fixed_info.smem_len` 是帧缓冲区的长度。我们指定使用 `PROT_READ|PROT_WRITE` 使帧缓冲区可读可写，并使用 `MAP_SHARED` 表示内存区域的变化将传播到实际帧缓冲区。打开的帧缓冲区设备的文件描述符为 `fd`，我们指定偏移量为 0，因为我们想要映射整个帧缓冲区。

如果成功（再次提醒，查看 CD 上的源码进行错误处理），`frame` 将指向帧缓冲区内存的开始。

## 写入像素数据

现在我们已经有了调色板以及在屏幕上放置像素的方法，我们将编写一个简单的程序。

```c
/* 计算偏移量 */
visible_frame = frame + offset;

/* 绘制顶部和底部边框。 */
for(col=0; col < fixed_info.width; col++){
    visible_frame[col] = 0;
    visible_frame[(fixed_info.height-1) * fixed_info.width + col] = 0;
}

/* 绘制显示器的左右边框。 */
for(row=0; row < fixed_info.height-1; row++){
    visible_frame[row * fixed_info.width] = 0;
    visible_frame[row * fixed_info.width + fixed_info.width-1] = 0;
}

/* 在中心绘制一个正方形 */
for(row=100; row < 200; row++){
    for(col=100; col < 200; col++){
        visible_frame[row * fixed_info.width + col] = 128;
    }
}

/* 在中间绘制一个圆盘。 */
for(row=0; row < fixed_info.height; row++){
    for(col=0; col < fixed_info.width; col++){
        if((row-240)*(row-240) + (col-320)*(col-320) <= 50*50){
            visible_frame[row * fixed_info.width + col] = 255;
        }
    }
}
```

## 清理工作

此时，我们可以清理资源并退出。

```c
munmap(frame, fixed_info.size);
free(new_cmap);
```

适用于内存和存储预算紧凑的设备。如果你受到资源限制但仍想使用 X，你可能想要研究一下 TinyX，它在 `http://XFree86.org` 上被描述为“一组专为极小尺寸设计的 X 服务器家族”。关于 Xlib 的更多信息，请参阅 Adrian Nye 编写的《Xlib Programming Manual》（O'Reilly, 1994）。Wikipedia 上也有几篇关于 X 的文章，例如 `http://en.wikipedia.org/wiki/Xlib`。

图形处理的另一种方案是 SimpleMediaLayer (`SDL`)，这是一种最初为开发和移植游戏而设计的多媒体库。与 Xlib 类似，`SDL` 是跨平台的，并管理用户输入以及图形。与 Xlib 不同，`SDL` 对窗口管理仅提供极少的支持。它的内存非常小；`SDL` 的库（包括用于 TrueType 字体的 `SDL_ttf`）在剥离后约占用 330kb。

由于其简单性（我们不需要窗口支持），我们选择 `SDL` 作为 Laddie 设备的图形库，并在下一节中通过一个简单的示例来演示该库。关于 `SDL` 的更多细节，特别是关于多媒体支持，请参阅 John R. Hall 编写的《Programming Linux Games》（No Starch Press, 2001）。`SDL` 网站（`http://www.libsdl.org`）也提供了良好的 `SDL` API 文档。我们使用 `SDL_ttf` 库作为 TrueType 字体的封装，这反过来需要来自 `http://www.freetype.org` 的 Free 程序包。访问 `http://www.libsdl.org/projects/sdl_ttf` 获取文档链接。

## 使用 SDL 实现 Hello, world!

为了介绍 `SDL`，让我们通过一个简单的程序来显示 Hello, world!，监控键盘，并在按下空格键时优雅地退出（见图 11-8）。

该程序位于 Laddie CD 中；在查看细节之前，我们建议构建并运行该 CD。启动 Laddie CD，在 framebuffer UI 加载后，按 ESC 退出。

![](img/a28f80056348678270f2ea0cfefd7891_205_0.png)

图 11-8：使用 `SDL` 显示“Hello, world!”

**注意** 确保 framebuffer 没有运行非常重要，因为它会干扰我们当前的示例。顺便提一下，如果你启动 CD 时 framebuffer UI 没有自动启动，你的 framebuffer 可能会有问题。在这种情况下，请参阅附录 C 获取帮助。framebuffer UI 的显示见图 11-10。

以 root 身份使用空密码登录，切换到 `sdl_hello` 目录，然后构建并运行程序。

```
laddie:$# cd /Code/src/examples/sdl_hello
laddie:$# make
laddie:$# ./sdl_hello
```

你应该看到图 11-8 所示的。当你按下空格键时，显示将消失，你将回到命令行提示符。在本节的剩余部分中，我们将展示如何实现 `sdl_hello` 程序。

我们的程序使用单一的 `main` 函数，并初始化 framebuffer，创建一个 `surface`（`surface` 是 `SDL` 中对矩形像素区域的术语），显示该 `surface` 并处理事件。在较早的示例中，我们不会在此处显示错误处理。请参阅 CD 中 `/Code/src/examples/sdl_hello` 目录下的 `sdl_hello` 程序源码，以获取错误处理代码示例。

### 初始化库

我们示例程序中的以下几行初始化了 `SDL` 和 `SDL_ttf` 库。

```
#include "SDL.h"
#include "SDL_ttf.h"
```

- `SDL_Init(SDL_INIT_VIDEO);`

- `TTF_Init();`

- `atexit(SDL_Quit);`

`atexit(TTF_Quit);`

`SDL` 支持多个子系统，包括 `TIMER`、`AUDIO`、`VIDEO`、`CDROM` 和 `JOYSTICK`，我们在调用 `SDL_Init()` 时选择了这些系统。为了显示文本，我们在本章使用了 `VIDEO` 子系统。我们初始化了 `SDL` 对 TrueType 字体的支持。调用 `atexit` 提供了程序退出时调用的函数（`SDL_Quit` 和 `TTF_Quit`）；它们确保 `SDL` 在程序结束时干净地退出。

### 初始化 Framebuffer

为了配置 framebuffer 的分辨率和每个像素位数，我们使用函数 `SDL_SetVideoMode`。

```
SDL_Surface* Screen;
```

- `Screen = SDL_SetVideoMode(640, 480, 0);`
