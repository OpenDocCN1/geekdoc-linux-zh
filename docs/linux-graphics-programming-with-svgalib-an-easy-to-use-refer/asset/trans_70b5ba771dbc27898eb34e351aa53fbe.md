
## 列表 14.1 访问五个内存区域。（上下文推断标题）

```c
physicalscreen = gl_allocatecontext();
gl_getcontext(physicalscreen);

gl_setcontextgavirtual(320x200x256);
virtualscreen = gl_allocatecontext();
gl_getcontext(virtualscreen);

gl_setcontext(virtualscreen);

/* draw the first screen of your background here*/

gl_getbox(0, 0, WIDTH, HEIGHT, &buffer1);
/* copy that screen to the first buffer */

/* draw the second background screen */

gl_getbox(0, 0, WIDTH, HEIGHT, &buffer2);
/* copy that screen to the second buffer */

/* draw the third background screen */

gl_getbox(0, 0, WIDTH, HEIGHT, &buffer3);
/* copy that screen to the third buffer */

/* draw the fourth background screen */

gl_getbox(0, 0, WIDTH, HEIGHT, &buffer4);
/* copy that screen to the fourth buffer */

/* draw the fifth background screen */

gl_getbox(0, 0, WIDTH, HEIGHT, &buffer5);
/* copy that screen to the fifth buffer */

gl_setcontext(physicalscreen);
```

主循环从这里开始。随着角色移动，oldx 的值会相应改变。根据位置，适当背景的一部分会被复制到物理屏幕上，如列表 14.2 所示。请注意，这是我第一次使用 `gl_copybox(int x1, int y1, int w, int h, int x2, int y2)`。

## 列表 14.2 访问五个内存区域。

```c
/* If the character's x value increases, the character is
moving to the right. Increase position accordingly, and
pull the necessary background segment from memory.
*/
while (key != 27)
{
    key = vga_getkey();

    if ((key == 'j') && (oldx > 0))
    {
        newx -= 1;
    }

    if ((key == 'l') && (oldx < 1280))
    {
        newx += 1;
    }

    if (newx > oldx)
    {
        /* slide the existing background left by one pixel */
        vga_waitretrace();
        gl_copybox(1, 0, (WIDTH - 1), HEIGHT, 0, 0);

        gl_setcontext(virtualscreen);

        /* insert the new segment on the right */
        if (oldx < 320)
        {
            x = oldx;
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer2);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 319, 0);
        } else if (oldx < 640) {
            x = oldx - 320;
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer3);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 319, 0);
        } else if (oldx < 960) {
            x = oldx - 640;
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer4);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 319, 0);
        } else {
            x = oldx - 960;
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer5);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 319, 0);
        }
        oldx = newx;
    } else if (newx < oldx) {
        /* slide the existing background right by one pixel */
        vga_waitretrace();
        gl_copybox(0, 0, (WIDTH - 1), HEIGHT, 1, 0);

        gl_setcontext(virtualscreen);

        /* insert the new segment on the left */
        if (oldx > 960) {
            x = 319 - (1280 - oldx);
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer4);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
        } else if (oldx > 640) {
            x = 319 - (960 - oldx);
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer3);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
        } else if (oldx > 320) {
            x = 319 - (640 - oldx);
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer2);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
        } else {
            x = 319 - (320 - oldx);
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer1);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
        }
        oldx = newx;
    }
}
```

## 计时

计时这个概念常被忽视，但对任何游戏都至关重要。除了评估精灵和其他屏幕元素的移动外，你的程序还需要显示每秒相同数量的帧。否则，游戏速度在不同处理器速度的计算机上将会不一致。一个选项是利用 `gettimeofday()`，它通常提供亚秒级的计时精度。该函数的性能因架构而异，但幸运的是，i386 架构表现极佳。

另一个选项是使用 `usleep()`，它的精度达到毫秒级，并在第 6 章中有详细描述。

Russell Marks，`zgv` 和 `zblast` 的作者，还建议使用 `settimer()` 在给定间隔设置一个标志。列表 14.3 展示了如何执行此操作。

### 列表 14.3 使用 settimer()。

```c
volatile int timer_flag=0;

void sighandler(int foo)
{
    timer_flag=1;
}

void start_timer(void)
{
    struct sigaction sa;
    struct itimerval itv;
    int tmp=1000000/20;      /* 20 ints/sec */

    sigemptyset(&sa.sa_mask);
    sa.sa_handler=sighandler;
    sa.sa_flags=SA_RESTART;
    sigaction(SIGALRM,&sa,NULL);

    itv.it_value.tv_sec=itv.it_interval.tv_sec=tmp/1000000;
    itv.it_value.tv_usec=itv.it_interval.tv_usec=tmp%1000000;
    setitimer(ITIMER_REAL,&itv,NULL);
}

void wait_for_timer(void)
{
    sigset_t mask,oldmask;

    sigemptyset(&mask);
    sigaddset(&mask,SIGALRM);

    /* The procmask stuff is to avoid a race condition (not actually
     * a big deal, would just rarely lose an interrupt, but FWHW...).
     */
    sigprocmask(SIG_BLOCK, &mask, &oldmask);
    if (!timer_flag)
        while (!timer_flag)
            sigsuspend(&oldmask);

    sigprocmask(SIG_UNBLOCK, &mask, NULL);
    timer_flag = 0;
}
```

