

## 无槽

以下是在 Linux 中受支持的所有无槽端口的列表：

- SLIP/CSLIP/PPP（串行端口）
- EQL（串行 IP 负载均衡）
- PLIP（并行端口）（使用 LapLink 电缆或双向电缆）

## ARCnet

SuSE Linux 可与所有 ARCnet 卡配合使用。

## Token Ring

Linux 支持以下令牌环卡：

- 任何不使用 DMA 的 IBM 令牌环卡
- IBM Tropic 芯片组卡
- Madge TokenRing OCI 16/4 Mk2

## FDDI

Linux 支持以下 FDDI 卡：

- DEFEA（EISA）/ DEFPA（PCI）（内核 2.0.24 及更高版本）

## 业余无线电（AX.25）

Linux 支持以下业余无线电卡：

- Gracilis PackeTwin
- Ottawa PI/PI2
- 大多数基于 8530 的 HDLC 板

## 以太网

Linux 支持以下以太网卡：

- Racal-Interlan NI5210（82586 以太网芯片）（避免使用此卡。它不能与当前驱动程序正常工作。）
- Racal-Interlan NI6510（am7990 lance 芯片）（从内核 1.3.66 开始，支持超过 16MB RAM。）
- Racal-Interlan PCI 卡（AMD PC net 芯片 97c970）

## ISDN

Linux 支持以下 ISDN 卡：

- SpellCaster's Datacommu te/BRI, Telecommute/BRI（ISA）（sc）

## ATM

Linux 支持以下 ATM 适配器：

- Efficient Networks ENI155P-MF 155 Mbps ATM 适配器（PCI）

## 帧中继

Linux 支持以下帧中继卡：

- Sangoma S502 56K 帧中继卡

## 无线

Linux 支持以下无线技术：

- Proxim RangeLan2 7100（ISA）/ 630x（OEM mini-ISA）

## 声音卡

Linux 对大多数声卡有良好的支持。以下是受支持声卡的列表：

- 6850 UART MIDI
- Adlib（OPL2）
- Audio Excell DSP16
- Aztech Sound Galaxy NX Pro
- 基于 Crystal CS4232/CS4236（PnP）的卡
- ECHO-PSS 卡（Orchid SoundWave32, Cardinal DSP16）
- Ensoniq SoundScape
- Gravis Ultrasound
- Gravis Ultrasound 16 位采样子板
- Gravis Ultrasound MAX
- Gravis Ultrasound ACE（无 MIDI 端口和音频录制）
- Gravis Ultrasound PnP（带 RAM）
- Logitech SoundMan Games（SBPro，44KHz 立体声支持）
- Logitech SoundMan Wave（Jazz16/OPL4）
- Logitech SoundMan 16（PAS-16 兼容）
- MediaTriX AudioTriX Pro
- Media Vision Premium 3D（Jazz16）
- Media Vision Pro Sonic 16（Jazz）
- Media Vision Pro Audio Spectrum
- Media Vision Pro Audio Studio
- Microsoft Sound System（AD1848）
- OAK OTI-601D 卡（Mozart）
- OPTi 82C924/82C925 卡（使用 MSS 驱动程序和 isapnp 工具）
- OPTi 82C928/82C929 卡（MAD16/MAD16 Pro/ISP16/Mozart）
- OPTi 82C931 卡
- Sound Blaster
- Sound Blaster Pro
- Sound Blaster
- Sound Blaster 32/64/AWE（像 Sound Blaster 16 一样配置）
- Sound Blaster AWE63/Gold 和 16/32/AWE（PnP 卡需要使用 isapnptools 激活）
- Turtle Beach Wavefront 卡（Maui, Tropez）
- Wave Blaster（和其他子板）
- 基于 ESS Technologies AudioDrive 芯片的卡（688, 1688）
- AWE32/64 支持从内核系列 2.1.x 开始（请查阅 Marcus Brinkmann 的 SoundBlaster AWE mini-HOWTO 获取安装详情）
- MPU-401 MIDI
- Sound Blaster Live!
- MPU-401 MIDI（智能模式）
- PC 扬声器 / 并行端口 DAC
- Turtle Beach MultiSound/Tahiti/Monterey

## 调制解调器

Linux 支持所有内置调制解调器和连接到串行端口的外置调制解调器。唉，一些制造商创建了仅限 Windows 95 的调制解调器。少量调制解调器附带在运行时下载控制程序的 DOS 软件。在 DOS 下加载程序并执行热启动通常可以启用这些调制解调器的使用。不过最好还是避免使用此类调制解调器，因为以后你将无法在非 PC 硬件上使用它们。

所有 PCMCIA 调制解调器都应与 PCMCIA 驱动程序配合使用。

## 打印机

Linux 支持各种打印机。然而，一类打印机专为 MS Windows 设计，不能与 Linux 配合使用。以下是受支持打印机的列表：

