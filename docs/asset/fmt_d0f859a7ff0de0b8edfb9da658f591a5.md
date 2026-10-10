
```c
01 void sdr7m__init(void)
02 {
03     ulong sdtr;
04     ulong rtr;
05     int i;
06     
07     /*
08      * 支持 100MHz 和 133MHz SDRAM
09      */
10     if (get_bus_freq(0) > 100000000) {
11         /*
12          * 133 MHz SDRAM
13      */
14         sdtr = 0x01074015;
15         rtr = 0x07f00000;
16     } else {
17         /*
18          * 默认: 100 MHz SDRAM
19      */
20         sdtr = 0x0086400d;
21         rtr = 0x05f00000;
22     }

24     for (i=0; i<N_MB0CF; i++) {
25         /*
26          * 禁用内存控制器。
27      */
28         mtsdram0(mem_mcoptl, 0x00000000);

31         /*
32          *为 bank 0 设置 MB0CF。
33      */
34     mtsdram0(mem_mb0cf, mb0cf[i].reg);
35 mtsdram0(mem_sdtrl, sdtrl);
36 mtsdram0(mem_rtr, rtr);

38 udelay(200);

40 * 设置内存控制器选项寄存器，MOPT1。
41 * 将 DC_EN 设置为 '1'并将 BRD_PRF 设置为 '01' 以实现 16 字节突发
42 * 读/预取；
43 */
44 mtsdram0(mem_mcopt1, 0x8080000);

46 udelay(1000);
47 if (get_ram_size(0, mb0cf[i].size) == mb0cf[i].size) {
48 /*
49 * OK，检测到大小
50 */
51 return;
52
53 }
```

第一个操作是读取 405GP 上的引脚拉接情况，以确定 SDRAM 时钟的设计值。在这种情况下，我们可以看到兼容了两个可能的值：100MHz 和 133MHz。根据这一选择，选择了常量，这些常量将在稍后的函数中使用，用于在 SDRAM 控制器中设置正确的位。

从第 24 行开始，使用循环来为每种内存大小设置参数。目前 U-Boot 具有逻辑支持大小为 4MB、16MB、32MB、64MB 或 128MB 的单 bank 内存。这些大小定义在 `...cpu/ppc4xx/` 中的表里。

## D.4 总结

SDRAM 设备是非常复杂的。本附录提供了一个简单的示例，帮助你应对 SDRAM 控制器设置的复杂性。SDRAM 控制器执行着关键功能，必须经过正确设置。深入研究规格书并消化其中提供的信息是不可替代的。本附录引用的两个示例文档是一个极好的起点。

### D.4.1 建议阅读

AMCC 405GP 嵌入式处理器用户手册

AMCC Corporation

www.amcc.com/Embedded/

Micron Technology, Inc.

Synchronous DRAM MT48LC64M4A2 数据

http://download.micron.com/pdf/datasheets/dram/sdram/256MSDRAM.pdf

## 附录 E

## 开源资源

本附录为开源开发者汇集了许多实用资源。包含了源代码仓库和邮件列表。同时也列出了新闻和信息。

### 源代码仓库和开发者信息

Linux 开发集中在网络上的几个位置。以下是针对各种架构和项目最重要的位置列表：

- Linux 内核及许多相关项目的家园

www.kernel.org

- 主要内核 GIT 仓库

http://git.kernel.org/

- MIPS 相关的开发

www.linux-mips.org

- ARM 相关的 Linux 开发

www.arm.linux.org.uk

- 海量开源项目的主要聚集地

http://sourceforge.net

### 邮件列表

有数百甚至上千个邮件列表服务于 Linux 和源码开发的各个方面。这里有几个可以考虑的。在这些列表发布内容之前，请确保你熟悉邮件列表礼仪。

这些列表大部分都维护有可搜索的存档。这是你应该咨询的第一地方。在大多数情况下，你的问题已经被问过并回答了。

从这里开始阅读关于如何利用公共列表的建议：

- Linux 内核邮件列表常见问题解答

www.tux.org/lkml

- 提供各种 Linux 内核相关邮件列表的服务器

http://vger.kernel.org

- Linux 内核邮件：流量极高；仅限内核开发

http://vger.kernel.org/vger-kernel-lists.html#linux-kernel

### Linux 新闻与进展

这些网络资源可以帮助你跟踪开源社区快速变化的态势：

- LinuxDevices.com

www.linuxdevices.com

- PowerPC 新闻及其他信息

http://penguinppc

- Linux 最新新闻与进展

Linux Weekly News

www.lwn.net

### 开源法律洞察与讨论

该网站提供侧重于开源知识产权法的信息和教育：

- Open-Bar 网站

www.open-bar.org

## 附录 F

## BDI-2000 示例配置文件

```ini
; 用于 UEI PPC 5200 板板的 bdiGDB 配置文件
; 版本 1.0
; 版本 1.1 (增加了串口设置)
----------------------------------------------------------------------
; 4 MB Flash (Am29DL323)
; 128 MB Micron DDR DRAM
; NOP

[INIT]
; 初始化核心寄存器
WREG MSR 0x00003002 ;MSR : FP,ME,RI ;MBAR : 0x08000000 内部寄存器
WM32 0x08000000 0x00008000 ; 重置后的默认值，MBAR 位在 0x08000000
; 因为它的 POR 值为 0x00008000 (!)
```

WSPR 311 0x08000000 ; MBAR : 保存内部寄存器偏移量

WSPR 279 0x08000000 ;SPRG7: 保存内部内存偏移Reg: 279

```ini
; 初始化 CDM (时钟分发模块)
; 硬件重置配置 {
; ppc_llf_cfg[..4] = 01000b
XLB:Core -> 1:3
Core:f(VCO) -> 1:2
XLB:f(VCO) -> 1:6

xlb_clk_sel = 0 -> XLB_CLK=f(sys) / 4 = 132 MHz

sys_pllf_cfg_1 = 0 -> NOP
sys_pllf_cfg_0 = 0 -> f(sys) = 16x SYS_XTAL_IN = 528 MHz
}
```

```ini
; CDM 配置寄存器
WM32 0x0800020c 0x01000101
; 启用 DDR 
; ipb_clk_sel = 1 -> XLB_CLK / 2 (ipb_clk = 66 MHz)
; pci_clk_sel = 01 -> IPB_CLK/2
```

```ini
; CS0 Flash
WM32 0x08000004 0x0000ff00 ;CS0 起 = 0xff000000 - Flash 内存位于 CS0
WM32 0x08000008 0x0000ffff ;CS0 止 = 0xffff
```
