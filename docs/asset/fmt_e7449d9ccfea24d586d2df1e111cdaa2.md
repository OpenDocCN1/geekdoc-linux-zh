
Please answer the following question with either 'y' or 'n'.

Do you want to enable these bindings for the Alt keys?

If you answer 'y', the left Alt key can serve as the meta key for Emacs and the keys that need ModeShift (AltGr) can be entered.

## Monitor

Next, specify your monitor. Be extremely careful with vertical and horizontal frequencies. These values can be found in your monitor manual.

> **Caution**
>
> Setting frequencies incorrectly can lead to irreparable damage to your monitor. The X Window System only addresses video modes that operate the monitor in the given frequency range. Entering frequencies for which the monitor was not designed can cause severe damage to it.

Some monitors are listed under `/usr/X11R6/lib/X11/doc/Monitors`. (However, we cannot be held liable if this information is inaccurate.)

To enter the horizontal frequency, the following selection is displayed:

| Choice | Hsync in kHz | Monitor type with characteristic modes |
| --- | --- | --- |
| 1 | 31.5 | Standard VGA, 640x480 @ 60 Hz |
| 2 | 31.5 - 35.1 | Super VGA, 800x600 @ 56 Hz |
| 3 | 31.5, 35.5 | 8514 Compatible, 1024x768 @ 87 Hz interl. (no 800x600) |
| 4 | 31.5, 35.15, 35.5 | Super VGA, 1024x768 @ 87 Hz interl., 800x600 @ 56 Hz |
| 5 | 31.5 - 37.9 | Extended Super VGA, 800x600 @ 60 Hz, 640x480 @ 72 Hz |
| 6 | 31.5 - 48.5 | Non-Interlaced SVGA, 1024x768 @ 60 Hz, 800x600 @ 72 Hz |
| 7 | 31.5 - 57.0 | High Frequency SVGA, 1024x768 @ 70 Hz |
| 8 | 31.5 - 64.3 | Monitor that can do 1280x1024 @ 60 Hz |
| 9 | 31.5 - 79.0 | Monitor that can do 1280x1024 @ 74 Hz |
| 10 | Enter your own horizontal sync range | |

Enter your choice (1-10):

*Output 6: Input of Horizontal Frequencies of the Monitor*

You should only choose one of the predefined modes if you are unsure of the settings for your monitor. Selection '10' allows you to enter your own frequencies.

The next screen asks you to enter your monitor's vertical frequency. It will also provide a selection:

| Choice | Vertical sync range |
| --- | --- |
| 1 | 50-71 |
| 2 | 50-90 |
| 3 | 50-100 |
| 4 | 40-150 |
| 5 | Enter your own vertical sync range |

Enter your choice (1-5):

*Output 7: Detailed Vertical Frequencies*

Again, using the known values is preferable to using one of the items '1' to '4'.

Next, enter a name, vendor name, and model for your monitor:

```
Enter an identifier for your monitor definition:
Enter the vendor name of your monitor:
Enter the model name of your monitor:
```

These are just descriptive names used to document your configuration, which do not affect the configuration itself. Merely pressing ↵ will select the default values, which are usually sufficient.

Your monitor configuration is now complete.

## Graphics Cards / X server

Next, you must specify your graphics card:

*Do you want to look at the card database?*

If you enter 'y', a selection of predefined cards is presented. Here, select your card by pressing the corresponding number. Do not trust this list blindly, since there can be differences in clock chip and RAMDAC³ settings.

This is why a menu item appears later for selecting a RAMDAC and a clock chip, even though you have entered them already. Then the predefined settings for this card will be presented as an extra option.

The card definitions contain information on clock chips, RAMDAC, and the X server to be used. Furthermore, some valuable information concerning the card is written to the device section in `XF86Config`.

If your card is not listed, do not panic. Switch back to the normal configuration by selecting 'q'. Only select one of the defined cards if it matches your card exactly. Selecting a card with a similar name is not recommended. Similar names do not necessarily refer to similar hardware.

More information on how to configure your card is given in chapter *Section Optimizing the Installation of the X Window System* on page 160.

After specifying your card, the X server is next.
