
# Sound Formats

A number of formats exist for storing sound recordings. Some of these formats are associated with specific technologies, and others are used strictly for proprietary reasons. Red Hat Linux supports several of the most popular sound formats, including

- Raw (.raw)—More popularly known as a headless format, audio files using this format contain an amorphous variety of specific settings and encodings. All other sound files contain a short section of the beginning—a header—that identifies the file type.
- MP3 (.mp3)—A popular but commercially licensed format for the digital encoding used by many Linux and Windows applications. MP3 isn't supported by any software included with Red Hat (which advises you to use the open source Ogg-Vorbis format instead).
- WAV (.wav)—The popular uncompressed Windows audio-visual sound format. It's often used as an intermediate file format when encoding audio.
- Ogg-Vorbis (.ogg)—Red Hat's preferred audio encoding format. You'll enjoy better compression, audio playback, and freedom from lawsuits by using this open source encoding format for your audio files.

> NOTE
> Due to patent and licensing issues, Red Hat has removed support for the MPEG, MPEG2 and MPEG3 (MP3) files in Red Hat 8.0. Although I can't offer any legal advice, it appears that individuals using MP3 software are okay; it's just that Red Hat cannot distribute the code because it sells its distribution. It seems—at this point—perfectly all right for you to obtain a version of Xmms (for example), which is a Winamp clone that plays MPEG1/2/3 files (you can learn more about Xmms in the "Music Players" section, later in this chapter). You can get Xmms directly from the source code.
> Another alternative is to use the Ogg-Vorbis format; it's completely free of restrictions. A free-not-CPL Ogg-Vorbis ripper for CD music is available from http://www.thecompany.com/projects/tkoggripper/ and an MP3-to-Ogg converter is available from http://faceprint.com/software.shtml/. Or you could download and install the non-cropped version from FreshRPMs at http://psyche.freshrpm.net/.

