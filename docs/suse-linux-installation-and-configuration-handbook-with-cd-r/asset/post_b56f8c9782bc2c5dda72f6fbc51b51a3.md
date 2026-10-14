
## Slotless

The following is a list of all the slotless ports that are supported in Linux:

- SLIP/CSLIP/PPP (serial port)
- EQL (serial IP load balancing)
- PLIP (parallel port) (using LapLink cable or bi-directional cable)

## ARCnet

SuSE Linux works with all ARCnet cards.

## Token Ring

Linux supports the following token ring cards:

- Any IBM token ring card not using DMA
- IBM Tropic chipset cards
- Madge TokenRing OCI 16/4 Mk2

## FDDI

Linux supports the following FDDI card:

- DEFEA (EISA) / DEFPA (PCI) (kernel 2.0.24 and later)

## Amateur Radio (AX.25)

Linux supports the following Amateur Radio cards:

- Gracilis PackeTwin
- Ottawa PI/PI2
- Most generic 8530-based HDLC boards

## Ethernet

Linux supports the following Ethernet cards:

- Racal-Interlan NI5210 (82586 Ethernet chip) (Avoid this card. It does not function properly with the current driver.)
- Racal-Interlan NI6510 (am7990 lance chip) (Starting with kernel 1.3.66, more than 16MB RAM is supported.)
- Racal-Interlan PCI card (AMD PC net chip 97c970)

## ISDN

Linux supports the following ISDN card:

- SpellCaster's Datacommu te/BRI, Telecommute/BRI (ISA) (sc)

## ATM

Linux supports the following ATM adapter:

- Efficient Networks ENI155P-MF 155 Mbps ATM adapter (PCI)

## Frame Relay

Linux supports the following frame relay card:

- Sangoma S502 56K Frame Relay card

## Wireless

Linux supports the following wireless technology:

- Proxim RangeLan2 7100 (ISA) / 630x (OEM mini-ISA)

## Sound Cards

Linux has good support for most sound cards. The following is a list of the supported sound cards:

- 6850 UART MIDI
- Adlib (OPL2)
- Audio Excell DSP16
- Aztech Sound Galaxy NX Pro
- Crystal CS4232/CS4236 (PnP)-based cards
- ECHO-PSS cards (Orchid SoundWave32, Cardinal DSP16)
- Ensoniq SoundScape
- Gravis Ultrasound
- Gravis Ultrasound 16-bit sampling daughterboard
- Gravis Ultrasound MAX
- Gravis Ultrasound ACE (No MIDI port and audio recording)
- Gravis Ultrasound PnP (with RAM)
- Logitech SoundMan Games (SBPro, 44KHz stereo support)
- Logitech SoundMan Wave (Jazz16/OPL4)
- Logitech SoundMan 16 (PAS-16-compatible)
- MediaTriX AudioTriX Pro
- Media Vision Premium 3D (Jazz16)
- Media Vision Pro Sonic 16 (Jazz)
- Media Vision Pro Audio Spectrum
- Media Vision Pro Audio Studio
- Microsoft Sound System (AD1848)
- OAK OTI-601D cards (Mozart)
- OPTi 82C924/82C925 cards (Use the MSS driver and isapnp tools)
- OPTi 82C928/82C929 cards (MAD16/MAD16 Pro/ISP16/Mozart)
- OPTi 82C931 cards
- Sound Blaster
- Sound Blaster Pro
- Sound Blaster
- Sound Blaster 32/64/AWE (Configure it like Sound Blaster 16)
- Sound Blaster AWE63/Gold and 16/32/AWE (PnP cards need to be activated using isapnptools)
- Turtle Beach Wavefront cards (Maui, Tropez)
- Wave Blaster (and other daughterboards)
- Cards based on the ESS Technologies AudioDrive chips (688, 1688)
- AWE32/64 support starts in kernel series 2.1.x (check the SoundBlaster AWE mini-HOWTO by Marcus Brinkmann for installation details)
- MPU-401 MIDI
- Sound Blaster Live!
- MPU-401 MIDI (intelligent mode)
- PC speaker / Parallel port DAC
- Turtle Beach MultiSound/Tahiti/Monterey

## Modems

Linux supports all internal modems and external modems connected to the serial port. Alas, some manufacturers have created Windows 95-only modems. A small number of modems come with DOS software that downloads the control program at runtime. Loading the program under DOS and performing a warm boot normally enables the use of these. Such modems are probably best avoided, though, because you won’t be able to use them with non-PC hardware in the future.

All PCMCIA modems should work with the PCMCIA drivers.

## Printers

Linux supports a large variety of printers. One subset of printers, however, is designed for only MS Windows and doesn’t work with Linux. The following is a list of supported printers:

- Apple Imagewriter
- C. Itoh M8510
- Canon BubbleJet BJI0e (bji0e)
- Canon BubbleJet BJC200, BJC-210 (B/W only), BJC-240 (B/W only) (bj200)
- Canon BubbleJet BJC-600, BJC-610, BJC-4000, BJC-4100, BJC-450, MultiPASS C2500, BJC-240, BJ-70 (bjc600)
- Canon BubbleJet BJC-800 (bjc800)
- Canon LBP-8II, LIPS III
- DEC LA50/70/75/75plus
- DEC LN03, LJ250
- Epson 9 pin, 24 pin, LQ series, AP3250
- Epson Stylus Color/Color II/500/800 (stcolor)
- HP 2563B
- HP DesignJet 650C
- HP DeskJet, DeskJet Plus (deskjet)
- HP DeskJet 500, DeskJet Portable (djet500)
- HP DeskJet 400/500C/540C/690C/693C (cdj500)
- HP DeskJet 550C/560C/600/660C/682C/683C/693C/850/870Cse (cdj550)
- HP DeskJet 850/870Cse/870Cxi/680 (cdj850)
- HP DeskJet 500C/510/520/5540C/693C printing black only (cdjmono)
- HP DeskJet 600 (lj4dith)
- HP DeskJet 600/870Cse, LaserJet 5/5L (ljet4)
- HP DeskJet 500/500C/510/520/540/550C/560C/850C/855C
- HP DeskJet 720, 820, and 1000 series
- HP PaintJet XL300, DeskJet 600/1200C/1600C (pjxl300)
- HP LaserJet/Plus/II/III/4
- HP PaintJet/XL
- IBM Jetprinter color
- IBM Proprinter
- Imagen ImPress
- Mitsubishi CP50 color
- NEC P6/P6+/P60
- Oki OL410ex LED (jet4)
- Okidata MicroLine 182
- Ricoh 4081/6000 (r4081)
- SPARCprinter
- StarJet 48 inkjet printer
- Tektronix 4693d color 2/4/8 bit
- Tektronix 4695/4696 inkjet plotter
- Xerox XES printers (2700, 3700, 4045, and so on)
- Canon BJC600/800 color printers

## Scanners

Linux supports scanners using the SANE package. This package supports the following scanners:

- A4 Tech AC 4096 / AS 8000P
- Adara Image Star I
- Conrad Personal Scanner 64, P105 handheld scanners
- Epson GT6000
- Fujitsu SCSI-2 scanners (contact Dr. G.W. Wettstein)
- Genius ColorPage-SP2
- Genius GS-B105G handheld scanner
- Genius GeniScan GS4500, GS4500A handheld scanners
- HighScreen Greyscan 256 handheld scanner
- HP ScanJet II series SCSI
- HP ScanJet IIc, IIcx, IIp, 3c, 4c, 4p, 5p, 5pse, plus
- Logitech Scanman+, Scanman 32, Scanman 256 handheld scanners
- Microtek ScanMaker E3, E6, II, IIXE, III, and 35t models
- Mustek M105 handheld scanner
- Mustek HT800 Turbo, Matador 105, and Matador 256 handheld scanners
- Mustek Paragon 6000CX
- Nikon Coolscan SCSI 35mm film scanner
- Pearl 256 handheld scanner
- UMAX SCSI scanners
- Genius GS-4000, ScanMate/32, ScanMate/GS handheld scanners
- Mustek HT105, M800 handheld scanners
- Voelker Personal Scanner 64 handheld scanner

The following scanners are not supported:

- Acer scanners (Acer is not releasing any programming information.)
- Escom 256 (Primax Lector Premier 256) handheld scanner
- Genius ScanMate/256, EasyScan handheld scanners
- Mustek CG8000 handheld scanner
- Trust AmiScan handheld scanner

## Amateur Radio

Linux supports the following cards:

- KISS-based Terminal Node Controllers
- Ottawa Pi card
- Gracilis PacketTwin card
- Other Z8530 SCC-based cards
- Parallel and serial port Baycom modems
- Sound Blaster cards
- Soundcards based on the Crystal chipset

## Terminals on Serial Port

Old terminals easily can be used under Linux by connecting them to your system's serial port. The following terminals are supported:

- VT52
- VT100
- VT220
- VT320
- VT420

## Joysticks

Joystick support exists in the latest XFree86 distributions (3.3.x) and kernel versions 2.2.xx and above.

## Video Capture Boards/Frame Grabbers/TV Tuners

Linux has support for the following video capture cards:

- CMOS Video Conferencing Kit (The video capture card has a BT849 chipset. It comes with a CCD camera.)
- Data Translation DT2803
- Data Translation DT2851 Frame Grabber
- Data Translation DT3155
- Diamond DTV2000 (based on BT848)
- Dipix XPG1000/FPG/PPMAPA (based on TI C40 DSP)
- Epix SVM
- Epix Silicon Video MUX series of video frame grabbing boards
- FAST Screen Machine II
- Hauppage Wincast TV PCI (based on BT848)
- Imaging Technology ITI/IC-PCI
- ImageNation Cortex I
- ImageNation CX100
- ImageNation PX500 (being worked on) (Ask for current status.)
- Imaging Technology, Inc. IC-PCI frame grabber board
- Matrox Meteor
- Matrox PIP-1024
- MaxiTV/PCI (based on ZR36120)
- Miro PCTV (based on BT848)
- MuTech MV1000 PCI
- MuTech MV200
- Philips PCA10TV (not in production anymore)
- Pro Movie Studio
- Quanta WinVision B&W video capture card
- Quickcam
- Sensus 700
