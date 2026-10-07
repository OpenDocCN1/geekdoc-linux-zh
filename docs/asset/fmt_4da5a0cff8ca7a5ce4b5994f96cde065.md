
## 第 10 章 同步串行通信接口

## 列表 10.4 继续

```c
SCLOW(); /* 将 SCL 设置为已知状态 */

SDAOW(); /* 将 SDA 设置为已知状态 */

udel(DELAY); /* 让线路稳定 */

}
```

```c
SCLHigh(); /* 启动停止条件 */

SDAHigh(); /* 启动停止条件 */

}
```

```c
/*
* receiveByte
* 此函数在读取
* 的数据位时切换时钟线。I2C 通信发送
* 高位 (MSB)。
*/

unsigned char receiveByte(void)
{
unsigned char i, b;
    SDAHigh(); /* 设置 SDA 状态 */
    b = 0;
    for (i = 0; i < 8; i++)
    {
        delay(DELAY); /* 让线路稳定 */
        SCLHigh(); /* 发送时钟 */
        delay(DELAY); /* 让线路稳定 */
        b = (b << 1) | readDA(); /* 移位并或入输入位 */
        SCLOW(); /* 发送时钟 */
    }
    /* 准备下一个字节 */
    delay(DELAY);
    SCLHigh();
    delay(DELAY*2);
    SCLOW();
    return b;
}
```

```c
/*
* sendByte
* 此函数在传输
* 数据位时切换时钟线。I2C 通信先发送高位。此函数
* 允许接收端确认位（第 9 位）。
*/

unsigned char sendByte(unsigned char b)
{
    unsigned char i;
    for (i = 0; i < 8; i++) {
        if (0x80 == (b & 0x80)) /* MSB 是 0 还是 1？ */
            SDAHigh();
        else
            SDAOW();
    }
    udel(DELAY); /* 让线路稳定 */
    SCLHigh(); /* 发送时钟 */
    udel(DELAY); /* 让线路稳定 */
    SCLOW(); /* 发送时钟 */
    b = (b << 1); /* 左移 */
}
```

```c
/* 准备下一个传出的字节 */
udel(DELAY);
SDAHigh();
SCLHigh(); udelay(DELAY*2); /* 2 次延迟可以帮助你在示波器上看到 ack */
```

```c
/* 在此处读取 ack，已发送的 ack 为 0。 */
i = readDA();
SCLOW();
return i;
}
```

```c
/*
 * writei2c
 * 此函数接受地址、字符缓冲区和长度。
 * 它启动通信，发送地址，然后发送缓冲区。
 * 如果发生 ack 错误，它会通知你（打印到控制台）。
 */

unsigned char writei2c(unsigned address, unsigned char *buffer, unsigned length)
{
unsigned char i, error;
    startCommunication();
    error = sendByte(address & 0xFE);
    /* 0xFE？ I2C 地址的最后一位是读/写位 */
    if (error) /* 在地址处未收到 ack */
    {
        stopCommunication();
        printk("no ack at address 0x%2X\n",address);
        return error;
    }
    /* 在此处发送缓冲区 */
    for (i = 0; i < length; i++)
    {
        error = sendByte(buffer[i]);
    }
    if (error) /* 对于发送的字节未收到 ack */
    {
        stopCommunication();
        printk("no ack at buffer %d\n",i);
        return error;
    }
    /* 我们完成了完成了 */
    stopCommunication();
    return 0;
}
```

