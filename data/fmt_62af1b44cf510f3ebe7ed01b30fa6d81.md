
- `index=base` : 在指定的 `addr` 上探测接口，其中 "`base`" 通常是 `0x1f0` 或 `0x170`，且 "`ctl`" 被假设为 "`base=+0206`"

- `index=base, ctl` : 同时指定 `base` 和 `ctl`

- `index=base, ctl, irq` : 指定 `base`、`ctl` 和 `irq` 数字

- `index=autotune` : 驱动将尝试将此接口上所有驱动器的速度调整为支持的最快 PIO 模式。并非所有芯片组类型都完全支持，并且很可能与旧式或奇特的 IDE 驱动产生问题。

- `index=noautotune` : 驱动不会尝试调整接口速度，这是大多数芯片组的默认设置，`cmd64` 除外。

- `index=serialize` : 不在 `index` 和 `deid(x^1)` 上重叠操作

# A 节：BootPrompt-HOWTO 391

以下内容仅在 `ide0` 上有效，且不能更改 `base`、`ctl` 端口的默认值。

- `ide0=dtc2278` : 探测/支持 `DTC2278` 接口

- `ide0=ht6560b` : 探测/支持 `HT6560B` 接口

- `ide0=cmd64_vlb` : 带有 `CMD640` 芯片的 VLB 卡必需（不用于 PCI — 自动检测）

- `ide0=qd6580` : 探测/支持 `qd6580` 接口

- `ide0=ali14xx` : 探测/支持 `ali14xx` 芯片组（ALI M1439/M1445）

- `ide0=umc8672` : 探测/支持 `umc8672` 芯片组

其他所有会被 BAD OPTION 消息拒绝。

### 标准 ST-506 磁盘驱动选项 (`hd=`)

磁盘驱动可以接受类似于 IDE 驱动的磁盘几何结构参数。注意，它只期望三个值（C/H/S）——多一个或少一个它都会静静地忽略你。此外，它只接受 `hd=` 作为参数，即 `hda=`、`hdb=` 等在此处无效的。格式如下：

```
hd=cyls, heads, sects
```

如果安装了两个磁盘，则用第二个磁盘的几何参数重复上述内容。

### XT 磁盘驱动选项 (`xd=`)

如果你足够不幸地正在使用这些数据传输速度高达 125KB/s 的旧式 8 位卡之一，那么这就是了。这些卡的探测代码会寻找已安装的 BIOS，如果没有，探测将找不到你的卡。或者，如果你的 BIOS 签名字符串未被识别，也将无法找到。在任何情况下，你都必须使用如下形式的启动参数：

```
xd=type, irq, iobase, hdb, dma_chan
```

# 392

# 资源附录

`type` 值指定卡的特定制造商，如下：0=通用；1=DTC；2,3,4=西部数据（Western Digital）；5,6,7=希捷（Seagate）；8=OMTI。同一制造商多个类型之间的区别在于用于检测的 BIOS 字符串，如果指定了类型 则不使用该字符串。

`xd_setup()` 函数对你输入的四个值不做任何检查。不要让它失望。以下是一个禁用/移除 BIOS 的 WD1002 控制器的示例用法，使用了“默认”的 XT 控制器参数：

```
xd=2, 5, 0x320, 3
```

### 光驱 (非-SCSI/ATAPI/IDE)

此节列出了所有与光驱设备相关的可能启动参数。注意，这不包括 SCSI 或 IDE/ATAPI 光驱。请查看此类类型光驱的相应章节。

注意，大多数此类光驱都有你应该阅读的文档文件，且它们都位于一个方便的地方：`linux/Documentation/cdrom`。

#### Aztec 接口 (`aztcd=`)

此类驱动的语法为：

```
aztcd=obase[,magic_number]
```

如果你将 `magic_number` 设置为 `0x79`，在固件版本未知的情况下，驱动将尝试运行。所有其他值均被忽略。

#### Sony CDU-31A 和 CDU-33A 索尼接口 (`cdu31a=`)

这种光驱接口位于某些 Pro Audio 卡以及其他索尼提供的卡上。语法如下：

```
cdu31a=iobase,[irq,is_pas_card]
```

指定 IRQ 值为零告诉驱动硬件不支持中断（如某些卡）。如果你的卡支持中断，应该使用它们，这可以降低 CPU 占用。如果是 Pro Audio 卡，`is_pas_card` 应该输入，否则不指定。

