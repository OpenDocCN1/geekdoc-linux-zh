
## Adjusting Volume

Ubuntu offers a handy utility that you can use to control the volumes for various outputs from your computer. For a simple master volume control, just click on the speaker icon in the top-right corner of the screen and move the slider up or down, as shown in Figure 7.1.

Alternatively you can control all the output volumes for the system to make sure that you have set everything to your taste, as shown in Figure 7.2. To access the volume control, right-click on the speaker icon and select Open Volume Control.

![](img/8f9e74e2b343ff525bebfb720a3d8441_184_0.png)

FIGURE 7.1 Control the master volume level with the volume slider.

![](img/8f9e74e2b343ff525bebfb720a3d8441_184_1.png)

FIGURE 7.2 Use the volume control to manage volume settings for all your sound output devices.

## Sound Formats

A number of formats exist for storing sound recordings. Some of these formats are associated with specific technologies, and others are used strictly for proprietary reasons. Ubuntu supports several of the most popular sound formats, including

- **raw (.raw)**—More properly known as *headerless format*, audio files using this format contain an amorphous variety of specific settings and encodings. All other sound files contain a short section of code at the beginning—a header—that identifies the format type.
- **MP3 (.mp3)**—A popular, but commercially licensed, format for the digital encoding used by many Linux and Windows applications. MP3 is not supported by any software included with Ubuntu (which advises you to use the open source Ogg-Vorbis format instead).
- **WAV (.wav)**—The popular uncompressed Windows audio-visual sound format. It is often used as an intermediate file format when encoding audio.
- **Ogg-Vorbis (.ogg)**—Ubuntu’s preferred audio encoding format. You enjoy better compression and audio playback, and freedom from lawsuits when you use this open-source encoding format for your audio files.

> **NOTE**
>
> Because of patent and licensing issues, Ubuntu has removed support for the MPEG, MPEG2, and MPEG3 (MP3) file formats in Ubuntu Linux. Although we cannot offer any legal advice, it appears that individuals using MP3 software are okay; it is just that Ubuntu cannot distribute the codec because it sells its distribution. It seems—at this point—perfectly all right for you to obtain an MP3-capable version of XMMS (for example), which is a Winamp clone that plays MPEG1/2/3 files. You can get XMMS directly from http://www.xmms.org/ because that group has permission to distribute the MP3 codec.
>
> You can also enable the MP3 codec within Ubuntu by downloading a plugin for GStreamer, the GNOME audio system. You do this by installing the `gstreamer0.10-plugins-ugly` package, which enables the MP3 codec in all the GNOME applications.

Ubuntu includes software (such as the sox command used to convert between sound formats) so that you can more easily listen to audio files provided in a wide variety of formats, such as AU (from NeXT and Sun), AIFF (from Apple and SGI), IFF (originally from Commodore’s Amiga), RA (from Real Audio), and VOC (from Creative Labs).

> **TIP**
>
> To learn more about the technical details of audio formats, read Chris Bagwell’s Audio Format FAQ at http://www.cnpbagwell.com/audio.html.

Ubuntu also offers utilities for converting sound files from one format to another. Conversion utilities come in handy when you want to use a sound in a format not accepted by your current application of choice. A repository of conversion utilities resides at http://ibiblio.org/pub/linux/apps/sound/convert/INDEX.html and includes MP3 and music CD-oriented utilities not found in Ubuntu. You have to know how to compile and install from source, however.

Ubuntu does provide sox, a self-described sound translator that converts music among the AIFF, AU, VOC, DAT, Ogg, WAV, and other formats. It also can be used to change many other parameters of the sound files.

Timidity is a MIDI-to-WAV converter and player. If you are interested in MIDI and musical instruments, Timidity is a handy application; it handles karaoke files as well, displaying the words to accompany your efforts at singing.

## Listening to Music

If you're anything like us, you might be a huge music fan. One of the downsides of having a fairly large music collection is the physical problem of having to store so many CDs. Wouldn't it be great if you could pack them all away somewhere, yet still have access to all the music when you want it? Some hi-fi manufacturers experimented with rather bulky jukeboxes that stored 250 CDs at once. The main downside with that was that finding a particular piece of music could take hours, having to cycle through each CD in the hope that it would match your mood.

Fortunately for you and me, Ubuntu is fantastic at working with CDs, even allowing you to rip all your CD collection into a vast searchable music library, letting you quickly create playlists and even giving you the ability to create your own customized CDs. Getting started couldn't be easier, mainly because Ubuntu comes preconfigured with everything you need to get started.

### RhythmBox

A standard CD player application was supplied in previous versions of Ubuntu, but this has now been dropped largely due to the fact that other applications made it redundant. In its place is RhythmBox, a useful application that does more than just play CDs. If you insert an audio CD into your computer, RhythmBox will appear and attempt to obtain information about the CD from the Internet service MusicBrainz. If it's successful, then you'll see the name of the CD appear in the left window of RhythmBox, as shown in Figure 7.3.

When you're ready to play your CD, simply click the name of the CD under the devices section and click the Play button, as shown in Figure 7.4. You can also define whether the CD should just repeat itself until stopped, or whether you want to shuffle the music (randomize the playlist).

Of course, just listening to your CDs doesn't really change anything; RhythmBox acts just like a regular CD player, allowing you to listen to specific tracks and define how you want to listen to your music by using playlists or sorting it by artists. The real fun starts when you click the Copy to Library button in your toolbar. RhythmBox then starts to extract, or
