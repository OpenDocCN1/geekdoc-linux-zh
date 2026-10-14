# Configuration in the X Window System

If you have installed and configured the X Window System (package `xf86`) and Tcl/Tk (package `tcl` and package `tk`), you can use `make xconfig` as an alternative. You will be presented with a GUI (Graphical User Interface) that makes kernel configuration very user-friendly. You should have started the X Window System as root or you will have to take additional steps like taking over the display from another user.

# Settings in the Kernel Configuration

All the kernel’s configuration options cannot be covered here in detail. Make use of the numerous help texts available on kernel configuration. The latest kernel documentation is always in `/usr/src/linux/Documentation`.

# Compiling the Kernel

> > **Tip**
> >
> > You may remove the comment sign `#` in the main Makefile (approximately line 92). That is the line containing `EXPORT_INSTALL_PATH=/boot`. This lets you install your own kernel to `/boot`.

We recommend compiling a “bzImage”. As a rule, this avoids the problem of the kernel getting too large, as can easily happen if you select too many features and create a “zImage”. You will then get error messages like “kernel too big” or “System is too big”.

After customizing the kernel configuration, start compilation by entering:

```
earth:/usr/src/linux # make dep
earth:/usr/src/linux # make clean
earth:/usr/src/linux # make bzImage
```

These three commands can be entered on one line as well. They are started one after the other. This might be useful for compiling a kernel overnight, for example. Just enter:

```
earth:/usr/src/linux # make dep clean bzImage
```

Depending on your system, it will take a few minutes for the kernel to recompile. During the compilation, you can still work on one of the other consoles.