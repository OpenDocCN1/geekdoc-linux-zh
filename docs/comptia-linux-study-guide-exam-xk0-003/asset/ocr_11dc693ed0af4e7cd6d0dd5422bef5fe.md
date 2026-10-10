# 22 Chapter 1 · Getting Started with Linux

If you have a working configuration, be sure to back up xorg.conf before modifying it. If you mistakenly delete or modify some critical line, you can easily end up with a system that won’t start X, and without a backup, it can be difficult to restore even a partially functioning system.

Many xorg.conf sections include Identifier, Mode1Name, VendorName, or BoardName lines. The Identifier provides a name for the section that can be used by other sections to refer to the first one. The Mode1Name, VendorName, or BoardName line, if present, is intended for human consumption, so you can put anything there you like. A Driver line, by contrast, points X to a driver for the device. This is extremely important, so you shouldn’t change it unless you’re positive that the current entry is wrong.

# Setting Miscellaneous Options

Some sections of the xorg.conf file relate to miscellaneous options or those that require just a handful of lines. Nonetheless, getting these settings right is important to a functioning X system. Specific sections in this category include the following:

**Files** The Files section hosts information on the locations of important files. The entries you’re most likely to change relate to the locations of X’s fonts. These are handled through the FontPath option line. Modern distributions often omit this section and instead rely on default settings. If you need to add fonts to your system, though, you may need to add FontPath entries that point to your existing and new font directories.

**The keyboard** One InputDevice section defines the operation of the keyboard in X. This section normally has a Driver “kbd” line. In most cases, the default settings (or those set automatically based on your install-time choices) work fine. You may want to adjust the XkbLayout option or XkbMode1 option to use a different layout or model if these features were set incorrectly. The AutoRepeat option sets the delay before keyboard repeat begins and the repeat rate, both in milliseconds (thousandths of a second). This feature is usually overridden in desktop environment configurations, so it may not have any practical effect.

**The mouse** A second InputDevice section, with a Driver “mouse” line, defines the mouse. The default settings autodetect the mouse, which works for the vast majority of PS/2 and USB mice. If you use a particularly obscure model, you may need to set Protooel and Device options, as in Option “Logitech” or Option “Device” /dev/ttyS1.

X programs frequently use the middle button; for instance, text editors use it for pasting text. Therefore, any Linux workstation should be equipped with a genuine three-button mouse rather than a two-button device. Scroll wheels on mice that are so equipped can usually function as a middle button, as well as handling wheel duty. The Option “Emulate3Buttons” 'yes' option enables you to use a two-button mouse in Linux, but doing so is awkward.