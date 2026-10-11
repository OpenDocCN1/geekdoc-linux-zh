
```
Kernel command line: block=/dev/sda2 rootfs=rootfs console=tty0 reboot-bios and enabled local APIC:
Enabling FPU save and restore... done.
Enabling unmasked SIMD FPU support... done.
Initializing PID table entries: 32 (order: 0, 128 bytes)
Detected Intel 8086 CPU @600MHz processor.
Console: white VGA:25
console [tty0] enabled
console [tty0] enabled
Dentry cache table entries: 1024 (order: 0, 4096 bytes)
Inode cache table entries: 1024 (order: 0, 4096 bytes)
Memory: 512K/512K available (197k code, 26k reserved, 597k data, 196k init)
virtual kernel memory layout:
fixmap : 0xffbf900 - 0xffff00 (280 KB)
valloc : 0xc0000000 - 0xcfff700 (1 MB)
lowmem : 0xc0000000 - 0xc7f0000 (7 MB)
.init : 0xc313000 - 0xc344000 (196 KB)
.data : 0xc27653c - 0xc30bcfc (597 KB)
.text : 0xc100000 - 0xc27653c (1497 KB)
Checking if this processor honours the WP bit even in supervisor mode...Ok.
Calibrating delay using timer specific routine.. 476 MIPS (lp)=238
```

# Linux Kernel 0.01

```c
/*
 * console.c
 * 此模块实现了控制台函数
 * void init(void) {
 *    struct tty_struct *queue;
 *    希望这将是一个完整的 VT 实现。
 * */

 * 注意：我们有时会短暂地禁用并启用中断
 * (为了在视频中写入字符)，但即使对于键盘编码器
 * 同样有效，只要在获取中断时没有禁用中断
 * 就像我们做的那样。希望一切顺利。

#include <linux/sched.h>
#include <linux/tty.h>
#include <asm/system.h>

#define SCREEN_START 0x8000
#define SCREEN_END 0x0000
#define LINES 25
#define COLUMNS 80
#define VERB 1

static void keyboard_interrupt(void) {
    static unsigned long sc_end=SCREEN_START+LINES*COLUMNS-2;
    static unsigned long m_x;
    static unsigned long m_y;
    static unsigned long top=0,bottom-LINES;
    static unsigned long lines,columns=COLUMNS;
    static unsigned long status=0;
    static unsigned long key_par=0;
    static unsigned long ques=0;
    static unsigned char attr=0xD;
```

# 使用终端创建文件

步骤 5：假设你现在想要创建一个文本文件，我们将使用主窗口以及完整的内容来操作。然后，输入：`cat > Test2.txt`。这将创建 `Test2.txt` 文件并将其放入终端编辑器。

步骤 8：`Xed` 是一个 GUI 应用程序，你可以通过应用窗口输入文本并保存文件（或任何文件），可以使用其顶部菜单栏的“文件 > 保存 > 另存为”功能来实现。

```
File Edit View Search Terminal Help
davidid@david-min ~ $ mkdir Test
davidid@david-min ~ $ cd Test
davidid@david-min ~ $ touch Test.txt
Test.txt
davidid@david-min ~ $ cat > Test2.txt
.txt
```

步骤 6：你会发现光标在 `cat > Test2.txt` 命令下方闪烁，带有通常的提示符。这将允许你输入文件将包含的文本。然后按 `Ctrl+D` 编辑并保存内容到文件中。

步骤 9：如果你更倾向于编辑/保存/创建文件，可以使用 `Nano`。`Nano` 是一个简单的基于文本的编辑器。要尝试它，输入 `nano Test2.txt`。这里屏幕底部有一个菜单。你可以在 `Nano` 中保存任何内容，按 `Ctrl+X` 并遵循屏幕上的指令。

```
File Edit View Search Terminal Help
davidid@david-min ~ Test.txt
davidid@david-min ~ $ cat Test.txt
This is some text
This is some text
davidid@david-min ~ $ cat > Test2.txt
This is some text
This is entered using the cat command from the Terminal. Cool, isn't it. Pressing Ctrl+D now.
Test2.txt
```

步骤 7：当然，你必须使用终端向文件输入文本。Mint 自带了 `Xed` 编辑器，它类似于 Windows 记事本。要在 `Xed` 中查看之前创建的文件，在终端中输入：`xed Test2.txt`，文本并按回车。

步骤 10：我们已经使用终端启动了一个 Mint 应用。`Xed` 也可以通过在终端内启动。例如，尝试：`firefox` 并按回车。关闭 `Firefox` 返回终端。通过知道应用程序的名称，就可以从终端运行它。此外，输入 `firefox` 可以让你使用终端。

```
File Edit View Search Terminal Help
File: Test2.txt
This is entered using the cat command from the Terminal. Cool, isn't it. Pressing Ctrl+D now...
```

![](img/383b23573296234863a9f25dc7161abc_56_0.png)

![](img/383b23573296234863a9f25dc7161abc_56_1.png)

# 创建和删除目录

与在终端中创建文件一样，你也可以创建和删除目录（如果你愿意也可以称为文件夹）。目录构成了文件系统的结构；如果没有逻辑目录，文件系统将陷入彻底的混乱。

## 管理文件夹

如何在终端中创建和删除文件夹是 Mint（实际上是整个 Linux）的一项需要掌握的重要技能。以下是你可以尝试的基础知识。

步骤 1：打开终端后，执行 `cd ~` 以确保你在自己的主目录（Home directory）。现在输入 `ls` 查看你当前位于主目录中的文件夹。你会发现文件夹在 Mint 中以青色（浅蓝色）标记。让我们从创建一个目录开始。输入：`mkdir testdir`。

步骤 3：如果你再次输入命令 `mkdir testdir`，你将收到一条消息：`mkdir: cannot create directory 'testdir': file exists`。不言而喻，在当前目录下只能有一个唯一命名的目录。但是，由于 Linux 是大小敏感的，你可以拥有 `Testdir`、`testDIR` 等。

![](img/383b23573296234863a9f25dc7161abc_57_0.png)

步骤 2：如果你现在再次输入 `ls`，你会发现新目录 `testdir` 已经与主区域的其他文件夹一起被创建。显然 `mkdir` 命令是创建目录的，你已经猜出它代表 Make Directory（创建目录）。

步骤 4：你可以在已经创建的目录内创建子目录。例如，通过 `cd testdir/` 进入目录以列出文件夹结构。自然那里什么都没有，因为你刚刚创建了该目录。现在通过 `cd ..` 返回主目录并输入 `mkdir reports`。返回测试目录，`cd testdir/` 并 `ls`。

![](img/383b23573296234863a9f25dc7161abc_57_1.png)
