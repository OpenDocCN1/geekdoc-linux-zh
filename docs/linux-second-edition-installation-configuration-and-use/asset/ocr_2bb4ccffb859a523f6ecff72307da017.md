# CONFIGURING THE X SERVER

For fine-tuning, you can also use the xvidtune program or its KDE kvidtune, which allow you to vary part of the timing values interactively during normal operation of X.

Various options can be added to the ModelLine lines: Interlace for the interlace mode (only possible with an odd number of virtual lines), /+Hync and +/-Vsync to change the polarity of the synchronization impulse, plus Composite and +/-Csync for a combined synchronization signal (includes both HSync and VSync).

The following example shows the monitor's section for his nearly age NEC 4D monitor. Three resolutions are defined: 640x480 points at 71 Hz, 816x612 points at 75 Hz, and 1024x768 points at 63 Hz.

```
Section "Monitor"
Identifier "nec 4d"
VendorName "nec"
ModelName "4d"
BandWidth 75
HorSync 30-57
폭 "640x480" 31 640 664 704 832 480 489 492 520
ModelLine "816x612" 50 816 824 960 1040 612 612 614 635
ModelLine "1024x768" 65 1024 1025 1065 1260 768 780 785 810
EndSection
```

As a second example, this is the Monitor section for a more recent screen.

```
Section "Monitor"
Identifier "iiyama 450"
VendorName "unknown"
ModelName "unknown"
HorSync 31.5-102
VertRefresh 40-100
ModelLine "1280x1024" 157.50 1280 1028 1334 1344 1504 1728
1024 1025 1068 1072 +hync +vsync
ModelLine "1152x864" 137.65 1152 1184 1312 1332 1536
864 866 885 902 -hync -vsync
ModelLine "1024x" 115.50 1024 1056 1248 1440
768 771 781 802 -hync -vsync
EndSection
```

# Screen

The Screen section indicates which Monitor is to be combined with which VGA device. The section contains one or more Display subsections. Each subsection applies to a specific color depth (8, 16, or 24 bpp), that bits per pixel.

Each Display section contains a list of all graphic modes to be supported. This list begins with the keyword Modes and contains the names of the graphic modes defined above in ModelLine. The order is significant – the first mode is taken as the default mode. You can switch to the other modes in order with Ctrl+Alt+- or = (numeric keypad).