
# Section 6: Paragraph after Code 1

*Listing 10.5* enforces a write barrier by calling `wmb()` to prevent the CPU from reordering the `outl()` before populating the DMA descriptor. On an x86 processor, `wmb()` reduces to a NOP because Intel CPUs enforce writes in program order. When writing the DMA descriptor address to the card and when populating the buffer’s bus address inside the DMA descriptor, the driver converts the native byte order to PCI little-endian format using `cpu_to_le32()`. On Intel CPUs, this again has no effect because both PCI and Intel processors communicate in little-endian. On several other architectures, for example, an ARM9 CPU running in the big-endian mode, both `wmb()` and `cpu_to_le32()` assume significance.

*Translation*: 列表 10.5 通过调用 `wmb()` 强制实施写屏障，以防止 CPU 在填充 DMA 描述符之前重新排序 `outl()`。在 x86 处理器上，`wmb()` 简化为 NOP，因为 Intel CPU 强制执行程序顺序的写入。当将 DMA 描述符地址写入卡片以及在 DMA 描述符内填充缓冲区的总线地址时，驱动程序使用 `cpu_to_le32()` 将本地字节序转换为 PCI 小端格式。在 Intel CPU 上，这再次没有影响，因为 PCI 和 Intel 处理器都使用小端通信。在几种其他体系结构上，例如以字节序模式运行的 ARM9 CPU，`wmb()` 和 `cpu_to_le32()` 都具有重要意义。

*Correction*: "big-endian mode" -> 大端模式.

# Section 7: Paragraph before Code 2

*Now that you have the descriptors and buffers mapped and ready to go, it’s time to look at how data is exchanged between the system and the CardBus device, as shown in Listing 10.6. We won’t dwell on the network interfaces and networking data structures because Chapter 15 is devoted to doing that.*

*Translation*: 现在你已经映射并准备好描述符和缓冲区，是时候看看系统和 CardBus 设备之间如何交换数据了，如列表 10.6 所示。我们不会深入研究网络接口和网络数据结构，因为第 15 章专门用于介绍这些内容。

# Section 8: Code Block 2 (Listing 10.6)

### Listing 10.6. Receiving and Transmitting Data

*Translation*: ### 列表 10.6. 接收和发送数据
