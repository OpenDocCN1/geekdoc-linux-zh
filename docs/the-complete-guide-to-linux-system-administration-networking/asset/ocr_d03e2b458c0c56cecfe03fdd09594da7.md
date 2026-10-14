+   The system may have trouble identifying hardware on your system that was not detected during the installation process. In this case it may help to specify information about the hardware via a boot parameter. The boot manager starts the Linux kernel with this parameter attached. These parameters are used both to affect how Linux recognizes hardware devices, and to alter the enabled features of the operating system.

# The Graphical Interface Doesn't Work

Sometimes the graphical interface doesn't work even though the installation program appears to detect your video hardware without a complaint. In this case, you probably selected a color depth or resolution that is not supported by the Linux driver. This can be true even if higher resolutions are supported on Windows—the Linux driver may still be in development or the developers lack critical technical information to make the video card perform to its capabilities.

Some video cards that are not supported by XFree86 are supported by commercial X Window System products that you can purchase and add to your Linux system after installing Linux. One such server is available from Xi Graphics (see www.xig.com). In the rare case that your card is not supported by any of these products, you can only use Linux in text mode. This is typical for many server installations, but if you want to use a graphical desktop, you need to invest in a different video card.

# A Device or Part of Memory Isn't Available

Sometimes hardware that is included on the list of supported hardware on the Linux vendor's Web site is nevertheless not available after starting Linux. This is often because the hardware is not correctly configured. As with a system that won't boot, the configuration can sometimes be corrected by adding a boot parameter when starting Linux. For example, some computers running Linux cannot access the CD-ROM drive correctly unless the device name is added as a boot parameter, like this:

```
linux cdrom=/dev/hdc
```

Or, Linux may not access all of the available system RAM because of limitations in the computer's BIOS. (The free command displays the amount of memory available to Linux.) You can tell Linux the amount of RAM on the system using this format:

```
linux mem==<amount of memory>>M
```

So to indicate 512 MB of RAM, you use the following command:

```
linux mem=512M
```

Be sure to use the correct value for the amount of RAM on your computer, or Linux crashes as it tries to work with nonexistent memory.