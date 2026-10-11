
PowerPC 405GP 用户手册描述了表 D-3 中 SDRAM 时序寄存器的字段。

#### 表 D-3
405GP SDRAM 时序寄存器字段

| 字段 | 值 | 注释 |
| :--- | :--- | :--- |
| CAS 延迟 (CASL) | 0x1 | SDRAM CAS 延迟。此值直接来自 SDRAM 芯片规格。它是芯片在发出读取命令（CAS 信号）到数据在数据总线上可用之间所需的时钟周期延迟。在本例中，0x1 代表两个时钟周期，如 405GP 用户手册所示。 |
| 预充电命令到下一次激活 (PTA) | 0x1 | SDRAM 预充电命令使给定的行失效。相比之下，激活命令使给定的行可用于随后的访问，例如在突发周期期间。此时序参数强制执行预充电到后续激活周期之间的最小时间间隔，并由 SDRAM 芯片决定。正确的值必须从 SDRAM 芯片规格中获取。在本例中，0x1 代表两个时钟周期，如 405GP 用户手册中确定。 |
| 读/写到预充电命令最小值 (CTP) | 0x2 | 此时序参数强制执行给定的 SDRAM 读或写命令到后续预充电命令之间的最小时间延迟。正确的值必须从 SDRAM 芯片规格中获取。在本例中，0x2 代表三个时钟周期，如 405GP 用户手册中确定。 |
| SDRAM 命令提前量 (LDF) | 0x1 | 此时序参数强制执行地址或命令周期到银行选择周期断言之间的最小时间延迟。正确的值必须从 SDRAM 芯片规格中获取。在本例中，0x1 代表两个时钟周期，如 405GP 用户手册中确定。 |

U-Boot 示例（清单 D-1）中配置的最后一个时序参数是刷新时序寄存器值。此寄存器需要单个字段来确定由 SDRAM 控制器执行的刷新间隔。表示该间隔的字段被视为以 SDRAM 时钟频率运行的简单计数器。在此例中，我们假设 SDRAM 时钟频率为 100MHz。在我们的示例中编程到此寄存器中的值是 `0x05f0_0000`。根据 PowerPC 405GP 用户手册，我们确定这将产生每 15.2 微秒一次的刷新请求。与其他时序参数一样，此值由 SDRAM 芯片规格决定。

典型的 SDRAM 芯片需要对每一行执行一次刷新周期。每行必须在制造商规定的最小时间内完成刷新。在 D.4.1 节“延伸阅读建议”中引用的芯片中，制造商规定每 64 毫秒内必须刷新 8,192 行。为了满足此特定设备的规格，这要求每 7.8 微秒生成一个刷新周期。

### D.4 总结

SDRAM 设备相当复杂。本附录提出了一个非常简单的示例，以帮助你理解 SDRAM 控制器配置的复杂性。SDRAM 控制器执行关键功能，必须正确设置。深入研究规格并消化所呈现的信息是没有替代方案的。本附录中引用的两份示例文档是极好的起点。

#### D.4.1 延伸阅读建议

- AMCC 405GP 嵌入式处理器用户手册
  - AMCC 公司
  - www.amcc.com/Embedded/

- Micron Technology, Inc.
  - Synchronous DRAM MT48LC64M4A2 数据表
  - http://download.micron.com/pdf/datasheets/dram/sdram/256MSDRAM.pdf

# 附录 E

![](img/7a1144833e62564667e7dd9eb4c9f03d_532_0.png)

## 源代码仓库和开发者信息

网络上有几个位置专注于 Linux 开发。以下是各种架构和项目的最重要网站列表：

- 主要内核源代码树
  - www.kernel.org
- 主要内核 GIT 仓库
  - www.kernel.org/git
- PowerPC 相关的开发和邮件列表
  - http://ozlabs.org/
- MIPS 相关开发
  - www.linux-mips.org
- ARM 相关的 Linux 开发
  - www.arm.linux.org.uk
- 大量开源项目的主要家园
  - http://sourceforge.net

## 邮件列表

数百甚至数千个邮件列表服务于 Linux 和开源开发的各个方面。以下是一些值得考虑列表。确保在发布到这些列表之前熟悉邮件列表礼仪。

大多数这些列表维护可搜索的存档。这是你应该咨询的第一个地方。在绝大多数情况下，你的问题已经被提问并回答了。从这里开始阅读，获取关于如何最好地使用公共邮件列表的建议：

- Linux 内核邮件列表 FAQ
  - www.rux.org/lkml
- 服务于各种 Linux 内核相关邮件列表的列表服务器
  - http://vger.kernel.org
- Linux 内核邮件列表——非常高的流量，仅限内核开发
  - http://vger.kernel.org/vger-lists.html#linux-kernel

## Linux 新闻与发展

许多新闻网站都值得偶尔浏览。以下是一些更受欢迎的网站列表。

- LinuxDevices.com
  - www.linuxdevices.com
- PowerPC 新闻及其他信息
  - http://penguinppc.org
- 通用 Linux 新闻与发展动态
  - www.lwn.net

## 开源洞察与讨论

以下公共网站包含有关开源法律问题的有用信息和教育内容。

- www.open-bar.org

# 附录 F

![](img/7a1144833e62564667e7dd9eb4c9f03d_536_0.png)

### BDI-2000 示例配置文件

```
; bdiGDB configuration file for the UEI PPC 5200 Board

; Revision 1.0

;Revision 1.1 (Added serial port setup)

--------------------------------------------------

; 4 MB Flash (Am29DL233)
; 128 MB Micron DDR DRAM

[INIT];

; init core register
WR$R  MSR   0x00003002  ;MSR : FP,ME,RI
WR$2  0x80000000  0x00808000  ;MBAR: internal registers at 0x80000000
         ; Default after RESET, MBAR sits at 0x80000000
         ; because it's FOR value is 0x0000_8000 ()
WSFR   311   0x80000000  ; MBAR: save internal register offset
                        ; SPR311 is the MBAR in G2_LE
WSFR   279   0x80000000  ;SPRG7: save internal memory offsetReg: 279
; Init CDM (Clock Distribution Module)
; Hardware Reset config {
;  ppc_pll_cfg0.4]= 01000b
;   XLB:Core -> 1:3
;   Core:f(WCO)-> 1:2
;   XLB:f(WCO)-> 1:6
;
; xlb_clk_sel = 0 -> XLB_CLK=f(sys)/ 4 = 132 Mhz
;
;  sys_pll_cfg_1 = 0 -> NOP
; sys_pll_cfg_0 = 0 -> f(sys) = 16x SYS_XTAL_IN = 528 Mhz
;
;
; CDM Configuration Register
WR$2  0x8000200c  0x01000101
      ; enable DDR Mode
      ; ipb_clk_sel = 1 -> XLB_CLK/ 2 (ipb_clk = 66 Mhz)
      ; pci_clk_sel = 01 -> IPB_CLK/2
; CS0 Flash
WR$2  0x80000004  0x0000fe00  ;CS0 start = 0xff000000 - Flash memory is on
CS0
WR$2  0x80000008  0x0000ffff  ;CS0 stop = 0xffffff
; IPBI Register and Wait State Enable
WR$2  0x80000054  0x00050001  ;CSB: enable CS0, disable CSBOOT,
                              ;Wait state enable\,
                              ; CS2 also enabled
WM$2  0x8000300  0x0004d530  ;BOOT ctrl
```
