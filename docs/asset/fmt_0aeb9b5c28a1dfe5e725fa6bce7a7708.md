
## 2.6 内核中相关的支撑功能是对`软锁死`（soft lockups）的感知，即调度停止发生超过 10 秒的情况。内核线程 `watchdog/N`（其中 `N` 为 CPU 编号）每秒都会更新一个每 CPU 时间戳。如果线程超过 10 秒未更新该时间戳，则被认为系统已锁死。在第21章“调试设备驱动程序”中的“`Kdumpt`”部分调试内核崩溃时，软锁死检测（在 `kernel/softlockup.c` 中实现）将为我们提供帮助。

内核中还有其他几个 misc 驱动程序。Qtronix 红外键盘驱动程序 `drivers/char/qtronix.c` 是另一个具有 misc 形式的字符驱动程序示例。在 `drivers/char/` 目录中对 `misc_register()` 执行 grep 操作，可以找出内核中存在的其他 misc 设备驱动程序。

## 字符设备注意事项

驱动方法以及由此用户应用程序发出的相关系统调用可能会失败或部分成功。你的应用程序必须对此进行考虑，以避免令人不快的意外。让我们看看一些常见的陷阱：

- `open()` 调用可能因多种原因失败。某些字符驱动程序仅支持单个用户同时使用，因此如果应用程序尝试打开已在使用中的设备，它们将以 `-EBUSY` 失败。如果打印机缺纸，当你发出设备 `open()` 时，驱动程序将以 `-ENOSPC` 失败。
- 成功的 `read()` 或 `write()` 可以返回介于 1 字节和请求的字节数之间的任意值，因此你的应用程序需要足够的逻辑来处理这种情况。
- `select()` 调用即使只有一个字节的数据准备好被读取或写入也会返回成功。
- 某些字符设备，如鼠标和触摸屏，仅支持输入，因此它们的驱动程序不支持写方法族（`write()`/`aio_write()`/`fsync()`）。其他设备，如打印机，仅支持输出，它们的驱动程序不支持读方法族（`read()`/`aio_read()`）。此外，许多字符驱动程序的方法是可选的，因此并非所有驱动程序都具有所有方法。当方法缺失时，相应的系统调用会失败。

## 查看源代码

字符驱动程序并不专属存在于 `drivers/char/` 目录中。以下是一些“超级”字符驱动程序的示例，它们值得特殊处理和目录：

- 串行驱动程序是管理计算机串行端口的字符驱动程序。然而，它们远比简单的字符驱动程序复杂，并单独位于 `drivers/serial/` 目录中。下一章将讨论串行驱动程序。
- 输入驱动程序负责键盘、鼠标和摇杆等设备。它们位于独立的源目录 `drivers/input/` 中，因此拥有单独的一章：第7章。
- 帧缓冲区（`/dev/fb/`）提供对视频内存的访问，就像 `/dev/mem` 导出对系统内存的访问一样。第12章“视频驱动程序”探讨了帧缓冲区驱动程序。
- 某些设备类支持少数拥有字符接口的硬件。例如，SCSI 设备通常是块设备，但 SCSI 磁带是字符设备。
- 某些子系统导出额外的字符接口，向用户空间呈现原始设备模型。MTD 子系统通常用于模拟各种类型闪存上的磁盘，但某些应用程序如果获得底层闪存内存的原始视图可能会更有利。这是通过 MTD 字符驱动程序 `drivers/mtd/mtdchar.c` 实现的，在第17章“存储技术设备”中进行了讨论。
- 某些内核层通过导出合适的字符接口提供钩子，用于实现用户空间设备驱动程序。应用程序可以通过这些接口直接访问设备的内部结构。一个例子是用于实现 SCSI 扫描仪和 CD 驱动器用户空间设备驱动程序的通用 SCSI 驱动程序 `drivers/scsi/sg.c`。另一个例子是 I²C 设备接口，`i2c-dev`。第19章解释了此类字符接口。

同时，在 `drivers/` 目录中运行 `grep -r on register_chrdev`，可以了解字符驱动程序在内核中的普及程度。

