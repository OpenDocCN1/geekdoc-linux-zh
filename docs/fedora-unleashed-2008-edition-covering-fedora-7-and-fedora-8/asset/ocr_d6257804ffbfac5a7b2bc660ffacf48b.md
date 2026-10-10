```
```
Load        "freetype"
Load        "type1"
Load        "dri"
EndSection
```
```

These modules can range from special video card support to font rasterizers. The modules are located in subdirectories under the /usr/lib/modules directory.

# The InputDevice Section

The *InputDevice* section configures a specific device, such as a keyboard or mouse, as in this example:

```
```
Section  "InputDevice"
    Identifier  "Keyboard0"
    Driver      "kbd"

    Option      "XkbModel"  "pc105"
    Option      "XkbLayout" "us"
EndSection
Section  "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Protocol"  "IMPS/2"
    Option      "Device"  "/dev/input/mice"
    Option      "ZAxisMapping" "4 5"
    Option      "Emulate3Buttons" "yes"
EndSection
```
```

You can configure multiple devices, and there might be multiple InputDevice sections. The preceding example specifies a basic keyboard and a two-button PS/2 mouse (actually, a Dell touchpad pointer). An InputDevice section that specifies use of a USB device could be used at the same time (to enable mousing with PS/2 and USB pointers) and might look like this:

```
```
Section  "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Device"  "/dev/input/mice"
    Option      "Protocol"  "IMPS/2"
    Option      "Emulate3Buttons" "off"
    Option      "ZAxisMapping" "4 5"
EndSection
```
```