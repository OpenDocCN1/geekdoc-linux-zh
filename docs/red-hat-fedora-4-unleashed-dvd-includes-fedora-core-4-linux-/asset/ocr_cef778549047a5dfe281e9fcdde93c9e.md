![](bbox=[0.15, 0.08, 0.83, 0.41])

**FIGURE 4.3**  The mouseconfig command can be used to configure a new pointing device.

Pointer configuration entries are stored in the file `/etc/sysconfig/mouse`, and can be examined like this:

```
# cat /etc/sysconfig/mouse
MOUSETYPE="ps/2"
XMOUSETYPE="PS/2"
FULLNAME="Generic Mouse (USB)"
XEMU3=yes
DEVICE=/dev/mouse
```

In this example, a two-button USB pointer emulates a PS/2 pointing device.

The corresponding entry contained in the `/etc/X11/xorg.conf`, used by X.org for the Fedora desktop looks like

```
Section "InputDevice"
    Identifier    "Mouse0"
    # Modified by mouseconfig
    Driver      "mouse"
    Option        "Device"        "/dev/mouse"
    Option        "Protocol"      "PS/2"
    Option        "Emulate3Buttons"    "yes"
    #Option      "ZAxisMapping"      "4 5"
EndSection
```

This entry enables the use of a USB pointing device during X sessions. See Chapter 6 to learn about X.