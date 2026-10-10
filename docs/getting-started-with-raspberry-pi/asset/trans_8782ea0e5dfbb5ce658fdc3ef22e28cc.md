
CMOS 驱动器的操作是同步完成的，且不依赖于中断。然而，许多驱动器的数据访问方法依赖于中断来收集数据，并且必须通过等待队列等数据结构与中断上下文代码进行通信。

列表 5.3 包含了属于 CMOS 驱动器的 `read()` 和 `write()` 方法。你无法直接从内核空间访问用户缓冲区，反之亦然，因此为了将 CMOS 内存内容复制到用户空间，`cmos_read()` 使用了 `copy_to_user()` 的服务。`cmos_write()` 使用 `copy_from_user()` 执行相反的操作。由于 `copy_to_user()` 和 `copy_from_user()` 在执行过程中可能会休眠，因此你在调用它们时不能持有自旋锁。

如前所述，通过操作一对 I/O 地址来访问 CMOS 内存。要从 I/O 地址读取不同大小的数据，内核提供了一系列与架构无关的函数：`in[b|w|l|sb|sl]()`。类似地，有一组例程 `out[b|w|l|sb|sl]()` 可用于写入 I/O 区域。列表 5.3 中的 `port_data_in()` 和 `port_data_out()` 使用 `inb()` 和 `outb()` 进行数据传输。

### 列表 5.3. 读取和写入

```c
/*
 * Read from a CMOS Bank at bit-level granularity
 */
ssize_t
cmos_read(struct file *file, char *buf,
          size_t count, loff_t *ppos)
{
    struct cmos_dev *cmos_devp = file->private_data;
    char data[CMOS_BANK_SIZE];
    unsigned char mask;
    int xferred = 0, i = 0, l, zero_out;
    int start_byte = cmos_devp->current_pointer/8;
    int start_bit  = cmos_devp->current_pointer%8;

    if (cmos_devp->current_pointer >= cmos_devp->size) {
        return 0; /*EOF*/
    }

    /* Adjust count if it edges past the end of the CMOS bank */
    if (cmos_devp->current_pointer + count > cmos_devp->size) {
        count = cmos_devp->size - cmos_devp->current_pointer;
    }

    /* Get the specified number of bits from the CMOS */
    while (xferred < count) {
        data[i] = port_data_in(start_byte, cmos_devp->bank_number)
                  >> start_bit;
        xferred += (8 - start_bit);
        if ((start_bit) && (count + start_bit > 8)) {
            data[i] |= (port_data_in (start_byte + 1,
                                      cmos_devp->bank_number) << (8 - start_bit));
            xferred += start_bit;
        }
        start_byte++;
        i++;
    }
    if (xferred > count) {
/* Zero out (xferred-count) bits from the MSB
    of the last data byte */
zero_out = xferred - count;
mask = 1 << (8 - zero_out);
for (i=0; 1 < zero_out; i++) {
    data[i-1] &= ~mask; mask <<= 1;
}
xferred = count;
}
if (!xferred) return -EIO;
/* Copy the read bits to the user buffer */
if (copy_to_user(buf, (void *)data, ((xferred/8)+1)) != 0) {
    return -EIO;
}

/* Increment the file pointer by the number of xferred bits */
cmos_devp->current_pointer += xferred;
return xferred; /* Number of bits read */
}

/*
 * Write to a CMOS bank at bit-level granularity. 'count' holds the
 * number of bits to be written.
 */
ssize_t
cmos_write(struct file *file, const char *buf,
    size_t count, off_t *ppos)
{
    struct cmos_dev *cmos_dev = file->private_data;
    int xferred = 0, i = 0, l, end_l, start_l;
    char *kbuf, tmp_kbuf;
    unsigned char tmp_data = 0, mask;
    int start_byte = cmos_dev->current_pointer/8;
    int start_bit = cmos_dev->current_pointer%8;

if (cmos_dev->current_pointer >= cmos_dev->size) {
    return 0; /* EOF */
}
/* Adjust count if it edges past the end of the CMOS bank */
if (cmos_dev->current_pointer + count > cmos_dev->size) {
    count = cmos_dev->size - cmos_dev->current_pointer;
}

kbuf = kmalloc((count/8)+1,GFP_KERNEL);
if (kbuf==NULL)
    return -ENOMEM;
/* Get the bits from the user buffer */
if (copy_from_user(kbuf,buf,(count/8)+1)) {
    kfree(kbuf);
    return -EFAULT;
}
/* Write the specified number of bits to the CMOS bank */
while (xferred < count) {
    tmp_data = port_data_in(start_byte, cmos_dev->bank_number);
mask = 1 << start_bit;
end_l = 8;
if ((count-xferred) < (8 - start_bit)) {
    end_l = (count - xferred) + start_bit;
}

for (l = start_bit; l < end_l; l++) {
    tmp_data &= ~mask; mask <<= 1;
}
tmp_kbuf = kbuf[i];
mask = 1 << end_l;
for (l = end_l; l < 8; l++) {
    tmp_kbuf &= ~mask;
    mask <<= 1;
}

port_data_out(start_byte,
               tmp_data | (tmp_kbuf << start_bit),
               cmos_devp->bank_number);
xferred += (end_l - start_bit);

if ((xferred < count) && (start_bit) &&
    (count + start_bit > 8)) {
    tmp_data = port_data_in(start_byte+1,
                            cmos_devp->bank_number);
    start_l = ((start_bit + count) % 8);
    mask = 1 << start_l;
    for (l=0; l < start_l; l++) {
        mask >>= 1;
        tmp_data &= ~mask;
    }
    port_data_out((start_byte+1),
                  tmp_data | (kbuf[i] >> (8 - start_bit)),
                  cmos_devp->bank_number);
    xferred += start_l;
}

start_byte++;
i++;

if (!xferred) return -EIO;
/* Push the offset pointer forward */
cmos_devp->current_pointer += xferred;
return xferred; /* Return the number of written bits */
}

/*
 * Read data from specified CMOS bank
 */
unsigned char
port_data_in(unsigned char offset, int bank)
{
    unsigned char data;

    if (unlikely(bank >= NUM_CMOS_BANKS)) {
        printk("Unknown CMOS Bank\n");
        return 0;
    } else {
        outb(offset, addrports[bank]); /* Read a byte */
        data = inb(dataports[bank]);
    }
    return data;
}

/*
 * Write data to specified CMOS bank
 */
void
port_data_out(unsigned char offset, unsigned char data,
               int bank)
{
    if (unlikely(bank >= NUM_CMOS_BANKS)) {
        printk("Unknown CMOS Bank\n");
        return;
    } else {
        outb(offset, addrports[bank]); /* Output a byte */
        outb(data, dataports[bank]);
    }
    return;
}
```

