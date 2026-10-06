
```
加载命令：
/sbin/modprobe ewr3.o
io = 0x300
irq = 5
(模块无自动探测！
在 EISA 总线上进行 EISA 探测。
静态链接探测 ISA 总线上的端口：
0x100, 0x120, 0x140, 0x160, 0x180, 0x1A0, 0x1C0,
0x200, 0x220, 0x240, 0x260, 0x280, 0x2A0, 0x2C0, 0x2E0,
0x300, 0x340, 0x360, 0x380, 0x3A0, 0x3C0)
```

# 网络设备支持 (eexpress.o.)

## 7.12.5 EtherExpress 16 支持 (eexpress.o.)

加载命令：

```
/sbin/modprobe eexpress.o
```

`io = 0x300`
`irq = 0`          (从 EEPROM 读取 IRQ 值)
探测端口：`0x300`, `0x270`, `0x320`, `0x340`

## 7.12.6 EtherExpressPro 支持 (eepro.o.)

加载命令：

```
/sbin/modprobe eepro.o
```

`io = 0x200`
`irq = 0`
探测端口：`0x200`, `0x240`, `0x280`, `0x2C0`, `0x300`, `0x320`, `0x340`, `0x360`

## 7.12.7 Fujita FMV-181/182/183/184 支持 (fmv18x.o.)

加载命令：

```
/sbin/modprobe fmv18x.o
```

`io = 0x220`      用于基地址
`irq = 0`          用于 IRQ

探测端口：`0x220`, `0x240`, `0x260`, `0x280`, `0x2a0`, `0x2c0`, `0x300`, `0x340`

## 7.12.8 HP PCLAN+ (27247B 和 27252A) 支持 (hp-plus.o.)

加载命令：

```
/sbin/modprobe hp-plus.o
```

`io = 0`          (如果不提供 `io=0xNNNN` 则会报错)
`irq = 0`          (从寄存器读取 IRQ)
探测端口：`0x200`, `0x240`, `0x280`, `0x2C0`, `0x320`, `0x340`

依赖于 `8390.0`。

## 7.12.9 HP PCLAN (27245 和其他 27xx) 支持 (hp.o.)

加载命令：

```
/sbin/modprobe hp.o
```

`io = 0`          (如果不提供 `io=0xNNNN` 则会报错)
`irq = 0`          (驱动程序通过 autoIRQ 选择 IRQ)
探测端口：`0x300`, `0x320`, `0x340`, `0x280`, `0x2C0`, `0x200`, `0x240`

依赖于 `8390.0`。

## 7.12.10 HP 10/10VG PCLAN (ISA, EISA, PCI) 支持 (hp100.o.)

加载命令：

```
/sbin/modprobe hp100.o
```

`hp100_port = 0` (IO 基地址)

(如果是 EISA 插槽，则进行 EISA 探测：

在 EISA 总线上探测从 `0x100` 到 `0x3E0`，步长为 `0x020`)

## 7.12.11 Ether 16i/32 支持 (eth16i.o)。

加载命令：

```
/sbin/modprobe eth16i.o
```

`io = 0x2a0` (如果不提供 `io=0xNNN` 则会报错)
`irq = 0` (驱动程序通过 autoIRQ 选择 IRQ)

`eth16i` 上的探测端口：

`0x260`, `0x280`, `0x2A0`, `0x240`, `0x340`, `0x320`, `0x380`, `0x300`

`eth32i` 上的探测端口：

`0x1000`, `0x2000`, `0x3000`, `0x4000`, `0x5000`, `0x6000`, `0x7000`, `0x8000`

`0x9000`, `0xA000`, `0xB000`, `0xD000`, `0xE000`, `0xF000`

## 7.12.12 NE2000/NE1000 支持 (ne.o)。

加载命令：

```
/sbin/modprobe ne.o
```

`io = 0` (明确要求 `io=0xNNN` 值)
`irq = 0` (通过 autoIRQ 确定 IRQ)

(探测端口：`0x300`, `0x280`, `0x320`, `0x340`, `0x360`)

依赖于 `8390.0`。

## 7.12.13 NI5210 支持 (ni52.o)。

加载命令：

```
/sbin/modprobe ni52.o
```

`io=0x360`
`irq=9`
`memstart=0xd000`
`memend=0xd400`

不要使用自动探测，`io=0`。

# EISA, VLB, PCI 和板载控制器

## 7.13.1 Ansel Communications EISA 3200 支持 (ac3200.o)。

加载命令：

```
/sbin/modprobe ac3200.o
```

由于是 EISA 板卡，自动探测应该有效。

依赖于 `8390.0`。

# 网络设备支持

## 7.13.2 板载 Apricot Xen-II 以太网 (apricot.o)。

加载命令：

```
/sbin/modprobe apricot.o
io = 0x300` (不可修改！)
irq = 10
```

## 7.13.3 DE425, DE434, DE435, DE450, DE500 支持 (de4x5.o)。

加载命令：

```
/sbin/modprobe de4x5.o
io = 0x000b
irq = 10
is_not_dec = 0
```

对于使用 DEC 21040/21141 芯片的非 DEC 卡，将其设为 1
(EISA 和 PCI 探测)

## 7.13.4 DEChip Tulip (de2xl4x) PCI 支持 (tulip.o)。

加载命令：

```
/sbin/modprobe tulip.o
读取 Documentation/networking/tulip.txt
```

## 7.13.5 Digi Intl. RightSwitch SE-X 支持 (digrs.o)。

这是用于 Digi International RightSwitch SE-X EISA 和 PCI 板卡的 Linux 驱动程序。这些是将 4 (EISA) 或 6 (PCI) 个交换机组合在一块板卡上。有一个用于设置每个端口输入输出过滤的工具，称为 "`dgrs`"。管理工具允许图形化查看性能，以及 SNMP 代理 IP 地址、生成时间。这些也可以在加载驱动时从命令行设置。还有一个配套工具 "`xright`"。

加载命令：

```
/sbin/modprobe digrs.o
```

| `debug=NNN` | 调试级别 |

| :--- | :--- |

| `dma=0/1` | 禁用/启用 PCI 卡 |

| `spant=0/1` | 禁用/启用生成树 |

| `hashtype=NNN` | 老化时间（默认 300 秒） |

| `ipaddr=A,B,C` | 设置 SNMP 地址 199,86,21 |

| `ipxnet=NNN` | 设置 IPX 数字 |

# 7.14 便携式适配器

## 7.14.1 D-Link DE600 支持 (de600.o)。

加载命令：

```
/sbin/modprobe de600.o
de600 = 0` (在端口 `0x378`，IRQ 7；可配置)
```

## 7.14.2 D-Link DE620 数据适配器 (de620.o)。

加载命令：

```
/sbin/modprobe de620.o
```

`bnc = 0`, `utp = 0` (强制介质。)
`io = 0x378` (也可配置)
`irq = 7`

# 7.15 Token Ring 支持

## 7.15.1 Tropic 芯片组适配器 (ibmtr.o)。

加载命令：

```
/sbin/modprobe ibmtr.o io=0xa0 irq=0
```

`io = 0xa0` 你不应使用 insmod 进行自动探测)

## 7.16 ARCnet 支持 (arcnet.o)。

读取 `/usr/src/linux/Documentation/arcnet.txt` 中的信息。该处还有 `arcnet-hardware.txt`。

加载命令：

```
/sbin/modprobe arcnet.o io=0x300 irq=2 shmem=0xd00
```

你可以将设备命名为 '`device=arc1`'（第二个板卡）或根据喜好命名为 '`device=eth0`'。

探测时，可能的地址有：

建议的：

`0x300`, `0x2E0`, `0x2F0`, `0x2D0`

其他的：

`0x200`, `0x210`, `0x220`, `0x230`, `0x240`, `0x250`, `0x260`, `0x270`,

`0x280`, `0x290`, `0x2A0`, `0x2B0`, `0x2C0`,

`0x310`, `0x320`, `0x330`, `0x340`, `0x350`, `0x370`,

`0x380`, `0x390`, `0x3A0`)

# 8 ISDN 子系统

设置 ISDN 网络是一项复杂的任务。在 `/usr/src/linux/Documentation/isdn` 中可以找到文档。

## 8.1 ISDN 支持 (isdn.o)。

加载命令：

```
/sbin/modprobe isdn.o
```

没有模块参数。

依赖于 `slhc.o`。

# 9 CD-ROM 驱动（不用于 SCSI 或 IDE/ATAPI 驱动器）

## 8.2 ICN 2B 和 4B 支持 (icn.o)。

加载命令：

```
/sbin/modprobe icn.o [parameters]
portbase=p membase=m icn_id=stringstringicn_id2=string2]
```

`p =` 基地址          (默认: `0x320`)

`m =` 共享内存      (默认: `0xd0000`)

