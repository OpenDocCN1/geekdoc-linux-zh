
## ISDN

- 3Com Sonix Arpeggio
  - `ftp://metalab.unc.edu/pub/Linux/kernel/patches/network/sonix.tgz`
- ASUSCOM Network Inc. ISDNlink 128K PC adapter (HiSax)
- AVM A1 (HiSax)
- AVM B1 (avmb1)
- Combinet EVERYWARE 1000 ISDN
  - `ftp://metalab.unc.edu/pub/Linux/kernel/patches/network/combinet1000isdn-1.02.tar.gz`
- Compaq ISDN S0 (ISA) (HiSax)
- Creatix PnP S0 (HiSax)
- Dr. Neuhaus Niccy PnP/PCI (HiSax)
- Dynalink IS64PH (HiSax)
- Eicon Diehl Diva 2.0 (ISA/PCI) (S0 and U interface, no PRO version) (HiSax)
- Eicon Diehl Diva Piccolo (HiSax)
- Elsa Microlink PCC-16, PCF, PCF-Pro, PCC-8 (HiSax)
- ELSA QuickStep 1000/1000PCI/3000 (HiSax)
- HFC-2BS0 based cards (HiSax)
- IBM Active 2000 (ISA) (act2000)
- ICN ISDN cards (icn)
- Ith Kommunikationstechnik GmbH MC 16 (ISA) (HiSax)
- ITK ix1-micro Rev.2 (HiSax)
- Octal PCBIT (pcbit)
- Sedlbauer Speed Card (HiSax)
- Teles S0-8/S0-16.0/S0-16.3/S0-16.3c/S0-16.4 and compatible ones (HiSax)
- Traverse Technologie NETjet PCI S0 (HiSax)
- USR Sportster internal TA (HiSax)

ISDN cards that emulate standard modems or common Ethernet adapters don’t need any special drivers to work.

## FRAME RELAY

- Emerging Technologies Inc Synchronous Adapters (`http://www.etinc.com`)
- ET/5025 (1 port, 8-bit ISA)
- ET/5025-16 (2 ports, 16-bit ISA)
- ET/5025-25 (2 ports, 16-bit ISA)
- ET/5025pq (4 ports, PCI)

## WIRELESS

- ZCOM WL2420 ISA
  - Product information can be found at `http://www.zcom.com.tw`. Object file kernel drivers are available at `www.boerde.de/~matthias/airnet/zcom_v12`.

## X.25

- Emerging Technologies Inc Synchronous Adapters (`http://www.etinc.com`)
- ET/5025 (1 port, 8-bit ISA)
- ET/5025-16 (2 ports, 16-bit ISA)
- ET/5025-25 (2 ports, 16-bit ISA)
- ET/5025pq (4 ports, PCI)

## POCKET AND PORTABLE ADAPTERS

For more information on Linux and use of the parallel port, go to the Linux Parallel Port Home Page `http://www.torque.net/linux-pp.html` or `http://www.torque.net/parport/`. Check “Supported Parallel Port Devices” for a complete list of supported parallel port devices (excluding printers).

## SLOTLESS

- SLIP/CSLIP/PPP (serial port)
- EQL (serial IP load balancing)
- PLIP (parallel port)—using LapLink cable or bidirectional cable

## ARCNET

Works with all ARCnet cards.

## TOKEN RING

- `http://www.linuxtr.net`
- 3Com 3C619/B/C Tokenlink 16/4 (ibmtr)
- 3Com 3C319 Velocity ISA (ibmtr)
- IBM PCI token ring adapter
- IBM Wake on LAN TR adapter
- IBM 16/4 TR PCI Adapter 2, Adapter 2 Wake on LAN, Adapter 2 Wake on LAN Special
- IBM High Speed 100/16/4 token ring
- IBM ISA 16/4, MCA 16/4 (ibmtr)
- IBM Tropic chipset cards
- Olicom RapidFire 3139, 3140, 3141, 3540
  - `http://www.olicom.com`
- Olicom OC-3136, OC-3137, OC-3138, OC-3129
  - `http://www.olicom.com`
- Madge Smart 100/16/4 PCI, 16/4 PCI Mk3, 16/4 PCI Mk2
  - `http://www.madge.com`
- Madge Presto PCI, 16/4 CardBus
  - `http://www.madge.com`
- SysKonnect TR4/16(+) SK-4190 ISA, SK-4590 PCI, SK-4591 PCI (sktr)

## FDDI

- DEC DEFEA (EISA)/DEFPA (PCI) (kernel 2.0.24 and later)

## AMATEUR RADIO (AX.25)

- Gracilis PacketTwin
- Ottawa PI/PI2
- Most generic 8530 based HDLC boards

## PCMCIA CARDS

- See “Supported PCMCIA Cards” for a complete list or the Web pages of David Hinds at `http://hyper.stanford.edu/HyperNews/get/pcmcia/home.html`.

## ALPHA, BETA DRIVERS

### ETHERNET

- Racal-Interlan NI5210 (i82586 Ethernet chip). Improved support in kernel 2.2 and newer.
- Racal-Interlan NI6510 (am7990 lance chip). Starting with kernel 1.3.66 more than 16MB RAM is supported.
- Racal-Interlan PCI card (AMD PCnet chip Am79C970)

### ISDN

- SpellCaster’s Datacomute/BRI, Telecomute/BRI (ISA) (sc)

### ATM

- Efficient Networks ENI155P-MF 155Mbps ATM adapter (PCI)
  - `http://lrcwww.epfl.ch/linux-atm/`

### Frame Relay

- Sangoma S502 56K Frame Relay card
  - `ftp://ftp.sovereign.org/pub/wan/fr/`

### Wireless

- Proxim RangeLAN2 7100 (ISA)/630x (OEM mini-ISA)
  - `http://www.komacke.com/distribution.htm`

### Unsupported

- 3Com 3C359 Velocity XL PCI
- 3Com 3C339 Velocity PCI
- IBM PCI LANStreamer, MCA LANStreamer token ring
- Intel TokenExpress PRO, TokenExpress 16/4
- SysKonnect/Schneider & Koch Token Ring cards (all of them)

## Sound Cards

More information on sound drivers and sound cards can be found on `http://www.opensound.com/ossfree` or `http://www.opensound.com/oss.html`.

### Supported

- 4Front Technology Virtual Mixer (includes SoftOSS)
- 4Front Technology Virtual Synth (SoftOSS)
- 6850 UART MIDI
- A-Plus Sound of Music (OPL3-SA)
- A-Trend Harmony 3D S751 (PCI)
- AcerMagic S23
- AdLib FM synthesizer card
- AdLib MSC 16 PnP (CS4235)
- AMD Interwave reference card
- ARC Probook
- Audio Excel DSP16
- Avance Logic ALS-007 chip-based cards.
  - Code for this chip is integrated in the Sound Blaster 16 driver. Isapnptools should be used for configuration.
- AW32 Pro (R2.2-W2)
- AW35 (CS4237)
- AW37 Pro (CS4235)
- Aztech Sound Galaxy NX Pro, NX Pro 16, WaveRider 32+
- Aztech Washington
- BTC Mozart Sound System
- BTC-1831 Sound Card (Opti 1688)
- Bravo Sound Card (Opti 82C930)
- Bull PowerPC built-in audio
- CRD4235-6/-8
- CS32-3DI
- Compaq Deskpro XL integrated Business Audio
- Creative EMU8000 addon (PnP)
- Creative Phone Blaster 28.8/33.6
- Creative Sound Blaster 1.0 to 2.0
- Creative Sound Blaster Pro
- Creative Sound Blaster 16
- Creative Sound Blaster 16 ASP
- Creative Sound Blaster 16 PnP (type-1 up to type-10)
- Creative Sound Blaster 16 Vibra
- Creative Sound Blaster 2.x
- Creative Sound Blaster 32/AWE
- Creative Sound Blaster 32/AWE PnP (type-1 up to type-10)
- Creative Sound Blaster AWE64 (type-1 up to type-7)
- Creative Sound Blaster AWE64 Gold (type-1 and type-2)
- Creative Sound Blaster PCI64/128
- Creative Sound Blaster AWE64/Gold and 16/32/AWE PnP cards need to be activated using autoprobe.
- Creative ViBRA16C/CL/S (type-1 and type-2) PnP
- Creative ViBRA16X PnP (half duplex only)
- Crystal Lake Crystal Clear Series 100
- Crystal Audio (CS4235)
- Crystal CRD4236B-1E
- Crystal CRD4237B-5/-8
- Crystal CSC0B35 (CS4236B)
- Crystal CX4237B-SIDE
- Crystal Onboard PnP Audio (CS4235)
- Dell Latitude built-in audio
- Diamond Crystal MM PC/104
- Digital AXP built-in audio
- ECHO-PSS cards (Orchid SoundWave32, Cardinal DSP16)
- ESS 1868, 1869 (type-1 and type-2), 1878, 1879, 1968 PnP AudioDrive
- Ensoniq AudioPCI (ES1371)
- Ensoniq AudioPCI/SoundBlaster PCI (ES1370)
- Ensoniq Soundscape Elite
- Ensoniq Soundscape PnP (model 1 and 2)
- Ensoniq Soundscape S-2000
- Ensoniq Soundscape VIVO, VIVO90
- Ensoniq ActionNote 880 C/CX
- Gallant’s sound card (SC-6000 and SC-66000 based)
- Generic AD1815-based soundcard (PnP)
- Generic CMI8330-based soundcard (PnP)
- Generic Crystal CS4232-based soundcard or motherboard (non PnP)
- Generic Crystal CS4232 by Acer (PnP mode)
- Generic Crystal CS4232 type-1 up to type-3 (PnP mode)
- Generic Crystal CS4235 type-1
- Generic Crystal CS4236 (type-1 up to type-3)
- Generic Crystal CS4236-based soundcard or motherboard (non PnP)
- Generic Crystal CS4236A (type-1 and type-2), CS4236B
- Generic Crystal CS4237-based soundcard or motherboard (non PnP)
- Generic Crystal CS4237B (type-1 and type-2)
- Generic Crystal CS4238-based soundcard or motherboard (non PnP)
- Generic ESS ES688, ES1688, ES1788, ES1868, ES1869, ES1887, ES1888-based soundcard or motherboard
- Generic Jazz16-based soundcard
- Generic MAD16 (OPTi 82C928), MAD16 Pro, MAD16 Pro (duplex) (OPTi 82C929)
- Generic Mozart soundcard (OAK OTI-601 chip)
- Generic OPTi 82C924, 82C925-based sound card (PnP)
- Generic OPTi 82C924 soundcard (non-PnP mode). Use the MSS driver and the isapnp tools.
- Generic OPTi 82C930
- Generic OPTi 82C931
  - See `http://spoke.nols.com/~drees/opti931.html`.
