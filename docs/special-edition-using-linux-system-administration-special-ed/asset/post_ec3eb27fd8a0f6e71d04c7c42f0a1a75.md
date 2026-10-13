
The following modem is not supported:

- Aztech MDP3858 56.6 (PCI)

## Printers/Plotters

All printers and plotters connected to the parallel or serial port should work. Alas, some manufacturers have created Windows 95-only printers. Check “Linux-Incompatible Hardware” for Linux-compatible hardware.

- HP LaserJet 4 series—free-lj4, printing modes control program
  `ftp://metalab.unc.edu/pub/Linux/system/printing/free-lj4-1.1p1.tar.gz`
- BiTronics parallel port interface
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/misc/bt-ALPHA-0.0.1.module.patch.gz`
- Epson Stylus Color 850. Use Magicfilter with one of the following filters: `stylus800-filter`, `stylus_color_360dpi-filter`, or `stylus_color_720dpi-filter`.

### Ghostscript

Many Linux programs output PostScript files. Non-PostScript printers can emulate PostScript Level 2 using Ghostscript.

- Ghostscript
  `ftp://ftp.cs.wisc.edu/pub/ghost/aladdin/`

### Ghostscript 5.1 Supported Printers

- Apple Imagewriter
- Apple Dot Matrix printer
- Apple StyleWriter 2x00 (bjc600)
- Brother HL-660 (jet4)
- C. Itoh M8510
- Canon BubbleJet BJ10e, BJ20 (bj10e)
- Canon BubbleJet BJ100, BJ200, BJC-210 (B/W only), BJC-240 (B/W only), BJC-250 (B/W only), BJC-70 (B/W only) (bj200)
- Canon BubbleJet BJC-600, BJC-610, BJC-4000, BJC-4100 (B/W only), BJC-4200, BJC-4300, BJC-4400, BJC-4550, BJC-210, BJC-450, MultiPASS C2500, BJC-240, BJC-70 (bjc600)
- Canon Bubblejet BJC-800, BJC-7000 (bjc800)
- Canon Bubblejet BJC-610 (uniprint)
- Canon LBP-8II, LIPS III
- DEC LA50/70/75/75plus
- DEC LN03, LJ250 (decl250)
- Epson 9 pin, 24 pin, LQ series, AP3250
- Epson Stylus Color/Color II/400/500/600/800 (stcolor)
- Epson Stylus Color/Color II/500/600/800/1520 (uniprint)
- Fujitsu 3400,2400,1200
- HP 2563B
- HP DesignJet 650C
- HP DeskJet, DeskJet Plus (deskjet)
- HP Deskjet 500, Deskjet Portable (djet500)
- HP Deskjet 500C (deskjet)
- HP Deskjet 550C (uniprint)
- HP DeskJet 400/500C/520C/540C/690C/693C (cdj500)
- HP DeskJet 550C/560C/600/660C/660Cse/682C/683C/693C/694C/695C/850/870Cse (cdj550)
- HP DeskJet 850/855/870Cse/870Cxi/890C/672C/680/1100C (cdj850)
- HP DeskJet 550C/510/520/540C/693C printing black only (cdjmono)
- HP DeskJet 600 (lj4dith)
- HP DeskJet 600/870Cse, LaserJet 5/5L/6L (ljet4)
- HP DeskJet 600/1200C (pixl300)
- HP Deskjet 500/500C/510/520/540/550C/560C/850C/855C and other PCL3 printers
  `ftp://ftp.pdb.sni.de/pub/utilities/misc/hpdj-2.1.tar.gz`
- HP Deskjet 710, 720, 820 and 1000 series
  `http://www.hptech.com/ppa/`
- HP Paintjet (pjtest)
- HP Paintjet XL (pjxltest)
- HP PaintJet XL300 (pjxl300)
- HP LaserJet/Plus/II/III/4/5/6
- IBM 3853 Jetrinter color
- IBM Proprinter
- Imagen ImPress
- Lexmark Optra E+ (ljet4)
- Mitsubishi CP50 color
- NEC P6/P6+/P60
- NEC Pinwriter P2X (uniprint)
- NEC SuperScript 860 (jetplus)
- Okidata OL410ex LED (jet4)
- Okidata MicroLine 182
- Ricoh 4081/6000 (r4081)
- SPARCprinter
- StarJet 48 inkjet printer
- Tektronix 4693d color 2/4/8 bit
- Tektronix 4695/4696 inkjet plotter
- Xerox XES printers (2700, 3700, 4045, etc.)

### ALPHA, BETA DRIVERS

- Epson Stylus Color 440

## SCANNERS

For scanner support there is the package SANE (Scanner Access Now Easy). Information can be found at http://www.mostang.com/sane/. It can be downloaded from ftp://ftp.mostang.com/pub/sane/. This is a universal scanner interface and comes complete with documentation and several front ends and back ends.

More information on handheld scanners can be found at http://www.willamowius.de/scanner.html.

Many scanners also have their own scanner-specific software packages that include drivers.

### SUPPORTED

- A4 Tech AC 4096 / AS 8000P (a4scan)
  ftp://ftp.informatik.hu-berlin.de/pub/local/linux/a4scan/a4scan.tgz
