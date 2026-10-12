Freeamp is not part of the Red Hat Linux distribution. The freeamp player is available from the FreeAmp Home Page (www.freeamp.org), although I recommend that you type `rpmfind freeamp` to find an RPM package of freeamp from a Red Hat mirror site. To start freeamp to run on your X display, type the following:

```
```
$ freeamp &
```
```

Figure 8-4 shows the freeamp display window.

![](bbox=[0.06, 0.23, 0.42, 0.34])

**Figure 8-4**: Use dials to adjust volume and to seek songs in freeamp.

Preferences for freeamp are stored in the `$HOME/.freeamp/preferences` file. Subdirectories to the .freeamp directory store information about your stored music, fonts, and themes used with the freeamp player.

You can also run freeamp in text mode. To do this, add the `-ui TextUI` option to the freeamp command line. However, you don't have to add the -ui options. If the DISPLAY variable is set, the X interface of freeamp is started; if DISPLAY is not set, freeamp starts in text mode.

The My Music Collection feature of freeamp lets you create and manage your own library of music. You can include MPEG-1 and MPEG-2 audio files. You can also save individual playlists. When you open a stored playlist, freeamp finds the files you listed and plays them back in the order you specified.

To play a SHOUTcast/http stream or an RTP/multicast stream, specify a URL on the freeamp command line. For example, the first command line that follows represents a SHOUTcast stream and the second line represents a multicast stream:

```
```
$ freeamp http://123.48.23.4:8000
$ freeamp rtp://132.43.21.4:4420
```
```

You can change the look and the arrangement of buttons on your freeamp window by changing the theme. Click the options button, click the Themes tab (from the Preferences window), select a theme from the Theme Selection area, and click OK. The new theme is immediately applied to freeamp.

# # Using MIDI audio players

MIDI stands for Musical Instrument Digital Interface. MIDI files are created from synthesizers and other electronic music devices. MIDI files tend to be smaller than other kinds of audio