
## Tip

If you're unsure of what device to use, try using `cat` to examine the contents of a device file, as in `cat /dev/ums0`. When you move the mouse, you should see gibberish appear on your screen. If nothing happens, press CTRL-C and try again. This procedure may put your terminal into an odd mode, though (for instance, displaying a bizarre character set). Type `reset` if this happens to restore a normal display.

## Adding or Removing Fonts

The `Files` section of Xf86Config controls the *font path*—a set of directories in which the X server searches for fonts. A `Files` section might look like this:

```
Section "Files"
RgbPath "/usr/X11R6/lib/X11/rgb"
ModulePath "/usr/X11R6/lib/modules"
FontPath "/usr/X11R6/lib/X11/fonts/misc/"
FontPath "/usr/X11R6/lib/X11/fonts/Speedo/"
FontPath "/usr/X11R6/lib/X11/fonts/Type1/"
FontPath "/usr/X11R6/lib/X11/fonts/75dpi/"
FontPath "/usr/X11R6/lib/X11/fonts/100dpi/"
FontPath "tcp://server:1101"
EndSection
```

The first couple of items in this section (RgbPath and ModulePath) don’t set the font path; only the lines labeled `FontPath` do this job. Each of these lines specifies one source for fonts. Most of these are subdirectories of `/usr/X11R6/lib/X11/fonts`—the standard location for fonts on a FreeBSD system. Each of these subdirectories contains a particular type of font. The final `FontPath` entry in this example is unusual. Rather than specifying a directory, this entry identifies a *font server*—a network server that delivers font information to any X server that asks for it. Font server configuration is described in Chapter 22.

XFree86 understands several different types of fonts. Many of the core X fonts (those that programs are likely to assume exist) are delivered in *bitmap* format, which in this context means a font that’s defined in terms of particular pixel being light or dark. Bitmap fonts are small and display quickly, but they display properly at only one size and resolution. To increase the size of a font, you need to create a new bitmap font. Another type of font is a *scalable* (or *outline*) font, which is defined in terms of a mathematical description of its outline. The two most popular outline font formats are Adobe's PostScript Type 1 (also known as Adobe Type Manager, or ATM) and Apple's TrueType. XFree86 4.x supports both of these formats, but XFree86 3.x and earlier don't support TrueType fonts. If you want to add fonts, your best bet is to use Type 1 or TrueType fonts.

> **Tip**
> *You can find font collections on CD-ROMs in computer stores. XFree86 expects fonts stored in the same file format that Microsoft Windows uses, so get the Windows version of a font, not the Macintosh version.*

One relatively straightforward way of adding fonts is to create a new subdirectory for your new fonts (a subdirectory of /usr/local should be safe). Placing the fonts in this directory isn't enough, though; you must create a summary file that tells X about the fonts. This file is called fonts.dir, and it's tedious to generate it manually. Fortunately, there are utilities to do this for Type 1 and TrueType fonts: type1inst and ttmkfdir, respectively. Both are available as packages and as part of the FreeBSD ports system. (The FreeBSD package and port name of type1inst is p5-type1inst.) To tell X about the fonts you've installed, follow these steps:

- 1. Change to the directory in which you've installed the fonts.
- 2. If the directory contains TrueType fonts, type `ttmkfdir > fonts.scale`. This command creates an intermediary file called fonts.scale.
- 3. If the directory contains Type 1 fonts, type `type1inst` to create a fonts.scale intermediary file.
- 4. Type `mkfontdir -e /usr/X11R6/lib/X11/fonts/encodings`. This action extracts information from fonts.scale and from any bitmap fonts that might be present to create a fonts.dir file.
- 5. Add a FontPath line to your /etc/XF86Config file pointing to your new font directory.
- 6. If you want to use the new fonts immediately, shut down X and restart it or type `xset fp rehash` to tell X to use the new font set.