Red Hat includes software (such as the sock command) that you can use to listen to audio files in a wide variety of formats, such as AU (from NeXT and Sun), AIFF (from Apple and SGI), IFF (originally from Commodore's Amiga), RA (from Real Audio), and VOC (from Creative Labs).

# CHAPTER 26 Multimedia Applications

> NOTE
> To learn more about the technical details of audio formats, read Chris Bagwell’s Audio Format FAQ at http://home.sprynet.net/-cbagwell/audio.html.

Red Hat Linux also offers utilities for converting sound files from one format to another. Conversion utilities come in handy when you want to use a sound in a format not accepted by your current application of choice. A repository of conversion utilities resides at http://biblio.org/pub/linux/apps/sound/convert/INDEX.html and includes MP3 and music CD-oriented utilities not found in Red Hat. You’ll have to know how to compile and install from source, however, you see something useful, you have to look at http://www.rmpfind.net/ to locate a binary RPM if you don’t feel up to the task.

Red Hat provides SoX, a self-described sound translator that will convert music between the AIFF, AU, VAR, DAT, OGG, and WAV formats, among others. It can also be used to change many other parameters of the sound files.

Timidity is a MIDI to WAV converter and player. If you're interested in MIDI and musical instruments, Timidity is a handy application; it handles karaoke files as well, displaying the words to accompany your efforts at singing.

# Music Players

Red Hat provides several music players. One of the most popular is Xmms, Winamp clone, which can play only music, but MPEG1/2/3, as Xmms supports a number of plug-ins that can add dancing, lighted oscilloscope-like displays, redirect its output to other devices, support unusual file formats, sync animations to the music, and otherwise increase its peak gain exponentially.

Kmid is a karaoke player and MIDI mapper, Kmid mappers enable you to map MIDI channels to the synthesizer instruments you want to control. If you enjoy karaoke, Kmid will also enable you to change the tempo of songs without changing the pitch, and permits the organization of your songs into collections with a selectable player mode.

Kscd is a KDE CD player that’s designed to play music from CDs in your computer’s drive. It features automatic access to the Internet CD Database (CDDB) so that the artist’s information and the name of the song can be displayed for you.

# Streaming Audio

Streaming audio is popular for playing games, listening to Internet radio, and other online audio content. Streaming audio is designed to produce an uninterrupted sound output, but it requires the system to perform a “juggling act.” Essentially, the system’s audio buffer is continually filled with audio information, which is fed to the buffer through the system’s Internet connection. To serve and connection connection capabilities, rate of input may vary. Because audio is used at a constant rate, streaming audio is to always keep the buffer full, although you might not be able to fill it at a constant rate.

Streaming audio is handled in Red Hat Linux in the .m3u format. The MPEG formats are also used for streaming audio. Red Hat doesn't provide any applications that use streaming audio, however. one is the Real Audio. A repository of conversion utilities resides at http://biblio.org/pub/linux/apps/sound/convert/INDEX.html and includes MP3 and music CD-oriented utilities not found in Red Hat. You’ll have to know how to compile and install from source, however, you see something useful, you have to look at http://www.rmpfind.net/ to locate a binary RPM if you don’t feel up to the task.

Red Hat provides SoX, a self-described sound translator that will convert music between the AIFF, AU, VAR, DAT, OGG, and WAV formats, among others. It can also be used to change many other parameters of the sound files.

Timidity is a MIDI to WAV converter and player. If you're interested in MIDI and musical instruments, Timidity is a handy application; it handles karaoke files as well, displaying the words to accompany your efforts at singing.

# Music Players

Red Hat provides several music players. One of the most popular is Xmms, Winamp clone, which can play only music, but MPEG1/2/3, as Xmms supports a number of plug-ins that can add dancing, lighted oscilloscope-like displays, redirect its output to other devices, support unusual file formats, sync animations to the music, and otherwise increase its peak gain exponentially.

Kmid is a karaoke player and MIDI mapper, Kmid mappers enable you to map MIDI channels to the synthesizer instruments you want to control. If you enjoy karaoke, Kmid will also enable you to change the tempo of songs without changing the pitch, and permits the organization of your songs into collections with a selectable player mode.

Kscd is a KDE CD player that’s designed to play music from CDs in your computer’s drive. It features automatic access to the Internet CD Database (CDDB) so that the artist’s information and the name of the song can be displayed for you.

# Streaming Audio

Streaming audio is popular for playing games, listening to Internet radio, and other online audio content. Streaming audio is designed to produce an uninterrupted sound output, but it requires the system to perform a “juggling act.” Essentially, the system’s audio buffer is continually filled with audio information, which is fed to the buffer through the system’s Internet connection. To serve and connection connection capabilities, rate of input may vary. Because audio is used at a constant rate, streaming audio is to always keep the buffer full, although you might not be able to fill it at a constant rate.

Streaming audio is handled in Red Hat Linux in the .m3u format. The MPEG formats are also used for streaming audio. Red Hat doesn't provide any applications that use streaming audio, however. one is the Real Audio. A repository of conversion utilities resides at http://biblio.org/pub/linux/apps/sound/convert/INDEX.html and includes MP3 and music CD-oriented utilities not found in Red Hat. You’ll have to know how to compile and install from source, however, you see something useful, you have to look at http://www.rmpfind.net/ to locate a binary RPM if you don’t feel up to the task.

Red Hat provides SoX, a self-described sound translator that will convert music between the AIFF, AU, VAR, DAT, OGG, and WAV formats, among others. It can also be used to change many other parameters of the sound files.

Timidity is a MIDI to WAV converter and player. If you're interested in MIDI and musical instruments, Timidity is a handy application; it handles karaoke files as well, displaying the words to accompany your efforts at singing.

# Music Players

Red Hat provides several music players. One of the most popular is Xmms, Winamp clone, which can play only music, but MPEG1/2/3, as Xmms supports a number of plug-ins that can add dancing, lighted oscilloscope-like displays, redirect its output to other devices, support unusual file formats, sync animations to the music, and otherwise increase its peak gain exponentially.

Kmid is a karaoke player and MIDI mapper, Kmid mappers enable you to map MIDI channels to the synthesizer instruments you want to control. If you enjoy karaoke, Kmid will also enable you to change the tempo of songs without changing the pitch, and permits the organization of your songs into collections with a selectable player mode.

Kscd is a KDE CD player that’s designed to play music from CDs in your computer’s drive. It features automatic access to the Internet CD Database (CDDB) so that the artist’s information and the name of the song can be displayed for you.

# Streaming Audio

Streaming audio is popular for playing games, listening to Internet radio, and other online audio content. Streaming audio is designed to produce an uninterrupted sound output, but it requires the system to perform a “juggling act.” Essentially, the system’s audio buffer is continually filled with audio information, which is fed to the buffer through the system’s Internet connection. To serve and connection connection capabilities, rate of input may vary. Because audio is used at a constant rate, streaming audio is to always keep the buffer full, although you might not be able to fill it at a constant rate.

Streaming audio is handled in Red Hat Linux in the .m3u format. The MPEG formats are also used for streaming audio. Red Hat doesn't provide any applications that use streaming audio, however. one is the Real Audio. A repository of conversion utilities resides at http://biblio.org/pub/linux/apps/sound/convert/INDEX.html and includes MP3 and music CD-oriented utilities not found in Red Hat. You’ll have to know how to compile and install from source, however, you see something useful, you have to look at http://www.rmpfind.net/ to locate a binary RPM if you don’t feel up to the task.

Red Hat provides SoX, a self-described sound translator that will convert music between the AIFF, AU, VAR, DAT, OGG, and WAV formats, among others. It can also be used to change many other parameters of the sound files.

Timidity is a MIDI to WAV converter and player. If you're interested in MIDI and musical instruments, Timidity is a handy application; it handles karaoke files as well, displaying the words to accompany your efforts at singing.

## Viewing and Video

To determine which chipset your card has, use the lspci command to list the PCI device, find the TV listing, and look for the chipset that uses. For example, the lspci output for your computer shows:

```
# lspci
00:00.0 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
→System Controller (rev 13)
00:01.0 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
AGP Bridge
00:07.0 ISA bridge: VIA Technologies, Inc. VT82C686 [Apollo Super]
→ (rev 40)
00:07.1 IDE interface: VIA Technologies, Inc. VT82C586 PIPC Bus Master
→ (rev 6)
00:07.2 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.3 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.4 SMBus: VIA Technologies, Inc. VT82C686 [Apollo Super AC]
→ (rev 40)
00:09.0 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
00:0b.0 Multimedia video controller: Broadtree Corporation Bt878 Video Capture
→ (rev 02)
00:0b.1 Multimedia video controller: Broadtree Corporation Bt878 Audio Controller
→ (rev 02)
00:dc.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029 (AS)
00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394
→ Controller
00:11.0 Network controller: Standard Microsystems Corp [SMC]
→ SMC2682W EZConnect
01:05.0 VGA compatible controller: NVIDIA Corporation NV15 [GeForce 2 Ti]
→ (rev a4)
```

To determine which chipset your card has, use the lspci command to list the PCI device, find the TV listing, and look for the chipset that uses. For example, the lspci output for your computer shows: Here, the lines listing the multimedia video controller and multimedia controller say say that our TV board uses a Broadtree Bt878 Video Capture chip and a Broadtree Bt878 Audio
