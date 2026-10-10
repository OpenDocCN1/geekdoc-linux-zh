+   - `Mixer` synth controls the volume of the synthesizer. This generally affects MIDI files.
+   - `Mixer` cd controls the volume of audio CDs.
+   - `Mixer` line controls the volume of a device connected to the line in the jack on a sound card.
+   - `Mixer` igain controls the input gain level.
+   - `Mixer` ogain controls the output gain level.

To make changes to any one of the levels, you can type `mixer`, followed by the name of the device and the desired level. For example, the following will set the cd volume to 90 percent on both the left and right channels:

```
mixer cd 90
```

If you want to set the left and right channels to different values, you need to include both values, separated by a colon. For example, the following will set the cd volume to 100 percent for the left channel and 80 percent for the right channel:

```
mixer cd 100:80
```

At system boot, most of the mixer values will default to 75 percent. If you wish to have different default values at system boot, there are two ways to accomplish this.

The first way is by creating a startup file in `/usr/local/etc/rc.d`. In the file, simply include a list of the desired mixer commands. You can name the file anything you want. For example, you might call the file `mixerset`. Here is an example of what the file might contain:

```
mixer vol 80:80
mixer cd 90:90
mixer pcm 50:50
```

As root, create this file in the directory `/usr/local/etc/rc.d` and save it as `mixerset`, for example. Next, make the file executable by issuing the following command:

```
chmod u+x mixerset
```

The commands inside this file will now be run at each system boot and cause the mixer to be set to the desired values.

> **TIP**
> If the previous steps are unclear to you, see Chapter 7, “Working with the Shell,” and Chapter 10, “System Configuration and Startup Scripts,” for more information on these topics.