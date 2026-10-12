
### 8.24 Joerg Weedck (jw@peanuts.informatik.tuebingen) / ESCOM

最初是来自 `ESCOM` 的 `486 DX/66`（哪块板？）带有板载 `IDE` 且没有板载 `SCSI`。

- `isa` 适配器：`1542` `SCSI` 控制器
- `mercury lite` (`s3`, `PCI`, `1MB`)
- `ISA-Soundblast-16`
- `mitsumi-cd`（慢的那个）

除了磁带机外，一切运行正常。备用-v7 自 `XFree86-2.1` 以后运行完美。他放弃了 `Intel` 板改用 `ASUS-SP3-g`，但在 `Linux` 下 `PCI` 内存模式会导致崩溃，“看起来像交换器中的死锁”。如果你有关于此的任何信息，请邮件给 `PCI-HOWTO` 的维护者。

关闭 `PCI` 内存功能就可以正常工作。与其给他发邮件，请阅读他的主页 `http://wiswer.informatik.tuebingen.de/jw`，那里也有有关于他 `PCI` 系统的信息。

### 8.25 Ulrich Teichert / ASUS

带有 `AMD486dx40` 的 `ASUS-PCI` 板（但实际上运行在 `33MHz` 上！）他的 `ISA-ET3000 Optima 1024A` 运行良好。连接到板载 `NCR53c810` 的 `Quantum540S` 硬盘没有问题。

## 9. 问题报告

### 9.1 Compaq PCI 系统，特殊型号 Presarios

`Patrick Yaner` (`p.yaner@eos.ncsu.edu`) 向我报告了一个 `Compaq` 特有的问题。似乎他们将 `PCI` `BIOS` 数据映射到内存的一个模糊区域，`Linux`（或 `OS/2`）无法访问该区域。它通常能找到，但无法进入，并在启动时给出“`pcbios.init`: 高内存区域条目，无法访问”。虽然这对显示（位于 `PCI` 总线）和 `IDE` 控制器没有影响，这意味着任何其他 `PCI` 设备（如以太网卡）无法被 `Compaq` 检测。

`Compaq` 为 `DOS` 提供了驱动 `http://ftp.compaq.com/pub/softpaq/Drivers/SP11116.ZIP`，但在 `Linux` 下意味着使用从 `DOS` 启动的程序，而不是 `LILO`。注意 `Compaq` 偶尔会更新其存档中的软件，因此文件 `ftp://ftp.compaq.com/pub/softpaq/allfiles.html`（也可用 `allfiles.txt` 提供）可能对于检查他们是否未升级很有用。

奇怪的是，这些信息也可以在 `SCI HOWTO` 中找到，尽管 `Pressarios` 是内置 `IDE` 的。

### 9.2 Zeos P120 中的 VLSI Wildcat 芯片

`Paul B` (`bame@sde.hp.com`) 报告：`Wildcat` 芯片在后期 `1.3` 和所有 `2.0` 内核中运行良好。

### 9.3 dmarples@comms.eee.strathlyde.ac.uk G/W 2000

`Gateway` `2000` `G/W` `2000` `4DX2/66` `PCI` `ATIGraphics-Ultra-Pro` `IDE`（不明品牌）。它运行良好——只有 `IDE` 卡在 `ISA` 兼容模式下运行，通过 `DOS` 程序切换到 `PCI` 模式后运行更快……这在 `Linux` 下不快，如果有一个补丁就好了。

### 9.4 cip574@wpax01.physik.uni-wuerzburg.de (Frank Hofmann) / ASUS

他带有 `16MB` `RAM`、基于 `ISA` 的 `S3/928` 以及带有 `Seagate` `T47550A` 硬盘的板载 `IDE` 控制器的 `ASUS` 板。较新的 `Linux` 内核对他来说没有问题。

他的问题是：使用 `X` 时，我的鼠标响应不像以前习惯那样。它有时落后于移动，如果快速移动则会跳跃。我认为这是由于板载串口接口使用了 `16550` 串口芯片。这在某个 `Linux` 新闻组（我不知道是哪一个）中讨论过。两周后，我习惯了。

# 问题报告

降低 `16550` 的阈值应该有所帮助。某个处应该有一个设置串口的补丁，不知道为什么。

## 9.5 axel/avalanche.cs-tu-berlin.de (Axel Mahler) / 华硕

`华硕` `PCI-I-486SP3` 主板（`Award` `BIOS` `4.50`, `16` `MB` `RAM`），板载 `NCR` 芯片已禁用，连接了 `Genoa` `Phantom/W32` `PCI`（用于 `PCI` 扩展）和 `Adaptec` `AHA-1542CF` (`BIOS` `v2.01`) 到：

- 一块 `IBM` `1.05` `GB` 硬盘
- 一台 `东芝` `CD-ROM` (`XM4101-B`)
- 一个 `HP` `DAT` 磁带机 (`2GB`)

在创建文件系统时，`mke2fs` (`0.4`, `v.11.93`) 卡死，导致无法安装。在将 `Genoa` `Phantom/W32` `PCI` 替换为 `ELSA` `Winner` `1000` `2MB` `PCI` 后，运行非常完美。我用旧的 `Eizo` `VGA-ISA` 测试了，它的表现和 `Genoa-Pci-card` 一样。

## 9.6 Frank Strauss (strauss@dagagoba.escape.de) / 华硕

`华硕` `SP` 板 `1486DX6/26` `NCR53ec10`，禁用了 `ISA` 插槽上的 `Adaptec` `1542B`，配备两块硬盘（`200MB` `Mactor`, `400MB` `Fujitsu`），`88MB` `RAM` 和 `Tandberg'` `ELSA` `Winner` `1000` `PCI`，`ISA` 插槽上的 `1MB-VRAM` `Soundblaster` `Pro` 位于 `IRQ` `5`，板载 `IDE` 禁用板载串口、并行口，启用软驱

重启后，机器有时会“挂起”（软重启和硬重启一样）——这可能与 `Adaptec` 和声卡无关，因为如果没有它们，系统有时无法启动。但如果它运行了（出现 `ELSA-WINNER-1000-PCI` 消息），它运行得正常。

两个串口按预期识别为 `16550`，但在某些大量数据传输的会话期间，`V22` 出现严重的数据丢失……问题似乎出在硬件上……

`CPU->PCIBurst` 在 `DOS/MS-Windows` 下无法工作

`CPU->PCIBurst` 在 `linux99` 下无法工作，切换虚拟控制台时会乱码，调用 `ghost`、`xdvi` 等应用时崩溃，`SCSI-ID` 在 (`!`) 处报错。

(我怀疑这些应用由于要传输到 `PCI-Winner-1000` 的数据量巨大，会消耗大量的 `CPU->PCI-burst`)

禁用 `CPU->PCI-Burst` 后，运行正常了，`Winner-1000` 在 `1152x846` 分辨率下（`1MB` 缓存不多）使用 `xastones`。带有 `tive` 的 `OpaqueMove` 绰绰有余 :-:-

他有一个 `SATURN` `EXE`，可以在启动 `Linux` 之前在 `DOS` 下引导，帮助在开启突发模式而不会死机……

有人说关闭 `Adaptec-I1542b` 上的“同步协商”(`sync negotiation`) 可能会解决这些问题？我想可以。我不知道 `Adaptec` `1542b` 是否可以这样做。

使用 `PCI-Burst` 时，达到了 `95k` `xastones`，所以他认为这样做没多大。他唯一的问题是，必须让 `Winner-1000` 运行在 `1152x900`，但这失败了，因为它似乎将任何高于 `1024` 像素的分辨率视为 `1280` 像素分辨率，浪费了 `y` 轴上 `86` 像素的结尾……这与 `PCI` 无关。这在 `XFree86-2.1` 中应该已经解决了。

## 9.7 egooch@mc.com / 华硕

- 主板 `ASUS` `PCI/I-486` `SP3` `RAM`: `16MB` (`4x4-SIMM`)
- `CPU` `486DX33` `CPU`
- `BIOS` 版本 `4.50` (`93/12/30`)
- 软驱 两个软驱器 (`1.2` 和 `1.44`)，使用华硕板载软驱控制器
- `SCSI` 尝试了 `WD7000` `SCSI` 控制器和 `Adaptec` `1542CF`，均工作正常。
- 两块 `SCSI` `320M` 硬盘
- `SCSI` `NEC84` `CD` 驱动器
- `SCSI` `QIC150` 存档磁带机
- 视频 - 汉唐 `ET4000` `ISA` 显卡
- 声音 - `PnAS1516` 声卡
- 打印机连接到华硕板载并行口

`PCI` 插槽上什么都没有，但他想买一块 `PCI` 显卡，目前使用 `WD7000` `SCSI` 控制器，一旦驱动程序出来就会切换到板载 `NCR` 芯片。

一切运行完美——连接了 `14.4K` 调制解调器的第一个串口在之前使用后重新连接调调器时偶尔会卡死。他说这不是华硕特有的问题，而是 `SMC-LSI` 设备及其 `16550UART` 的缺陷。第二个端口上的逻辑串口鼠标工作正常。降低鼠标端口的 `16550` 阈值绝对有帮助，但这似乎需要一个特殊的补丁版耳机？我还没有得到相关信息，如果你知道更多，请联系我。

## 9.8 Stefan.Dalibor@informatik.uni-langen.de / 技嘉

- 主板 - `GA-486GS` 技嘉，带有 `256Kb` 缓存，`I4-DX2`
- `BIOS` - `AMI`; `93/8`
- `SCSI` - 板载没有 `scsi` 芯片，使用 `Adaptec` `1542C`
- 视频 - `ELSA` `Winner` `1000`
