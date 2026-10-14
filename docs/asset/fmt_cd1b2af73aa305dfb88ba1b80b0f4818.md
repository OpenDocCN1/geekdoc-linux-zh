
`e100_send_packet()` 将帧放入队列，并配置 DMA 通道开始传输该帧。我们为该设备注册了 Tx 中断处理程序，它将在一个帧的 DMA 传输完成时执行。在 Tx 处理程序中，我们将检查已经处理了多少 DMA 描述符（传输的帧数）。`e100tx_interrupt()` 例程被注册为 Tx 的中断处理程序。我们在第 1037 行确认中断。我们在 1035–1053 行之间迭代，直到满足以下条件之一：

- 我们已到达列表的末尾。在这种情况下，`myFirstTxDesc` 与 `myNextTxDesc` 相同。
- 我们指向了正在被 DMA 引擎处理的 DMA 描述符 `R_DMA_CH0_FIRST`。

在每次迭代中，我们将 `myFirstTxDesc` 指向 Tx 环形缓冲区中的下一个描述符（第 102 行，18.13）。在每次迭代中，我们释放与相关的 `sk_buff`

```c
arch/cris/drivers/ethernet.c
1025 static void
1026 e100tx_interrupt(int irq, void *dev_id, struct *pt_regs * regs)
1027 (
1028     struct network_device *dev = (struct network_device *)dev_id;
1029     unsigned long irq = *R_IRQ_MASK_2;
1030     struct network_local *np = (struct network_local *)dev->priv;
1033     if (irq & IO_STATE(R_IRQ_MASK_2, d_eol)) {
1034         /* Report the frames */
1035     do {
1037         *R_DMA_CH0_FIRST = IO_STATE(R_DMA_CH0_FIRST, cmd, restart);
1038         /* Check the frames */
1039         if (myFirstTxDesc == myNextTxDesc) {
1040             break;
1041         }
1042         /* Free the skb */
1043         dev_free_skb(myFirstTxDesc->skb);
1044         /* Advance the pointer */
1045         myFirstTxDesc = myFirstTxDesc->next;
1046         /* Check the next descriptor */
1047         if (myFirstTxDesc == R_DMA_CH0_FIRST) {
1048             netif_queue(dev);
1049         }
1050     } while (myFirstTxDesc != R_DMA_CH0_FIRST);
1051     }
1052 }
```

`R_DMA_CH0_FIRST` 宏指向环形缓冲区中正在处理的描述符。我们始终知道当前正在处理哪个 DMA 描述符，并且不会释放与该 DMA 描述符及之后描述符相关的 `sk_buf`。我们遍历 Tx DMA 环形缓冲区直到末尾，并检查 DMA 指向的帧是否已经处理（见第 963 行）。如果正在被处理，我们就释放与 DMA 描述符相关的 `sk_buf`。

`myFirstTxDesc` 被赋值指向环形缓冲区中的下一个描述符。

## `arch/cris/drivers/ethernet.c`

---

## 18.7 SUMMARY

每个网络接口由 `struct net_device` 定义。该结构体包含处理硬件的回调函数。当模块安装时，`net_device` 对象在初始化路由中使用设备特定的回调函数和某些参数进行初始化。

在本章中，我们学习了 Rx 和 Tx 缓冲区的设计和工作。DMA 环形缓冲区逻辑实现在支持 DMA 的网卡上。我们配置它以找到环形缓冲区中的第一个 DMA 描述符。

![](img/b3f231108facab5be0138b2cfd3f681a_737_0.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_1.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_2.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_3.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_4.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_5.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_6.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_7.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_8.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_9.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_10.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_11.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_12.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_13.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_14.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_15.png)

![](img/b3f231108facab5be0138b2cfd3f681a_737_16.png)

**图 18.16. 生成 Tx 中断且 Tx 形缓冲区中的第一个数据包被释放。**

handler。这节省了我们大量的 CPU 周期。在传输时，我们不需要将帧拷贝到设备队列中。对于支持 DMA 的网卡，传输被简化了并再次为我们节省了 CPU 周期。我们将网络缓冲区的地址程序写入 NIC DMA，其余部分由 DMA 引擎本身处理。

# ikcd 与调试 TCP/IP 栈

有不同的调试器可用于调试 Linux 内核，例如 `kdb`、`gdb`、`ikcd` 等。`ikcd` 是一个 Linux 崩溃转储分析器。该工具可以生成内核崩溃转储并将其保存到指定位置，崩溃转储可用于分析内核崩溃的原因。在对运行中的系统进行单步调试方面，我们做不了什么，对此可以使用 `kdb` 或 `gdb`。`ikcd` 可用于运行内核内存以分析数据结构。

在本章中试图让读者熟悉 `ikcd` 以及它如何通过查看内核数据结构来调试 TCP/IP 栈。我们通过一些小例子来关联 TCP 连接、添加新路由（QoS），并尝试通过查看数据结构来观察变化是如何发生的。由于资源和时间限制，无法演示相关的任务和工具。但人们可以获得关于 TCP/IP 栈的各个方面的想法。

认为最好的调试方法是构建一个内核模块来记录给定连接的接收和发送数据包的统计信息，记录特定的 TCP 状态机变量如拥塞窗口、慢启动阈值、接收和发送缓冲区、时间戳等，以便在连接结束时更容易测试和分析 TCP/IP 协议的行为。

TCP/IP 架构、设计与实现（Linux 版）。作者 S. Seth 和 M. Venkates

Copyright © 2008 IEEE Computer Society

723

我们在当前的讨论中不讨论 `ikcd` 的配置和功能，但将讨论与主题相关的内容。这将深入内核数据结构。剩下的留给读者实践和想象。

## 19.1 ikcd 源码与补丁

我们可以从 `sourceforge.net` 获取 `ikcd` 源码。`ikcd` 是构建 `ikcd` 时生成的内核数据结构数据库。`ikcd` 的路径和 `system map` 文件是 `lcrash` 的参数。以下命令可以启动内核 dump 中的 `lcrash` 程序：

```
lcrash core-file system.map
```

也可以通过运行以下命令在运行系统上使用 `lcrash`：

```
lcrash /dev/mem system.map
```

默认生成的 `ikcd` 可能不包含所有内核数据结构的存位。SG 开发了一个工具来生成所有内核数据类型的存位。我们需要以调试模式构建内核并运行 `dwarfextract` 二进制以以下方式构建 `ikcd` 文件：

```
dwarfextract -p vmlinux ikcd
```
