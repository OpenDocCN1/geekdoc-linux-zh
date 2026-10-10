...[/content]`.

Let's break down the translation section by section:

**Section 1: Numbered List (2-4)**
*   **2. The PCI hotplug layer detects card insertion and gleans the vendor ID and device ID of each device function from the card's PCI configuration space.**
    *   *Translation*: 2. PCI 热插拔层检测到卡片插入，并从卡片的 PCI 配置空间中获取每个设备功能的供应商 ID 和设备 ID。
*   **3. Because the IDs match with those registered by the card's Ethernet and serial drivers, the corresponding probe() methods are invoked. This results in the invocation of net_driver_probe() and modem_driver_probe() described respectively in Listing 10.3 and Listing 10.4.**
    *   *Translation*: 3. 由于这些 ID 与卡片的以太网和串行驱动器注册的 ID 匹配，因此调用了相应的 probe() 方法。这导致了分别在列表 10.3 和列表 10.4 中描述的 net_driver_probe() 和 modem_driver_probe() 的调用。
*   **4. The probe() methods configure the Ethernet and modem portions of the PCI driver with resource information. This leads to the allocation of a networking interface (ethX) and a serial port (ttySX) to the card. From this point on, application data flows over these interfaces.**
    *   *Translation*: 4. probe() 方法使用资源信息配置 PCI 驱动器的以太网和调制解调器部分。这导致为卡片分配了一个网络接口 (ethX) 和一个串行端口 (ttySX)。从这一点开始，应用程序数据通过这些接口流动。

**Section 2: Heading and Paragraphs**
*   **## Data Transfer**
    *   *Translation*: ## 数据传输
*   **The network function belonging to the sample CardBus device uses the following strategy for data transfer: The card expects the device driver to supply it with an array of two receive DMA descriptors and an array of two transmit DMA descriptors. Each DMA descriptor contains the address of an associated data buffer, its length, and a control word. You can use the control word to tell the device whether the descriptor contains valid data. For a transmit descriptor, you may also program it to request an interrupt after data transmission. The card looks for a valid descriptor and DMA's data to/from the associated data buffer. To suit this elementary scheme, the example driver uses only the coherent DMA interface. The driver coherently allocates a large buffer that holds the descriptors and their associated data buffers. The receive and transmit buffers are 1536 bytes long to match the maximum transmission unit (MTU) of Ethernet frames. The descriptors and buffers are pictorially shown in Figure 10.2. The top 24 bytes of each array in the figure hold two 12-byte DMA descriptors, and the rest of the memory is occupied by two 1536-byte DMA buffers. The 12-byte descriptor layout shown in the figure is assumed to match the format specified in the card's data sheet.**
    *   *Translation*: 属于示例 CardBus 设备的网络功能使用以下策略进行数据传输：卡片期望设备驱动程序为其提供两个接收 DMA 描述符数组和两个发送 DMA 描述符数组。每个 DMA 描述符包含关联数据缓冲区的地址、其长度和一个控制字。你可以使用控制字来告诉设备描述符是否包含有效数据。对于发送描述符，你还可以将其编程为在数据传输后请求中断。卡片寻找有效的描述符，并将数据 DMA 到/从关联的数据缓冲区。为了适应这种基本方案，示例驱动程序仅使用一致性 DMA 接口。驱动程序一致性分配一个大缓冲区，用于容纳描述符及其关联的数据缓冲区。接收和发送缓冲区的长度为 1536 字节，以匹配以太网帧的最大传输单元 (MTU)。描述符和缓冲区在图 10.2 中以图形方式显示。图中每个数组的前 24 字节容纳两个 12 字节的 DMA 描述符，其余内存由两个 1536 字节的 DMA 缓冲区占用。假设图中所示的 12 字节描述符布局与卡片数据表中指定的格式相匹配。

**Section 3: Images**
*   `![](img/07cc6f9c8c74622020874f66bfb53dc4_279_0.png)` -> Keep as is.
*   `![](img/07cc6f9c8c74622020874f66bfb53dc4_280_0.png)` -> Keep as is.

**Section 4: Table**
*   **Table 10.3 shows the register layout of the card's network function.**
    *   *Translation*: 表 10.3 显示了卡片网络功能的寄存器布局。
*   **| Register Name | Description | Offset into I/O Space |**
    *   *Translation*: | 寄存器名称 | 描述 | I/O 空间中的偏移量 |
*   **|---|---|---|** -> Keep
*   **| DMA_RX_REGISTER | Holds the bus address of the receive DMA descriptor array (dma_bus_rx) | 0x0 |**
    *   *Translation*: | DMA_RX_REGISTER | 保存接收 DMA 描述符数组的总线地址 (dma_bus_rx) | 0x0 |
*   **| DMA_TX_REGISTER | Holds the bus address of the transmit DMA descriptor array (dma_bus_tx) | 0x4 |**
    *   *Translation*: | DMA_TX_REGISTER | 保存发送 DMA 描述符数组的总线地址 (dma_bus_tx) | 0x4 |
*   **| CONTROL_REGISTER | Control word that commands the card to initiate DMA, stop DMA, and so on | 0x8 |**
    *   *Translation*: | CONTROL_REGISTER | 命令卡片启动 DMA、停止 DMA 等的控制字 | 0x8 |

**Section 5: Code Block 1 (Listing 10.5)**
*   **### Listing 10.5. Setting Up DMA Descriptors and Buffers**
    *   *Translation*: ### 列表 10.5. 设置 DMA 描述符和缓冲区
*   **```c ... ```** -> Do not translate code.

**Section 6: Paragraph after Code 1**
*   **Listing 10.5 enforces a write barrier by calling `wmb()` to prevent the CPU from reordering the `outl()` before populating the DMA descriptor. On an x86 processor, `wmb()` reduces to a NOP because Intel CPUs enforce writes in program order. When writing the DMA descriptor address to the card and when populating the buffer’s bus address inside the DMA descriptor, the driver converts the native byte order to PCI little-endian format using `cpu_to_le32()`. On Intel CPUs, this again has no effect because both PCI and Intel processors communicate in little-endian. On several other architectures, for example, an ARM9 CPU running in the big-endian mode, both `wmb()` and `cpu_to_le32()` assume significance.**
    *   *Translation*: 列表 10.5 通过调用 `wmb()` 强制实施写屏障，以防止 CPU 在填充 DMA 描述符之前重新排序 `outl()`。在 x86 处理器上，`wmb()` 简化为 NOP，因为 Intel CPU 强制执行程序顺序的写入。当将 DMA 描述符地址写入卡片以及在 DMA 描述符内填充缓冲区的总线地址时，驱动程序使用 `cpu_to_le32()` 将本地字节序转换为 PCI 小端格式。在 Intel CPU 上，这再次没有影响，因为 PCI 和 Intel 处理器都使用小端通信。在几种其他体系结构上，例如以字节序模式运行的 ARM9 CPU，`wmb()` 和 `cpu_to_le32()` 都具有重要意义。
    *   *Correction*: "big-endian mode" -> 大端模式.

**Section 7: Paragraph before Code 2**
*   **Now that you have the descriptors and buffers mapped and ready to go, it’s time to look at how data is exchanged between the system and the CardBus device, as shown in Listing 10.6. We won’t dwell on the network interfaces and networking data structures because Chapter 15 is devoted to doing that.**
    *   *Translation*: 现在你已经映射并准备好描述符和缓冲区，是时候看看系统和 CardBus 设备之间如何交换数据了，如列表 10.6 所示。我们不会深入研究网络接口和网络数据结构，因为第 15 章专门用于介绍这些内容。

**Section 8: Code Block 2 (Listing 10.6)**
*   **### Listing 10.6. Receiving and Transmitting Data**
    *   *Translation*: ### 列表 10.6. 接收和发送数据
*   **```c ... ```** -> Do not translate code.

**Section 9: Final Paragraph**
*   **When the CardBus device receives an Ethernet packet, it DMAs it to a free RX descriptor and interrupts the CPU. The interrupt handler mydevice_interrupt() collects the packet from the receive DMA buffer, copies it to a networking data structure (sk_buff), and passes it on to higher protocol layers.**
    *   *Translation*: 当 CardBus 设备接收到一个以太网数据包时，它将其 DMA 到一个空闲的 RX 描述符并中断 CPU。中断处理程序 mydevice_interrupt() 从接收 DMA 缓冲区收集数据包，将其复制到网络数据结构 (sk_buff)，并将其传递给更高的协议层。

Refining terms:
*   "Listing" -> "列表" or "清单"? In technical docs, "List" is often used. "Listing 10.3" is usually "List 10.3" or "Listing 10.3". I will use "列表" as it is common in Chinese translations of technical manuals (e.g., O'Reilly books).
*   "probe()" -> keep as is (function name).
*   "CardBus" -> keep as is.
*   "DMA" -> keep as is.
*   "sk_buff" -> keep as is.

Let's double check the code block contents. The instruction says "Inline code (`code`) and code blocks do not need translation." This applies to the content inside the triple backticks. I will leave the C code completely untouched.

One detail: `Listing 10.5` in the text refers to the code block. In Chinese context, "列表" is fine.

Let's assemble the final output.

[content]
2. PCI 热插拔层检测到卡片插入，并从卡片的 PCI 配置空间中获取每个设备功能的供应商 ID 和设备 ID。

3. 由于这些 ID 与卡片的以太网和串行驱动器注册的 ID 匹配，因此调用了相应的 probe() 方法。这导致了分别在列表 10.3 和列表 10.4 中描述的 net_driver_probe() 和 modem_driver_probe() 的调用。

4. probe() 方法使用资源信息配置 PCI 驱动器的以太网和调制解调器部分。这导致为卡片分配了一个网络接口 (ethX) 和一个串行端口 (ttySX)。从这一点开始，应用程序数据通过这些接口流动。

## 数据传输

属于示例 CardBus 设备的网络功能使用以下策略进行数据传输：卡片期望设备驱动程序为其提供两个接收 DMA 描述符数组和两个发送 DMA 描述符数组。每个 DMA 描述符包含关联数据缓冲区的地址、其长度和一个控制字。你可以使用控制字来告诉设备描述符是否包含有效数据。对于发送描述符，你还可以将其编程为在数据传输后请求中断。卡片寻找有效的描述符，并将数据 DMA 到/从关联的数据缓冲区。为了适应这种基本方案，示例驱动程序仅使用一致性 DMA 接口。驱动程序一致性分配一个大缓冲区，用于容纳描述符及其关联的数据缓冲区。接收和发送缓冲区的长度为 1536 字节，以匹配以太网帧的最大传输单元 (MTU)。描述符和缓冲区在图 10.2 中以图形方式显示。图中每个数组的前 24 字节容纳两个 12 字节的 DMA 描述符，其余内存由两个 1536 字节的 DMA 缓冲区占用。假设图中所示的 12 字节描述符布局与卡片数据表中指定的格式相匹配。

![](img/07cc6f9c8c74622020874f66bfb53dc4_279_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_280_0.png)

表 10.3 显示了卡片网络功能的寄存器布局。

| 寄存器名称 | 描述 | I/O 空间中的偏移量 |
|---|---|---|
| DMA_RX_REGISTER | 保存接收 DMA 描述符数组的总线地址 (dma_bus_rx) | 0x0 |
| DMA_TX_REGISTER | 保存发送 DMA 描述符数组的总线地址 (dma_bus_tx) | 0x4 |
| CONTROL_REGISTER | 命令卡片启动 DMA、停止 DMA 等的控制字 | 0x8 |

### 列表 10.5. 设置 DMA 描述符和缓冲区

```c
/* Device-specific data structure for the Ethernet Function */
struct device_data {
    struct pci_dev *pdev;    /* The PCI Device structure */
    struct net_device *ndev;  /* The Net Device structure */
    void *dma_buffer_rx;      /* Kernel virtual address of the
                              * receive descriptor */
    dma_addr_t dma_bus_rx;		/* Bus address of the receive
descriptor */
    void *dma_buffer_tx;		/* Kernel virtual address of the
transmit descriptor */
    dma_addr_t dma_bus_tx;		/* Bus address of the transmit
descriptor */
    /* ... */
    spinlock_t device_lock;	/* Serialize */
} *mydev_data;

/* On-card registers related to DMA */
#define DMA_RX_REGISTER_OFFSET		0x0	/* Offset of the register
holding the bus address
of the RX descriptor */

#define DMA_TX_REGISTER_OFFSET		0x4	/* Offset of the register
holding the bus address
of the TX descriptor */

#define CONTROL_REGISTER			0x8	/* Offset of the control
register */

/* Control Register Defines */
#define INITIATE_XMIT			0x1

/* Descriptor control word definitions */
#define FREE_FLAG			0x1	/* Free Descriptor */
#define INTERRUPT_FLAG		0x2	/* Assert interrupt after DMA */

/* Invoked from Listing 10.3 */
static void
dma_descriptor_setup(struct pci_dev *pdev)
{
    /* Allocate receive DMA descriptors and buffers */
    mydev_data->dma_buffer_rx =
        pci_alloc_consistent(pdev, 3096, &mydev_data->dma_bus_rx);

    /* Fill the two receive descriptors as shown in Figure 10.2 */
    /* RX descriptor 1 */
    mydev_data->dma_buffer_rx[0] = cpu_to_le32((unsigned long)
        (mydev_data->dma_bus_rx + 24));	/* Buffer address */
    mydev_data->dma_buffer_rx[1] = 1536;	/* Buffer length */
    mydev_data->dma_buffer_rx[2] = FREE_FLAG;	/* Descriptor is free */

    /* RX descriptor 2 */
    mydev_data->dma_buffer_rx[3] = cpu_to_le32((unsigned long)
        (mydev_data->dma_bus_rx + 1560));	/* Buffer address */
    mydev_data->dma_buffer_rx[4] = 1536;	/* Buffer length */
    mydev_data->dma_buffer_rx[5] = FREE_FLAG;	/* Descriptor is free */

    wmb();	/* Write Memory Barrier */

    /* Write the address of the receive descriptor to the appropriate
register in the card. The I/O base address, ioaddr, was populated
in Listing 10.3 */
    outl(cpu_to_le32((unsigned long)mydev_data->dma_bus_rx),
        ioaddr + DMA_RX_REGISTER_OFFSET);
    /* Allocate transmit DMA descriptors and buffers */
    mydev_data->dma_buffer_tx =
        pci_alloc_consistent(pdev, 3096, &mydev_data->dma_bus_tx);

    /* Fill the two transmit descriptors as shown in Figure 10.2 */
    /* TX descriptor 1 */
    mydev_data->dma_buffer_tx[0] = cpu_to_le32((unsigned long)
        (mydev_data->dma_bus_tx + 24));  /* Buffer address */
    mydev_data->dma_buffer_tx[1] = 1536;        /* Buffer length */
    /* Valid descriptor. Generate an interrupt
       after completing the DMA */
    mydev_data->dma_buffer_tx[2] = (FREE_FLAG | INTERRUPT_FLAG);
    /* TX descriptor 2 */
    mydev_data->dma_buffer_tx[3] = cpu_to_le32((unsigned long)
        (mydev_data->dma_bus_tx + 1560)); /* Buffer address */
    mydev_data->dma_buffer_tx[4] = 1536;        /* Buffer length */
    mydev_data->dma_buffer_tx[5] = (FREE_FLAG | INTERRUPT_FLAG);

    wmb(); /* Write Memory Barrier */
    /* Write the address of the transmit descriptor to the appropriate
       register in the card. The I/O base, ioaddr, was populated in
       Listing 10.3 */
    outl(cpu_to_le32((unsigned long)mydev_data->dma_bus_tx),
         ioaddr + DMA_TX_REGISTER_OFFSET);
}

