
Type `y` and press Enter. You might then see the following (if running the script via a telnet session):

> $DISPLAY is set, which may indicate that you are running this installation from an X session. It is recommended that X not be running while doing the installation.
>
> Do you wish to continue? (y/n) [n]

Type `y` and press Enter. The install script will then perform some preliminary checks and then ask if it is OK to overwrite your existing X11 configuration:

> Checking which OS you're running...
> uname reports 'Linux' version '2.2.12-20', architecture 'i586'.
> Object format is 'ELF'. libc version is '5.1'.
>
> Checking for required files ...
>
> You appear to have an existing installation of X. Continuing will overwrite it. You will, however, have the option of being prompted before most configuration files are overwritten.
> Do you wish to continue? (y/n) [y]

Note that the default answer is enclosed in brackets ( `[]` ). If the default is OK, you can just press Enter. Press Enter to continue.

> Removing some old directories that are no longer required...
>     removing old directory /usr/X11R6/lib/X11/objc/compiled
>
> XFree86 now installs most customizable configuration files under /etc/X11 instead of under /usr/X11R6/lib/X11, and has symbolic links under /usr/X11R6/lib/X11 that point to /etc/X11. You currently have files under the following subdirectories of /usr/X11R6/lib/X11:
>
>     app-defaults  lnxproxy  proxy/mgr  restart  xserver
>
> Do you want to move them to /etc/X11 and create the necessary links? (y/n) [y]

This step will save your original system defaults, so you can just press Enter. The script will then list the files that are moved. You'll then be asked the following:

> Do you want to overwrite the app-defaults config files? (y/n) [n]

If you're not concerned about the existing defaults file (which contains default resource settings for various X11 clients), type `y` and press Enter. If you want to save the file, type `n` and press Enter. (Hint: You should probably answer `n` to the xdm and xinit files to preserve your existing graphical login.) The script will continue asking about each original default. Page through the answers. The script will then begin extracting the compressed tarballs. If you have included any of the optional files (listed in Table 6.2), you'll be asked if you want to install them. After that, the script will finish.

# Configuring XFree86 4.0

When the installation finishes, you can attempt to configure X11 for your notebook by using the new XFree86 command with its `-configure` option:

```
# XFree86 -configure
```

The command will attempt to autodetect your notebook's graphic chipset:

```
...
(II) NEMAGIC: Driver for Neomagic chipsets: neo2070, neo2090, neo2093, neo2097, neo2160, neo2200
...
Your XF86Config file is /root/XF86Config.new
```

To test the server, run `XF86x86 -xf86config /root/XF86Config.new`

In this example, the new X server detected a NeoMagic chipset. If the test command line is successful, you can copy the file named `XF86Config.new` to the `/etc/X11` directory with the name `XF86Config`, and restart X. However, if you have problems, you'll still need to configure X11! Fortunately, XFree86 4.0 includes an updated `xf86config` command. From the command line of the console, type `xf86config` and press Enter:

```
# xf86config
```

You'll first be asked to select your mouse type, device, keyboard type, and keyboard language. (Hint: If you have successfully configured X11 before installing the new XFree86 4.0, keep a copy of your original `XF86Config` on hand to answer the questions.) You'll then be asked to enter your monitor settings and choose your graphics chipset by looking at the new XFree86 4.0 database (the file named `Cards`, under the `/usr/X11R6/lib/X11` directory):

```
Do you want to look at the card database?
```

Type `y` and press Enter to see the card database. When the initial, numbered list of cards appears, you can press Enter to page through the database until you come to your notebook's graphics chip:

- 360 Miro Crystal 20SD with ICD2061A (BIOS 2.xx) S3 864
- 361 Miro Crystal 20SD with ICS2494 (BIOS 1.xx) S3 864
- 362 Miro Crystal 20SV S3 964
- 363 Miro Crystal 22SD S3 Trio64
- 364 Miro Crystal 40SV S3 964
- 365 Miro Crystal 80SV S3 968
- 366 Miro Crystal 8S S3 801/805
- 367 Miro Crystal DMD S3 6326
- 368 MiroMedia 3D S3 VI/RGE
- 369 Miro MiROvideo 20TD ET4000/W32(1/lp)
- 370 Miro Video 20SV S3 968
- 371 NeoMagic (laptop/notebook) MagicGraph 128 series
- 372 Number Nine FX Motion 331 S3 Trio64V+
- 373 Number Nine FX Motion 332 S3 964
- 374 Number Nine FX Motion 531 S3 868
- 375 Number Nine FX Motion 771 S3 968
- 376 Number Nine FX Vision 330 S3 Trio64
- 377 Number Nine GXE Level 10/11/12 S3 928

