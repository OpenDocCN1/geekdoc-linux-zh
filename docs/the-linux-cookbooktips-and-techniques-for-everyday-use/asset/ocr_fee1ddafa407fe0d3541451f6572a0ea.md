# The Linux Cookbook: Tips and Techniques for Everyday Use:

+   - To add a 100 millisecond echo to the sound file `old.wav` and write output to `new.wav`, type:

```
sox old.wav new.wav echo .5 .5 100 .5 RET
```

+   - To add a one-second echo to the sound file `old.wav` and write output to `new.wav`, type:

```
sox old.wav new.wav echo .5 .5 1000 .5 RET
```

+   - To add a "tin-can" echo effect to `old.wav` and write the output to `new.wav`, type:

```
sox old.wav new.wav echo 1 .5 5 .5 RET
```

> **NOTE:** The `echos` effect works like `echo`, but adds a *sequence* of echos to the sound file.

# 24.2.5 Adding Flange to a Sound File

The `flanger` effect adds flange to a sound file. It takes as arguments the "gain-in" and "gain-out" volume levels, as well as the delay and decay in milliseconds, and the speed of the flange, in Hertz. Specify the type of modulation with either `-s` (for sinusoidal) or `-t` (for triangular).

+   - To add an "underwater" flange to the file `old.wav` and write the output to `new.wav`, type:

```
sox old.wav new.wav flanger .5 .5 4 .5 1 -t RET
```

+   - To add flange that sounds somewhat like a "wah-wah" effects pedal to the file `old.wav` and write the output to `new.wav`, type:

```
sox old.wav new.wav flanger .5 .5 .5 1 2 -t RET
```

# 24.2.6 Adding Phase to a Sound File

The `phaser` effect adds phase to a sound file. It takes the same arguments as the `flanger` effect.

+   - To add a heavy phase to the file `old.wav` and write the output to `new.wav`, type: