
```c
int main(int argc, char *argv[])
{
    char *fname;
    int fbdev;
    struct fb_fix_screeninfo fixed_info;
    struct fb_var_screeninfo var_info, old_var_info;
    Fbmode *modelist;
    Fbmode *selected;
    u_int8_t pixel_r, pixel_g, pixel_b;
    int x, y;
    u_int32_t pixel_value;
    void *framebuffer;
    int framebuffer_size;
    int ppc_fix;
```

/* 让用户在命令行上指定备用 framebuffer 设备。默认值为 */

if (argc >= 2) 

    fname = argv[1];

else

    fname = "/dev/fb0";

```

```c

printf("Using framebuffer device %s.\n", fname);

```

```c

/* 打开 framebuffer 设备。 */

fbdev = open(fname, O_RDWR);

if (fbdev < 0) {

    printf("Error opening %s.\n", fname);

    return 1;

}

```

```c

/* 获取变量屏幕信息。 */

if (ioctl(fbdev, FBIIGET_VSCREENINFO, &var_info) < 0) {

    printf("Unable to retrieve variable screen info: %s\n",

    strerror(errno));

    close(fbdev);

}

```

```c

/* 备份这些信息以便稍后恢复。 */

old_var_info = var_info;

```

```c

/* 加载模式数据库。 */

modelist = FB_ParseModeDB("/etc/fb.modes");

if (modelist == NULL) {

    printf("Unable to load /etc/fb.modes.\n");

    close(fbdev);

}

```

```c

/* 切换到 640x480 模式。使用找到的第一个。 */

selected = modelist;

while (selected != NULL) {

    if (selected->xres == 640 && selected->yres == 480) {

        break;

    }

    selected = selected->next;

}

```

```c

if (selected == NULL) {

    printf("No 640x480 modes found in /etc/fb.modes.\n");

    FB_FreeModeDB(modelist);

    close(fbdev);

    return 1;

}

```

# 在 Linux 控制台下玩游戏

```c

/* 将定时数据拷贝到变量信息结构中。 */

var_info.xres = selected->xres;

var_info.yres = selected->yres;

var_info.xres_virtual = var_info.xres;

var_info.yres_virtual = var_info.yres;

var_info.pixclock = selected->dotclock;

var_info.left_margin = selected->left;

var_info.right_margin = selected->right;

var_info.upper_margin = selected->upper;

var_info.lower_margin = selected->lower;

var_info.hsync_len = selected->hsync;

var_info.vsync_len = selected->vsync;

```

```c

/* 请求 16bpp。 */

var_info.bits_per_pixel = 16;

```

```c

/* 这是同步标志的位掩码。 */

var_info.sync = selected->hync * FB_SYNC_HOR_HIGH_ACT + 

selected->vsync * FB_SYNC_VERT_HIGH_ACT + 

selected->csync * FB_SYNC_COMP_HIGH_ACT + 

selected->extsync * FB_SYNC_EXT;

```

```c

/* 这是模式属性的位掩码。 */

var_info.vmode = selected->laced * FB_VMODE_INTERLACED +

selected->doublescan * FB_VMODE_DOUBLE;

```

```c

var_info.activate = FB_ACTIVATE_NOW;

```

```c

/* 使用 ioctl 设置模式。它可能不会接受我们提供的精确参数，在这种情况下，它会修改结构。如果我们的选择完全不可接受，ioctl 将会失败。 */

if (ioctl(fbdev, FBIOGET_VSCREENINFO, &var_info) < 0) {

    printf("Unable to set variable screen info: %s\n",

           strerror(errno));

    close(fbdev);

    return 1;

}

```

```c

printf("Mode switch ioctl succeeded.\n");

printf("Got resolution %ix%i @ %ibpp.\n",

       var_info.xres, var_info.yres, var_info.bits_per_pixel);

```

# 334
# 第 8 章

```c

/* 获取固定屏幕信息。 */

if (ioctl(fbdev, FBIOGET_FSCREENINFO, &fixed_info) < 0) {

    printf("Unable to retrieve fixed info: %s\n",

    strerror(errno));

    close(fbdev);

    return 1;

}

```

```c

/* 内存映射 framebuffer。根据 SDL 源码，在 PowerPC 上补偿这种错误的实现是必要的。这对于其他架构应该不是问题（这提取自 SDL_fbdev.c） */

ppc_fix = ((long)fixed_info.smem_start - ((long)fixed_info.smem_start & ~(PAGE_SIZE-1)));

framebuffer_size = fixed_info.line_length + ppc_fix;

