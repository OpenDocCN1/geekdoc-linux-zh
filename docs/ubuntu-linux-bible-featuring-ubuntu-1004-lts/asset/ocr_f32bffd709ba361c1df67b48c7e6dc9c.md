# Chapter 16: Working with Multimedia

This dialog lists all of the audio devices that were detected on your system, which will only be one device on most systems. Make sure that the profile for any audio device listed on this panel is set to something like "Analog Stereo Duplex" or "Analog Stereo Output." (You can use either of these as a starting point and select a more optimal once once you get audio working on your system.)

Next, select the Output tab, which displays a screen like the one shown in Figure 16-2.

# 16-2
Sound output settings in the Sound Preferences utility

![](bbox=[0.038, 0.305, 0.415, 0.602])

Select the output device that you want to use, and ensure that the Mute checkbox is not selected beside the Output volume slider at the top of the "Sound Preferences" dialog. To test the audio on your system, you can either start an audio application or use the sample alert sounds provided on the "Sound Preferences" application's Sound Effects tab (discussed later in this chapter in the section, "Testing and Customizing System Sounds"). You can double-click on any of these to produce the associated sound.

# Tip

Most motherboards nowadays feature integrated audio hardware. Unless you've added a sound card to your system (in which case you probably know what it is), you can identify the primary audio device on your system by using the lspci command, in the following example:

```
$ lspci | grep -i audio
00:1b.0 Audio device: Intel Corporation 82801H HD Audio...
```