/* Invoked from Listing 10.3 */
static void
dma_descriptor_release(struct pci_dev *pdev)
{
    pci_free_consistent(pdev, 3096, mydev_data->dma_bus_tx);
    pci_free_consistent(pdev, 3096, mydev_data->dma_bus_rx);
}
```

列表 10.5 通过调用 `wmb()` 强制实施写屏障，以防止 CPU 在填充 DMA 描述符之前重新排序 `outl()`。在 x86 处理器上，`wmb()` 简化为 NOP，因为 Intel CPU 强制执行程序顺序的写入。当将 DMA 描述符地址写入卡片以及在 DMA 描述符内填充缓冲区的总线地址时，驱动程序使用 `cpu_to_le32()` 将本地字节序转换为 PCI 小端格式。在 Intel CPU 上，这再次没有影响，因为 PCI 和 Intel 处理器都使用小端通信。在几种其他体系结构上，例如以大端模式运行的 ARM9 CPU，`wmb()` 和 `cpu_to_le32()` 都具有重要意义。

现在你已经映射并准备好描述符和缓冲区，是时候看看系统和 CardBus 设备之间如何交换数据了，如列表 10.6 所示。我们不会深入研究网络接口和网络数据结构，因为第 15 章专门用于介绍这些内容。

### 列表 10.6. 接收和发送数据

```c
/* The interrupt handler */
static irqreturn_t
mydevice_interrupt(int irq, void *dev_id)
{
    struct sk_buff *skb;
    /* ... */
    /* If this is a receive interrupt, collect the packet and pass it
       on to higher layers. Look at the control word in each RX DMA
       descriptor to figure out whether it contains data. Assume for
       convenience that the first RX descriptor was used by the card
       to DMA this received packet */
    packet_size = mydev_data->dma_buffer_rx[1];
    /* In real world drivers, the sk_buff is pre-allocated, stream-
mapped, and supplied to the card after setting the FREE_FLAG
during device open(). The received data is directly
DMA'ed to this sk_buff instead of the memcpy() performed here,
as you will learn in Chapter 15. The card clears the FREE_FLAG
before the DMA */
    skb = dev_alloc_skb(packet_size); /* See Figure 15.2 of Chapter 15 */
    skb->dev = mydev_data->ndev; /* Owner network device */
    memcpy(skb, mydev_data->dma_buffer_rx[24], packet_size);
    /* Pass the received data to higher-layer protocols */
    skb_put(skb, packet_size);
    netif_rx(skb);
    /* ... */
    /* Make the descriptor available to the card again */
    mydev_data->dma_buffer_rx[2] |= FREE_FLAG;
}

