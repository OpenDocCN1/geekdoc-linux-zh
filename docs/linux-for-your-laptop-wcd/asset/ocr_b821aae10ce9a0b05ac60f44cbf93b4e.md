This chapter introduces general concepts, strategies, software, and hardware you can use to extend your mobile Linux sessions while using your notebook's batteries. You'll learn about accepted practices for battery treatment and Linux software you can use to monitor usage and extend battery life with an aim to conserve energy. This chapter builds on the advanced power management information you learned in Chapter 7, "Advanced Power Management."

# ## General Strategies

There are many strategies you can use to extend your mobile sessions. Some of these are obvious, and others require you to read your notebook's manual to determine specific features or keyboard controls for your notebook.

# ### Change the Screen Display

The first strategy is to reduce your screen's brightness, either through manual or keyboard controls, to an acceptable level for your environment. Active-matrix screens consume more power than passive-matrix (DSTN) displays. Some laptops allow you to turn off the LCD's backlight, but this can render most active-matrix screens unreadable except in the dark. Other laptops, such as Sonys, also provide BIOS settings for initial screen brightness. An alternative is to turn off your notebook's display and use an external monitor, although this is not always convenient and might be impossible when you're on the road.

# ### Don't Play Audio

Don't play audio through your notebook's speakers. Use the headphone jack instead, or don't listen to audio and turn off sound by unloading the sound modules with the `rmmod` command. For example (on a Dell Inspiron 7500), first use the `lsmod` command to list the modules in use:

```
```
$ lsmod

Module          Size  Used by
maestro         26176   0  (unused)
soundcore        3524   2  [maestro]
```
```