
## PART VI

### App B

- Microtek Phantom 636 (SANE microtek2)
- Mustek MFC-600S, MFC-600CD, MFC-800S (SANE mustek)
- Mustek MFS-6000CX, MFS-6000SP, MFS-8000SP, MFS-1200SP, MFS-12000CX (SANE mustek)
- Mustek SE-6000SP, SE-12000SP (SANE mustek)
- Mustek HT105, M800 handheld scanners (scan-driver)
  - `ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz`
- Network Scan MM100
  - Information can be found on `http://thor.prohosting.com/~chrordig/Primax/index.html`. The driver can also be found here.
- Nikon LS-20, LS-30, LS-1000 (SANE Coolscan)
- Plustek OpticPro 4830P, OpticPro 4831P, OpticPro 9630P/PL, OpticPro 600P, OpticPro FBIII, OpticPro FBIV (SANE plustek)
  - The sane driver can be found at `http://www.efn.org/~rick/plustek/`.
- Primax Colorado Direct 300, Colorado Direct 600/30bit, Storm Totalscan
  - Information can be found on `http://thor.prohosting.com/~chrordig/Primax/index.html`. The driver can also be found here.
- Siemens S9036 (SANE agfafocus)
- Tamarack Artisan 6000C, 8000C, 12000C (SANE tamarack)
- UMAX Vista-S8, UC-1260, Mirage IIse, PL-II (SANE umax)
- Vobis HighScan (SANE microtek2)
- Voelkner Personal Scanner 64 handheld scanner (scan-driver)
  - `ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/scan-driver-0.1.8.tar.gz`
- Vuego 310S (SANE snapsan)

### UNSUPPORTED

- Acer scanners. Acer is not releasing any programming information.
- Escom 256 (Primax Lector Premier 256) handheld scanner
- Genius ScanMate/256, ScanMate/Color, EasyScan handheld scanners
- Mustek CG 8000 handheld scanner
- Primax Colorado Direct 9600, Colorado 1200p, Colorado USB 19200
  - Information can be found on `http://thor.prohosting.com/~chrordig/Primax/index.html`.
- Trust Ami Scan handheld scanner
- UMAX parallel scanners

## Other Hardware

### Amateur Radio

The following cards and so forth are supported:

- KISS-based Terminal Node Controllers
- Ottawa PI card
- Gracilis PacketTwin card
- Other Z8530 SCC based cards
- Parallel and serial port Baycom modems
- Soundblaster cards
- Soundcards based on the Crystal chipset

### VESA Power Savings Protocol (DPMS) Monitors

Support for power savings is included in the Linux kernel. Use setterm to enable support in the Linux console, and xset to enable support under X.

### Touch Screens

The Metro-X X-server is supporting the following touch-screen controllers:

- Control Touch serial touch screen
  - `http://www.controltouch.com`
- EloGraphics
- Lucas Deeco
- MicroTouch

### Terminals on Serial Port

Old terminals can easily be used under Linux by connecting them to the serial port of your system. All of the following terminals are supported:

- VT52
- VT100
- VT220
- VT320
- VT420

### Joysticks

Joystick support is in the latest XFree86 distribution (3.3.x) and in kernel versions 2.1.xx and 2.2.xx. For older kernels the following links are useful.

### Joystick driver

For information on joystick drivers: http://atrey.karlin.mff.cuni.cz/~vojtech/joystick. An FTP archive can be found at ftp://atrey.karlin.mff.cuni.cz/pub/linux/joystick.

Currently supported joysticks are the following:

- Amiga joysticks on Amiga
- CH Flightstick Pro compatibles with additional two hats and two buttons
- DirectPad Pro parallel port joystick interfaces (http://www.ziplable.com/dpadpro/index.html)
- FP Gaming Assassin 3D (http://www.fpgaming.com/portfolio/assn3d.html)
- Gamepads with 6 and 8 buttons
- Genius Flight2000 Digital F-23 (http://www.genius.kye.de/english/product/game.html)
- Gravis Blackhawk Digital (http://www.gravis.com/products/js_blackhawkdigital.html)
- Gravis GamePad Pro (http://www.gravis.com/products/gp_gamepadpro.html)
- Gravis Xterminator GamePad (http://www.gravis.com/products/xterminator.html)
- Logitech CyberMan 2 (http://www.cyberman2.de)
- Logitech ThunderPad Digital (http://www.logitech.ch/Game+Controllers/ThunderPadDigital.html)
- Logitech WingMan Extreme Digital (http://www.logitech.ch/Game+Controllers/WingManExtremeDigital.html)
- MadCatz Panther (http://www.fpgaming.com/portfolio/panther.html)
- MadCatz Panther XL (http://www.fpgaming.com/portfolio/panthx1.html)
- Microsoft SideWinder 3D Pro (http://www.eu.microsoft.com/products/hardware/sidewinder/3Dpro/default.htm)
- Microsoft SideWinder Force Feedback Pro (http://www.eu.microsoft.com/products/hardware/sidewinder/force-feedback/default.htm)
- Microsoft SideWinder GamePad (http://www.eu.microsoft.com/products/hardware/sidewinder/gamepad/default.htm)
- Microsoft SideWinder Precision Pro (http://www.eu.microsoft.com/products/hardware/sidewinder/precision-pro/default.htm)
- Multisystem joysticks (Atari, Amiga, Commodore, Amstrad)
- Multisystem joysticks using 0.8.0.2 hw interface
- Nintendo Entertainment System (and clone—SVI, Pegasus ...) gamepads
- PPDJ Lightning L4 gamecard (http://www.ppdj.net)
- Sega Genesis (MegaDrive) gamepads
- Sega Master System gamepads
- Sega Saturn gamepads
- SNESKey parallel port joystick interfaces
- Sony PlayStation gamepads
- Standard joysticks with 2, 3, or 4 axes, and up to 4 buttons
- Super Nintendo Entertainment System gamepads
- ThrustMaster FCS compatibles with additional hat
- ThrustMaster Millennium 3D Inceptor (http://www.thrustmaster.com/products/millennium.htm)
- ThrustMaster Rage 3D (http://www.thrustmaster.com/products/rage3d.htm)
- TurboGraFX parallel port joystick interface (http://www2.burg-halle.de/~schwenke/parport.html)

### VIDEO CAPTURE BOARDS/FRAME GRABBERS/TV TUNERS

The following are programs available that support TV tuners:

- BTTV http://www.thp.Uni-Koeln.DE/~rjkm/linux/bttv.html
- Xawtv
- Xtvscreen
- All cards with Bt848/Bt848a/Bt849/Bt878/Bt879 and normal Composite/S-VHS inputs are supported. Teletext and Intercast support (PAL only) through VBI samples decoding in software.
- Adlink 7200 Digital I/O device
  - ftp://metalab.unc.edu/pub/Linux/science/lab/adl7200-0.60.tar.gz
- Adlink 7300A Digital I/O device
  - ftp://ftp.systemy.it/pub/develop/adl7300-0.04.tar.gz
- CMOS Video Conferencing Kit. The video capture card has a Bt849 chipset. It comes with a CCD camera.
- Data Translation DT2803
- Data Translation DT2851 Frame Grabber
  - ftp://metalab.unc.edu/pub/Linux/apps/video/dt2851-2.01.tar.gz
- Data Translation DT3155
  - http://krusty.eecs.umich.edu/people/ncowan/linux/welcome.html
- Diamond DTV2000 (based on Bt848)
- Dipix XPG1000/FPG/PPMAPA (based on TI C40 DSP). Most add-on cards are supported.
  - http://www.thp.Uni-Koeln.DE/~rjkm/linux/bttv.html or http://www.atlantek.com.au/USERS/www/linux/frame.html. The driver can be found at
  - ftp://ftp.atlantek.com.au/pub/dipix.
- Epix SVM
- Epix Silicon Video MUX series of video frame grabbing boards
  - http://www.ssc.com/lj/issue13/npc13c.html
- FAST Screen Machine II
  - ftp://metalab.unc.edu/pub/Linux/apps/video/ScreenMachineII.2.0.tgz
- Hauppauge Wincast TV PCI (based on Bt848)
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
- Imaging Technology Inc. IC-PCI frame grabber board
  - http://gandalf.expmech.ing.tu-bs.de/pub/driver/icpci-0.2.0.tar.gz
- Matrix Vision MV-Delta
  - http://www.matrix-vision.de/
- Matrox Meteor
  - ftp://metalab.unc.edu/pub/Linux/apps/video/meteor-1.4a.tgz
- Matrox PIP-1024
  - http://www.powerup.com.au/~sobeyp/pip_tar.gz
- MaxiTV/PCI (based on ZR36120)
  - ftp://metalab.unc.edu/pub/Linux/kernel/misc-cards/zr36120-971127.tgz
- Miro PCTV (based on Bt848)
  - http://www.thp.Uni-Koeln.DE/~rjkm/linux/bttv.html
- MuTech MV1000 PCI
  - ftp://metalab.unc.edu/pub/Linux/apps/video/mv1000drv-0.33.tgz
