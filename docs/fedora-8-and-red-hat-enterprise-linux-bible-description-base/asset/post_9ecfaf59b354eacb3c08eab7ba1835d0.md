
## Chapter 8: Music, Video, and Images in Linux

337

| File Extension or Pseudonym | Description | File Extension or Pseudonym | Description |
| :--- | :--- | :--- | :--- |
| .dat | Text data files, which contain a text representation of sound data. | .gsm | Lossy Speech Compression (GSM 06.10), used to shrink audio data in voice mail and similar applications. |
| .hcom | Macintosh HCOM files. | .maud | Amiga format used to produce sound that is 8-bit linear, 16-bit linear, A-law, and u-law in mono or stereo. |
| .ogg | Ogg Vorbis compressed audio, which is best used for compressing music and streaming audio. | .osdsp | Pseudo file, used to open the OSS /dev/dsp file and configure it to use the data type passed to sox. Used to either play or record. |
| .prc | Psion record.app format, newer than the WWE format. | .sf | IRCAM sound files, used by Csound package and MixView sample editor. |
| .sph | Speech audio SPHERE (Speech Header Resources) format from NIST (National Institute of Standards and Technology). | .smp | Sample/Vision files from Turtle Beach, used to communicate with different MIDI samplers. |
| .sunau | Pseudo file, used to open a `/dev/audio` file and set it to use the data type being passed to sox. | .txw | Yamaha TX-16W from a Yamaha sampling keyboard. |
| .vms | Used to compress speech audio for voice mail and similar applications. | .voc | Sound Blaster VOC file. |
| .wav | Microsoft WAV RIFF files. This is the native Microsoft Windows sound format. | .wve | 8-bit, A-law, 8 kHz sound files used with Psion Palmtop computers. |
| .raw | Raw files (contain no header information, so sample rate, size, and style must be given). | .ub, .sb, .uw, .sw, .ul, .al, .lu, .la, .sl | Raw files with set characteristics: ub is unsigned byte; sb is signed byte; uw is unsigned word; sw is signed word; and ul is ulaw. |

**TIP:** Type `sox -h` to see the supported audio types. This also shows supported options and effects.

If you are not sure about the format of an audio file, you can add the `.auto` extension to the filename. This triggers `sox` to guess what kind of audio format is contained in the file. The `.auto` extension can be used only for the input file. If `sox` can figure out the content of the input file, it translates the contents to the sound type for the output file you request.

In its most basic form, you can convert one file format (such as a WAV file) to another format (such as an AU file) as follows:

```
$ sox file1.wav file1.au
```

To see what `sox` is doing, use the `-V` option. For example:

```
$ sox -V file1.wav file1.voc

sox: Reading Wave file: Microsoft PCM format, 2 channel, 44100 samp/sec
sox: 176400 byte/sec, 4 block align, 16 bits/samp, 50266944 data bytes
sox: Input file: using sample rate 11025
            size bytes, style unsigned, 1 channel
sox: Input file1.wav: comment "file1.wav"

sox: Output file1.voc: using sample rate 44100
            size shorts, encoding signed (2's complement), 2 channels
sox: Output file: comment "file1.wav"
```

You can apply sound effects during the `sox` conversion process. The following example shows how to change the sample rate (using the `-r` option) from 10,000 Hz to 5,000 Hz:

```
$ sox -r 10000 file1.wav -r 5000 file1.voc
```

To reduce the noise, you can send the file through a low-pass filter. Here’s an example:

```
$ sox file1.voc file2.voc lowp 2200
```

For more information on SoX and to get the latest download, go to the SoX — Sound eXchange— home page (http://sox.sourceforge.net).

### Extracting and encoding music

Storing your music collection on your computer’s hard disk makes it easy to manage and play your music. Using ripping software, you can copy music tracks from a music CD to your hard disk. As part of the same process (or as a separate step), you can encode each track into another form. That encoding is usually done to reduce the size of the audio files.

Tools that come with Fedora and RHEL for extracting audio tracks from CDs and copying them to your hard disk include the Sound Juicer window and the `cdparanoia` command. Encoders that come with Fedora and RHEL that are typically used for encoding music include oggenc and flac. Although encoding is often done as part of the extraction process (for example, in Sound Juicer), I give an example of how to use oggenc to encode WAV files to Ogg Vorbis format on the command line.

### Extracting music CDs with Sound Juicer

Sound Juicer is an intuitive graphical tool for extracting music tracks from commercial music CDs. It can read the tracks of a music CD; get CD album, artist, and track information about the CD (provided you have an Internet connection); and save the tracks to your hard disk. During that process, you can also have Sound Juicer encode the tracks in Ogg Vorbis, FLAC, or Voice-quality WAV format.

> NOTE: Sound Juicer requires the lame plug-in to do encoding that can be played in MP3 players. (Lame stands for "Lame ain't an MP3 encoder," so who am I to argue with that?) Anyway, the lame package contains the lame command-line encoder. The gstreamer-plugins-mp3 package, available from Lwna.org, includes the software needed to do lame encoding in Sound Juicer.

To start Sound Juicer, select Applications → Sound & Video → Sound Juicer CD Extractor. (Or you can launch it by typing sound-juicer or by selecting Music → Import Audio CD from Rhythmbox.) Figure 8-8 shows an example of the Sound Juicer window.

![](img/fb202c163797a743c3c6cf236316bc96_372_0.png)

Here’s how to use Sound Juicer to extract songs from an audio CD and encode them to any supported encoding type:

- 1. After starting Sound Juicer, insert an audio CD into your computer’s CD drive and select Re-read on the Sound Juicer window. (If another audio player starts up, you can close it.)
- 2. Select **Edit** → **Preferences**. The Preferences window appears, as shown in **Figure 8-8**.
- 3. Set the following **Preferences**:
    - **CD Drive** — If you have multiple CD drives, choose the one you want to extract from.
    - **Music Folder** — Choose the folder the music tracks will be written to. Make sure that the disk partition containing the folder has enough space for you to store your music collection. As I noted earlier, a separate partition is a good idea for a large collection.
    - **Track Names** — Here’s where you identify the names that will be used to store your music. The folder hierarchy is set to the artist’s name, followed by the Album title. So multiple albums by the same artist will be in the same folder. The tracks themselves, indicated by the File name box, are stored by track number and song title, separated by a dash. You can choose different ways of indicating the files and folder names used to store your music.
    - **Output** — This sets the type of encoding that is done to each track. Your choices are FLAC, Ogg Vorbis, and WAV. With a gstreamer-plugins-mp3 package installed, you should have the choice of MP3 as well. I normally use Ogg Vorbis because the quality is good and it takes less disk space. In cases where I want higher quality output (with some compression), I tend to use FLAC. Choose WAV to store the file without compression (highest quality, largest size).
- 4. Close the Preferences window and select **Extract** from Sound Juicer. The tracks are extracted, encoded, and stored on your hard disk to the folder you selected.

### Extracting and encoding music CDs from commands

Instead of using a graphical tool (such as Sound Juicer) to extract and encode your music CDs, you can use commands instead. The commands described here are available on most Linux systems, while those systems might tend to offer different graphical tools. Using these commands, you also have more flexibility in setting options to use for your encoding.

This procedure takes you through the process of extracting tracks from CD (**cdparanoia**) and encoding them to Ogg Vorbis (**oggenc**).

- 1. Create a directory to hold the audio files, and change to that directory. Make sure the directory can hold up to 660MB of data (or less if you are burning fewer songs). For example:

```
# mkdir /tmp/cd
# cd /tmp/cd
```
