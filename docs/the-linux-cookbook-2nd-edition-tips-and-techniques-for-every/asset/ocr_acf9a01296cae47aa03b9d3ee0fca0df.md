⇒ To convert all of the raw audio files in the current directory to audio CD format files, type:

```
$ for i in *.raw [RET]
{ [RET]
sox -s -w -c2 -r 44100 $i -x $i.cdr [RET]
} [RET]
```

This command writes all of the .raw files to new files of the same name but with a .cdr extension. You could then use cdrecord to burn an audio CD with the .cdr files (see Recipe 22.3 [Writing an Audio CD-R], page 482).

To convert a file to a particular format without using the standard extension, specify the format to write to with the -t option.

⇒ To convert the file new.wav to the audio CD format and write output to a file named cd-single, type:

```
$ sox new.wav -t cdr cd-single [RET]
```

# 23.3.1 Converting an MP3 File

SOund eXchange
DEB: sox
RPM: sox
WWW: http://sox.sourceforge.net/

Mpg123
DEB: mpg321
RPM: mpg321
WWW: http://mpg321.sourceforge.net/

To convert an MP3 file to another format, use mpg321 (or another command line MP3 player) to play the file to the standard output, and then use sox to read the resultant raw audio and write it to another file with a specified input format.

⇒ To convert the MP3 file remix.mp3 to a WAV file remix.wav, type (all on one line):

```
$ mpg321 -b 10000 -s remix.mp3 | sox -t raw -r 44100 -s -w -c 2 - remix.wav [RET]
```

NOTES: The process of making an MP3 file from a raw audio or WAV format audio file is called encoding (or sometimes "ripping") an MP3 file; programs