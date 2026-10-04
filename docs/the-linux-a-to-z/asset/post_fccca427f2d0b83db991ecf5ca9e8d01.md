
One of the most difficult parts to sort out in the X-configuration file is the ModeLine entries specified in this section. These entries just list sets of closely connected values which are associated with the various screen resolutions available. Again, an examples file is available to give lists of many common ModeLine entries:

/usr/X11R6/lib/X11/doc/modeDB.txt

If necessary, these values can be calculated, given enough information about all the hardware, but it is beyond the scope of this book to delve so deeply into the workings of X windows, especially when some of the required data about the monitor typically is not available in its specification sheet.

However, if you can't find suitable ModeLines in the example file, you should read the documentation in the file:

/usr/X11R6/lib/X11/doc/VideoModes.doc

The contents of the quotes (") in each ModeLine entry is just a label to allow reference to be made to these lines later in the file. By convention, these labels are given mnemonic significance, though this is not strictly necessary.

### 10.2.6 Device Section

This is the section which describes your video card and its characteristics to the X-server. Initially, you need not put many values in this section, as, in general, the X-server is capable of probing the hardware to discover most of the values for itself. The only entry you must supply is the Identifier definition, which is, again, just a label by which this section can be referenced later. Once you have used the server to probe the hardware (we'll look at how to do this a little later), then extra details can be filled in to give a device section which could look as follows:

```
Section "Device"
    Identifier  "My video card"
    Chipset     "et4000"
    VideoRam    1024
    Clocks      25.20 28.32 32.50 36.00 40.00 44.90 31.50 37.50
    Clocks      50.30 56.70 64.90 72.00 80.00 89.80 63.00 75.10
EndSection
```

### 10.2.7 Screen Section

This final section is the place where all the labels from previous sections are drawn together:

```
Section "Screen"
    Driver      "SVGA"
    Device      "My video card"
    Monitor     "My monitor"
    Subsection  "Display"
        Depth       8
        Virtual     1024 1024
        ViewPort    0 0
        Modes       "800x600" "1024x768" "640x480"
    EndSubsection
EndSection
```

The Driver definition specifies which X server you are using – SVGA specifies the XF86_SVGA server. The Device and Monitor use previously defined symbolic names to refer back to the appropriate sections.

Then, in the Display subsection, more display related details are given. Depth specifies the number of bits per pixel. Virtual specifies the size of the virtual screen in pixels. The size of the virtual screen must fit into the size of display memory on your video card. ViewPort says where on the virtual screen the top left corner of the physical screen will appear. If the current screen resolution is less than the virtual screen size, then it is possible to pan around the virtual screen under the control of the mouse. Finally, Modes gives a list of the video modes that you want to be able to use. The first mode in the list will be the default screen resolution when X-windows first executes.

Once X-windows is running, the other video modes can be accessed using the Ctrl-Alt-Plus and Ctrl-Alt-Minus key combinations. The Plus and Minus keys in these combinations are the + and - keys on the keyboard's numeric keypad.

### 10.2.8 Probing the Hardware

When you get to this stage, it is a good idea to start the X-server. However, for the time being, it should be set up only to probe the hardware, so that you can extract the information required to fill in the details in the device section that we left out earlier. This is easily done with the X command:

```
$ X -probeonly
```

The following listing gives some typical output for the previous command:

```
XF86Config: /etc/XF86Config
(**) stands for supplied, (--) stands for probed/default values
(**) Mouse: type: MouseSystems, device: /dev/mouse, baudrate: 1200
(**) SVGA: Graphics device ID: "ET4000"
(**) SVGA: Monitor ID: "Tatung XGA"
(**) FontPath set to "/usr/X11R6/lib/X11/fonts/misc/,/usr/X11R6/lib/X11/fonts/Type1/,/usr/X11R6/lib/X11/fonts/Speedo/,/usr/X11R6/lib/X11/fonts/75dpi/"
(--) SVGA: ET4000: Initial hibit state: high
(--) SVGA: chipset: et4000
(--) SVGA: videoram: 1024k
(--) SVGA: clocks: 25.14 28.32 32.43 35.93 39.95 44.85 31.44 37.52
(--) SVGA: clocks: 50.28 56.55 64.86 71.96 79.97 89.75 62.94 74.91
(--) SVGA: Maximum allowed dot-clock: 90.000 MHz
(**) SVGA: Mode "800x600": mode clock = 36.000, clock used = 35.930
(**) SVGA: Mode "640x480": mode clock = 25.000, clock used = 25.140
(**) SVGA: Mode "1024x768": mode clock = 65.000, clock used = 64.860
(**) SVGA: Virtual resolution set to 1024x1024
(--) SVGA: Generic SpeedUps selected (Flags=0x30)
(--) SVGA: ET4000: SpeedUps selected (Flags=0xf)
```

As indicated by the second line of the output, lines preceded by (**) are for values that have been specified in the XF86Config file, while lines preceded with (--) contain values which the server discovered by probing the hardware.

This shows where to obtain the values which are subsequently plugged back into the device section of the XF86Config file. Once the values have been added to the configuration file, the X-server will not probe the hardware for the values when it is run on subsequent occasions.

## 10.3 Starting X-windows

Once the XF86Config file is set up, you can start up X-windows properly. On non-Linux systems you may have seen the command xinit to start up X-windows. Under Linux, this is done with the command:

```
$ startx
```

which actually arranges to run xinit anyway. During the X-initialization sequence, xinit will also run any commands found in the file .xinitrc in your home directory (if the file exists). If you don't have a personal .xinitrc file, then xinit will look for the file:

/usr/X11R6/lib/X11/xinit/xinitrc

### 10.3.1 .xinitrc

The .xinitrc file is used to specify the initial configuration of the X-windows display. Typically, it will be used to start X-windows with certain applications already running. It can also be used to determine the initial screen layout, specifying where on the screen the windows for the initial applications should be placed. For example:

```
#!/bin/sh

xterm -geometry 80x43+220+0 -bg gray -fg black &
exec fvwm
```

The first line of this file specifies that the rest of the file should be interpreted using the /bin/sh shell program rather than your current shell. The second line causes the program xterm to be executed. This program is a standard terminal emulator which provides emulation of both the DEC VT102 text terminal and the Tektronix 4014 graphics terminal. The & on the end of the line is needed to push the command into the background so that the rest of the script can be executed without waiting for the xterm to terminate first. The last line in the example starts up a window manager (fvwm here), of which there are many, each offering slightly different look and feel to the X-windows environment.

It is possible to start up several applications between the shell and the window manager. In general, any extra commands should be terminated with an ampersand (&) character, like the xterm line in the example. Note that the line which starts the window manager is not pushed into the background like the rest, but replaces the current process by being run with exec command.

When the window manager terminates, the X-server is shut down, closing your X-windows session. This is normally done with a menu option, as you will see later. The server can also be shut down directly by pressing the keyboard key combination Ctrl-Alt-Backspace.

## 10.4 fvwm

The fvwm window manager provides a virtual windows system that allows multiple desktops to be accessed via a simple pager window. When fvwm is executed it will search for a configuration file, specified in your home directory, called .fvwmrc. This file, if it exists, is used to set up a lot of details about the window manager's operation. It covers such things as the colors used for window backgrounds, and active and passive window borders. It specifies which windows will move with you when you switch desktops, and which will be left behind. It allows you to specify which applications are sufficiently important that their windows are not normally overlaid, and thus remain visible however cluttered the desktop gets. It also allows you to set up your own menus and actions to be bound to the mouse buttons (and some of the keys on the keyboard) when various parts of a window's border and background are selected. Some typical .fvwmrc contents are given in the next example. Full details of all the options can be found in the manual page for the fvwm command:
