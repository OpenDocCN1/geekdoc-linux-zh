

**图 5.26** 以太网驱动 1—data: linux/drivers/net/3c501.c。

```c
/*
 * 写入 RX_STATUS 的正常接收模式。我们必须对短包产生中断，
 * 以避免虚假的 rx 锁死。
 */
#define RX_NORM 0xA8      /* 0x66 == 所有地址，xA8 仅发送给我 . */
#define TX_PROM 0x68 /* 年舞会，嗯，混杂模式 . */
#define TX_MULT 0xE8 /* 接收组播包 . */
#define TX_NORM 0xA0      /* 对可能导致芯片挂起的操作产生中断 */
/*
 * TX_STATUS 寄存器。
 */
#define TX_COLLISION 0x02
#define TX_16COLLISIONS 0x04
#define TX_READY 0x08
#define RX_BUNT 0x08
#define RX_MISSED 0x01 /* 错过了一个数据包，由于 3c501 的脑损伤。 */
#define RX_GOOD 0x30      /* 好包 0x20，或简单的溢出 0x10。 */
```

## 3c501 初始化

在这里我们看到了设备的初始化。为了与操作系统接口，需要进行一些特定的操作，以确保数据可用并启动网卡驱动程序。我们在这里从网卡获取站地址或 MAC 地址。

**图 5.27** 以太网驱动 2—init a: linux/drivers/net/3c501.c。

```c
/*
 * 为此驱动程序的独占使用保留 I/O 资源
 */
if (!request_region(ioaddr, EL1_IO_EXTENT, dev->name))
	return -ENODEV;
```

## 130 TCP/IP 和 Linux 协议实现

```c
280
281  /*
282      * 从特殊端口读取站地址的 PROM 数据。
283   */
284
285  for (i = 0; i < 6; i++)
286  {
287      outw(i, ioaddr, EL1_DATAPTR);
288      station_addr[i] = inb(ioaddr + EL1_SAPROM);
289
290  }
291  /*
292   * 检查 S.A. 的前三个字节是否为 3Com 的前缀，或
293   为 Sagar NP943 的前缀。
294   */
295
296  if (station_addr[0] == 0x02 && station_addr[1] == 0x60
297      && station_addr[2] == 0x8c)
298  {
299      name = "3C501";
300  } else if (station_addr[0] == 0x00 && station_addr[1] == 0x80
301      && station_addr[2] == 0xCB)
302  {
303      name = "NP943";
304  }
305  else {
306      release_region(ioaddr, EL1_IO_EXTENT);
307      return -ENODEV;
308  }
```

在这里我们要找到设备所所在的 IRQ。

**图 5.28** 以太网驱动 2—init b: linux/drivers/net/3c501.c。

```c
309  /*
310   * 我们通过关闭中断线并让其浮空置来实现自动 IRQ。
311     高。
312   */
313
314  if (dev->irq < 2)
315  {
316      autoirq_setup(2);
317      inb(RX_STATUS);      /* 清除挂起的中断。 */
318      inb(TX_STATUS);
319      outb(AX_LOOP + 1, AX_CMD);
320
321      outb(0x00, AX_CMD);
322
323      autoirq = autoirq_report(1);
324
325      if (autoirq == 0)
326      {
```

## 协议实现框架 13

```c
327      printk("%s probe at %x failed to detect IRQ line.\n",
328              name, ioaddr);
329      release_region(ioaddr, EL1_IO_EXTENT);
330      return -EAGAIN
331  
332  }
333  
334  outb(AX_RESET+AX_LOOP, AX_CMD);    /* 回环模式。 */
335      dev->base_addr = ioaddr;
336      memcpy(dev->dev_addr, station_addr, ETH_ALEN);
337
338  if (dev->mem_start & 0xf)
339      el_debug = dev->mem_start & 0x7;
340      if (autoirq)
341          dev->irq = autoirq;
342
343  printk(KERN_INFO: "%s Ether at %lx, using %x.\n", dev->name,
344              base_addr,
345              autoirq ? " ":" dev->irq);
```

如果目前一切顺利，我们需要为设备分配空间。

**图 5.29** 以太网驱动 2–init c: linux/drivers/net/3c501.c。

```c
346 #ifndef CONFIG_IP_MULTAST
347 printk(KERN_WARNING: 不建议在组播内核中使用 3c501
348         n");
349 #endif
350 if (el_debug)
351     printk("%s", version);
352
353  /*
354   * 初始化设备结构。
355   */
356  dev->priv = kmalloc(sizeof(struct net_local), GFP_KERNEL);
357 if (dev->priv == NULL) {
358     release_region(ioaddr, EL1_IO_EXTENT);
359     return -ENOMEM
360 }
361  memset(dev->priv, 0, sizeof(struct net_local));
```

这部分填充了特定驱动的设备函数指针。如果一切顺利，将执行通用初始化。

