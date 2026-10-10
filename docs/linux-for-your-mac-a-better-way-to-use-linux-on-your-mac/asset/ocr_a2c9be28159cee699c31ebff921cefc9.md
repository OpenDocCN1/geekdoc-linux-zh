Yet another way to configure X is to boot Linux using proper base video values, and then use a graphical configuration client that starts a "safe" X session. These video values are kernel arguments passed to the Linux kernel by BootX or yaBoot, and generally take the form:

```
video=adapter:vmode:XX,cmode:XX
```

The `adapter` keyword (such as `ayfb`) denotes the type of graphics chipset used. The `vmode` setting is a one- or two-digit value (in the range of 1-20) that corresponds to a resolution. The `cmode` setting is a one- or two-digit value (8, 15, 16, 24, or 32) that corresponds to a color depth. These video settings may also be accomplished after Linux boots by using the `fbset` command.

You can also use XFree86 version 4.0's (or newer) X server to configure settings. And if all else fails, you can manually create your own configuration file (because it is a text file).

> It is generally not a good idea to use someone else's `XF86Config` file unless you use it for a matching video card and monitor combination. iBook and PowerBook users can share configuration files between same model notebooks.

![](bbox=[0.86, 0.45, 0.98, 0.54])

If you craft your own `XF86Config` file, there is a template file named `XF86Config.eg` located under the `/usr/X11R6/lib/X11` directory (you can read the sample for example entries). Manually creating your own `XF86Config` file can be challenging if you are new to X!

# Using the xf86config Command

The `xf86config` command is a text-based console application included with XFree86 and every Linux distribution. It can be used to configure a working `XF86Config` file. This command is a menu-driven program that uses various databases of monitors and video cards, which are installed under the `/usr/X11R6/lib/X11` directory to provide choices during the configuration process. You must be the root operator in order to configure X to work with your system. Start the `xf86config` command like this:

```
# xf86config
```

After you press Enter, you will start answering questions to configure X. You will be asked about your pointing device (mouse), keyboard, monitor, video card, desired color depth, and desired resolution. Be sure to have your equipment's manuals on hand, along with technical specifications for your graphics hardware, pointing device, and monitor.