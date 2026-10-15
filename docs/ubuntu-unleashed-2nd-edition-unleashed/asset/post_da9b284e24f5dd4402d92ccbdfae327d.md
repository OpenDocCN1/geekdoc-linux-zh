
This example identifies an installed video card as using an ATI Radeon 9600 XT (RV350) graphics chipset. The Driver entry tells the Xorg server to load the fglrx_drv.o module from the /usr/lib/xorg/modules/drivers directory. Different chipsets have different options. For example, here's the entry for a NeoMagic video chipset:

```
Section "Device"
    Identifier    "NeoMagic (laptop/notebook)"
    Driver        "neomagic"
    VendorName    "NeoMagic (laptop/notebook)"
    BoardName     "NeoMagic (laptop/notebook)"
    Option        "externDisp"
    Option        "internDisp"
EndSection
```

In this example, the Device section specifies the driver for the graphics card (neomagic_drv.o) and enables two chipset options (externDisp and internDisp) to allow display on the laptop's LCD screen and an attached monitor.

The Xorg server supports hundreds of different video chipsets. If you configure X11 but subsequently change the installed video card, you need to edit the existing Device section or generate a new xorg.conf file, using one of the X configuration tools discussed in this chapter, to reflect the new card's capabilities. You can find details about options for some chipsets in a companion man page or in a README file under the /usr/lib/X11/doc directory. You should look at these sources for hints about optimizations and troubleshooting. However, all this should be fairly rare as Ubuntu sports a comprehensive hardware detection system, automatically adjusting settings to take account of newly installed hardware.

## The Screen Section

The Screen section ties together the information from the previous sections (using the Screen0, Device, and Monitor Identifier entries). It can also specify one or more color depths and resolutions for the session. Here's an example:

```
Section "Screen"
    Identifier        "Default Screen"
    Device            "ATI Technologies, Inc. RV350 AR [Radeon 9600 XT]"
    Monitor           "C17-5"
    DefaultDepth      24
    SubSection "Display"
        Depth          24
        Modes          "1280x1024" "1024x768" "800x600" "640x480"
    EndSubSection
    SubSection "Display"
        Depth          16
        Modes          "1280x1024" "1024x768" "800x600" "640x480"
    EndSubSection
    SubSection "Display"
```

```
Depth        8
Modes        "1280x1024" "1024x768" "800x600" "640x480"
EndSubSection
...
```

In this example a color depth of millions of colors and a resolution of 1280x1024 is the default, with optional resolutions of 1024x768, 800x600, and 640x480. Multiple Display subsection entries with different color depths and resolutions (with settings such as Depth 16 for thousands of colors) can be used if supported by the graphics card and monitor combination. You can also use a DefaultDepth entry (which is 24, or millions of colors, in the example), along with a specific color depth to standardize display depths in installations.

You can also specify a desktop resolution larger than that supported by the hardware in your monitor or notebook display. This setting is known as a virtual resolution in the Display subsection. This allows, for example, an 800x600 display to pan (that is, slide around inside) a virtual window of 1024x768.

### NOTE

> If your monitor and graphics card support multiple resolutions and the settings are properly configured, you can use the key combination of Ctrl+Alt+Keypad+ or Ctrl+Alt+Keypad- to change resolutions on the fly during your X session.

## Configuring X

Although the Ubuntu installer can be relied upon to configure X during installation, problems can arise if the PC's video card is not recognized. If you do not get the graphical login that should come up when you reboot after installation (refer to Chapter 3, "Installing Ubuntu"), then you will have to do some configuration by hand in order to get X working. Note that some installs, such as for servers, do not require that X be configured for use to support active X sessions, but might require installation of X and related software to support remote users and clients.

You can use the following configuration tools, among others, to create a working xorg.conf file:

- dpkg --reconfigure xserver-xorg—This is Ubuntu's text-based configuration tool, which guides you through creating an xorg.conf file.
- Xorg—The X server itself can create a skeletal working configuration.

The following sections discuss how to use each of these software tools to create a working xorg.conf file.
