uncommon for XFree86 4.x's XF86Config file to lack Modeline lines, instead relying upon DDC to obtain this information.)

**Device** The XF86Config file contains one or more Device sections, which provide information on your video card. With most modern video cards, this section is quite short. You should not adjust these settings unless you add RAM to your video card or replace the board entirely (in which case, you may want to run an X configuration utility to do the dirty work). The Driver option specifies the driver that XFree86 uses, so you may need to change this option if you upgrade your video card.

**Screen** A Screen section references the Monitor and Device sections by name. You may want to adjust the Screen section for your monitor/video card combination to configure it for your preferred screen resolution and bit depth. There are two important options in the Screen section:

    **DefaultDepth** This option sets the color depth that X uses when it starts. The default is 8, which results in a mere 256-color display. The value 16 is usually a better choice on modern hardware. Values of 24 and 32 work well on some systems, but occasionally produce problems.

    **Subsection "Display"** A Display subsection defines the characteristics of a given color depth. The Depth line identifies the color depth for which the subsection is written, and the Modes line identifies the resolutions at which X will work in this color depth. You can use this feature to define different resolutions to be associated with different color depths. Your video card may be incapable of producing 32-bit color at your highest resolution, so you can specify a lower maximum resolution for the 32-bit display. You can then start multiple X servers, as described earlier, using the color depth as a cue to use a different resolution. XFree86 4.x sometimes relies upon DDC to compute this information dynamically.

**DRI** If you're lucky enough to have a video card with 3-D acceleration features supported by XFree86, you can define who may access these features in this section. A simple line allows all users to access DRI functions:

```
Mode 0666
```

**Tip** XFree86 4.x uses DDC by default, but it sometimes yields less–than–optimal results. For example, one author uses an iiyama VisionMaster Pro 450 monitor, which is able to display 1280×1024 at 100Hz, but DDC produces only an 85Hz display at this resolution. This problem can be overcome by copying the appropriate Modeline lines for a 100Hz 1280×1024 display from a 3.3.x XF86Config file to the 4.x XF86Config file. (These lines are clearly marked in the default 3.3.x XF86Config file.)

# ## XFfree86 3.3.x

XFfree86 3.3.x configuration is similar to that of XFfree86 4.x, but the earlier versions lack several configuration file features. The most important of these are the ServerLayout, Module, and DRI sections. XFfree86 3.3.x uses sections called Keyboard and Pointer for setting keyboard and mouse options, rather than InputDevice sections. The DefaultDepth option is called DefaultColorDepth in

330