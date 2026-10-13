
## SUPPORTED

### Common CD-ROM Drives

- SCSI CD-ROM drives
  - (From the CD-ROM HOWTO) Any SCSI CD-ROM drive with a block size of 512 or 2048 bytes should work under Linux; this includes the vast majority of CD-ROM drives on the market.
- EIDE (ATAPI) CD-ROM drives (IDECD)
  - Almost all double-, quad-, and six-speed drives are supported, including:
    - Mitsumi FX400
    - NEC-260
    - Sony 55E

### Proprietary CD-ROM Drives

- Aztech DAZ68-01A, Orchid CDS-3110, Okano/Wearnes CDD-110, Conrad TXC, CyCDROM CR520ie/CR540ie/CR940ie (AZTCD)
- Creative Labs CD-200 (SBPCD)
- Funai E2550UA/MK4015 (SBPCD)
- GoldStar R420 (GSCD)
- IBM External ISA (SBPCD)
- Kotobuki (SBPCD)
- Lasermate CR328A (OPTCD)
- LMS Philips CM 206 (CM206)
- Longshine LCS-7260 (SBPCD)
- Matsushita/Panasonic CR-521/522/523/562/563 (SBPCD)
- MicroSolutions Backpack parallel port drive (BPCD)
- Mitsumi CR DC LU005S (MCD/MCDX)
- Mitsumi FX001D/F (MCD/MCDX)
- Optics Storage Dolphin 8000AT (OPTCD)
- Sanyo CDR-H94A (SJCD)
- Sony CDU31A/CDU33A (CDU31A)
- Sony CDU-510/CDU-515 (SONYCD535)
- Sony CDU-535/CDU-531 (SONYCD535)
- Teac CD-55A SuperQuad (SBPCD)

### Alpha, Beta Drivers

- LMS/Philips CM 205/225/202
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/cdrom/lmscd0.4.tar.gz`
- NEC CDR-35D (old)
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/cdrom/linux-neccdr35d.patch`
- Sony SCSI multi-session CD-XA
  `ftp://tsx-11.mit.edu/pub/linux/patches/sony-multi-0.00.tar.gz`
- Parallel Port Driver
  `http://www.torque.net/linux-pp.html`

### Notes

All CD-ROM drives should work similarly for reading data. There are various compatibility problems with audio CD playing utilities (especially with newer low-end NEC drives). Some alpha drivers may not have audio support yet.

Early (single-speed) NEC CD-ROM drives may have trouble with currently available SCSI controllers.

PhotoCD (XA) is supported. The `hpcdtoppm` program by Hadmut Danisch converts PhotoCD files to the portable pixmap format. The program can be obtained from `ftp://ftp.gwdg.de/pub/linux/hpcdtoppm` or as part of the PBM utilities.

Also, reading video CD is supported in kernel series 2.1.3x and later. A patch is available for kernel 2.0.30.

Finally, most IDE CD-ROM Changers are supported.

### CD-Writers

Linux now supports many CD-Writers. For an up-to-date list of CD-Writers supported, check the CD-Writing mini-HOWTO at `http://metalab.unc.edu/LDP/HOWTO/CD-Writing-HOWTO.html`, check `http://www.shop.de/cgi-bin/winni/lsc.pl` or check `http://www.gwdg.de:8080/cgi-bin/winni/lsc.pl`. Execute `ftp://metalab.unc.edu/pub/Linux/utils/disk-management/` and `cdrecord` `http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html` can be used for writing CDs. The X-CD-Roast package for Linux is a graphical front-end for using CD writers. The package can be found at `ftp://metalab.unc.edu/pub/Linux/utils/disk-management/xcdroast-0.96d.tar.gz`.

- Grundig CDR 100 IPW
- HP CD-Writer+ 7100
- HP SureStore 4020i
- HP SureStore 6020es/i
- JVC XR-W2010
- Kodak PCD 225
- Mitsubishi CDRW-226
- Mitsumi CR-2600TE
- Olympus CDS 620E
- Philips CDD-5210/522, 2000, 2600, 3610
- Pinnacle Micro RCD-5020/5040
- Plextor CDR PX-24CS
- Ricoh MP 1420C
- Ricoh MP 6200S/6201S
- Sanyo CRD-R24S
- Smart and Friendly Internal 2006 Plus 2.05
- Sony CDU 920S/924/926S
- Taiyo Yuden EW-50
- TEAC CD-R50S
- WPI (Wearnes) CDR-632P
- WPI (Wearnes) CDRW-622
- Yamaha CDR-100
- Yamaha CDR-200/200t/200tx
- Yamaha CDR-400t/400tx

