
# Testing Your Sound Configuration

Try to play a sound included in the KDE distribution. Use the play command to test your sound card by playing ktalkd.wav (the sound of a phone ringing), like this:

```
# play /opt/kde/share/sounds/ktalkd.wav
```

You can find many sound utilities for SuSE Linux on this book's CD-ROM. Some handy utilities include kmix for KDE and xmix to control the balance and source of your system's sound.

# Alternative Sound Configuration with ALSA

Browse to http://www.alsa-project.org and download a copy of the Advanced Linux Sound Architecture drivers for Linux. ALSA is a great source for a set of free sound drivers for many sound cards not supported by the included Open Sound System modules.

At the time of this writing, ALSA reportedly supports these cards:

- Addonics SV 750
- Audio 16 Pro EPC-SOU9301
- AzTech PCI 64-Q3D
- Best Union Miss Melody 4DWave
- CHIC True Sound 4DWave
- Dynasonic 3-D
- ExpertColor MED-3931 v2.0
- ExpertMedia Sound 16 MED-1680
- Gravis UltraSound Plug & Play
- HIS 4DWave PCI
- Hoontech SoundTrack Digital 4DWave NX
- Jaton SonicWave 4D
- Maui
- MED3210
- Mozart S601206-G
- Schubert 32 PCI (PINE)
- Shark Predator-4D-PCI
- SoundBlaster PCI 128
- SoundBlaster PCI 64
- Sound Player S-928
- STB Sound Rage 32
- Tropez
- Tropez Plus (Tropez+)
- Turtle Beach Malibu
- UltraSound 32-Pro (STB)
- Warpspeed ONSpeed 4DWave PCI

# Games CHAPTER 30

The ALSA software comes in compressed tape archives, and must be downloaded, uncompressed, installed, and configured before. This software supports many more sound cards than are listed because of sound chipset compatibility. This software distribution is worth a try if you cannot get sound working with the included sound drivers. The ALSA developers should get a big vote of thanks for providing this software!

# Configuring Sound the Easy Way

Of course, there's an even easier way to configure SuSE for sound. Browse to http://www.opensound.com/linux.html and download a copy of the Open Sound System, or OSS. You can find links to detailed technical procedures for manual sound configuration, or you can use the commercial version of OSS, which supports more than 200 sound cards (and which saves you a lot of time and effort).

OSS installs using a shell script. When you use OSS online, you receive a license message by email. You can also use a demonstration version to try out the software. If you're having a hard time configuring sound on your system, give OSS a try!

# Summary

Linux has a wealth of available games. Many of these games were inherited by default from early UNIX operating systems. It is a credit to the early game programmers that these games remain popular and still have the ability to amuse and enchant today's Linux users. New Linux users will be able to rediscover the joys of playing older challenging games and will also enjoy the fruits of the growing popularity of Linux: Commercial-quality games are being developed, marketed, and sold for Linux.

![](img/cbac72550c7126a22162e94d91a0c360_990_0.png)

# Appendices

# PART V

## In This Part

- A SuSE Package Listing 959
- B Linux Howto Reference 981
- C Top Linux Commands and Utilities 991
- D LDP 1031
- E GNU License 1035

# SuSE Package Listing

# Appendices
Part V

This appendix is a handy cross-reference to the software included in this book's CD-ROM.
SuSE Unleashed includes SuSE, Inc.'s evaluation CD-ROM, a specially selected collection of from SuSE's commercial six CD-ROM collection (so you can imagine how big this appendix would be to document CD-ROMs!). Table A.1 can help you, build, and install a custom configuration for your system or LAN. This is especially helpful if you have constraints such as hard drive storage or to create custom network multimedia configurations for your install. By using this appendix's table of packages, can choose to build any system, from a minimal configuration to a full install. This appendix might also helped experienced SuSE Linux installs save time and can be used as a pre-flight checklist for selected software.

The appendix was created with the rpm command. Because SuSE Linux is distributed in rpm arrays, the table was quickly built using rpm's package query commands, along with the --queryformat option, and the NAME, SIZE, and DESCRIPTION fields. By filtering t output of the command through the tr (or transliterate) command (to create single-line table descriptions with a carriage return at the end of every line), the table is quickly built

```
# rpm -qa --queryformat '%(NAME)%%(SIZE)%%(SUMMARY)\n' sort >table.txt
```

| TABLE A.1 SuSE Linux 6.2 Package Cross-Reference |
| Package Name | Size (Bytes) | Description |
|---|---|---|
| 3d_chess | 57800 | 3d-dimensional game. |
| 3dpixm | 2483262 | 3D pixmaps for the fwm window manager. |
| 3dpixms | 1224477 | 3D pixmaps for the fwm window manager. |
| a2ps | 2486273 | ASCII text to PostScript conversion utility. |
| aaa_base | 368250 | Base SuSE Linux package. |
| aaa_dir | 176211 | SuSE Linux directory structure. |
| aaa_skel | 112017 | Users home directory configuration files. |
| aalib | 203099 | Low-level graphics library. |
| acroread | 14750011 | Adobe Acrobat PDF reader. |
| addrbo | 456769 | Addressbook program. |
| afio | 93859 | Makes cpo-format archives. |
| afterstp | 798661 | The Afterstep window manager for X. |
| alien | 158021 | Perl script software package conversion utility. |
| antivirus | 2092467 | Virus-scanner software package. |
| apache | 3520354 | The Apache HTTP server. |
| apmd | 130146 | Rik Faith's APM software. |
| aps | 190711 | Printer filter system. |
| arc | 145715 | ARC archives. |

# SuSE Package Listing
APPENDIX A

| TABLE A.1 SuSE Linux 6.2 Package Cross-Reference |
| Package Name | Size (Bytes) | Description |
|---|---|---|
| archie | 44690 | archie. |
| asclock | 34709 | asclock. |
| ash | 100518 | ash. |
| at | 63679 | at. |
| audiofil | 30853 | audiofil. |
| autoconf | 29276 | autoconf. |
| autofs | 31130 | autofs. |
| autolog | 22753 | autolog. |
| automake | 63222 | automake. |
| automate | 25276 | automate. |
| automate3 | 63955 | automate3. |
| axe | 21694 | axe. |
| bash | 110667 | bash. |
| bash1 | 40429 | bash1. |
| bc | 254017 | bc. |
| bdflush | 97876 | bdflush. |
| bindd | 234349 | bindd. |
| binview | 144015 | binview. |
| binutils | 87255 | binutils. |
| bison | 236947 | bison. |
| bluefish | 201440 | bluefish. |
| books | 37130 | books. |
| bttv | 35967 | bttv. |
| cd cddao | 15060 | cddao. |
| cdrecord | 344084 | cdrecord. |
| cdwrite | 229082 | cdwrite. |
| cdtools | 313558 | cdtools. |
| cfengine | 934990 | cfengine. |
| compress | 195714 | compress. |
| conv | 27664 | conv. |
| coolmail | 48002 | coolmail. |
| cpio | 82140 | cpio. |
| cracklib | 294976 | cracklib. |
| cron | 63089 | cron. |
| ctags | 76423 | ctags. |
| cvs | 872555 | cvs. |
| dallock | 69255 | dallock. |
| ddd | 1106732 | ddd. |
| deco | 221440 | deco. |
| detex | 21694 | detex. |
| devs | 35967 | devs. |
| dhclient | 303198 | dhclient. |
| dhcp | 778990 | dhcp. |
| dial | 447886 | dial. |
| dialog | 37130 | dialog. |
| dictd | 1020324 | dictd. |
| dicts | 26947882 | dicts. |
| dochost | 20336 | dochost. |
| dosemu | 3481773 | dosemu. |
| dosfsck | 100143 | dosfsck. |

# Appendices
PART V

TABLE A.1 SuSE Linux 6.2 Package Cross-Reference |
| Package Name | Size (Bytes) | Description |
|---|---|---|
| cddao | 15060 | CD-at-once (DAO). |
| cdrecord | 344084 | Audio recording. |
| cdwrite | 229082 | CD writer. |
| cdtools | 313558 | Various tools for CDs. |
| cfengine | 934990 | Abstract programming language. |
| compress | 195714 | Compression program. |
| conv | 27664 | Unit conversion. |
| coolmail | 48002 | Mail notification. |
| cpio | 82140 | The cpio archive. |
| cracklib | 294976 | Security utility to test passwords. |
| cron | 63089 | Paul Virkie's scheduling system. |
| ctags | 76423 | The ctags programming utility. |
| cvs | 872555 | Front-end to the Revision Control System (RCS). |
| dallock | 69255 | X11 clock with melting digits. |
| ddd | 1106732 | The DDD debugger (Data Display Debugger). |
| deco | 221440 | Visual front-end to Linux, similar to the Norton Commander (or no command). |
| detex | 21694 | Utility to remove (La-)TeX macros. |
| devs | 35967 | The /dev directory files. |
| dhclient | 303198 | DHCP client server for Linux. |
| dhcp | 778990 | The DHCP server. |
| dial | 447886 | Demand-dialing daemon for SLIP and PPP links. |
| dialog | 37130 | Graphic utility for console shell scripts. |
| dictd | 1020324 | Dictionary lookup client and server. |
| dicts | 26947882 | Sources of 14 spell dictionaries. |
| dochost | 20336 | Central documentation server for the SuSE online-support system. |
| dosemu | 3481773 | DOS virtual machine. |
| dosfsck | 100143 | The Linux equivalent of PC/MS-DOS's CHKDSK. |