Marks 接着建议使用列表 14.4 中的代码来访问列表 14.3 中列出的函数。

### 列表 14.4 使用 Russell Marks 的 set_timer()。

```c
start_timer();

while (!quit)
{
    wait_for_timer();

    do_a_frame(); /* That is, process your next image */
}
```

最后，列表 14.5 展示了管理这种复杂同步性的又一种方法。这次，代码来自 BSD 的俄罗斯方块（Tetris）实现。

### 列表 14.5 游戏计时。

```c
int wait(tvp)
{	register struct timeval *tvp;

int i;
struct timeval startv, endtv, *s;
#define NILTZ (struct timezone *)0
if (tvp) {
	(void) gettimeofday(&startv, NILTZ);
endtv = *tvp;
	s = &endtv;

} else
	s = 0;

again:
	i = 1;
	switch (select(1, (fd_set *) &1, (fd_set *) 0, (fd_set *) 0, s)) {
            case -1:
                if (tvp - 0)
                    return (-1);
                if (errno == EINTR)
                    goto again;

                stop("select failed, help");
                /* NOTREACHED */

            case 0: /* timed out */
                tvp->tv_sec = 0;
                tvp->tv_usec = 0;
                return (0);
            }
            if (tvp) {
                /* since there is input, we may not have timed out */
                (void) gettimeofday(&endtv, NULL);
                TV_SUB(&endtv, &startv);
                TV_SUB(tvp, &endtv); /* adjust *tvp by elapsed time */
            }

            return (1);
        }
```

## 来自 Russel Marks 的笔记

不直接在 `signal handler()` 中调用 `do_a_frame()` 的优势有两点——在信号处理程序中你可以安全执行的操作非常有限，而“轮询”方式意味着在速度太慢无法处理游戏的机器上，系统会优雅降级（即游戏运行缓慢，而不是完全崩溃）。此外，轮询模型比处理中断更省事。最后一点：你*可以*显式地停止计时器，但由于它只是设置一个标志，通常没有必要，你可以让它继续运行。

```c
/*
 * 'tsleep' for the current turn time (using select).
 * Eat any input that might be available.
 */
void tsleep()
{
    struct timeval tv;
    char c;

    tv.tv_sec = 0;
    tv.tv_usec = fallRate;
    while (TV_POS(&tv))
        if (rnwait(&tv) && read(0, &c, 1) != -1)
            break;
}
```

824  第 14 章

# 将所有部分整合在一起

既然你已经了解了大多数简单游戏幕后发生的事情，何不亲手尝试制作一个？也许你可以从重新编程一个旧经典开始，将其移植到 SVGAlib。我发现如果你确切知道成品的外观，编码会容易得多。显然，如果你的意图是复制现有游戏，那就不会有问题。图 14.2 展示了 Breakout（打砖块），这是 Atari 的一款老游戏，许多初出茅庐的程序员在“试水”阶段都会克隆这款游戏。

> **注意：**
> 你知道 *Breakout* 是由 Steve Jobs 和 Steve Wozniak 在 Jobs 于 Atari 工作期间创作的吗？

另一个相对简单但仍涉及计时的是俄罗斯方块（Tetris）。嘿，你可能会觉得它单调，但女孩们很喜欢它。

# 结语

希望本章介绍的基本技巧能帮助开发那些你一直想写却不知如何下手的游戏。当然，SVGAlib 是 Linux 下玩游戏的理想选择，因为它始终具有原生的全屏访问权限，更不用说其绘图功能之快速（比 Pecos 这边的任何都要快）。现在一切都巧妙地结合在一起，是不是挺令人惊叹的？

利用第 3 章和第 4 章的绘图原语、第 7 章的字体处理、第 9 章的图形文件输入以及第 10 章的动画，你现在应该能够整合出一个能与许多其他游戏相媲美的游戏了。

# 本章引入的函数摘要

以下是本章涵盖的函数摘要：

- void gl\_putboxmask(int x, int y, int w, int h, void \*dp)
- void gl\_copybox(int x1, int y1, int w, int h, int x2, int y2)

![](img/2e475714ef8969ed272622c46473d334_307_0.png)

