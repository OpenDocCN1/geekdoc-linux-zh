color depths, and your XF86Config file's Screen section should have Display sub-section entries for each color depth. For example:

```
Section "Screen"
Driver "svga"
Device "My Video Card"
Monitor "LCD Panel 1024x768"
Subsection "Display"
Depth 8
Modes "1024x768" "800x600" "640x480"
EndSubsection
Subsection "Display"
Depth 16
Modes "1024x768" "800x600" "640x480"
EndSubsection
Subsection "Display"
Depth 24
Modes "1024x768" "800x600" "640x480"
EndSubsection
EndSection
```

These entries show configurations for color depths of 8-bit planes (256 colors), 16 (thousands of colors), and 24 (millions of colors), with different resolutions for each color depth. Use startx with its bpp (bit plane) option to start an X11 session with millions of colors:

```
# startx -- -bpp 24
```

After you press Enter, X will start. The X server determines whether the notebook can support a resolution of 1024×768 with millions of colors. If not, the next res- olution is tried, and so on until one is found that works. Ideally, you should know the limitations of your notebook's display for each color depth and then craft your system's XF86Config file to support each resolution and color depth. Some note- books, such as Sony's 505TX and TR series, can also use special option entries in XF86Config's Device section to support these modes. For example:

```
Option "lcd_center"
Option "no_stretch"
```

These entries, as detailed in the file README.neo (505s use a NeoMagic graph- ics chipset) under the /usr/X11R6/lib/X11/doc directory, disable stretching of lower-resolution modes and center the lower-resolution screen on the notebook's LCD. This allows for better font display when using various combinations of