framebuffer = mmap(NULL, framebuffer_size,

PROT_READ | PROT_WRITE, MAP_SHARED, fbdev, 0);

if (framebuffer == NULL) {

    printf("Unable to mmap framebuffer: %s\n",

    strerror(errno));

    close(fbdev);

    return 1;

}

```

```c

printf("Mapped framebuffer.\n");

if ((fixed_info.visual == FB_VISUAL_TRUE && var_info.bits_per_pixel == 16)) {

    /* 白色像素。 */

    pixel_r = 0xFF;

    pixel_g = 0xFF;

    pixel_b = 0xFF;

    /* 当我们处理 SDL 时使用了相同的像素打包技术。 */

    pixel_value = ((pixel_r << var_info.red_offset) +

    ((pixel_g << var_info.green_offset) +

    ((pixel_b << var_info.blue_offset)));

    /* 在屏幕中心画一个像素。 */

    x = var_info.xres / 2;

    y = var_info.yres / 2;

    *((u_int16*)framebuffer + fixed_info.line_length/2 + x) = (u_int16)pixel_value;

} else {

    printf("Unsupported visual. (请求 16bpp.)\n");

    pixel_value = 0;

}

/* 等待几秒。 */

sleep(5);

/* 恢复旧模式。 */

old_var_info.activate = FB_ACTIVATE_NOW;

if (ioctl(fbdev, FBIOGET_VSCREENINFO, &old_var_info) < 0) {

    printf("Warning: Unable to restore video mode: %s\n",

    strerror(errno));

}

```

/* 关闭 fbdev。 */
munmap(framebuffer, framebuffer_size);
close(fbdev);

return 0;
```

我们通过打开 framebuffer 设备并读取显示信息开始，就像我们在列表 8-1 中做的那样。与其尝试适配，只要在源代码中注明了出处，就可以在任何程序中使用 `fbmodedb.c` 和 `fbmodedb.h`。我最初编写它们是为了包含在 SDL 中，并使用 `fb_var_screeninfo` 结构的副本在稍后恢复原始模式。

# 使用源码吧，卢克！

Linux framebuffer 接口的文档并不完善。为了编写书的这一部分并清晰理解 API，我阅读了大量的源码。这其实相当有趣；在未开发且无文档的领域中开辟道路正是编程的意义所在。

我遇到的最好的 framebuffer 参考是 SDL 源码。它的 framebuffer 处理例程编写得很好，测试充分且相当全面。虽然通过研究 `fb.h` 头文件和内核自带少量文档确实可以学会 framebuffer 编程，但 SDL 让整个接口结构变得更容易理解。如果你发现自己处于困难或晦涩的编码困境中，寻找一些已经实现了你尝试完成的代码。你可能会节省大量时间。

# 控制台输入处理

在之前的章节中，我们使用 SDL 来管理输入设备处理。然而，使用 framebuffer 控制台时，我们远离了这些便利。因此，我们需要开发访问键盘和其他输入设备的替代方法。

首先是键盘输入。我们可以通过将终端设置为原始模式并设置几个属性来实现。这看起来很丑，但有效用。下一个问题是鼠标支持，它来自 GPM 程序（存在于每个 Linux 系统中作为标准的控制台鼠标接口）。我们将简要查看这些每一个，并将该主题的详细论述留给内核头文件和 SDL 源码。

# 终端键盘输入

当程序运行在 framebuffer 控制台下时，它实际上运行在一个特殊配置的终端 `VT` 下，因此受到普通键盘处理的影响。如果我们想读取文本行（例如使用 `fgets`），这是没问题的，但游戏需要更多的输入处理。幸运的是，可以通过 `ioctl` 重新配置虚拟终端以获得对扫描码的直接访问。

这可能会变得棘手，所以我们在这里深入基础。如果你的输入处理需求更复杂，你可以尝试 SDL 的输入代码或 `libgdi` 库（一种旨在补充 GGI 图形库的输入设备）。

# 扫描码狂热

在硬件层面，键盘无非一组连接到网格的按钮、一个检测按键的小型微控制器以及一根与计算机通信的串行线。当你按下按键时，微控制器检测到*扫描（键盘扫描）*代码。它通过线将此代码发送到计算机的主板，由另一个微控制器将其转换为一个或多个扫描码字节。操作系统通过端口 60h 从主板键盘控制器读取扫描码。

X Window 系统直接处理扫描码（如果你愿意，可以很容易从内核获取），但内核可以可选地进一步该过程，将扫描码转换为键码。键码是八位值，其中低七位表示键（没问题，大多数键盘包含少于 128 个键），第八位表示按下或释放。

到目前为止这似乎很容易处理；疯狂点出现在哪里？问题在于与本地字符集（例如 ASCII）中的值关联。即使我们可能不需要响应按键按下生成文本，但我们可能需要知道这 128 个可能的键码中的哪一个

对应于，例如左箭头键。这非常麻烦，因为键盘的修饰键（Shift、Alt、Ctrl 等）会影响生成的符号。共有八种可能的修饰键，它们的任何组合都可能导致按键产生不同的符号。这些键码/修饰键的组合都与一个键映射（keymap）相关，该键映射包含按键时生成的字符。在通常情况下，如果我们想为每个键生成本地字符码，我们需要处理 $2^8=256$ 种可能的键映射（尽管大多数游戏只需要使用第一个键映射即可，它们通常只需要唯一地标识每个键，而不是生成可打印的文本）。内核提供了 `ioctl` 来查找特定映射上特定键关联的符号。

## 原始状态 (The Raw Deal)

内核提供了三种主要的键盘操作模式：*xlate*、*mediumraw* 和 *raw*。*xlate* 模式是默认模式，完全不适用于游戏，因为它只报告按按下而忽略释放（这使得我们无法像 `SDL.GetKeyState` 那样维护键盘状态表）。*mediumraw* 模式同时报告按下和释放的键码数据。最后，*raw* 模式提供直接的扫描数据（scanc）。对于游戏，最好的模式可能是 *mediumraw* 模式，因为它告诉我们按下和释放信息，并避免了我们去解析扫描序列（这些序列有点晦涩）。如果你正试图将一个旧的 DOS 游戏移植到 Linux，*raw* 模式可能是更好的选择（因为它将给你提供与以前直接从硬件读取的游戏相同的扫描码）。

要将键盘置于 *mediumraw* 模式，我们首先需要它的文件描述符。这实际上是当前 TTY（需要是一个虚拟终端）或系统控制台的文件描述符。找到一个合适的文件描述符（参见示例代码），我们可以发送带有 `K_MEDIUMRAW` 参数的 `KDSMODE` `ioctl` 调用（对于 *raw* 模式，你会使用 `K_RAW`）。请注意，这不会以任何方式影响键盘本身——它只是调整了内核对按键事件的报告。

键盘切回 *xlate* 模式（保持行缓冲禁用；参见列表 8-3 中的 `tcsetattr` 调用）。你可以自己完成完整的翻译，但其中有很多头疼的问题需要处理。

## 第 8 章

340

在 *mediumraw* 模式下，键盘上的每个键（包括左、右 Shift、Ctrl、Alt 键）在按下和释放时都会产生唯一的键码。我们可以从终端的文件描述符中将其读取为字节。

列表 8–3 展示了如何将键盘驱动程序置于 mediumraw 模式并读取按键数据。该程序与大多数 Linux 发行版附带的 `showkey` 程序非常相似。（事实上，`showkey` 的源码帮助我弄清楚了这套机制是如何工作的。）

### 代码列表 8–3 (keycodes.c)

```c
* 简单的按键查看器，与 showkey 程序相似。
在虚拟终端中运行它。如果出现问题
你无法使用控制台，请按 Alt-SysRq-R 让键盘
退出 raw 模式（这假设 Magic SysRq 已
编译到你的内核中——它非常有用！）
此代码并非源于 showkey，但感谢
作者们提供的指导。 */
```

```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <termios.h>
#include <sys/ioctl.h>
#include <linux/keyboard.h>
#include <linux/kd.h>
```

```c
* 检查给定的文件描述符是否与
本地键盘关联。
如果是，返回 1；否则返回 0（或某些因素
阻止了我们的检查）。 */
int is_keyboard(int fd)
{
```

```c
int data;

/* 查看键盘驱动程序是否识别此文件描述符。 */
data = 0;
if (ioctl(fd, KDKBTYPE, &data) != 0)
    return 0;
```

## 在 Linux 控制台上玩游戏

* 在当前的 Linux 版本中，键盘驱动程序始终对键盘类型查询响应 KB_101。可能检查上述 ioctl 是否成功或失败就足够。 */

```c
if (data == KB_84) {
    printf("找到 84 键键盘。\n");
    return 1;
} else if (data == KB_101) {
    printf("找到 101 键键盘。\n");
    return 1;
}

/* 抱歉，检查没通过。 */
return 0;
```

```c
int main()\{
    struct termios old_term, new_term;
    int kb = -1; /* 键盘文件描述符 */
    char *files_to_try[] = {"/dev/tty", "/dev/console", NULL};
    int old_mode = -1;
    int i;
```
