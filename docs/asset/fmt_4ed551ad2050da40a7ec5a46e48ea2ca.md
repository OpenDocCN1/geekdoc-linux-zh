
## STEP 2

顺便说一下，`Vim`是一个高级文本编辑器，我们将以它为例进行安装。进入新文件夹，`cd Vim`，然后在新的`Vim`文件夹内，将以下命令输入到终端：`wget ftp://ftp.vim.org/pub/vim/unix/vim-7.4.tar.bz2`。

![](img/f80199d101da92d953f18eaa6205b48e_51_2.png)

## STEP 4

我们现在需要解压缩文件的内容，因此输入：`tar -xf vim-7.4.tar.bz2`到终端。注意：你可以输入`tar -xf v`并按`Tab`键自动补全剩余的文件名。

![](img/f80199d101da92d953f18eaa6205b48e_51_3.png)

## STEP 5

如果你再次输入`ls`，你会注意到已创建一个新文件夹：`vim74`；在`Mint`中以浅蓝色文本表示文件夹。创建主应用的根文件夹总是很有帮助的，然后当你通过此方法升级应用时，每个单独的版本都会有自己的文件夹。

![](img/f80199d101da92d953f18eaa6205b48e_52_0.png)

## STEP 6

输入`cd vim74`进入文件夹，再次`ls`查看其内容。很可能存在相当数量的文件，其中大部分是应用的核心文件，而其他文件将被标记为`README`或`INSTALL`。明智的做法是先阅读这些文件，因为它们提供了有关安装的重要信息。

![](img/f80199d101da92d953f18eaa6205b48e_52_1.png)

## STEP 7

安装的第一部分需要你输入`./configure`。`./configure`命令会检查你的系统是否存在与应用相关的任何缺失依赖项。如果收到关于`C`编译器的错误，则输入：`sudo apt-get install build-essential`。第三方应用`Ncurses`被记录为缺失。我们需要使用以下命令安装它：`sudo apt-get install libncurses5-dev libncursesw5-dev`。

![](img/f80199d101da92d953f18eaa6205b48e_52_2.png)

## STEP 8

你可能需要继续安装新的依赖项，具体取决于应用。每次安装新的依赖项后，重新运行`./configure`，当它不再报告错误时，你可以继续安装的下一阶段。注意：你可能需要在线搜索某些错误信息。

![](img/f80199d101da92d953f18eaa6205b48e_52_3.png)

## STEP 9

成功运行`./configure`后，系统会创建一个`Makefile`。这需要通过输入：`make`到终端来“制作”。这可能需要一段时间，具体取决于应用的大小。

![](img/f80199d101da92d953f18eaa6205b48e_52_4.png)

## STEP 10

最后，你需要在终端输入：`sudo make install`。这将安装应用，并使其在系统中可供使用。完成后，你可以执行该应用，在此例中通过在终端输入`vim`或通过`Dash`搜索它。

![](img/f80199d101da92d953f18eaa6205b48e_52_5.png)

## 使用终端

```
Kernel command line: block2mtd.block2mtd=/dev/hda2,131072.rootfs root=/dev/mtdblock0 rootfstype=jffs2 init=/etc/preinit  noinintrd console=tty0 console=ttyS0,38400n8 reboot=bios
Found and enabled local APIC!
Enabling fast FPU save and restore... done.
Enabling unmasked SIMD FPU exception support... done.
Initializing CPU#0
PID hash table entries: 32 (order: 5, 128 bytes)
Detected 1991.657 MHz processor.
Console: colour VGA+ 80x25
console [tty0] enabled
console [ttyS0] enabled
Dentry cache hash table entries: 1024 (order: 0, 4096 bytes)
Inode-cache hash table entries: 1024 (order: 0, 4096 bytes)
Memory: 5112k/8128k available (1497k kernel code, 2624k reserved, 597k data, 196k init, 0k highmem)
virtual kernel memory layout:
    fixmap  : 0xffffb000 - 0xfffff000   ( 280 kB)
    vmalloc : 0xc1000000 - 0xffff7000   (1007 MB)
    lowmem  : 0xc0000000 - 0xc07f0000   ( 7 MB)
      .init : 0xc0313000 - 0xc0344000   ( 196 kB)
      .data : 0xc027653c - 0xc030bcfc   ( 597 kB)
      .text : 0xc0100000 - 0xc02753c   (1497 kB)
Checking if this processor honours the WP bit even in supervisor mode...Ok.
Calibrating delay using timer specific routine.. 4047.64 BogoMIPS (lpj=20238210)
```

## Linux Kernel 0.01

## Did You Know...

```
console.c

/*
 * This module implements the console I/O functions
 * Linux console driver
 *
 * Hopefully this will be a rather complete VT102 implementation.
 */

/* NOTE: We sometimes disable and enable interrupts for a short while
 * to put a word in video RAM, but this will work even for keyboard
 * interrupts. We know interrupts aren't enabled when getting a keyboard
 * interrupt, as we use trap-gates. Hopefully all is well.
 */

#include <linux/sched.h>
#include <linux/tty.h>
#include <asm/io.h>
#include <asm/system.h>

#define SCREEN_START 0xb8000
#define SCREEN_END   0xbffff
#define LINES 25
#define COLUMNS 80
#define SPAR 16

extern void keyboard_interrupt(void);

static unsigned long origin=SCREEN_START;
static unsigned long scr_end=SCREEN_START+LINES*COLUMNS*2;
static unsigned long pos;
static unsigned long top;
static unsigned long bottom=LINES;
static unsigned long lines=LINES*COLUMNS;
static unsigned long state;
static unsigned long spar_pos=SPAR;
static unsigned long spar_char;
static unsigned long spar_attr=0x07;
```
