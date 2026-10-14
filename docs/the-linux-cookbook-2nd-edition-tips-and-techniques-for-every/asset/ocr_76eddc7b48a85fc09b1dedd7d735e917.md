**NOTES:** You can have only one group selected for capture at a time, and when you select a group as an input source for recording, you are simply turning the microphone or other input on; recording does not occur until you use a recording tool.

# ## 21.2 Playing a Sound File

SOund eXchange

DEB: sox
RPM: sox
WWW: http://sox.sourceforge.net/

The play tool distributed with “SOund eXchange” (a sound file translation tool) can recognize and play many audio formats, including OGG, WAV, VOC, AU, AIFF, and SND format files, as well as audio CD-format files and various raw binary formats. Just about the only common audio formats it can’t handle are MIDI and MP3, which are discussed in the sections to follow. Give the name of a file as an argument to play.

⇒ To play the file sousa.aiff, type:

```shell
$ play sousa.aiff RET
```

**NOTES:** Before you begin playing sound, make sure you’ve set the master and PCM volume levels with the mixer (see Recipe 21.1 [Adjusting the Audio Controls], page 463). The most common reason for no sound being produced when you try to play sound is not having the volume turned up!

ALSA comes with aplay, a tool for playing sound files that is similar to play but does not recognize as many formats.

# ### 21.2.1 Playing an Ogg File

Ogg123
DEB: vorbis-tools
RPM: vorbis-tools
WWW: http://www.vorbis.com/

Use ogg123 to play Ogg Vorbis files, giving the name of the file as an argument.

⇒ To play the file track1.ogg, type:

```shell
$ ogg123 track1.ogg RET
```