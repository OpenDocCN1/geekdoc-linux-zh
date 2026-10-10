# Using CentOS

# FIGURE 7-7

Extract songs from music CDs and encode them using Sound Juicer.

![](bbox=[0.15, 0.19, 0.6, 0.47])

+   3.  Set the following Preferences:
+   	- **CD Drive** — If you have multiple CD drives, choose the one you want to extract from.
+   	- **Music Folder** — Choose the folder the music tracks will be written to. Make sure that the disk partition containing the folder has enough space for you to store your music collection. As I noted earlier, a separate partition is a good idea for a large collection.
+   	- **Track Names** — Here’s where you identify the names that will be used to store your music. The folder hierarchy is set to the artist’s name, followed by the Album title. So multiple albums by the same artist will be in the same folder. The tracks themselves, indicated by the “File name” box, are stored by track number and song title, separated by a dash. You can choose different ways of indicating the files and folder names used to store your music.
+   	- **Output Format** — This sets the type of encoding that is done to each track. Your choices are FLAC, Ogg Vorbis, and WAV. With a gstreamer-plugins-mp3 package installed, you should have the choice of MP3 as well. I normally use Ogg Vorbis because the quality is good and it takes less disk space. In cases in which I want higher-quality output (with some compression), I tend to use FLAC. Choose WAV to store the file without compression (highest quality, largest size).

+   4.  Close the Preferences window and select Extract from Sound Juicer. The tracks are extracted, encoded, and stored on your hard disk to the folder you selected.