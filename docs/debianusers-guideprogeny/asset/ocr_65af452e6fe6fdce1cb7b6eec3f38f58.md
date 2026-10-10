If you have been using the mouse during the install, you can accept the settings listed. However, if your mouse is not working, you adjust the settings.

+   1.  Select the port to use.
+       In most cases, it is `/dev/ttyS0` (COM1) or `/dev/ttyS1` (COM2) for a serial mouse, or `/dev/psaux` for a PS2 mouse.

+   2.  Select the protocol or driver to use.
+       If you are using a serial mouse, then select the name of the manufacturer from the drop-down list. Use `ps2` for a generic `ps2` mouse.
+   
+       If you cannot find a protocol for your mouse or pointing device, select `Auto` to have it detected automatically.
+   
+       You can also try different protocols to see if your mouse can use them.

+   3.  Select **Emulate 3-button mouse** if you have a 2 button one.
+       With three button emulation, pressing both buttons on the pointer is the same as pressing the middle button on a three-button pointer.
+   
+       Linux is designed for use with a three-button mouse, so most users of two-button mouses should choose this option.

+   4.  Select “**Enable scroll-wheel event**” to use a scroll wheel.
+       If your mouse has a scroll wheel, you probably want this option.

+   5.  Select the Next button. The X Server screen opens.

> **Note**
> If you were not using a pointer but entered workable settings from the Pointer screen, the pointer becomes usable at the end of the configuration stage.