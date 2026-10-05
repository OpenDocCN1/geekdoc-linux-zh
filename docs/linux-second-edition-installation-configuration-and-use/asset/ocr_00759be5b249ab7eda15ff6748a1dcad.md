Graphics cards with sufficient memory allow you to use Virtual to define a virtual screen which is larger than the currently visible section. With the mouse you can move around this virtual screen without delays. You should, however, not use the whole available memory for the virtual screen, but should leave some space for a font cache (this leads to a significant speed increase). The keyword ViewPort specifies the first visible pixel at the start of X (only of interest if the virtual screen is bigger than the actual resolution).

With a virtual screen getting used to. If the virtual screen automatically set up by most configuration programs bothers, you need to comment out the Virtual instruction. (In this case, the size of the virtual screen is oriented towards the highest-resolution graphics mode specified in the Screen section.)

```
Section "Screen"      # for an SVGA card
Driver "vga256"
Device "sigma legend 11"
Monitor "nec 4d"
Subsection "Display"
    Depth               8 # bpp, thus 256 colors
    Modes              "1024x768" "64x480" "816x612"
    Virtual            1024 900
    ViewPort           0 0
EndSection
```

With some accelerated VGA sections, several Display sections with different color depth (8. 16. 24, or 32 bpp) can be displayed simultaneously (see manF86.Accel. At the start of the X server, the 8-bpp mode is activated. The Display sections with higher resolutions come into play only if start a higher color depth is explicitly set by means of --bpp 16 or 24. Alternatively you can change the default mode by specifying DefaultColorDepth n in the Screen section.

```
Section "Screen"\      "Accel"
Driver
Device             "Primary Card"
Monitor            "Primary Monitor"
DefaultColorDepth24
Subsection "Display"
    Depth               8
    Modes              "1280x1024" "1152x864" "1024x768"
EndSubsection
Subsection "Display"
    Depth               15
    Modes              "1280x1024" "1152x864" "1024x768"
EndSubsection
Subsection "Display"
    Depth               24
    Modes              "1280x1024" "1152x864" "1024x768"
EndSubsection
EndSection
```