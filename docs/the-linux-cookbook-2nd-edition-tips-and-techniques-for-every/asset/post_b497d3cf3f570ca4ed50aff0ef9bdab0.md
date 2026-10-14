
⇒ Here are two ways to use this.

- To add an “underwater” flange to the file `old.wav` and write the output to `new.wav`, type:

  ```
  $ sox old.wav new.wav flanger .5 .5 .4 .5 1 -t
  ```

- To add a flange that sounds somewhat like a “wah-wah” effects pedal to the file `old.wav` and write the output to `new.wav`, type:

  ```
  $ sox old.wav new.wav flanger .5 .5 .5 1 2 -t
  ```

## 23.2.6 Adding Phase to a Sound File

The “phaser” effect adds phase to a sound file. It takes the same arguments as the “flanger” effect.

⇒ Here are two ways to use this.

- To add a phase to the file `old.wav` and write the output to `new.wav`, type:

  ```
  $ sox old.wav new.wav phaser 1 .5 4 .5 1 -s
  ```

- To add a phased “breathing” effect to the file `old.wav` and write the output to `new.wav`, type:

  ```
  $ sox old.wav new.wav phaser .5 .5 .5 .9 .5 -t
  ```

**NOTES:** Using a decay greater than .5 may result in feedback.

## 23.2.7 Adding Chorus to a Sound File

To add a chorus effect to a sound file, use “chorus.” Its options are the “gain-in” and “gain-out” of the volume, the delay and decay in milliseconds, the speed in Hertz, and the depth of the chorus in milliseconds. Specify either `-s` or `-t` for sinusoidal or triangular modulation.

⇒ Here are two ways to use this.

- To add a 100 millisecond chorus to the file `old.wav` and write the output to `new.wav`, type:

  ```
  $ sox old.wav new.wav chorus 1 .5 100 1 1 1 -t
  ```

- To add a deep, “alien-sounding” chorus to the file `old.wav` and write the output to `new.wav`, type:

  ```
  $ sox old.wav new.wav chorus 1 .5 100 1 5 9 -t
  ```

## 23.2.8 Adding Vibro-Champ Effects to a Sound File

The “vibro” effect imitates the effect of the old Fender Vibro-Champ amplifier. Give the speed in Hertz (30 maximum) as an option, and specify an optional depth value between 0 and 1 (the default is .5).

⇒ Here are some ways to use this.

- To add a subtle Vibro-Champ effect to the file old.wav and write the output to new.wav, type:

  ```
  $ sox old.wav new.wav vibro 1 [RET]
  ```

- To add an effect of a maxed-out Vibro-Champ to the file old.wav and write the output to new.wav, type:

  ```
  $ sox old.wav new.wav vibro 30 1 [RET]
  ```

## 23.2.9 Reversing the Audio in a Sound File

Use the “reverse” effect to reverse the sound in a sound file.

⇒ To reverse the sound in the file old.wav and write the output to new.wav, type:

```
$ sox old.wav new.wav reverse [RET]
```

## 23.3 Converting Sound Files

Sound eXchange  
DEB: sox  
RPM: sox  
WWW: http://sox.sourceforge.net/  

Use sox for most sound-file conversions. Give as arguments the name of the input file and the name of the output file to write to; use a file name extension specifying the sound format for the output file (see Appendix B [Conventional File Name Extensions], page 723).

⇒ To convert the file new.wav to an audio CD format file, type:

```
$ sox new.wav new.cdr [RET]
```

This command writes a new file, new.cdr, in the audio CD format; the original file, new.wav, is not altered.

You may sometimes need to specify additional options, such as with raw audio files where the sampling rate and other properties must be specified.

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

## 23.3.1 Converting an MP3 File

Sound eXchange  
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

**NOTES:** The process of making an MP3 file from a raw audio or WAV format audio file is called encoding (or sometimes "ripping") an MP3 file; programs
