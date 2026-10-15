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

# The Screen Section

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