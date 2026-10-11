> ALERT
> You will see questions about the format and sections of the `XF86Config` file, regardless of the version. If asked which section configures the pointing device, and the keyword `InputDevice` is not present, it's asking about the older file, and `Pointer` is correct. LPI exams always give you just enough information to answer the question, no more.

# Important XF86Config Sections

Some sections are more likely to be configured or to cause certain effects to happen, so we'll take them one by one to ensure you understand how they work and can be configured.

Here's the `Files` section:

```
"""
# Lots of comments removed...
RgbPath       "/usr/X11R6/lib/X11/rgb"
FontPath      "unix/:7100"
"""
```

The entries of importance in the `Files` section are

+   - `RgbPath`—The database of colors and aliases (names) that applications will use
+   - `FontPath`—Can be a local path (`unix/:7100`), a remote system (`tcp/some.domain.com:7100`), or an X font server path (in a later section)

> ALERT
> It's important to know the entries for a local path and how to denote a remote path. References to remote systems are typically pointing to a font server, and are used by multiple machines to enforce common fonts in an application.

The `InputDevice` section is as follows:

```
Section "InputDevice"
    Identifier "mouse0"
    Driver    "mouse"
    Option    "Protocol" "IMPS/2"
    Option    "Device" "/dev/psaux"
    Option    "ZAxisMapping" "4 5"
    Option    "Emulate3Buttons" "no"
EndSection
```

The entries of importance in the `InputDevice` section are

+   - `Driver`—This is the actual driver for the mouse. It's loaded and, if it's not the right one, the mouse won't function.
+   - `Protocol`—This is the communication method used to interpret the mouse movements (if the scroll wheel doesn't work, try `IMPS` rather than `ps/2`). USB mouse devices might need the `Auto` protocol.