- Adara Image Star I
  http://fb4-1112.uni-muenster.de/ffwd/
  ftp://fb4-1112.uni-muenster.de/pub/ffwd/mtekscan-0.2.tar.gz
- Conrad Personal Scanner 64, P105 handheld scanner (scan-driver)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz
- Epson GT-5500 (SANE epson)
- Epson GT-6000
  ftp://metalab.unc.edu/pub/Linux/apps/graphics/capture/ppic0.5.tar.gz
- Escom Image Scanner 256 (SANE umax)
- Fujitsu SCSI-2 scanners
  Contact Dr. G.W. Wettstein at greg%wind.UUCP@plains.nodak.edu
- Genius ColorPage-SP2
  http://fb4-1112.uni-muenster.de/ffwd/
  ftp://fb4-1112.uni-muenster.de/pub/ffwd/mtekscan-0.2.tar.gz
- Genius GS-B105G handheld scanner (gs105)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/gs105-0.0.1.tar.gz
- Genius GeniScan GS-4500, GS-4500A handheld scanners (gs4500)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/gs4500-2.0.tar.gz
- HighScreen Greyscan 256 handheld scanner (BW only) (gs4500)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/gs4500-2.0.tar.gz
- HP ScanJet II series SCSI
  ftp://metalab.unc.edu/pub/Linux/apps/graphics/capture/hpscanpbm-0.3a.tar.gz
- HP ScanJet IIc, IIcx, IIp, 3c, 4c, 4p, 5p, 5pse, plus
  http://www.tummy.com/xvscan/
- Linotype Hell Jade, Jade2 (SANE umax)
- Logitech Scanman+, Scanman 32, Scanman 256 handheld scanners (logiscan)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/logiscan-0.0.4.tar.gz
- Microtek ScanMaker E3, E6, II, IIXE, II and 35t models
  http://fb4-1112.uni-muenster.de/ffwd/
  ftp://fb4-1112.uni-muenster.de/pub/ffwd/mtekscan-0.2.tar.gz
  E3 and E6 scanners are also supported by http://www.tummy.com/xvscan/.
- Mustek M105 handheld scanner (scan-driver)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz
- Mustek HT800 Turbo, Matador 105, Matador 256 handheld scanners (scan-driver)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz
- Mustek Paragon 6000CX
  ftp://metalab.unc.edu/pub/Linux/apps/graphics/capture/muscan-2.0.6.taz
- Nikon Coolscan SCSI 35mm film scanner
  ftp://metalab.unc.edu/pub/Linux/apps/graphics/capture/coolscan-0.2.tgz
- Nikon AX-210 (SANE umax)
- Pearl 256 handheld scanner (scan-driver)
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz
- Polaroid DMC (SANE dmc)
- Vobis/Highscreen ScanBooster Premium (SANE umax)
- UMAX SCSI scanners
  ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/umax-0.5.5.tar.gz
- UMAX Vista S6, S6E, T630, Supervista S-12 (SANE umax)
- UMAX S-6E, S-6EG, S-12, S-12G (SANE umax)
- UMAX Astra 600S, 610S, 1200S, 1220S (SANE umax)
- UMAX UC 630, 840, 1200S, 1200SE (SANE umax)
- UMAX UG 80, 630 (SANE umax)
- UMAX PSD, Gemini D-16 (SANE umax)

> **Note**
>
> The Mustek drivers work only with GI1904 interface cards. Eric Chang, eric.chang@chrysalis.org, has created a patch to use them with IF960 interface cards.

### ALPHA, BETA DRIVERS

- Abaton Scan 300/S (SANE abaton)
- Abaton Scan 300/GS (SANE abaton)
- Agfa Focus, Focus II (SANE agfafocus)
- Agfa Focus Color, Focus Color Plus (SANE agfafocus)
- Agfa Focus Lineart (SANE agfafocus)
- Agfa Arcus II (SANE microtek)
- Agfa StudioScan II, IIsi (SANE microtek)
- Agfa SnapScan 300, 310, 600 (SANE snapscan)
- Apple Scanner, OneScanner, ColorOneScanner (SANE apple)
- Artec/Ultima AT3, AT6, AT12 (SANE artec)
- Artec A6000C+ (SANE artec)
- Canon CanoScan 300, CanoScan 600, CanoScan 2700F (SANE canon)
- Genius Colorpage-Vivid+
  - Information can be found on http://thor.prohosting.com/~chrordig/primax/index.html. The driver can also be found here.
- Genius GS-4000, ScanMate/32, ScanMate/GS handheld scanners (gs4500)
  - ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/gs4500-2.0.tar.gz
- HP ScanJet IIc, IIp, IIcx, 3c, 4c, 3p, 4p, 5p, 6100c, 6200c (SANE hp)
- HP PhotoSmart PhotoScanner (SANE hp)
- Kodak DC210 (SANE dc210)
- Kodak DC20, DC25 (SANE dc25)
- Microtek ScanMaker E2, E3, E6, II, IIG, IHR, IISP, III, 35t+, 600Z(S), 600G(S) (SANE microtek)
- Microtek ScanMaker E3plus, 330, 630, 636, X6 (SANE microtek2)
