
邮件列表：EATA 邮件列表为使用 `EATA-DMA` 和 `EATA-PIO` 驱动的 Linux 用户提供了一个论坛，用于讨论和发布新版本等。如需加入邮件列表，请向 `"linux-request@i-connect.net"` 发送邮件，并在正文中包含 `"subscribe"`。

### /proc/scsi 支持
要获取高级命令，请执行以下操作：
```
echo "eata.dma_latency" >/proc/scsi/eata.dma/<driver.no>
```
并再次关闭：
```
echo "eata.dma_nlatency" >/proc/scsi/eata.dma/<driver.no>
```

### 常见问题
1. 从机未找到控制器。解决方案：使用其中一个 `asci*` 启动盘。
2. IDE 驱动可以在内核 `<v1.3` 中检测到 EATA 板的 ST-506 接口。

   (a) 这看起来类似于以下 2 个示例之一：
   `hdc.c`: ST-506 interface disk with more than 16 heads detected, possibly due to non-standard sector translation. Giving up. (disk _cyl=63, head=64)
   `hdc`: providing with STATUS inside of ALTSTATUS
   `hdc`: MP0242 A, 0MB/128KB Cache, CHS=0/0/0
   `hdc`: cannot handle disk with 0 physical heads
   `hdd`: providing with STATUS inside of ALTSTATUS
   `hdd`: MP0242 A, 0MB/128KB Cache, CHS=0/0/0
   `hdd`: cannot handle disk with 0 physical heads

   如果 IDE 驱动因为此出现问题，你将无法访问你的（实际）IDE 硬件，请更改 EATA 板的 IO 端口和/ IRQ。
   (b) 如果 IDE 驱动找到了它能处理的硬件（容量为 504MB 的硬盘），它将利用 IO 端口和 IRQ，以便驱动可以使用它们。在这种情况下，也更改端口和 IRQ (!=14, 15)。

说明：
3. 某些 SK2011 板的固件损坏。请联系 DPT 客户支持进行更新。

1. 如果你使用 PCI 板，必须使用 `CONFIG_PCI`。

## Future Domain 16x0 带有 TMC-1800、TMC-18C30、TMC-18C50 或 TMC-36c70 芯片

### 支持的配置
- BIOS：2.0, 3.0, 3.2, 3.4, 3.5
- BIOS 地址：0xc800, 0xca00, 0xce00, 0xde00
- 端口：0x140, 0x150, 0x160, 0x170
- IRQs：3, 5, 10, 11, 12, 14, 15
- DMA：未使用
- IO：端口映射

### 自动探测
适用于所有支持的配置，需要安装 BIOS

### 自动探测覆盖 (Autrobe Override)
无

### 陈旧性问题，通过升级修复
1. 旧版本不支持 TMC-18C50 芯片，在较新的板上会失败。
2. 旧版本将没有用于自动检测的最新 BIOS 签名。
3. Linux 1.0.9 和 1.1.6 之前的版本不支持新的 SCSI 芯片或 3.4 BIOS。

### 说明
1. Future Domain BIOS 从高 ID 到 0 扫描 SCSI 设备，顺序与其他 SCSI BIOS 反之。dda 将是“反序”（即，D: 反序 C.）。你可能还需要为 LILO 使用 disktab 覆盖。

## 通用 NCR5380 / T130B (标准)

### 支持与不支持的配置
- 端口：全部
- IRQs：全部
- DMA 通道：不使用 DMA
- IO：端口映射

### 自动探测
无

### 自动探测覆盖
编译时：定义 `GENERIC_NCR5380_OVERRIDE` 为一个元组数组，包含端口、irq、dma、板卡类型 - 例如：
```
#define GENERIC_NCR5380_OVERRIDE ((0x330, 5, DMA_NONE, BOARD_NCR5380))
```
用于端口 330、IRQ 5 的 NCR5380 板。
```
#define GENERIC_NCR5380_OVERRIDE ((0x330, 5, DMA_NONE, BOARD_NCR5380))
```
用于端口 0x350 的 T130B 板。

旧版本的代码消除了 `BOARD*` 条目。符号 IRQs `IRQ_NONE` 和 `IRQ_AUTO` 可以使用。

