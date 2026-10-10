
Most popular sound devices for the PC, whether on separate cards or built into your computer’s motherboard, will be automatically detected when a Red Hat Linux system boots up. Appropriate modules will be loaded, so you can immediately begin using your sound card.

In the current Fedora release, PulseAudio (`www.pulseaudio.org`) replaced Advanced Linux Sound Architecture (ALSA) as the sound system used with Fedora. PulseAudio basically provides the interfaces between audio applications and your sound card. By incorporating plug-ins, PulseAudio lets you use applications that were designed to be used with ALSA.

The alsa-utils RPM package contains the commands and configuration files you can use to tune your sound card and adjust audio levels. Other friendly graphical tools have been added by the GNOME and KDE projects for managing sound.

After your sound card is working and audio levels are adjusted, you can use any of the dozens of audio applications that come with Linux with your sound card. Those applications include music players, video players, video conferencing applications, games, and audio recorders, to name a few.

As for audio content, the following list describes the types of audio content you might want to play, which players can be used for each type of content, and whether or not the software comes with Fedora or RHEL. (If not, I describe where you can get software to play that content and issues associated with getting and using that software.)

- **Music CDs (CDDA)** — Commercial music CDs are nearly all stored in the Compact Disc Digital Audio system (CDDA). Fedora and RHEL applications that can play music CDs include CD Player (gnome-cd) and KsCD (kscd). Rhythmbox can play music CDs, as well as import songs to your hard disk (using Sound Juicer) so you can manage your music from one location. Other applications in Fedora that can play audio files from CDs include xmms and grip.

- **Ogg Vorbis Audio** — If you are compressing and storing music from scratch, Ogg Vorbis is probably the best choice if you want to avoid completely any royalty issues. The libvorbis codec is included with Fedora and RHEL and makes it possible to play audio encoded in Ogg Vorbis format in a variety of Linux music players, including xmms, Rhythmbox, ogg123, and many others. The vorbis-tools package also includes utilities for encoding (oggenc) and decoding (oggdec) Ogg Vorbis content to or from WAV and raw music formats. The Xiph.org Foundation develops both Ogg Vorbis audio formats and Theora video formats.

- **MP3 Audio** — MPEG Audio Layer 3 (MP3) has become the standard format for storing audio files that are transmitted over computer networks (such as the Internet). Because of licensing issues associated with distributing MP3 players, Red Hat does not include codecs needed to encode or decode MP3 files in any of its distributions. However, Fedora does give you the opportunity to download free, legal MP3 decoders from Fluendo (as described earlier in this chapter).

Another way to get MP3 support, which may not be legal where you are, is to install the xmwms-mp3 package, which contains software needed by Linux audio players to play MP3 audio files with the xmms music player. You need the lame package to create compressed audio files from WAV, AIFF, or raw audio files that play on MP3 players. Many use the mpg321 command-line MP3 player, which is available in the mpg321 package. (All of these packages are available from the Linux.org RPM repository. See Chapter 5 on installing software from the Linux.org repository.)

- **FLAC Audio** — FLAC is an open source lossless audio format. *Lossless* means that it compresses the audio as much as possible without losing audio sound quality. In comparing the same song compressed in Ogg Vorbis and FLAC (using default settings), FLAC files were on average about six times the size of the Ogg Vorbis files.

Many of the same applications that can play Ogg Vorbis files can play FLAC files as well. Rhythmbox, ogg123, and xmms can all play FLAC files. You can encode FLAC audio using Sound Juicer or the `flac` command, among others.

- **Other Audio Formats** — While the audio formats mentioned previously are the most common ones used for music files today, there are other audio formats you may want to play from Linux. Refer to the description of the `sox` utility for several audio formats that are supported by that utility. Use the `play` command (which comes with the `sox` package) or `aplay` (which is in the `alsa-utils` package) to play content stored in any of those supported formats.

Audio formats that are sometimes included with video files are described in the section on video players later in this chapter. For an official description of which contentious multimedia encoding software (and other software) Fedora doesn’t include, refer to the Fedora Project Forbidden Items page (http://fedoraproject.org/wiki/ForbiddenItems).

## Configuring a sound card

Configuring a sound card in Linux consists primarily of having the right modules load (which usually happens automatically at boot time) and then using the sound utilities you choose (such as alsamixer or amixer) to adjust the settings for the sound card. Today’s sound cards often have more than the old Mic-In, Line-In, Speaker-out, and Joystick ports. So when you go to adjust your audio levels, there are more items you need to learn about.

### Sound card features

Sound cards can pack an amazing number of features these days. Most PCs these days come with built-in sound support. Here are some of the features you should look for if you want to purchase a sound card separately:

- **Sound recording and playback quality** — When you record and play back audio, quality and file size are determined, in part, by word length (the number of bits that are used to hold a numerical value) and sample rates. Typical word lengths include 8-bit (less popular), 16-bit, or 24-bit digital sizes. To convert the sound, the board samples the sound in waves from 8 kHz to 96 kHz, or 8,000 to 96,000 times per second. (Of course, the higher the sampling, the better the sound and larger the output.)

- **Full-duplex support** — This allows for recording and playback to occur at the same time. This is particularly useful for bidirectional Internet communication or simultaneous recording and playback.

- **PCI or USB interface** — Most people purchase a PCI sound card to put in the case of their desktop system, when sound ports on the computer's motherboard are not sufficient. However, if you are using a PC (such as a Shuttle) with limited slots or a laptop, there are USB sound cards that are supported in Linux.

Several different ports on the board enable you to connect input/output devices. These ports can include some or all of the following:

- **Line-In (blue)** — Connects an external CD player, cassette deck, synthesizer, MIDI, Disc, or other device for recording or playback. If you have a television card, you might also patch that card's line out to your sound card's line in.
- **Microphone (red)** — Connects a microphone for audio recording or communications.
- **Headphone/Line-Out/Speaker Out (green)** — Connects speakers, headphones, or a stereo amplifier. (On sound cards I've tested, this is marked as Headphone in mixer utilities.)
- **Joystick/MIDI (15-pin connector)** — Connects a joystick for gaming or MIDI devices. (Some sound cards no longer have these ports because they are now available from most motherboards.)
- **Digital out (orange)** — A digital out connector can be used to connect a digital audio tape (DAT) device or CD recordable (CD-R) device.
- **Rear out (black)** — Can be used to deliver audio output to powered speakers or an external amplifier.
- **Internal CD Audio** — This internal port connects the sound card to your computer's internal CD-ROM drive (this port isn't exposed when the board is installed).

For some sound applications, you need to identify the device files used to communicate with the sound card and other sound hardware. The devices that the audio programs use to access audio hardware in Fedora and RHEL include:

- `/dev/audio`, `/dev/audio1` — Devices that are compatible with Sun workstation audio implementations (audio files with the .au extension).
- `/dev/cdrom` — Device representing your first CD-ROM drive. (Additional CD-ROM drives are located at `/dev/cdzrom1`, `/dev/cdzrom2`, and so on.)
- `/dev/dsp`, `/dev/dsp1` — Digital sampling devices, which many audio applications identify to access your sound card.
- `/dev/mixer`, `/dev/mixer1` — Sound-mixing devices.
