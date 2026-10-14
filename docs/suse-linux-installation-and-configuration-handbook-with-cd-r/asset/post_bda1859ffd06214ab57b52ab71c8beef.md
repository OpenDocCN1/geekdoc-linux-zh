
The following are not supported:

- Parallel port SCSI adapters
- Non-Adaptec-compatible DTC boards (327x, 328x)

## Hard Drives

Linux supports all hard drives, as long their controllers are supported. All direct access SCSI devices with a block size of 256, 512, or 1024 bytes should work. Other block sizes will not work. Large IDE (EIDE) drives work fine with newer kernels, but the boot partition must lie in the first 1024 cylinders because of PC BIOS limitations.

Some Conner CEP1060S drives might have problems with Linux and ext2fs. The symptoms are inode errors during e2fsck and corrupt filesystems. Conner has released a firmware upgrade to fix this problem, though.

## Tape Drives

Linux supports several tape drives. The following is a list of supported drives:

- SCSI tape drives
- Seagate Sidewinder 50 AIT (on ICP 6527 RAID-controller)
- QIC-02 drives
- Iomega DITTO internal (ftape 3.04c and newer)
- * QIC-117, QIC-40/80, QIC-3010/3020 (QIC-WIDE) drives

In addition to those drives listed previously, most tape drives using the floppy controller should work with Linux.

## ATAPI Tape Drives

## CD-ROMs

Linux supports a variety of CD-ROMs, including the following:

- SCSI CD-ROM drives
- EIDE (ATAPI) CD-ROM drives (IDECD)
- Mitsumi FX400
- Nec-260
- Sony 55E
- Aztech CDA268-01A, Orchid CDS-3110, Okano/Wearnes CDD-110, Conrad TXC, CyCDROM CR520ie/CR540ie/CR940ie (AZTCD)
- Creative Labs CD-200(F) (SBPCD)
- Funai E2550UA/MK4015 (SBPCD)
- GoldStar R420 (GSCD)
- IBM External ISA (SBPCD)
- Kotobuki (SBPCD)
- Lasermate CR328A (OPTCD)
- LMS Philips CM 206 (CM206)
- Longshine LCS-7260 (SBPCD)
- Matsushita/Panasonic CR-521/522/523/562/563 (SBPCD)
- MicroSolutions Backpack parallel port drive (BPCD)
- Mitsumi CR DC LU005 (MCD/MCDX)
- Mitsumi FX001D/F (MCD/MCDX)
- Optics Storage Dolphin 8000AT (OPTCD)
- Sanyo CDR-H94A (SJCD)
- Sony CDU31A/CDU33A (CDU31A)
- Sony CDU-510/CDU-515 (SONYCD535)
- Sony CDU-535/CDU-531 (SONYCD535)
- TEAC CD-55A SuperQuad (SBPCD)
- LMS/Philips CM 205/225/202
- NEC CDR-35D (old)
- Sony SCSI multisession CD-XA
- Parallel Port Driver

## CD-Writers

The following is a list of all the supported CD-Writers in Linux:

- Grundig CDR 100 IPW
- HP CD-Writer+ 7100 and 8100
- HP SureStore 4020i
- HP SureStore 6020es/i
- JVC XR-W2010
- Mitsubishi CDRW-225
- Mitsumi CR-2600TE
- Olympus CDS 620E
- Philips CDD-522/2000/2600/3610
- Pinnacle Micro RCD-5020/5040
- Plextor CDR PX-24CS
- Ricoh MP 1420C
- Ricoh MP 6200S/6201S
- Sanyo CRD-R24S
- Smart and Friendly Internal 2006 Plus 2.05
- Sony CDU 920S/924/926S
- Taiyo Yuden EW-50
- TEAC CD-R50S
- WPI(Wearnes) CDR-632P
- WPI(Wearnes) CDRW-622
- Yamaha CDR-100
- Yamaha CDR-200/200t/200tx
- Yamaha CDR-400t/400tx

## Removable Drives

Linux supports all SCSI drives as long as the controller is supported, including optical (MO), WORM, floptical, Bernoulli, Zip, Jaz, SyQuest, PD, and others. The following is a list of those supported:

- Panasonic MO (combines a CD-ROM drive and an optical removable disk)
- Parallel port Zip drives
- Parallel port Avatar Shark-250
- Fujitsu magneto-optical disk drives M2513
- LS-120 floptical
- PD-CD

## Mice

Linux supports the following mice:

- Microsoft serial mouse
- Mouse Systems serial mouse
- Logitech Mouseman serial mouse
- Logitech serial mouse
- ATI XL Inport busmouse
- C&T 82C710 (QuickPort) (Toshiba, TI Travelmate)
- Microsoft busmouse
- Logitech busmouse
- PS/2 (auxiliary device) mouse

## Controllers (I/O)

Linux will support any standard serial/parallel/joystick/combo cards. Linux supports 8250, 16450, 16550, and 16550A UART's. In addition, cards that support non-standard IRQs (IRQ > 9) can be used.

## Controllers (Multiport)

Linux supports both types of multiport controllers, non-intelligent and intelligent. The non-intelligent cards that are supported are as follows:

- AST FourPort and clones (4 port)
- Accent Async-4 (4 port)
- Arnet Multiport-8 (8 port)
- Bell Technologies HUB6 (6 port)
- Boca BB-1004, 1008 (4, 8 port) (no DTR, DSR, and CD)
- Boca BB-2016 (16 port)
- Boca IO/AT66 (6 port)
- Boca IO 2by4 (4 serial / 2 parallel, uses 5 IRQs)
- Computone ValuePort (4, 6, 8 port) (AST FourPort-compatible)
- DigiBoard PC/X, PC/Xem, PCI/Xem, EISA/Xem, PCI/Xr (4, 8, 16 port)
- Comtrol Hostess 550 (4, 8 port)
- PC-COMM 4-port (4 port)
- SIIG I/O Expander 4S (4 port, uses 4 IRQs)
- STB 4-COM (4 port)
- Twincom ACI/550
- UseNet Serial Board II (4 port)

The following intelligent cards are supported:

- Computone IntelliPort II (4/8/16 port)
- Cyclades Cyclom-8Y/16Y (8, 16 port) (ISA/PCI)
- DigiBoard PC/Xe (ISA), PC/Xi (EISA), and PC/Xeve
- Equinox SST Intelligent serial I/O cards
- Hayes ESP 1, 2, and 8 port versions
- Stallion EasyIO (ISA) / EasyConnection 8/32 (ISA/MCA) / EasyConnection 8/64 (PCI)
- Stallion EasyConnection 8/64 (ISA/EISA) / ONboard (ISA/EISA/MCA) / Brumby (ISA)
- Control RocketPort (8/16/32 port)
- DigiBoard COM/Xi
- Moxa C102, C104, C168, C218 (8 port), C320 (8/16/24/32 expandable), and C320T
- RISCom/8
- Specialix SIO/XIO (modular, 4 to 32 ports)
- Specialix IOX+

## Network Adapters

Linux has good support for most network cards. The basic rule here is the newer the card, the better the performance. Linux supports the following cards:

- 3Com 3C501 (avoid this one like the plague)
- 3Com 3C503, 3C505, 3C507, 3C509/3C509B (ISA) / 3C579 (EISA)
- 3Com Etherlink III Vortex Ethercards (3C590, 3C592, 3C595, 3c597) (PCI), 3Com Etherlink XL Boomerang Ethercards (3c900, 3c905) (PCI), and 3Com Fast Etherlink Ethercard (3c515) (ISA)
- AMD LANCE (79C960) / PCnet-ISA/PCI (AT1500, HP J2405A, NE1500/NE2100)
- AT&T GIS WaveLAN
- Allied Telesis AT1700
- Allied Telesis LA100PCI-T
- Ansel Communications AC3200 EISA
- Apricot Xen-II / 82596
- Cabletron E21xx
- Cogent EM110
- Crystal Lan CS8920, Cs8900
- Danpex EN-9400
- DEC DE425 (EISA) / DE434/DE435 (PCI) / DE450/DE500 (DE4x5 driver)
- DEC DE450/DE500-XA (tulip driver)
- DEC DEPCA and EtherWORKS
- DEC EtherWORKS
- DEC QSiilver's (Tulip driver)
- Fujitsu FMV-181/182/183/184
- HP PCLAN (27245 and 27xxx series)
- HP PCLAN PLUS (27247B and 27252A)
- HP 10/100VG PCLAN (J2577, J2573, 27248B, J2585) (ISA/EISA/PCI)
- ICL EtherTeam 16i / 32 EISA
- Intel EtherExpress
- Intel EtherExpress Pro
- KTI ET16/P-D2, ET16/P-DC ISA (work jumperless and with hardware-configuration options)
- NE2000/NE1000 (be careful with clones)
- Netgear FA-310TX (tulip chip)
- New Media Ethernet
- PureData PDUC8028, PD18023
- SEEQ 8005
- SMC Ultra / EtherEZ (ISA)
- SMC 9000 series
- SMC PCI EtherPower 10/100 (Tulip driver)
- SMC EtherPower II (epic100.c driver)
- Schneider & Koch G16
- Western Digital WD80x3
- Zenith Z-Note / IBM ThinkPad 300 built-in adapter
- Znyx 312 etherarray (Tulip driver)

## ISDN

Linux supports many of the popular ISDN cards. The following is a list of all the cards Linux supports:

- 3Com Sonix Arpeggio
- ASUSCOM Network, Inc. ISDNLink 128K PC adapter (HiSax)
- AVM A1 (HiSax)
- Combinet EVERYWARE 1000 ISDN
- Compaq ISDN S0 (ISA) (HiSax)
- Creatix PnP S0 (HiSax)
- Dr. Neuhaus Niccy PnP/PCI (HiSax)
- Dynalink IS64PH (HiSax)
- Eicon.Diehl Diva 2.0 ISA and PCI (S0 and U interface, no PRO version) (HiSax)
- Eicon.Diehl Diva Piccola (HiSax)
- Elsa Microlink PCC-16, PCF, PCP-Pro, PCC-8 (HiSax)
- ELSA QuickStep 1000/1000PCI/3000 (HiSax)
- HFC-2BS0-based cards (HiSax)
- IBM Active 2000 (ISA) (act2000)
- ICN ISDN cards (icn)
- Ilh Kommunikationstechnik GmbH MIC 16 (ISA) (HiSax)
- ITK ix1-micro Rev.2 (HiSax)
- Octal PCBIT (pcbit)
- Sedlbauer Speed Card (HiSax)
- Teles 8.0/16.0/16.3 and compatible ones (HiSax)
- Teles 16.3c (HiSax)
- Teles S0 (HiSax)
- Traverse Technologies NETjet PCI S0 (HiSax)
- USR Sportster internal TA (HiSax)

## Pocket and Portable Adapters

The following is a list of all the pocket and portable adapters that are supported in Linux:

- Accton parallel port ethernet adapter
- AT-Lan-Tec/RealTek parallel port adapter
- D-Link DE600/DE620 parallel port adapter