## 5. HOSTS

### 内核命令行
```
ncr5380=port,irq
ncr5380=port,irq,dma
ncr5c00=port,irq
```
255 可用于无 irq，254 用于自动探测。

### 常见问题
1. 使用旧版（发布前 6）通用 NCR5380 驱动的 T30B 板不支持 `ncr5c00` 命令选项。兼容寄存器距离基地址偏移八。因此，如果你的地址设置为 0x350，请在内核命令行中使用 `ncr5380=0x350,254`。

### 陈旧性问题，通过升级修复
1. 在访问 T30B 或其他 NCR5c00 板时内核锁死。发布前的 6 版本 Generic5380 驱动不支持这些上的中断。

### 说明
1. 通用驱动尚未支持 DMA，且不支持伪 DMA。

## 5. NCRc8xx (标准)

### 支持与不支持的配置
- 基地址：全部
- IRQs：全部
- DMA 通道：PCI 不适用
- IO：端口映射，总线主

### 自动探测
需要 PCI BIOS，使用 BIOS 例程搜索设备并读取配置空间。驱动在某些寄存器中使用预编程值初始化，因此必须安装 BIOS。

### 陈旧性问题，通过升级修复
1. 旧版本的 Linux 有 6.2.7 问题。
2. 旧版本的 Linux 不识别 '815' 和 '825' 板。
3. 发行版内核包含 4 或 5 版本的驱动，该驱动不支持 disconnect/reconnect（这是其最明显的影响）、多主机适配器以及无 BIOS 操作。最新版本的驱动可在：
```
ftp://tx-11.mit.net/pub/linux/scsi/ncr5381
```
目前是 1.2.10 以及其他补丁，使发布版本仅限于 1.3x。这些补丁并不完全干净，由于基线版本中的某些 ELF 和其他补丁，如果你手动控制补丁，就不应该使用它们。请注意只需要最新的补丁；这些是增量的。如果你想在 1.3x 内核上运行新的 NCR 驱动，之前的 Harald Evensen <Harald.Evensen@pvv.unit.no> pub/Linux/ncr
```
ftp://pvv.unit.no ~*/pub/Linux/ncr
```
这些补丁可能是干净的。请查看这些目录中的所有 README。如果你对运行 ALPHA 代码感兴趣，应该加入 NCR 邮件列表，因为中间错误修复和后续版本的发布在此列表中。如需订阅，向 `majordomo@colorado.edu` 发送邮件并包含：
```
subscribe ncr53c8
```
在文中。你可以通过向同一地址发送邮件并包含：
```
unsubscribe ncr53c8
```
在文中。

1. 很多人遇到过问题：芯片在 DOS 下工作正常但在 Linux 下因丢失中断导致超时失败。这通常是因为槽位或主板设备的 IRQ 跳线与 CMOS 设置中的值不匹配。双重检查
   - 你使用的 IRQ 仅供板载 NCR 芯片使用，或者安装了槽位 NCR 芯片
   - 任何选择板载芯片或槽位 IRQ 的主板跳线都与你的 CMOS 设置匹配
   - 某些 PCI 主板具有“自动”分配功能，可能有效也可能无效。

这可能是因为在仅支持 PCI INTA 的系统中在 PCI 板上选择了 PCI INTB、INT 或 INTD。如果你使用具有选择 PCI 中断线之间跳线的 NCR 板，请确保你使用的是 INTA。最后，PCI 应该使用水平触发而非边沿触发。检查你的板跳线是否设置为水平触发，如果失败为边沿触发，说明你的系统可能损坏了。

这个问题在某些 Vigen 主板上特别常见，手册中没有说明板载 IRQ 跳线设置。我听说所谓的 IRQS 实际上是 IRQ9，视情况而异。

2. 使用 S3 928 或 Tseng ET 4000W32 PCI 视频板时会发生死机/其他问题。这些芯片的某些版本中存在硬件缺陷。不要使用它们。

3. 启动时收到消息，指示 I/O 映射被禁用，因为地址 0 的位 0...1 表示非 I/O 映射。由于某些芯片中的一个缺陷，导致配置寄存器的字读取返回的高低 16 位交换了。

