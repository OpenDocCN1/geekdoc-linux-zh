
| Entry | Function |
|:---|:---|
| SuspendTime <Time> | Specifies the timeout for the monitor to enter Suspend power-saving mode, in minutes. The default is 30. |
| OffTime <Time> | Specifies the timeout for the monitor to power off, in minutes. The default is 40. |
| SubSection "Display" | Begins a block that configures display specific information. Table 9-7 shows the entries available in this subsection. |

### Table 9-7 Display Subsection Entries

| Entry | Function |
|:---|:---|
| Depth <bpp> | Specifies the default color depth that the X server will run. |
| Weight <RGB> | An optional entry that specifies the RGB weight to use when in 16 bpp (bits per pixel) mode. |
| Virtual <x dimensions> <y dimensions> | Defines the virtual desktop dimensions. This is used to give the user a larger desktop than his or her monitor can handle. |
| ViewPort <x0> <y0> | Sets the starting location of the upper left corner when a virtual desktop is used. If this entry is omitted, the display is centered in the virtual desktop. |
| Modes "Mode Name" ... | Specifies a list of mode entries to use for this display. |
| Option "Option String" | Allows you to send special settings to the driver or X server. |

### Using XF86Setup

XF86Setup is a graphical configuration tool. It uses the 16-color VGA X server, which should work on almost all video cards. Figure 9-1 shows the main configuration screen. XF86Setup uses a tabbed type interface, with these screens:

- Mouse
- Keyboard
- Card
- Monitor
- Mode selection
- Other

To start the configuration, just type **XF86Setup**. Once you have gone through all of the tabs click Done, and XF86Setup will test the X server with your settings. The following sections describe each of the tabs.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_382_0.png)

**Figure 9-1:** XF86Setup tool

### Mouse

The Mouse tab allows you to set the options for your pointing device. This screen is shown in Figure 9-2. When you first go to this tab, you are presented with a screen that shows the keyboard shortcuts to move around. This way you can navigate around to set up your mouse before the mouse begins to work. Choose the correct mouse type, device, and number of buttons. If you have a two-button mouse be sure to enable three-button emulation.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_383_0.png)

### Keyboard

The Keyboard tab allows you to set the options for your keyboard. This screen is shown in Figure 9-3. Choose the correct keyboard type, and the Shift and Control key functions.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_383_1.png)

### Card

The Card tab allows you to set the options for your video card. This screen is shown in Figure 9-4. Choose the correct video card for your system. If your card is not listed, try to find another listing for the video chipset it uses or pick another card that uses the same chipset. The Detailed Setup option lets you define manual entries to the X configuration file and specify the amount of video RAM on your card.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_384_0.png)

**Figure 9-4:** Card tab

### Monitor

The Monitor tab allows you to set the resolution options for your monitor. This screen is shown in Figure 9-5. Choose the resolution and refresh rates that match your monitor. If none of the options match, you can enter the horizontal and vertical sync rates for your monitor. These settings should be available in your monitor manual.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_385_0.png)

**Figure 9-5:** Monitor tab

### Mode selection

The Mode selection tab allows you to set the resolutions and color depths to run while in X. This screen is shown in Figure 9-6. Choose the resolutions that you want to have available while in X, as well as the default color depth. Table 9-8 lists the color depths. Not all X servers support all color depths.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_385_1.png)

**Figure 9-6:** Mode selection tab

### Table 9-8 Color Depths

| Bit Depth | Colors |
|:---|:---|
| 8bpp | 256 colors |
| 16bpp | 65,535 colors |
| 24bpp | 16.7 million colors |
| 32bpp | 16.7 million colors (faster on some video cards) |

### Other

The last tab is the Other tab, which has miscellaneous settings. This screen is shown in Figure 9-7. This screen lets you set several small options, such as how to kill the server, whether clients can change the video mode, and who can change keyboard and mouse settings.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_386_0.png)

> **Exam Tip** XF86Setup provides an easy-to-use graphical interface for configuring your X server.

### Using xf86config

Another XFree86 configuration tool is `xf86config`. It is a text mode tool that uses a series of menus to gather input from the user. It is not as pretty as XF86Setup, but it does not require the 16-color VGA server to be installed.