如果字符驱动器的 `write()` 方法成功返回，这意味着该驱动器已承担了对应用程序传递给它的数据的处理责任。然而，这并不保证数据已成功写入设备。如果应用程序需要这种保证，它可以调用 `fsync()` 系统调用。对应的 `fsync()` 驱动器方法确保应用程序数据从驱动器缓冲区刷新并写入设备。CMOS 驱动器不需要 `fsync()` 方法，因为在这种情况下，驱动器写入等同于设备写入。

如果用户应用程序的数据驻留在多个缓冲区中，并且需要将其发送到设备，它可以请求多次驱动器写入，但出于以下原因，这样做效率低下：

1.  多次系统调用及相关上下文切换的开销。
2.  驱动器最了解设备，因此它可能更聪明地高效地从不同缓冲区收集数据并将其分发给设备。

因此，Linux 和其他 UNIX 变体支持 `read()` 和 `write()` 的矢量版本。Linux 字符驱动器基础设施过去提供两个专门的方法来执行矢量操作：`readv()` 和 `writev()`。然而，从 2.6.19 内核版本开始，这两种方法已被整合到通用的 *Linux 异步 I/O*（AIO）层中。Linux AIO 是一个广泛的话题，超出了本文讨论的范围，因此我们只关注 AIO 提供的同步矢量功能。

矢量驱动器方法的原型如下：

```c
ssize_t aio_read(struct kiocb *iocb, const struct iovec *vector,
unsigned long count, loff_t offset);
ssize_t aio_write(struct kiocb *iocb, const struct iovec *vector,
unsigned long count, loff_t offset);
```

`aio_read()`/`aio_write()` 的第一个参数描述 AIO 操作，第二个参数是一个 `iovecs` 数组。后者是矢量函数使用的主要数据结构，包含保存数据的缓冲区的地址和长度。实际上，这种机制是第 10 章中讨论的分散/聚集 DMA 在用户空间的等价物。请参阅 `include/linux/l_io.h` 中 `iovecs` 的定义，以及 `drivers/net/tun.c` 中字符驱动器矢量方法示例实现。

- 1 在第 15 章“网络接口卡”的侧边栏“TUN/TAP 驱动器”中有讨论。

另一种数据访问方法是 `mmap()`，它将设备内存与用户虚拟内存关联起来。应用程序可以调用相应的系统调用（也称为 `mmap()`），并直接对返回的内存区域进行操作以访问驻留在设备中的内存。没有很多驱动器实现 `mmap()`，因此我们不会在这里深入探讨。相反，请参阅 `drivers/char/mem.c` 了解 `mmap()` 实现的示例。第 19 章“用户空间中的驱动器”中“访问内存区域”一节说明了应用程序如何使用 `mmap()`。我们的示例 CMOS 驱动器没有实现 `mmap()`。

你可能已经注意到，`port_data_in()` 和 `port_data_out()` 在一个名为 `unlikely()` 的宏内部封装了银行号健全性检查。两个宏 `likely()` 和 `unlikely()` 通知 GCC 相关条件评估成功的概率。GCC 在预测分支时使用此信息。因为我们标记银行健全性检查失败的可能性较小（unlikely），GCC 生成的智能代码使 `else(){}` 子句与代码流顺序地粘合在一起。对于 `if(){}` 子句则进行分支处理。如果你使用 `likely()` 而不是 `unlikely()`，情况则相反。

## Seek

内核使用内部指针来跟踪当前文件访问位置。应用程序使用 `lseek()` 系统调用请求重新定位此内部文件指针。利用 `lseek()` 的服务，你可以将文件指针重置到文件内的任何偏移量。`lseek()` 的字符驱动器对应方法是 `llseek()` 方法。`cmos_llseek()` 在 CMOS 驱动器中实现了此方法。

如前所述，CMOS 的内部文件指针是按位移动而不是按字节移动的。如果从 CMOS 驱动器读取一个字节的数据，文件指针必须移动 8，因此应用程序必须相应地执行 seek 操作。`cmos_llseek()` 还根据 CMOS 银行的大小实现了文件结束语义。

为了理解 `llseek()` 的语义，让我们从查看 `lseek()` 系统调用支持的命令开始：

- `SEEK_SET`，它将文件指针设置到提供的固定偏移量。
- `SEEK_CUR`，它根据当前位置计算偏移量。
- `SEEK_END`，它根据文件末尾计算偏移量。此命令可以使文件指针越过文件末尾，但不会改变文件大小。如果在文件末尾标记之外读取且没有明确写入数据，则返回 `nought`（零）。这种技术通常用于创建大文件。CMOS 驱动器不支持 `SEEK_END`。

