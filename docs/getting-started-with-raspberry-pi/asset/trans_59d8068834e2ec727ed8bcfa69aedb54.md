
## 控制台驱动程序

*控制台*（console）是一种用于显示内核生成的 `printk()` 消息的设备。如果你查看图 12.5，你会发现控制台驱动程序分为两个层级：顶层由诸如*虚拟终端*驱动程序、*打印机控制台*驱动程序以及稍后讨论的示例 *USB-UART* 控制台驱动程序等组成；底层驱动程序则负责高级操作。因此，控制台驱动程序使用了两种主要的接口定义结构。顶层控制台驱动程序围绕 `struct console` 展开，该结构定义了诸如 `setup()` 和 `write()` 等基本操作。底层驱动程序以 `struct consw` 为核心，该结构指定了诸如设置光标属性、控制台切换、屏幕清屏、调整大小以及设置调色板信息等高级操作。这些结构定义在 `include/linux/console.h` 中，定义如下：

1. 
   ```c
   struct console {
       char    name[8];
       void    (*write)(struct console *, const char *, unsigned);
       int     (*read)(struct console *, char *, unsigned);
       /* ... */
       void    (*unblank)(void);
       int     (*setup)(struct console *, char *);
       /* ... */
   };
   ```

2. 
   ```c
   struct consw {
       struct module *owner;
       const char *(*con_startup)(void);
       void        (*con_init)(struct vc_data *, int);
       void        (*con_deinit)(struct vc_data *);
       void        (*con_clear)(struct vc_data *, int, int, int, int);
       void        (*con_putc)(struct vc_data *, int, int, int);
       void        (*con_putcs)(struct vc_data *,
                       const unsigned short *, int, int, int);
       void        (*con_cursor)(struct vc_data *, int);
       int         (*con_scroll)(struct vc_data *, int, int, int, int);
       /* ... */
   };
   ```

正如你可能通过查看图 12.5 所猜测的那样，大多数控制台设备需要这两个层级的驱动程序协同工作。在许多情况下，*vt* 驱动程序是顶层控制台驱动程序。在 PC 兼容系统上，VGA 控制台驱动程序（*vgacon*）通常是底层控制台驱动程序；而在嵌入式设备上，帧缓冲控制台驱动程序（*fbcon*）往往是底层驱动程序。由于帧缓冲抽象提供了间接层，*fbcon* 与其他底层控制台驱动程序不同，它是硬件无关的。

让我们简要了解一下这两个层级控制台驱动程序的架构：

- 顶层驱动程序用规定的入口点填充 `struct console`，并使用 `register_console()` 将其注册到内核中。注销操作通过 `unregister_console()` 完成。该驱动程序与 `printk()` 进行交互。该驱动程序所属的入口点会调用关联的底层控制台驱动程序的服务。
- 底层控制台驱动程序用指定的入口点填充 `struct consw`，并使用 `register_con_driver()` 将其注册到内核中。注销操作通过 `unregister_con_driver()` 完成。当系统支持多个控制台驱动程序时，驱动程序可能会改为调用 `take_over_console()` 来注册自身并接管现有控制台；`give_up_console()` 则完成相反的操作。对于传统显示设备，底层驱动程序与顶层 vt 控制台驱动程序以及 vc_screen 字符驱动程序（允许访问虚拟控制台内存）进行交互。

一些简单的控制台，如线式打印机和下文讨论的 USB_UART，只需要一个顶层控制台驱动程序。

2.6 内核中的 fbcon 驱动程序还支持控制台旋转。PDA 和手机上的显示屏通常以纵向方式安装，而汽车仪表板和 IP 电话则是显示屏可能处于横向模式的系统示例。有时，由于经济或其他因素，嵌入式设备可能需要将横向 LCD 以纵向模式安装，或者反过来。控制台旋转支持在这些情况下非常有用。由于 fbcon 是硬件无关的，因此控制台旋转的实现也是通用的。要启用控制台旋转，请在内核配置期间启用 CONFIG_FRAMEBUFFER_CONSOLE_ROTATION，并在内核命令行中添加 `fbcon=rotate:x`，其中 x 为 0 表示正常方向，1 表示 90 度旋转，2 表示 180 度旋转，3 表示 270 度旋转。

### 设备示例：重访手机

为了学习如何编写控制台驱动程序，让我们重访第 6 章中使用的 Linux 手机。本节中的任务是开发一个通过手机中的 USB_UART 运行的控制台驱动程序。为了便于理解，图 12.7 重现了第 6 章中图 6.5 的手机。让我们编写一个控制台驱动程序，通过 USB_UART 将 `printk()` 消息发送出去。这些消息由 PC 主机捕获，并通过终端仿真会话显示给用户。

#### 图 12.7。通过 USB_UART 连接的控制台。

