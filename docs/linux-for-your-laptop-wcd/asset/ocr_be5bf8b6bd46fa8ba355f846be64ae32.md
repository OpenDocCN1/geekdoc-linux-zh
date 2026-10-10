```
#
#id:5:initdefault:
...
```

This example shows that the default runlevel has been set to 5, or multiuser X11 mode.

# Not All Distributions Are Alike!

Note that other Linux distributions, especially SUSE Linux, do not use the same runlevel configuration as Red Hat-based distributions. This means that the values in the `/etc/initab` file might be different, depending on the type of Linux distribution installed on your notebook. SUSE Linux, for example, uses runlevel 3 as multiuser mode with X11.

Here is the pertinent line in `/etc/initab` that launches your X11 login screen:

```
# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodademon
```

This example shows Red Hat’s default entry. If you prefer to use the K Desktop Environment’s K display manager (kdm), you can use an entry that looks like this:

```
# Run xdm in runlevel 5
# xdm is now a separate service
# x:5:respawn:/etc/X11/prefdm -nodademon
x:5:respawn:/usr/bin/kdm -nodademon
```

This example forces Linux to launch the kdm client for your X11 session login.

# Using Different Resolutions

Ideally, you should have a screen resolution of 1024×768 pixels when using X11. This is because some X11 clients, such as `xfix`, `xboing`, `xmahjongg`, and others, require that screen size. However, until recently, the majority of notebooks sold featured maximum resolutions of 800×600. Some mini-notebooks, such as the Sony C-1X series, provide 1024×480, or a half-size XGA screen, but most mid- and even lower-priced notebooks today support larger displays. Higher-end notebooks provide surprisingly good LCD displays up to 1280×1024. The largest display (SXGA+) currently available from Dell and IBM top out at a whopping 1400×1050!