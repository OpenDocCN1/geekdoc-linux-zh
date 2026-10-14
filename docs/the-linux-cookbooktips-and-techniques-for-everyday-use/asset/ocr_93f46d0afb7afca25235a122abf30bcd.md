+   • To select the microphone jack as the recording source, type:

```
$ amixer set MIC capture RET
```

NOTE: You can have only one group selected for capture at a time, and when you select a group as an input source for recording, you are simply turning the microphone or other input on; recording does not occur until you use a recording tool.

# 22.3 Playing a Sound File

@sf(Debian): `sox'
@sf(WWW): http://home.sprynet.com/~cbagwell/sox.html

The play tool distributed with sox (a sound file translation tool) can recognize and play many audio formats, including WAV, VOC, AU, AIFF, and SND format files, as well as audio CD-format files and various raw binary files; just about the only common audio formats it can't handle are MP3 and MIDI files, which are discussed in the sections to follow.

+   • To play the file `pentastar.aiff', type:

```
$ play pentastar.aiff RET
```

NOTE: Before you begin playing sound, make sure you've set the master and PCM volume levels with the mixer (see section Adjusting the Audio Controls). The most common reason for no sound being produced when you try to play sound is not having the volume turned up!

ALSA comes with aplay, a tool for playing sound files that is similar to play, but does not recognize as many formats.

+   22.3.1 Playing an MP3 File    Playing MP3 files.
+   22.3.2 Playing a MIDI File    Playing MIDI files.