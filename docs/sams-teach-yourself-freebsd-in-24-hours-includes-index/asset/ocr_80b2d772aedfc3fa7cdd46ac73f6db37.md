# Playing DVDs

It used to be only a pipe dream that users could watch DVD video discs under Linux or FreeBSD; however, this is no longer the case, thanks to the developers of a program called Ogle.

The first thing you need in order to run Ogle, naturally, is a DVD drive. FreeBSD will recognize most common IDE/ATA DVD drives as /dev/acd0, just as with regular CD-ROM drives.

Armed with this equipment, all you should need to do is install the Ogle port, which includes its GUI, available at /usr/ports/graphics/ogle-gui. (This port implicitly installs the command-line /usr/ports/graphics/ogle port.) Once this is done, type ogle to start up the Ogle GUI.

With the DVD you want to watch in the drive, use the menu command Open to open the device /dev/acd0. (You can also use the Open dialog to open the contents of a VIDEO_TS folder, if you have copied the contents of a DVD to your hard drive, by specifying /path/to/VIDEO_TS as the target.) You might also be able to use the Open Disc menu command, which will automatically open the DVD in the drive without your having to specify the device name.

Ogle has many features that you are probably accustomed to using in standard DVD players, including menus, full-screen mode, title/chapter search, and a number of high-quality audio formats. However, a few features are missing at this time, such as the ability to seek back and forth through the video with a slider, and reverse playback. Ogle will undoubtedly continue to evolve however; and in the meantime, the basics ought to work quite well.

# Summary

In this hour, you learned how to configure sound support in FreeBSD by adding the pcm device driver to the kernel, and also creating device nodes for sound support. We then looked at a small sample of the sound applications available for FreeBSD.

Multimedia hardly stops with sound playback, however; and so we looked at the basics of CD burning, MPEG and DivX video playback, and DVD playback—all features that are central to multimedia as we are accustomed to it today.