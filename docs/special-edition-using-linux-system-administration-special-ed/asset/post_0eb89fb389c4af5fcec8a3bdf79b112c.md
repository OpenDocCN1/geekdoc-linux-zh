
- Generic Soundscape-based soundcard
- Generic Windows Sound System compatible
- Generic Yamaha OPL3-SA1 (YMF701)-based soundcard
- Generic Yamaha OPL3-SA2 (YMF711)-based soundcard (type-1, type-3, type-4)
- Generic Yamaha OPL3-SA3 (YMF715)-based soundcard
- Generic Yamaha OPL3-SAx (YMF715/YMF719) non-PnP
- Gravis Ultrasound
- Gravis Ultrasound Extreme
- Gravis Ultrasound 16-bit sampling daughterboard
- Gravis Ultrasound MAX
- Gravis Ultrasound ACE
- Gravis Ultrasound PnP (with RAM), PnP Pro
- HP OmniBook 2100 (CS4236)
- Home Studio 64 (analog audio only)
- IBM Audio Feature (CS423x)
- Logitech SoundMan Games (SBPro, 44kHz stereo support)
- Logitech SoundMan Wave (Jazz16/OPL4)
- Logitech SoundMan 16 (PAS-16 compatible)
- MED3201 audio card
- Maxi Sound 32 PnP (analog audio only)
- Maxi Sound 64 Dynamic 3D (analog audio only)
- Media Sound SW/32 (non-PnP mode)
- Media TriX AudioTriX Pro, 3D XG
- Media Vision Premium 3D (Jazz16)
- Media Vision Pro Sonic 16 (Jazz)
- Media Vision Pro Audio Spectrum 16 (PAS-16)
- Media Vision Pro Audio Studio 16
- Media Vision Thunderboard
- Microsoft Windows Sound System board (AD1848)
- MiroSound PCM1-pro
- MultiWave AudioWave Green 16
- Music Quest MIDI connector card (MCC)
- Music Quest MQX-16, MQX-16S MIDI adapter
- Music Quest MQX-32, MQX-32M MIDI adapter
- Music Quest PC MIDI card
- NEC Harmony
- Orchid SoundDrive 16EZ
- Pine PT201
- Primax SoundStorm FM 16, SoundStorm Wave
- Pro Audio Spectrum 16, Studio 16
- RME Digi32, Digi32 Pro, Digi32/8
- Reveal SC300
- Reveal WaveXtreme Pro (with RAM)
- Roland MPU IPC-T MIDI adapter
- S3 SonicVibes
- Shark Mako
- Sharp PC8800
- Shuttle Sound System 48
- Spacewalker HOT-255 PCI 3D (PCI)
- TerraTec Maestro 32/96
- Terratec EWS64XL (audio only)
- Terratec Sound System Base 1 (AD1816)
- Terratec Sound System Base 64 (AD1816)
- Tomato Sound System (OPTi 82C930)
- Trust Sound Expert De Luxe Wave 32
- Turtle Beach Classic/Tahiti/Monterey
- Turtle Beach Maui
- Turtle Beach Monte Carlo 928, Monte Carlo 929
- Turtle Beach Pinnacle/Fiji
- Turtle Beach Tropez, Tropez Plus (audio only)
- Turtle Beach Daytona (audio only)
- Wearnes Classic 16
- Yamaha Sound Edge SW20-PC
- Zefiro Acoustics ZA2 (NOT RECOMMENDED)
- Zenith Z-Player
- AWE32/64 support is started in kernel series 2.1.x (check the SoundBlaster AWE mini-HOWTO by Marcus Brinkmann for installation details).
- MPU-401 MIDI Intelligent mode (don't enable blindly)
- MPU IPC-T
- MQX-32M
- MPU-401 MIDI UART only dumb port (don’t enable blindly)
- Yamaha FM synthesizers (OPL2, OPL3, OPL3-SA(x) (since kernel series 2.1.x) and OPL4)
- OSS supports all MIDI daughter cards including Wave Blaster, TB Rio, and Yamaha DB50XG. The only requirement is that the “host” card be supported by OSS. Note that only the “host” card needs to be configured using soundconf. The daughter card will be automatically accessible through the MIDI of the “host” card.

### 1.3.2 Alpha, Beta drivers

- 4Front Tech. Waveloop audio device
- Acer FX-3D (AD1816 based)
- AVM Apex Pro card (AD1816 based)
- Aztech AZT1008, AZT12320, AZT3000
- Aztech SC-16 3D (AD1816 based)
- Creative Sound Blaster Vibra16x
- Creative Sound Blaster Live! and Live! Value Edition
- Creative Labs has beta driver for this card. They work with kernels 2.0.36 and 2.2.5 (and most likely newer kernels in these series). The drivers can be downloaded under the software download area at http://www.creativelabs.com.
- Highscreen Sound-Booster 32 Wave 3D (AD1816 based)
- Highscreen Sound-Booster 16 (AD1816 based)
- HP Kayak (AD1816 based)
- IBM MWave
- Newcom SC-16 3D (AD1816 based)
- PC speaker/Parallel port DAC
  `ftp://ftp.informatik.hu-berlin.de/pub/os/linux/hu-sound/`
- Rockwell WaveArtist chipset
- Sonorus STUDI/O
- SY-1816 (AD1816 based)
- Terratec Base 1, Base 64 (AD1816 based)
- Terratec EWSS64S (AD1816 based)
- Turtle Beach Malibu `ftp://ftp.cs.colorado.edu/users/mccreary/archive/tbeach/multisound/`

For the AD1816 sound chip-based sound cards, isapnptools is needed for configuration.

### Unsupported

- A-Trend Harmony 3DS724 (PCI)
- Atech PCI 388-A3D
- Adaptec AME-1570
- Aureal Vortex (PCI)
- Cardinal DSP 16
- Contributed low-level drivers
- Crystal CS4614 (PCI)
- Cyrix MediaGX built-in audio
- Diamond Monster Sound MX300
- Diamond Sonic Impact
- Dream 94PnP Home Studio
- EON Bach SP901 (A3D)
- ESS (PCI)
- ESS Maestro-1 (PCI), Maestro-2 (PCI)
- ESS Solo-1 (PCI)
- Echo Personal Sound System
- Generic ALS007, ALS100-based soundcard
- Orchid NuSound 3D
- Orchid SoundWave 32
- Paradise DSP-16
- Quicknet Internet LineJACK
- Terratec XLerate (A3D)
- Turtle Beach Montego
- Turtle Beach TBS-2000
- Videologic SonicStorm
- Wearnes Beethoven ADSP-16
- Western Digital Paradise DSP-16
- Yamaha YMF724 (PCI)

The ASP chip on Sound Blaster 16 series is not supported. AWE32’s onboard E-mu MIDI synthesizer is not supported.

Nathan Laredo (laredo@gnu.ai.mit.edu) is willing to write AWE32 drivers if you send him a complimentary card. He is also willing to write drivers for almost any hardware if you send him free samples of your hardware.

Sound Blaster 16s with DSP 4.11 and 4.12 have a hardware bug that causes hung/stuck notes when playing MIDI and digital audio at the same time. The problem can happen with either Wave Blaster daughterboards or MIDI devices attached to the MIDI port. There is no known fix.

## HARD DRIVES

All hard drives should work if the controller is supported.

(From the SCSI HOWTO) All direct access SCSI devices with a block size of 256, 512, or 1024 bytes should work. Other block sizes will not work (note that this can often be fixed by changing the block or sector sizes using the MODE SELECT SCSI command).

Large IDE (EIDE) drives work fine with newer kernels. The boot partition must lie in the first 1024 cylinders due to PC BIOS limitations.

Some Conner CFP1060S drives may have problems with Linux and ext2fs. The symptoms are inode errors during e2fsck and corrupt file systems. Conner has released a firmware upgrade to fix this problem. Contact Conner at 1-800-4CONNER (US) or +44-1294-315333 (Europe). Have the microcode version (found on the drive label, 9WA1.6x) handy when you call.

Many Maxtor and Western Digital IDE drives are reported to not happily co-exist on the same IDE cable with the other manufacturer's drive. Usually one of the drives will fail during operation. A solution is to put them on different IDE cables.

Certain Micropolis drives have problems with Adaptec and BusLogic cards. Contact the drive manufacturers for firmware upgrades if you suspect problems.

- Multiple device driver (RAID-0, RAID-1)
  `ftp://sweet-smoke.ufr-info-p7.ibp.fr/public/Linux/`

### UNSUPPORTED

The following hard drives are mentioned as not supported by Linux. Read the bug report available.

- NEC D3817, D3825, D3827, D3847
  - These drives are slightly non-SCSI-2 compliant in the values reported in Mode Sense Page 3. In Mode Sense Page 3 all NEC D38x7 drives report their sector size as zero. The NEC drives are the first brand of drive we have ever encountered that reported the sector size as zero. Unfortunately, that field in Mode Sense Page 3 is not modifiable and there is no way to update the firmware on the D38x7 drives to correct this problem. Problems are mentioned for D3825 and D3827 (both revision 0407). Revision 0410 of these two hard drives seems to solve this problem.

## Tape Drives

### Supported

- SCSI tape drives
  - (From the SCSI HOWTO) Drives using both fixed and variable length blocks smaller than the driver buffer length (set to 32k in the distribution sources) are supported. Virtually all drives should work. (Send mail if you know of any incompatible drives.)
- Seagate Sidewinder 50 AIT (on ICP 6527 RAID-controller)
- QIC-02 drives
- Iomega Ditto internal (ftape 3.04c and newer)

### Alpha, Beta Drivers

- QIC-117, QIC-40/80, QIC-3010/3020 (QIC-WIDE) drives
  - Most tape drives using the floppy controller should work. Various dedicated controllers (Colorado FC-10/FC-20, Mountain Mach-2, Iomega Tape Controller II) are also supported.
  - `ftp://metalab.unc.edu/pub/Linux/kernel/tapes`
- ATAPI tape drives
  - For these an alpha driver (ide-tapec) is available in the kernel. ATAPI tape drives supported are
  - Seagate TapeStor 8000
  - Conner CTMA 4000 IDE ATAPI Streaming tape drive

### Unsupported

- Emerald and Tecmar QIC-02 tape controller cards—Chris Urlich
  - `insom@math.ucr.edu`
- Drives that connect to the parallel port (for example: Colorado Tracker)
- Some high-speed tape controllers (Colorado TC-15)
- Irwin AX250L/Accutrak 250 (not QIC-80)
- IBM Internal Tape Backup Unit (not QIC-80)
- COREtape Light

## CD-ROM Drives

For more information on CD-ROM drives check the CDROM-HOWTO at `http://metalab.unc.edu/LDP/HOWTO/`.
