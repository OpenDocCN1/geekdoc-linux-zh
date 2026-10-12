
当接收到注册了 `SA_SAMPLE_RANDOM` 处理的中断时，`add_interrupt_randomness()` 由中断程序调用。参数 `irq` 是中断号。随机数生成器使用中断之间的时间作为噪声源。注意，并非所有设备都适用于此；如果设备产生确定性的中断（例如定时器中断）或可能被外部攻击者影响（例如网络设备），则不应馈入池。可以接受的设备是硬盘，它以不可预测的速率产生中断。

`randomness()` 使用扫描码（`scancode`）和连续按键之间的时间间隔向填充池（`pool`）提供数据。有趣的是，熵足够智能，能够自动返回（当用户按下键时）同时返回扫描码和时间间隔，因此它们对熵的贡献微乎其微。唯一的参数是所按按键的扫描码。

```
mouse_randomness() 使用鼠标位置作为中断之间的时间间隔来填充池。参数 `mouse_data` 是硬件报告的鼠标位置。
```

所有这些例程都会将数据添加到熵池，计算给定的熵的估计值，并按相应数量增加熵估计值。

所有这些导出函数都使用内部函数 `timer_randomness()` 向填充池提供数据。该函数计算同类型类型连续事件之间的时间间隔，并将延迟添加到填充池中。例如，两个不同中断之间的时间间隔在很大程度上是随机的——尤其是当精确测量时。低位是电信号。在向填充池提供数据后，它会计算数据中存在多少随机性。这是通过首先计算上一次计时的一阶、二阶和三阶差分，以及一阶和二阶差分来实现的。这些差分中最大的值向下取整为 12 位，作为熵估计值。

## 输出接口

内核导出了一个从内核获取随机数据的接口：

```
void get_random_bytes(void *buf, int nbytes)
```

该函数在 `buf` 指向的缓冲区中返回随机数据。无论熵估计值是否为零，函数都会返回。对于内核来说，这并不像用户空间加密应用那样令人。随机数据适用于少数内核任务，特别是网络功能，它被用于为连接中的初始 TCP 序列数种子。

内核代码可以在随机数的帮助下完成以下操作：

```
unsigned long rand;
get_random_bytes(&rand, sizeof(rand));
```

对于用户空间进程，内核提供了两个字符设备：`/dev/random` 和 `/dev/urandom`。前者 `/dev/random` 适用于需要强随机数的情况，例如高安全性加密应用。它只返回最多熵估计值所指示的最大数量的随机数据位。当熵估计值达到零时，`/dev/random` 会阻塞，直到熵估计值足够正值才会返回剩余数据。相反，设备 `/dev/urandom` 不具有此功能，但通常是同样安全的。两个设备都从同一个池返回数字。

读取任何一个文件都是简单的。这里是一个应用程序可以用于提取一个字长度熵的用户空间函数示例：

```
unsigned long get_random(void)
{
    unsigned long seed = 0;
    int fd;
    fd = open("/dev/urandom", O_RDONLY);
    if (fd == -1) {
        perror("open");
        return 0;
    }
    if (read(fd, &seed, sizeof(seed)) < 0) {
        perror("read");
        seed = 0;
    }
    if (close(fd)) {
        perror("close");
    }
    return seed;
}
```

或者，你可以使用 `dd` 程序轻松地将 `$bytes` 字节读入文件 `$file` 中：

```bash
dd if=/dev/urandom of=$file count=1 bs=$bytes
```

## 算法复杂度

在计算机科学及相关领域中，通常将算法的算法复杂度（或可扩展性）表示为一个有意义的值（而不是描述性术语，如增长率）是有用的。表示可扩展性的方法有多种。一种常用技术是研究算法的渐近行为。这是算法随着输入变得极大或趋于无穷大时的行为。渐近行为显示了算法随着输入不断变大，可扩展性如何。研究算法的可扩展性——即随着输入规模的增加其性能如何——使我们能够相对于基准对算法进行建模，并更好地理解其行为。