![](img/07cc6f9c8c74622020874f66bfb53dc4_352_0.png)

代码清单 12.3 开发了一个通过 USB_UART 工作的控制台驱动程序。该代码清单中还包含第 6 章中 USB_UART 驱动程序使用的 `usb_uart_port[]` 结构体和几个定义，以创建一个完整的驱动程序。与该代码清单相关的注释解释了驱动程序的工作原理。

图 12.7 展示了我们的示例 USB_UART 控制台驱动程序在 Linux-Video 子系统中的位置。如你所见，USB_UART 是一个简单的设备，只需要一个顶层控制台驱动程序。

### **代码清单 12.3。通过 USB_UART 连接的控制台**

```c
#include <linux/console.h>
#include <linux/serial_core.h>
#include <asm/io.h>

#define USB_UART_PORTS 2 /* 该手机有 2 个 USB_UART 端口 */

/* 每个 USB_UART 有一个 3 字节的寄存器集，包括
偏移量为 0 的 UU_STATUS_REGISTER，偏移量为 1 的
UU_READ_DATA_REGISTER，以及偏移量为 2 的 UU_WRITE_DATA_REGISTER，
如第 6 章“串行驱动程序”中的表 1 所示 */
#define USB_UART1_BASE 0xe8000000 /* USB_UART1 的内存基址 */
#define USB_UART2_BASE 0xe9000000 /* USB_UART2 的内存基址 */
#define USB_UART_REGISTER_SPACE 0x3
/* 状态寄存器中各比特位的含义 */
#define USB_UART_TX_FULL 0x20
#define USB_UART_RX_EMPTY 0x10
#define USB_UART_STATUS 0x0F

#define USB_UART1_IRQ 3
#define USB_UART2_IRQ 4
#define USB_UART_CLK_FREQ 16000000
#define USB_UART_FIFO_SIZE 32

/* 每个支持的 USB_UART 端口的参数 */
static struct uart_port usb_uart_port[] = {
{
.mapbase = (unsigned int)USB_UART1_BASE,
.iotype = UPIO_MEM, /* 内存映射 */
.irq = USB_UART1_IRQ, /* 中断号 */
.uartclk = USB_UART_CLK_FREQ, /* 时钟频率 Hz */
.fifosize = USB_UART_FIFO_SIZE, /* FIFO 大小 */
.flags = UPF_BOOT_AUTOCONF, /* UART 端口标志 */
.line = 0, /* UART 线路号 */
},
{
.mapbase = (unsigned int)USB_UART2_BASE,
.iotype = UPIO_MEM, /* 内存映射 */
.irq = USB_UART2_IRQ, /* 中断号 */
.uartclk = USB_UART_CLK_FREQ, /* 时钟频率 Hz */
.fifosize = USB_UART_FIFO_SIZE, /* FIFO 大小 */
.flags = UPF_BOOT_AUTOCONF, /* UART 端口标志 */
.line = 1, /* UART 线路号 */
}
};

/* 向 USB_UART 端口写入一个字符 */
static void
usb_uart_putc(struct uart_port *port, unsigned char c)
{
/* 等待直到 USB_UART 的 TX FIFO 中有空间。
通过查看状态寄存器中的
USB_UART_TX_FULL 比特位来检测此状态 */
while (__raw_readb(port->membase) & USB_UART_TX_FULL);

/* 将字符写入数据端口 */
__raw_writeb(c, (port->membase+l));
}

/* 控制台写入 */
static void
usb_uart_console_write(struct console *co, const char *s,
				u_int count)
{
int i;

/* 写入每个字符 */
for (i = 0; i < count; i++, s++) {
usb_uart_putc(&usb_uart_port[co->index], *s);
}
}

/* 获取通信参数 */
static void __init
usb_uart_console_get_options(struct uart_port *port,
				int *baud, int *parity, int *bits)
{
/* 读取当前设置（可能由引导加载程序设置）
或返回奇偶校验、数据位数
和波特率的默认值 */
*parity = 'n';
*bits = 8;
*baud = 115200;
}

/* 设置控制台通信参数 */
static int __init
usb_uart_console_setup(struct console *co, char *options)
{
struct uart_port *port;
int baud, bits, parity, flow;

/* 验证端口号并获取
相应结构体的句柄 */
if (co->index == -1 || co->index >= USB_UART_PORTS) {
co->index = 0;
}
port = &usb_uart_port[co->index];

/* 使用串行层提供的函数来解析选项 */
if (options) {
uart_parse_options(options, &baud, &parity, &bits, &flow);
} else {
usb_uart_console_get_options(port, &baud, &parity, &bits);
}
return uart_set_options(port, co, baud, parity, bits, flow);
}

/* 填充控制台结构体 */
```
