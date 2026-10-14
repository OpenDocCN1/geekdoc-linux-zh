There can be several different Monitor sections in XF86Config. Even multiple Screen sections are possible. Which one is started depends on the server started.

# Screen Section

First, we will take a closer look at the screen section. As mentioned above, this combines a monitor with a device section and determines which resolution using which color depth should be used. A screen section might look like the example in File 12.

```
```text
Section "Screen"
    DefaultDepth 16
    SubSection "Display"
        Depth        16
        Modes        "1152x864" "1024x768" "800x600"
        Virtual      1152x864
    EndSubSection
    SubSection "Display"
        Depth        24
        Modes        "1280x1024"
    EndSubSection
    SubSection "Display"
        Depth        32
        Modes        "640x480"
    EndSubSection
    SubSection "Display"
        Depth        8
        Modes        "1280x1024"
    EndSubSection
    Device       "Device[0]"
    Identifier   "Screen[0]"
    Monitor      "Monitor[0]"
EndSection
```
```

*File 12: The Screen Section of the File /etc/X11/XF86Config*

The line Identifier (here Screen[0]) gives this section a defined name with which it can be uniquely referenced in the following ServerLayout section. The lines Device and Monitor specify the graphics card and the monitor that belong to this definition. These are just links to the Device and Monitor sections with their corresponding names or “identifiers”. These sections are discussed later in more detail.