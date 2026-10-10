

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

## 附录 F

![](img/7a1144833e62564667e7dd9eb4c9f03d_536_0.png)

### BDI-2000 示例配置文件

```
; bdiGDB configuration file for the UEI PPC 5200 Board
; Revision 1.0
;Revision 1.1 (Added serial port setup)
--------------------------------------------------
; 4 MB Flash (Am29DL233)
; 128 MB Micron DDR DRAM
;
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
      ; bits 0-7: WaitP (try 0xff)
      ; bits 8-15: WaitX (try 0xff)
; bit 16: Multiplex or non-mux'ed (0x0 = non-muxed)
; bit 17: reserved (Reset value = 0x1, keep it)
; bit 18: Ack Active (0x0)
; bit 19: CE (Enable) 0x1
; bits 20-21: Address Size (0x11 = 25/6 bits)
; bits 22:23: Data size field (0x01 = 16-bits)
; bits 24:25: Bank bits (0x00)
; bits 26-27: WaitType (0x11)
; bits 28: Write Swap (0x0 = no swap)
; bits 29: Read Swap (0x0 = no swap)
; bit 30: Write Only (0x0 = read enable)
; bit 31: Read Only (0x0 = write enable)

; CS2 Logic Registers
WM32 0x80000014 0x0000e00e
WM32 0x80000018 0x0000efff

; LEDs:
; LED1 - bits 0-7
; LED2 - bits 8-15
; LED3 - bits 16-23
; LED4 - bits 24-31
; off = 0x01
; on = 0x02
; mm 0xe00e2030 0x02020202 1 (all on)
; mm 0xe00e2030 0x01020102 1 (2, on off)

WM32 0x8000308 0x0045b30 ; CS2 Configuration Register
; bits 0-7: WaitP (try 0xff)
; bits 8-15: WaitX (try 0xff)
; bit 16: Multiplex or non-mux'ed (0x0 = non-muxed)
; bit 17: reserved (Reset value = 0x1, keep it)
; bit 18: Ack Active (0x0)
; bit 19: CE (Enable) 0x1
; bits 20-21: Address Size (0x10 = 24 bits)
; bits 22:23: Data size field (0x11 = 32-bits)
; bits 24:25: Bank bits (0x00)
; bits 26-27: WaitType (0x11)
; bits 28: Write Swap (0x0 = no swap)
; bits 29: Read Swap (0x0 = no swap)
; bit 30: Write Only (0x0 = read enable)
; bit 31: Read Only (0x0 = write enable)

WM32 0x80000318 0x01000000 ; Master LFC Enable

; init SDRAM controller
; For the UEI PPC 5200 Board,
; Micron 46V32M16-7SE (8 MEG x 16 x 4 banks)
; 64 MB per Chip, for a total of 128 MB
; arranged as a single *space* (i.e. 1 CS)
; with the following configuration:
;   8 Mb x 16 x 4 banks
;   Refresh count: 8K (A0..12) 13 bits
;   Row addressing: 8K (A0..9) 10 bits
;   Bank Addressing: 4 (BA0..1) 2 bits
; Key Timing Parameters: (−75℉)
;     Clockrate (CL=2) 133 Mhz
;     DO Window 2.5 ns
;     Access Window: +/- 75 ns
;     DQS − DQ Skew: +0.5 ns
;     t(REFI): 7.8 us MAX
;
; Initialization Requirements (General Notes)
; The memory Mode/Extended Mode registers must be
; initialized during the system boot sequence. But before
; writing to the controller Mode register, the mode_en and
; cke bits in the Control register must be set to 1. After
; memory initialization is complete, the Control register
; mode_en bit should be cleared to prevent subsequent access
; to the controller Mode register.

; SDRAM init sequence
; 1) Setup and enable chip selects
; 2) Setup config registers
; 3) Setup TAP Delay

; Setup and enable SDRAM CS
WM32   0x8000034  0x000001a ;SDRAM CS0, 128MB @ 0x00000000
WM32   0x8000038  0x0800000 ;SDRAM CS1, disabled @ 0x08000000

WM32   0x8000108  0x73723930 ;SDRAM Config 1 Samsung
;    ; Assume CL=2
;    ; bits 0-3: srdr2zp in clocks (0x6)
;    ; bits 507: swt2rwp: in clocks -> Data sheet suggests
;    ;    0x3 for DDR (0x3)
;    ; bits 8-11: rd_latency -> for DDR 0x7
;    ; bits 13-15: act2rw -> 0x2
;    ; bit 16: reserved
;    ; bits 17-19: prereact -> 0x2
;    ; bits 20-23: ref2act -> 0x09
;    ; bits 25-27: wr_latency -> for DDR 0x03
;    ; bits 28-31: Reserved

WM32   0x800010c  0x46770000 ;SDRAM Config 2 Samsung
;    ; bits 0-3: bdr2zp -> for DDR 0x4
;    ; bits 4-7: bwt2rwp -> for DDR 0xf
;    ; bits 8-11: bdrd2wt -> 0x6
;    ; bits 12-15: burst_length -> 0x07 (bl - 1)
;    ; bits 16-13: Reserved

; Setup initial Tap delay
WM32  0x80000204  0x18000000  ; Start in the end of the range (24 = 0x18)
Samsung

WM32    0x80000104  0xf10f0f00 ;SDRAM Control (was 0xd14f0000)
; bit 0: mode_en (1=write)
; bit 1: cke  (MEM_CLK_EN)
; bit 2: ddr (DDR mode on)
; bit 3: ref_en (Refresh enable)
; bits 4-6: Reserved
; bit 7: hi_addr [XIA[4:7] as row/col
;   must be set to 11 'cuz we need 13 RA bits
;   for the Micron chip above
; bit 8: reserved
; bit 9: drive_rule - 0x0
; bit 10-15: ref_interval, see UM 0x0f
; bits 16-19: reserved
; bits 20-23: dgs_oel[3:0] (not sure)
; but I think this is req'd for DDR 0xf
; bits 24-28: Reserv'd
; bit 29:'1 = soft refresh
; bit 30 1 = soft_precharge
; bit 31: reserved

WM32   0x80000104  0xf10f0f02 ;SDRAM Control: precharge all
WM32   0x80000104  0xf10f0f04 ;SDRAM Control: refresh
WM32   0x80000104  0xf10f0f04 ;SDRAM Control: refresh

WM32   0x80000100  0x01800000  ; SDRAM Mode Samsung
reg 0x0
; bits 0-1: MEM_MRA - selects std or extended MODE
; bits 2-13: MEM_MA (see DDR DRAM Data sheet)
; bits 2-7: Operating Mode -> 0x0 = normal
; bits 8-10: CAS Latency (CL) -> Set to CL=2 for
DDR (0x2)
; bit 11: Burst Type: Sequential for PMS5200 ->
0x0
; bits 12-14: Set to 8 for RPC5200 -> 0x3
; bit 15: cmd = 1 for MODE REG WRITE

WM32    0x80000104  0x710f0f00 ;SDRAM Control: Lock Mode Register (was
0x514f0000)

; ********** Initialize the serial port ************
; Pin Configuration
WM32  0x00000b00  0x00008004  ; UART1

; Reset PSC
WB8   0x80002008  0X10  ; Reset - Select MRL

WM16  0x80002004  0   ; Clock Select Register - 0 enables both Rx &
Tx Clocks

WM32   0x80002040   0             ; STCR - UART Mode
WM32   0x80002000   0x13          ; Write MR1 (default after reset)
                                      ; 8-bit, no parity
WM32   0x80002000   0x07          ; Write MR2 (after MR1) (one stop bit)
WM32   0x80002018   0x0           ; Counter/Timer Upper Reg (115.2KB)
WM32   0x8000201c   0x12          ; Counter/Timer Lower Reg (divider = 18)

; Reset and enable serial port Rx/Tx
WM32   0x80002008   0x20
WM32   0x80002008   0x30
WM32   0x80002008   0x05

; define maximal transfer size
TSZ4   0x80000000   0x80003FFF   ; internal registers

; define the valid memory map
MMAP   0x00000000   0x07ffffff   ; Memory range for SDRAM
MMAP   0xF8000000   0x3ffffff    ; ROM space
MMAP   0xE0000000   0xE000eFFF   ; PowerPC logic
MMAP   0x80000000   0x8fffffff   ; Default MBAR
MMAP   0xC0000000   0XCfffFFFF   ; Linux Kernel
```

[TARGET]
CPUType    5200          ; CPU 类型
JTAGClock  0             ; 使用 16 MHz JTAG 时钟
WORKSPACE  0x80008000    ; 用于快速下载的地址空间
Wakeup     1000          ; 给予复位完成时间
Startup    reset
Memdelay   -2000         ; 额外的内存访问延迟
BootAddr   0xffe00100
RegList    All
DebugMode  Soft ; 或 hard
PowerUp    1000
WakeUp     500
MMU        XLAT
PTBase     0x000000f0

[HOST]
IP       192.168.1.9
Format   elf
Load     manual          ; 手动加载代码或在复位后自动加载
Prompt   uei>

[FLASH]
ChipType  AM29BX16      ; Flash 类型 (AM29F | AM29BX8 | AM29BX16 | I28BX8 | I28BX16)
ChipSize  0x00400000    ; 单个 flash 芯片的字节大小
Buswidth  16            ; flash 内存总线的位宽 (8 | 16 | 32)

