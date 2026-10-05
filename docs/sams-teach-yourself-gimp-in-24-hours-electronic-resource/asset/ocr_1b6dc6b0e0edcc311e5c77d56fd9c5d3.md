# Using Peripherals with Linux

```
EndSection
SubSection "WacomEraser"
Port "/dev/ttyS0"
DeviceName "EraserCore"
Mode Absolute
AlwaysCore
Suppress 15
EndSection
EndSection
```

Of course, this might need a little tweaking from the example listed here, and the device setting will depend on how your device is set up. If you are using one of the pens that shares a PS/2 port with your mouse, /dev/mouse should be a safe bet. Likewise, if it uses a dedicated serial port (recommended), you will need to use /dev/ttyS0.

After this is in place, you will need to make sure that the GIMP supports Xinput. (The latest releases of GTK have this built in.) You can grab patches for GTK here: http://www.gtk.org/-atoylar/xinput/patches.html. You will need to recompile GIMP after applying the patches.

![](bbox=[0.864, 0.363, 0.971, 0.433])

# A Word About Video Editing

Video editing in the GIMP is now in its infantile stages, but it does promise to be quite a powerful feature in future releases. Nonetheless, you can get started playing with video now—with a few tweaks.

As of yet, you cannot use the ATI All-In-Wonder card with Linux, although there is work being done on this. Stay tuned, this could change pretty quickly.

There is right now another developmental branch of GIMP that is singularly dedicated to further improving interoperability with the GIMP and professional video editing equipment. This series is not yet ready for prime time, but if you are so inclined, you can learn more about it at http://film.gimp.org.

# Summary

Using peripherals in order to help acquire and manipulate graphics with Linux is usually not a difficult task, but it can be a process that require a little digging. Sometimes certain devices (especially scanners) might have support from specific software packages. Some of them are only commercially supported. Any good Linux resource or