## Removable Drives

All SCSI drives should work if the controller is supported, including optical (MO), WORM, floptical, Bernoulli, Zip, Jaz, SyQuest, PD, and others.

Panasonic MO combines a CD-ROM drive and an optical removable disk. You must set a switch when configuring the kernel for both parts to work at the same time.

- Parallel port Zip drives
  `ftp://gear.torque.net/pub/`
- Parallel port Avatar Shark-250
  `http://www.torque.net/parport/`

Removable drives work like hard disks and floppies, just fdisk/mkfs and mount the disks. Linux provides drive locking if your drives support it. mtools can also be used if the disks are in MS-DOS format.

CD-R drives require special software to work. Read the CD-R Mini-HOWTO.

Linux supports both 512 and 1024 bytes/sector disks. Starting with kernel 2.1.32 Linux also supports 2048 bytes/sector. A patch to kernel 2.0.30 is available at http://liniere.gen.u-tokyo.ac.jp/2048.html.

The 2048 bytes/sector support is needed for

- Fujitsu magneto-optical disk drives M2513

Starting with pre-patch-2.0.31-3 IDE/ATAPI internal Zip drives, flopticals and PDs are supported.

- LS-120 floptical
- PD-CD

## Mouse Devices

### Supported

- Microsoft serial mouse
- Mouse Systems serial mouse
- Logitech Mouseman serial mouse
- Logitech serial mouse
- ATI XL Inport busmouse
- C&T 82C710 (QuickPort) (Toshiba, TI Travelmate)
- Microsoft busmouse
- Logitech busmouse
- PS/2 (auxiliary device) mouse

### Alpha, Beta Drivers

- Sejin J-mouse
  ```
  ftp://metalab.unc.edu/pub/Linux/kernel/patches/console/jmouse.1.1.70-jmouse.tar.gz
  ```
- MultiMouse—use multiple mouse devices as single mouse
  ```
  ftp://metalab.unc.edu/pub/Linux/X/system/misc/MultiMouse-1.0.tgz
  ```
- Microsoft IntelliMouse

### Notes

Touchpad devices such as Alps Glidepoint also work, so long as they’re compatible with another mouse protocol.

Newer Logitech mouse devices (except the Mouseman) use the Microsoft protocol and all three buttons do work. Even though Microsoft's mouse devices have only two buttons, the protocol allows three buttons.

The mouse ports on the ATI Graphics Ultra and Ultra Pro use the Logitech busmouse protocol. (See the Busmouse HOWTO for details.)

## Modems

All internal modems or external modems connected to the serial port should work. Alas, some manufacturers have created Windows 95-only modems. Check “Linux-Incompatible Hardware” for Linux-incompatible hardware. Furthermore, many flash upgradable modems only have flash programs for Win95/NT. These modems cannot be upgraded under Linux.

A small number of modems come with DOS software that downloads the control program at runtime. These normally are used by loading the program under DOS and doing a warm boot. Such modems are probably best avoided because you won't be able to use them with non-PC hardware in the future.

All PCMCIA modems should work with the PCMCIA drivers.

Fax modems need appropriate fax software to operate. Also be sure that the fax part of the modem supports Class 2 or Class 2.0. It seems to be generally true for any fax software on UNIX that support for Class 1.0 is not available.

An exception to this is the Linux efax program, which supports both Class 1 and Class 2 fax modems. In some cases there can be a few (minor) technical problems with Class 1 modems. If you have a choice it is recommended that you get a Class 2 modem.

- Digicom Connection 96+/14.4+—DSP code downloading program  
  `ftp://metalab.unc.edu/pub/Linux/apps/serialcomm/smdl-linux.1.02.tar.gz`
- Motorola ModemSURFR internal 56K. Add a couple of lines to RC.SERIAL to account for IRQ and ports if they are nonstandard.
- ZyXEL U-1496 series—ZyXEL 1.4, modem/fax/voice control program  
  `http://www.pe1chl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz`
- ZyXEL Elite 2864 series—modem/fax/voice control program  
  `http://www.pe1chl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz`
- ZyXEL Omni TA 128—modem/fax/voice control program  
  `http://www.pe1chl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz`

Also multimodem cards are supported by Linux.

- Moreton Bay RASTel multimodem card  
  Check `http://www.moreton.com.au/linux.htm` for Linux drivers.