#### Sony CDU-535 接口 (`sony535=`)

光驱接口的语法为：

```
sony535=iobase[,irq]
```

零可以作为 I/O 基址，用于指定 IRQ 值。

#### GoldStar 接口 (`gscd=`)

光驱接口的语法为：

```
gscd=iobase
```

#### ISP16 接口 (`isp16=`)

光驱接口的语法为：

```
isp16=[port,drive_type]
```

对 `irq` 使用零意味着它们未使用。`drive_type` 的允许值为 `noisp16`、`Sanyo` 和 `Mitsumi`。`noisp16` 禁用驱动。

#### Mitsumi 标准接口 (`mcd=`)

光驱接口的语法为：

```
mcd=iobase,[irq,wait_value]
```

`wait_value` 用于用于驱动的内部超时，取决于编译。

#### Mitsumi XA/MultiSession 接口 (`mcdx=`)

目前该“实验性”驱动有 `setup` 函数，但尚未实现参数。用于相同的硬件，但驱动具有扩展功能。

#### Optics 接口 (`optcd=`)

此类卡的语法为：

```
optcd=iobase
```

#### Phillips CM206 接口 (`cm206=`)

此类卡的语法为：

```
cm206=[iobase,irq]
```

驱动假设 3 到 11 之间的数字为 IRQ 值，`0x300` 到 `0x370` 之间的数字为 I/O 端口，因此你可以任何顺序指定一个或两个。它也接受 `cm206=auto` 来启用自动探测。

#### Sanyo 接口 (`sjcd=`)

```
sjcd=iobase[,irq,dma_channel]
```

#### SoundBlaster Pro 接口 (`sbcd=`)

语法为：

```
sbcd=iobase,type
```

其中 `type` 为以下之一（大小敏感）：'SoundBlaster', 'LaserMate' 或 'SPEA'。I/O 基址是光驱接口的，而不是声部分的。

# 串口和 ISDN 驱动

#### ICN ISDN 驱动 (`icn=`)

该 ISDN 驱动期望启动参数形式：

```
icn=iobase,membase,icn_id1,icn_id2
```

其中 `iobase` 是卡的 i/o 端口地址，`membase` 是共享内存基地址，两个 `icn_id` 是唯一的 ASCII 字符串标识。

#### PCBIT ISDN 驱动 (`pcbit=`)

此启动参数采用整数对形式：

```
pcbit=membase1,irq1[,membase2,irq2]
```

其中 `membaseN` 是第 N 张卡的共享内存基，`irqN` 是第 N 张卡的中断设置。默认值为 IRQ 5 和 `membase` `0xD000`。

# Teles ISDN 驱动 (`teles=`)

该 ISDN 驱动期望启动参数形式：

```
teles=iobase,irq,membase,protocol,teles_id
```

其中 `iobase` 是卡的 i/o 端口地址，`membase` 是卡的共享内存基地址，`irq` 是卡使用的中断通道，`teles_id` 是唯一的 ASCII 字符串标识。

#### DigiBoard 驱动 (`digi=`)

`DigiBoard` 驱动接受六个逗号分隔的标识符或整数字符串。顺序如下：

- 启用/禁用此卡

- 卡类型：PC/Xi(0), PC/Xe(1), PC/Xeve(2), PC/Xem(3)

- 启用/禁用替代引脚排列

- 此卡的端口数量

- 配置配置的 I/O 端口（使用字符串标识时为十六进制）

- 内存窗口基址（使用字符串标识时为十六进制）

正确的启动提示参数示例（均为标识符和整数形式）：

```
digi=E,PC/Xi,D,16,200,D0000
digi=1,0,16,512,851968
```

注意，在缺少 `digi=` 启动参数的情况下，驱动默认 i/o 为 `0x200`，共享内存基址为 `0xD000`。没有执行自动探测。更多细节可以在 `linux/Documentation/digiboard.txt` 文件中找到。

# RIScom/8 多端口串口驱动 (`riscom8=`)

通过为每个安装的板提供四个唯一的 i/o 端口值，最多支持四块板。其他细节可以在 `linux/Documentation/riscom8.txt` 中找到。

# Baycom 串口/并行无线调制解调器 (`baycom=`)

这些设备的启动参数格式为：
