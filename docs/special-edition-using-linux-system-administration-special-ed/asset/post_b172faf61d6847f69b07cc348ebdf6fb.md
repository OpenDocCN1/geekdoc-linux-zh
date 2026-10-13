
## ATA/IDE CD-ROM ADAPTERS

You should at least have kernel 1.3.72.

- Argosy EIDE CD-ROM (ide_cs)
- Caravelle CD-36N (ide_cs)
- CNF CARDport CD-ROM (ide_cs)
- Creative Technology CD-ROM (ide_cs)
- Digital Mobile Media CD-ROM (ide_cs)
- EXP CD940 CD-ROM (ide_cs) (Some work, some do not)
- EXP Traveler 620 CD-ROM (ide_cs)
- H45 Technologies Quick 2x CD-ROM (ide_cs)
- H45 Technologies QuickCD 16X (ide_cs)
- IBM Max 20X CD-ROM (ide_cs)
- IO DATA CDP-TX4/PCIDE, CDP-TX6/PCIDE, CDV-HDN6/PCIDE (ide_cs)
- IO DATA CDP-TX10/PCIDE, CDP-FX24/CBIDE, MOP-230/PCIDE (ide_cs)
- IO DATA HDP-1G/PCIDE, HDP-1.6G/PCIDE (ide_cs)
- Microtech International MicroCD (ide_cs)
- Microtech Mii Zip 100 (ide_cs)
- NOVAC NV-CD410 (ide_cs)
- Sony PCGA-CD5 CD-ROM (ide_cs)
- TEAC IDE Card/II (ide_cs)

## MULTIFUNCTION CARDS

You should at least have kernel 1.3.73.

- 3Com 3c562, 3c562B/C/D, 3c563B/C/D (3c589_cs)
- 3Com Megahertz 3CCEM556, 3CXEM556, 3CCEM556B (3c589_cs)
- 3Com Megahertz 3CCFEM556 (3c574_cs)
- 3Com 3CCFEM556B (3c575_cb, ethernet only!!)
- Accton UE2218 (pcnet_cs)
- ActionTec ComNet 33.6 (pcnet_cs)
- AnyCom Fast Ethernet + 56K Combo (pcnet_cs)
- Asus combo card (pcnet_cs)
- Billionton LMSL7-10B (pcnet_cs)
- Compaq Microcom CPQ550 Modem + 10/100 LAN (xirc2ps_cs)
- Dayna Communicard (pcnet_cs)
- D-Link DME336T, DMF560TX (pcnet_cs)
- Gateway Telepath Combo (smc91c92_cs)
- Grey Cell GCS3400 (pcnet_cs)
- GVC LAN modem (pcnet_cs)
- IBM Home and Away, Home and Away 28.8 (pcnet_cs)
- IO DATA PCMCIA-336T (pcnet_cs)
- Intel EtherExpress PRO/100 LAN/Modem (xirc2ps_cs)
- Linksys LANmodem 28.8 (PCMLM28), 33.6 (PCMLM336) (pcnet_cs)
- Linksys EtherFast LANmodem 56K (PCMLM56) (pcnet_cs)
- Megahertz/U.S. Robotics EM1144, EM3288, EM3336 (smc91c92_cs)
- Motorola Mariner (smc91c92_cs)
- Motorola Marquis (3c589_cs)
- Ositech Jack of Diamonds, Jack of Hearts (smc91c92_cs)
- Ositech Jack of Spades CardBus (epic_cb, experimental, requires kernel 2.2.x or later)
- PREMAX LAN modem (pcnet_cs)
- Psion V.34 Gold Card (pcnet_cs)
- Psion Gold Card Netglobal 56K+10Mb (pcnet_cs)
- Rover ComboCard 33.6 (pcnet_cs)
- TDK 3000/3400/5670 (pcnet_cs)
- Telecom Device SuperSocket LM336 (pcnet_cs)
- Xircom CreditCard CEM28, CEM33, CEM56 (xirc2ps_cs)
- Xircom RealPort REM10BT, REM56G-100 (xirc2ps_cs)
- Xircom RBEM56G-100BTX, CEM56G-100BTX (tulip_cb, experimental, requires kernel 2.2.x or later)

