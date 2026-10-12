
## TABLE 4.2 continued

| Driver | Card |
| :--- | :--- |
| glide | 3dfx Voodoo 1, 2 graphics cards |
| glint | Permedia 2, 2v, GLINT 500TX, MX, Gamma, Delta |
| i740 | Intel i740 |
| i810 | Intel 810 (requires agpgart kernel module) |
| mga | Matrox Millenium I, II, Mystique, G100, G200, G400 |
| neomagic | NeoMagic NM-series (including 256AV) |
| nv | NVIDIA Riva TNT, TNT2, GeForce and Quadro |
| r128 | ATI Rage 128 |
| rendition | Rendition/Micron Verite 1000, 2100, 2200 |
| svirge | S3 ViRge, ViRGE/VX, DX, GX, GX2, MX, MX+, Trio3D, 2X |
| sis | SiS 530, 620, 632E (partial support for 630, 300, 540) |
| tdfx | 3dfx Voodoo 3, Banshee graphics cards |
| tga | DEC 21030 TGA |
| trident | Trident TVGA8900D, TGU19420DG, TGU19440AG, TGU19660, TGU19680, Providia 9685, Cyber9320, 9382, 9385, 9388, 9397, 9520, 9397/DVD, 9525/DVD, 3DImage975, 875, Blade3D, CyberBlade/f7, DSTN/7 and 11 |
| tseng | Tseng Labs ET4000AX, W32, W32i, W32p, ET6000, 6100 |
| vga | IBM VGA and compatibles |

## XF86Config Screen Section

The XF86Config Screen section tells the X server the desired screen, device, monitor, and color settings to use, such as the color depth (such as 8-, 16-, 24- or 32-bits per pixel), the screen size (such as 640x480, 800x600, or 1024x768), and (possibly) the size of a virtual screen:

```
Section "Screen"
    Identifier "Screen0"
    Device "Neomagic Corporation || MagicMedia 256AV"
    Monitor "LCD Panel 1024x768"
    DefaultColorDepth 16
    Subsection "Display"
        Depth 8
        Modes "640x480" "800x600" "1024x768"
        Virtual 1024 768
    EndSubSection
    Subsection "Display"
        Depth 16
        Modes "640x480" "800x600" "1024x768"
        Virtual 1024 768
    EndSubSection
EndSection
```

This example shows a Screen section with two Display subsections that define a 256-color (Depth 8) and a thousands of colors session (Depth 16). These two definitions allow flexibility in specifying the number of colors to use for an X session. If enabled, the `DefaultColorDepth` keyword will force the X session to thousands of colors.

The Screen section also contains directions for the X server on what resolutions and virtual screen size to try to support. The example configuration provides the choice of a 1024x768, 800x600, or 640x480 display, with 640x480 being the default. According to the example, if you use a resolution of say, 800x600, you'll also use a virtual display of 1024x768, which offers the ability to “pan” the display, or shift the display when your pointer reaches an edge of the screen. To disable the virtual display, comment out the `Virtual` line, or use a virtual setting equal to a desired resolution (such as 800x600 for the 800x600 mode).

You can toggle resolutions during your X session by holding down the `Ctrl+Alt` keys and pressing the plus (+) or minus (-) key on your keypad. Laptop users may need to also use an `Fn` key or the `NumLock` key before switching resolutions.

Note that you can reorder the different resolutions on the `Modes` line. You may also find that even though `xconfigurator`, `xf86config`, or another tool automatically configured different modes, not all modes may work properly. In this case, simply remove the mode to avoid problem displays when toggling through the resolutions.

## Starting X11 with the startx Command

The `startx` command is an easy way to start an X session if you're working on a single computer or boot Linux to runlevel 3 mode (X11, multituser and networking enabled). There are other ways to start X (see the section “Using xdm” later in this chapter). The `startx` command is a handy shell script that will pass on command-line options to the X server for your X sessions.

The `startx` command is typically used to pass starting color-depth information to the X server, as well as to find client commands or options to run for the session (usually your `.xinitrc` file in your home directory: see the section “The .xinitrc File”).

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_136_0.png)

If you use a similar Screen definition as in the previous section, the default X session will use 256 colors when you start your X session like this:

```
# startx
```

If your video card and monitor support a greater color depth, you can start a 16 *bit/planes per-pixel* (thousands of colors represented by 16 bits per pixel) X session using the *depth* command-line option like this:

```
# startx --depth 16
```

Unless you’ve changed the *DefaultColorDepth* option in your system’s *XF86Config* file to set a specific color depth, using *startx* by itself will usually start an X session using 8-color *bitplanes* or 256 colors. Color values typically passed with the *depth* option also include 24 and 32 for millions of colors.

## Options, Options, Options!

The *XFree86* X server understands nearly 100 command-line options. However, you’ll rarely need to use more than a few options. Some common options include:

- *probeonly*—Useful when *stdout* is redirected to a file (such as *XFree862report.txt*) to only probe and report on your graphics chipset
- *vt=N*—Use virtual console *N* for the X session
- *depth* *NN*—Use color depth *NN*, such as 8, 16, or 24
- *allowMouseOpenFail*—Start a session without a pointer
- *showconfig*—Display an internal report
- *version*—Useful to display the version
- *xf86config* *path*—Use specified file instead of *XF86Config*
- *dpi* *NNN*—Use specified dots-per-inch
- *screen* *name*—Use specified Screen section
- *layout* *name*—Use specified Layout section

To see a complete list of options, read the *XFree86* man page or use *XFree86*’s *help* command-line option.

## Using the Console and Multiple X Sessions

You can also use *startx* to start multiple X11 sessions on the same computer, possibly using different window managers, and then navigate between the sessions using *virtual* consoles. Red Hat Linux supports up to six different login screens or consoles, accessed by pressing Alt+FX, where X is F1 through F6.

For example, if you log into Linux using a text-only console, you'll be at the first virtual console. After you log in, press Alt+F2, you'll then see another login prompt at the second console. To get back to your first login, press Alt+F1.

When you log into Linux and start an X11 session with startx, X uses a seventh virtual screen. Since you've started X from an X11 virtual console, this console will be unavailable for use. However, you can get to another virtual console, such as the second, by pressing Ctrl+Alt+F2 while in X11. You'll then see the Red Hat Linux login prompt. To go back to your X session, press Alt+F7. Using this approach, you can jump back and forth between your X session and different text consoles.

To use multiple X11 sessions at different color depths on different virtual consoles, first start a session with the startx command. After the X desktop appears, press Ctrl+Alt+F2 and log in to Linux again. If your graphics card supports thousands of colors, use the startx command to start an X session. This time, however, include the :1, -depth 16, and vt 16 command-line options:

```
# startx -- :1 -depth 16 vt 16
```

The screen clears and you'll be running an X session with a different color depth! To jump to your other X11 session, press Ctrl+Alt+F7. To jump to another virtual console, press Ctrl+Alt+F3 (since the first and second consoles are in use). To jump back to your original X session, press Ctrl+Alt+F8.

## The .xinitrc File

When you use the startx command to initiate an X session on your computer, details about which window manager to use or other X clients to start can be found in a file called .xinitrc in your home directory. A sample or template file called xinitrc is installed in the /etc/X11/xinit directory. You can copy this file to your home directory with the filename .xinitrc and modify it.

Although the default .xinitrc file contains shell logic to load system resources or set different environment variables, you can define a simpler version from scratch, such as the one in Listing 4.2, which can be used to start 12 different X window managers. (For more information about several X window managers included on this book's CDs-ROMs, see Chapter 5.)