/* This function is registered in Listing 10.3 and is called from
the networking layer. More on network device interfaces in
Chapter 15 */
static int
mydevce_xmit(struct sk_buff *skb, struct net_device *dev)
{
    /* Use a valid TX descriptor. Look at Figure 10.2 */
    /* Locking has been omitted for simplicity */
    if (mydev_data->dma_buffer_tx[2] & FREE_FLAG) {
        /* Use first TX descriptor */
        /* In the real world, DMA occurs directly from the sk_buff as
you will learn later on! */
        memcpy(mydev_data->dma_buffer_tx[24], skb->data, skb->len);
        mydev_data->dma_buffer_tx[1] = skb->len;
        mydev_data->dma_buffer_tx[2] &= ~FREE_FLAG;
        mydev_data->dma_buffer_tx[2] |= INTERRUPT_FLAG;
    } else if (mydev_data->dma_buffer_tx[5] & FREE_FLAG) {
        /* Use second TX descriptor */
        memcpy(mydev_data->dma_buffer_tx[1560], skb->data, skb->len);
        mydev_data->dma_buffer_tx[4] = skb->len;
        mydev_data->dma_buffer_tx[5] &= ~FREE_FLAG;
        mydev_data->dma_buffer_tx[5] |= INTERRUPT_FLAG;
    } else {
        return -EIO; /* Signal error to the caller */
    }
    wmb(); /* Don't reorder writes across this barrier */

    /* Ask the card to initiate DMA. ioaddr is defined
in Listing 10.3 */
    outl(INITIATE_XMIT, ioaddr + CONTROL_REGISTER);
}
```

当 CardBus 设备接收到一个以太网数据包时，它将其 DMA 到一个空闲的 RX 描述符并中断 CPU。中断处理程序 mydevice_interrupt() 从接收 DMA 缓冲区收集数据包，将其复制到网络数据结构 (sk_buff)，并将其传递给更高的协议层。