表 5.3 总结了本章使用的主要数据结构及其在源树中的定义位置。表 5.4 列出了本章使用的主要内核编程接口及其定义位置。

| | 数据结构 | 位置 | 描述 |
|---|---|---|---|
| | `cdev` | `include/linux/cdev.h` | 内核中字符设备的抽象 |
| | `file_operations` | `include/linux/fs.h` | 字符驱动程序方法 |
| | `dev_t` | `include/linux/types.h` | 设备主次编号 |

## 表 5.4. 内核编程接口总结

| 数据结构 | 位置 | 描述 |
| :--- | :--- | :--- |
| `poll_table` | `include/linux/poll.h` | 由被轮询数据驱动程序拥有的等待队列表 |
| `pardevice` | `include/linux/parport.h` | 并行端口设备的内核抽象 |
| `rtc_class_ops` | `include/linux/rtc.h` | 顶层与底层 RTC 驱动程序之间的通信接口 |
| `miscdevice` | `include/linux/miscdevice.h` | 杂项设备表示 |
| 内核接口 | 位置 | 描述 |
| :--- | :--- | :--- |
| `alloc_chrdev_region()` | `fs/char_dev.c` | 请求动态分配设备主号 |
| `unregister_chrdev_region()` | `fs/char_dev.c` | `alloc_chrdev_region()` 的反向操作 |
| `cdev_init()` | `fs/char_dev.c` | 将字符驱动程序方法与关联的 cdev 连接起来 |
| `cdev_add()` | `fs/char_dev.c` | 将设备号与 cdev 关联 |
| `cdev_del()` | `fs/char_dev.c` | 移除 cdev |
| `container_of()` | `include/linux/kernel.h` | 从结构体成员获取其包含结构体的地址 |
| `copy_from_user()` | `arch/x86/lib/usercopy_32.c` (适用于 i386) | 将数据从用户空间复制到内核空间 |
| `copy_to_user()` | `arch/x86/lib/usercopy_32.c` (适用于 i386) | 将数据从内核空间复制到用户空间 |
| `likely()` | `include/linux/compiler.h` | 告知 GCC 关联条件成功的可能性 |
| `unlikely()` | `include/linux/compiler.h` | 告知 GCC 关联条件求值失败的可能性 |
| `request_region()` | `include/linux/ioport.h`, `kernel/resource.c` | 声明对 I/O 区域的主权 |
| `release_region()` | `include/linux/ioport.h`, `kernel/resource.c` | 放弃对 I/O 区域的主权 |
| `in[b\|w\|l\|sn\|sl]()` | `include/asm-your-arch/io.h` | 用于与 I/O 区域交换数据的函数族 |
| `out[b\|w\|l\|sn\|sl]()` | `include/asm-your-arch/io.h` | 用于与 I/O 区域交换数据的函数族 |
| `poll_wait()` | `include/linux/poll.h` | 将等待队列添加到内核 poll_table |
| `fasync_helper()` | `fs/fcntl.c` | 确保如果驱动程序发出 kill_fasync()，则向拥有者应用程序分发 SIGIO |
| `kill_fasync()` | `fs/fcntl.c` | 向拥有者应用程序分发 SIGIO |
| `parport_register_device()` | `drivers/parport/share.c` | 向 parport 注册并行端口设备 |
| `parport_unregister_device()` | `drivers/parport/share.c` | 注销并行端口设备 |
| `parport_register_driver()` | `drivers/parport/share.c` | 向 parport 注册并行端口驱动程序 |
| `parport_unregister_driver()` | `drivers/parport/share.c` | 注销并行端口驱动程序 |
| `parport_claim_or_block()` | `drivers/parport/share.c` | 声明并行端口 |
| `parport_write_data()` | `include/linux/parport.h` | 向并行端口写入数据 |
| `parport_read_data()` | `include/linux/parport.h` | 从并行端口读取数据 |
| `parport_release()` | `drivers/parport/share.c` | 释放并行端口 |
