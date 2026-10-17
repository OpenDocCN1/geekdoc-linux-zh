
```c
static int do_io = 1;

#ifdef KERNEL__

static int read_is_sleeping = 0;
static int write_is_sleeping = 0;
static int abort_read = 0;
static int abort_write = 0;
static int read_is_open = 0;
static int write_is_open = 0;
static int interrupts_are_enabled = 0;
static int autostart=1;

#endif

static int tick_counter=0;
```

## Listing 25.6 verbose_outb()

Listing 25.6 显示了 `outb()` 函数的包装器，它提供了可选的调试输出，并允许在没有相应硬件的情况下禁用 `outb()`。

`unsigned short word;`

### Listing 25.6 verbose_outb()

```c
void verbose_outb(int port, int value)
{
  #ifdef KERNEL__
    if(verbose_io) printf("outb%02X,%04X\n",port,value);

#else
  if(verbose_io) printk("outb(%02X,%04X)\n",port,value);
#endif

if(do_io) outb(port,value);
}
```

## 延迟函数

列表 25.7 所示的 `do_delay()` 函数仅用于用户态驱动程序，并提供步骤之间的延迟。除非 `fastdelay` 不为零，否则它将使用 `usleep()` 库，在这种它将使用延迟循环。这些延迟仅设置最小延迟；在用户态程序中，多任务处理可能会导致额外的延迟。

```c
Listing 25.7 延迟函数
#ifdef _KERNEL_
  void do_delay() {
  ;}
#else
  void do_delay() {
  int i;

  if(fastdelay>0) {
    for(i=0;i<fastdelay;i++) {
      /* dummy operation so optimizer doesn't **/
      /* eliminate loop */
      verbose_outb(word&0x00FF,base+0);
    }
  } else {
    usleep(delay);
  }
  }
#endif
```

## 状态报告

列表 25.8 显示了一个报告每个轴上步进电机位置的函数。在用户态程序中，它将被打印到 `stdout`；在内核驱动程序中，结果将存储在环形缓冲区中，以便供用户态控制程序使用 `read()`、`fget()`、`fancf()` 或类似的函数进行读取。还会报告 16 位输出字的值；这是最后输出到并行端口数据和状态寄存器的值。

## 进程间通信与网络编程

第三部分

## 列表 25.8 状态报告

```c
void report_status()
{
  char buf[128];
  int rc;
  int i;
  int len;

  sprintf(buf, "x=%d,y=%d,z=%d,word=%%0X\n", xpos,ypos,zpos,word);
  #ifdef KERNEL__
  len=strlen(buf);

  for(i=0;i<len;i++) {
    rc=ring_buffer_write(&read_buffer,&buf[i]);
  }
  /* we need to wake up read function */
  if(read_is_sleeping)
    if(debug==5) printk("stepper: waking up read\n");
    wake_up_interruptible(&read_wait);
  else
    puts(buf);
  #endif
}
```

## 步进控制

列表 25.9 显示了实际驱动步进电机的函数。`move_one_step()` 函数将每个轴移动一个半步。由于每次需要步进时驱动的下半部（bottom half）都会调用一次，因此这需要是一个增量移动而不是完整的端到端移动。在用户态版本中，将使用 `move_all()` 来完成完整的移动。

数组 `x_step`、`y_step` 和 `z_stestep` 表示为了电旋转的八个半步中的每个步骤需要设置哪些位。这些位可以更改以适应不同的布线或反转旋转的“正向”方向。变量 `flipbits` 用于反转某些位，以补偿标准并行端口接口中包含的反相器。变量 `irq_enable_bit` 将稍后用于启用并行端口卡上的中断。

`parse_one_char()` 函数实现了一个移动指令的简单解析器。它以一次一个字符模式运行；使用此函数时，下半部不需要将命令重新组成分行。

## 列表 25.9 步进控制

```c
unsigned short x_steptable[8]=
{0x0001,0x0005,0x0004,0x0006,0x0002,0x00A,0x0008,0x0009};
unsigned short y_steptable[8]=
{0x0010,0x0050,0x0040,0x0060,0x0020,0x00A,0x0080,0x0090};
unsigned short z_steptable[8]=
{0x0100,0x0500,0x0400,0x0600,0x0200,0x0A00,0x0800,0x0900};
unsigned short flipbits = 0x0B00;
unsigned short irq_enable_bit=0x1000;

void move_one_step()
{
  /* This is a simple axis routine *
  /* The axis will not move in coordinate fashion *
  unless the angle is a multiple of 45 degrees */
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

#ifndef KERNEL
if(interrupts_enabled) word |= irq_enable_bit;
#endif
/* Some of the signals are inverted */
/* output low byte to data register */
verbose_outb(word & 0xFF,base+0);

/* output high byte to control register */
verbose_outb(word >> 8,base+2);

if(verbose) report_status();
}

void move_all() {
    while(xpos!=xdest) && (ypos!=ydest) && (zpos!=zdest) {
        move_one_step();
        do_delay();
    }
}
```
