# 24.2.2 Changing the Sampling Rate of a Sound File

To change the sampling rate of a sound file, use the `-r` option followed by the sample rate to use, in Hertz. Like the `-v` option, specify this option before giving the name of the output file.

+   - To change the sampling rate of file `old.wav` to 7,000 Hz, and write the output to `new.wav`, type:

```
$ sox old.wav -r 7000 new.wav RET
```

# 24.2.3 Adding Reverb to a Sound File

To add reverb to a sound file, use the `reverb` effect. `reverb` takes three arguments: the volume of the output (its "gain-out"), the time (in milliseconds) of reverb, and the length (in milliseconds) of delay. You can specify more than one delay; the more you specify, the more of an overlapping echo the reverb will have.

+   - To add a basic reverb to file `old.wav` and write the output to file `new.wav`, type:

```
$ sox old.wav new.wav .5 1000 100 RET
```

+   - To add a spacey, echoing reverb to file `old.wav` and write the output to `new.wav`, type:

```
$ sox old.wav new.wav reverb 1 1000 333 333 333 333 RET
```

*NOTE:* This last example makes a sound similar to some of the recordings of the band Flying Saucer Attack. You know who they are, don't you?)

# 24.2.4 Adding Echo to a Sound File

To add echo to a sound file, use the `echo` effect. It takes as arguments the "gain-in" and "gain-out" volume levels, as well as the delay and decay, both in milliseconds.