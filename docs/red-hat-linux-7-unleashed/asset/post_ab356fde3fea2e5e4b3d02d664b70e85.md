
## XF86Config Module Section

As you can see, you'll find additional fonts for X11 installed under the `/usr/share/fonts` directory. The ISO8859-2 fonts are part of a collection of nearly 400 central European (or Latin 2) fonts, and provide support for encoding characters in nearly a dozen Slavic and Central European languages.

You can verify the inclusion and availability of these fonts with the `xfontsel` client. Use `xfontsel` like this at the command line of a terminal window:

```
# xfontsel
```

You'll see a window (as shown in Figure 4.10) from which you can select different foundry and families of fonts (by clicking fmly).

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_130_0.png)

The `Module` section is used to load server and rendering support, and specifies the names of modules to load from the `/usr/X11R6/lib/modules` directory:

```
Section "Module"
	Load "GLCore"
	Load "dbe"
	Load "dri"
	Load "extmod"
	Load "glx"
	Load "pex5"
	Load "record"
	Load "xie"
	Load "type1"
	Load "freetype"
EndSection
```

In this example, nearly all rendering and drawing support libraries are loaded, along with support for Type1 and TrueType fonts. The software libraries reside under the `/usr/X11R6/lib/modules/extensions` directory, and not all are required for proper windowing support for your X11 window manager. For example, don't load the `dri` module if you do not use an accelerated 3D graphics card.

This new approach to providing support for new graphics hardware in the form of loadable modules is already being used by some manufacturers. For example, 3dfx Interactive, Inc., manufacturer of the Voodoo and Banshee line of graphics cards, provides numerous links and modules to support its new hardware under XFree86 4.0.1. Browse to `http://linux.3dfx.com` for more details.

### XF86Config ServerFlags Section

The `ServerFlags` section can be used to configure special actions allowed by your XFree86 X server. Enable a particular action by including the `Option` keyword, followed by the desired option. Some options should generally not be enabled, such as disabling the ability to kill the server session (`DontZap`):

```
Section "ServerFlags"
#   Option    "DontZap"
#   Option    "DontZoom"
#   Option    "blank time"  "10"    # 10 minutes
    Option    "standby time"  "20"
    Option    "suspend time"  "30"
    Option    "off time"      "60"
#   Option    "NoPM"
    Option    "AllowMouseOpenFail"
EndSection
```

Not all the available options are shown. The `DontZoom` feature may be disabled if you use X in only one video resolution, such as 800×600 pixels. However, you should note the new options to control screensaving (`blank time`) and DPMS. You can use these settings to control your display for power saving. The `NoPM` option disables DPMS. The `AllowMouseOpenFail` option allows the server to start without a pointer device.

### XF86Config InputDevice Section

The `InputDevice` sections tell the X server to expect a keyboard and type of mouse. The XFree86 3.3.6-format Keyboard and Pointer sections are still recognized for compatibility, but the new `InputDevice` sections should be used in your `XF86Config` instead.

```
# InputDevice (Keyboard)
Section "InputDevice"
    Identifier    "Keyboard0"
    Driver "keyboard"
    Option "XkbLayout" "us"
EndSection

# InputDevice (PS/2 pointer)
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "auto"
Option "Device" "/dev/mouse"
Option "Protocol" "PS/2"
EndSection
```

In this example, a single keyboard, using US layout, and a single mouse, using PS/2 protocol, are defined for use during the X session. You may have multiple devices defined for use. The `auto` protocol option may be used if your system has Plug-and-Play mouse detection.

To define a USB mouse, use the IMPS/2 device option (because Linux supports PS/2 mouse initialization), along with a pointer to the USB mouse device like this:

```
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "Protocol" "IMPS/2"
Option "Device" "/dev/input/mice"
EndSection
```

Note that you'll also want to run the `gpm` daemon with the proper settings before starting X:

```
# gpm -t ps2 -m /dev/input/mice
```

Of course, the best solution to install a USB mouse is to use the `mouseconfig` command. Two-button mouse users will definitely want to enable three-button emulation, in which a simultaneous pressing of both buttons simulates the middle (or Button 2) press. One common use of Button 2 is to paste text or graphics. For more information about configuring a mouse, see the file `README.mouse` under the `/usr/X11R6/lib/X11/doc` directory. Information regarding USB input devices will be found in the file `input.txt` under the `/usr/share/doc/kernel-doc-2.2.16/usb` directory.

## XF86Config Monitor Section

The Monitor section contains details such as your monitor's identifier, vendor's name, model name, and horizontal and vertical sync ranges. Note that the legacy modelines (one for each video resolution) are no longer required! The XFree86 server should automatically calculate the correct timings and frequencies!

```
Section   "Monitor"
    Identifier "LCD Panel 1024x768"
    VendorName "Unknown"
    ModelName  "Unknown"
    HorizSync  31.5-48.5
    VertRefresh 60
EndSection
```

However, if you need to include a modeline in the Monitor section, you can. This is especially helpful if you need to support an off-brand monitor or fine-tune your settings.

The basic parts of a mode are different values representing (from left to right):

- A label of the screen resolution, such as 800x600
- A video frequency (DotClock) in MHz
- The number of visible dots per line on your display
- The Start Horizontal Retrace value (number of pulses before video sync pulse starts)
- The End Horizontal Retrace value (end of sync pulse)
- The total number of visible and invisible dots on your display
- The Vertical Display End value (number of visible lines of dots on your display)
- The Start Vertical Retrace value (number of lines before the sync pulse starts)
- The End Vertical Retrace value (number of lines at the end of the sync pulse)
- The Vertical Total value (total number of visible and invisible lines on your display)

```
Mode     "1024x768"
        DotClock    45
        HTimings    1024 1048 1208 1264
        VTimings    768 776 784 817
EndMode
```

This example defines a modeline for use with a 1024×768 display (perhaps a laptop or LCD panel monitor). Problems can arise when you're faced with crafting a custom modeline for a monitor or display that falls outside the range of normal displays. For example, what if your display is 1024×480 (such as for a Sony ClXS laptop)? In this case, you can try using Andreas Bohne’s Web-based Modeline Calculator at http://www.dkfz-heidelberg.de/spec/linux/modeline/. Another, perhaps more flexible tool is Anders Ostreim’s modeline command, found at http://home.kvalito.no/~bagnthor/files/files.shtml.

## XF86Config Device Section

The Device section details your video chipset, the proper driver to load for chipset support, the graphics card memory, frequency settings for a clockchip, and other options. This section of your `XF86Config` file is critical—the device definition is used to tell the X server exactly what type of video chipset and options to support. Note that your computer's Device section and Driver entry will certainly be different from this (for a NeoMagic laptop):

```
# Device
Section "Device"
    Identifier    "NeoMagic Corporation||MagicMedia 256AV"
    Driver        "neomagic"
#   VideoRam      2048
#   Option      "intern_disp"
#   Option      "extern_disp"
#   Option      "lcd_center"
#   Option      "no_stretch"
EndSection
```

You may also have multiple Device sections defined in your `XF86Config`. This approach is used when you have more than one graphics card installed on your system, and want to use one or more displays. Also note that various Option entries may be included in the Device section.

Depending on the specified driver and your graphics chipset, you may find a number of options available for use. In the example, the `extern_disp` option may be used to enable the X session to be displayed on an external monitor (most likely by enabling a signal to the monitor port). You should always check your driver's documentation, in a README file under the `/usr/X11R6/lib/X11/doc` directory, man page, or through http://www.xfree86.org.

Some of the drivers included with XFree86 4.0.1 are listed in Table 4.2 (which was derived from the file named Status under the `/usr/X11R6/lib/X11/doc` directory). Note that the table reflects card support for the 4.0.1 release. Support for many more cards will be forthcoming in subsequent releases.

**TABLE 4.2 XFree86 4.0.1 Drivers and Supported Cards**

| Driver | Card |
| :--- | :--- |
| apm | Alliance AT24, 25, 3D |
| ati | ATI Mach64 cards, others |
| chips | C&T 65520, 65525, 65530, 65535, 65540, 65545, 65546, 65548, 65550, 65554, 69000, 64200, 64300 |
| cirrus | Cirrus Logic Alpine and Laguna chipset |