```

使用 ICN 双卡时，必须定义两个 idstring。
idstring 必须以字符开头！

依赖于 `isdn.o`。

## 8.3 PCBIT-D 支持 (pcbit.o)。

加载命令：

```
/sbin/modprobe pcbit.o
```

`mem = 0`      default = `0xd0000`

`irq = 0`      default = `5`

依赖于 `isdn.o`。

## 8.4 Teles/NICCY1016PC/Creatix 支持 (teles.o)。

加载命令：

```
/sbin/modprobe teles.o io...
```

`io=m0,i10,p0,do[ml,il,pl1,dl] ... ,mn,in,pn,dn] teles_id=idstring`

`m0 =` 第一块板卡的共享内存。（默认: `0xd0000`）

`i0 =` 第一块板卡的 IRQ。（默认: `15`）

`p0 =` 第一块板卡的基地址。（默认: `0xd80`）

`d0 =` 第一块板卡的 D 道协议。1=TR6, 2=EDSS1（默认: 2）

`pl1,ml1,dl =` 第二块板卡的参数（默认: 无）
`pn,in,mn,dl =` 第 n 块板卡的参数（最多使用 16 块板卡）

`idstring =` 使用工具访问和识别时的驱动 ID，
当使用线路监控器时。（默认: 无）
`idstring` 必须以字符开头！

板卡类型由端口、irq 和共享内存决定：

```
port == 0, shared memory != 0 -> Teles S0-8
port != 0, shared memory != 0 -> Teles S0-16.0
port != 0, shared memory == 0 -> Teles S0-16.3
```

依赖于 `isdn.o`。

# 9.1 Aztech/Orchid/Okano/Wearneas/TXC/CyDROM 支持 (aztcd.o)。

![](img/e0ed64e774a11b94fd26515a09cd8c_1202_0.png)

1202

加载命令：
`/sbin/modprobe aztcd=aztcd={baseaddress}`

查阅 `Documentation/cdrom/aztcd` 获取完整信息。

## 9.2 金星 R420 CDROM 支持 (gscd)。

关于金星 R420 CDROM 以及此 Linux 驱动的所有信息，请访问已安装的 WWW 页面：http://linux.rz.fh-hannover.de/~raupch。

加载命令：
`/sbin/modprobe gscd.gscd=0340`。

```
x 的默认基地址
这适用于大多数应用程序。
地址选择通过金星接口卡上的
跳线 PN801-1 到 PN801-4 完成。
适当的设置为：0300, 0310, 0320, 0330, 0340, 0350,
0360, 0370, 0380, 0390, 03A0,03B0,03C0,03D0,03E0,03F0
```

## 9.3 松下/美能/Creative、长星、TEAC 支持 (sbpcd)。

加载命令：
`/sbin/modprobe sbpcd.sbpcd=[address], x`
`address = iaddress`
`x = SBPRO` 设置，查阅 `Documentation/cdrom/sbpcd`

## 9.4 三光 (Mitsumi) 标准型 noXA/多轨道支持 (mcd.o)。

加载命令：
`/sbin/modprobe mcd.o mcd=0x300,11,0x304,5`

其中参数以地址和 irq 成对出现。

## 9.5 三光 MitsumiA/多轨道支持 (mcdx.o)。

加载命令：
`/sbin/modprobe mcdx.o mcdx=0x300,11,0x304,5`

其中参数以地址和 irq 成对出现。

## 9.6 Optics Storage DOLPHIN 8000AT CDROM 支持 (optcd.o)。

这是用于所谓“DOLPHIN”驱动器的程序，具有 34 针 Sony 兼容接口。对于 IDE 兼容的 Optics Storage 8001 驱动器，你需要 ATAPI CDROM 驱动程序。该驱动似乎适用于 Lasermate CR328A。

加载命令：
`/sbin/modprobe optcd.o optcd=0x340`

参数为显卡的基地址。

## CD 驱动程序（非 SCSI 或 IDE/ATAPI 驱动器）

## 9.7 飞利/LMS CM206 CDROM 支持 (cm206.o)。

这是飞利/LMS cm206 cdrom 驱动程序，配合 cm260 热插适配卡使用。

加载命令：

```
/sbin/modprobe cm206.o cm206=0x300,11
```

其中参数为显卡的基端口和 irq。
基端口和 irq 行的顺序不重要。
你可以仅指定其中一个，
另一个将取编译时的默认值。

## 9.8 三洋 CDR-H94A CDROM 支持 (sjcd.o)。

加载命令：

```
/sbin/modprobe sjcd.o sjcd_base=0x340
```

其中参数为显卡的基地址。
默认地址 = `0x340`，无 irq，无 dma。

## 9.9 ISP16/MAD/16/Mozart 软配置 cdrom 接口支持 (isp16.o)。

加载命令：

```
/sbin/modprobe isp16.o [parameters]
```

```
isp16_cdrom_base=<port>
isp16_cdrom_irq=<irq>
isp16_cdrom_dma=<dma>
isp16_cdrom_type=<drive_type>
```

有效值为：
`port=0x340,0x320,0x330,0x360`
`irq=0,3,5,7,9,10,11`
`dma=0,3,5,6,7`
`drive_type=-noispl6,Sanyo, Panasonic,Sony,Mitsuki`。

> 注意这些选项对默认值很敏感。

## 9.10 Sony CDU31A/CDU33A CDROM 支持 (cdu31a.o)。

加载命令：

```
/sbin/modprobe cdu31a.o [parameters]
```

```
cdu31a_port=<I/O address> - 设置基 I/O。
必须指定此项。
```

```
cdu31a_irq=<interrupt> - 设置中断号。
不留此项将关闭中断。
```

## 9.11 Sony CDU535 CDROM 支持 (sonycd535.o)。

加载命令：

```
/sbin/modprobe sonycd535.o sonycd535=[address]
```
