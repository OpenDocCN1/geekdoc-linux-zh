
- Canon BubbleJet BJ600, BJ610, BJ4000, BJ4100, BJ450, MultiPass C2500, BJ240, BJ70 (`bj600`)
- Canon BubbleJet BJ800 (`bj800`)
- Canon LBP-811, LIPS III
- DEC LA50/70/75/75plus
- DEC LN03, LJ250
- Epson 9针, 24针, LQ 系列, AP3250
- Epson Stylus Color/Color II/500/800 (`color`)
- HP 2563B
- HP Designjet 650c
- HP Deskjet, Deskjet Plus (`deskjet`)
- HP Deskjet 500, Deskjet Portable (`deskjet`)
- HP Deskjet 400/500C/540C/693C (`cdj500`)
- HP Deskjet 550C/560C/600C/660C/682C/693C/870C/870se (`cdj550`)
- HP Deskjet 850/870ce/870C (`cd85`)
- HP Deskjet 500C/510C/520C/5540C/693C (`cdjmono`)
- HP Deskjet 600 (`j4`)
- HP Deskjet 600 (`j44d`)
- HP Paintjet 600/870ce, 5/L (`ij4`)
- HP Paintjet 500C/510C/520C/540/550/560C/840C/850C/855C
- HP Paintjet 300,1200C/1600C (`pj300`)
- HP LaserJet/Plus/II/III
- HP Paintjet/XL

## 附录 C Linux 硬件性 HOWTO

- IBM Jetprinter
- Imagen ImPress
- Mitsubishi CP50 颜色
- NEC P6+/P60
- Oki OL410ex (`jet4`)
- Okidata MicroLine 182
- Ricoh 4081/600 (`r4081`)
- SPARCprinter
- StarJet 48 喷墨
- Tektronix 4693 颜色 2/4
- Tektronix 4695/4696 喷墨
- Xerox ES 打印机 (2700, 3700, 4045, 等)
- Canon BJC600/800 颜色

`ftp://petole.imag.fr/pub/postscript/bjc00/`

## 扫描仪

- 扫描仪有一个 SANE (Scanner Access) 软件包。可以在 `http://www.mostang.com/sane/` 或 `ftp://mostang.com/pub/sane/` Find信息。这是一个通用扫描仪。它带有多个前端和后端。关于手持扫描仪的更多信息可以在 `http://swt.windik.uni-hamburg.de/~illamo/scanner` 。

## 支持的

- A4 Tech AC 4096 / AS 8000 `ftp://informatik.hu-berlin.de/pub/local/a4scan/a4scan.tgz`
- Adara Image Star I `http://www.torque.net/shark.html` (注：此处原文网址与描述不符，保留原文)
- 扫描仪 4 喷墨 (`j4`)
- 600 (`j4`)
- 扫描仪 4 喷墨 (`j4`)
- 扫描仪 600 (`j44d`)
- Deskjet 600 (`j4`)
- HP LaserJet 4 系列 - free-lj4 打印程序

`http://sunsite.unc.edu/pub/Linux/system/printing/free-lj4-1.1.tar.gz`

## Ghostscript

- BiTronics 并行口

`http://sunsite.unc.edu/pub/Linux/patches/misc/ALPHA-0.1.patch.gz`

- 许多 Linux 程序输出 PostScript 文件。非 PostScript 打印机可以使用 Ghostscript 模拟 PostScript Level 2。
- Ghostscript 打印机

`ftp://cs.wisc.edu/pub/aladdin/`

- Ghostscript 打印机
- Apple Imagewriter
- Itoh M8510
- Canon BubbleJet BJ10e (`bj10e`)
- Canon BubbleJet BJ200, BJ210 (仅限黑), BJ240 (仅限黑) (`bj200`)
- Canon BubbleJet BJ600, BJ610, BJ4000, BJ4100, BJ450, MultiPass C2500, BJ240, BJ70 (`bj600`)
- Canon BubbleJet BJ800 (`bj800`)
- Canon LBP-811, LIPS III
- DEC LA50/70/75/75plus
- DEC LN03, LJ250
- Epson 9针, 24针, LQ 系列, AP3250
- Epson Stylus Color/Color II/500/800 (`color`)
- HP 2563B
- HP Designjet 650c
- HP Deskjet, Deskjet Plus (`deskjet`)
- HP Deskjet 500, Deskjet Portable (`deskjet`)
- HP Deskjet 400/500C/540C/693C (`cdj500`)
- HP Deskjet 550C/560C/600C/660C/682C/693C/870C/870se (`cdj550`)
- HP Deskjet 850/870ce/870C (`cd85`)
- HP Deskjet 500C/510C/520C/5540C/693C (`cdjmono`)
- HP Deskjet 600 (`j4`)
- HP Deskjet 600 (`j44d`)
- HP Paintjet 600/870ce, 5/L (`ij4`)
- HP Paintjet 500C/510C/520C/540/550/560C/840C/850C/855C
- HP Paintjet 300,1200C/1600C (`pj300`)
- HP LaserJet/Plus/II/III
- HP Paintjet/XL

# 不支持

- Escom 256 (Primax Lector 256) 手持式扫描仪
- Genius ScanMate/256, EasyScan 手持式扫描仪
- Mustek CG8000 手持式扫描仪
- Trust Ami Scan 手持式扫描仪

# 其他硬件

## VESA 节能协议 (DPMS) 显示器

- Linux内核包含了节能支持。只需使用 `setterm` 即可启用支持。

# 触摸屏

- Metro-X X-server 支持以下触摸屏：
- Carrol Touch 串口触摸屏。`http://www.carrolltouch.com`

# 串口终端

- 将旧终端通过连接到系统的串口端口，可以轻松地在 Linux 下使用。至少支持以下终端：
- VT52
- VT100
- VT220
- VT320
- VT420

# 摇杆

最新的 XFree86 发行版 (3.3.x) 和内核版本 2.1.xx 已支持摇杆。对于旧版本的内核，下面的链接非常有用。
- 摇杆驱动 `ftp://sunsite.unc.edu/pub/Linux/kernel/patches/console/joystick-0.8.0.tgz`
- 摇杆驱动（模块） `ftp://sunsite.unc.edu/pub/Linux/kernel/patches/console/joystickfixed.tgz`

# 视频采集卡 / 帧采集器 / 电视调谐器

- 有几个支持电视调谐器的程序。这些是：
- BTTV `http://www.thp.Uni-Koeln.DE/-rjkm/linux/bttv.html`
- Xawtv

# 其他硬件

- Data Translation DT2803
- Data Translation DT2851 帧采集卡

`ftp://sunsite.unc.edu/pub/Linux/apps/video/dt2851-2.01.tar.gz`

- Data Translation DT3155 `http://krusty.eecs.umich.edu/people/ncowan/linux/welcome.html`
- Diamond DT2000 (基于 IT BT848)
