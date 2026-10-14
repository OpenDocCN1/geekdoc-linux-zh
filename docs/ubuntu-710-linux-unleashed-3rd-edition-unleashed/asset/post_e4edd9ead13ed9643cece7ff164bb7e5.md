
These modules can range from special video card support to font rasterizers. The modules are located in subdirectories under the /usr/lib/modules directory.

## The InputDevice Section

The InputDevice section configures a specific device, such as a keyboard or mouse, as in this example:

```
Section "InputDevice"
    Identifier  "Keyboard0"
    Driver      "kbd"

    Option      "XkbModel"      "pc105"
    Option      "XkbLayout"     "us"
EndSection
Section "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Protocol" "IMPS/2"
    Option      "Device"  "/dev/input/mice"
    Option      "ZAxisMapping" "4 5"
    Option      "Emulate3Buttons" "yes"
EndSection
```

You can configure multiple devices, and there might be multiple InputDevice sections. The preceding example specifies a basic keyboard and a two-button PS/2 mouse (actually, a Dell touchpad pointer). An InputDevice section that specifies use of a USB device could be used at the same time (to enable mousing with PS/2 and USB pointers) and might look like this:

```
Section "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Device"  "/dev/input/mice"
    Option      "Protocol" "IMPS/2"
    Option      "Emulate3Buttons" "off"
    Option      "ZAxisMapping" "4 5"
EndSection
```

## The Monitor Section

The Monitor section configures the designated display device as declared in the ServerLayout section, as shown in this example:

```
Section "Monitor"
    Identifier  "Monitor0"
    VendorName  "Monitor Vendor"
    ModelName   "Monitor Model"
    DisplaySize 300    220
    HorizSync    31.5-48.5
    VertRefresh 50-70
    Option "dpms"
EndSection
```

Note that the X server automatically determines the best video timings according to the horizontal and vertical sync and refresh values in this section. If required, old-style modeline entries (used by distributions and servers prior to XFree86 4.0) might still be used. If the monitor is automatically detected when you configure X (see the “Configuring X” section, later in this chapter), its definition and capabilities are inserted in your xorg.conf file from the MonitorsDB database. This database contains more than 600 monitors and is located in the /usr/share/hwdata directory.

## The Device Section

The Device section provides details about the video graphics chipset used by the computer, as in this example:

```
Section "Device"
    Identifier  "Videocard0"
    Driver      "radeon"
    VendorName  "Videocard vendor"
    BoardName   "ATI Radeon Mobility M6"

EndSection
```

This example identifies an installed video card as using an ATI Mobility M6 graphics chipset. The Driver entry tells the Xorg server to load the radeon_drv.o module from the /usr/lib/modules/drivers directory. Different chipsets have different options. For example, here’s the entry for a NeoMagic video chipset:

```
Section "Device"
    Identifier  "NeoMagic (laptop/notebook)"
    Driver      "neomagic"
    VendorName  "NeoMagic (laptop/notebook)"
    BoardName   "NeoMagic (laptop/notebook)"
    Option      "externDisp"
    Option      "internDisp"
EndSection
```

In this example, the Device section specifies the driver for the graphics card (neomagic_drv.o) and enables two chipset options (externDisp and internDisp) to allow display on the laptop’s LCD screen and an attached monitor.

The Xorg server supports hundreds of different video chipsets. If you configure X11 but subsequently change the installed video card, you need to edit the existing Device section or generate a new xorg.conf file, using one of the X configuration tools discussed in this chapter, to reflect the new card’s capabilities. You can find details about options for some chips in a companion man page. You should look at these sources for hints about optimizations and troubleshooting.

## The Screen Section

The Screen section ties together the information from the previous sections (using the Screen0, Device, and Monitor Identifier entries). It can also specify one or more color depths and resolutions for the session. Here’s an example:

```
Section "Screen"
    Identifier "Screen0"
    Device     "Videocard0"
    Monitor    "Monitor0"
    DefaultDepth 24
    SubSection "Display"
        Viewport   0 0
        Depth      16
        Modes      "1024x768" "800x600" "640x480"
    EndSubSection
EndSection
```

In this example, a color depth of thousands of colors and a resolution of 1024x768 is the default, with optional resolutions of 800x600 and 640x480. Multiple Display subsection entries with different color depths and resolutions (with settings such as Depth 24 for millions of colors) can be used if supported by the graphics card and monitor combination. You can also use a DefaultDepth entry (which is 24, or thousands of colors, in the example), along with a specific color depth to standardize display depths in installations.

You can also specify a desktop resolution larger than that supported by the hardware in your monitor or notebook display. This setting is known as a virtual resolution in the Display subsection. This allows, for example, an 800x600 display to pan (that is, slide around inside) a virtual window of 1024x768.

> NOTE
> If your monitor and graphics card support multiple resolutions and the settings are properly configured, you can use the key combination of Ctrl+Alt+Keypad+ or Ctrl+Alt+Keypad- to change resolutions on the fly during your X session.

## Configuring X

Although the Ubuntu installer can be used to configure X during installation, problems can arise if the PC’s video card is not recognized. If you are unable to configure X during installation (refer to Chapter 1, "Installing Ubuntu"), do not specify booting to a graphical configuration and skip the X configuration portion of the installation. Note that some installs, such as for servers, don’t require that X be configured for use to support active X
