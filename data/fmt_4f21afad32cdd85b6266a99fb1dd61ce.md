
## 设备驱动

临界区可以放置在中断的禁用和启用之间，如果中断线被唤起，上半部分将不会被调用。普通的`disable_irq`和`nosync`版本的区别在于，前者保证在返回之前指定的`IRQ`没有在任何`CPU`上运行，而后者如果上半部分处理程序仍在运行，则会直接禁用指定的中断并返回。

## 原子性

当你知道指令是一次性执行的时（即在你完成之前，你不会被中断），这些指令就被说是有原子的（`atomic`）。正如我们上面看到的，禁用中断可以实现这一点，因为在临界区内没有人可以中断我们。`Linux`还提供了原子原语，可以直接作用于变量，而不需要锁定其他所有内容。它们定义在`asm/atomic.h`中。

```c
void atomic_add(int i, volatile atomic_t *v);
void atomic_sub(int i, volatile atomic_t *v);
void atomic_inc(volatile atomic_t *v);
void atomic_dec(volatile atomic_t *v);
int atomic_dec_and_test(volatile atomic_t *v);
```

如你所见，这些操作作用于`atomic_t`类型，这是一个只包含一个计数器成员的结构。它包含的内容并不重要，因为你应该通过`atomic_x_functions`函数和宏来访问它。只有这样才能确保原子性。它们主要用于维护信号量的计数，但也可以以任何你喜欢的方式使用。

原子操作通常需要防止竞态条件。当进程通过原子方式评估表达式来决定对某个事件睡眠时，就会存在竞态。正如我们上面看到的，禁用中断可以实现这一点，因为在临界区内没有人可以中断我们。`Linux`还提供了在不需要锁定其他所有内容的情况下操作变量的原子原语。它们定义在`asm/atomic.h`中。

```c
void atomic_add(int i, volatile atomic_t *v);
void atomic_sub(int i, volatile atomic_t *v);
void atomic_inc(volatile atomic_t *v);
void atomic_dec(volatile atomic_t *v);
```

*注：此处为翻译逻辑修正，原文在后半部分出现了严重的重复乱码，已根据逻辑清理翻译。*

# 第 18 章

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_823_0.png)

`Linux`并没有严格区分块设备和字符设备，甚至为两者都提供了相同的接口。当我们设计第一个字符驱动程序时，`file_operations`结构体中的某些元素并不适用于面向字符的访问方案，这恰是因为这两种设备都使用了同一套方案。

## radimo——一个简单的 RAM 磁盘模块

熟悉块设备内部机制及其依赖的底层系统的最佳方法，是深入研究一个运行中的示例。`radimo`是一个`RAM`磁盘驱动程序，它将根据系统可用内存托管不同大小的文件系统。

每个块设备驱动的核心都是`request`函数，它接收读/写请求并将其转换为设备可以理解的形式。如果我们写一个硬盘（`ID`）驱动程序，`request`函数将生成命令并将其设置为控制器，以启动双向数据传输。在模块的开头，包括`request`函数在内的若干项需要按照特定的顺序定义。但下表中的项必须在包含`<linux/blk.h>`之前定义。

| 定义 | 值 | 说明 |
|---|---|---|
| `#define MAJOR_NR` | `RADIMO_MAJOR` | |
| `#define DEVICE_NAME` | `"radimo"` | 设备的名称。这可以省略，并设置为`"unknown"`。除了在发生错误时打印名称外，没有其他特殊功能。 |
| `#define DEVICE_REQUEST` | `radimo_request` | 设备的请求函数。它也是强制性的。 |

## 设备驱动程序

| 定义 | 值 | 说明 |
|---|---|---|
| `#define DEVICE_NR (device)` | `(MINOR (device))` | 用于可分区的设备，使其能够使用次设备号进行分区选择。 |
| `#define DEVICE_ON (device)`<br>`#define DEVICE_OFF (device)` | | 电机驱动设备可以将此项设置为与设备启动和停止相关的函数。当请求结束时，块系统将调用`off`函数。`DEVICE_OFF`必须定义为空设备，但`DEVICE_ON`可以省略。 |
| `#define DEVICE_NO_RANDOM` | | 如果定义，该设备将不会为系统熵提供贡献。这与中断处理程序中的`SA_SAMPLE_RANDOM`类似。 |

定义上述内容后，即可包含`linux/blk.h`。

## 大小问题

块设备与两个扇区大小相关：硬件扇区大小和软件扇区大小。前者数据在设备控制的物理介质上的排列方式，而后者是设备内部的排列。目前大多数设备的硬件扇区大小为`512`字节，尽管存在像`MO`硬盘这样的异类，它们通常使用`2,048`字节的扇区。

这些大小在初始化时通过数字索引的全局数组设置。

```c
#define RADIMO_HARDS_SIZE 512
#define RADIMO_BLOCK_SIZE 1024

static int radimo_hard = RADIMO_HARDS_SIZE;
static int radimo_soft = RADIMO_BLOCK_SIZE;
...
```

我们顺应潮流使用`512`字节的硬件扇区大小。这并不重要，因为`radimo`在内部的缓冲区中存储数据。软件块大小可以是任何值，但有几个限制：它必须大于或等于硬件扇区大小、是硬件扇区大小的倍数，并且小于页面（`PAGE`）。如果你忘记设置其中任何一个，硬件扇区大小默认为`512`，块大小默认为`1024`。

除了扇区大小，设备的总大小也存储在全局数组中。参数以千字节为单位给出，内核会自动返回`-ENOSPC`（设备无空间）。

```c
blk_size[RADIMO_MAJOR] = &radimo_size;
```

如果内核有多个虚拟设备（例如通过次设备号索引），`radimo_size`和其他变量可以是一个数组，然后通过`[MAJOR]`索引。各种与块相关的全局结构的实际定义位于`drivers/block/11_rw_blk.c`中，其中也包含关于它们的注释。

## 注册块设备

一旦完成设备定义，就会设置`file_operations`结构体。自内核`2.3.26`以来，块设备使用的设置方法与字符设备不同，因此情况变得稍微复杂了一些。引入`block_device_operations`结构体是为了简化某些内核内部实现，并让块设备编写者更容易跟踪它们。许多开发者对块层仍感到不满，预计在未来的发布中会有更多更改。为了实现最大的可移植性，我们在这里展示不同的版本以及如何在编译时测试内核版本。在本章的剩余部分，我们将关注`2.4`内核系列中使用的方法。

> 如果你需要旧版本内核的参考，可能可以在当地图书馆找到这本书的旧版本，但我们强烈建议你直接升级内核。

```c
#if LINUX_VERSION_CODE < 0x20326
/* 如果内核版本小于 2.3.26，则使用此项 */
static struct file_operations radimo_fops = (
    read:
        block_read,       /* 通用块读 */
    write:
        block_write,      /* 通用块写 */
    ioctl:
        radimo_ioctl,
    open:
        radimo_open,
    release:
        radimo_release,
    revalidate:
        radimo
);
#else
/* 在较新的内核中使用此 */
static struct block_device_operations radimo_fops = {
```