## ATA/IDE CARD DRIVES

These card drives are supported starting with kernel 1.3.72. Both Flash-ATA cards and rotating-media cards are supported. The very old Western Digital 40MB drives are not supported because they do not conform to the PCMCIA ATA specifications.

## ATA/IDE INTERFACE CARDS

- Archos Zip100 MiniDrive (ide_cs)
- Microtech International XpressDock (ide_cs)
- DataStor Technology PCMCIA ATA/ATAPI Card (ide_cs)
- Creo DNBoy (ide_cs)
- GREYSTONE DD-25 (ide_cs)
- Shining Technology CitiDISK 250PE (ide_cs)
- Sicon Peripheral Micro Mate (ide_cs)

## PARALLEL PORT CARDS

See the appendix on supported parallel port devices.

## MISCELLANEOUS CARDS

- GemPlus GPR400 Smart Card Reader http://www.linuxnet.com/smartcard/code.html (Wolf Geldmacher wgeldmacher@...)
- IBM Smart Capture (iscc_cs) (Koji Okamura oka@ec.kyushu-u.ac.jp)
- IBM Ethernet (cs89x0_cs) (Danilo Beuche danilo@cs.uni-magdeburg.de)
- National Instruments DAQcard700 ftp://ftp.rtlinux.org/pub/rtlinux/sources/DAQcard700/ (Oleg Subbotin)
- Netwave AirSurfer Plus (asplus_cs) http://ipoint.vlsi.uiuc.edu/wireless/asplus.html (Jay Moorman jmoorma@uiuc.edu)
- New Media Bus Toaster SCSI (new version) (sym53c500_cs) (Tim Corner tcorner@via.at)
- New Media BASICS SCSI (sym53c500_cs) (Tim Corner tcorner@via.at)
- Nokia/InTalk ST-500A http://www.absoval.com/linux-wlan (Mark Mathews mark@absoval.com)
- Proxim RangeLAN2 and Symphony wireless LAN cards http://www.komacke.com/distribution.html (Dave Koberstein davek@komacke.com)
- RATOC REX-9590 (iscc_cs) (Koji Okamura oka@nanotsu.kobe-u.ac.jp)
- Samsung MagicWave SWL-1000N http://www.absoval.com/linux-wlan (Mark Mathews mark@absoval.com)
- Silicom SPE ethernet, SEM EtherModem, SES EtherSerial http://www.silicom.co.il/linux.htm
- SIMA TECH SCSI9000 (sym53c500_cs) (Tim Corner tcorner@via.at)
- SST 5136-DN-PC DeviceNet Interface (ss5136_cs) http://www.gnofn.org/~marksu/ss5136man.html
- Trimble Mobile GPS (uses serial/modem driver)
- Y-E Data FlashBuster floppy drive adapter (floppy_cs) (David Bateman dbateman@eng.uts.edu.au)
- Zoom Telephonics ZoomAir 4000 http://www.absoval.com/linux-wlan (Mark Mathews mark@absoval.com)

## WORKING ON ...

People are working on the following cards:

- Roland SC-55 MIDI (Toshiyuki Nakatsu ir9k-nkt@asahi.net.or.jp)
- CyberRom CD-ROM (David Rowntree rowntree@dircon.co.uk)
- IO DATA PCSC-II (Katayama Nobuhiro kata-n@po.iijnet.or.jp)
- Macnica mPS-1x0 (Katayama Nobuhiro kata-n@po.iijnet.or.jp)
- Proxim RangeLAN/2 http://students.ou.edu/D/James.R.Duchek-1/rangelan2.htm (Jim Duchek jimduchek@primary.net)
- TView Prose (Brenden Tuck friar@zendragon.com)

## UNSUPPORTED

- Adaptec/Trantor APA-460 SlimSCSI
- Eiger Labs SCSI w/FCC ID K36..
- New Media WAVjammer and all other sound cards
- New Media LiveWire+
- Nikon CoolPix100
- Panasonic KXL-D720, KXL-D745, KXL-D783
- SMC 8016 EliteCard
- Xircom CE II Ethernet/Modem
- Xircom CE-10BT Ethernet

## SUPPORTED PARALLEL PORT DEVICES

More and more, the parallel port is used to connect devices other than printers. To support this, parallel port drivers are written for the devices to work. This section presents devices for which parallel port support is written.

To be clear: Printers are not presented in this appendix because they are not supported by parallel port support projects.

Check the Linux Parallel Port support pages for more information at http://www.torque.net/parport. Here you can find

- Paride subsystem for parallel port IDE devices (http://www.torque.net/parport/paride.html)
- Support for parallel port SCSI devices (http://www.torque.net/parport/psscsi.html)

### ETHERNET

- Accton EtherPocket adapter
- AT-Lan-Tec/RealTek parallel port ethernet adapter
- D-Link DE600/DE620 parallel port ethernet adapter

### HARD DRIVES

- H45 Quick HD
- KingByte IDE/ATAPI disks
- KT Technologies HD portable hard disk
- MicroSolutions backpack hard-drives
- SyQuest EZ-135
- SyQuest EZ-230
- SyQuest SparQ
- ValueStor external hard-drive

### TAPE DRIVES

- Hewlett-Packard Colorado Tracker 250 tape drive (all except the T1000e)
- Hewlett-Packard HP Colorado 5GB tape drive
- Iomega Ditto tape drive
- MicroSolutions backpack 8000t, 8000td tape drives

### CD-ROM DRIVES

- Freecom Power CD
- Freecom Traveller CD-ROM
- H45 Quick CD
- Hewlett-Packard HP 7100e/7200e CD-R
- KingByte IDE/ATAPI CD-ROMs
- MicroSolutions backpack CD-ROM. Models 163550 and later are supported by the parallel drive. For models 160550 and 162550 separate drivers are available.
- MicroSolutions backpack PD/CD drive
- SyQuest SyJet

### REMOVABLE DRIVES

- Avatar Shark 250
- Imation Superdisk
- Iomega ZIP, ZIP Plus drives

### IDE ADAPTERS

- Arista ParaDrive products
- DataStor Commuter disks
- Fidelity International Technologies TransDisk products
- Freecom IQ Cable Parallel
- Shuttle Technology EPAT/EP EZ parallel port IDE adapter
- Shuttle Technology EPIA parallel port IDE adapter

### SCSI ADAPTERS

- Adaptec APA-348 mini-SCSI plus adapter cable
  - Driver available at `http://www.torque.net/parport/parscsi.html`
- Adaptec APA-358 mini-SCSI EPP adapter cable
  - Driver available at `http://www.torque.net/parport/parscsi.html`
- Shuttle Technology EPSA-2 parallel port SCSI adapter
  - Driver available at `http://www.torque.net/parport/parscsi.html`
- Shuttle Technology EPST parallel port SCSI adapter
  - Driver available at `http://www.torque.net/parport/parscsi.html`

### DIGITAL CAMERAS

- Connectix QuickCam

### PCMCIA PARALLEL PORT CARDS

The parport_cs driver requires kernel 2.2.x or later.

- Quatech SPP-100
- IOtech DBK35, WBK20A

## PLUG AND PLAY DEVICES

For people having trouble getting Plug and Play devices to work, the ISA PnP utilities written by Peter Fox are available. Quote from the README:

```
These programs allow ISA Plug-And-Play devices to be configured
on a Linux machine.

This program is suitable for all systems, whether or not they
include a PnP BIOS.
```