## 132 TCP/IP 和 Linux 协议实现

**图 5.30** 以太网驱动 2—init d: linux/drivers/net/3c501.c。

```c
364 lp=dev->priv;
365 spin_lock_init(&lp->lock);
366
367  /*
368   * 设备结构中特定于驱动条目。
369   */
370 dev->open = &el_open;
371 dev->hard_start_xmit = &el_start_xmit;
372 dev->tx_timeout = &el_timeout;
373 dev->watchdog_time = HZ;
374 dev->stop = &el_close;
375 dev->get_stats = &el_get_stats;
376 dev->set_multicast_list = &set_multicast_list;
377
378  /*
379   * 设置通用属性
380   */
381 ether_setup(dev);
382 return 0;
383 }
```

## 3c501 开始传输

DMA 网络设备有很多工作（即它们可以与处理器并行处理工作）。但是，它们在某些阶段可能会很慢，因此常见的做法是将工作分开，并尽可能减少（短）关键区域。

**图 5.31** 以太网驱动 2—txstart a: linux/drivers/net/3c501.c。

```c
451 /*
452  * el_start_xmit;
453  * @dev: 等队发送的数据包
454  * @dev: 我们想要发送的 3c501 网卡
455  */
456  * 尝试向 3c501 网卡发送数据包。这里有一些有趣的
457  * 捕获，因为 3c501 是非常老旧的因此
```

## 133 协议实现框架

```c
+ * 一个愚蠢的技术。
* 如果我们在另一个 CPU 上处理中断，它就无法加载数据包，
* 因为我们仍在尝试检索最后一个 RX 数据缓冲区。
* 当传输超时时，将网卡置于控制模式并
* 重新开始。这种情况发生的频率足以记录。
* 我们在将数据包加载到板卡时避免持有自旋锁。
* 设备非常慢，DMA 模式更慢。如果在向控制器加载 1500 字节时
* 持有锁，将会丢失大量的
* 字符。这要求我们进行额外的锁定，但我们
* 没有真正的选择。
```

新的几段代码提取显示了传输启动代码的延续。本质（如注释所示），我们告诉网卡有数据准备好发送，以及在哪里，然后告诉它离开并发送，并在我们需要时中断我们。

**图 5.32** 以太网驱动 2-tstart: linux/drivers/net/3c501.c。

```c
static int el_start_xmit(struct sk_buff *skb, struct net_device *dev)
{
    struct net_local *lp = (struct net_local *)dev->priv;
    int ioaddr = dev->base_addr;
    unsigned long flags;

    /*
     * 在我们切换 txing 和切换模式之间避免传入中断
     * 因为驱动程序假设 txing 是网卡可靠的指标
     */

    spin_lock_irqsave(lp->lock, flags);
    /*
     * 避免基于计时器的重传冲突。
     */

    netif_stop_queue(dev);
```

**图 5.33** 以太网驱动 2—txstart b: linux/drivers/net/3c501.c。

```c
do
{
    int gp_start = 0x800 - (ETH_ZLEN < skb->len : ETH_ZLEN);
    unsigned char *buf = skb->data;
```

TCP/IP 和 Linux 协议实现

```c
498  lp->tx_pkt_start = gp_start;
499  lp->collisions = 0;
500
501  lp->stats.tx_bytes += skb->len;
502
503
504  /*
505   * 状态清除模式 [理论上]
506   * 网卡上不再有挂起的中断。
507   */
508
509  outb_p(AX_SYS, AX_CMD);
510  inb_p(RX_STATUS);
511  inb_p(TX_STATUS);
512
513  lp->loading = i;
514  lp->txring = 1;
515
516  /*
517   * 当我们愉快地向板卡加载字节时重新开启中断
518   * 
519   */
520  spin_unlock_irqrestore(&lp->lock, flags);
521
522  outw(000, AX_BUF_CLR);      /* 将数据区域置为 0。 */
523  outw(gp_start, GP_LOW);      /* 数据包将加载到缓冲区起始
524  outsb(DATAPORT,skb->len);   /* 加载缓冲区（每个字节都会增加
525  指针） */
526  outw(gp_start, GP_LOW);      /* 板卡复用同一个寄存器 */
```

**图 5.34** 以太网驱动 2txstart b: linux/drivers/net/3c501.c。

```c
if (lp->loading != 2)
{
  outb(AX_XMIT, AX_CMD);      /* 触发 ... 触发下一个。 */
  lp->loading=0;
  dev->trans_start = jiffies;
  if (el_debug > 2)
    printk(" queued xmit.\n");
  dev->free_skb (skb);
  return 0;
}
/* 尽管我们尽力，在加载时出现了一个接收 */
if (el_debug>2)
  printk("%s: 在此加载期间发生抖动.\n", dev->name);
  spin_lock_irqsave(&lp->lock, flags);
while(i);
```

