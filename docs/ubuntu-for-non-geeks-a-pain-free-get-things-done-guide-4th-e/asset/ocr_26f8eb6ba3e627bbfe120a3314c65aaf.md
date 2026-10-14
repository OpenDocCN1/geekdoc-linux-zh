# Converting Audio File Formats

As I pointed out at the beginning of the chapter, there may be some points of incompatibility when it comes to certain audio file formats, your hardware, and Ubuntu. Fortunately, SoundConverter (shown in Figure 15-9) makes it easy to convert Ogg Vorbis files to MP3 format, or vice versa. It can also convert AAC files to MP3 or Ogg Vorbis format, if that is of interest to you. Because SoundConverter does not come bundled with Ubuntu, you will have to install it. To do so, just run the Ubuntu Software Center, search for soundconverter, and install the application.

![](bbox=[0.25, 0.31, 0.68, 0.68])

Figure 15-9: Converting audio file formats with SoundConverter

To use SoundConverter, just select Applications ▸ Sound & Video ▸ Sound Converter. Once SoundConverter starts, add the songs you want to convert to the main pane by clicking either the Add File or Add Folder button. You can also drag audio files from your Music folder (or wherever else you store them).

Once you’ve chosen the files to convert, you need to choose which format to convert them to. You can do this by selecting Edit ▸ Preferences and then making your choice in the Preferences window (Figure 15-10). While you’re there, it is also a good idea to tell SoundConverter to place your converted files in a location other than the folder where the original files are stored. Doing this prevents having to deal with duplicates in Linux audio playback applications that automatically scan your Music folder, such as Rhythmbox. You might also want to check the Create subfolders box to keep things organized.

Once you have set things up and are ready to convert, click Close in the Preferences window, and then click Convert in the main window. SoundConverter will then begin doing its stuff.