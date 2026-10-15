
## 步进控制

列表 25.9 显示了实际驱动步进电机的函数。`move_one_step()` 函数将每个轴轴移动一个半步长。由于驱动程序的下半部会在每次需要步进时调用一次，因此这需要是一个简单的增量移动，而不是端到端的移动。在用户态版本中，将使用 `move_all()` 执行完全移动。

数组 `x_steptable`、`y_steptable` 和 `z_steptable` 表示每个电周期的八个半步中每一个需要设置哪些位。这些位可以更改以适应不同的接线或反转“正向”旋转方向。变量 `flipbits` 用于反转某些位，以补偿标准并行端口接口中包含的反相器。变量 `irq_enable_bit` 将后用于启用并行端口卡的中断。

`parse_one_char()` 函数实现了一个简单的移动指令解析器。它以一次一个字符的模式运行；下半部不需要将命令重新组组成行即可使用。

### 列表 25.9 步进控制

```c
unsigned short x_steptable[8]=
{0x0001,0x0005,0x0004,0x0006,0x0002,0x000A,0x0008,0x0009};
unsigned short y_steptable[8]=
{0x0010,0x0050,0x0040,0x0060,0x0020,0x00A0,0x0080,0x0090};
unsigned short z_steptable[8]=
{0x0100,0x0500,0x0400,0x0600,0x0200,0x0A00,0x0800,0x0900};
unsigned short flipbits = 0x0800;
unsigned short irq_enable_bit=0x01000;
```

```c
void move_one_step()
{
/* 这是一个非常简单的多轴移动例程 */
/* 轴不会以坐标方式移动 */
/* 除非角度是 45 度的倍数 */
if(xdest > xpos) {
xpos++;
} else if(xdest < xpos) {
xpos--;
}
if(ydest > ypos) {
ypos++;
} else if(ydest < ypos) {
ypos--;
}
if(zdest > zpos) {
zpos++;
} else if(zdest < zpos) {
zpos--;
}
word = x_steptable[xpos%8]
| y_steptable[ypos%8]
| z_steptable[zpos%8];
```

```c
#ifdef __ERNEL__
if(interrupts_are_enabled) word |= irq_enable_bit;
#endif
```

```c
/* 一些信号是反的 */
word ^= flipbits;
/* 将低字节输出到数据寄存器 */
outb( word & 0x00FF, base+0);
```

### 列表 25.9 继续

```c
/* 将高字节输出到控制寄存器 */
outb(word >> 8, base+2);
```

```c
if(verbose_move) report_status();
}
void move_all() {
    while( (xpos!=xdest) || (ypos!=ydest) || (zpos!=zdest) {
        move_one_step();
        do_delay();
    }
}
```

```c
void parse_one_char(char c) {
    static int value;
    static int dest=' ';
    static int negative=0;
    #if 0
    c = toupper(c)
    #else
    if ((c-'a') && (c<'z')) { c = c - 'a' + 'A'; }
    #endif
    switch(c) {
        case('X'):
        case('Y'):
        case('Z'):
            dest=c;
            break;
        case('='):
        case(':):
            break;
        case('-'):
            negative = !negative;
            break;
        case('*'):
            negative = 0;
        case('0'):
        case('1'):
        case('2'):
        case('3'):
        case('4'):
        case('5'):
        case('6'):
        case('7'):
        case('8'):
        case('9'):
            value *= 10;
            value += (c-'0');
            break;
        case('?'):
            report_status();
        case('\r'):
        case('\n'):
        case(','):
            if (negative) {
                value = -value;
            } if (dest=='X') {
                xuser = value;
            } else if (dest=='Y') {
                yuser = value;
            } else if (dest=='Z') {
                zuser = value;
            }
            value = 0;
            negative = 0;
            if (c=='\n' || c=='r') {
                xdest = xuser;
                ydest = yuser;
                zdest = zuser;
                #ifdef __KERNEL__
                if (debug>=3) {
                    printf("xdest=%d ydest=%d zdest=%d\n",
                           xdest, ydest, zdest);
                }
                #endif
            }
            break;
    }
}
```

## 寻址操作

列表 25.10 显示的 `stepper_seek()` 函数实际上是内核驱动特定的第一个函数，实现了下半部。每当调用 `seek()` 设置文件位置时，该函数就会被调用。注意 `open()`、`seek()` 和 `fopen()` 也可能调用 `seek()`。

参数 `inode` 和 `file` 提供指向用户打开的文件结构的指针，这些定义在 `/usr/include/linux/fs.h` 中。

参数 `offset` 和 `orig` 定义偏移量和起点（文件开头、结尾或当前位置）。这些值用于设置当前文件位置，并在 `seek` 的手册页中有详细说明。

### 列表 25.10 寻址操作

```c
#ifndef __ERNEL
static int stepper_seek(struct inode *inode,
 struct *file, off_t offset, int orig)
{
 /* 除了将 offset 置 0 外什么都不做 */
 return(file->f_pos=0);
}
#endif
```
