InputDevice "Mouse0" "CorePointer"
InputDevice "Keyboard0" "CoreKeyboard"
InputDevice "DevInputMice" "AlwaysCore"
EndSection

In this example, a single display is used (the numbers designate the position of a screen), and two default input devices, Mouse0 and Keyboard0, are used for the session.

# **The Files Section**

The Files section of the xorg.conf file might look like this:

Section "Files"
RgbPath "/usr/lib/X11/rgb"
FontPath "unix/:7100"
EndSection

This section lists available session colors (by name, in the text file rgb.txt) and the port number to the X font server. The font server, xfs, is started at boot time and does not require an active X session. If a font server is not used, the FontPath entry could instead list each font directory under the /usr/lib/X11/fonts directory, as in this example:

FontPath "/usr/lib/X11/fonts/100dpi:1"
FontPath "/usr/lib/X11/fonts/misc:1"
FontPath "/usr/lib/X11/fonts/75dpi:1"
FontPath "/usr/lib/X11/fonts/type1:1"
FontPath "/usr/lib/X11/fonts/Speedo"
...

These directories contain the default compressed fonts that are available for use during the X session. You configure the font server by using the file named config under the /etc/X11/fs directory. This file contains a listing, or catalog, of fonts for use by the font server. By adding an alternate server entry in this file and restarting the font server, you can specify remote font servers for use during X sessions. This can help centralize font support and reduce local storage requirements (even though only 25MB is required for the almost 5,000 fonts installed with Fedora and X).

# **The Module Section**

The Module section of the xorg.conf file specifies loadable modules or drivers to load for the X session. This section might look like this:

Section "Module"
Load "dbe"
Load "extmod"
Load "fbbdevhw"
Load "glx"
Load "record"