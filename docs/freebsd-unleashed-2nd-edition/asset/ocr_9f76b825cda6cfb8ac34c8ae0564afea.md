* **Option** "NoPM"—This option will disable some events that relate to power management. By default, power management is enabled on systems that can support it. You should need to add this option only if you are experiencing strange problems that seem to be related to power-management events.

A few other options can be included in this section, but they are less commonly used. If you are interested in some of the other options available, see the man page for XF86Config.

# Section “InputDevice”

This section is where the input devices are configured. There can be multiple **InputDevice** sections in the configuration file. Usually there will be at least two: one for the keyboard and one for the mouse or other pointing device.

**InputDevice** sections have several keywords associated with them. The first is the **Identifier** keyword. It is followed by a name that identifies this device. X-Windows doesn’t really care what you call the device, but it is best to use a descriptive name that defines the device.

The second is the **Driver** keyword. It is followed by the name of the driver for this device, in quotes. The most common drivers are “keyboard” and “mouse”, but there are a few others such as “microtouch” for a touch screen.

The final part of the **InputDevice** section consists of options for the device.

The following sections look at the two most common **InputDevice** sections—the keyboard and the mouse—and discuss some of the option lines available for configuring them.

# Configuring the Keyboard Options

Here is an example of the first part of the **InputDevice** section for the keyboard:

```
Section “InputDevice”
    Identifier     “Keyboard1”
    Driver        “Keyboard”
```

You can choose from a number of available options for controlling keyboard behavior. Here are some of the most commonly used of these options:

+   * **Option** “Protocol”—If this option is omitted or commented out, the default value of “standard” will be used. There is probably no reason to change this.
+   * **Option** “AutoRepeat” “x y”—This option controls the repeat rate of the keys on the keyboard. The number represented by $x$ is the delay in milliseconds before the key starts repeating. The number represented by $y$ is the number of times the key will repeat each second.