
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

### 计时

计时这个概念常被忽视，但对任何游戏都至关重要。除了评估精灵和其他屏幕元素的移动外，你的程序还需要显示每秒相同数量的帧。否则，游戏速度在不同处理器速度的计算机上将会不一致。一个选项是利用 `gettimeofday()`，它通常提供亚秒级的计时精度。该函数的性能因架构而异，但幸运的是，`i386` 架构表现极佳。

另一个选项是使用 `usleep()`，它的精度达到毫秒级，并在第 6 章中有详细描述。

Russell Marks，`zgv` 和 `zblast` 的作者，还建议使用 `settimer()` 在给定间隔设置一个标志。列表 14.3 展示了如何执行此操作。

### 列表 14.3 使用 `settimer()`