# 参考文献与阅读列表

这份参考文献按主题分类，包含了一些与本书主题相似或互补的、较为有趣且实用的书籍。

这些书籍在时间的推移中已被证明是非常实用的。其中一些代表了各自领域的“圣经”，而另一些则仅仅在某些方面被认为有趣、富有见地或具有娱乐性。我希望它们也能对你有所帮助。

请注意，补充本书内容的最佳参考或“额外阅读”是内核源码。在 Linux 上工作，我们都天赋获得了对整个现代操作系统源代码的完整且无限制的权限。不要视其理所当然！深入其中吧！

## 操作系统设计书籍

这些书籍涵盖了本科课程中讨论的操作系统设计。它们都涉及了设计功能性操作系统所包含的概念、算法、问题和解决方案。

- *Tanenbaum, Andrew. Operating Systems: Design and Implementation.* Prentice Hall, 1997.* 一本关于 Unix 类系统 `Minix` 设计与实现的极佳入门著作。

- *Tanenbaum, Andrew. Modern Operating Systems.* Prentice Hall, 2001.* 对标准操作系统设计问题进行了强有力的概述，并讨论了当今现代操作系统（如 `Unix` 和 `Windows`）中使用的许多概念。

- *A. Silbersatz, P. Galvin, and G. Gagne. Operating System Concepts.* John Wiley and Sons, 2001.* 因为封面上看似无关的恐龙，这本书也被称为“恐龙书”。一本关于操作系统的极佳介绍。该书频繁修订；其中任何一个版本都可以。

## Unix 内核书籍

这些书籍讨论了 Unix 内核的设计与实现。前三本讨论了特定 Unix 变体，后两本关注所有 Unix 变体共同的问题。

`Bach`, Maurice. The Design of the Unix Operating System. Prentice Hall, 1986. 对 `System V Release 2` 设计的良好讨论。

`M. McCusick`, `K. Bostic`, `M. Karels`, and `J. Quarterman`. The Design and Implementation of the 4.4BSD Operating System. Addison-Wesley, 1996. 系统设计者对 `4.4BSD` 系统设计的良好讨论。

`J. Mauro` and `R. McDougall`. Solaris Internals: Core Kernel Architecture. Prentice Hall, 2000. 对 `Solaris` 内核中核心子系统和算法的有趣讨论。

`Vahali`, Utreh. Unix Internals: The New Frontiers. Prentice Hall, 1995. 一本关于现代 Unix 特性（如线程管理和内核抢占）的卓越著作。

`Schimmutt`, Curt. Unix Systems for Modern Architectures: Symmetric Multiprocessing and Caching for Kernel Programmers. Addison-Wesley, 1994. 一本关于在现代架构上支持现代 Unix 之危险的卓越著作。

## Linux 内核书籍

这些书籍与本书一样讨论了 Linux 内核。

`A. Rubin` and `J. Corbett`. Linux Device Drivers. O'Reilly and Associates, 2001. 关于如何为 `2.4` 内核编写驱动优秀讨论。

`D. Bovet` and `M. Ceati`. Understanding the Linux Kernel. O'Reilly and Associates, 2002. 对 `2.4` Linux 内核内部算法的良好讨论。它聚焦于内核的底层设计。

`D. Moshergian` and `S. Eanian`. IA-64 Linux Kernel: Design and Implementation. Prentice Hall, 2002. 对 `Intel Itanium` 架构及其 Linux `2.4` 内核移植的极佳视角。

## 其他内核书籍

了解你的敌人——竞争对手——永远无害。这些书籍讨论了 Linux 之外的操作系统的设计与实现。让我们看到他们拥有什么，以及出了什么问题。

`M. Kogan` and `H. Deitel`. The Design of OS/2. Addison-Wesley, 1996. 对 `OS/2 2.0` 的有趣视角。
