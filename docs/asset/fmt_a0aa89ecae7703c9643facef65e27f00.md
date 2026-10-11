
| 6 | Input Data (--) |

| 7 | Reserved for Telephone use |

| 8 | Reserved for Telephone use |

If you want to make a cable, the following should spell it out for you: Differential signals must be on the same twisted pair to get the required minimal impedance/loss of a UTP cable. If you look at the above table, you will see that `1+2` and `3+6` are the two sets of different signal. Not `1+3` and `2+6` at 10MHz, with short lengths, you *may* get away with such errors, if it is only over a short length. Don't even think about it at 100MHz.

For a normal patch cord, with ends `A` and `B`, you want straight pin-to-pin mapping, with input and output each a pair of twisted wires (for impedance). This means `1A` goes to `1B`, `2A` goes to `2B`, `3A` goes to `3B` and `6A` goes to `6B`. The wires joining `1A–1B` and `2A–2B` must be a twisted pair. Also the wires joining `3A–3B` and `6A–6B` must be another twisted pair.

If you don't have a cable, and want to make a `null cable`, what you want to do is make the input of `A` the output of `B` and the output of `A` be the input of `B`, without changing the polarity. This means `1A` to `3B` (out+ A in+ B) and `2A` to `6B` (out– A in– B). These two wires are twisted pair. They carry what/plug `A` considers output, and what is seen as input/plug `B`. Then connect `3A` to `1B` (in+ A out+ B) and also connect `6A` to `2B` (in– A out– B). These second two must be a twisted pair.

## 6.2 以太网卡诊断程序

Donald 编写的任何诊断程序都可以从他的网站获取。

以太网卡诊断

- Allied Telesis AT1700 -- `at1700.c`
- Cabletron E21XX -- `e21.c`
- HP PCLAN+ -- `hp+.c`
- Intel EtherExpress -- `eexpress.c`
- PCI NE2000 卡 -- `ne2k-pci-diag.c`
- ISA NE2000 卡 -- `ne2k.c`
- RealTek (ATP) 口袋适配器 `atp-diag.c`
- 所有其他网卡 -- 尝试使用 `cat /proc/net/dev` 和 `dmesg` 查看内核关于目标网卡提供了哪些有用信息。

# Linux 以太网教程

## 7. 技术信息

对于想要进一步了解网卡工作原理、玩玩现有的驱动程序、甚至尝试为目前不支持的网卡编写自己的驱动的人，这些信息将非常有用。如果你不属于这一类，可以跳过本节。

### 7.1 程序化 I/O (PIO) vs. 共享内存 vs. DMA

如果你已经可以连续发送和接收数据包，你只需要在总线上放置更多位即可。大多数现代以太网 `dp8390` 驱动（`wd80x3`, `SMC-Ultra`, `3c503`, `ne2000`）都非常接近连续发送包（取决于当前的中断延迟），而 `3c509` 和 `AT1500` 在自动发送连续包方面没有问题。

#### 程序化 I/O（例如 NE2000, 3c509）

- 优点：不使用任何受限系统资源，只需要几个 I/O 寄存器，且没有 16M 限制。
- 缺点：通常传输最慢，CPU 全程等待，且通常很难实现交错的数据包访问。

#### 共享内存（例如 WD80x3, SMC–Ultra, 3c503）

- 优点：简单，比程序化 I/O 快，并允许对数据包进行随机访问。在可能的情况下，Linux 驱动程序会在从网卡拷贝数据时计算输入 IP 数据包的校验和，与同类的 PIO 卡相比进一步减少了 CPU 占用。
- 缺点：占用内存空间（对于 DOS 用户来说是个大问题，在 Linux 下基本上不是问题），而且仍然会占用 CPU。

#### 从机（普通）直接内存器访问（例如 Linux 中没有！）

- 优点：在实际数据传输期间释放 CPU。
- 缺点：检查边界条件、对齐连续缓冲区以及编写 DMA 寄存器使其成为所有技术中最慢的。它还使用了稀缺的 DMA 通道，并需要对齐的内存缓冲区。

#### 总线主设备直接内存器访问（例如 LANCE, DEC 21040）

- 优点：在数据传输期间释放 CPU，可以将缓冲区串联，总线上几乎不需要或不需要丢失 CPU 时间。大多数总线主设备驱动现在使用“拷贝中断”（copybreak）方案，即大数据包由网卡直接放入内核缓冲区，小数据包由 CPU 拷贝，从而为后续处理预热缓存。
- 缺点：（仅适用于 ISA 卡）需要低内存缓冲区和 DMA 通道。任何总线主设备在遇到其他“总线占用者”总线主设备时都会遇到问题，特别是一些原始的 SCSI 适配器。设计不当的主板芯片组在处理总线主设备时存在问题。不使用任何类型的 DMA 设备的原因之一是用 486 处理器来替换 386：这些处理器在每个 DMA 周期中必须刷新其缓存。（这包括 `Cx486DLC`, `Ti486DLC`, `Cx486SLC`, `Ti486SLC` 等。）

### 7.2 总线宽度对性能的影响

ISA 可以达到 5.3MB/sec，这对于 10Mbps 以太网来说似乎足够了。但在 100Mbps 网络的情况下，你需要更快的缓冲区来利用网络带宽。

#### ISA 8 位卡 vs 16 位卡

你可能买不到 8 位 ISA 以太网卡，但可以在二手市场找到很多，价格非常廉。这使得它们在未来几年内很受欢迎。上述结论适用于 16 位 ISA 卡，因为 PCI 卡现在很常见。

一些对于轻量使用提供足够性能的 8 位卡是 `wd8003`，`ec501` 性能很差，这些 12 年历史的遗迹应该被避免。（把它们给 Alan，他正在收集……）

8 位路径对性能不会产生太大影响，因为你可以预计从快速 ISA 总线上的快速主机获得约 800 kb/ps 的下载速度。如果你的大部分网络流量去往远程站点，那么路径上的瓶颈会在其他地方，你只有在本地子网活动时才会注意到速度差异。

### 7.3 32 位（VLB/EISA/PCI）以太网卡

注意，10Mbit 网络通常不需要要求 32 位接口。参见 程序化 I/O vs... 以了解为什么 8MHz ISA 总线上的 10Mbps 以太网真的不是瓶颈。

### 7.4 编写驱动

在 Linux 中使用以太网卡唯一你需要适当的驱动。对于这一点，制造商向公众发布技术编程信息而无需让你（或任何人）签署终身契约是关重要的。获取文档（或者，如果你不写代码，他人编写你所需要的程序的概率）的一个很好的参考，是 Cynr（靠近 Clarkson）数据包驱动的可用性。Russ Nelson 运行在支持 Linux 驱动开发方面提供了极大帮助。网络用户可以尝试这个

- Russ Nelson 的数据包驱动

由于有了文档，你可以为你的网卡编写驱动并让它在 Linux 上运行（至少在）。请记住，某些旧硬件是为

### 7.6 来自 3Com 的技术信息

如果你对为 3Com 网卡编写驱动程序感兴趣，可以从 3Com 获取技术文档。

Cameron 非常友好，在下方告诉了我们操作方法：

3Com 的以太网适配器在我们的“技术参考”（Technical References, TRs）中为编写者提供了文档。这些手册描述了板卡的编程接口，但它们没有介绍终端用户可以使用诊断程序、安装程序等。
