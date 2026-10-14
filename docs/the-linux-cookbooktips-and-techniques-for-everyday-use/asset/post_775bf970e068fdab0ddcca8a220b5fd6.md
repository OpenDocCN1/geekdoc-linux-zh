
xmms

Inspired by Winamp, XMMS is a popular, comprehensive audio player for X that features an array of plug-ins, support for many sound formats (including MP3 and Ogg Vorbis), and "skins" to change its look and feel; it can use FreeAmp themes as well—see previous listing for freeware. { ${fDebian}} `xmms` { ${fWWW}}: http://www.xmms.org/

[<] [>]      [<<] [Up] [>>]                                      [Top] [Contents] [Index] [?]

## 23. Audio Compact Discs

Audio compact discs can be played on systems that have a CD-ROM drive and sound card installed. You can control playback of an audio CD in all the ways you can with a traditional CD player, except on a Linux system you control playback with software tools on the command line. There are tools for reading the audio data from a CD and writing it to a file (which you can later write to a CD-R disc, or convert to MP3 format).

Tools and techniques for manipulating CD-ROMs (data CDs) are in CD-ROMs.

+   23.1 Controlling CD Audio
+   Controlling CD audio.
+   23.2 Sampling Sound from a CD
+   Making a sample of an audio CD.
+   23.3 Writing an Audio CD-R
+   Writing a CD-R.
+   23.4 Other Audio CD Applications
+   More CD tools and applications.

### 23.1 Controlling CD Audio

```
@sf(Debian): `cdtool`
@sf(WWW): ftp://jaka.cerl.uiuc.edu/pub/tinsel/
```

These recipes describe various ways to play audio CDs using the command-line tools found in the `CDTOOL` suite. Other CD audio tools, including X clients, are listed in Other Audio CD Applications.

+   23.1.1 Playing an Audio CD
+   Playing an audio CD.
+   23.1.2 Pausing an Audio CD
+   Pausing an audio CD.
+   23.1.3 Stopping an Audio CD
+   Stopping an audio CD.
+   23.1.4 Shuffling Audio CD Tracks
+   Shuffling tracks.
+   23.1.5 Displaying Information about an Audio CD
+   Getting information on the current CD.
+   23.1.6 Ejecting an Audio CD
+   Ejecting a disc.

### 23.1.1 Playing an Audio CD

Use cdplay to play an audio CD in the CD-ROM drive; the sound is output through the speakers connected to the LINE OUT jack on your sound card. (You may need to use the audio mixer to adjust the volume level and other settings; see Adjusting the Audio Controls.)

- To play an audio CD, type:

```
$ cdplay RET
```

To begin with a particular track, give the number of the track as an argument.

- To play an audio CD, beginning with the third track, type:

```
$ cdplay 3 RET
```

To end with a particular track, give the number of the track as a second argument.

- To play an audio CD, beginning with the first track and ending with the fourth track, type:

```
$ cdplay 1 4 RET
```

- To play only the third track of an audio CD, type:

```
$ cdplay 3 3 RET
```

### 23.1.2 Pausing an Audio CD

Use cdpause to pause audio CD playback.

- To pause the current CD playback, type:

```
$ cdpause RET
```

Use cdplay to start playback at the point where it was paused; to restart the playback from the beginning.

use cdplay with `x` as an argument.

- To restart a paused CD, type:

```
$ cdplay RET
```

- To restart a paused CD from the beginning, type:

```
$ cdplay x RET
```

### 23.1.3 Stopping an Audio CD

To stop playback of an audio CD, use cdstop.

- To stop the current CD playback, type:

```
$ cdstop RET
```

### 23.1.4 Shuffling Audio CD Tracks

Use cdplay with the `shuffle` argument to play the CD tracks in random order.

- To shuffle CD playback, type:

```
$ cdplay shuffle RET
```

where scsibus is the number of the SCSI bus (0 for the primary bus), target is the SCSI target ID (usually a number from 1 to 6), and lun is its LUN number (most always 0).

Use the `speed` argument to set the speed factor for writing data: give `speed=2` to specify double speed or `speed=4` to specify quad speed.

Use the `-dummy` option to run with the drive laser turned off, so no actual burning takes place; this is useful when you are first using a CD-R drive and need to test your configuration to make sure you've got it right. Another useful option is `-v`, which gives a more verbose message output.

Give the names of the audio files to burn, in the order that they should appear on the disc, as arguments to the `-audio` option. The files are written in CD-DA CD audio format, and they should contain 16-bit stereo at 44,100 samples/second (the `.cdr` or `.cdda` files meet this criterion).

- To burn the file `symphony.cdr` to the disc in the CD-R drive whose target ID is 2 on the primary SCSI bus, type:

```
$ cdrecord dev=0,2,0 -audio symphony.cdr RET
```

- To burn all the files in the current directory ending with a `.cdr` extension at double speed to the CD-R drive whose target ID is 2 on the primary SCSI bus, and give verbose output, type:

```
$ cdrecord dev=0,2,0 speed=2 -v -audio *.cdr RET
```

- To run a test burn of the file `symphony.cdr` to the disc in the CD-R drive whose target ID is 6 (LUN 1) on the primary SCSI bus, type:

```
$ cdrecord dev=0,6,1 -dummy -audio symphony.cdr RET
```

When you use wildcards for files, as in the second-to-the-last example, the shell expands the files in alphabetical order. To write a group of tracks in a particular order without specifying all of their names as arguments, rename them so that their names begin with numbers that correspond to the order you want to write them in (see section Moving Files and Directories).

For example, if you have the three files `morning-song.cdr`, `midday-song.cdr`, and `evening-song.cdr`, and you want to write them in that order, rename the files to `01-morning-song.cdr`, `02-midday-song.cdr`, and `03-evening-song.cdr`; otherwise, if you specify them as `*.cdr`, the shell will sort their names so that they will be written to CD-R in the order of `evening-song.cdr`, `midday-song.cdr`, and `morning-song.cdr` ---exactly the opposite of what was intended!

To write a disc containing both data and audio tracks, first specify the file for the data track (it should contain a filesystem image in either ISO 9660 or Rock Ridge format), and then follow it with the `-audio` option and the names of the audio tracks to use. The resulting CD-R will be both mountable as a data CD and playable on audio CD players (the first track on the disc, the data track, will be skipped when playing the audio).
