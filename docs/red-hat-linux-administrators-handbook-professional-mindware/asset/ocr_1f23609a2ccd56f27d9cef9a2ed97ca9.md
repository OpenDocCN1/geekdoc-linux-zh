# Table 14-3 *Continued*

| Option | Description |
|---|---|
| Emulate3Timeout | Use to set the timeout (in milliseconds) for three-button emulation. The X server will wait for the specified number of milliseconds to decide whether or not a third button was pressed when you had down both of the buttons. |

Monitor section: Used to describe your monitor. This is the most commonly modified section in the XF86Config file. Here is an example of this section:

```
Section "Monitor"

Identifier "My Monitor"
VendorName "Unknown"
ModelName "Unknown"
 HorizSync 31.5 - 82.0
 VertRefresh 50-100

# This is a set of standard mode timings.
# Modes that are out of monitor spec
# are automatically deleted by the server
# (provided the HorizSync and VertRefresh lines
# are correct), so there's no immediate need to
# delete mode timings (unless particular mode
# timings
# don't work on your monitor). With these modes,
# the best standard mode that your monitor
# and video card can support for a given resolution
# is automatically used.

# 640x400 @ 70 Hz, 31.5 kHz hsync
Modeline "640x400" 25.175 640 664 760 800 400
 409 411 450

# 640x480 @ 60 Hz, 31.5 kHz hsync
```