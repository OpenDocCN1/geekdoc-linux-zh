To reduce the noise, you can send the file through a low-pass filter. Here’s an example:

```
$ sox file1.voc file2.voc lowp 2200
```

For more information on SoX and to get the latest download, go to the SoX — Sound eXchange home page (http://sox.sourceforge.net).

# ## Extracting and Encoding Music

Storing your music collection on your computer’s hard disk makes it easy to manage and play your music. Using ripping software, you can copy music tracks from a Music CD to your hard disk. As part of the same process (or as a separate step), you can encode each track into another form. That encoding is usually done to reduce the size of the audio files.

Tools that come with CentOS for extracting audio tracks from CDs and copying them to your hard disk include the **Sound Juicer** window and the `cdparanoia` command. Encoders that come with CentOS that are typically used for encoding music include `oggenc` and `flac`. Although encoding is often done as part of the extraction process (e.g., in Sound Juicer), I give an example of how to use `oggenc` to encode WAV files to Ogg Vorbis format on the command line.

# ### Extracting Music CDs with Sound Juicer

*Sound Juicer* is an intuitive graphical tool for extracting music tracks from commercial music CDs. It can read the tracks of a Music CD, get CD album, artist, and track information about the CD (provided you have an Internet connection), and save the tracks to your hard disk. During that process, you can also have Sound Juicer encode the tracks in Ogg Vorbis, FLAC, or Voice-quality WAV format.

**NOTE** You can use the Flueno codecs, described earlier in this chapter, to get support for MP3 playback. There is a fee for purchasing MP3 decoding software.

To start Sound Juicer, select **Applications** > **Sound & Video** > **Sound Juicer Audio CD Extractor**. (Or you can launch it by typing `sound-juicer` or by selecting **Sound Juicer** > Import Audio CD from Rhytmbox.) Figure 7-7 shows an example of the Sound Juicer window.

Here’s how to use Sound Juicer to extract songs from an audio CD and encode them to any supported encoding type:

+   1.  After starting Sound Juicer, insert an audio CD into your computer’s CD drive and select Re-read on the Sound Juicer window. (If another audio player starts up, you can close it.)
+   2.  Select **Edit** > **Preferences**. The Preferences window appears.