Enter a number to choose the corresponding card definition.

Press enter for the next page, q to continue configuration.

Type the number of your chipset (such as `371`, using our example), and press Enter:

```
371

Your selected card definition:

Identifier: NeoMagic (laptop/notebook)
Chipset: MagicGraph 128 series
Driver: vga

This card is basically UNSUPPORTED. It may only work as a generic
VGA-compatible card. If you have an XFree86 version more recent than what
this card definition was based on, there's a chance that it is now
supported.

Press enter to continue, or ctrl-c to abort.
```

In this example, the database contains information that the NeoMagic card is not supported, and the script automatically chooses this `vga` X server module for the card. This example was used because there is a fix. Continue through the script to answer questions about video RAM, the default color depth (such as monochrome, 256, thousands of colors, or millions of colors). You’ll then see the following:

```
I am going to write the XF86Config file now. Make sure you don’t accidentally overwrite a previously configured one.

Shall I write it to /etc/X11/XF86Config?
```

Type `y` and press Enter. At this point, most notebook users can try to start an X session using the `startx` command like this:

```
# startx
```

However, NeoMagic chipset users should edit the resulting `/etc/X11/XF86Config` file and then look for the first `Driver` entry:

```
Driver    "vga"
```

This should be changed to

```
Driver    "neomagic"
```

Next, look for the `Device` section’s `Driver` entry:

```
Driver    "vga"
```

This entry should be changed to

```
Driver    "neomagic"
```

Save the changes and exit your editor. You can then try to start your X11 session. This fix, which specifies that the X server module should load the `neomagic.o` server module instead of the designated `vga.o` module, should work with many different types of notebooks using NeoMagic graphics chipsets. The new set of graphics card server modules is installed under the `/usr/X11R6/lib/modules/drivers` directory:

| aga_drv.o | fbdev_drv.o | neomagic_drv.o | tga_drv.o |
| :--- | :--- | :--- | :--- |
| ati_drv.o | glide_drv.o | nv_drv.o | trident_drv.o |
| chips_drv.o | glint_drv.o | r128_drv.o | tsecg_drv.o |
| cirrus_alpine.o | i740_drv.o | rendition_drv.o | vga_drv.o |
| cirrus_drv.o | i810_drv.o | svga_drv.o | |
| cirrus_laguna.o | linix | sis_drv.o | |
| cyrix_drv.o | mga_drv.o | tdfx_drv.o | |

You’ll find new manual pages installed on your system when you install XFree86 4.0. To read about Trident chipsets, use the `man` command like this:

```
$ man trident
```

Note that the initial XFree86 4.0 distribution’s documentation might be somewhat sparse. This situation will improve in subsequent releases.

### Research Your Chipset

If you’re having trouble configuring X11 using either the new or previous version of XFree86, the first thing you can do is read the appropriate `README` file for your notebook’s chipset. Look under the `/usr/X11R6/lib/X11/doc` directory. You’ll find the following:

```
# ls README.*
```

- README
- README.3DLabs
- README.Config
- README.DBcTga
- README.DGA
- README.I128
- README.LinkRit
- README.Linux
- README.MGA
- README.Mach32
- README.Mach64
- README.NVIDIA
- README.Oak
- README.P5000
- README.S3
- README.S3V
- README.S1S
- README.Video7
- README.W32
- README.WestDg
- README.apx
- README.P5000
- README.ark
- README.ati
- README.chips
- README.cirrus
- README.rendition
- README.clikprog
- README.trident
- README.cyrix
- README.epson
- README.tseng
- README.1740
- README.mouse
- README.neo

For example, if your notebook uses a variant of the NeoMagic graphics chipset, the file `README.neo` contains information about options you can use in your system’s `XF86Config` file that can help you with the following:

- Troubleshooting display flicker problems
- Understanding color-depth support
- Configuring your notebook to use an external display
- Finding out what notebooks use a similar chipset
- How to specifically set video RAM settings
- Using various driver options to stretch or shrink your display

### X11 Font Configuration

X11 fonts are stored in various directories under the `/usr/X11R6/lib/X11/fonts` directory. Each font directory contains various font files, along with a font directory file named `fonts.dir`. This file is created with the `mkfontdir` X11 client, and it
