+   To add an effect of a maxed-out Vibro-Champ to the file `old.wav` and write the output to `new.wav`, type:

```
$ sox old.wav new.wav vibro 30 1 RET
```

# 24.2.9 Reversing a Sound File

Use the `reverse` effect to reverse the sound in a sound file.

+   To reverse the sound in the file `old.wav` and write the output to `new.wav`, type:

```
$ sox old.wav new.wav reverse RET
```

# 24.3 Converting Sound Files

@sf(Debian): `sox`
@sf(WWW): http://home.sprynet.com/~cbagwell/sox.html
Use sox for most sound-file conversions. Give as arguments the name of the input file and the name of the output file to write to; use a file name extension specifying the sound format for the output file (see section Sound File Formats).

+   To convert the file `new.wav` to an audio CD format file, type:

```
$ sox new.wav new.cdr RET
```

This command writes a new file, `new.cdr`, in the audio CD format; the original file, `new.wav`, is not altered.

You may sometimes need to specify additional options, such as with raw audio files where the sampling rate and other properties must be specified.

+   To convert all of the raw audio files in the current directory to audio CD format files, type: