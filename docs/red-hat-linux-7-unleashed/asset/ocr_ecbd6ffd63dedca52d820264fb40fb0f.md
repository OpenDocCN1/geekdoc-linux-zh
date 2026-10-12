# Virtual Console Screen Devices

The virtual console (VC) screen devices provide read access to the VCs memory. This can be used to get screen capture capabilities for virtual consoles, for example. The devices are not readable by ordinary users; hence, other users cannot eavesdrop on your session.

There are two sets of device nodes for this purpose:

```
$ ls -l /dev/vcs[012] /dev/vcsa[012]
crw-w-----    1 root    tty    7,   0 Jul 21 16:29 /dev/vcs0
crw-w-----    1 root    tty    7,   1 Jul 21 16:29 /dev/vcs1
crw-w-----    1 root    tty    7,   2 Jul 21 16:29 /dev/vcs2
crw-w-----    1 root    tty    7, 128 Jul 21 16:29 /dev/vcsa0
crw-w-----    1 wsb     tty    7, 129 Jul 21 16:29 /dev/vcsa1
crw-w-----    1 root    tty    7, 130 Jul 21 16:29 /dev/vcsa2
```

Each set is numbered from 0 to 63, corresponding to the numbering system for the /dev/tty* console devices. The device /dev/vcs0, like the device /dev/tty0, always refers to the currently selected VC.

The /dev/vcs* files provide a snapshot of what is in view on the corresponding VC. This snapshot contains no newlines because there are none actually on the screen; after all, a newline character just moves the cursor. To make the captured data into the kind of thing you usually see in text files or send to printers, you need to add newlines in the appropriate places. This can be done with the dd command:

```
$ dd bs=80 conv=unblock </dev/vcs1 | lpr
```

This example works only if the screen actually is 80 columns wide. This is not always true; the kernel can set up a different video mode at boot time, and you can use the SVGATextMode command to change it at any time.

You can overcome this problem by using the other set of devices, /dev/vcsa*. Reading from these devices gives a header, followed by the screen data with attribute bytes. The header consists of two bytes indicating the screen size (height first), followed by two bytes indicating the cursor position. The screen data is provided at a rate of two bytes per character cell, the first containing the attribute byte and the second containing the character data (as with /dev/vcs*). You can use this data to provide full-color screen dumps and so on. The following script uses a /dev/vcsa device to determine the width of the VC and to get the conversion of the corresponding /dev/vcs device right:

```
#!/bin/sh

#Insist on exactly one argument (the VC number to dump)
[ $0 -eq 1] || { echo "usage: $0 [vc-number]";>; exit 1}
```