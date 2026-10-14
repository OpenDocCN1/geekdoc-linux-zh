# Configuration Using xf86config

In most cases, XF86Setup is superior to xf86config as a simple configuration tool. There are, nevertheless, some rare cases where XF86Setup fails. If so, just use xf86config, which almost always works.

XFree86-4.0 includes a similar text-based program, xf86config. At some points, this contains dialogs that have been somewhat modified and, of course, it writes the configuration file to /etc/X11/XF86Config. In XFree86-4.0 however, the use of xf86config is usually not needed, since “problem” graphics cards can also be configured with the framebuffer or with the vga module as described in Section FAQ and Troubleshooting on page 147.

Make sure you have the following information available:

+   - mouse type, port to which the mouse is connected, and baud rate (the baud rate is normally optional)
+   - specifications of the graphics card
+   - monitor data (frequencies, etc.)

If these settings are known or you have your manuals at hand, start the configuration. Remember that you have to be root to do this.
The configuration is started with:

```
earth:/root # /usr/X11R6/bin/xf86config
```

# Mouse

Following the welcome screen, you will be asked about your mouse type. You will be presented with the following selections:

+   1. Microsoft compatible (2-button protocol)
+   2. Mouse Systems (3-button protocol)
+   3. Bus Mouse
+   4. PS/2 Mouse
+   5. Logitech Mouse (serial, old type, Logitech protocol)
+   6. Logitech MouseMan (Microsoft compatible)
+   7. MM Series
+   8. MM HitTablet

*Output 5: Mouse Selection for X*

While selecting the mouse, bear in mind that many of the new Logitech mice are either Microsoft compatible or use the MouseMan protocol. The selection Bus Mouse refers to any bus mouse, including Logitech.