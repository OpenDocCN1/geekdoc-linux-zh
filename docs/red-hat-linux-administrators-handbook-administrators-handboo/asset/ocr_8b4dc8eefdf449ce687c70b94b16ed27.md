**Device.** Specifies the device path. If you use a mouse as your pointing device and have it connected to serial port 1 (cua0) or serial port 2 (cua1), you can specify /dev/cua0 or /dev/cua1, respectively. However, the best method is to create a symbolic link called /dev/mouse that points to your serial port device (cua0 or cua1), and have the device set to /dev/mouse. This way, if you change the port, you simply need to readjust the link, and not the configuration file as well.

Other commonly used options that you can add in this section are listed in Table 14-3.

# Table 14-3 Options for the Pointer Section of XF86Config

| Option | Description |
|---|---|
| BaudRate | Use to set the baud rate for your pointer device. |
| Port | Same use as the Device option, described in the preceding list. |
| Button | Use to set the number of buttons. |
| Emulates3Buttons | Use to emulate a three-button mouse with a two-button mouse. When you press both buttons together, the third button is emulated. |
| Emulate3Timeout | Use to set the timeout (in milliseconds) for three-button emulation. The X server will wait for the specified number of milliseconds to decide whether or not a third button was pressed when you hold down both of the buttons. |

# **Monitor section:** Used to describe your monitor.

This is the most commonly modified section in the XF86Config file. Here is an example of this section:

```
Section "Monitor"

Identifier "My Monitor"
VendorName "Unknown"
ModelName "Unknown"
HorizSync 31.5 - 82.0
VertRefresh 50-100

# This is a set of standard mode timings.
```