> **Note** Do not get confused between **XF86Config** and `xf86config`. **XF86Config** is the configuration file, and `xf86config` is the tool that can be used to create it.

Figure 9-8 shows an example of `xf86config`. This tool is much more cumbersome to use than XF86Setup and requires more intimate knowledge of the hardware present in your system. We don’t recommend that you use this tool unless you have problems with the others. The following steps walk you through the configuration process.

1. The first few screens configure your mouse. Choose the correct type of mouse you have or the closest option offered.
2. Choose whether to enable three-button emulation for two-button mice.
3. Enter the path to the mouse device. Most distributions link the file `/dev/mouse` to the actual interface device. So if you are unsure, try `/dev/mouse`.
4. The next couple of screens explain the keyboard maps and prompt you to choose the correct keymap. Choose the correct one for your system. Most users should choose option 1 or 2.
5. The next few screens configure the monitor. Choose the synchronization rates for your monitor. If there is no entry that matches your monitor, enter the rates listed in your monitor manual.
6. Next, you will be prompted for three text strings. These are the identifier, vendor, and model of your monitor. These are used to keep different monitor configurations separate in the X configuration file. There are no wrong answers, so type in the information requested in case you need to reference it later in the X configuration file.
7. Next, you will be prompted for your video card or chipset. A long list of available configurations is displayed. Scroll through the list and enter the number that closest matches the video card or video chipset in your system.
8. Choose the correct X server for your video card. The last option presented tells `xf86config` to install the X server specified in the video card configuration you chose. This is usually the best option to take.
9. Specify the amount of video memory installed in your system.
10. Again, you will be prompted for three strings making up the identifier, vendor, and model. Enter information that is appropriate for your configuration should you need to reference it later in the X configuration file.
11. Some video cards require a RAMDAC setting. Check with your video card manufacturer or look on the card itself for the RAMDAC chipmaker. This is usually a large chip near the video output connector.
12. Some video cards have a programmable clock chip that requires configuration. Newer video cards do not use this. Unless you know your video card requires this setting, hit Enter to go on without making a selection.
13. Older video cards required clock probes to get the correct clock information. This could either be done during setup and put in the configuration file or be done every time the X server started. Unless your video card is several years old it is best to not do a probe.
14. The next several screens let you set the supported resolutions and color depths. The default settings are displayed, but you have the option to change them if you want.
15. Virtual desktops allow you to have a resolution that is larger than your monitor can support. This way you can scroll around the larger desktop and have more workspace. When prompted, tell `xf86config` whether you want to use virtual desktops or not.
16. The final step is to have `xf86config` write the new `XF86Config` file.

```
Now you must determine which server to run. Refer to the manpages and other documentation.  The following servers are available (they may not all be installed on your system):
        1  The XF86_Mono server.  This is a monochrome server that should work on any
           VGA-compatible card, in 640x480 (more on some SVGA chipsets).
        2  The XF86_VGA16 server.  This is a 16-color VGA server that should work on
           any VGA-compatible card.  This is a 16-color VGA server that should work
           on any SVGA-compatible card.
        3  The XF86_SVGA server.  This is a 256 color SVGA server that supports
           a number of SVGA chipsets.  Its some chipsets it is accelerated or
           supports higher color depths.
        4  The accelerated servers.  These include XF86_S3, XF86_Mach32, XF86_Mach8,
           XF86_R514, XF86_P9000, XF86_RDX, XF86_W12Z, XF86_Mach64, XF86_1126,
           XF86_S3V, and XF86_3DLabs.

These four server types correspond to the four different "Screen" sections in
XF86Config (vga2, vga16, svga, accel).

        5  Choose the server from the card definition, XF86_S3.
Which one of these server types do you intend to run by default (1-5)?
```

![](img/96d9ccd181675a8ae8b6a1146c919d2b_388_0.png)

> **Exam Tip** `xf86config` is a text mode configuration tool that is harder to use than XF86Setup.

### Detecting video hardware

The *SuperProbe* tool can be used to probe the video hardware in a system and report back information. This information can be useful for determining which video card to choose with the other XF86Config creation tools. Be careful though; this tool can cause the system to lock up, requiring you to reboot. The following is an example of its output:
