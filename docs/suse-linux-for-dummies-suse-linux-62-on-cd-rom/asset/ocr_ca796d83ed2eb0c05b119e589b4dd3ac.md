# Chapter 6: Solving Problems with the X Window System Installation

Expectation management: Although you may find this hard to believe, the X server may not be able to run with the configuration options that you have selected. The video card, monitor, color depth, and resolution settings are all interrelated by a mathematical formula, but that is beyond the scope of this book. If you are successful on the first attempt, we congratulate you! If not, do fret. The first thing to do is double-check your configuration settings. Next, go through the settings in SaX and adjust them. For example, perhaps you need to try a lower resolution, color depth, or sync rates. If you are curious about the interrelationships of these settings, you can read all about them in the Video HOWTOW by issuing this command:

```
[root@localhost]# less /usr/doc/howto/en/XFree86-Video-Timings-HOWTO.gz
```

You can use the up- and down-arrow keys to scroll through the document; when you are finished, press the q key to quit, which will bring you back to the command line.

![](bbox=[0.166, 0.452, 0.703, 0.745])

Figure 6-7: Color set settings and resolutions.

Test the configuration setting by clicking the Next button at the bottom-right corner of your screen.

If your video card and monitor are capable of handling your configuration settings, then the X server will start and a purple screen will appear with arrows on it. This screen is used for adjusting the size and shape of the image on the screen so that it fits your monitor. When the screen has been set to