4. 如果启用了 PCI 写缓冲或 CPU->PCI 缓存，某些系统会出现问题。如果你有问题，请禁用这些选项。

5. 某些在板载 BIOS ROM 和系统 BIOS 中都有 NCR SDMS 软件的无法启动 DOS。在某处启用镜像应该解决这个问题。

6. 如果你遇到消息：
```
'scias: IRQ0 not free, detaching'
```
或
```
'scias: IRQ25 not free, detaching'
```
NCR 芯片在 PCI 配置寄存器中存储的全 0 或 1。要么你有配置问题（见 1），要么你的主板 BIOS 有缺陷。作为解决方法，你可以编辑 `drivers/src/ncr53e7.xx.c`，并修改 `pci_init()` 使你拥有
```
irq = my_irq;
```
在之前
```
return normal_init (tpnt, board, chip, (int) base,
(int) io_port, (int) irq, DMA_NONE, 1, bus, device_fn,
options);
```
- 7. 某些系统带有隐藏的 BIOS 芯片。在确保你从供应商那里获得了最新的 ROM 之前，不要提交任何 报告。
- 8. 命令行覆盖 `ncr3c810=xxx` 等参数不起作用。
在发行版内核中，它们的入口点没有包含在 `init/main.c` 中，这是非常有刻意的之：
驱动程序并没有尝试避免对使用了命令行覆盖的板卡进行探测，因此如果你在 PCI 配置例程实际显示板卡出现的地方使用了覆盖，你将遇到大问题。
你可能需要覆盖的唯一理由是 PCI 硬件 | BIOS 损坏，在这种情况下，Linux 会返回某些错误，使得覆盖变得意义微乎其微。
几乎所有认为自己需要命令行覆盖的人，都是因为他们收到了来自驱动程序的配置或错误信息。如果你有配置问题，说明你的系统损坏了或配置有问题，任何覆盖都无法解决这个问题。
- 9. 某些板卡（主要是 Nextor）不使用 NCR BIOS 超时。其中某些 ROM 处理同步传输时会进行同步电源协商，并在上电后让驱动器处于未知状态。当发行版 Linux 驱动程序尝试与它们通信时，它会超时且无法恢复，因为它没有使用总线重置或重新协商。
如果你遇到这个问题，可以在板卡的设置程序中禁用同步传输，或者升级到 NCR 驱动的新版 ALPHA 接收器，它将进行同步协商。
- 10. Ryan $1365 *825 板卡在超时方面存在问题，特别是当启用了断开连接时。这些板卡中的某些删除了关于终端跳线的文档——导致在当你需要时它是关闭的，而在它不该关闭时却是开启的。
尝试反转跳线的位置。

### 说明
- 1. 必须设置 `CONFIG.PCI`

## 5.14 Seagate ST0x/Future Domain TMC-8xx/TMC-9xx (标准型)

### 支持和不支持的配置
| 特性 | 值 |
| :--- | :--- |
| 基地址 | 0x8000, 0x0ca00, 0x0cc00, 0xe000, 0xdc00, 0xde000 |
| IRQs | 3, 5 |
| DMA 通道 | 不使用 DMA |
| IO | 内存映射 |

### 自动探测 (Autoprobe)
仅探测地址，假设 IRQ 为 5，需要安装 BIOS。

### 自动探测
编译时：
将 `OVERRIDE` 定义为基地址，根据需要将 `CONTROLLER` 定义为 FD 或 SEAGATE，并将 `IRQ` 定义为相应的 IRQ。

内核命令行：
`st0x=address,irq` 或 `tmc8xx=address,irq`（仅对 .99.13b 及更高版本有效）

### 旧问题，通过升级修复
![](img/e0ed64e774a11b944fd2651b5a09cd8c_1408_0.png)
1. Linux .99.12 内核之前的版本在与某些慢速设备握手时存在问题，这是当你向总线写数据时发生的情况：
- (a) 写字节到数据寄存器，数据寄存器断言总线
- (b) time_remaining = 12us
- (c) 等待 time_remaining > 0 且 REQ 未被断言
- (d) 如果 time_remaining > 0，则断言 ACK
- (e) 等待 time_remaining > 0 且 REQ 已断言
- (f) 取消断言 ACK

问题出现在慢速设备的命令处理中，当它们读取命令时，REG/ACK 握手超过了 12us —— REQ 没有在驱动程序预期的时刻下降，导致驱动程序最终为每个 REQ 脉冲发送了多个字节的数据。

2. 在 Linux .99.12 中，修复仲裁代码时引入了一个 bug，导致某些系统上的选择失败。这在 .99.13 中已修复。

## 常见问题
- 1. 当 Linux 尝试读取分区表或其他磁盘访问时，会出现命令超时。板卡出厂默认设置是针对 MSDOS 的，会被中断。要让板卡支持中断，Seagate 使用 W3 (ST01) 或 JP3 (ST02) 并短接 F-G 引脚以中断 IRQ 5。
2. Seagate 将 SCSI 磁带和 CDROM 绑定到 PC IO 通道和（可选的）OWS 。。的是，它不会告诉你看门定时器超时，你无法确定 REQ 是否已变低，并可能将 REQ 脉冲误认为多次 REQ。

处理这个问题意味着使用紧凑循环寻找 REQ 变低，由于中断的存在，你无法捕获该转换。这会导致性能损失，因此将其应用到所有 SCSI 设备上是不理想的。相反，它是根据 SCSI 设备中的 'broken' 字段按每个设备进行选择的，你应该将你的设备添加到 scsi_devices 的设备列表中（目前，TENEX CDROM 驱动器尚未将其重置为零）。
- 3. 未来的板卡（特定示例包括 840, 841, 880 和 881）无法工作。未来的板卡使用 Seagate 映射，并填充 MSG 和状态寄存器位。你应该编辑 `seagate.h`，交换 MSG 和 STAT 的定义，并重新编译内核，将 CONTROLLER 定义为 SEAGATE 和适当的 IRQ。
- 4. 当使用 fdisk 更新驱动器时，你会收到指示 HDIO.REQ 或 HDIO.GEO 失败的错误信息，必须指定头数和磁道。可以查看 6.4。
- 5. 手动指定驱动器几何结构后，后续读取分区表会导致分区不在边界上，物理和逻辑边界不匹配等。
- 6. 某些在 .99.13 之前工作的系统在较新版本的 Linux 上失败。旧版本的 Linux 分配 CONTROL 和 DATA 寄存器的顺序与 Seagate 文档不同，某些系统如此。`seagate.c` 中的代码如下：
```
cli();
DATA = (unsigned char) ((1 << target) |
(controller_type == SEAGATE ? 0x80 : 0x40);
CONTROL = BASE_CMD | CMD_DRVR_ENABLE | CMD_SEL |
(reselect ? CMD_ATTN : 0);
```
改为：
```
cli();
CONTROL = BASE_CMD | CMD_DRVR_ENABLE | CMD_SEL |
(reselect ? CMD_ATTN : 0);
DATA = (unsigned char) ((1 << target)) |
(controller_type == SEAGATE ? 0x80 : 0x40);
sti();
```
你的问题。定义：
> FAST 或 FAST32 将尽可能使用传输
> ARBITRATE 会导致主机适配器仲总线以获得更好的 SCSI-II 兼容性，而不是只等待 BUS FREE。它应该允许每个 lun 执行一个命令
> SLOW_HANDSHAKE 将允许与握手不够快的设备（例如某些 CD ROM）兼容
> SLOW_RATE-x 在握手不正常时允许你指定默认传输速率。

## 5.15 PAS16 SCSI (标准型)

### 支持和不支持的配置
| 特性 | 值 |
| :--- | :--- |
| 端口 | 0x388, 0x384, 0x38x, 0x288 |
| IRQs | 10, 12, 14, 15 |
| 重要 | IRQ 必须与板卡的音频部分 IRQ 不同 |
| DMA | 不用于板卡的 SCSI 部分 |
| IO | 端口映射 |

### 自动探测
不需要 BIOS

### 自动探测覆盖
编译时：将 `PAS16_OVERIDE` 定义为端口、irq 元组。例如：
```
#define PAS16_OVERIDE {{0x388, 10}}
```
