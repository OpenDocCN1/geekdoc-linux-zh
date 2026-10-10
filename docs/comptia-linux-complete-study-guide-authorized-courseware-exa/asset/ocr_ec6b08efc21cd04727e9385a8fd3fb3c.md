```
EndSubSection
SubSection 'Display'
      Depth          8
      Modes        '1024x768' '800x600' '640x480'
EndSubSection
EndSection
```

The Device and Monitor lines refer to the Identifier lines in your Device and Monitor sections, respectively. The Screen section includes one or more Display subsections, which define the video modes that X may use. This example creates two such displays. The first uses a color depth of 24 bits (Depth 24) and possible video mode settings of 1024x768, 1024x600, 800x600, and 640x480. (These video modes are actually names that refer to the mode lines defined in the Monitor section, or to standard mode lines.) The second possible display uses an 8-bit color depth (Depth 8) and supports only 1024x768, 800x600, and 640x480 video modes.

To choose between the Display subsections, you include a DefaultDepth line. (This line is called DefaultColorDepth in XFree86 3.3.6 and earlier.) In this example, X uses the 24-bit display if possible, unless it's overridden by other options when starting X.

Graphical video modes require a certain amount of RAM on the video card. (On some laptop computers and computers with video hardware integrated into the motherboard, a portion of system RAM is reserved for this use by the BIOS.) The total amount of RAM required is determined by an equation:

```
R = xres * yres * bpp ÷ 8, 388,608
```

In this equation, R is the RAM in megabytes, xres is the x resolution in pixels, yres is the y resolution in pixels, and bpp is the bit depth. For instance, consider a 1280 × 1024 display at 24-bit color depth:

```
R = 1280 × 1024 × 24 ÷ 8, 388,608 = 3.75MB
```

All modern video cards have at least 32MB of RAM—usually much more. This is more than enough to handle even very high resolutions at 32-bit color depth (the greatest depth possible). Thus, video RAM shouldn't be a limiting factor in terms of video mode selection, at least not with modern video hardware. Very old video cards can impose limits, so you should be aware of those limits.

![](bbox=[0.15, 0.74, 0.23, 0.79])

Modern video cards ship with large amounts of RAM to support 3D acceleration features. X supports such features indirectly through special 3D acceleration packages, but 3D acceleration support is limited compared to basic video card support. If 3D acceleration is important to you, you should research the availability of this support.

In Exercise 6.1, you'll adjust the X resolution and color depth by editing the XF86Config or xorg.conf file.