```c
/*
 * function read2c
* 此函数接受地址、字符缓冲区和长度。
 * 它启动通信，发送地址，然后将回复读入
 * 缓冲区。如果发生 ack 错误，它会通知你（打印到控制台）。
 */

unsigned char read2c(unsigned address, unsigned char *buffer, unsigned length)
{
unsigned char i, error;
    startCommunication();
    error = sendByte(address & 0xFE);
    /* 0xFE？ I2C 地址的最后一位是读/写位 */
    if (error) /* 在地址处未收到 ack */
    {
        stopCommunication();
        printk("no ack at address 0x%2X\n",address);
        return error;
    }
    /* 在此处读取缓冲区 */
    for (i = 0; i < length; i++)
    {
        buffer[i] = receiveByte();
    }
    if (error) /* 对于发送的字节未收到 ack */
    {
        stopCommunication();
        printk("no ack at buffer %d\n",i);
        return error;
    }
}
```

# 列表 10.4 续

```c
unsigned char i, error;
startCommunication();
error = sendByte(address | 0x01);
if (error) /* 在地址处未收到 ack */
  stopCommunication();
  printf("no ack at address 0%%2X\n",address);
  return error;
}

/* 在此处接收缓冲区的字节 */
for (i = 0; i < length; i++) {
  buffer[i] = receiveByte();
}

/* 我们完成了 */
stopCommunication();
return 0;
}

/*
* function proc_write_display
* 此函数在用户向
* /proc/trailblazer/temperature_display.0 写入内容时被调用。它包含一个
* 从数字 (0-9,a-f) 到要开启的段的映射数组
*/

static int proc_write_temperature_display(struct file,
const char *buffer,
unsigned long count, void *data) {
unsigned char e, displaybuffer[5];

/** seg 是一个段映射表。元素 0xFC 告诉
* SAA1064 开启段以显示 0。同样，
* seg 的其他条映射到 1 到 9 以及 a 到 f。
*/

unsigned char seg[] = { 0xFC, 0x60, 0xDA, 0xF2, 0x66,
0x86, 0x8E, 0xE0, 0xFE, 0xF6,
0xEE, 0x3E, 0x9C, 0x7A, 0x8E );
```

```c
if (count >= 4)
{
    displaybuffer[0] = 0x01;
    displaybuffer[1] = seg[buffer[0]-'0']; /* 减去 '0' 偏移 *
    displaybuffer[2] = seg[buffer[1]-'0']; /* 用户写入的 ascii 数字 *
    displaybuffer[3] = seg[buffer[2]-'0']; /* 映射到设备文件的 *
    displaybuffer[4] = seg[buffer[3]-'0']; /* 数字等值
e = write2c(SAA1064ADDRESS, displaybuffer, 5);

/* 用于调试
    printf("proc_write_display = %d\n",e); */
}

return 1;
}
```

```c
/*
* function init_SAA1064_rpxllf
* 此函数创建 /proc 目录项：trailblazer 和
* trailblazer/temperaturedisplay0。它找到 IMMR，然后将
* PB30 和 PB31 配置为通用 I/O、开漏和输出。
* 它初始化 SAA1064 并使其显示中间段 '-'
* 作为驱动程序加载成功的标志。
*/
```

```c
/* 创建 temperaturedisplay 并允许所有用户可读 - 0444 */
temperaturedisplay_0_file = create_proc_entry("temperaturedisplay", 0444,
    tb_dir);
if(temperaturedisplay_0_file == NULL) {
    rv = -ENOMEM;
    goto no_temperaturedisplay;
}

temperaturedisplay_0_file->data = NULL;
temperaturedisplay_0_file->read_proc = NULL;
temperaturedisplay_0_file->write_proc = &proc_write_temperature_display;
temperaturedisplay_0_file->owner = THIS_MODULE;

/* 获取 IMR */
immap = (imap_t *)mfspr(IMR & 0xFFFF0000);

/* 将 PB30 和 PB31 设置为通用 I/O */
immap->im_cpm.cp_pbbar &= -SDA;
immap->im_cpm.cp_pbbar &= -SCL;

/* 将 PB30 和 PB31 设置为开漏 */
immap->im_cpm.cp_pbodr |= SDA;
immap->im_cpm.cp_pbodr |= SCL;

/* 将 PB30 和 PB31 设置为输出 */
nimmap->im_cpm.cp_pbdbir |= SDA;
nimmap->im_cpm.cp_pbdbir |= SCL;

/* 为成功的模块加载器打印一些信息 */
printk("*IMR = 0x%04X\n",immap);
printk("*PBARAR = 0x%04X\n",immap->im_cpm.cp_pbbar);
printk("*PBDIR = 0x%04X\n",immap->im_cpm.cp_pbdir);
printk("*PBODR = 0x%04X\n",immap->im_cpm.cp_pbodr);
printk("*PDBAT = 0x%04X\n",immap->im_cpm.cp_pbdat);
buffer[0] = 0x00; /* 内部起始 SAA1064 寄存器地址 */
buffer[1] = 0x46; /* 12mA 电，所有数字开启，动态模式 */
buffer[2] = 0x02; /* 每个显示上开启 '.\.' 段 */
buffer[3] = 0x02;
buffer[4] = 0x02;
buffer[5] = 0x02;
if (write2c(SAA1064ADDRESS, buffer, 6))
{
    printf("Display failed\n");
    rv = -EREMIO;
    goto no_temperaturedisplay;
}
else
    printf("Display initialization passed\n");

/* 全部初始化 */
printk(KERN_INFO "%s %s initialized\n", MODULE_NAME, MODULE_VERSION);
return 0;

no_temperaturedisplay:
remove_proc_entry("temperaturedisplay", tb_dir);
out:
    return rv;
}
```

```c
/*
* function cleanup_SAA1064_rpxllf display to show that
* 这里的函数关闭 SAA1064 显示。它移除 /proc 项
 */

static void __exit cleanup_SAA1064_rpxllf(void)
{
    unsigned char buffer[5];
    buffer[0] = 0x00;
    buffer[1] = 0x00; /* 配置，关闭 */
    write2c(SAA1064ADDRESS, buffer, 2);

remove_proc_entry("temperaturedisplay", tb_dir);
remove_proc_entry("trailblazer", NULL);
printk(KERN_INFO "%s %s removed\n", MODULE_NAME, MODULE_VERSION);
}

module_init(init_SAA1064_rpxllf);
module_exit(cleanup_SAA1064_rpxllf);
```

# 与 Philips Semiconductor SAA1064 的 I2C 通信

```c
MODULE_AUTHOR("Craig Hollabaugh");
MODULE_DESCRIPTION("SAA1064 driver for RPX");
EXPORT_SYMBOLS;
```

`SAA1064.c` 设备驱动包含三个主要函数：

- `init_SAA64`: 这是初始化函数，创建 `/proc` 项 `trailblazer` 和 `temperaturedisplay`。
- `proc_write_display`: 当用户对 `/proc/trailblazer/temperaturedisplay` 执行操作时调用此函数。`proc_write_display()` 调用 `write2c` 与 `SAA1064` 执行实际的 I2C 通信。
- `cleanup_1064`: 这是模块函数，移除 `/proc` 项。

你可以使用以下步骤编译并测试 SAA1064 设备驱动程序：

1. 使用此命令编译 SAA1064 设备驱动程序：
```bash
root@dev1$: powerpc-linux-gcc -O2 -DKERNEL -I/usr/src/powerpc-linux/include
-c SAA1064.c
-o /tftpboot/powerpc-rootfs/tmp/SAA1064.o
```

2. 使用此命令在 RPX 上加载驱动：
```bash
# insmod SAA1064.o
IMR = 0xFA20000
PBAR = 0x1CF0
PBDIR = 0x1333
PBODR = 0x0033
PBAT = 0x0483
Display initialization passed
SAA1064 initialized
```
此控制台输出显示 SAA1064 设备驱动初始化正确。SAA1064 LED 显示 '-'

3. 使用此命令向显示器写入数字：
```bash
# echo -n 1234 > /proc/trailblazer/temperaturedisplay
```