- Apple Imagewriter
- C. Itoh M8510
- Canon BubbleJet BJI0e（bji0e）
- Canon BubbleJet BJC200, BJC-210（仅黑白）, BJC-240（仅黑白）（bj200）
- Canon BubbleJet BJC-600, BJC-610, BJC-4000, BJC-4100, BJC-450, MultiPASS C2500, BJC-240, BJ-70（bjc600）
- Canon BubbleJet BJC-800（bjc800）
- Canon LBP-8II, LIPS III
- DEC LA50/70/75/75plus
- DEC LN03, LJ250
- Epson 9 针, 24 针, LQ 系列, AP3250
- Epson Stylus Color/Color II/500/800（stcolor）
- HP 2563B
- HP DesignJet 650C
- HP DeskJet, DeskJet Plus（deskjet）
- HP DeskJet 500, DeskJet Portable（djet500）
- HP DeskJet 400/500C/540C/690C/693C（cdj500）
- HP DeskJet 550C/560C/600/660C/682C/683C/693C/850/870Cse（cdj550）
- HP DeskJet 850/870Cse/870Cxi/680（cdj850）
- HP DeskJet 500C/510/520/5540C/693C 仅打印黑色（cdjmono）
- HP DeskJet 600（lj4dith）
- HP DeskJet 600/870Cse, LaserJet 5/5L（ljet4）
- HP DeskJet 500/500C/510/520/540/550C/560C/850C/855C
- HP DeskJet 720, 820 和 1000 系列
- HP PaintJet XL300, DeskJet 600/1200C/1600C（pjxl300）
- HP LaserJet/Plus/II/III/4
- HP PaintJet/XL
- IBM Jetprinter 彩色
- IBM Proprinter
- Imagen ImPress
- Mitsubishi CP50 彩色
- NEC P6/P6+/P60
- Oki OL410ex LED（jet4）
- Okidata MicroLine 182
- Ricoh 4081/6000（r4081）
- SPARCprinter
- StarJet 48 喷墨打印机
- Tektronix 4693d 彩色 2/4/8 位
- Tektronix 4695/4696 喷墨绘图仪
- Xerox XES 打印机（2700, 3700, 4045 等）
- Canon BJC600/800 彩色打印机

## 扫描仪

Linux 使用 SANE 软件包支持扫描仪。该软件包支持以下扫描仪：

- A4 Tech AC 4096 / AS 8000P
- Adara Image Star I
- Conrad Personal Scanner 64, P105 手持扫描仪
- Epson GT6000
- Fujitsu SCSI-2 扫描仪（联系 Dr. G.W. Wettstein）
- Genius ColorPage-SP2
- Genius GS-B105G 手持扫描仪
- Genius GeniScan GS4500, GS4500A 手持扫描仪
- HighScreen Greyscan 256 手持扫描仪
- HP ScanJet II 系列 SCSI
- HP ScanJet IIc, IIcx, IIp, 3c, 4c, 4p, 5p, 5pse, plus
- Logitech Scanman+, Scanman 32, Scanman 256 手持扫描仪
- Microtek ScanMaker E3, E6, II, IIXE, III 和 35t 型号
- Mustek M105 手持扫描仪
- Mustek HT800 Turbo, Matador 105 和 Matador 256 手持扫描仪
- Mustek Paragon 6000CX
- Nikon Coolscan SCSI 35mm 胶片扫描仪
- Pearl 256 手持扫描仪
- UMAX SCSI 扫描仪
- Genius GS-4000, ScanMate/32, ScanMate/GS 手持扫描仪
- Mustek HT105, M800 手持扫描仪
- Voelker Personal Scanner 64 手持扫描仪

以下扫描仪不受支持：

- Acer 扫描仪（Acer 未发布任何编程信息。）
- Escom 256（Primax Lector Premier 256）手持扫描仪
- Genius ScanMate/256, EasyScan 手持扫描仪
- Mustek CG8000 手持扫描仪
- Trust AmiScan 手持扫描仪

## 业余无线电

Linux 支持以下卡：

- 基于 KISS 的终端节点控制器
- Ottawa Pi 卡
- Gracilis PacketTwin 卡
- 其他 Z8530 SCC 基于卡
- 并行和串行端口 Baycom 调制解调器
- Sound Blaster 卡
- 基于 Crystal 芯片组的声卡

## 串行端口上的终端

旧终端可以通过将其连接到系统的串行端口在 Linux 下轻松使用。以下终端受支持：

- VT52
- VT100
- VT220
- VT320
- VT420

## 操纵杆

操纵杆支持存在于最新的 XFree86 发行版（3.3.x）以及内核版本 2.2.xx 及以上版本中。

## 视频采集板/帧 grabber/电视调谐器

Linux 对以下视频采集卡提供支持：

- CMOS 视频会议套件（视频采集卡具有 BT849 芯片组。它附带 CCD 相机。）
- Data Translation DT2803
- Data Translation DT2851 帧 grabber
- Data Translation DT3155
- Diamond DTV2000（基于 BT848）
- Dipix XPG1000/FPG/PPMAPA（基于 TI C40 DSP）
- Epix SVM
- Epix Silicon Video MUX 系列视频帧抓取板
- FAST Screen Machine II
- Hauppage Wincast TV PCI（基于 BT848）
- Imaging Technology ITI/IC-PCI
- ImageNation Cortex I
- ImageNation CX100
- ImageNation PX500（正在进行中）（请询问当前状态。）
- Imaging Technology, Inc. IC-PCI 帧 grabber 板
- Matrox Meteor
- Matrox PIP-1024
- MaxiTV/PCI（基于 ZR36120）
- Miro PCTV（基于 BT848）
- MuTech MV1000 PCI
- MuTech MV200
- Philips PCA10TV（不再生产）
- Pro Movie Studio
- Quanta WinVision B&W 视频采集卡
- Quickcam
- Sensus 700