At this point, your new fonts should be available in X applications that let you choose fonts. You can test this with a simple utility called xfontsel (Figure 13-4), which lets you display any of your installed fonts at a variety of sizes and with various attributes set.

> **Tip**
> *You can forego some of this trouble by installing a prepackaged font set. The FreeBSD ports system provides several in the x11-fonts ports set. Of particular interest is the urwfonts package. This is a set of Type 1 fonts released by URW to duplicate fonts available on PostScript printers.*

![](img/f34d37e3abe9f4517128e54f80ab2616_381_0.png)

> Figure 13-4. The xfontsel program lets you test your installed fonts to be sure they’re working as they should.

Unfortunately, not all programs rely exclusively upon X’s font-delivery mechanisms for fonts. The reason is that X’s font handling is inadequate for some programs’ needs, so some programs require that you install fonts independently of X’s fonts. Word processors are particularly likely to have this requirement. If you see your fonts in xfontsel but not in a regular program, consult its documentation to determine whether you need to install the font into the program in addition to installing it in X.

If you want to reduce the clutter in your font menus, you can remove fonts. You can either trim entire directories from your font path or trim entries from the `fonts.dir` files. Removing directories from your font path is likely to cause problems unless they’re directories you added to begin with. To trim entries from `fonts.dir`, look for the line containing the font’s name. A typical entry looks like this:

```
n0210231.pfb -Adobe-Times-medium-i-normal--0-0-0-0-p-0-iso8859-1
```

Some fonts provide multiple entries for font variants such as bold or italic, and bitmap fonts provide one entry for each font size. Thus, you may need to remove several font entries. When you’re done, adjust the first line of the file, which lists the number of entries in the file (the number of lines minus one). It’s a good idea to back up the `fonts.dir` file before you work on it.

> Don’t remove fonts that are provided as a standard part of FreeBSD. Some programs assume that some of these fonts are present, so some programs may crash or behave strangely if they’re not. You might use this process to trim fonts added from a font package, though.

## Tools to Help Reconfigure X

Reconfiguring X by editing XF86Config provides you with a great deal of flexibility, but it can be a tedious and tricky process, particularly if you’re new to FreeBSD. Fortunately, there are some tools that can help you do the job. This section briefly describes two of them: XFree86 itself and the xf86cfg tool.

XFree86 4.x includes the ability to probe your hardware and generate an XF86Config file. To use this feature, type XFree86 -configure. This command generates a great deal of status information and creates a file called /root/XF86Config.new, which you can use as the basis for further modifications. You can test this file by typing XFree86 -xf86config /root/XF86Config.new, which should launch X using the new configuration file. There’s a good chance that this command won’t work correctly on the first try, or it may not work as you want it to. The auto-configuration routines frequently miss or misidentify certain types of hardware, such as mice driven through the moused server.

If you generate the XF86Config.new file and find it to be lacking, or if you want to modify an existing file, you may want to try editing it with xf86cfg. This program is included as part of a standard XFree86 4.x installation, and provides a GUI interface to XF86Config editing, as shown in Figure 13-5. Of course, the fact that it uses a GUI interface means that you must already have an X server running on the computer you intend to configure. Thus, xf86cfg is useful for tweaking an already working configuration, or perhaps for creating a new configuration prior to changing a video card. You can call it as follows:

```
$ xf86cfg -XF86config /path/to/XF86Config
```

The /path/to/XF86Config could point to /etc/XF86Config or to a test file such as /root/XF86Config.new, as created by XFree86 using its -xf86config option. Once the program is running, you can configure a component by right-clicking it and selecting Configure from the pop-up menu. This action creates a dialog box in which you can enter or change information relating to the device, as described in the preceding sections. You can also add devices by clicking the device icons near the top of the window. To add a new device to the layout, right-click it and select Enable from the pop-up menu. For most workstations, there’s little need to add components; you’re most likely to do this if you want to use multiple monitors to expand your working desktop area, or if you want to define an external USB keyboard or mouse for optional use with a notebook computer.
