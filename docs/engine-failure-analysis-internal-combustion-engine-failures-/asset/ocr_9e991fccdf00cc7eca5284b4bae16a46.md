To use the devices defined in this section, you must tell the X server to load the appropriate module. You can do so by means of an entry in the Modules section, which was discussed earlier.

The following table discusses the entries you can use to define a joystick subsection.

# JOYSTICK SUBSECTION OPTIONS

| Use This Entry | To Do This |
|---|---|
| **AlwaysCore** | Enable core pointer sharing |
| **CenterX** *value* | Set the X center when the joystick is idle |
| **CenterY** *value* | Set the Y center when the joystick is idle |
| **Delta** *value* | Set the maximum value |
| **DeviceName** *name* | Specify the name of the device |
| **MaximumXPosition** *value* | Set the maximum X value |
| **MaximumYPosition** *value* | Set the maximum Y value |
| **MinimumXPosition** *value* | Set the minimum X value |
| **MinimumYPosition** *value* | Set the minimum Y value |
| **Port** *path* | Specify the path to the device driver |
| **TimeOut** *timeout* | Set the time (in milliseconds) between two polls of the device driver |

# XFree86 Version 4

The latest version of XFree 86, version 4, is now becoming available in Linux distributions and was released just as this book was going to press; future editions will fully document the version 4 configuration file. This section highlights the most important changes from version 3.3:

+   - **Single Binary** Previous versions of XFree86 used several separate binaries designed for the various classes of video drivers and displays. In version 4, there is one XFree86 binary; it is designed to work with loadable modules so that the binary itself does not have to be uninstalled (and a different one installed subsequently) when you change video drivers.