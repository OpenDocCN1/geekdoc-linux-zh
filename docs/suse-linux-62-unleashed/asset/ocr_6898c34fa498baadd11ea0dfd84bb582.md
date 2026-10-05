# SuSE System Administration
PART III

Config options: 0

Installed drivers:
Type 10: MS Sound System
Type 27: Compaq Deskpro XL
Type 1: OPL-2/OPL-3 FM
Type 26: MPU-401 (UART)
Type 2: Sound Blaster
Type 20: Sound Blaster PnP
Type 7: SB MPU-401
Type 36: SoftOSS Virtual Wave

Card config:
SoftOSS Virtual Wave Table
Compaq Deskpro XL at @0x50 irq 11 drq 0,0
Sound Blaster at @0x20 irq 5 drq 1,5
(SB MPU-401 at @0x30 irq 5 drq 0)
OPL-2/OPL-3 FM at @0x38 drq 0

Audio devices:
0: MSS audio codec (SoundPro CMI 8330)
1: Sound Blaster 16 (4.13) (DUPLEX)

Synth devices:
0: SoftOSS
1: Yamaha OPL3

Timers:
0: System clock
1: SoftOSS

Mixers:
0: MSS audio codec (SoundPro CMI 8330)
1: Sound Blaster

+   * parport contains directories for each parallel port and reports on the devices attached to each port:

```
$ cat /proc/parport/0/hardware
base: 0x378
irq: none
dma: none
modes: SPP,ECP,ECPP,ECPPS2
```