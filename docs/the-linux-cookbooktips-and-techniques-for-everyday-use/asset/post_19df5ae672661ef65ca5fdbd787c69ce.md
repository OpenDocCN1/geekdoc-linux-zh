
+   To burn the data track `band-info` and all the audio tracks in the current directory with a `.cdda` extension to the CD-R drive whose target ID is 2 on the primary SCSI bus, type:

```
$ cdrecord dev=0,2,0 band-info -audio *.cdda RET
```

> NOTE: When writing an audio CD, you should have as few processes running as possible. If cdrecord has to pause even momentarily to let the system shuffle other processes, the CD-R could be ruined! For this reason, it is advisable to avoid switching between consoles—or between windows, if running X—during the CD-R burning process.

## 23.4 Other Audio CD Applications

The following table lists some of the other available tools and applications that work on audio compact discs.

| TOOL | DESCRIPTION |
| dynamic | Project Dynamic is a tool for playing samples of audio CDs; it is distinctive in that it can play audio CDs backwards. {@sf{WWW}}: http://www.cse.unsw.edu.au/~flatmax/dynamic/ |
| workbone | An interactive CD player that can be used on the console or in X; it allows you to skip forward and backward through tracks as they are playing. |
| workman | A tool for playing audio CDs, with a graphical interface that looks like the front panel of a physical CD player. |
| xcdroast | XCDRoast is a graphical front-end to the cdrecord tool for use in X. {@sf{WWW}}: http://www.xcdroast.org/ |

## 24. Editing Sound Files

All kinds of tools and applications exist to edit sound files. This chapter shows some of those tools, giving methods for for cutting and pasting sound files, applying effects and filters, and converting sound files between formats.

- 24.1 Working with Selections from Sound Files
  Working with selections from sound files.
- 24.2 Sound Effects
  Applying some command-line sound effects.
- 24.3 Converting Sound Files
  Converting sound files.
- 24.4 Other Tools for Sound Editing
  Different audio editing environments and tools.

### 24.1 Working with Selections from Sound Files

```
@sf(Debian): `snd`
@sf(WWW): http://ccrma-www.stanford.edu/CCRMA/Software/snd/
```

Snd is a sound-file editing environment for X, and aims to be for sound what Emacs is to text. (And it uses Emacs-style key bindings.)

You'll find a complete manual for it in the `/usr/doc/snd` directory; this section explains how to use Snd to work with selections from sound files.

To open a sound file in Snd, give the name of the file to be opened as an argument to snd.

- To open the sound file `mixdown.wav` in Snd, type:

```
$ snd mixdown.wav RET
```

This command starts Snd with a WAV file called `mixdown.wav`:

### 24.1.3 Mixing Sound Files Together

To mix different audio files together as multiple tracks in Snd, choose Mix from the File menu and specify the files to use as the individual tracks.

### 24.2 Sound Effects

```
@sf(Debian): `sox`
@sf(WWW): http://home.sprynet.com/~cqawell/sox.html
```

The "Sound eXchange" tool, sox, is a sound sample translator. It reads sound as files or standard input and outputs the sound either to a file or standard output, while translating in between. You can use sox to convert sound files between formats or process sounds with special effects. This section describes some of the special effects you can apply to sound files with sox.

When applying an effect, the original file is never altered. You must specify an output file, or use '-' to indicate the standard output, specifying the output format with `-t`. You can only apply one effect with each sox command; thus, to add both echo and reverb to a sound file, you would need to issue two sox commands.

The amount and levels applied for each effect will vary with every situation. As such, consider the following recipes guidelines only for using the options; you will probably end up experimenting a bit to get your intended effect for any particular sound file.

Almost all of the sound effects are applied by specifying the input and output file arguments, followed by the name of the effect to use and any options the effect takes (with notable exceptions, like the `-v` option for changing the amplitude of a file).

NOTE: For more information on the effects Sox can do, see the various files in `/usr/doc/sox/`, and read the soxman page (see section Reading a Page from the System Manual).

+   24.2.1 Changing the Amplitude of a Sound File  Changing the amplitude of a sound file.
+   24.2.2 Changing the Sampling Rate of a Sound File  Changing a sound file's sampling rate.
+   24.2.3 Adding Reverb to a Sound File  Adding reverb to a sound file.
+   24.2.4 Adding Echo to a Sound File  Adding echo to a sound file.
+   24.2.5 Adding Flange to a Sound File  Adding flange to a sound file.
