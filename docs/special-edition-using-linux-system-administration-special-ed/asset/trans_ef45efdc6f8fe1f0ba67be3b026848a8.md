

## 第六部分

### 附录 B

- Microtek Phantom 636（SANE microtek2）
- Mustek MFC-600S、MFC-600CD、MFC-800S（SANE mustek）
- Mustek MFS-6000CX、MFS-6000SP、MFS-8000SP、MFS-1200SP、MFS-12000CX（SANE mustek）
- Mustek SE-6000SP、SE-12000SP（SANE mustek）
- Mustek HT105、M800 手持扫描仪（scan-driver）
  - `ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz`
- Network Scan MM100
  - 相关信息可在 `http://thor.prohosting.com/~chrordig/Primax/index.html` 找到。驱动程序也可在此处找到。
- Nikon LS-20、LS-30、LS-1000（SANE Coolscan）
- Plustek OpticPro 4830P、OpticPro 4831P、OpticPro 9630P/PL、OpticPro 600P、OpticPro FBIII、OpticPro FBIV（SANE plustek）
  - SANE 驱动程序可在 `http://www.efn.org/~rick/plustek/` 找到。
- Primax Colorado Direct 300、Colorado Direct 600/30bit、Storm Totalscan
  - 相关信息可在 `http://thor.prohosting.com/~chrordig/Primax/index.html` 找到。驱动程序也可在此处找到。
- Siemens S9036（SANE agfafocus）
- Tamarack Artisan 6000C、8000C、12000C（SANE tamarack）
- UMAX Vista-S8、UC-1260、Mirage IIse、PL-II（SANE umax）
- Vobis HighScan（SANE microtek2）
- Voelkner Personal Scanner 64 手持扫描仪（scan-driver）
  - `ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz`
- Vuego 310S（SANE snapsan）

### 不支持的设备

- Acer 扫描仪。Acer 未发布任何编程信息。
- Escom 256（Primax Lector Premier 256）手持扫描仪
- Genius ScanMate/256、ScanMate/Color、EasyScan 手持扫描仪
- Mustek CG 8000 手持扫描仪
- Primax Colorado Direct 9600、Colorado 1200p、Colorado USB 19200
  - 相关信息可在 `http://thor.prohosting.com/~chrordig/Primax/index.html` 找到。
- Trust Ami Scan 手持扫描仪
- UMAX 并口扫描仪

## 其他硬件

### 业余无线电

支持以下卡及其他设备：

- 基于 KISS 的终端节点控制器
- Ottawa PI 卡
- Gracilis PacketTwin 卡
- 其他基于 Z8530 SCC 的卡
- 并口和串口 Baycom 调制解调器
- Soundblaster 卡
- 基于 Crystal 芯片组的声卡

### VESA 省电协议（DPMS）显示器

Linux 内核包含省电支持。使用 setterm 在 Linux 控制台中启用支持，使用 xset 在 X 下启用支持。

### 触摸屏

Metro-X X 服务器支持以下触摸屏控制器：

- Control Touch 串口触摸屏
  - `http://www.controltouch.com`
- EloGraphics
- Lucas Deeco
- MicroTouch

### 串口终端

旧终端只需连接到系统的串口，即可轻松在 Linux 下使用。支持以下所有终端：

- VT52
- VT100
- VT220
- VT320
- VT420

### 操纵杆

最新的 XFree86 发行版（3.3.x）以及 2.1.xx 和 2.2.xx 内核版本中提供了操纵杆支持。对于较旧的内核，以下链接很有用。

### 操纵杆驱动程序

有关操纵杆驱动程序的信息：http://atrey.karlin.mff.cuni.cz/~vojtech/joystick。FTP 存档可在 ftp://atrey.karlin.mff.cuni.cz/pub/linux/joystick 找到。

目前支持的操纵杆如下：

- Amiga 操纵杆（适用于 Amiga）
- 兼容 CH Flightstick Pro，带附加两个苦力帽和两个按钮
- DirectPad Pro 并口操纵杆接口（http://www.ziplable.com/dpadpro/index.html）
- FP Gaming Assassin 3D（http://www.fpgaming.com/portfolio/assn3d.html）
- 带 6 个和 8 个按钮的游戏手柄
- Genius Flight2000 Digital F-23（http://www.genius.kye.de/english/product/game.html）
- Gravis Blackhawk Digital（http://www.gravis.com/products/js_blackhawkdigital.html）
- Gravis GamePad Pro（http://www.gravis.com/products/gp_gamepadpro.html）
- Gravis Xterminator GamePad（http://www.gravis.com/products/xterminator.html）
- Logitech CyberMan 2（http://www.cyberman2.de）
- Logitech ThunderPad Digital（http://www.logitech.ch/Game+Controllers/ThunderPadDigital.html）
- Logitech WingMan Extreme Digital（http://www.logitech.ch/Game+Controllers/WingManExtremeDigital.html）
- MadCatz Panther（http://www.fpgaming.com/portfolio/panther.html）
- MadCatz Panther XL（http://www.fpgaming.com/portfolio/panthx1.html）
- Microsoft SideWinder 3D Pro（http://www.eu.microsoft.com/products/hardware/sidewinder/3Dpro/default.htm）
- Microsoft SideWinder Force Feedback Pro（http://www.eu.microsoft.com/products/hardware/sidewinder/force-feedback/default.htm）
- Microsoft SideWinder GamePad（http://www.eu.microsoft.com/products/hardware/sidewinder/gamepad/default.htm）
- Microsoft SideWinder Precision Pro（http://www.eu.microsoft.com/products/hardware/sidewinder/precision-pro/default.htm）
- 多系统操纵杆（Atari、Amiga、Commodore、Amstrad）
- 使用 0.8.0.2 硬件接口的多系统操纵杆
- Nintendo Entertainment System（以及兼容机——SVI、Pegasus……）游戏手柄
- PPDJ Lightning L4 游戏卡（http://www.ppdj.net）
- Sega Genesis（MegaDrive）游戏手柄
- Sega Master System 游戏手柄
- Sega Saturn 游戏手柄
- SNESKey 并口操纵杆接口
- Sony PlayStation 游戏手柄
- 具有 2、3 或 4 个轴以及最多 4 个按钮的标准操纵杆
- Super Nintendo Entertainment System 游戏手柄
- 兼容 ThrustMaster FCS，带附加苦力帽
- ThrustMaster Millennium 3D Inceptor（http://www.thrustmaster.com/products/millennium.htm）
- ThrustMaster Rage 3D（http://www.thrustmaster.com/products/rage3d.htm）
- TurboGraFX 并口操纵杆接口（http://www2.burg-halle.de/~schwenke/parport.html）

### 视频采集卡/帧捕捉器/电视调谐器

以下是支持电视调谐器的可用程序：

- BTTV http://www.thp.Uni-Koeln.DE/~rjkm/linux/bttv.html
- Xawtv
- Xtvscreen
- 支持所有带有 Bt848/Bt848a/Bt849/Bt878/Bt879 芯片和标准 Composite/S-VHS 输入的卡。通过软件中的 VBI 采样解码，支持图文电视和 Intercast（仅限 PAL）。
- Adlink 7200 数字 I/O 设备
  - ftp://metalab.unc.edu/pub/Linux/science/lab/adl7200-0.60.tar.gz
- Adlink 7300A 数字 I/O 设备
  - ftp://ftp.systemy.it/pub/develop/adl7300-0.04.tar.gz
- CMOS 视频会议套件。视频采集卡采用 Bt849 芯片组，配有 CCD 摄像头。
- Data Translation DT2803
- Data Translation DT2851 帧捕捉器
  - ftp://metalab.unc.edu/pub/Linux/apps/video/dt2851-2.01.tar.gz
- Data Translation DT3155
  - http://krusty.eecs.umich.edu/people/ncowan/linux/welcome.html
- Diamond DTV2000（基于 Bt848）
- Dipix XPG1000/FPG/PPMAPA（基于 TI C40 DSP）。支持大多数附加卡。
  - http://www.thp.Uni-Koeln.DE/~rjkm/linux/bttv.html 或 http://www.atlantek.com.au/USERS/www/linux/frame.html。驱动程序可在以下位置找到：
  - ftp://ftp.atlantek.com.au/pub/dipix.
- Epix SVM
- Epix Silicon Video MUX 系列视频帧采集板
  - http://www.ssc.com/lj/issue13/npc13c.html
- FAST Screen Machine II
  - ftp://metalab.unc.edu/pub/Linux/apps/video/ScreenMachineII.2.0.tgz
- Hauppauge Wincast TV PCI（基于 Bt848）
  - http://www.thp.Uni-Koeln.DE/~rjkm/linux/bttv.html
- Imaging Technology ITI/IC-PCI
  - ftp://ftp.gom-online.de/pub/IC-PCI/icpci-0.3.2.tar.gz
- ImageNation Cortex I
  - ftp://metalab.unc.edu/pub/Linux/apps/video/cortex.drv.1.1.tgz
- ImageNation CX100
  - ftp://metalab.unc.edu/pub/Linux/apps/video/cxdrv-0.86.tar.gz
- ImageNation PX500
  - ftp://ftp.systemy.it/pub/develop
- ImageNation PXC200
  - ftp://ftp.systemy.it/pub/develop
- Imaging Technology Inc. IC-PCI 帧采集板
  - http://gandalf.expmech.ing.tu-bs.de/pub/driver/icpci-0.2.0.tar.gz
- Matrix Vision MV-Delta
  - http://www.matrix-vision.de/
- Matrox Meteor
  - ftp://metalab.unc.edu/pub/Linux/apps/video/meteor-1.4a.tgz
- Matrox PIP-1024
  - http://www.powerup.com.au/~sobeyp/pip_tar.gz
- MaxiTV/PCI（基于 ZR36120）
  - ftp://metalab.unc.edu/pub/Linux/kernel/misc-cards/zr36120-971127.tgz
- Miro PCTV（基于 Bt848）
  - http://www.thp.Uni-Koeln.DE/~rjkm/linux/bttv.html
- MuTech MV1000 PCI
  - ftp://metalab.unc.edu/pub/Linux/apps/video/mv1000drv-0.33.tgz

