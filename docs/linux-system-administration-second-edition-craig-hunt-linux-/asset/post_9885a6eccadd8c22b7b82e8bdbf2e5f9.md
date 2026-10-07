
```
id:5:initdefault:
```

The critical component of this line is the digit—5 in this example. This digit indicates the default run level for the computer, as described in Chapter 3. Run level 1 is a single-user mode that’s often used for emergency maintenance; run level 6 forces the computer to reboot; and the intervening run levels are defined by the distribution. On most distributions, including Red Hat 7.3, run level 3 is used for text-mode startup, and 5 indicates full GUI startup via XDM. (These numbers are arbitrary; for instance, Slackware Linux uses 3 and 4 instead of 3 and 5.)

Although Linux starts at a run level specified in /etc/inittab, you can change the run level of a running system using the telinit command, as in `telinit 3` to change to run level 3.

**Tip** If you plan to change your X configuration, it’s best to switch out of full GUI login mode first. Use `telinit 3` to switch to a text-mode login. You can then change your X configuration and type `startx` to launch X. If there’s a problem with the configuration, you’ll be dropped back to a working text-mode session. You can then examine the .xsession-errors file in your home directory for clues to what went wrong. You can then correct the problem and, when X is working, use `telinit 5` to return to a full GUI configuration. If you change your X configuration without testing it in this way, you run the risk of creating a system that can’t start X, but that keeps trying to do so, thus blocking your use of the console.

## Configuring a Font Server

A font server is a network server that delivers font bitmaps to computers that request them. The font server may work from font bitmaps or fonts in scalable outline formats, such as PostScript Type 1 or TrueType fonts. When the server uses the latter, it rasterizes the font—that is, the server converts the font into a bitmap of the size the client requests. The principal benefit to using a font server is that you can configure a font server on a single computer with all the fonts you want, and you need not install those fonts on other computers on the network. Instead, you tell those computers to access the font server that’s been configured in the way you desire. Some distributions use font servers because XFree86 3.3.x does not by default understand TrueType fonts (although XFree86 4.x does). It’s easier to add TrueType support to a separate font server program than to the XFree86 3.3.x font handler, so using a local font server is a good way to provide TrueType font support in Linux.

**Warning** Check the license terms of any font before adding it to a font server. In the United States, outline fonts are considered computer programs, and therefore may be copyrighted and subject to terms of use similar to those of other programs. These terms may forbid the use of a font on a font server or require a per-client payment.

## Adding Fonts to a Font Server

Some Linux distributions don’t use font servers by default, although they’re perfectly capable of doing so. Other distributions, including Red Hat, use font servers as a matter of course, although they’re usually configured to be accessible only to the local computer. You can check your system’s configuration by examining the XF86Config or XF86Config-4 file (located in /etc/X11 in Red Hat, but in /etc on some other distributions). Early in this file, there should be one or more lines that begin with `FontPath`:

```
FontPath     "/usr/X11R6/lib/X11/fonts/Type1"
FontPath     "unix/:7100"
```

Each of these lines specifies a location where fonts may be found. The first line of this example indicates a directory on the X server computer's hard disk, but the next two specify font servers. The `unix/:7100` server is a default Red Hat 7.3 server, which is private to the local computer. The `tcp:dino:7101` server is a network–accessible font server running on port 7101 of the computer called dino. (See Chapter 12 for a discussion of ports and hostnames.) This line has been added to the default configuration; it is *not* a standard part of any distribution's configuration.

The default Red Hat 7.3 font server is controlled from the file `/etc/X11/fs/config`. This file includes several settings, the most important of which are the following:

- **catalogue**: This setting is a comma-delimited list of directories that contain fonts. The list may span multiple lines and ends when a directory is not followed by a comma.
- **default-point-size**: You can set the default size of fonts, in 10ths of a *point* (a common measure of font size), for when a program doesn't specify a font size. Red Hat sets this value to 120, which corresponds to 12 points.
- **default-resolutions**: Point sizes relate to physical size, but computer displays vary in the number of pixels displayed on any given size of screen. Because computer graphics (including font displays) work on pixels, point size can vary depending upon the size of your monitor and the resolution at which you run it. Most displays use a resolution of between 72 and 100 dots per inch (dpi). The resolution may vary both horizontally and vertically. Your screen might be 75×80 dpi, for instance. You can set the default resolution using the `default-resolutions` setting, which lists both horizontal and vertical resolutions, separated by commas. You can specify a second default resolution after the first, separated from the first by commas.

If you want to add fonts to your system, you must specify the path to those fonts, either directly in XF86Config or by including the path in `/etc/X11/fs/config`. You must also create an appropriate configuration file *within* the font directory to tell the system about the fonts you've added. It's best to separate fonts of different types in different directories; for instance, TrueType fonts in one directory and Type 1 fonts in another. To create X font information files for a directory, follow these steps:

1. Use a text-mode login or open an xterm window.
2. Change to the target font directory.
3. If the directory contains TrueType fonts, issue the command `ttmkfdir . >fonts.scale`. This action creates the `fonts.scale` file, which contains font names associated with each font file and other critical information.
4. If the directory contains PostScript Type 1 fonts, do the following:
   - A. Obtain and install the `type1inst` package. (It may be obtained from [http://rpmfind.net/linux/RPM/TbYName.html](http://rpmfind.net/linux/RPM/TbYName.html), among other places.)
   - B. Type `type1inst` to create a `fonts.scale` file for the Type 1 fonts in a directory.
5. Issue the command `mkfontdir -e /usr/X11R6/lib/X11/fonts/encodings`. This creates a `fonts.dir` file from the `fonts.scale` file or from font information in bitmap fonts in the directory.
6. Check the `fonts.dir` file. It should begin with a number (indicating the number of fonts defined in the file). Each subsequent line should then begin with a font filename and conclude with an X font specification, which includes the font name and assorted other information.

At this point, your configuration files point to the new font directory, which should contain a `fonts.dir` file that correctly identifies the new fonts. You can either shut down X and restart it or issue the following commands to begin using the newly defined fonts:

```
# killall -USR1 xfs
# xset fp rehash
```

**Warning** If there's an error in your new font configuration, X may behave very strangely or fail to start. This can be particularly troublesome if your system is configured to boot directly into X, because Linux may lock itself into a cycle of trying to start X, failing, and trying again, making the system inaccessible from the console. You should therefore ensure that you have access to the system through some other means, such as a dumb terminal (Chapter 6) or a Telnet login. Alternatively, if you encounter problems, you can modify the configuration from an emergency boot floppy.

To check that your changes have taken effect, you can use the `xfontsel` program, shown in Figure 13.3. This program allows you to display all the fonts that are available on the X server from which it's run.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_346_0.png)

**Note** Like most X programs, `xfontsel` takes its fonts from the X server, not the computer on which the program runs. Therefore, the same program run from the same computer might have different fonts available to it when run via X servers on different computers.

## Configuring a New Font Server

If you want to use the networking capabilities of a font server, you can set up one system to serve fonts to others on your network, thus simplifying your administrative tasks. To do this, follow these steps:

1. Create a new font server configuration file. You can base it on the `/etc/X11/fs/config` file, but should place it somewhere else, such as `/etc/xfsconfig`.
2. Create font directories that contain the font files you want to share, as well as the `fonts.scale` and `fonts.dir` configuration files, as described earlier.
3. Modify your new font server configuration file so that it serves fonts from the directories you created in step 2 or from existing font directories.
4. Add a line to a convenient startup script (such as `/etc/rc.d/rc.local`) to launch `xfs` using this new configuration file, serving fonts using port 7101 (which is more or less standard for this purpose). This line should resemble the following:
